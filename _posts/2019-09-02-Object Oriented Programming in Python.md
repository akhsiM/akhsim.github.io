---
title: Classes in Python | Python Object Oriented Programming
layout: post-toc
tags: python programming
---

## Introduction
### What is OOP?

Object-oriented Programming (OOP) is a programming paradigm which provides a means of structuring programs so that properties and behaviours are bundled into individual *objects*.

For example, an object would represent an employee with given name, last name, salary.

OOP is different to, for example, procedural programming which structures program like a recipe in that it provides a set of steps in the form of functions and code blocks that flow sequentially in order to complete a task. In OOP, *objects are at the center* of programming as it does not only represent the data (like PP) but also the overall structure and blueprint of the program.

Python is a multi-paradigm programming language. OOP is one of the paradigms that best suits the problem at hand. In a program, multiple paradigms can be used and mixed between each others.
### Syntax

```python
class User:
	pass

user = User()
user.first_name = 'Bruce'
user.last_name = 'Lee'
print(user.first_name, user.last_name)
```

```
: Bruce Lee

#+Name: PEP8 style guide for class object naming
#+begin_quote
"..lowercase with words seperated by underscores as necessary to improve readability.."
```


```python
class User:
	pass

user2 = User() 
user2.first_name = 'Bruce'
user2.last_name = 'Lee'

first_name = 'Hello'
last_name = 'World'

print(user2.first_name, user2.last_name)
print(first_name, last_name)

user1 = User()
user1.first_name = 'Clark'
user1.last_name = 'Kent'
print(user1.first_name, user1.last_name)
```

```
: Bruce Lee
: Hello World
: Clark Kent
```

### Why should we use Classes?

Classes allow us to logically group our data and functions in a way that's easily to reuse and to build upon (if need be).

### Difference between a Class and an instance of a class

A Class is like a blueprint of objects of a similar type.

An instance of a Class is an object with the blueprint that is the Class. Any instance of the class is a unique instance with unique attributes.

## The `init` method

A method is a function inside a class.

The init method is called everytime a new instance of the class is initiated. In some other languages, the init method is called the *constructor*.

`self` should always be the *first* argument, which is reference to the object being created.

```python
class User:
	def __init__(self, full_name, birthday):
	# Assign the init arguments to the initiating object.
		self.name = full_name
		self.birthday = birthday
	
	# extract first and lastname
		name_pieces = full_name.split(' ')
		self.gvn = name_pieces[0]
		self.sn = name_pieces[-1]
user = User('Bruce Lee', '31031983')
print(user.name)
print(user.sn, user.gvn) 
 ```

```
: Bruce Lee
: Lee Bruce
```

**Note**: In the above example, the only valid attributes of the class User upon init are `name, birthday, gvn, sn`. These are the variables that have been assigned to `self`. Calling any other attributes that have not been assigned to `self` would result in an `AttributeError`.

## The docstring

```python
class User:
	""" This is a docstring, They are pretty useful.
We should always write this."""
	pass

help(User)
```

The docstring is displayed when running help(`class`) command.
## Calling a method
### Syntax
```python
class Employee:
	def __init__(self, first_name, last_name, pay):
		self.gvn = first_name
		self.sn = last_name
		self.pay = pay
		self.email = first_name + '.' + last_name + '@company.com'
	
	def fullname(self):
		return '{} {}'.format(self.gvn, self.sn)

employee1 = Employee('Bruce', 'Lee', 50000)

print(employee1.gvn)

print(employee1.fullname())
```

```
: Bruce
: Bruce Lee
```

### Calling the class method directly

```python
class Employee:
	def __init__(self, first_name, last_name, pay):
		self.gvn = first_name
		self.sn = last_name
		self.pay = pay
		self.email = first_name + '.' + last_name + '@company.com'
	
	def fullname(self):
		return '{} {}'.format(self.gvn, self.sn)

employee1 = Employee('Bruce', 'Lee', 50000)

print(employee1.fullname())
# These are the same
print(Employee.fullname(employee1))
```

```
: Bruce Lee
: Bruce Lee
```

Calling a method on the class instead of on the instance provides the same result, however calling the Class requires us to type the name of the instance into the argument.

This explains the `self` argument, which is automatically placed as an argument whenever you invoke a method from an instance of a class.

### The `self` argument

