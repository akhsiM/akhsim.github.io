---
title: Django User Management
layout: post-toc
tags: software backend python 
---

# Model Permissions

When a model is created, Django automatically creates four default permissions for four actions:
- ~add~: To add an instance of the model.
- ~delete~: To delete an instance of the model.
- ~change~: To update an instance of the model.
- ~view~: To view instances of the model.

Permission names follow this naming convention: ~<app>.<action>_<modelname>~.

For example, the name of the permission to change a user is ~auth.change_user~.

## Checking Model Permissions

Model Permissions are granted to users or groups. To check if a user has a certain permission, we can do:

```
>>> from django.contrib.auth.models import User
>>> u = User.objects.create_user(username='kenny')
>>> u.has_perm('auth.change_user')
False
```

~.has_perm()~ will always return ~True~ for active superuser even if the permission doesn't really exist. What this means is when we are checking permissions for a superuser, the permissions are not really being checked.

## Enforce Permissions

Django models don't enforce permissions themselves. The only place where permissions are enforced out of the box is Django Admin.

In Django apps, the user is normally obtained from the request. Therefore most of the times, if permissions are needed, they would be enforced at *view layer*. 

### at the View layer

For example, we can prevent a user without view permission to access a view that shows other user information by:
```python
from django.core.exceptions import PermissionDenied

def users_list_view(request):
	if not request.user.has_perm('auth_view_user'):
		raise PermissionDenied()
```

If the user has not logged in, ~request.user~ would be an instance of ~AnonymousUser~, which is a Django special object. Using ~has_perm()~ on ~AnonymousUser~ will always return ~False~.

If the user making the request doesn't have the ~view_user~ permission, the ~PermissionDenied~ exception would be raised and a response 403 is returned to the client.

#### using decorator

There is a shortcut decorator that we can use for the same thing:
```python
from django.contrib.auth.decorators import permission_required

@permission_required('auth.view_user')
def users_list_view(request):
	pass
```

### at the Template layer

We can also enforce permissions in templates through a special template variable called *perms*. For example, if we want to show the delete button only to users with delete permission:

```html
{% if perms.auth.delete_user %}
<button>Delete User</button>
{% endif %}
```
### in Django Admin

Django-admin has a very tight integration with the built-in authentication system and model permissions. On default Django-admin enforces model permissions:
- If the user has no permission on a model, they wouldn't be able to see or access it in the admin.
- If the user has view and change permission on a model, they will be able to view and update instances but won't be able to add new or delete existing ones.

# Implement Custom Business Roles in Django-Admin

One of the most vulnerable places in every app is the authentication system. This is the ~User~ model in a Django app. Therefore, to protect our app, we need to start with the ~User~ model.

First, we need to take control over the ~User~ model admin page by extending the built-in ~User~ admin model and make your own Custom User Admin.

## A Custom User Admin

We first need to unregister the existing model admin provided by Django, and then register our own:
```python
from django.contrib import admin
from django.contrib.auth.models import User
from django.contrib.auth.admin import UserAdmin

# Unregister the OOTB modeladmin
admin.site.unregister(User)

# Register our own modeladmin, based on the default UserADmin
@admin.register(User)
class CustomUserAdmin(UserAdmin):
	pass
```

By extending Django's ~UserAdmin~ we take advantage of all the work already done by the Django developer.

## Prevent Update of Fields

We can prevent admin users from modifying certain fields in the model.

If we want to prevent any users, including superusers from updating a field, we can mark the field as read-only.

```python
from django.contrib import admin
from django.contrib.auth.models import User
from django.contrib.auth.admin import UserAdmin

@admin.register(User):
class CustomUserAdmin(UserAdmin):
	readonly_fields = [
		'date_joined',
	]
```

### ..conditionally

We can also *conditionally* prevent update of fields.

Let's say we want to prevent non-superusers from being able to changing a user's username.

```python
from django.contrib import admin
from django.contrib.auth.models import User
from django.contrib.auth.admin import UserAdmin

@admin.register(User)
class CustomUserAdmin(UserAdmin):
    def get_form(self, request, obj=None, **kwargs):
        form = super().get_form(request, obj, **kwargs)
        is_superuser = request.user.is_superuser

        if not is_superuser:
            form.base_fields['username'].disabled = True

        return form

```

- We override the ~get_form()~ method. This function is used by Django to generate a default change form for a model.
- In order to conditionally disabled the field, we first fetch the default form generated by Django, then apply the condition, disabling the ~username~ field.

## Prevent Non-Superusers from granting superuser rights

Superuser is a very strong permission that should not be granted lightly. However on default *any user with a change permission on the ~User~ model can make any user a superuser, including themselves*. Therefore we want to close this hole.

```python
from typing import Set

from django.contrib import admin
from django.contrib.auth.models import User
from django.contrib.auth.admin import UserAdmin

@admin.site.register(User)
class CustomUserAdmin(UserAdmin):
	def get_form(self, request, obj=None, **kwargs):
		form = super.get_form(request, obj, **kwargs):
		is_superuser = request.user.is_superuser
		disabled_fields = set()

		if not is_superuser:
			disabled_fields |= {
				'username',
				'is_superuser',
			}

		for f in disabled_fields:
			if f in form.base_fields:
				form.base_fields[f].disabled = True

		return form
				
```

- We intialized an empty set ~disabled_fields~ that will hold the fields to disable. ~set~ is a data structure that holds *unique values*. It makes sense to use a set in this case because we only need to disable a field once.
- The operator ~|=~ is used to perform an in-place *or* update.
- Then we apply the condition. If ther user is not superuser, we add two fields to the set. 
- Lastly we iterate over the fields in the set and mark all of them as disabled, then return the form.
### Django User Admin Two-Step Form

