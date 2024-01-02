---
title: Python - High Order Function & Decorator
layout: post-toc
tags: python
---
# First-Class Functions & Higher Order Functions
	
## General introduction & Definition

In this article I am learning about Python decorators. However, it is important to grasp the concepts of first-class functions, higher-order functions before moving on to decorator. This is because "high-order function" is the underlying concept that engines the usage of decorator.

Let's note down some key concepts. I found these from various sources on the Internet. There are a lot of ways which the definitions can be stated, these are the simplest, the most ELI:

> When you say that a language has first-class functions, it means that the language treats functions as values – that you can assign a function into a variable, pass it around etc. Higher-order functions are functions that work on other functions, meaning that they take one or more functions as an argument and can also return a function.
> 
> The “higher-order” concept can be applied to functions in general, like functions in the mathematical sense. The “first-class” concept only has to do with functions in programming languages. It’s seldom used when referring to a function, such as “a first-class function”. It’s much more common to say that “a language has/hasn’t first-class function support”.
> 
> The two things are closely related, as it’s hard to imagine a language with first-class functions that would not also support higher-order functions, and conversely a language with higher-order functions but without first-class function support.
> ...
> First class functions are functions that are treated like an object (or are assignable to a variable).
> 
> Higher order functions are functions that take at least one first class function as a parameter, or return at least one first class function.
> 
> (https://stackoverflow.com/questions/10141124/any-difference-between-first-class-function-and-high-order-function)

> A Programming language is said to have first-class functions if it treats functions as first-class citizens. -- Wikipedia 

> A first-class citizen (sometimes called first-class objects) in a programming language is an entity which supports all the operations generally available to other entities. These operations typically include being passed as an argument, returned from a fucntion and assigned to a variable. -- Wikipedia


## Example of First Class Function

Let's take an example of how a function can be passed in as an argument:

```python
def square(x):
	return x * x

f = square(5)
z = square


print(square)
print(z)
print(f)
print(z(5))
```

#+RESULTS:
: <function square at 0x7f2574a910d0>
: <function square at 0x7f2574a910d0>
: 25
: 25

In the above example, when we printed out ~z~, ~z~ is equal to the ~square~ function. This is one of the aspects what it means to be a first-class function, i.e ~z~ is a first-class function. We can treat variable ~z~ like a function, this is demonstrated by ~z(5)~. 

## High Order Function and why it's related to First Class Function

*High-order function*: One of the consequences  of having first-class fucntions is that we can then pass on a function as an argument to another function. This latter function is now called *higher order*. A high order function is one that takes a function as an argument.

A high order function can also be a fucntion that *return* another function.

## Example 1 of High Order Function: The #map# function

 A great example of passing a function as an argument to another function is the ~map~ function. The ~map~ function takes a function and an array as its argument. It runs each value of the array through the function and then returns a new array of the results.

We can see this in our custom map function below:

```python
def square(x):
	return x * x

def cube(x):
	return x * x * x

def my_map(func, arg_list):
	result = []
	for i in arg_list:
		result.append(func(i))
	return result

print(my_map(square, [1, 2, 3, 4, 5]))
print(my_map(cube, [1, 2, 3, 4, 5]))
```

#+RESULTS:
: [1, 4, 9, 16, 25]
: [1, 8, 27, 64, 125]

*Note*: In the above example, when we pass the function ~cube()~ and ~square()~ into the ~my_map()~ function, we are *not* executing the functions. Therefore we should *not* include the parentheses.

## Example 2 of High Order Function: return another function with #logger# function 

This can be quite complicated.

In the example below we have a ~logger()~ function. Within it we have a ~log_message()~ function that does not take any argument. When then ~log_message()~ function runs it prints out 'Log' and the argument that is passed to the ~logger()~ function.

```python
def logger(msg):

	def log_message():
		print('Log:', msg)

	return log_message

log_hello = logger("Hello world!")
log_hello()

```

#+RESULTS:
: Log: Hello world!

An important point to note is that when we call the execution of ~log_hello()~ it remembers the argument that was passed in the initial ~logger()~ function in the previous line. This is what we call "closure".

## A "close to real life" example of High Order Function

Another example of why we would be returning a function as a result of another function is:

```python
def html_tag(tag):
	def wrap_text(msg):
		print("<{0}>{1}</{0}>".format(tag, msg))

	return wrap_text

print_h1 = html_tag('h1')
print_p = html_tag('p')

print_h1("This is a headline.")
print_p("This is a line of paragraph.")
```

#+RESULTS:
: <h1>This is a headline</h1>
: <p>This is a line of paragraph.</p>

In the above example, both the ~print_h1~ and ~print_p~ variables are object of a higher order function ~html_wrap()~. When we used ~print_h~, for example, we are basically using ~html_tag~ with a *remembered* argument of ~'h1'~. 

## What is Closure?

Closure is the method of binding data to a function without actually passing them as parameters. It is a function object that remember values in enclosing scopes even if they are not present in memory.

A closure is a function obejct that remember values in enclosing scopes even if they are not present in memory.
# Decorator

## First Example

Let's take an example:
- We have an outer function that doesn't take any parameter
- Within the outer function, we have a variable ~message~.
- Within the outer function, we also have an inner message that can access the ~message~ variable.
>> When execute the outter function, the inner function is executed.

```python
def outer_function():
	message = 'Hi'
	
	def inner_function():
		print(message)
	
	return inner_function()

outer_function()
```

#+RESULTS:
: Hi

Let's instead return the inner function without executing it:

```python
def outer_function():
	message = 'Hi'
	
	def inner_function():
		print(message)
	
	return inner_function

print(outer_function())
```

#+RESULTS:
: <function outer_function.<locals>.inner_function at 0x7f376df2b040>

We can also assign this to a variable object that is waiting to be executed:

```python
def outer_function():
	message = 'Hi'
	
	def inner_function():
		print(message)
	
	return inner_function

my_func = outer_function()
my_func()
my_func()
my_func()
```

#+RESULTS:
: Hi
: Hi
: Hi

Let's make some changes to the outer function. We'll make it take an actual argument. The argument will just be what was previously the local variable ~message~.

```python
def outer_function(message):
	
	def inner_function():
		print(message)
	
	return inner_function

hi_function = outer_function("Hi")
hello_function = outer_function("Hello")

hi_function()
hello_function()
```

#+RESULTS:
: Hi
: Hello

## Comes the Decorator

Decorators are very similar to what we just did above. 

Decorators provide a simple syntax for calling higher-order functions. By definition, a decorator is a function that takes another function and extends the behaviour of the latter function by adding some functionalities. All of this is done without explicitly modifying the function that is passed in.

Let's look at an example:
- The example is similar to the above with a change of naming
- We start with a decorator function which is similar to the outer function above:
```python
def decorator_function(message):	
	def warpper_function():
		print(message)	
	return wrapper_function
```

.. however instead of passing in ~message~ , which is a string, as the argument, we want to pass in a function argument.

We also create another function that can be passed in as the argument.
```python
def decorator_function(original_function):	
	def wrapper_function():
		return original_function()	
	return wrapper_function

def display():
	print('display function ran')

decorated_display = decorator_function(display)
decorated_display()
```

#+RESULTS:
: display function ran

In this extremely simple example, when we run ~decorated_display()~ we actually run the ~display()~ function through the inner ~wrapper_function~ function.

Why the hell would we want to do this? Well we would want to do this when we want to add some functionalities into the original function through the use of wrapper function.

Let's change our script a bit - say the added functionality is to simply print an additional line:

```python
def decorator_function(original_function):	
	def wrapper_function():
		print(f"The below function - '{original_function.__name__}' has been wrapped in a decorator.")
		return original_function()	
	return wrapper_function

def display():
	print("display function ran")

def say_hello():
	print("Hello world")

decorated_display = decorator_function(display)
decorated_display()
decorated_display = decorator_function(say_hello)
decorated_display()
```

```
: The below function - 'display' has been wrapped in a decorator.
: display function ran
: The below function - 'say_hello' has been wrapped in a decorator.
: Hello world
```

## The decorator syntax

The syntax of Python decorator is simple. We simply put the higher order function right before the original function, which is the first order function with the decorator symbol ~@~ at the start. Doing this, we ensure that every time we run the first order function, it gets the added functionality of the higher order function.

```python
def decorator_function(original_function):	
	def wrapper_function():
		print(f"The below function - '{original_function.__name__}' has been wrapped in a decorator.")
		return original_function()	
	return wrapper_function

@decorator_function
def say_hello():
	print("Hello world")

say_hello()
say_hello()
```

```
: The below function - 'say_hello' has been wrapped in a decorator.
: Hello world
: The below function - 'say_hello' has been wrapped in a decorator.
: Hello world
```

## Working with function with argument(s)

The above simple syntax only works with original functions that do not take any argument. If we try this with a function that takes arguments, we'd get TypeError:

```python
def decorator_function(original_function):	
	def wrapper_function():
		print(f"The below function - '{original_function.__name__}' has been wrapped in a decorator.")
		return original_function()	
	return wrapper_function

@decorator_function
def display_name(name):
	print(name)

display_name('John')
```

```
: Traceback (most recent call last):
:   File "<stdin>", line 1, in <module>
:   File "/tmp/babel-RnTXfm/python-axzpJT", line 15, in <module>
:     display_name('John')
: TypeError: wrapper_function() takes 0 positional arguments but 1 was given
```
.. So what we need is to be able to pass any number of positional or keyword arguments to our wrapper function and have it executing our original function with the arguments.

This is simple. We simply add *"*args, **kwargs"* which to the wrapper function as well as the wrapped original function. Simply put, these additions makes the functions take any number of argument that is passed to it.

```python
def decorator_function(original_function):	
	def wrapper_function(*args, **kwargs):
		print(f"The below function - '{original_function.__name__}' has been wrapped in a decorator.")
		return original_function(*args, **kwargs)	
	return wrapper_function

@decorator_function
def display_name(name):
	print(name)

display_name('John')
```

```
: The below function - 'display_name' has been wrapped in a decorator.
: John
```
## Working with Classes as decorator

Instead of using functions, we can also use Classes as decorator.

When we create the decorator function, we pass the original function as an argument. We won't be able to do the exact same thing with Class. With class we use the  ~init~ dunder method. 

Then to add the additional functionality to the original function, we can implement the dunder ~__call__~ method.

In the below example, for ease of reference I'm going to leave the decorator function in the script so we can compare the construction of class decorator versus function decorator.

```python
def decorator_function(original_function):	
	def wrapper_function():
		print(f"The below function - '{original_function.__name__}' has been wrapped in a decorator.")
		return original_function()	
	return wrapper_function


class decorator_class(object):

	def __init__(self, original_function):
		self.original_function = original_function
	
	def __call__(self, *args, **kwargs):
		print(f"The wrapper call method executed this before '{self.original_function.__name__}'")
		return self.original_function(*args, **kwargs)

@decorator_class
def hello():
	print("Hello world")
	
hello()
```

#+RESULTS:
: The wrapper call method executed this before 'hello'
: Hello world
## Looking at a practical example for decorator

A very common use case for decorator is indeed *logging*.

```python
def my_logger(orig_func):
	import logging
	logging.basicConfig(filename='{}.log'.format(orig_func.__name__), level=logging.INFO)

	def wrapper(*args, **kwargs):
		logging.info(
			"Ran with args: {}, and kwargs: {}".format(args, kwargs)
		)
		return orig_func(*args, **kwargs)

	return wrapper

def my_timer(orig_func):
	import time

	def wrapper(*args, **kwargs):
		t1 = time.time()
		result = orig_func(*args, **kwargs)
		t2 = time.time() - t1
		print("{} ran in {} second(s)".format(orig_func.__name__, t2))
		return result
	
	return wrapper

@my_logger
@my_timer
def display_info(name, age):
	print(f"{name} is {age} years old." )

display_info('Kenny', 26)

```

#+RESULTS:
: Kenny is 26 years old.
: display_info ran in 4.7206878662109375e-05 second(s)

After we ran the above, a log file was also created in our directory:

#+begin_src bash
cat display_info.log
```

#+begin_src 
| INFO:root:Ran with args: ('Kenny' | 26) | and kwargs: {} |
```

Let's try to *switch the decorators around*, this time we put ~@my_timer~ first, our result would be different:

```python
def my_logger(orig_func):
	import logging
	logging.basicConfig(filename='{}.log'.format(orig_func.__name__), level=logging.INFO)

	def wrapper_log(*args, **kwargs):
		logging.info(
			"Ran with args: {}, and kwargs: {}".format(args, kwargs)
		)
		return orig_func(*args, **kwargs)

	return wrapper_log

def my_timer(orig_func):
	import time

	def wrapper(*args, **kwargs):
		t1 = time.time()
		result = orig_func(*args, **kwargs)
		t2 = time.time() - t1
		print("{} ran in {} second(s)".format(orig_func.__name__, t2))
		return result
	
	return wrapper

@my_timer
@my_logger
def display_info(name, age):
	print(f"{name} is {age} years old." )

display_info('Kenny', 26)

```

```
: Kenny is 26 years old.
: wrapper_log ran in 0.006289482116699219 second(s)
```

See how the ~my_timer~ times the log wrapper function instead of the original function? It's because the ~my_timer~ decorator actually wraps the wrapper function. That's actually not what we want.  

To make sure that we *preserve the information of our original function with multiple decorator*, we need to use the ~wrap~ function from the ~functool~ library when we stack multiple decorators together.

#  Stacking decorators with #functool# module and the #wrap# decorator

It's quite confusing. We are putting a decorator wrap within a decorator.

```python
from functools import wraps

def my_logger(orig_func):
	import logging
	logging.basicConfig(filename='{}.log'.format(orig_func.__name__), level=logging.INFO)

	@wraps(orig_func)
	def wrapper_log(*args, **kwargs):
		logging.info(
			"Ran with args: {}, and kwargs: {}".format(args, kwargs)
		)
		return orig_func(*args, **kwargs)

	return wrapper_log

def my_timer(orig_func):
	import time

	@wraps(orig_func)
	def wrapper(*args, **kwargs):
		t1 = time.time()
		result = orig_func(*args, **kwargs)
		t2 = time.time() - t1
		print("{} ran in {} second(s)".format(orig_func.__name__, t2))
		return result
	
	return wrapper

@my_timer
@my_logger
def display_info(name, age):
	print(f"{name} is {age} years old." )

display_info('Kenny', 26)

```

#+RESULTS:
: Kenny is 26 years old.
: display_info ran in 0.013379096984863281 second(s)

Adding the ~funtools.wraps~ decorator ensure that the information from the original function is preserved.