Don't forget to use the `self` argument. Without this, althougth the class creation would have no problem, when we call the actual method, there would be an error message. Although it looks like no argument is passed, the instance argument is passed *automatically* when the method is called.

```python
class Employee:
	def __init__(self, first_name, last_name, pay):
		self.gvn = first_name
		self.sn = last_name
		self.pay = pay
		self.email = first_name + '.' + last_name + '@company.com'
	
	def fullname():
		return '{} {}'.format(self.gvn, self.sn)

employee1 = Employee('Bruce', 'Lee', 50000)

print(employee1.fullname())

```

```
: Traceback (most recent call last):
:   File "<stdin>", line 1, in <module>
:   File "/tmp/babel-10144YHR/python-10144Osv", line 13, in <module>
:     print(employee1.fullname())
: TypeError: fullname() takes 0 positional arguments but 1 was given
```

## Methods

Regular methods in a class automatically takes the instance as the first argument in the method call. (See [[self][self]])

### Class Methods

- Class method definition is preceded by the `@classmethod` decorator.
- Instead of `self`, we can specify the class variable by using `cls`. 

Class methods are similar to other instance methods (e.g `__init__`) in a class. However instead of having the `self` instance passed as the first argument to it, class methods' first argument is the actual *uninstantiated* class itself (`cls`).

#### Example 1 - Set new Pay Raise amount
```python
class Employee:
	pay_raise_amt = 1.04

	def __init__(self, first_name, last_name, pay):
		self.gvn = first_name
		self.sn = last_name
		self.pay = pay
		self.email = first_name + '.' + last_name + '@company.com'

	@classmethod
	def set_new_raise_amt(cls, amount):
		cls.pay_raise_amt = amount

employee1 = Employee('Bruce', 'Lee', 50000)
employee2 = Employee('Manny', 'Pacquiao', 500000)

print(Employee.pay_raise_amt)
Employee.set_new_raise_amt(1.05)
print(employee1.pay_raise_amt) 
print(employee2.pay_raise_amt)	
	
```

```
: 1.04
: 1.05
: 1.05
```

#### Example 2 - Alternative constructor

This is an example of *alternative constructor*.

The aim is to be able to instantiate an object from a simple string, with the properties seperated by a dash.
```python
class Employee:
	pay_raise_amt = 1.04

	def __init__(self, first_name, last_name, pay):
		self.gvn = first_name
		self.sn = last_name
		self.pay = pay
		self.email = first_name + '.' + last_name + '@company.com'

	@classmethod
	def from_string(cls, emp_str):
		first, last, pay = emp_str.split('-')
		return cls(first, last, pay)

emp_str = 'Bruce-Lee-50000'
employee1 = Employee.from_string(emp_str)

print(employee1.email)		
```

```
: Bruce.Lee@company.com
```

### Static Method

Instead of passing the instance (`self`) or the class (`cls`) as an argument to the method, a static method does not pass anything on default.

They behave just like regular function however they are organised in the class because they have a logical connection to the class. They essentially know nothing about the class.

Static methods definition is preceded by the `@staticmethod` decorator:
```python
import datetime
class Employee:
	pay_raise_amt = 1.04

	def __init__(self, first_name, last_name, pay):
		self.gvn = first_name
		self.sn = last_name
		self.pay = pay
		self.email = first_name + '.' + last_name + '@company.com'
	
	@staticmethod
	def is_workday(day):
		if day.weekday() > 4:
			return False
		return True

print(Employee.is_workday(datetime.date(2019, 9, 3)))
		
	
```

```
: True
```

### Difference between `@classmethod` and `@staticmethod`

*Similarities*:
- Both are callable functions that are defined inside a class.
- Both do not require a class object to be instanstiated. /(Unlike instance methods, which operate on an object)/

*Differences*:
- Class methods work with the class and has access to class variables. Its first parameter must always be the (uninstantiated) class.

- Static methods do not work with the class and knows nothing about the class. It only has some logical connection to the class, like a helper method, but do not interact with any specific instance.
- Static method definition is immutable via inheritance.

## Special (Magic | Dunder) Methods

### Introduction

Magic methods in Python are special methods that are not invoked by us howver the invocation happens internally from the class on a certain action.

Built-in classes in Python define many magic methods. This can be retrieved by `dir()` function. 
```python
print(dir(int))
print()
x = 10
print((x + 10))
print((x.__add__(10)))
print(repr(x))
```