When we create a new user in Django-admin, we go through a two-step form. In the first form we fill in the username and password. In the second form, we update the rest of the fields.

This two-step process is unique to the ~User~ model. In order to accomodate this unique process, we need to verify that the field exists before we disable it. Otherwise we would get a ~KeyError~.
## Grant Permissions Only Using Groups

The way permissions are managed is specific to each team/ organization. However it's easier to manage permissions in groups. Grouping permissions together makes life easier rather than trying to manage them at individual user level.

To manage permissions only using groups, we need to *prevent users from granting permissions to specific users*. Instead we *only* want to allow associating useres to groups. To do that we have to disable the field ~user_permissions~ for all non-superusers.

```python
from typing import Set

from django.contrib import admin
from django.contrib.auth.models import User
from django.contrib.auth.admin import UserAdmin

@admin.register(User)
class CustomUserAdmin(UserAdmin):
    def get_form(self, request, obj=None, **kwargs):
        form = super().get_form(request, obj, **kwargs)
        is_superuser = request.user.is_superuser
        disabled_fields = set()  # type: Set[str]

        if not is_superuser:
            disabled_fields |= {
                'username',
                'is_superuser',
                'user_permissions',
            }

        for f in disabled_fields:
            if f in form.base_fields:
                form.base_fields[f].disabled = True

        return form

```

## Prevent Non-Super-Users from editing their own permissions

Strong users are often a weak spot of the system. Users who possess strong permissions have the potential to cause significant damage. To prevent this, we can prevent users from editing their own permissions:

```python
from typing import Set

from django.contrib import admin
from django.contrib.auth.models import User
from django.contrib.auth.admin import UserAdmin

@admin.register(User)
class CustomUserAdmin(UserAdmin):
    def get_form(self, request, obj=None, **kwargs):
        form = super().get_form(request, obj, **kwargs)
        is_superuser = request.user.is_superuser
        disabled_fields = set()  # type: Set[str]

        if not is_superuser:
            disabled_fields |= {
                'username',
                'is_superuser',
                'user_permissions',
            }

        # Prevent non-superusers from editing their own permissions
        if (
            not is_superuser
            and obj is not None
            and obj == request.user
        ):
            disabled_fields |= {
                'is_staff',
                'is_superuser',
                'groups',
                'user_permissions',
            }

        for f in disabled_fields:
            if f in form.base_fields:
                form.base_fields[f].disabled = True

        return form

```

- The argument ~obj~ is the instance of the object that is currently being edited:
  - When ~obj is None~, the form is being used to create a new user.
  - When ~obj is not None~, the form is being used to edit an existing user.

- To check if the user making the request is operating on themselves, we can compare ~request.user~ with ~obj~. 
- The ability to customize the form based on the ~obj~ is very useful. We can use this to implement elaborate business roles.

## Override Permissions

Sometimes it can be useful to completely override the permissions in Django admin. A common scenario is when you use permissions in other place and you don't want staff users to make changes in the admin.

In order to implement the four built-in permissions, Django uses *hooks*. Internally, these hooks use the current user's permissions to make a decision. However we can override these hooks and provide a different decision.

To prevent staff users from deleting a model instance, regardless of their permissions, we can do the following:

```python
from django.contrib import admin
from django.contrib.auth.models import User
from django.contrib.auth.admin import UserAdmin

@admin.register(User)
class CustomUserAdmin(UserAdmin):
    def has_delete_permission(self, request, obj=None):
        return False
```

## Restrict Access to Custom Actions

*Custom Admin Actions* requires special attention. As Django is not familiar with them, it cannot restrict them by default. Out of the box, a custom action will be accessible to any admin user with any permission on the model.

For example, let's say we have a custom admin action to mark multiple userse as active:
```python
from django.contrib import admin
from django.contrib.auth.models import User
from django.contrib.auth.admin import UserAdmin

@admin.register(User)
class CustomUserAdmin(UserAdmin):
	actions = [
		'activate_users',
	]

	def activate_users(self, request, queryset):
		cnt = queryset.filter(is_active=False).update(is_active=True)
		self.message_user(request, 'Activated {} users.'.format(cnt))
	activate_users.short_description = 'Activate users'
```

This custom action updates user information, so we only want users with change permissions to be able to use it. Because it's a custom user action though, any person with access to django-admin and useradmin interface can use it. Therefore we need to hide ~activate_users()~ from users without user change permission by overriding ~get_actions()~.

```python
from django.contrib import admin
from django.contrib.auth.models import User
from django.contrib.auth.admin import UserAdmin

@admin.register(User)
class CustomUserAdmin(UserAdmin):
	actions = [
		'activate_users',
	]

	def activate_users(self, request, queryset):
		cnt = queryset.filter(is_active=False).update(is_active=True)
		self.message_user(request, 'Activated {} users.'.format(cnt))
	activate_users.short_description = 'Activate users'

	def get_actions(self, request):
		actions = super().get_actions(request)
		if not request.user.has_perm('auth.change_user'):
			del actions['activate_users']
		return actions
```

~get_actions()~ is the default Django function that returns an ~OrderedDict~. Within this dict, each object has a key which is just the name of the action, as well as the value being the actual function being called. In order to adjust the return value, we override the function, fetch the original dict with ~super()~, and conditionally remove the custom action ~activate_users~ from the dict.