```
: ['__abs__', '__add__', '__and__', '__bool__', '__ceil__', '__class__', '__delattr__', '__dir__', '__divmod__', '__doc__', '__eq__', '__float__', '__floor__', '__floordiv__', '__format__', '__ge__', '__getattribute__', '__getnewargs__', '__gt__', '__hash__', '__index__', '__init__', '__init_subclass__', '__int__', '__invert__', '__le__', '__lshift__', '__lt__', '__mod__', '__mul__', '__ne__', '__neg__', '__new__', '__or__', '__pos__', '__pow__', '__radd__', '__rand__', '__rdivmod__', '__reduce__', '__reduce_ex__', '__repr__', '__rfloordiv__', '__rlshift__', '__rmod__', '__rmul__', '__ror__', '__round__', '__rpow__', '__rrshift__', '__rshift__', '__rsub__', '__rtruediv__', '__rxor__', '__setattr__', '__sizeof__', '__str__', '__sub__', '__subclasshook__', '__truediv__', '__trunc__', '__xor__', 'bit_length', 'conjugate', 'denominator', 'from_bytes', 'imag', 'numerator', 'real', 'to_bytes']
: 
: 20
: 20
: 10
```

From the above, when we does `+`, the operator actually calls the `__add__` method. Variable assignment invokes the `__new__` method.

This is why the same operator, i.e `+`, perform different operations for strings and integers. 

Special methods are always surrounded by double underscores `__`. These are called *Dunder*. For example, `__init__` is called "Dunder init".

The three most common methods are `__repr__`, `__str__` and `__init__` methods.

### Using the Dunder repr method

According to the official Python documentation, `_repr__` is a built-in function used to compute the "official" string reputation of an object, while `__str__` is a built-in function that computes the "informal" string representations of an object.


```python
class Employee:
	pay_raise_amt = 1.04

	def __init__(self, first_name, last_name, pay):
		self.gvn = first_name
		self.sn = last_name
		self.pay = pay
		self.email = first_name + '.' + last_name + '@company.com'

emp1 = Employee('Bruce', 'Lee', 50000)

print(emp1)
```

```
: <__main__.Employee object at 0x7f8204872f28>
```

```python
class Employee:
	pay_raise_amt = 1.04

	def __init__(self, first_name, last_name, pay):
		self.gvn = first_name
		self.sn = last_name
		self.pay = pay
		self.email = first_name + '.' + last_name + '@company.com'
	
	def __repr__(self):
			return "Employee('{}', '{}', {})".format(self.gvn, self.sn, self.pay)

emp1 = Employee('Bruce', 'Lee', 50000)

print(emp1)
```

``` With the Dunder repr method:
: Employee('Bruce', 'Lee', 50000)

#+Name: With the Dunder repr and str method:
```python
class Employee:
	pay_raise_amt = 1.04

	def __init__(self, first_name, last_name, pay):
		self.gvn = first_name
		self.sn = last_name
		self.pay = pay
		self.email = first_name + '.' + last_name + '@company.com'
	
	def __repr__(self):
		return "Employee('{}', '{}', {})".format(self.gvn, self.sn, self.pay)
	
	def __str__(self):
		return '{} - {}'.format((self.gvn + ' ' + self.sn), self.email)

emp1 = Employee('Bruce', 'Lee', 50000)

print(emp1)
print()
print(repr(emp1))
print(str(emp1))
```

```
: Bruce Lee - Bruce.Lee@company.com
: 
: Employee('Bruce', 'Lee', 50000)
: Bruce Lee - Bruce.Lee@company.com
```

#### More about repr method

The `repr` method takes a single parameter `Obj` whose printable representation is to be returned.

The return value is a printable representational string of the given object.

The returned string would yield an object with the same value when passed to `eval()`.

```python
eval(repr(obj)) == object
```

What is the difference between `repr()` and `str()?`

(More on this topic: https://stackoverflow.com/questions/1436703/difference-betw```
een-str-and-repr)

### Using the Dunder add method

```python
print(1 + 2)
print(int.__add__(1, 2))
print((1 + 2) == int.__add__(1, 2))
```

```
: 3
: 3
: True
```

We can customize how the operator `+` works by the use of Dunder add method.

```python
class Employee:
	pay_raise_amt = 1.04

	def __init__(self, first_name, last_name, pay):
		self.gvn = first_name
		self.sn = last_name
		self.pay = pay
		self.email = first_name + '.' + last_name + '@company.com'
	
	def __add__(self, other):
		return self.pay + other.pay

emp1 = Employee('Bruce', 'Lee', 50000)
emp2 = Employee('Jet', 'Li', 55000)

print(emp1 + emp2)
```

```
: 105000
```
More on this: https://docs.python.org/3.7/reference/datamodel.html?highlight=emulating%20numeric%20types
## Class Variables

Class variables are variables that are *shared* amongst all instances of the same class.

For example, with the class Employee, we'd like to share variables such as given name, last name, pay ..

```python
class Employee:
	pay_raise_amt = 1.04  ## This is a Class Variable

	def __init__(self, first_name, last_name, pay):
		self.gvn = first_name
		self.sn = last_name
		self.pay = pay
		self.email = first_name + '.' + last_name + '@company.com'
	
	def fullname(self):
		return '{} {}'.format(self.gvn, self.sn)

	def pay_raise(self):
		self.pay = int(self.pay * self.pay_raise_amt)

employee1 = Employee('Bruce', 'Lee', 100000)
print(employee1.__dict__)
employee1.pay_raise()
print(employee1.__dict__)

print('Accessing var from Instance:', employee1.pay_raise_amt)
print('Accessing var from Class:', Employee.pay_raise_amt)

Employee.pay_raise_amt = 1.10  ## Change Class Variable
print('New Class Variable is applied across all instances:', employee1.pay_raise_amt)

employee1.pay_raise_amt = 1.20
print('New Instance Variable:', employee1.pay_raise_amt)
print('Changing Instance Variable does nothing to the Class Variable', Employee.pay_raise_amt)
print(employee1.__dict__)
```

```
: {'gvn': 'Bruce', 'sn': 'Lee', 'pay': 100000, 'email': 'Bruce.Lee@company.com'}
: {'gvn': 'Bruce', 'sn': 'Lee', 'pay': 104000, 'email': 'Bruce.Lee@company.com'}
: Accessing var from Instance: 1.04
: Accessing var from Class: 1.04
: New Class Variable is applied across all instances: 1.1
: New Instance Variable: 1.2
: Changing Instance Variable does nothing to the Class Variable 1.1
: {'gvn': 'Bruce', 'sn': 'Lee', 'pay': 104000, 'email': 'Bruce.Lee@company.com', 'pay_raise_amt': 1.2}

Class variables can be accessed via both the Class (`Employee.pay_raise_amt`) or the Instance (`employee1.pay_raise_amt`).

Note how there is no `pay_raise_amt` in the `__dict()__` method call of the instance before the change to the variable. This is because after the change, `pay_raise_amt` was turned into an Instance Variable that exists in `employee1` which is seperate from the default Class Variable.
### Class Variable vs Instance Variable in method definition 

Note in the above snippet, there was this part:
```python
	def pay_raise(self):
		self.pay = int(self.pay * self.pay_raise_amt)
```

What it does is apply the `pay_raise_amt` of the Instance, not the Class variable. Unless a change to the instance variable was applied, the method `pay_raise` would use the fallback/ default Class variable value.

That can also be forced by typing this instead:

```python
	def pay_raise(self):
		self.pay = int(self.pay * Employee.pay_raise_amt)
```

## Class inheritance

Inheritance allows us to inherit class attributes from parent class. It is useful so that we can create *subclasses* that inherits from parent classes then we can also modify the subclasses without touching the parent classes.

```python
class Employee:
	pay_raise_amt = 1.04

	def __init__(self, first_name, last_name, pay):
		self.gvn = first_name
		self.sn = last_name
		self.pay = pay
		self.email = first_name + '.' + last_name + '@company.com'

	@classmethod
	def set_new_raise_amt(cls, amount):
		cls.pay_raise_amt = amount

class Developer(Employee):
	# inherit from Employee Class
	pass 

dev1 = Developer('Bruce', 'Lee', 50000)
print(dev1.email)	
```

```
: Bruce.Lee@company.com
```

### Modifying the subclass

#### Example 1: Simple change by invoking a method

Aim: Change the pay raise amount of Developer to 1.05 instead of 1.04.

```python
class Employee:
	pay_raise_amt = 1.04

	def __init__(self, first_name, last_name, pay):
		self.gvn = first_name
		self.sn = last_name
		self.pay = pay
		self.email = first_name + '.' + last_name + '@company.com'

	@classmethod
	def set_new_raise_amt(cls, amount):
		cls.pay_raise_amt = amount

class Developer(Employee):
	# inherit from Employee Class
	pass

Developer.set_new_raise_amt(1.05)  ## Changes Pay Raise amount for only Developer Class.

print(Employee.pay_raise_amt)  ## Unchanged
print(Developer.pay_raise_amt)
```

```
: 1.04
: 1.05
```

#### Example 2: More complicated change

Aim: Developer to have an init value for Programming Language.

```python
class Employee:
	pay_raise_amt = 1.04

	def __init__(self, first_name, last_name, pay):
		self.gvn = first_name
		self.sn = last_name
		self.pay = pay
		self.email = first_name + '.' + last_name + '@company.com'

	@classmethod
	def set_new_raise_amt(cls, amount):
		cls.pay_raise_amt = amount

class Developer(Employee):
	# inherit from Employee Class
	def __init__(self, first_name, last_name, pay, p_lang):
		# inherit the parent class init
		super().__init__(first_name, last_name, pay)
		# Doing this allows us to modify existing methods with minimal codechange i.e more maintainable
		# This also works:
		# Employee.__init__(self, first_name, last_name, pay)
		self.p_lang = p_lang

dev1 = Developer('Bruce', 'Lee', 50000, 'C++')
print(dev1.email)
print(dev1.p_lang)
```

```
: Bruce.Lee@company.com
: C++
```

#### Example 3: The Manager class

Aim: Create a class for Manager that also contains information about employees that he supervises.
```python
class Employee:
	pay_raise_amt = 1.04

	def __init__(self, first_name, last_name, pay):
		self.gvn = first_name
		self.sn = last_name
		self.pay = pay
		self.email = first_name + '.' + last_name + '@company.com'

	def fullname(self):
		return '{} {}'.format(self.gvn, self.sn)

class Manager(Employee):
	# Pass arguments for employees which the manager supervises
	def __init__(self, first_name, last_name, pay, employees=None):
		super().__init__(first_name, last_name, pay)
		if employees is None:
			self.employees = []
		else:
			self.employees = employees
		print ('Created new Manager', super().fullname())
	
	def add_emp(self, emp):
		if emp not in self.employees:

	def remove_emp(self, emp):
		if emp in self.employees:
			self.employees.remove(emp)

	def print_emps(self):
		for emp in self.employees:
			print('-->', emp.fullname())

mgr1 = Manager('Daniel', 'Smith', 100000)
mgr1.print_emps()

emp1 = Employee('Bruce', 'Lee', 50000)
emp2 = Employee('Jackie', 'Chan', 50000)

mgr2 = Manager('Jonathan', 'Pickle', 100000, [emp1, emp2])
mgr2.print_emps()
print()

mgr2.add_emp(Employee('Jet', 'Li', '55000'))
mgr2.print_emps()
```

```
: Created new Manager Daniel Smith
: Created new Manager Jonathan Pickle
: --> Bruce Lee
: --> Jackie Chan
: 
: --> Bruce Lee
: --> Jackie Chan
: --> Jet Li
```

### Checking subclass and instance

Python has 2 built-in functions for this.
- First argument = instance (or subclass)
- Second argument = class (or parent class)

```python
class Employee:
	pay_raise_amt = 1.04

	def __init__(self, first_name, last_name, pay):
		self.gvn = first_name
		self.sn = last_name
		self.pay = pay
		self.email = first_name + '.' + last_name + '@company.com'

	@classmethod
	def set_new_raise_amt(cls, amount):
		cls.pay_raise_amt = amount

class Developer(Employee):
	# inherit from Employee Class
	pass 

dev1 = Developer('test', 'test', 100000)

print(isinstance(dev1, Developer))
print(issubclass(Developer, Employee))
```

```
: True
: True
```

## Miscelanous 

### `dir` 

`dir` is a powerful in-built function of Python 3. It returns all properties and attributes of a class. These includes class attributes, methods, .etc. 

```python
dir(class)
dir(instance)
```

### `__dict__`

Every class has a `__dict__` method. It returns all variables of an instance.
Note that it does not return the default class variables.

### `help()`
Useful for reading docstring and properties. This can also be used to see inherited attributes.
   ```python
print(help(class))
print(help(instance))
```

### `super()`

`super()` alone returns a temporary object of the superclass. A super class is also known as a parent class. This allows us to invoke methods of the parent class, when working with a subclass.
