---
layout: post-toc
title: Automate the boring stuff with Python
tags: python programming
---


# Introduction

All programs use basic instructions as building blocks. The commons are:
- "Do this; then do that."
- "If this conditin is true, perform this action; otherwise, do that action."
- "Do this action that number of time."
- "Keep doing that until this condition is true."

Example:

```python
passwordFile = open("AutomateBoringStuff/SecretPasswordFile.txt")
secretPassword = passwordFile.read()
print('Enter your password.')
typedPassword = input()
if typedPassword == secretPassword:
    print('Access granted')
    if typedPassword == '12345':
        print('That password is one that an idiot puts on their luggage.')
else:
    print('Access denied')
```

# Note Python virtual environment:
  
- emacs elpy has been set up to use the interpreter in *`/myenv/bin/python3.7*, which is a *virtual environment*.
- This can be shown by running `print(sys.executable)` after `import os, sys`.
- In shell, to enter this virtualenv we have to do `source `/myenv/bin/activate` which will enter the virtual environment. The `source` command runs a source file within the *current shell*.

# Chapter 1 - Python Basics

## Expression, Variable, Operator and Data type
   
### Expression

```python
2 + 2


```

``` 
: 4
```
In the above example, `2+2` is called an *expression*. An expression is the most basic programming instruction in any programming language. Expressions consists of _values_ (e.g 2) and operators (e.g '+') . They can always *evaluate* i.e reduce to a single value.

### Operators

Python Math Operators from Highest to Lowest Precedence
<<operator>> <<operators>>
| Operator |             Operation              | Example | Evalutes to... |
|----------|------------------------------------|---------|----------------|
|   <c>    |                <c>                 |   <c>   |      <c>       |
|    **    |              Exponent              | 2 ** 3  |       8        |
|    %     |         Modulus/remainder          | 22 % 8  |       6        |
|    //    | Integer division/ floored quotient | 22 // 8 |       2        |
|   '/'    |              Division              | 22 / 8  |      2.75      |
|   '*'    |           Multiplication           |  3 * 5  |       15       |
|    -     |            Subtraction             |  5 - 2  |       3        |
|    +     |              Addition              |  2 + 2  |       4        |

The order of operations (also called /precendence/) of Python math operators is similar to that of mathematics. The ** operators is evaluated first, then % .etc, from *left to right*.  To override the usual precedence, use *parentheses*. 

### Data type

A *data type* is a category for values. Every value belongs to exactly one data type. The most common data types in Python are listed in the table below.
<<data type>> <<data types>>
|           Data type            |                  Examples                   |
|--------------------------------|---------------------------------------------|
|              <c>               |                     <c>                     |
|            Integers            |          -2, -1, 0, 1, 2, 3, 4, 5           |
| Floating-point numbers (float) |      -1.25, -1.0, --0.5, 0.0, 0.5, 1.0      |
|            Strings             | 'a', 'aa', 'aaa', 'Hello', 'Hello World 11' |

The meaning of an operator may also be changed based on the data type of the values next to it.

E.g: '+' is the addition operator when it operates on two integers or floats. However when + is used on two string values, it joins the string as the string *concatenation*.  If we use + on a string and an integer, Python will not know how to handle it.

Python cannot convert data type automatically. However we can do this.

The * operator when used between a string and an integer will *multiply the string*. It cannot be used on two strings.
``` 
>>> 4 + 4 
8
>>> 'Hello' + 'World'
'HelloWorld'

>>> 'Hello' + 4
TypeError: Can't convert 'int' object to str implicity.

>>> 'Alice' * 2
'AliceAlice'

>>> 'Alice' * 'Hello'
TypeError: can't multiply sequence by non-int of type 'str'.
```
 
### Variable
<<variable>> <<variables>>
A variable is like a box in computer's memory where a *single value* can be stored. For reuse of a result that has been evaluated, we can store it in a variable.

A value is stored in a variable with an *assignment statement*. It is initialized/ created the first time a value is stored in it. When a value is assigned a new variable, the old value is forgotten, or *overwritten*. 


To name a variable, we have to follow *three rules*:

``` 
>>> 'Alice' + "world"
'Aliceworld'
>>> "alice" + "world"
'aliceworld'
>>> spam = 40
>>> spam
40
>>> eggs = 2 
>>> spam + eggs
42
```

1. It can be only one word.
2. It can use only letters, numbers and the underscore (_) character.
3. It can't begin with a number

*Note*: To name a variable with two words we can use *underscore* or *capitalization*, i.e 'my_student' or 'myStudent'. The official Python code style, PEP 8 says to use underscore. However, the most important thing is to be *consistent*.

Note that variable names are *case sensitive*.





## Basic about writing codes

Python *ignores* blank lines so this can be useful to make code easier to read, like paragraphs in a book.
"#" starts a comment line.

Looking at the `print('Hello World!')` line. It means "Print out the text in the string 'Hello World!'. When Python executes this line, we say that Python is calling the print() *function* and 'Hello World' is being passed to the function call as an *argument*. The quotes aren't printed as they are just used to mark where the string begins and end.

Remember that *expressions can always evaluate to a _single_ value*. 

Example:
- `myName = input()` is a function call. It evaluates to a string equal to user input. This string is then assigned to the myName variable. We can also think of this as an expression that eventually evaluates to whatever string the user typed in.
- and then if we do `print('Hello ' + myName)`, this expression evaluates to 'Hello Kenny' if we inputted 'Kenny' for myName.


## The str(), int(), and float() Functions

`print('hello ' + 29)` would return an error because 29 is an integer and 'hello ' is a string and these two data types cannot concatenate. 

To concatenate these two arguments, we need to turn the value `29` into a string.  This can be done by the `str()` function, as follow:
```python
print('I am ' + str(26) + ' years old.')

```

```
: I am 26 years old.
```
The `str()`, `int()`, and `float()` functions evalutes to string, integer and float forms of the passed value respectively.

`int()` is handy, for examle `input()` function always returns a string, even if user enters a number.

```python
myAge = '29'
print(myAge)
type(myAge)

myAge = int(myAge)
print(myAge)
type(myAge)

```

```
: 
: 29
: <class 'str'>
: >>> >>> 29
: <class 'int'>
```
If we pass a value to `int()` that cannot be evaluated  as an integer, Python will display an error message, for example:

```python
int('99.99')
```

```
: Traceback (most recent call last):
:   File "<stdin>", line 1, in <module>
: ValueError: invalid literal for int() with base 10: '99.99'
```
# Chapter 2 - Flow control

The real strength of programming isn't just executing one instructions after another. Based on how the expressions evaluate, the program can decide to skip instructions, repeat them or choose one of several instructions to run. In fact we should never want our program to start from the first line of code and simply execute every line straight to the end.

This is what *Flow control* statements are for. They decide which Python instructions to execute under which conditions.

## Boolean

Before learning about flow control statements, we first need to learn how to represent /yes/ and /no/ options. To that end we need to explore Boolean values, comparison operators and Boolean operators.

While int, floats and string data types have an unlimited number of possible values, the *Boolean* data type has only two values: `True` and `False`.  In Python, follow this syntax for Boolean values:
- They always lack the quotes we'd normally put around string.
- They always start with a capital *T* or *F*, with the rest of the string in lowercase.

*Comparison operators*

| Operator | Definition               |
|----------|--------------------------|
| '=='     | Equal to                 |
| !=       | Not equal to             |
| <        | Less than                |
| >        | Greater than             |
| <=       | Less than or equal to    |
| >=       | Greater than or equal to |

These operators evaluate to either `True` or `False` depending on the values we give them.

Note: An *integer* or *floating-point* value will always be unequal to a string value. The other operators work properly *only* with integer and floating-point values.

The three *Boolean operators* *(and, or and not)* are used to compare Boolean values. Like comparison operators they also evaluate these expressions down to a Boolean value. The `and` and `or` operators always take *two* Boolean values or expressions. They are considered *binary* operators.

- The `and` operator evalues an express to `True` if *both* Boolean values are `True`. Otherwise it evaluates to `False`.
- The `or` operator evaluates an expression to `True` if *either* of the two Boolean values is `True`. It only evaluates to `False` if both Boolean values are `False`.
- The `not` operators operates on only *one* Boolean value (or expression). It simply evaluates to the opposite Boolean value. It can be nested.

These three are called *Boolean operators* because they always operate on the Boolean values `True` and `False`.
```python
not True
```

```
: False
```python
not False
```

```
: True
```python
(4 < 5) and (5 < 6)
```

```
: True
```python
(4 > 5) and (5 < 6)
```

```
: False
```python
(4 > 5) or (5 < 6)
```

```
: True
```
Order of evaluation:
- Left first, then right.
- Brackets are prioritized.
- not first, then and then or.

## Flow control - The condition

Flow control statements most often start with a part called *condition*, and are all followed by a block of code called *the clause*.

The Boolean expressions could all be considered conditions, which are similar to expression. Condition is just a more specific name in the context of flow control statements. *Conditions always evaluate down to a Boolean value*, `True` or `False`. A flow control statement decides what to do based on whether its condition is `True` or `False`. Almost every flow control statement uses a condition.

## Block of code

Lines of Python code can be grouped together in blocks. Beginnings and end of blocks can be identified by the indentation of the lines of code. There are three rules for blocks:

1. Blocks begin when indentation increases.
2. Blocks can contain other blocks.
3. Blocks end when the indentation decreases to zero or to a containing block's indentation.

## The `if` and `else` statements

The statement represents the actual decision that the program will make.

Most common type of flow control statement: `if` statement. An `if` statement will execute if the condition is `True`. The clause is skipped if the condition is `False`.

```
If this condition is true, execute the code in the clause.
```

*Python syntax*:
```python
if 4 < 5:
    print('Hello!')
```

```
: Hello!
```
An `if` statement can be followed by an `else` statement. The `else` clause is executed only when the `if` statement's condition is `False`.

```
If tis condition is true, execute this code. Or else, execute *that* code.
```

An `else` statement doesn't have a condition.

```python
if 4 > 5:
    print("Hello!")
else:
    print("Aloha!")
```

```
: Aloha!
```
*Only one of the `if` or `else` statement will execute.*

## The `elif` statement

In scenarios where we want one of many possible clauses to execute, the `elif` statement is used. The `elif` statement is an "else if" statement that *always follows an `if` or another `elif` statement*. 

`elif statement` provides another condition that is checked *only if all the previous conditions were* `False`.

```python
if 4 > 5:
    print("Hello")
elif 5 < 4:
    print ("Aloha")
elif 4 < 6:
    print("Finally!")
```

```
: Finally!
```
When there is a chain of `elif` statements, only *one or none* of the clauses will be executed. When one `True` condition has been found on one `elif` statement, *the rest of the other `elif` clauses are skipped*.

The order of the `elif` statements does matter.

```
Remember: At most only *one* of the `elif` clauses will be executed. Therefore, the order of `elif` statements matter.
```

Optionally, we can also have an `else` statement after the last `elif`. In this case, it is *guaranteed* that at least and only one of the clauses will be executed. The `else` clause will execute when all `if` and `elif` statements are `False`.

### Comparison between `if` and `elif` 

```python
a = 2
if a > 1:
    a += 1
elif a > 2:
    a += 2
print(a)
```
: 3
```python
a = 2
if a > 1:
    a += 1
if a > 2:
    a += 2
print(a)
```
: 5
```
In the first code block, `elif` is part of `if` and only the `if` statement is executed. The `elif` statement was bypassed.
In the second code block, both `if` statement's conditions were met and executed in series.

## The `while` statement
### Overview and how to
We can make a block of code execute *over and over* again with a `while` statement. The code in a `while` clause will be executed *as long as* the `while` statement's condition is `True`. 

Syntax and example:

```python
n = 1
while n < 5:
    print("Count " + str(n))
    print("Hello my name is Kenny.")
    n += 1
```

```
: Count 1
: Hello my name is Kenny.
: Count 2
: Hello my name is Kenny.
: Count 3
: Hello my name is Kenny.
: Count 4
: Hello my name is Kenny.
```
Although the syntax between `while` and `if` are the similar, at the end of an `if` clause the program execution continues whereas at the end of a `while` clause the program execution *jumps back* to the start of the `while` statement. This is why..

```
The `while` clause is often called a *loop*.
```

Another example could be:

```python
verification = "your name"
while input != verification:
    input = input()
    print("Please type your name")
```

As long as the user input is *not* "your name", the while loop's condition will remain `True` and the program would just keep asking forever. 

### break

There are some situations where your want the `while` condition to always remain `True`. So you need a way to *break out* of a `while` loop.

There is a shortcut to getting the program execution to break out of a `while` loop's clause early. If the execution reaches a `break` statement, it immediately exits the `while` loop's clause. A break statement simply contains the `break` keyword.

Example:
```python
while True:
    print('Please type your name')
    name = input()
    if name == "your name":
        break
```

The first line `while True` essentially creates an *infinite* loop because the expression `True` always evalues down to the value `True`.  In this scenario, the proram execution will always enter the loop and will only exit it when a `break` statement is executed. Of course we do still have common programming bug around infinite loop.

### continue

    Instead of "continue", the `continue` statements actually jump back to the start of the loop.
Similary to the `break` statements, the `continue` statements are also used inside loops. Its action is similar to what happens when the execution reaches the end of the loop which is *jumping back* to the start of the loop.

Example:
```python
while True: 
    name = input('What is your name?: ') 
    if name != "Kenny": 
        continue 
    age = input("Oh hello " + name + ", how old are you? ") 
    print("Hello " + name + ", who is " + str(age) + " years old.") 
    break 
```

Results:
``` 
What is your name?: asda
What is your name?: asdsa
What is your name?: sajfgdsf
What is your name?: Csdas
What is your name?: sakjdn
What is your name?: askndas
What is your name?: akdnjs
What is your name?: kenny
What is your name?: Kenny
Oh hello Kenny, how old are you? 26
Hello Kenny, who is 26 years old.
```

### Trapped in an infinite loop

Solution: Press `CTRL + C`.
Action: Sending a `KeyboardInterrupt` error to the program and cause it to stop immediately.

### "Truthy" and "Falsey" values

There are some values in other data types that conditions will consider equivalent to `True` and `False`.

| `False` values | `True` values |
|--------------|-------------|
|            0 | All         |
|          0.0 | other       |
|   '' (empty) | values      |
|--------------|-------------|

```python
name = '' # Set name = empty string
while not name: # While name is empty, continue asking for name
    print("Enter your name: ")
    name = input() # If a blank input is received, the loop continues.
```

Explanation:

- If `name` is empty, the value of `name` would equivalate to `False`.
- `while not name` becomes `while not False`, or `while True`, and the `while` statement's condtion is `True`.

```python
print("How many guests are coming?")
num_of_guests = int(input()) #Asking for user input
if num_of_guests:
    print("Be sure to have enough room.")
print('Done.')
```

Explanation:
- If `num_of_guests` is *anything but zero*, the if statement's condition is `True`, and the program will print the reminder for the user.

## The `for` statement and `range()` function

The `while` loop keeps looping while its condition is `True`. However if we want to execute a block of code a certain `n` number of time, we can use `for` loop statement and the `range()` function.

Syntax:
``` 
for [variable name] in range([int, where int <= 999]):
    clause
```

Example:
```python
for i in range(5):
    print("Hello, this is " + str(i) + " iteration.")
```

```
: Hello, this is 0 iteration.
: Hello, this is 1 iteration.
: Hello, this is 2 iteration.
: Hello, this is 3 iteration.
: Hello, this is 4 iteration.
```
When `range(5)`, the the loop's clause is run *five* times. the first time it is run, the variable `i` is set to `0`.

The variable `i` will go up to, *but not inlcude* the integer passed to `range()`.

```python
sum = 0
for i in range(101):
    sum += i
print(sum)
```

```
: 5050
```
a `while` loop can be used interchangably:
```python
sum = 0
i = 0
while i < 101:
    sum += i
    i += 1
print(sum)
```

```
: 5050
```
or

```python
i = 0
while i < 5:
    print("Hello, this is " + str(i) + " iteration.")
    i += 1
```

```
: Hello, this is 0 iteration.
: Hello, this is 1 iteration.
: Hello, this is 2 iteration.
: Hello, this is 3 iteration.
: Hello, this is 4 iteration.
```
### `range()` function with starting, stopping and stepping arguments

Some functions can be called with multiple arguments separated by a comma. This includes the `range()` function.

Example:

```python
for i in range(15,20):
    print(i)
```

```
: 15
: 16
: 17
: 18
: 19
```
The `range()` function can also be called with *three* arguments where the third argument will be the *step* argument.

```python
for i in range(15,20,2):
    print(i)
```

```
: 15
: 17
: 19
```
You can also use negative arguments to make the `for` loop counts down instead of up.

Syntax:
``` 
range([start],[stop],[step])
```

## Importing Modules

### `import` a  standard library
`print()`, `len()` functions are so called built-in functions. They belong to a basic set of functions that come with Python.

Python also comes with a set of modules called the *standard library*. Each module is a Python program that contains a related group of functions that can be *embedded* in our programs.

Example: the `math` module has mathematics-related functions, the `random` module hsa random number-related functions, and so on.

Before we can use the functions in a module, we need to import the module with an `import` statement.

Syntax:
``` 
import [module 1], [module 2]
```

.. however we should do:

```python
import module1
import module2
```

Once a module is imported, we can use all the functions of that module.

```python
  import random
  for i in range(5):
    print(random.randint(1,10))    

```

```
: 5
: 5
: 6
: 10
: 9
```
`random.randint(1,10)` calls a random integer value between 1 and 10 when it's executed. The results will be different most times.

We need to type `random.` infront  of `randint` because the `randint` is in the `random` module. Python would then know to look for `randint` inside `random` module.

### `from import` statement

An alternative form of `import` is composed of the `from` keyword followed by the module name, and a star.

For example, instead of
```python
import random
print(random.randint(1,5))
```
: 4
```
we can do
```python
from random import randint
i=randint(1,5)
print(i)
```


### ending a program early with `sys.exit()`

A program normally terminates when execution reaches the *bottom* of the insturctions. However we can cause the program to terminate or exit by calling the `sys.exit()` function. 

Example:
```python
import sys
while True:
    print('Type exit to exit')
    response = input()
    if response == 'exit':
        sys.exit()
    print('You typed ' + response + ', not exit.')
```

``` 
Type exit to exit.
test
You typed test, not exit.
Type exit to exit.
lol
You typed lol, not exit.
Type exit to exit.
exit

SystemExit

```
# Chapter 3 - Functions
  A function is like a mini-program within a program.
## `def` statement

Example:
```python
def hello(): # a def statement defines a function. In this scenario a function is named hello()
    print('Howdy!')
    print('Hello there!')

hello() # function call
```

```
: Howdy!
: Hello there!
```
A function call is just the function's name followed by parentheses, possibly with some number of arguments within, or just none.

When the program execution reaches a function call, it will jump to the top line in the function and begin executing code there. At the end of the function, the execution returns to the line that called the function and continues moving through the code as before.

A major purpose of functions is to group code that get executed multiple times. In general, we want to *avoid* duplicating code. One of the reasons is in the scenario of bug fixing or updating, we dont have to change the same code block everywhere we call it. Another reason is we want our programs to contain less redundancies, more readable, shorter and easier to update,

## `def` statement with parameters

```python
print('Hello, this is an argument')
```

```
: Hello, this is an argument
```
When we called the `print()` function, we passed in values. These are called *arguments*.

Example:
```python
def hello(yourname, myname): # define function that take 2 arguments
# There are two parameters - yourname & myname
    print('Hello, ' + yourname + ', my name is ' + myname) 

hello('Roku','Kenny') # 2 arguments are passed
hello('Roku') # only 1 argument - this will return an error 
```

```
: Hello, Roku, my name is Kenny
: Traceback (most recent call last):
:   File "<stdin>", line 1, in <module>
:   File "/tmp/babel-21385xpm/python-21385Drc", line 6, in <module>
:     hello('Roku') # only 1 argument - this will return an error 
: TypeError: hello() missing 1 required positional argument: 'myname'
```
A *parameter* is a variable that an argument is stored in when a function is called. When the function returns/ end, the value(s) stored in parameter(s) are forgotten. The variable is effectively destroyed after a function call. This is similar behaviour to how a program's variables are forgotten when the program terminates.

## `return` values and `return` statements

```python
len('Hello')
```

```
: 5
```
In the above example, when we called the `len()` function and pass it an argument /'Hello'/, the function evaluates to an integer value `5`, which is the length of the string we passed. In general, this is called a *return value* of the function `len()`. 

When we create a function using the `def` statement, we can specify what the return value should be with a `return` statement.

```python
import random

def get_answer(answerNumber):
    if 1 <= answerNumber <= 3:
        return 'It is certain.'
    elif 4 <= answerNumber <= 6:
        return 'It is decidedly so.'
    elif 7 <= answerNumber <= 9:
        return 'Yes'


for i in range(4):
    r = random.randint(1,9)
    fortune = get_answer(r)
    print('Roll ' + str(i+1) + ':')
    print(fortune + '\n')
```

```
Roll 1:
It is certain.

Roll 2:
Yes

Roll 3:
It is certain.

Roll 4:
It is certain.
```

The `get_answer` function can return 3 different values depending on the argument that is passed to it. Depending on what `answerNumber` is, which in that program is a random integer between 1 and 9 inclusive, the function returns one of three possible string values.

We can also do this:

```python
import random

def get_answer(answerNumber):
    if 1 <= answerNumber <= 3:
        return 'It is certain.'
    elif 4 <= answerNumber <= 6:
        return 'It is decidedly so.'
    elif 7 <= answerNumber <= 9:
        return 'Yes'

for i in range(4):
    print('Roll ' + str(i+1) + ':\n' + get_answer(random.randint(1,9)) + '\n') 
```

```
Roll 1:
Yes

Roll 2:
It is decidedly so.

Roll 3:
Yes

Roll 4:
It is certain.
```

As a function evaluates to a return value, it can be used within an expression because expressions are simply composed of *values and operator*.

## The `None` value

There is a value called `None`, which represents the absence of a value. 

`None` is the *only value* of the `NoneType` data type. In other languages the equivalence would be `null`, `nil` or `undefined`. Just like the two Boolean brothers `True` and `False`, `None` is typed witih a *Capital `N`*.

This value-without-a-value can be helpful when we need to store something that won't be confused for a real value in a variable. For example we can use this with the `print()` function which does *not* return any value but simply display texts on the screen.  Therefore, `print()` actualy returns a `None` value. We can see this below:

```python
spam = print('Random text')
if spam == None:
    print('See, I told you. \'spam == None\' evaluates to True.')
```

```
: Random text
: See, I told you. 'spam == None' evaluates to True.
```
Behind the scene, Python adds `return None` to the end of any function definition with no `return` statement. This is similar to how a `while` or `for` loop implicitly ends with a `continue`. Also `return None` = `return`
## Local and Global Scope
  
Parameters and variables that are assigned in a called functions are said to exist in that function's local scope.

For example:
```python
def greeting(name):
   print('Hello, ' + name + ', how are you feeling today?')

greeting('Kenny')
```

```
: Hello, Kenny, how are you feeling today?
```
In the above example, name is a parameter/ variable and 'Kenny' is a argument that exist in the function `greeting()`'s local scope.

A *scope* is basically a container for variables. When a scope is destroyed, all the values/ arguments stored in the scope's variables are forgotten.

There is only one *global scope*, it is created *when the program begins*. When the program terminates, the global scope is destroyed, all its vavariableriables forgotten.

A *local scope* is created whenever a function is called. Any variables assigned in this function exist within the local scope. *When the function returns*, the local scope is destroyed, and all it svariables are forgotten.

- Code in global scope cannot use local variables.
```python
def spam():
    eggs = 100 # local scope
spam()
print(eggs)
```

```
: Traceback (most recent call last):
:   File "<stdin>", line 1, in <module>
:   File "/tmp/babel-10254-gQ/python-10254XeD", line 4, in <module>
:     print(eggs)
: NameError: name 'eggs' is not defined
```
- However, a local scope can access global variables.
```python
test = "Hello Test." # global scope
def hello():
    print(test)

hello()
test = "Hello Update." # global scope
hello()
```

```
: Hello Test.
: Hello Update.
```
- Code in a function's local scope cannot use variables in any other local scope.
- You can use the same name for different variable if they are in different scope (i.e global `spam` and local `spam`)

It is bad habits to rely on global variables, especially if your programs get larger and larger. When variables are modified by the code in a particular call to a function, the function interacts with the rest of the program only through its parameters and the return value. This is easier in the scenario of debugging. If a program contains nothing but global variables and had a bug because of a global variable being set to bad value, it would be hard to track down where this bad value was set.

## The Global Statement

To modify a global variable from within a function's local scope, use the `global` statement. Using this ensure Python does *not* create a local variable within the local scope.

```python
def spam():
    global eggs
    eggs = 'spam'

eggs = 'global'
spam()
print(eggs)
```

```
: spam
```
The last line above which is a `print(eggs)` call outputs `spam` because `eggs` is *declared global* at the top of `spam()`. When the `spam()` function is called and `eggs` is set to 'spam', this assignment is done to the globally scoped `eggs`. No local eggs variable is created.

```python
def spam():
    global eggs
    eggs = 'spam' # global

def bacon():
    eggs = 'bacon' #local

def ham():
    print(eggs) #global

eggs = 42 # global
spam() # this changes the global variable
bacon() # no change to global variable
print(eggs)
```

```
: spam
```
There are four rules to tell whether a variable is in a local or global scope:

1. If a variable is being used in the global scope, that is outside of all functions, then it is always a global variable.
2. If there is a `global` statement for that variable within a function, it is a global variable.
3. Otherwise, if the variable is used in an assignment statement within a function, it is a local variable.
4. If the variable is *not* used in an assignment statement, it is a global variable.

In a function, a variable will always either be global or always be local.

Demonstration of Rule 3:
```python
def test():
    print(spam)
    spam = 'Hello'

spam = "Hello My name is Global."

test() # This will return an error.
```

```
: Traceback (most recent call last):
:   File "<stdin>", line 1, in <module>
:   File "/tmp/babel-10254-gQ/python-10254LOQ", line 6, in <module>
:     test() # This will return an error.
:   File "/tmp/babel-10254-gQ/python-10254LOQ", line 2, in test
:     print(spam)
: UnboundLocalError: local variable 'spam' referenced before assignment
```
`test()` returns an error because Python sees that there is an assignment statement for `spam` in the `test()` function, therefore it considers `spam` a local variable. However `print(spam)` is executed before the variable assignment so at this point the variable does not exist. *Python does not fall back to using a global variable.*

## Exception Handling

An *Exception* is an error within a Python program. In real life we don't want this to happen because the program would crash. Instead we want the program to *detect error*, handle them and continue to run.

```python
def forty2_divided_by(x):
    return 42 / x

print(forty2_divided_by(2))
print(forty2_divided_by(3))
print(forty2_divided_by(0))
print(forty2_divided_by(4))
    
```

```
: 21.0
: 14.0
: Traceback (most recent call last):
:   File "<stdin>", line 1, in <module>
:   File "/tmp/babel-10254-gQ/python-10254YfK", line 6, in <module>
:     print(forty2_divided_by(0))
:   File "/tmp/babel-10254-gQ/python-10254YfK", line 2, in forty2_divided_by
:     return 42 / x
: ZeroDivisionError: division by zero
```
In the above example, a `ZeroDivisionError` is an Exception that happens when we try to divide a number by `0`.  As we can see this crashed the program and the function call `print(forty2_divided_by(4))` is ignored.

*Errors can be handled* with `try` and `except` statements.
``` 

try [code that could potentially produce error]
except [if an error happens]

```

```python
def forty2_divided_by(x):
    try:
        return 42/x
    except ZeroDivisionError as e: # Catching the exception then call it e
        return(str(e) + " - However, this isn't terminating.")

print(forty2_divided_by(14))
print(forty2_divided_by(0))
print(forty2_divided_by(3))
```

```
: 3.0
: division by zero - However, this isn't terminating.
: 14.0
```
In the above example we only had one function call within a `try` block. However *any number of errors that occur in function calls* in a `try` block will also be caught.

## Practice: Guess the Number

```python
from random import randint


def initGame():
    print("I'm thinking of a number between 1 and 5.")
    print("You'll get three guesses." + "\n")
    secretNumber = randint(1, 5)

    # Hints
    toosmall = "Your guess was smaller than the secret number.\n"
    toobig = "Your guess was bigger than the secret number.\n"

    for guessesTaken in range(3):
        print("Take a guess.")
        guess = int(input())

        if guess < secretNumber:
            print(toosmall)
        elif guess > secretNumber:
            print(toobig)
        else:
            break  # correct guess

    if guess == secretNumber:
        print("GRATZ! You won after " + str(guessesTaken+1) + " guesses.")
    else:
        print("The number was " + str(secretNumber) + ". You lost.")

    return None

initGame()
```

*Note for self*:  While writing the above code I spent a bit of time on a logic error. I realised this happened because `if` was used instead of `elif`  in this line:
```python
elif guess > secretNumber
```
With another `if`, the `else` statement belongs to the second (or last) `if` statement and the first `if` becomes obsolet.
## Practice - The Collatz Sequence
 
   
The Collatz Sequence

Write a function named collatz() that has one parameter named number. If number is even, then collatz() should print number // 2 and return this value. If number is odd, then collatz() should print and return 3 * number + 1.

Then write a program that lets the user type in an integer and that keeps calling collatz() on that number until the function returns the value 1. (Amazingly enough, this sequence actually works for any integer—sooner or later, using this sequence, you’ll arrive at 1! Even mathematicians aren’t sure why. Your program is exploring what’s called the Collatz sequence, sometimes called “the simplest impossible math problem.”)

Remember to convert the return value from input() to an integer with the int() function; otherwise, it will be a string value.

Hint: An integer number is even if number % 2 = 0, and it’s odd if number % 2 1. 

The output of this program could look something like this:

``` 
Enter number:
3
10
5
16
8
4
2
1
```


*Input Validation*

Add try and except statements to the previous project to detect whether the user types in a noninteger string. Normally, the int() function will raise a ValueError error if it is passed a noninteger string, as in int('puppy'). In the except clause, print a message to the user saying they must enter an integer.


```python
# The Collatz Program
    def collatz_number(x):
    # One parameter, a number, which is x.

    if x % 2 == 0:  # return x // 2 for even x
        result = x // 2
    elif x % 2 == 1:  # return x*3 + 1 for odd x
        result = (x * 3) + 1

    return result


    def collatz():
    # Take user input.
    # Repeats until an integer is entered.
    while True:
        try:
        user_input = input('Enter an integer: ')
        user_input = int(user_input)
        break
        except ValueError:
        print('An integer, please.')
        continue
    i = 0

    result = user_input  # starting point

    # Keep on collatzing until reaching number 1.

    while result != 1:
        result = collatz_number(result)
        i += 1
        print('collatz ' + str(i) + ': ' + str(result))

    print("\nResult: " + str(i) + ' runs.')
```
# Chapter 4 - Lists

A list is a value that contains multiple values in an ordered sequence.

List and its cousin tuple are important data types that can contain *multiple values*.

List can contain other lists. Therefore it can be used to arrange data into hierarchical order.

The term *list value* refers to the list itself, not the values inside the list value.

A list value looks like this `['cat', 'dog', 'rat', 'elephant']`. A list begins with an opening square bracket `[` and end with a closing square bracket `]`. Values inside the list are called *items* and are separated with commas (i.e being *comma=delimited*). 

```python
test = ['cat', 'dog', 'elephant', None]
print(test)
for i in test:
    print(i)
```

```
: ['cat', 'dog', 'elephant', None]
: cat
: dog
: elephant
: None
```
The test variable is assigned only *one value - the list value*. However the list value itself contains other values.

## Indexes

`list[i]`: list is the name of the list variable and i refers to the index.

- The first value in the list is at *index 0*, and so on.

Example:
```python
test = ['dog', 'cat', 'elephant']
print(test[0])
print(test[2])
print('The ' + test[1] + ' ate the ' + test[2] + '.')
```

```
: dog
: elephant
: The cat ate the elephant.
```
*Error*:
- `IndexError` is given by Python when we use an index that exceeds the number of values in our list values.
- Indexes can only be integer values, not float. Using a float would cause `TypeError` error.

### Looped lists and multiple indexes

*List can also contains other list values, the values in these lists of lists can be accessed using _multiple indexes_, for example:*

```python
test = ['dog', 'cat', 'elephant', ['bee', 'cockroach', 'butterfly']]

print(test[1])
print(test[3][2]) 
# index 3 refers to the list, the following [2] points to 3rd item in the contained list
```

```
: cat
: butterfly
```
### Negative Indexes

```python
test = ['dog', 'cat', 'elephant']

print(test[-1])
print(test[-3] == test[0])
```

```
: elephant
: True
```
While indexes start at `0` and go up, we can also use negative integers for the index. The last item within the list can be referred to using index `-1` 
### Sublists and slices 

An index can get a *single value* from a list.

A slice can get *several values* from a list in the form of a new list.

```python
test = ['dog', 'cat', 'elephant', 'lion', 'tiger', 'cheetah', 'panther', 'Iron Man']
print(test[0:2]) # elephant is not included
print(test[-1:-5])
print(test[-5:-1]) # test[-1] 'Iron Man' is not included

print(test[-2:])

```

```
: ['dog', 'cat']
: []
: ['lion', 'tiger', 'cheetah', 'panther']
: ['panther', 'Iron Man']
```
A slice is typed between square brackets like an index but it has *two integers* separated by a colon.

In a slice, the *first* integer is the *starting index*. The *second* integer is the *ending index*. A slice goes up to the *ending index* _non-inclusive_. 

As a shortcut, we can leave either index out on either side of the colon. Leaving out the first index is the same as using 0. Leaving out the second index is the same as the length of the list. A list length can be return using `len()`

```python
test = ['dog', 'cat', 'elephant', 'lion', 'tiger', 'cheetah', 'panther', 'Iron Man']
print(len(test))
print(test[7]) # last item  has index of len(list) - 1
``` 

```
: 8
: Iron Man
```
### Changing a value of a list item with indexes

  ```python
  test = ['dog', 'cat', 'elephant', 'lion', 'tiger', 'cheetah', 'panther', 'Iron Man']
  test[0] = 'not a dog anymore'
  print(test)
  test[1] = test[0]
  print(test)
  ```

  ```
  : ['not a dog anymore', 'cat', 'elephant', 'lion', 'tiger', 'cheetah', 'panther', 'Iron Man']
  : ['not a dog anymore', 'not a dog anymore', 'elephant', 'lion', 'tiger', 'cheetah', 'panther', 'Iron Man']

## List concatenation and list replication

| OPERATOR |     USAGE     |          EFFECT           |
|----------|---------------|---------------------------|
|   <c>    |      <c>      |            <c>            |
|    `+`     | between lists | combine lists into a list |
|    `*`     |  list & int   |      replicate list       |

```python
test = ['dog', 'cat', 'elephant']
avenger = ['Iron Man', 'Thor']

print(test + avenger)  # Order matters here
print(avenger * 4)
```

```
: ['dog', 'cat', 'elephant', 'Iron Man', 'Thor']
: ['Iron Man', 'Thor', 'Iron Man', 'Thor', 'Iron Man', 'Thor', 'Iron Man', 'Thor']
```
## Removing list item with `del`
<<del>>
```python
test = ['dog', 'cat', 'elephant']
del test[0]
print(test)
```

```
: ['cat', 'elephant']
```
The `del` statement also be used to delete or "unassign" simple variable. However it's almost never used for this.
## Working with lists

Instead of using multiple, repetitive variables, we can use a single list variable that contains multiple similar values.

Example: Instead of ...
```python
dog1 = 'Roku'
dog2 = 'Hachi'
print(dog1 + dog2)
```

```
: RokuHachi
```
We can do..
```python
dog = ['Roku', 'Hachi']
print(dog[0] + dog [1])

# then to add to the existing dog list we can do
dog += ['Alex']
print(dog)
```

```
: RokuHachi
: ['Roku', 'Hachi', 'Alex']
```
## Using `for` loops with lists

Technically, a `for` loop repeats the code block for each value in a list-like value.

For example if we do
```python
for i in range(4):
    print(i)
```

```
: 0
: 1
: 2
: 3
```
The `range(4)` bit is a list that has value that is similar to `[0,1,2,3]`. Remember `range(x)` is from `0` up to `x` non-inclusive.

```python
for i in [0,1,2,3]:
    print(i)
``` 

```
: 0
: 1
: 2
: 3
```
A common Python techniques is to use list with `range(len(some_list))` with a `for` loop to iterate over the indexes of a list. For example:

```python
some_list = ['Frenchie', 'Poodle', 'Chihuahua', 'Shiba Inu', 'Labrador', 'Akita']
for i in range(len(some_list)):
    print('Index ' + str(i) + ' in some_list is ' + some_list[i])
```

```
: Index 0 in some_list is Frenchie
: Index 1 in some_list is Poodle
: Index 2 in some_list is Chihuahua
: Index 3 in some_list is Shiba Inu
: Index 4 in some_list is Labrador
: Index 5 in some_list is Akita
```
In the above example the loop access both the index (`i`) as well as the value at that index (`somelist[i]`). Best of all, `range(len(some_list))` will iterate through all the indexes of some_list, no matter how many items it contains.
## the `in` and `not in` operators

These two values can be used in expressions that connect two values to evaluate to a Boolean value. This is good for checking values in a pre-determined set.

Example:

```python
test = ['dog', 'cat', 'Thor']
print('Thor' in test)
print('Thor' not in test)
print('elephant' in test)
```

```
: True
: False
: False
## The multiple assignment trick
<<multiple_assignment>>
Instead of doing:
```python
cat = ['fat', 'orange', 'loud']
size = cat[0]
color = cat[1]
disposition = cat[2]
```
print(size)
print(color)
print(disposition)
```
: fat
: orange
: loud
```
We can do use the multiple assignment trick which is..
```python
cat = ['fat', 'orange', 'loud']
size, color, disposition = cat
print(size)
print(color)
print(disposition)
```

```
: fat
: orange
: loud
```
To do this, *the number of variables* and the *length of the list* must be *exactly equal*, otherwise a ValueError would be produced..

```python
cat = ['fat', 'orange', 'loud']
size, color, disposition, test = cat
```
: Traceback (most recent call last):
:   File "<stdin>", line 1, in <module>
:   File "/tmp/babel-10254-gQ/python-10254sFe", line 2, in <module>
:     size, color, disposition, test = cat
: ValueError: not enough values to unpack (expected 4, got 3)
```
The multiple assignment trick can actually be used for separate variables..

```python
a, b = 'Alice', 'Bob'
print(a)
print(b)
b, a = a, b 
print(a)
print(b)
```
: Alice
: Bob
: Bob
: Alice
```
## Augmented Assignment Operators

Instead of doing..
```python
test = 45
test = test + 1
print(test)
```

```
: 46
```
We could do..

```python
test = 45
test += 1
print(test)
```

```
: 46
```
| Augmented Assignment | Equivalent Assignment |
|      Statement       |       Statement       |
|----------------------|-----------------------|
|         <c>          |          <c>          |
|      spam += 1       |    spam = spam + 1    |
|      spam -= 1       |    spam = spam - 1    |
|      spam *= 1       |    spam = spam * 1    |
|      spam /= 1       |    spam = spam / 1    |
|      spam %= 1       |    spam = spam % 1    |
|----------------------|-----------------------|

## Methods and List Methods

A *method* is the same thing as a function, except it is "called on" a value. 

The difference in syntax is displayed below:
``` 
function() _object_
_object_.method()
```

*Each data type has its own set of methods.*

The list data type for example has several useful methods..

### `append()` and `insert()`

These can be used to add items to a list. `append()` add the item to the *end* of the list, whereas `insert()` can add a value at *any index* in the list.

```python
animal = ['cat', 'dog']
animal.append('mouse')
print(animal)
```
: ['cat', 'dog', 'mouse']
```python
animal = ['cat', 'dog']
animal.insert(0, 'chicken')
print(animal)
animal.insert(1, 'mouse')
print(animal)
```
: ['chicken', 'cat', 'dog']
: ['chicken', 'mouse', 'cat', 'dog']
```
Notice that the code is `animal.append(..)` not `animal = animal.append(..)`. This is because neither method gives the new value. Both of them `return None`. Rather, the list is modified *in place*. 

These two methods are list methods and can only be called on list values. If we use a method on a data type that doesn't have that method, you'd get `AttributeError`.
```python
test = "hello"
test.append("hell")
```

```
: Traceback (most recent call last):
:   File "<stdin>", line 1, in <module>
:   File "/tmp/babel-10254-gQ/python-10254sMS", line 2, in <module>
:     test.append("hell")
: AttributeError: 'str' object has no attribute 'append'
```
### `remove()`

```python
animal = ['dog', 'cat', 'dog', 'mouse', 'elephant']
animal.remove('dog')  # Only the first value of 'dog' is removed
print(animal)
print()
animal.remove('python') # return an error 
```

```
: ['cat', 'dog', 'mouse', 'elephant']
: 
: Traceback (most recent call last):
:   File "<stdin>", line 1, in <module>
:   File "/tmp/babel-10254-gQ/python-10254Trk", line 5, in <module>
:     animal.remove('python') # return an error 
: ValueError: list.remove(x): x not in list
```
The [[del][del]] statement is good to be used when we know the index of an item within a list. However the `remove()` method is good when we know the value we want to remove.

### `sort()`

```python
number = [2, 5, 3, 3.14, 1, -1]
number.sort()
print(number)

animal = ['dog', 'cat', 'ant']
animal.sort()
print(animal)
```

```
: [-1, 1, 2, 3, 3.14, 5]
: ['ant', 'cat', 'dog']
```
To sort values in reverse order, we can pass the argument `reverse = True` to the method.

Another thing to note is that `sort()` sorts the list *in place*, it cannot be captured. 

```python
number = [2, 5, 3, 3.14, 1, -1]
number.sort(reverse=True)
print(number)
```

```
: [5, 3.14, 3, 2, 1, -1]
```
There are other rules.. the complete set of rules is:

1. sort() returns None.
```python
number = [2, 5, 3, 3.14, 1, -1]
print(number.sort())
```
: None
```
2. sort() cannot sort both int and str. We'd get `TypeError`.

3. sort() uses *ASCIIbetical order* not alphabetical order. This way the uppercase letters come before lower case letter i.e 'Z' comes before 'a'. We can however pass `str.lower` for the `key` parameter in the method call.
```python
animal = ['Dog', 'Zebra', 'ant', 'rhinocerous', 'bull', 'cow']
animal.sort()
print(animal)
print()

animal.sort(key=str.lower)
print(animal)
```  

```
: ['Dog', 'Zebra', 'ant', 'bull', 'cow', 'rhinocerous']
: 
: ['ant', 'bull', 'cow', 'Dog', 'rhinocerous', 'Zebra']
## Exception to indentation rule
```
List is one of the few things that are exceptions to the indentation rule.

```python
animal =['dog',
  'cat', 'mouse',
             'bull'
]
print(animal)
```

```
: ['dog', 'cat', 'mouse', 'bull']
```
Another one is `print()`. It's a good idea to use `\`. `\` means "this will continues on next line".
```python
print("Hello, \
how are you?")
```

```
: Hello, how are you?
## List-like data type: strings
```
Lists aren't the only data types that represent ordered sequences of values.
```python
name = 'Kenny Nguyen'
for i in range(len(name)):
    print('str index ' + str(i) + ': ' + name[i]) 

# Let's do something cool

for i in range(len(name)):
    print(i * ' ' + name[i])
```

```
str index 0: K
str index 1: e
str index 2: n
str index 3: n
str index 4: y
str index 5:  
str index 6: N
str index 7: g
str index 8: u
str index 9: y
str index 10: e
str index 11: n
K
 e
  n
   n
    y
      
      N
       g
        u
         y
          e
           n
```
## Mutable and Immutable data types

Although lists and strings are similar in that they both represent an ordered sequence of value, they differ in important way. A list value is a *mutable* data type however a string is *immutable*. 

```python
list_of_animals = ['dog', 'cat', 'mouse']
list_of_animals[0] = 'elephant' # Changing value at index = 1
print(list_of_animals)
print()
an_animal = 'dog'
an_animal[0] = 'h' # TypeError
print(an_animal)
```

```
: ['elephant', 'cat', 'mouse']
: 
: Traceback (most recent call last):
:   File "<stdin>", line 1, in <module>
:   File "/tmp/babel-10254-gQ/python-10254ynY", line 6, in <module>
:     an_animal[0] = 'h' # TypeError
: TypeError: 'str' object does not support item assignment
```
Instead, the proper way to "mutate" a string is to use clicing and concatenation to build a *new* string.
(we can of course also re-use the variable name to essentially modify its value..))

```python
name = 'Kenny the dumbie'
print(name)
new_name = name[0:10] + 'silly'
print(new_name)
```

```
: Kenny the dumbie
: Kenny the silly
## The Tuple Data type
```
Tuples are very similar to lists except in two ways:
```
1. Syntax: Tuples are typed with parentheses, `(` and `)` instead of square brackets.
   /Although, when indexing, we still put the index number in [ ]./ 
2. Important: Tuples are *immutable*. 
```

```python
tuple = ('dog', 'cat')
for i in range(len(tuple)):
    print(tuple[i])
print()
print('.. Let\'s try to mutate a tuple... ')
tuple[0] = 'mouse'
```

```
: dog
: cat
: 
: .. Let's try to mutate a tuple... 
: Traceback (most recent call last):
:   File "<stdin>", line 1, in <module>
:   File "/tmp/babel-10254-gQ/python-10254y1A", line 6, in <module>
:     tuple[0] = 'mouse'
: TypeError: 'tuple' object does not support item assignment
```
Tuples can be used to convey to anyone reading the code that we intend for a sequence of value to *never* change. Also because they are immutable, Python's optimizations allow them to be processed faster than lists.

Python is one of the several programming languages where it's OK to use a *trailing comma*. This can be used to turn a single value into a tuple.
```python
name = ('Kenny')
print(type(name))
name  = ('Kenny', )
print(type(name))
```

```
: <class 'str'>
: <class 'tuple'>
## References
```
As we have seen, variables can be used to store `str`, `int` or `float`..
```python
spam = 42
cheese = spam
spam = 100
print(spam)
print(cheese)
```
: 100
: 42
```
In the above example, even though we change the variable `spam` to value `100`, `cheese` remains `42` because `cheese` and `spam` are two different variables that store different values, although the value of cheese was copied from spam.

*Lists don't work this way.* When we assign a list to a variable, we are actually assigning a *list reference* to the variable. A reference is a value that points to some bit of data. A list reference is a value that points to a list.

To make it easier:
```python
spam = [0, 1, 2, 3, 4, 5]
cheese = spam
cheese[1] = 'Hello'

print(spam)
print(cheese)
```
: [0, 'Hello', 2, 3, 4, 5]
: [0, 'Hello', 2, 3, 4, 5]
```
It looks a bit odd. `cheese[1] = 'Hello'` changed the `cheese` list, however the `spam` list was also changed.

This is because:
```python
spam = [0, 1, 2, 3, 4, 5]  # When the list was created, its reference was assigned to variable spam.
cheese = spam              # This line copies ONLY the list reference in spam to cheese, not the value.
cheese[1] = 'Hello'        # When cheese is modiified, it modifies the SAME list that both cheese and
                           # .. refers to.
print(spam)                # There is only ONE underlying list.
print(cheese)              # Both spam and cheese are list references of the same underlying list.
```

```
Assignment of a list works differently in that only the *list reference* is assigned to the variable(s), which point to the same list.

Modification to any reference updates the *underlying* list. 
```


## PRACTICE PROJECTS

### Comma Code

    ```
Say you have a list value like this:

spam = ['apples', 'bananas', 'tofu', 'cats']

Write a function that takes a list value as an argument and returns a string with all the items separated by a comma and a space, with and inserted before the last item. For example, passing the previous spam list to the function would return 'apples, bananas, tofu, and cats'. But your function should be able to work with any list value passed to it.
    ```python
def comma_code(alist):
    if type(alist) != list:
        print('Not a list.')
    else:
        alist[len(alist) - 1] = ', and ' + str(alist[len(alist) - 1]) 
        for i in range(len(alist) - 2):
            alist[i] = str(alist[i]) + ', '
        result = str(alist[0])
        for i in range(len(alist) - 1):
            result += str(alist[i+1])
        print(result)    
test = [1, 2, 3, 4, 5]
comma_code(test)
a_string = "hello test"
comma_code(a_string)
spam = ['apples', 'bananas', 'tofu', 'cats']
comma_code(spam)
```

```
: 1, 2, 3, 4, and 5
: Not a list.
: apples, bananas, tofu, and cats
```

### Character Picture Grid

Say you have a list of lists where each value in the inner lists is a one-character string, like this:

``` 
grid = [['.', '.', '.', '.', '.', '.'],
        ['.', 'O', 'O', '.', '.', '.'],
        ['O', 'O', 'O', 'O', '.', '.'],
        ['O', 'O', 'O', 'O', 'O', '.'],
        ['.', 'O', 'O', 'O', 'O', 'O'],
        ['O', 'O', 'O', 'O', 'O', '.'],
        ['O', 'O', 'O', 'O', '.', '.'],
        ['.', 'O', 'O', '.', '.', '.'],
        ['.', '.', '.', '.', '.', '.']]

```

You can think of grid[x][y] as being the character at the x- and y-coordinates of a “picture” drawn with text characters. The (0, 0) origin will be in the upper-left corner, the x-coordinates increase going right, and the y-coordinates increase going down.

Copy the previous grid value, and write code that uses it to print the image.
```
..OO.OO..
.OOOOOOO.
.OOOOOOO.
..OOOOO..
...OOO...
....O....
```

Hint: You will need to use a loop in a loop in order to print grid[0][0], then grid[1][0], then grid[2][0], and so on, up to grid[8][0]. This will finish the first row, so then print a newline. Then your program should print grid[0][1], then grid[1][1], then grid[2][1], and so on. The last thing your program will print is grid[8][5].

Also, remember to pass the end keyword argument to print() if you don’t want a newline printed automatically after each print() call.

#### Solution


 ```python
 grid = [['.', '.', '.', '.', '.', '.'],
         ['.', 'O', 'O', '.', '.', '.'],
         ['O', 'O', 'O', 'O', '.', '.'],
         ['O', 'O', 'O', 'O', 'O', '.'],
         ['.', 'O', 'O', 'O', 'O', 'O'],
         ['O', 'O', 'O', 'O', 'O', '.'],
         ['O', 'O', 'O', 'O', '.', '.'],
         ['.', 'O', 'O', '.', '.', '.'],
         ['.', '.', '.', '.', '.', '.']]
 for y in range(6):
     for x in range(9):
         if x == 8:
             End = '\n'
         else:
             End = ''
         print(str(grid[x][y]), end = End)

    
 ```

 ```
 : ..OO.OO..
 : .OOOOOOO.
 : .OOOOOOO.
 : ..OOOOO..
 : ...OOO...
 : ....O....

#### Explanation and then move onto the next iteration of y value. What this means is we have to put the x loop #within# the y loop as *nested loops are always executed first before the parent loop*. The `End` value is define
 
# Chapter 5 - Dictionaries and Structuring Data

Dictionary data type provides a flexible way to access and organize data. Dictionaries and lists are closely related.

Like a list, a dictionary is a collection of many values. However, unlike a list, indexes for a dictionaries can use many different data types, not just integers, i.e instead of `list[1][0]` we can have `dict[hello][english]`. 

Indexes for dictionaries are called *keys*, and a key with its *value* is called a _*key-value*_ pair.

In Python, a dictionary is typed with *braces* `{}`.

```python
myCat = {'size': 'fat', 'color': 'gray'}
print(myCat['size'])
print('My cat has a ' + myCat['color'] + ' coat')
```

```
: fat
: My cat has a gray coat
```
Dictionaries can still use integer value as keys just like lists. But they do not have to start at 0 and can be any number, i.e `dictionary = {12345: "Hello world"}`.

## Dictionaries vs. Lists

| Dictionaries          | Lists                     |
|-----------------------|---------------------------|
| Braces                | Square brackets           |
| Index can be any type | Index of ordered number   |
| Unordered, so cannot  | Ordered, so can be sliced |
| be sliced             |                           |
| `KeyError`              | `IndexError`                |
|-----------------------|---------------------------|

## `keys()`, `values()` and `items()` methods

These are the three dictionary methods that will return list-like values of dictionary's keys, values or both keys and values. The returned values aren't true lists as they cannot be modified and lack the `append()` method. But these data types (`dict_keys`, `dict_values` and `dict_items()` respectively) can be used in `for` loop.

```python
dog = {'name': 'Roku'
      ,'breed': 'Shiba Inu'
      ,'gender': 'Male'
      ,'desexed': 'Yes'}
print('Keys: ')
for i in dog.keys():  # Print all keys
    print(i)

print('Values: ')
for i in dog.values():   # Print all values
    print(i)

print('Items: ')
for i in dog.items():  # Print all items
    print(i)
print()

print('Turning everything into a list..')
test = list(dog.values())  # Turn all dict_values into a list
print(test)
print()

print('Multiple assignment..')
for k, v in dog.items():  # Multiple assignment
    print('Attribute - ' + str(k) + ': ' + str(v))

print()
print('Boolean: ')
print('Roku' in dog.values())  # Using key for Boolean. This is CASE SENSITIVE.

```

```
Keys: 
name
breed
gender
desexed
Values: 
Roku
Shiba Inu
Male
Yes
Items: 
('name', 'Roku')
('breed', 'Shiba Inu')
('gender', 'Male')
('desexed', 'Yes')
```
Turning everything into a list..
['Roku', 'Shiba Inu', 'Male', 'Yes']

Multiple assignment..
Attribute - name: Roku
Attribute - breed: Shiba Inu
Attribute - gender: Male
Attribute - desexed: Yes

Boolean: 
True
```

## The `get()` method

This method takes two arguments: a key of the value to retrive and a fall back value to return if the key does not exist.

Fallback value replaces `KeyError` in the case of no value to retrive.

```python
dog = {'name': 'Roku'
      ,'breed': 'Shiba Inu'
      ,'gender': 'Male'
      ,'desexed': 'Yes'}

print('My dog name is ' + dog.get('name', 0) + '.')

print('My dog weighs ' + str(dog.get('weight', 0)) + '.')  # Fallback value will be used.
```

```
: My dog name is Roku.
: My dog weighs 0.
```
## The `setdefault()` method

This method offers a way to set default values in one line of code.

It is a nice shortcut to *ensure that a key exists*. 

Instead of ..
```python
dog = {'name': 'Roku'
      ,'breed': 'Shiba Inu'
      ,'gender': 'Male'
      ,'desexed': 'Yes'}

if 'weight' not in dog:
    dog['weight'] = 'null'

print(dog)
```
: {'name': 'Roku', 'breed': 'Shiba Inu', 'gender': 'Male', 'desexed': 'Yes', 'weight': 'null'}
```
We can do..
```python
dog = {'name': 'Roku'
      ,'breed': 'Shiba Inu'
      ,'gender': 'Male'
      ,'desexed': 'Yes'}

dog.setdefault('weight', '13.6 kg')  
# First argument is key, second argument is value to set IF KEY DOES NOT EXIST.

print(dog)

dog.setdefault('weight', 'null')

# The following has no effect because 'weight' already has a value.
print(dog)
```
: {'name': 'Roku', 'breed': 'Shiba Inu', 'gender': 'Male', 'desexed': 'Yes', 'weight': '13.6 kg'}
: {'name': 'Roku', 'breed': 'Shiba Inu', 'gender': 'Male', 'desexed': 'Yes', 'weight': '13.6 kg'}
```

Example: Using Python to count occurences of each letter in a string.
```python
string = 'It was a bright cold day in April, and the clocks were striking thirteen.'

def count_letter(str):
    count = {}
    for char in str:
        count.setdefault(char, 0)
        count[char] = count[char] + 1
    return count

print(count_letter(string))
```

```
: {'I': 1, 't': 6, ' ': 13, 'w': 2, 'a': 4, 's': 3, 'b': 1, 'r': 5, 'i': 6, 'g': 2, 'h': 3, 'c': 3, 'o': 2, 'l': 3, 'd': 3, 'y': 1, 'n': 4, 'A': 1, 'p': 1, ',': 1, 'e': 5, 'k': 2, '.': 1}
```
## Pretty printing `pprint()` and `pformat()`

Pretty print is helpful is helpful when we want a cleaner display of dictionary that what `print()` normally provides.

```python
dog = {'name': 'Roku'
      ,'breed': 'Shiba Inu'
      ,'gender': 'Male'
      ,'desexed': 'Yes'}

print(dog)
```
: {'name': 'Roku', 'breed': 'Shiba Inu', 'gender': 'Male', 'desexed': 'Yes'}
```python
import pprint

dog = {'name': 'Roku'
      ,'breed': 'Shiba Inu'
      ,'gender': 'Male'
      ,'desexed': 'Yes'}

pprint.pprint(dog)
```

```
: {'breed': 'Shiba Inu', 'desexed': 'Yes', 'gender': 'Male', 'name': 'Roku'}
```python
import pprint
string = 'It was a bright cold day in April, and the clocks were striking thirteen.'

def count_letter(str):
    count = {}
    for char in str:
        count.setdefault(char, 0)
        count[char] = count[char] + 1
    return count

pprint.pprint(count_letter(string))
```

```
{' ': 13,
 ',': 1,
 '.': 1,
 'A': 1,
 'I': 1,
 'a': 4,
 'b': 1,
 'c': 3,
 'd': 3,
 'e': 5,
 'g': 2,
 'h': 3,
 'i': 6,
 'k': 2,
 'l': 3,
 'n': 4,
 'o': 2,
 'p': 1,
 'r': 5,
 's': 3,
 't': 6,
 'w': 2,
 'y': 1}
```
From the above we can see that `pprint` produces an output that looks much cleaner with the keys *sorted* nicely. it is helpful especially for nested list/ dictionaries.

What `pprint.pformat()` does is return the "prettified" text as a string instead of displaying it in stdout. Essentially:
```
pprint.print(aDictionary) == print(pprint.pformat(aDictionary))
```

## Nested dictionaries and lists

As we model more complicated things in life we may need to utilize dictionaries and list that contain other dictionaries and lists.

Lists are useful to contain a *ordered* series of values whereas dictionaries are useful for associate keys with values. For example here is a program that uses a dictionary that contains other dictionaries:

```python
allGuests = {'Alice': {'apples': 4, 'pretzels': 2}
	    ,'Bob'  : {'oranges': 5 , 'biscuits': 10}
            ,'Alex' : {'apples': 5, 'biscuits': 7}}

for guest in allGuests.keys():
    for item in allGuests.get(guest):
        print(guest,'is bringing',str(allGuests.get(guest).get(item)), item + '.')
```

```
: Alice is bringing 4 apples.
: Alice is bringing 2 pretzels.
: Bob is bringing 5 oranges.
: Bob is bringing 10 biscuits.
: Alex is bringing 5 apples.
: Alex is bringing 7 biscuits.
```
## PRACTICE PROJECT - Fantasy Game Inventory

   ```
You are creating a fantasy video game. The data structure to model the player’s inventory will be a dictionary where the keys are string values describing the item in the inventory and the value is an integer value detailing how many of that item the player has. For example, the dictionary value {'rope': 1, 'torch': 6, 'gold coin': 42, 'dagger': 1, 'arrow': 12} means the player has 1 rope, 6 torches, 42 gold coins, and so on.

Write a function named displayInventory() that would take any possible “inventory” and display it like the following:

Inventory:
12 arrow
42 gold coin
1 rope
6 torch
1 dagger
Total number of items: 62
   ```

```python
import pprint

Kennys_Items = {'rope': 1, 'torch': 6, 'gold coin': 42, 'dagger': 1, 'arrow': 12}

def displayInventory(dict):
    inventory = 'Inventory:\n'
    totalnum = 0
    for item, number in dict.items():
        inventory += item + ' ' + str(number) + '\n'
        totalnum += number
    inventory += 'Total number of items: ' + str(totalnum)
    return(inventory)
       
print(displayInventory(Kennys_Items))
```

```
: Inventory:
: rope 1
: torch 6
: gold coin 42
: dagger 1
: arrow 12
: Total number of items: 62
# Chapter 6 - Manipulating Strings
```
Text is one of the most common forms of data our programs will handle. 

Typing string values in Python is fairly straightforward, string data type begin and end with a *single quote*.

## String literals

### Double Quotes

 *How do we use a quote inside a string?*
 > We use *double* quote.

 Using double quotes allows us to have a single quote character in it.
 ```python
 test = "Kenny's dog is pretty naughty."
 print(test)
 ```

 ```
 : Kenny's dog is pretty naughty.

 However, if we need *both* single and double quotes in a string, we need an escape character.

### Escape Character
<<escape_char>>
 An *escape* character allows us to use characters that are otherwise impossible to put into a string.

 It consists of a backslash ( \ ) followed by the special character we want to add into the string. 
 ```python
 test = 'Kenny\'s dog says \"woof woof\".'
 print(test)
 ```

 ```
 : Kenny's dog says "woof woof".

 Despite `\"` or `\'` consist of two characters, it is commonly referred to as a singular escape character.

 List of escape characters:

 | ESCAPE CHARACTER | PRINT AS ..  |
 |------------------|--------------|
 |       <c>        |     <c>      |
 |        \'        | Single quote |
 |        \"        | Double quote |
 |        \t        |     Tab      |
 |        \n        |   Newline    |
 |        \\        |  Backslash   |

### Raw strings

 ```python
 test = r'That is Carol\'s cat'
 print(test)
 ```
 ```
 : That is Carol\'s cat

 Putting an `r` infront of a string turns it into a *raw string*. A raw string completely ignores all escape characters and prints any backslash that appears in the string.

 Raw strings are good if we are printing string values that contain many backslashes, such as the strings used for [[RegEx][regexp]] described in next chapter.

### Multiline strings with Triple Quotes

 Although we can use escape character `\n` to put a newline into a string, it is often easier to use multiline string, which is one that begins and end with either three single quotes `'''` or three double quotes `"""`. 

 Any quotes, tabs or newlines in a multiline string, that is inbetween the triple quotes, are considered part of the string. Python's indentation rules for blocks *do not* apply to lines inside a multiline string.

 ```python
 query = """ SELECT *
 FROM tb_students
 WHERE student_name = 'stupid' """
 print(query)
 ```

 ```
 : SELECT *
 : FROM tb_students
 : WHERE student_name = 'stupid'

 The above is much easier than:
 ```python
 query = 'SELECT *\nFROM tb_students\nWHERE student_name = \'stupid\''
 print(query)
 ```

 ```
 : SELECT *
 : FROM tb_students
 : WHERE student_name = 'stupid'

### Multiline Comments

 While the hash `#` character can be used to mark the beginning of a comment line, a multiline string is often used for comments that span multiple lines.
 ```python
 ''' This program is a random program'''
 # The above is a comment, and so is this line.
 print("hello world")
 ```

 ```
 : hello world

## Indexing and Slicing Strings

Similar to lists, strings also use indexes and slices. You can think of it this way
``` 
'   H   e   l   l   o       w   o   r   l   d    !   '
    0   1   2   3   4   5   6   7   8   9   10   11
```

In action:
```python
greeting = "Hello world!"
spam = greeting[0:4]
print(greeting + ' contains ' + spam + '.')
```

```
: Hello world! contains Hell.
```
## `in` and `not in` operators with strings

```python
greeting = "Hello World"

print('Hello' in greeting)
print('hello' in greeting)
print('hellO'.lower() in greeting.lower())
print('World' in greeting)
print('llo W' not in greeting)
```

```
: True
: False
: True
: True
: False
## Useful string methods
### `upper()` and `lower()`, `isupper()` and `islower()` methods
```python
spam = 'Hello World!'
spam = spam.upper()
print(spam)
print(spam.isupper())
print(spam.islower())
```

```
: HELLO WORLD!
: True
: False
```
`upper()` and `lower()` do not change the string itself because string is *immutable*. That is why we needed to re-assign the string value after invoking the method. 

These methods are helpful if we need to make case-insensitive comparison/ verification. Although `'Hello'` and `'hellO'` aren't equal, `'Hello'.lower()` is equal to `'hellO'.lower()`. 

`isupper()` and `islower()` methods return a Boolean value if the string has *at least* one letter and all letters are uppercase or lowercase respectively.
### The `isX` methods

Along with `isupper()` and `islower()`, there are other string methods that have names beginning with `is`, which return a Boolean value that describe the nature of the string.

These are:

|     <c>     | <l>                                                                                 |
|   METHODS   | returns...                                                                          |
|-------------|-------------------------------------------------------------------------------------|
|  `isalpha()`  | `True` if the string consists of only letter and is not blank.                        |
|  `isalnum()`  | `True` if the string consists of only letters and number (no space) and is not blank. |
| `isdecimal()` | `True` if the string consists of only numeric characters and is not blank             |
|  `istitle()`  | `True` if the string consists only of words that begin with a single UPPERCASE letter |
|             | _followed by only lowercase letters_.                                                 |

### The `startswith()` and `endswith()` string methods 

These return `True` if the string value they are called on begins or ends respectively with the string passed to the methods. Otherwise they return `False`.

```python
hello = "Hello World!"

print(hello.endswith('ld!'))
print(hello.endswith('d'))
```

```
: True
: False
```
These methods can be used as alternatives to the `==` operator if we need to check only whether the first or last part (rather than the whole string) of the string is equal to another string.

### The `join()` and `split()` methods

The `join()` method is useful when we want to join together a list of strings. *It is called on a string value and takes a list value*.
The *returned string* is the concatenation of each string in the passed-in arguments.

```python
', '.join(['cat','dog'])
```

```
: 'cat, dog'
```
The string that `join()` method calls on is inserted in between each string of the list arguments. It acts as the delimiter or separator.

The `split()` method is opposite. *It is called on a string value and takes a string argument*.
The *returned list* contains the strings that were separated by the string that was in passed as the argument.

```python
'Hello World'.split()
```

```
: ['Hell', ' W', 'rld']
```
If left the argument in `split()` is left empty, the default value is set to a whitespace character, meaning that the string which the method is called upon would be splitted at where the space, tab or newline characters are found.

```python
'Hello World!'.split('l')
```

```
: ['He', '', 'o Wor', 'd!']
```
*The argument/ delimited that is passed in `split()` _is not_ included in the returned list at all.*

### Justifying text with `rjust()`, `ljust()` and `center()`

The `rjust()` and `ljust()` methods return a *padded* version of the string they are called on. Padding just means that spaces were inserted to either *left or right* respectively of the text. This is to "justify" the text.

```python
test = "Hello World!"
print(test)
print(test.rjust(20))  # This add 20 spaces to the left of test, the result is a right-justified version of test.
```

```
: Hello World!
:         Hello World!
```
We can also use the second argument, which defaults to a single space.

```python
test = "Hello World!"
print(test.rjust(20, '*'))
```

```
: ********Hello World!
```
`center()` works similarly to `rjust()` and `ljust()` except it centers the text by adding the character to both sides.

```python
test = "Hello World!"
print(test.center(20, '*'))
```

```
: ****Hello World!****
```
Notice how the total number of char will end up being equal to the first argument of `center()`. In the above example it's 20.

```python
print(len("Hello World!".center(20)))
```

```
: 20
```
These methods are useful when we want to print tabular data that needs correct spacing.

For example..
```python
picnic_items = {'Sandwiches' : 20
               ,'Spring Rolls': 10
               ,'Biscuits' : 15
               ,'Cookies' : 15
               ,'Ice-Creams': 100
               ,'Boardgames': 5}
print("Picnic Items".center(40,'=') + '\n' + 'Items'.center(20) + 'Amount'.rjust(20))
for food, number in picnic_items.items():
    print(food.ljust(20,'.') + str(number).rjust(20))
```

```
: ==============Picnic Items==============
:        Items                      Amount
: Sandwiches..........                  20
: Spring Rolls........                  10
: Biscuits............                  15
: Cookies.............                  15
: Ice-Creams..........                 100
: Boardgames..........                   5
```
As above using `rjust()`, `ljust()` and `center()` let us ensure that strings are neatly aligned even if we aren't sure how many characters long our strings are.
### Removing whitespace with `strip()`, `rstrip()`, `lstrip()`

Sometimes we want to strip off whitespace characters from a string, either from left side, right side or both. Whitespace characters include space, tab and newline. 

```python
test = '     Hello World!!!   '

print(test)
print(test.strip())
print(test.rstrip())
print(test.lstrip())
```

```
: Python 3.7.3 (default, May 13 2019, 12:59:09) 
: [GCC 7.4.0] on linux
: Type "help", "copyright", "credits" or "license" for more information.
:     Hello World!!!   
: Hello World!!!
:      Hello World!!!
: Hello World!!!
: python.el: native completion setup loaded
```

Or we can also pass a string argument which specifies which characters on the ends should be stripped:
```python
spam = 'SpamSpamBaconSpamEggsSpamSpam'
print(spam.strip('maSp'))
```

```
: BaconSpamEggs
```
`strip('maSp')` strips any occurences of a, m, S and p from both ends of the string `spam` until both ends aren't one of `[m, a, S, p]`. The order of the characters in the string argument *does not matter*. `strip('ampS')` does the same thing as `strip('Spam')` or etc..
### Copying and pasting string with `pyperclip` module

The pyperclip module has `copy()` and `paste()` functions that can send text to and receive text from the host computer's clipboard. Sending the output of the program to the clipbpard makes it easy to paste it to an email, word processor or some other applications. 

Pyperclip does not come with Python therefore we have to do `pip install pyperclip`. 

# Chapter 7 - Pattern matching with RegEx
<<RegEx>>
Regular expressions are similar to seraching for text by pressing `Ctrl-F` on most applications however it is *the next step*. RegEx allows you to specify a *pattern* of text to search for.

RegExs are helpful and is the back-end search engine of most modern text editors and word processors like Words and Excel .etc. RegExs are huge time-savers, not just for end-users but for programmers.

Some even argues that before one is taught how to program, he should be taught RegEx. It can mean the difference between solving a problem in 3 steps and solving it in 3000 steps.

## FInding patterns of text without RegEx

Say we want to find a phone number in a string. We know the pattern, three numbers + a hyphen + three number + a hyphen then four number. E.g: 999-999-9999.

Let's write a function named `isPhoneNumber()` to check whether a string matches this pattern, returning either True or False.

```python
def isPhoneNumber(text):
    if len(text) != 12:
        return False
    for i in range(3):
        if not text[i].isdecimal():
            return False
    if text[3] != '-':
        return False
    for i in range(4, 7):
        if not text[i].isdecimal():
            return False
    if text[7] != '-':
        return False
    for i in range(8, 12):
        if not text[i].isdecimal():
            return False

    return True

print(isPhoneNumber('999-999-9999'))
print(isPhoneNumber('9999-999-999'))
print(isPhoneNumber('hello world'))

def findPhoneNumber(text):
    for i in range(len(text)): 
        chunk_of_text = text[i:i+12]
        if isPhoneNumber(chunk_of_text):
            print('Found phone number!!!!', chunk_of_text)

test = " Hello World! there is a phone number in this chunk of text and it's definitely one hundred person will be at the very end of the string and that is definitely 929-998-0089 "

findPhoneNumber(test)
```

```
: True
: False
: False
: Found phone number!!!! 929-998-0089
```
As we could see the `isPhoneNumber` does several checks to see whether the string `text` is a valid phone number. If any of these fails the function would return `False`. 

For larger and more complicated strings, we would have to even perform *more checks*, by adding more code.

The `findPhoneNumber` runs iterations of the `for` loop. Each iteration creates a new chunk of 12 characters and goes through `isPhoneNumber` once. This loop goes through the entire string and print any `chunk_of_text` it finds that satisfies the `isPhoneNumber()` function.

While the strings we used in the above example are short. It could be millions of characters long and the program would till run in less than a second. A smilar program with RegEx would also run in less than a second, however RegEx makes it quicker to write these program.

## Finding pattern of text with RegEx

Coming back to `isPhoneNumber()`,  we will be using RegEx this time.

Regular Expressions are descriptions for a pattern of text. For example, a `\d` in a regex stands for a digit character that is any single numeral from 0 to 9, i.e `'\d\d\d-\d\d\d-\d\d\d\d'` 

RegExes can be much more complicated, for example adding a `{3}` after a patter is like saying "Match this pattern three time", i.e `'\d{3}-\d{3}-\d{4}'`

## Creating RegEx Objects

All the regex functions in Python are in the `re` module that comes with Python. We have to import it.

Passing a string value representing your regular expression to `re.compile()` returns a RegEx pattern object, or a *RegEx object*.

When creating a RegEx object, we should use a *raw string* so that we are passing a literal backslash, not an [[escape_char][/escape character/]]. This is because RegExes frequently use backslashes in them. Without passing a raw string we'd be typing many extra backslashes.

## Matching RegEx Objects

RegEx Objects have a `search()` method that searchs the string it is passed for any matches to the regexp itself.

```python
import re
phoneNumber_regex = re.compile(r'\d\d\d-\d\d\d-\d\d\d\d')
test = phoneNumber_regex.search(" Hello World! there is a phone number in this chunk of text and it's definitely one hundred person will be at the very end of the string and that is definitely 929-998-0089")
print(test)
print(type(test))
print(test.group())
```

```
: <re.Match object; span=(160, 172), match='929-998-0089'>
: <class 're.Match'>
: 929-998-0089
```
The `search()` method returns None if the regex pattern is not found in the passed string. If the pattern is found, the `search()` method returns a *Match* object `<class 're.Match'>`.  Match objects have a method `group()` that returns the actual matched text (`match ='xxx'`) from the searched string. 

## REVIEW of RegEx

There are several steps to using RegEx in Python. Each step is fairly simple.

1. Import the regex module with `import re`.
2. Create the Regex object with `re.compile()` function. Use a *raw string*.
3. Pass the string we want to search into the regex obect's `search()` method. This will return a `Match` object.
4. Call the `Match` object's `group()` method to return a string of the actual matched text.

## Grouping of RegEx with Parentheses

Coming to our phoneNumber_regex example, what we can also is seperate the area code from the rest of the phone number by adding parentheses in the regex object. This in turn create *groups* in the regex.

```python
import re
phoneNumber_regex = re.compile(r'(\d\d\d)-(\d\d\d-\d\d\d\d)')
test = phoneNumber_regex.search(" Hello World! there is a phone number in this chunk of text and it's definitely one hundred person will be at the very end of the string and that is definitely 929-998-0089")
print(test)
print(test.group(1))
print(test.group(2))
print(test.group())
print(test.groups())
```

```
: <re.Match object; span=(160, 172), match='929-998-0089'>
: 929
: 998-0089
: 929-998-0089
: ('929', '998-0089')
```
In the above example, instead of just doing `'\d\d\d-\d\d\d-\d\d\d\d'`, we added parentheses to seperate the regular expression into two groups:

| GROUP 1  | GROUP 2         |
| `(\d\d\d)` | `(\d\d\d-\d\d\d)` |

By passing the integer which represents the group to the `group()` method, we can collect different parts of the matched text. Passing `0` or nothing to the `group()` method will return the entire matched text.

In the last line of the above, we saw the `groups()` method (plural). This method returns all the groups at once in form of `tuple`. This, in combination with [[multiple_assignment][multiple assignment]] can be very handy.We can assign several values to variables.

### Matching a parenthesis in regex

As parentheses have a special meaning in regular expressions, to match a parenthesis in text we have to escape the `(` and `)` characters with a backslash. The `\(` and  `\)` escape characters in the *raw string* passed to `re.compile()` will match actual parenthesis character.

## Matching multiple groups with Pipe

We can use the pipe `|` character to match one of many expressions.

For example the regular expression `r'Batman|Robin'` will match either `'Batman'` *or* `'Robin'`.

When both of the expressions exist in the searched string, the *first* occurence of the matching text will be returned as the `Match` object, i.e:
```python
import re
GothamRegex = re.compile(r'Batman|Robin')
test1 = GothamRegex.search('In Gotham city we have both Robin and Batman.')
print(test1.group())
test2 = GothamRegex.findall('In Gotham city we have both Robin and Batman.')  # Refer to findall() method
print(test2)
```

```
: Robin
: ['Robin', 'Batman']
```
We can also use the pipe character in combination with grouping parentheses to match one of several strings, i.e:
```python
import re
findBatStuff = re.compile(r'Bat(man|mobile|car|phone|computer)')  # the things in parentheses are GROUP 1

test1 = findBatStuff.search('Hello, in this string there is an item that belongs to the Bat and it\'s the Batmobile.')
print('found the', test1.group())
print(test1.group(1))
``` 

```
: found the Batmobile
: mobile
```
If we need to find an actual pipe character, we can escape it with backslash `\|` since in a raw string, this will be read as a literal `|`. 

## `findall()` method

The `search()` method returns the _first_ expression that is matched in a string in a `Match` type object. Instead we could use `findall()` which return *every match* in the searched string in a `List` object. The returned list is a list of all the matched (sub) strings in the searched string.

```python
import re
GothamRegex = re.compile(r'Batman|Robin')
test2 = GothamRegex.findall('In Gotham city we have both Robin and Batman. We also have Batman and Robin')  # Refer to findall() method

for i in range(len(test2)):
    print('Match ' + str(i) + ': ' + test2[i])

```

```
: Match 0: Robin
: Match 1: Batman
: Match 2: Batman
: Match 3: Robin
```
If there are groups in the regular expressions, `findall()` will return a list of tuples of strings instead of strings. 

## OPTIONAL matching using `?`

Sometimes we want to match a patern only *optionally*. That is the regex should find a match *whether or not* that bit of text is there. To do this we use the `?` character to flag the group that *precedes* it as an optional part of the pattern.

```python
import re
batRegex = re.compile(r'Bat(wo)?man')  # the 'wo' bit is optional, due to the ? flag

test1 = batRegex.search('The Adventure of Batman')
print(test1.group())  

test2 = batRegex.search('The Adventure of Batwoman')
print(test2.group())
```

```
: Batman
: Batwoman
```
## Matching zero or more with asterisk `#` 

We can the asterisk in regex to match zero or more occurence of the group that precedes the `*` flag. This means the group can be completely absent or repeated many times.

```python
import re
batRegex = re.compile(r'Bat(wo)*man')

test1 = batRegex.search('The adventure of Batman')
print(test1.group())
test3 = batRegex.search('The adventure of Batwowowowowowoman')
print(test3.group())
test2 = batRegex.search('The adventure of Batwowman')
print(test2 == None)
```

```
: Batman
: Batwowowowowowoman
: True
```

Again, if we actually want to match `*`, escape it with `\*`.

## Matcing one or more with plus `+`

Similar to asterisk, `+` gives us the ability to match one or more occurences of the group. If there is zero occurence it will not match. Unlike asterisk, the group preceding the `+` flag MUST appear *at least one*. It is not optional.

```python
import re
batRegex = re.compile(r'Bat(wo)+man')

test1 = batRegex.search('The adventure of Batman')
print(test1 == None)
test3 = batRegex.search('The adventure of Batwowowowowowoman')
print(test3.group())

```

```
: True
: Batwowowowowowoman
```
Again, to match `+`, use `\+` in the raw string.

## Matching specific repetitions with Curly Brackets `{}`

We can use curly brackets to match patterns that repeat a specific number of times.

For example `(Ha){3}` will match `'HaHaHa'` but not `'HaHa'` since the later only has two repeats of `(Ha)`.

Instead of just one number we can also use a range by writing a min, followed by a comma then the max within the curly bracket.

```python
import re
hahaha = re.compile(r'(Ha){3,5}')

print(type(hahaha))
print(type(hahaha.search('HaHaHello')))

print(type(hahaha.search('HelloHaHaHaHa')))

print((hahaha.search('HelloHaHaHaHa')).group())
```

```
: <class 're.Pattern'>
: <class 'NoneType'>
: <class 're.Match'>
: HaHaHaHa
```

We can also *leave out* the min and max in the curly brackets to leave either *unbounded*.

Curly brackets make our regex shorter, i.e instead of `(Ha)(Ha)(Ha)` we can just do `(Ha){3}`.

## Greedy and nongreedy matching

Since `(Ha){3,5}` can match three, four or five instances of `Ha` in string `HaHaHaHa`, why does the  `Match` object's `group()` call returns `HaHaHaHa` but not `HaHaHa` which is *shorter*? After all these are both valid matches of the regular expression  

This is because Python's regex are *greedy* by default. This means that in ambiguous situations they will match the longest string possible.

Instead of using greedy matching which is default, what we can do is flag a `?` right after the curly brackets.

A `?` when used with the curly brackets declares a *nongreedy* match whereas in normal situations flag an optional group. These two are entirely unrelated.

```python
import re
hahaha = re.compile(r'(Ha){3,5}?')  # non greedy

print((hahaha.search('HelloHaHaHaHa')).group())

```

```
: HaHaHa
```
## SHORTHAND CODES FOR CHARACTER CLASSES

| Shorthand character class | Representation                                |
|---------------------------|-----------------------------------------------|
|            <c>            | <l>                                           |
|            \d             | Any numeric digit from 0 to 9.                |
|            \D             | Any character that is *not* a digit from 0 to 9 |
|            \w             | Any letter, numeric digit, or the underscore  |
|                           | character. Think of it as matching 'word'     |
|                           | character.                                    |
|            \W             | Any character that is *not* a letter, numeric   |
|                           | digit, or the underscore character.           |
|            \s             | Any space, tab or newline character. Think of |
|                           | this as matching 'space' character.           |
|            \S             | Any character that is not space character.    |

Example: `r'\d+\s\w+'` matches a string that contains at least a digit, followed by space and then one word.

```python
import re
whobringswhat = 'Kenny is bringing 2 biscuits. John is bringing 3 cookies. Mai is bringing 5 coconuts.\
 Justin is bringing 5 knives. Carla is bringing 5 dogs, for some reason.'
print(whobringswhat)

def finditems(info):
    findhowmany_and_watch = re.compile(r'\d+\s\w+')
    match = findhowmany_and_watch.findall(info)
    return match  # The return of findall is a list. No need to call group().

print(finditems(whobringswhat))
```

```
: Kenny is bringing 2 biscuits. John is bringing 3 cookies. Mai is bringing 5 coconuts. Justin is bringing 5 knives. Carla is bringing 5 dogs, for some reason.
: ['2 biscuits', '3 cookies', '5 coconuts', '5 knives', '5 dogs']
```
### Matching our own custom character classes

Sometimes we find the generic character classes too broad. We can define our own character class using square brackets.
For example `[AaEeUuIiOo]` matches any vowel, irrespective of casing.

We can do range using hyphen, e.g `[a-zA-Z0-9]` will match all lower case letters, upper case letters and numbers.

`[0-5.]` matches any digit from 0-5 and a period. We do need need to escape the `.` because inside the square brackets regex are not interpreted as such, things like `?` (optional), `*` (zero or more) ..etc.. don't work.

If we place a caret character `^` just after the character class' opening bracket. We make it a negative character class. A negative character class matches thing that are *not* in the character class.

## The Caret `^` and Dollar Sign `$` 

A caret symbol can be used at the start of regex to indicate that a match must occur at the beginning of the searched text.

A dollar sign symbol, placed at the end of the regex indicates the string must *end* with this regex pattern.

We can use these together, to match the entire string with the regex.

## The #WILDCARD#

The `.` (dot) character in a regex is called a wildcard. It matches any character except for a new line.

```python
import re 
atRegex = re.compile(r'.at')
string = 'Batman has a cat. The cat is fat and it also has a hat.'

print(atRegex.findall(string))
```

```
: ['Bat', 'cat', 'cat', 'fat', 'hat']
```
`.*` matches everything and anything.

The dot star uses greedy match. It always tries to grab as much text as possible.

To use the dot character to match everything *including* a newline, pass `re.DOTALL` as the second argument to `re.compile()`.

```python
import re
find_name  = re.compile(r'\s+.*', re.DOTALL)

string = 'Everythingafterthis will be captured, including the new line which is after this dot.\nThis is pretty awesome.'
print(string)
print()
print(find_name.search(string).group())
```

```
: Everythingafterthis will be captured, including the new line which is after this dot.
: This is pretty awesome.
: 
:  will be captured, including the new line which is after this dot.
: This is pretty awesome.
```
## Case-insensitive matching

Like the `re.DOTALL` second argument, we can use `re.I` or `re.IGNORECASE` as the second argument within `re.compile()` to make the regex case-insensitive.

## `re.VERBOSE`

The normal regular expression, so-called "compact" regular expressions are pretty hard to read. A few months or years on, it would be difficult even for the us to understand what we meant at the time of code writing.

For this, what we'd need is inline documentation.

This is doable with something called *verbose regular expressions*. A verbose regex is different from a compact regex in two ways:
- Whitespace is ignored. Spaces, tabs and carriage returns are not matched as spaces, tabs and carriage returns. They are not matched at all.
- Comments are ignored. 

In order to use verbose regular expressions, we need to pass an extra argument when working with them: `re.VERBOSE`. This is a cosntant defined in the `re` module that signals that the pattern should be treated as verbose regular expression.

## PRACTICE PROJECT - Phone Number and Email Address Extractor

Say you have the boring task of finding every phone number and email address in a long web page or document. If you manually scroll through the page, you might end up searching for a long time. But if you had a program that could search the text in your clipboard for phone numbers and email addresses, you could simply press CTRL-A to select all the text, press CTRL-C to copy it to the clipboard, and then run your program. It could replace the text on the clipboard with just the phone numbers and email addresses it finds.

Whenever you’re tackling a new project, it can be tempting to dive right into writing code. But more often than not, it’s best to take a step back and consider the bigger picture. I recommend first drawing up a high-level plan for what your program needs to do. Don’t think about the actual code yet—you can worry about that later. Right now, stick to broad strokes.

For example, your phone and email address extractor will need to do the following:

    Get the text off the clipboard.

    Find all phone numbers and email addresses in the text.

    Paste them onto the clipboard.

Now you can start thinking about how this might work in code. The code will need to do the following:

    Use the pyperclip module to copy and paste strings.

    Create two regexes, one for matching phone numbers and the other for matching email addresses.

    Find all matches, not just the first match, of both regexes.

    Neatly format the matched strings into a single string to paste.

    Display some kind of message if no matches were found in the text.

This list is like a road map for the project. As you write the code, you can focus on each of these steps separately. Each step is fairly manageable and expressed in terms of things you already know how to do in Python.

### Resolution

```python
## HOW-TO USE
# 1. Copy a bunch of text to clipboard
# 2. Run this program
# 3. Profit
## 

import re 
import pyperclip as pyp

text = pyp.paste()


## Step 1 - Create a Regex for Phone Number

phone_no_regex = re.compile(r'''(
                            (\d{3}|\(\d{3}\))?    # area code - optional: 3 digits or 3 digits within brackets
                            (\s|-|\.)?            # seperator - optional: a space, a dash, or a dot
                            (\d{3})               # first 3 digits
                            (\s|-|\.)             # seperator 
                            (\d{4})               # last 4 digits
                            (\s*(ext|x|ext.)\s*\d{2,5})?  # extension - optional: zero or more space, then ext  
                                                          # then zero or more space then 2 to 4 digits
                             )'''
                            ,re.VERBOSE)

## Step 2 - Create a Regex for Email Address

email_regex = re.compile(r'''(
                         [a-zA-Z]{1}           # starting with first letter
                         [a-zA-Z0-9._-]+       # legal email characters
                         @{1}                  # one 'at'
                         [a-zA-Z0-9]+          # domain name
                         \.{1}                 # a dot
                         [a-zA-Z]{2,5}            # last bit of domain name, between 2-4 characters
                          )'''
                            ,re.VERBOSE)

# This isn't a regex that will match every single email address, but it will match almost all.


## Step 3 -- Create a function that finds all and returns phone and email

def find_phoneNo_and_email(text):
    text = str(text)
    
    phoneNo = phone_no_regex.findall(text)
    emails =  email_regex.findall(text)
    
    results = []
    
    sepRegex = re.compile(r'\s|\.')
    # List phone numbers:
    
    print('Found', str(len(phoneNo)), 'phone numbers:')
    for number in phoneNo:
        print('-', sepRegex.sub('-',number[0]))
        results.append('- ' + sepRegex.sub('-',number[0]))
    
    print()
    
    # List emails:
    
    print('Found', str(len(emails)), 'email addresses:')
    for i in range(len(emails)):
        print('-', emails[i])
        results.append('- ' + emails[i])
    
    listOfresults = ''
    for i in range(len(results)):
        listOfresults += results[i] + '\n'
    
    pyp.copy(listOfresults)
    
    print('\nList of results has been copied to clipboard.')
    
    return None
find_phoneNo_and_email(text)
```

# Chapter 8 - Input validation

Input validation code checks that values entered by the user, e.g: from `input()` function, are formatted correctly.

For example, if we want our user to enter their age, our code should not accept nonsensical answers such as negative numbers or words. 

Input validation is helpful that it can prevent bugs or security vulnerabilities. For example, if we write a `withdrawfromaccount()` function, we need to ensure that the withdraw amount is a positive number. Otherwise it would end up adding money!

Without any libraries, typically we can perform input validation by repeatedly asking the user for input until they enter a valid value e.g:
```python
while True
	print('Enter your age')
	age = input()
	try:
		age = int(age)
	except:
		print('Please use numerical digits.')
		continue
	if age < 1:
		print('Please enter a positive number.')
		continue
	break
print(f'Your age is {age}.')
```

In the above module, user will be prompted for their age until they enter a positive number. If they enter a non-numerical value, the `continue` statement within the `except` clause will bring them back to the beginning of the `while` loop. If they enter a negative number, the `continue` statement within the `if` clasue will also bring them back to the beginning of the loop.

If we do this for every input, however, writing it quickly becomes tedious. Moreover we may miss certain cases and allow invalid input to pass through our checks. Therefore, it's handy learn how to use the third-party *PyInputPlus* module for input  validation.

## PyInputPlus

The PyInputPlus library contains functions similar to `input()` for several kinds of data like numbers, dates, email addresses and more. For invalid inputs, such as poorly formatted date or a number that's not within an intended range, PyInputPlus will reprompt the users for input just like our manual code. The library also has other useful features like a limit for the number of times it reprompts useres and a timeout function if users are required to respond within a time limit.

PyInputPlus isn't part of the standard library, so you have to install it using pip.

## PyInputPlus common functions

- *inputStr()* is like the built-in `input()` function but has the general PyInputPlus features. We can also pass a custom validation function to it.
- *inputNum()* ensures the user enters a number and returns an int or float, depending on if the number has a decimal point.
- *inputChoice()* ensures the user enters one of the provided choices.
- *inputMenu()* is similar to `inputChoice()` but provides a menu with numbered or lettered options.
- *inputYesNo()* ensures the user enters a "yes" or "no" response.
- *inputBool()* is similar to `inputYesNo()`, but takes a "True" or "False" response and returns a boolean value.
- *inputEmail()* ensures the user enters a valid email address.
- *inputFilepath()* ensures the user enters a valid file path and filename. It can also optionally check if that file with that name exists.
- *inputPassword()* is like the built-in `input()`, however it displays * characters as teh user types so that passwords or other sensitive information aren't displayed on the screen.
-------------------------

Example:

With only two lines (including the import line), we can implement a integer input validation:
```python
import pyinputplus as pyip

response = pyip.inputNum()
```

[[./images/pyipNum.png]]

We can also do a prompt:
```python
import pyinputplus as pyip

response = pyip.inputInt(prompt= 'Enter a Number: ')
```

[[./images/inputIntwithprompt.png]]

## `inputNum` | `inputInt` | `inputFloat` - implement range limit

Range limit can be implemented by optional keyword arguments like `min`, `max`, `greaterThan` and `lessThan`. 

```python
import pyinputplus as pyip

response = pyip.inputInt(prompt= 'Enter a Number: ', min= 5, max= 10)
```

``` 
Enter a Number: 1
Number must be at minimum 5.
Enter a Number: 11
Number must be at maximum 10.
Enter a Number: 2
Number must be at minimum 5.
Enter a Number: 7
```

## the `blank` keyword argument

By default, blank input isn't allowed unless the `blank` keyword argument is set to `True`.

If `False`:
``` 
[kkennynguyen Input Validation]$ python work.py 
Enter a Number: 
Blank values are not allowed.
Enter a Number: 
```

If `True`:
``` 
[kkennynguyen Input Validation]$ python work.py 
Enter a Number: 
[kkennynguyen Input Validation]$ 
```

## limit | timeout

By default, the PyInputPlus functions will continue to ask the user for valid input for as long as the program runs. If we'd like a function to stop asking the user for input after a certain number of tries or certain amount of time, we can use the `limit` and `timeout` keyword argument.

The `limit` keyword argument accepts an integer value to determine how many attempts a PyInputPlus function will make to receive a valid input before giving up. After this amount of tries, Python will throw this error: `pyinputplus.RetryLimitException`.

The `timeout` keyword argument accepts an integer value to determine how many seconds the user has to enter a valid input before InputPlus function gives up. If the user enters an input after this amount of time, Python will throw this error: `pyinputplus.TimeoutException`. 

## default keyword argument

When we use the above limit/timeout keyword arguments and also pass a `default` keyword argument, the function returns the default value instead of raising an exception.

```python
import pyinputplus as pyip

response = pyip.inputInt(prompt= 'Enter a Number: ', min=5, max=10, limit=3, default='N/A')

print(response)
```

``` 
[kkennynguyen Input Validation]$ python work.py 
Enter a Number: 2
Number must be at minimum 5.
Enter a Number: 2
Number must be at minimum 5.
Enter a Number: 2
Number must be at minimum 5.
N/A
```

## The `allowRegexes` and `blockRegexes` keyword arguments

These two keyword arguments take a list of regular expression strings to determine what the pyinputplus function will accept or reject as valid input.

For example, this module only accepts Roman numerals *in addition to the usual numbers*. Note that we used `inputNum`.

```python
import pyinputplus as pyip

response = pyip.inputNum(allowRegexes=[r'(I|V|X|L|C|D|M)+', r'zero'])
print(response)
```

``` 
[kkennynguyen Input Validation]$ python work.py 
test
'test' is not a number.
asdas
'asdas' is not a number.
XVII
XVII
```

We can of course also use `BlockRegexes`. For example, let's not allow input that starts with numbers 1, 3, 5, 7, 9.

```python
import pyinputplus as pyip

response = pyip.inputNum(blockRegexes=[r'^[13579]'])
```

``` 
[kkennynguyen Input Validation]$ python work.py 
12
This response is invalid.
14
This response is invalid.
23
```

If we specify both an `allowRegexes` and `blockRegexes`, *the allow list overrides the block list.*

For example, in function below we don't accept anything that starts with /cat/ but accepts /category/:

```python
import pyinputplus as pyip

response = pyip.inputStr(allowRegexes=[r'category'], blockRegexes=[r'^cat'])
```

``` 
[kkennynguyen Input Validation]$ python work.py 
catepillar
This response is invalid.
cat
This response is invalid.
category
```

## `inputCustom()`

We can write a custom function to perform our own custom validation logic by passing the function to `inputCustom()`. 

Let's go through an example: Implement a user validation that accepts a series of digit that adds up to 10.

There is no pyinputplus.inputAddsUptoTen(), however we can create our own function that:
- Accepts a single striing argument of what the user entered.
- Raises an exception if the string fails validation
- Returns None if inputCustom() should return the string unchanged.
- Returns a non-None value of inputCustom() should return a different string from the one user entered.
- Is passed as the first argument to inputCustom().

```python
import pyinputplus as pyip


def addsUpToTen(numbers):
    num_list = list(numbers)
    for i, digit in enumerate(num_list):
        num_list[i] = int(digit)
    numsum = sum(num_list)
    if numsum != 10:
        raise Exception("The digits must add up to 10, not %s." % (numsum))
    return int(numbers)


response = pyip.inputCustom(addsUpToTen)
```

``` 
$ python work.py 
12345
The digits must add up to 10, not 15.
123
The digits must add up to 10, not 6.
1234
```

The inputCustom() function also supports the general PyInputPlus features, such as `blank`, `limit`, `timeout`, `default`, `allowRegexes` and `blockRegexes` keyword arguments.

## Project: How to keep an idiot busy for hours

Let’s use PyInputPlus to create a simple program that does the following:

    Ask the user if they’d like to know how to keep an idiot busy for hours.
    If the user answers no, quit.
    If the user answers yes, go to Step 1.

Of course, we don’t know if the user will enter something besides “yes” or “no,” so we need to perform input validation. It would also be convenient for the user to be able to enter “y” or “n” instead of the full words. PyInputPlus’s inputYesNo() function will handle this for us and, no matter what case the user enters, return a lowercase 'yes' or 'no' string value.

When you run this program, it should look like the following:

Want to know how to keep an idiot busy for hours?
sure
'sure' is not a valid yes/no response.
Want to know how to keep an idiot busy for hours?
yes
Want to know how to keep an idiot busy for hours?
y
Want to know how to keep an idiot busy for hours?
Yes
Want to know how to keep an idiot busy for hours?
YES
Want to know how to keep an idiot busy for hours?
YES!!!!!!
'YES!!!!!!' is not a valid yes/no response.
Want to know how to keep an idiot busy for hours?
TELL ME HOW TO KEEP AN IDIOT BUSY FOR HOURS.
'TELL ME HOW TO KEEP AN IDIOT BUSY FOR HOURS.' is not a valid yes/no response.
Want to know how to keep an idiot busy for hours?
no
Thank you. Have a nice day.

```python
import pyinputplus as pyip

while True:
    answer = pyip.inputYesNo(
        prompt='Want to know how to keep an idiot busy for hours?\n',
        allowRegexes=[r'y|Y|n|N']
    )
    if answer.lower() == 'no':
        print('Thank you. Have a nice day')
        break

```

# Chapter 9 - Reading and writing files

If we want our data to persist after the program finishes running, we need to save it to a file.

## Backslashes on Windows and Forward Slash on OS X and Linus

   In Python os module, there is a `os.sep` variable that is set to the correct folder-seperating slash for the OS running the program.
```python
import os
print(os.sep)
```

```
: /
(It would be a back slash on Windows)
```
If we want our program to work on both Windows and Unix-based operating systems, we need to write our Python program to handle both cases.

This is simple to do with `os.path.join()` function. If we pass it the string values of individual files and folder names in our path, `os.path.join()` will return a string with a file path using the correct path seperator.

```python
import os
print(str(os.path.join('usr','bin','spam')))
```

```
: usr/bin/spam
```
Running this same line on Windows would have yielded `usr\\bin\\spam` (double back slashes to escape).

`os.path.join()` is also usefule when we want to create strings for filenames.

```python
fileNames = ['myfile.csv', 'myphoto.jpg']

for fileName in fileNames:
    print(os.path.join('/home','kkennynguyen','Documents', fileName))
```

```
: /home/kkennynguyen/Documents/myfile.csv
: /home/kkennynguyen/Documents/myphoto.jpg
```
## Current working directory (cwd)
<<cwd>> 

Every program that runs on our computer has a current working directory. Any filenames or path that does not begins with the root folder (=/= on Unix or =C:\= on Windows) are assumed to be under cwd.

We can get cwd as a string value with `os.getcwd()` function. We can change cwd with `os.chdir()`.

```python
import os

print(os.getcwd())

os.chdir('..')  # move one folder up
print(os.getcwd())
```

```
: /home/kkennynguyen/pCloudDrive/Documents/OrgNotes/Learning
: /home/kkennynguyen/pCloudDrive/Documents/OrgNotes
```
## Absolute vs Relative path

   - An *absolute* path always begins with the root folder.
   - A *relative* path is relative to the program's current working directory

(There are also special folder names that can be used in a path which are `.` (this directory) and `..` (parent directory).)


`.\spam.txt` and `spam.txt` are basically the same thing. `.\` is optional in a relative path.

## Create new folder with `os.makedirs()`

```python
import os
print(os.getcwd())
os.makedirs('test_folder')
```

```
: /home/kkennynguyen/pCloudDrive/Documents/OrgNotes
```
## The `os.path` module

The `os.path` module contains many helpful functions related to file names and file paths, one of which being the `os.path`join()` method to build paths in a way that will work in any OS.

Calling `os.path.dirname(/path/)` will return a string of everything that comes before the last slash in the path argument.

Calling `os.path.basename(path)` will return a string of everything comes after the last slash in the path argument.

Calling `os.path.split(path)` will return a tuple value of basename and dirname.
```python
import os
print(os.getcwd())
print('listing dir:')
print(os.listdir())
print('dirname:')
path = '/home/kkennynguyen/pCloudDrive/Documents/MeetingNotes'
print(os.path.dirname(path))
print('basename:')
print(os.path.basename(path))
print('dir and basename splitted:')
print(os.path.split(path))
print('Using the split method to split on the string in the slash seperator to get a list ..')
print(path.split(os.sep))
```

```
/home/kkennynguyen/pCloudDrive/Documents/OrgNotes
listing dir:
['MeetingNotes', 'TrainingNotes', 'BriefingNotes', 'Personal', 'Learning', 'test_folder', 'ConfigFile2904', 'OrgTutorial.html', 'OrgTutorial.org', 'ChecklistWindowsPC.org', 'QuickNotes.org']
dirname:
/home/kkennynguyen/pCloudDrive/Documents
basename:
MeetingNotes
dir and basename splitted:
('/home/kkennynguyen/pCloudDrive/Documents', 'MeetingNotes')
Using the split method to split on the string in the slash seperator to get a list ..
['', 'home', 'kkennynguyen', 'pCloudDrive', 'Documents', 'MeetingNotes']
```
## Finding File Sizes and Folder content

```python
import os 

path = os.getcwd()
print(path)

# Get Size of the file in path argument
print(os.path.getsize(path))
print()
# Get all file in the path argument
print(os.listdir(path))
print()
# Get individual size
totalsize = 0
for file in os.listdir(path):
    print(file, ':', os.path.getsize(file))
    totalsize += os.path.getsize(file)
print('Total Size:', totalsize)
```

```
/home/kkennynguyen/pCloudDrive/Documents/OrgNotes
4096
```
['MeetingNotes', 'TrainingNotes', 'BriefingNotes', 'Personal', 'Learning', 'test_folder', 'ConfigFile2904', 'OrgTutorial.html', 'OrgTutorial.org', 'ChecklistWindowsPC.org', 'QuickNotes.org']

MeetingNotes : 4096
TrainingNotes : 4096
BriefingNotes : 4096
Personal : 4096
Learning : 4096
test_folder : 4096
ConfigFile2904 : 2962
OrgTutorial.html : 15828
OrgTutorial.org : 1436
ChecklistWindowsPC.org : 2314
QuickNotes.org : 193438
Total Size: 240554
```
## Checking path validity

Many Python functions crash with an error if the non-existent path is supplied.

We can use `os.path.exists(path)` to check.

- `os.path.exists(path)` returns `True` if the file or folder referred to in the argument *exists*.
- `os.path.isfile(path)` returns `True` if the path argument exists and is a file.
- `os.path.isdir(path)` returns `True` if the path argument exists and is a folder.

## File Reading and Writing Process
There are three steps to reading or writing a file in Python
1. Call the `open()` function to return a `File` object.
2. Call the `read()` or `write()` method on the `File` object.
3. Close the file by calling the `close()` method on the `File` object.

First we create a random test.txt file..
``` sh :exports both :results output :session
echo 'Hello World' > test.txt
dir
echo
cat 'test.txt'
```

```
AutomateBoringStuff
AutomateBoringStuff.html
AutomateBoringStuff.html
AutomateBoringStuff.html
AutomateBoringStuff.org
Chapter_8_-_Reading_and_writing_files
git-cli.html
git-cli.org
LinuxLearning.org
nav-sprite-global_bluebeacon-V3-1x_optimized._CB483188077__2019-05-08_22-22-17.png
pexels-photo-414612_2019-05-10_22-30-19.jpeg
SQL_Essential_Training.org
test.txt
```
Hello World
```

Then we can open the file in Python..
```python
import os

testFile = open(os.getcwd() + os.sep + 'test.txt')

print(type(testFile))

print(testFile.read())
## We can also use readlines() method to get a list of string, one string for each line of text


```

```
: <class '_io.TextIOWrapper'>
: Hello World
```
In order to *write* to a file, we need to open it in *write mode*  (or *append mode*). We can't write to a file that we have opened in read mode. Write mode allow us to write on the file. Append mode wil lappend text to the end of the existing file.

```python
import os 

testFile = open(os.getcwd() + os.sep + 'test.txt', 'w')  ## write
testFile.write('Hello World v1!')
testFile.close()
testFile = open(os.getcwd() + os.sep + 'test.txt', 'a')  ## append
testFile.write('\nMy name is Kenny.')
testFile.close()
testFile = open(os.getcwd() + os.sep + 'test.txt')  ## read
print(testFile.read())

```

```
: Hello World v1!
: My name is Kenny.
# Chapter 10 - Organizing files
```
## The `shutil` module

The `shutil` module stands for *shell utilities*. It has functions to let us copy, move, rename and delete files in our Python programs. To use this module do:
```python
import shutil
```

## Copying Files and Folders

The `shutil` module provides function for copying files as well as entire folders.

To copy do:

```python
shutil.copy(source, destination)
```
Both source and destination are strings. If destination is a filename, it will be used as the new name of the copied file.

The `shutil.copy()` function returns a string of the path of the copied file.

Example:
```python
import shutil, os

os.chdir('`')  # go to home dir

shutil.copy('./Documents/foo.txt', './Notes/texts')
shutil.copy('./Documents/eggs.txt', './Notes/eggs2.txt')
```

``` 
`/Notes/texts/foo.txt
`/Notes/egg2.txt
```

The second call copies the file but also give it a new name.

### `shutil.copytree()`

While `shutil.copy()` copies a single file, `shutil.copytree()` copy an *entire folder* and every folder and file contained within it.

## Moving and renaming files and folders

Calling `shutil.move(source, dest)` will move the file or folder at `source` to the path `dest` and will return a string of the absolute path of the new location.

Similarly to `shutil.copy()`, if `dest` is a folder, the `source` file gets moved into `dest` and keeps its current filename.

If `dest` is a filename, the `source` file is moved and renamed.

We should *be careful* when using `move()` because if there is an existing file in the destination folder with the same name, the file would be overwritten.

If a folder with the specified name does not exist, the `source` file will get renamed into what ever specified in `dest`. 

## Permanent delete

We can delete a single file or a single empty folder with functions in the `os` module, where as to delete a folder and all of its contents, we use the `shutil` module.

This deletes the file at `path`.
```python
os.unlink(path)
```

This delete the folder at `path`. This folder must be empty.
```python
os.rmdir(path)
```

This removes the folder at `path`, and *all files and folders it contains will also be deleted.*
```python
shutil.rmtree(path)
```

These things delete *PERMANENTLY*, so exercise with caution. It's a good idea to comment out these statements and run `print()` commands in a loop first to print out the filenames.

For example: Instead of..
```python
import os
for filename in os.listdir():
    if filename.endswith('.rxt'):
        os.unlink(filename)
```

..do this:

```python
import os
    for filename in os.listdir()
        # os.unlink(filename)
        print(filename)  ## making sure the correct files are listed FIRST.
```

## Safe Delete

We can do safe delete with third party `send2trash` module. Since it's a third party we need to do `pip install` first.

Using `send2trash` is much safer than the permadelete functions from Python's default libraries. It will send folders and files to our computer's trash or recycle bin instead of permanently deleting them.

```python
import send2trash
send2trash.send2trash('foo.txt')
```

Things to note:
- While sending things to the bin is safe and let us recover them later, it will not free up disk space like permanently deleting them.
- The `send2trash()` can only send files to the bin, it cannot retrieve them.

## Walking a dir tree

We can use `os.walk()` to rename every file in some folder and also every file in every subfolder of that folder, meaning that we'd want to walk through the directory tree, touching files as we go.

```python
import os 

for folderName, subFolders, fileNames in os.walk('.'):
    print('The current folder is ' + folderName)
    
    for subFolder in subFolders:
        print('The subfolder of ' + folderName + ': ' + subFolder)
    for fileName in fileNames:
        print('File inside ' + folderName + ': ' + fileName)
```

The `os.walk()` function returns three values on each iteration through the loop:
- A string of the current folder's name
- A list of strings of the folders in current folder
- A list of strings of the files in the current folder

By current folder, it is the folder of the current iteration of the for loop. The current working directory (`os.getcwd()`) is not changed by `os.walk()`.


## Compressing Files with `zipfile` module

Compressing a file reduces its size, which is useful when transfering it over the Internet, especially when working with multiple files and folders.

A zipped file that contains multiple folders is called and archive file.

`zipfile` module can be used to both create and open /(or extract/) ZIP files.

### Reading ZIP file

    ```python
import zipfile

# First, we create a ZipFile (case-sensitive) object
exampleZip = zipfile.ZipFile('foo.zip')

# list the name of things contained within the ZipFile object
exampleZip.namelist()

# we can also get info on a specific item
exampleItem = exampleZip.getinfo('file.txt')
exampleItem.file_size
exampleItem.compress_size    
    ```

While a `ZipFile` object represents an entire archive file, a `ZipInfo` object holds useful information about a /single file/ within the archive.

### Extracting from ZIP files

The `extractall()` method for `ZipFile` objects extracts all the files and folder from a ZIP file int other current working directory (`os.getcwd()`)

```python
import zipfile, os
os.chdir('`/Downloads')

exampleZip = zipfile.ZipFile('example.zip')

exampleZip.extractall()  # extract to `/Downloads
exampleZip.close()
```

Alternatively, instead of extract to $PWD you can also pass an argument to `extractall()` to have it extract the files into a folder. If the folder does not exist, it will be created.

Instead of `extractall()`, you can also use `extract()` which extracts a single file from the ZIP file.

The argument we pass to `extract()` must match one of the string in the list returned by `namelist()`. We can also pass a second argument to `extract()` to extract the file into a different folder from $PWD.

`extract()` returns the absolute path to which the file was extracted.

### Creating and Adding to ZIP files

To create a ZIP file, we must open the `ZipFile` object in /write/ mode by passing 'w' as the second argument. This is similar to opening a text file in write mode using `open()`.


By default, `write()` in write mode will *erase* all existing contents of a ZIP file. If we want to simply add files to an existing ZIP file, pass `'a'` as the 2nd arguement to the `zipfile.ZipFile()` to open the ZIP file in *append* mode.

When we pass a path to `write()` method of the `ZipFile` object, Python will compress the file at the path and add it into the ZIP file. The `write()` method first argument is a string of the filename to add. The second argument is the compression type parameter, which tells Python what algorithm it should use to compress the files. `compress_type=zipfile.ZIP_DEFLATED` is a compression algorithm that works well on all types of data.

### Project: Renaming files with Ameri
# Chapter 11- Debugging

The more complicated the more programs we write, the more likely we'll start finding not-so-simple bugs in them. It is important that we know how to use the right tools to find the root cause of bugs in our program to help us fix bugs faster and with less effort.

Our computer only does what we tell it to do, it cannot read minds so it can't do what we intended it to do. Professionals create bugs all the time, so we shouldn't feel discouraged when our program runs into a problem.

In general, the earlier we catch bugs, the easier they will be easier to fix.

## Raising Exceptions

An exception is raised when Python encounters a bug in our code, or when it tries to execute invalid code. We can handle Python's exception with `try` and `except` statements so that our program can recover from the anticipated excpetion. However we can also *raise our own exception* in our code. Raising an exception is a way of saying 'Stop running the code in this fucntion and move the program execution to the `except` statement/ block.

Exceptions can be raised with a `raise` statement. A `raise` statement consists of:
- The `raise` keyword
- A call to the `Exception()` function
- A string with a helpful error message passed to the `Exception()` function.

```python
raise Exception('test')
```

```
: Traceback (most recent call last):
:   File "<stdin>", line 1, in <module>
: Exception: test
```
If there are no `try` and `except` statements covering the `raise` statement, the program simply crashes and displays the error message, like above.

Often, it's the code that calls the function that would know how to handle an exception rather than the function itself. This means that we will commonly see a `raise` statement inside a function and the `try` and `except` statements in the code calling the function.

```python
def boxPrint(symbol, width, height):
    if len(symbol) != 1:
        raise Exception('Symbol must be a single character string.')
    if width <= 2:
        raise Exception('Width must be greater than 2.')
    if height <= 2:
        raise Exception('Height must be greater than 2.')

    print(symbol * width)
    for i in range(height - 2):
        print(symbol + (' ' * (width - 2)) + symbol)
    print(symbol * width)

for sym, w, h in (('*', 4, 4), ('O', 20, 5), ('x', 1, 3), ('ZZ', 3, 3)):
    try:
        boxPrint(sym, w, h)
    except Exception as err:
        print('An exception happened: ' + str(err))
```

```
,****
,*  *
,*  *
,****
OOOOOOOOOOOOOOOOOOOO
O                  O
O                  O
O                  O
OOOOOOOOOOOOOOOOOOOO
An exception happened: Width must be greater than 2.
An exception happened: Symbol must be a single character string.
```

In the above example, within the `boxPrint()` function, we have three `if` blocks that call the `raise` statement when the requirements are not met.

Later when we call the `boxPrint()` function, our `try/except` block will handle the invalid argument.

## Getting the Traceback as a string

When Python encounters an error, it produces a treasure information called *Traceback*. The traceback includes the error message, the line number of the line that causes the error and the sequence of the function call that led to the error. This sequence of calls is called the /call stack/.

```python
def foo():
	cheese()
def cheese():
	raise Exception('End of call stack.')
foo()
```

```
: Traceback (most recent call last):
:   File "<stdin>", line 1, in <module>
:   File "/tmp/babel-UOMNXg/python-tCAYlt", line 5, in <module>
:     foo()
:   File "/tmp/babel-UOMNXg/python-tCAYlt", line 2, in foo
:     cheese()
:   File "/tmp/babel-UOMNXg/python-tCAYlt", line 4, in cheese
:     raise Exception('End of call stack.')
: Exception: End of call stack.
```
In programs where functions can be called from multiple places, the call stack can help determine which call led to the error.

The traceback is displayed whenever a raised exception goes unhandled. However we can also obtain it as a string by calling `traceback.format_exc()`. This function is useful if we want the information from the exception's traceback, but we also want an `except` statement to gracefully handle the exception. To do this, we need to import the `traceback` module.

```python
import traceback


try:
    raise Exception("this is the error.")
except:
    with open('error', 'w') as file:
        file.write(traceback.format_exc())
    print('Traceback info was written to error.')
```

When we run the code above, the output will not show the traceback because we gracefully handled it with our `except` statement. However the traceback is written to a file named 'error' that is in the same directory as the Python script.

This is the terminal output:
``` 
Traceback info was written to error.
```

This is the 'error' file content:
``` 
Traceback (most recent call last):
  File "Debugging.py", line 5, in <module>
    raise Exception("this is the error.")
Exception: this is the error.
```

Later in this chapter we'll learn how use the `logging` module which is more effective than simply writing the traceback into text files.

## Assertions

An assertion is a sanity check to make sure our code isn't doing something obviously wrong. These sanity checks are performed by `asset` statements. If this fails then an `AssertionError` exception is raised.

When we code our programs and find ourself thinking "of course this would never happen", we should add an `assert` to check it. Assertions should not be used in place of real error handling. Assertions check for things that *should never happen*.

An `assert` statement consists of the following:
- The `assert` keyword
- The condition, that is an expression that evaluate to either `True` or `False`.
- A comma
- A string to display when the condition is False

In plain English, an `assert` statement says: "I assert that the following condition holds true, and if not, there is a bug somewhere so immediately stop the program.". 

Example:
```python
ages = [26, 15, 17, 80, 57, 73]
ages.sort()
print(ages)
assert ages[0] <= ages[-1] # Assert that first age is smaller or equal than last age
```

```
: [15, 17, 26, 57, 73, 80]
```
Because the condition `ages[0] <= ages[-1]` evaluates to `True`, the `assert` statement does nothing.

Let's intentionally make an error:

```python
ages = [26, 15, 17, 80, 57, 73]
ages.reverse()
print(ages)
assert ages[0] <= ages[-1], "This isn't sorted!" # Assert that first age is smaller or equal than last age
```

```
: [73, 57, 80, 17, 15, 26]
: Traceback (most recent call last):
:   File "<stdin>", line 1, in <module>
:   File "/tmp/babel-UOMNXg/python-7OwQGG", line 4, in <module>
:     assert ages[0] <= ages[-1], "This isn't sorted!" # Assert that first age is smaller or equal than last age
: AssertionError: This isn't sorted!
```
### Assertion versus error handling

Unlike exceptions, our code should *not* handle `assert` statements with `try` and `except`. If an `assert` fails, our program *should crash* because an impossible scenario has happened.  This effectively shortent the time between the original cause of the bug and when we first notice the bug. Remember, a bug should always be caught as earlier as possible. The later we notice the bug, the more amount of code we'd have to dig through.

Assertions are for programmers errors and not user errors. User errors should be expected. Programmer errors should not, they should be thought of as impossible scenarios. In an ideal world, assertions should only fail when a program is under development. A user should never see an assertion error in a finished program.

For errors that our program can run into as a normal part of its operation (such as the file not being found, or the user entering invalid input), we should raise an exception and handle it. For these, we *should not* use `assert`. Users can actually run `python -O script.py` to turn off assertions.

Assertions are also *not* a replacement for comprehensive testing.

### Assertion - A Traffic Light simulation

Let's say we have a traffic light simulation program, the data that represents the stoplight at an intersection is a dictionary with key `ns` and `ew` for the stoplights facing north-south and east-west respectively.

For example: This stoplight represents the lights at the intersection of Market Street and 2nd Street:
``` 
market_2nd = {'ns': 'green', 'ew': 'red'}
```

Ok now we can write a `switchLight()` function that should simply switch each light to the next color in a sequence: green -> yellow -> red -> green..

Our code probably looks something like this:
```python
def switchLights(stoplight):
	for key in stoplight.keys():
		if stoplight[key] == 'green':
			stoplight[key] = 'yellow'
		elif stoplight[key] == 'yellow':
			stoplight[key] = 'red'
		elif stoplight[key] == 'red':
			stoplight[key] = 'green'

switchLights(market_2nd)
```

There is a problem with this code. Python will not throw any error because the code is valid. Let's pretend we have written a thousand lines of codes and don't notice the problem.

When we run a simulation with virtual car, our code'll run fine, but all our cars would crash.

Let's pretend we'd write another thousand lines of code, then we'd run the simulation. At this point we'd have no idea where the hell the problem could be!? At this point, we don't know whether the problem is in the code simulating the cards or in the code simulating the drivers, or the wind.. whatever. It could take hours and hours to trace the bug back to `switchLight()`.

We could save hours and hours of investigation by simply adding an assertion to check that at least one of the lights is always red.

Let's run the program without the assertion:

```python
market_2nd = {'ns': 'green', 'ew': 'red'}

def switchLights(stoplight):
	for key in stoplight.keys():
		if stoplight[key] == 'green':
			stoplight[key] = 'yellow'
		elif stoplight[key] == 'yellow':
			stoplight[key] = 'red'
		elif stoplight[key] == 'red':
			stoplight[key] = 'green'

switchLights(market_2nd)
print(market_2nd)
```

```
: {'ns': 'yellow', 'ew': 'green'}
```
See the problem? Our stop light would just stop at the yellow lights, and cars would hit each other.

Let's now write an assertion to check that at least one light is always red:

```python
market_2nd = {'ns': 'green', 'ew': 'red'}

def switchLights(stoplight):
	for key in stoplight.keys():
		if stoplight[key] == 'green':
			stoplight[key] = 'yellow'
		elif stoplight[key] == 'yellow':
			stoplight[key] = 'red'
		elif stoplight[key] == 'red':
			stoplight[key] = 'green'
	assert 'red' in stoplight.values(), 'Neither light is red!' + str(stoplight)

switchLights(market_2nd)
print(market_2nd)
```

```
: Traceback (most recent call last):
:   File "<stdin>", line 1, in <module>
:   File "/tmp/babel-UOMNXg/python-Hjfi7o", line 13, in <module>
:     switchLights(market_2nd)
:   File "/tmp/babel-UOMNXg/python-Hjfi7o", line 11, in switchLights
:     assert 'red' in stoplight.values(), 'Neither light is red!' + str(stoplight)
: AssertionError: Neither light is red!{'ns': 'yellow', 'ew': 'green'}
```
This way, our program would crash right there and then. It's not ideal to have our program crash. However it is good to be able to immediately point out that a sanity check failed. Things like these save us a lot of future debugging effort.

## Logging

Although we have not use logging in our code, we use a lot of `print()` to output some variable's value while our program is running. The `print()` itself is a form of logging to debug our code.

Logging is a great way to understand what is happening in our program and in what order it's happening.

Python's logging module makes it easy to create a record of custom messages that we write. The log messages will describe when the program execution has reached the logging function call and list any variables we have specified at that point in time.

On the other hand, a missing log message indicates that a part of our code was skipped and never executed.

### Using the logging module

To enable the logging module to display log messages on our screen as our program runs, we need to copy the following to the top of our program:

```python
import logging
logging.basicConfig(level=logging.DEBUG, format=' %(asctime)s -  %(levelname)s -  %(message)s')
```

Basically when Python logs an event, it creates a *LogRecord* object that holds information about the event. The `logging` module's `basicConfig()` function lets us specify what details about the *LogRecord* object we want to see (`level=`) and how we want the details displayed (`format=`).

Let's look at an example below where we write a function to calculate the factorial of a number.

```python
import logging
logging.basicConfig(level=logging.DEBUG, format='%(asctime)s -  %(levelname)s-  %(message)s')
logging.debug('Start of program')

def factorial(n):
    logging.debug('Start of factorial(%s%%)'  % (n))
    total = 1
    for i in range(n + 1):
        total *= i
        logging.debug('i is ' + str(i) + ', total is ' + str(total))
    logging.debug('End of factorial(%s%%)'  % (n))
    return total

print(factorial(5))
logging.debug('End of program')
```

```
2020-05-27 00:49:52,690 -  DEBUG-  Start of program
2020-05-27 00:49:52,690 -  DEBUG-  Start of factorial(5%)
2020-05-27 00:49:52,690 -  DEBUG-  i is 0, total is 0
2020-05-27 00:49:52,690 -  DEBUG-  i is 1, total is 0
2020-05-27 00:49:52,690 -  DEBUG-  i is 2, total is 0
2020-05-27 00:49:52,690 -  DEBUG-  i is 3, total is 0
2020-05-27 00:49:52,690 -  DEBUG-  i is 4, total is 0
2020-05-27 00:49:52,690 -  DEBUG-  i is 5, total is 0
2020-05-27 00:49:52,690 -  DEBUG-  End of factorial(5%)
0
2020-05-27 00:49:52,691 -  DEBUG-  End of program
```

Here, what we do is using the `logging.debug()` when we want to print log information.

Whenever the `login.debug()` function is called, it will refer back to the `basicConfig()` setup. The information will be in the format we specified in the `basicConfig()` and will include the message we pass to `debug()`.

We can see that the `logging.debug()` calls printed out not just the strings passed to them but the timestamp and the word DEBUG.

Now let's fix our program:

```python
import logging
logging.basicConfig(level=logging.DEBUG, format='%(asctime)s -  %(levelname)s-  %(message)s')
logging.debug('Start of program')

def factorial(n):
    logging.debug('Start of factorial(%s%%)'  % (n))
    total = 1
    for i in range(1, n + 1):
        total *= i
        logging.debug('i is ' + str(i) + ', total is ' + str(total))
    logging.debug('End of factorial(%s%%)'  % (n))
    return total

print(factorial(5))
logging.debug('End of program')

```

```
2020-05-27 00:51:37,875 -  DEBUG-  Start of program
2020-05-27 00:51:37,876 -  DEBUG-  Start of factorial(5%)
2020-05-27 00:51:37,876 -  DEBUG-  i is 1, total is 1
2020-05-27 00:51:37,876 -  DEBUG-  i is 2, total is 2
2020-05-27 00:51:37,876 -  DEBUG-  i is 3, total is 6
2020-05-27 00:51:37,876 -  DEBUG-  i is 4, total is 24
2020-05-27 00:51:37,876 -  DEBUG-  i is 5, total is 120
2020-05-27 00:51:37,876 -  DEBUG-  End of factorial(5%)
120
2020-05-27 00:51:37,876 -  DEBUG-  End of program
```
### Use debug instead of `print()`

Importing logging and setting up the config is somewhat tedious. We may want to use `print()` instead, however we should not give in to this temptation!

Once we have done with debugging, we'll end up spending a lot of time removing `print()` calls from our code after each log message. We might accidentally remove a `print()` call that is legitimately intended for non-log messages.

The nice thing about log messages is that we can fill our program with as many as we like, and we can always disable them all later by adding a single `logging.disable(logging.CRITICAL)` call. Unlike `print()`, the `logging` module makes it easy to switch between showing and hiding log messages.

Log messages are intended for the programmer, not the user. For message that we want the user to see, we should use `print()`. However, stuff like the contents of some dictionary value or how long it takes to run a function, the users don't really care.

### Logging Levels

There are five logging levels:

| Level    | Logging Function   | Description & When it's used                                               |
|----------|--------------------|----------------------------------------------------------------------------|
| DEBUG    | logging.debug()    | This is the lowest level, it is used for small details. It is typically    |
|          |                    | of interest when dianosing problem.                                        |
| INFO     | logging.info()     | Used to record information on general events in our programs or confirm    |
|          |                    | that things are working at their point in the program.                     |
|          |                    | These are confirmations that things are working as expected.               |
| WARNING  | logging.warning()  | Used to indicate a potential problem that doesn't prevent the program      |
|          |                    | from working but might do so in the future. The software is still working  |
|          |                    | as expected.                                                               |
|          |                    | Example: "Disk Space low"                                                  |
| ERROR    | logging.error()    | Used to record an error that caused the program to fail to do something.   |
|          |                    | The software has not been able to perform some function.                   |
| CRITICAL | logging.critical() | The highest level. It is used to indicate a fatal error that has caused or |
|          |                    | is about to cause the programe to stop running entirely.                   |

Our logging message is passed as a string to these functions.

The logging levels are suggestions. *Ultimately, it is up to us to decide which category our log message faills into.*

The benefit of logging levels is that we can change what priority of logging message we want to see. Passing `logging.DEBUG` to the `basicConfig()` function's `level` keyword argument will show messages from ALL levels (DEBUG is the lowest level). After we develop our program some more, we may be interested only in errors. In that case, we can set the `basicConfig()` level argument to `logging.ERROR`. This will show only ERROR and CRITICAL logging message.

### Disabling logging

Disabling logging is easy. After we have finished debugging our program, we'd probably don't want all these log messages cluttering the screen. The logging.disable() function disables these so that we don't have to go into our program and remove all logging calls by hand.

What we do is passing `logging.disable({logging level})` and it will suppress all log messages at that level or below. Therefore `logging.disable(logging.CRITICAL)` should disable logging entirely.

```python
import logging
logging.basicConfig(level= logging.DEBUG)

logging.critical('CRITICAL ERROR!!!!')
logging.disable(logging.CRITICAL)
logging.critical('STILL CRITICAL!!!')
logging.debug('Hello world')
```

```
: 2020-05-27 01:10:42,152 -  CRITICAL-  CRITICAL ERROR!!!!
```
### Logging to a file

Instead of displaying the log messages to the screen, we can write them to a text file.

We do this by passing to the `basicConfig()` function a `filename` keyword argument.
```python
import.basicConfig(filename='myProgramLog.log'....)
```

The log messages will be saved to *myProgramLog.log*. Writing logs to a file is helpful because while logs are helpful, they clutter the screen and make it hard to read the actual program's output.

## The Debugger

Debugger is a feature of Mu editor, IDLE and other editor software that allows us to execute our programe *one line at a time*. The debugger will run a single line of code and wait for us to tell it to continue. By running programe "under the debugger" like this, we can take as much tiem as we want to examine the values in the variables at any givent point during the program's lifetime. This is a valuable tools in tracking down bugs.

A debugger typically has a few buttons:
- *Continue*: This button causes the program to execute normally *until it terminates or reaches a breakpoint*. This is normally used if we are done with debugging and want the programe to continue normally.
- *Step Over*: This button executes the next line of code, similar to Step In however it will "step over" the code in the function. The function's code will be executed at full speed and the next pause is when the function call returns. For example if we do `print(foo(x))`, the `foo(x)` will be "stepped over" and the next pause is when `print()` returns.
- *Step In*: This button causes the debugger to execute the next line of code and pause again. If the next line of code is a function call, the debugger will "step into" that function and jump to the first line of code in that function. For example if we do `print(foo(x))` then the debugger will step into the first line of `foo(x)` after `def foo(x):`
- *Step Out*: This causes the debugger to execute lines of code at full speed until it returns from the current function. We use this when we have stepped into a function call with the Step In button and want to simply keep executing instructions until we get back out.
- *Stop*: This stops the debugger entirely and terminate the programe effective immediately.

### Breakpoints

A *breakpoint* can be set on a specific line of code and forces the debugger to pause whenever the program execution reaches that line.

# Chapter 12 - Web Scraping

Web scraping is the term for using a program to download and 

Web scraping is the term for using a program to download and process content from the web. One of a very popular example is Google running many web scraping programs to index web pages for its search engine.

There are several modules that makes it easy to scrape web pages in Python:
- *webbrowser* - Opens a browser to specific page.
- *requests* download files and web pages from the internet.
- *bs4* parses html
- *selenium* launches and control a web browser. It is also able to fill in forms and stimulate mouse clicks.

## Project - #mapit.py# with #webbrowser# module

The *webbrowser* module can only do one thing, which is to open an URL on a web browser.

This, will open our system's default web browser and go to google.

```python
import webbrowser

webbrowser.open('https://google.com/')
```

```
: None
```
Let's make an example project - writing a simple script to automatically launch Google Map in our browser using the contents of our clipboard.

This is what our program should do:

1. Gets a street address from the command line arguments or clipboard.
2. Opens the web browser to Google Maps page for the address.

### Handling command line argument

```python
import sys
import webbrowser

url_prefix = 'https://www.google.com/maps/place/'

if len(sys.argv) > 1:
    address = ' '.join(sys.argv[1:])

url = url_prefix + address
print(url)
webbrowser.open(url)
```

## Downloading files from the web with the Requests Module

The *requests* module lets us download file easily from the internet without having to worry about complicated issues such as network errors, connection problems and data compression. 

The *requests* module does not come with Python, it was written because Python's own *urllib2* module is too complicated to use.

What we do is use the `request.get()` function that takes a string of URL to download. The return value is of *Response* object, which contains the response that the web server gave to our request.

```python
import requests

r = requests.get('https://automatetheboringstuff.com/files/rj.txt')

print(type(r)) # Type of return value

print(r.status_code) # Status code of return value

print(r.status_code == requests.codes.ok) # Check if response is OK

```

```
: <class 'requests.models.Response'>
: 200
: True
```
The *Response* object has a status_code attribute that can be checked against `requests.codes.ok` which is a variable that has the integer value `200` - HTTP Response Status Code of Success. 

We can also check for success by calling the `raise_for_status()` method on the `Response` object.

```python
import requests

r = requests.get('https://automatetheboringstuff.com/files/rj.txt')

r.raise_for_status() # This will not return anything because the status is OK

r2 = requests.get('https://automatetheboringstuff.com/files/thisdoesnotexiost.txt')

r2.raise_for_status()
```

```
: Traceback (most recent call last):
:   File "<stdin>", line 1, in <module>
:   File "/tmp/babel-e8Rzee/python-4Ok5Fq", line 9, in <module>
:     r2.raise_for_status()
:   File "/usr/lib/python3.8/site-packages/requests/models.py", line 941, in raise_for_status
:     raise HTTPError(http_error_msg, response=self)
: requests.exceptions.HTTPError: 404 Client Error: Not Found for url: https://automatetheboringstuff.com/files/thisdoesnotexiost.txt
```
The `raise_for_status` method is a good way to ensure that our programe halts if a bad download occurs. This is a good thing as we want to catch our errors as soon as it happens. 

If we don't want out program to halt completely, i.e the download isn't a deal-breaker, we can also wrap the `raise_for_status` method within a `try-except` block ie:

```python
import requests

r = requests.get('https://automatetheboringstuff.com/files/rj.txt')

r.raise_for_status() # This will not return anything because the status is OK

r2 = requests.get('https://automatetheboringstuff.com/files/thisdoesnotexiost.txt')

try:
	r2.raise_for_status()
except:
	print('There was an error with r2 - response: %s' % r2)
```

```
: There was an error with r2 - response: <Response [404]>
```
### Saving downloaded file to hard drive with `iter_content()` method

To write the web page to a file, we can also use a for loop with the `Response` object's `iter_content()` method. This returns "chunks" of the content on each iteration through the loop. Each chunk is of the *bytes* data type and we can specify how many butes each chunk will contain. One hundred thousand bytes is generally a good size, so we can pass 100000 as the argument.

We also need to open the file in *write binary mode* by passing the string 'wb' as the second argument to `open()`. This needs to be done regardless of the content-type of the page, e.g even if the entire page is in plain-text.

```python
import requests

r = requests.get('https://automatetheboringstuff.com/files/rj.txt')

try:
	r.raise_for_status() # This will not return anything because the status is OK
except:
	print('There was an error.')

with open('sample.txt', 'wb') as file:
	for chunk in r.iter_content(100000):
		file.write(chunk)
```

## Parsing HTML with `bs4`` module

*BeautifulSoup* is a module that can be used for extracting information from an HTML (or xml) page. This is the preferred method over regular expression. The BeautifulSoup module's name is *bs4* which stands for Beautiful Soup version 4.

The `bs4.BeautifulSoup()` needs to be called with a string containing the HTML it will parse. This function returns a `BeautifulSoup` object.
```python
import requests, bs4

r = requests.get('https://nostarch.com')
r.raise_for_status()

noStarchSoup = bs4.BeautifulSoup(r.text, 'html.parser')
print(type(noStarchSoup))
```

```
: <class 'bs4.BeautifulSoup'>
```
The *html.parser* parser used above comes with Python. We can also use other parsers like the newer and faster *lxml* parser.

### Finding an Element with the `select()` method 

We can retrive a web page element from a BeautifulSoup obejct by calling the `select()` method and passing a string of CSS selector for the element we are looking for. This is similar to using regex however instead of just a general string, we are using a pattern to look for things in the HTML pages instead of just general text.

The various selector patterns can also be combined to make sophisticated matches. For example, `soup.select('p #author')` match any element that has an id attribute of author *AND* inside a <p> element. Instead of writing the selector ourself, we can also right-click on the element on a web browser's *Inspect Element* view  and select *Copy > CSS Selector*.

Example of CSS Selector:
[[./images/soupselect.png]]

The `select()` method returns a list of `Tag` objects. These `Tag` objects can also be passed to the `str()` function to show the HTML tags they represent. Tag values also have an `attrs` attributes that show all the HTML attributes of the tag as a dictionary.

We can also extract the text content by `getText()`.

```python
import bs4

html = '''<!-- This is the example.html example file. -->

<html><head><title>The Website Title</title></head>
<body>
<p>Download my <strong>Python</strong> book from <a href="https://
inventwithpython.com">my website</a>.</p>
<p class="slogan">Learn Python the easy way!</p>
<p>By <span id="author">Al Sweigart</span></p>
</body></html>'''

test = bs4.BeautifulSoup(html, 'html.parser')

authors = test.select("#author")

print(type(authors))

print(len(authors))

print(type(authors[0]))

print(authors[0])

print(str(authors[0]))

print(authors[0].attrs)

print(authors[0].getText())

print(authors[0].get('id'))


```

```
: <class 'bs4.element.ResultSet'>
: 1
: <class 'bs4.element.Tag'>
: <span id="author">Al Sweigart</span>
: <span id="author">Al Sweigart</span>
: {'id': 'author'}
: Al Sweigart
: author
```
The `get()` method for *Tag* objects makes it simple to access attributes values from an element. In the above example we got the id attributes from `authors[0]`.

## Controlling the browser with #selenium#

The *selenium* module lets Python directly control the browser by programmatically clicking links and filling in login information, mimicking the human user interaction with the page. Using this module we can interact with web pages in a much more advanced way than with *requests* and *bs4*. However because this launches a web browser, it's a bit slower and hard to run in the background. Therefore we need to consider our use cases. It's probably not a good idea to write a script using Selenium just to download a text file.

Still, we have to use *selenium* to interact with a web pages that depend on JavaScript code that updates the page client-side. Major ecommerce websites such as Amazon always have software systems to recognize traffic that they suspect is a script harvesting their info or signing up for multiple free accounts.  These sites may put a timeout limit on us and refuses to serve pages to us a while which would break out script. For these things, *selenium* module is much more likely to function than *requests*.

A major "tell" to websites that we are using a script is the *user-agent* parameter that identifies the web browser and is included in all HTTP requests. We can see our *user-agent* by visiting https://www.whatsmyua.info/. 

Using *requests*, the user-agent would be something like 'python-requests/2.21.0'.

Using *selenium*, we are much more likely to pass this human-test because selenium uses a normal web driver which would have the same *user-agent* as that of a normal web browser session. It also has the same traffic pattern. However, selenium can still be detected by websites and a lot of ticketing and ecommerce websites often block browsers controlled by selenium.

```python
from selenium import webdriver
browser = webdriver.Firefox()

print(type(browser))
```

```
: <class 'selenium.webdriver.firefox.webdriver.WebDriver'>
```
When we call the `webdriver.Firefox()` statement, Firefox starts up.

We can also browse to a page with:
```python
browser.get('https://google.com/')
```

### Finding Elements on the Page

*WebDriver* objects have a few methods for finding elements on a page. They are divided into `find_element_*` and `find_elements_*` methods. The `find_element_*` methods return a single WebElement object, representing the *first* element on the page that matches the query. The `find_elements_*` returns a list of WebElement objects for every matching element on the page.

[[./images/selmethods.png]]

Except the `*_by_tag_name()` methods, the arguments to all the methods are case-sensitive. If no element exists that match what the method is looking for, the *selenium* module raises a *NoSuchElement* exception.

-------

Once we have a WebElement object, we can find out more about it by reading the attributes or calling these methods:

[[./images/selwebemethods.png]]

```python
from selenium import webdriver
browser = webdriver.Firefox()
browser.get('https://inventwithpython.com')
try:
    elem = browser.find_element_by_class_name('cover-thumb')
    print('Found <%s> element with that class name!' % (elem.tag_name))
except:
    print('Was not able to find an element with that name.')
```

```
: Found <img> element with that class name!
```
#### Note about elements with multiple class names

In the above example, this is a snippet of the HTML on https://inventwithpython.com:

``` html
    <div class="card text-center col-md-4" style="width: 20rem;">
      <a href="#invent"><img class="card-img-top cover-thumb" src="images/cover_invent4th_thumb.png" alt="Cover of Invent Your Own Computer Games with Python" /></a>
      <div class="card-block">
        <h4 class="card-title"><a href="#invent">Invent Your Own Computer Games with Python, 4th Edition</a></h4>
        <a href="#invent" class="btn btn-primary">More Info</a>
      </div>
    </div>
```

As shown above, the img elements actually has class = `"card-image-top cover-thumb".` This does not mean that the class has a space in its name. This is a declaration for an element with *two* classes: `card-image-top` and `cover-thumb`. It's not a single class.

Therefore, this will not work:

```python
from selenium import webdriver

browser = webdriver.Firefox()

browser.get('https://inventwithpython.com')

try:
    elem = browser.find_element_by_class_name('card-img-top cover-thumb')
    print('Found <%s> element with that class name!' % (elem.tag_name))
except:
    print('Was not able to find an element with that name.')

browser.close()
```

```
: Was not able to find an element with that name.
```
What we can do is join the class names by a period `.`, i.e like this:

```python
from selenium import webdriver

browser = webdriver.Firefox()

browser.get('https://inventwithpython.com')

try:
    elem = browser.find_element_by_class_name('card-img-top.cover-thumb')
    print('Found <%s> element with that class name!' % (elem.tag_name))
except:
    print('Was not able to find an element with that name.')

browser.close()
```

```
: Found <img> element with that class name!
```
#### Clicking the Page

The WebElement objects returned from *find_element* and *find_elements* methods have a `click()` method that simulates a mouse click on that element. This method can be used to follow a link, make a selection on a radio button, clicking the Submit button or trigger whatever else might happen when the element is clicked by the mouse.

#### Filling Out and Submitting Forms

Sending keystrokes to text fields on a web page is a amtter of finding the `<input>` or `<textarea>` element for that text field and then calling the `send_keys()` method.

#### Sending Special Keys

The *selenium* module has a module for keyboard keys that are impossible to type into a string value. These values are stored in attributes in the `selenium.webdriver.common.keys` module.

That's quite a long module name so we should use something like this:
```python
from selenium.webdriver.common.keys import Keys
```

#### Clicking Browser buttons

The *selenium* module can simulate clicks on various browser buttons as well:

*browser.back()* - Back Button
*browser.forward()* - Forward Button
*browser.refresh()* - Click the reload button
*browser.quit()* - Click the Close Window button

# Chapter 13 - Working with Excel Spreadsheets

An Excel spreadsheet document is called a workbook. A single workbook is saved in a file with the *.xlsx* extension. Each workbook can contain multiple /sheets/, also called /worksheets/. The sheet the user is currently viewing or last viewed below closing Excel is the /active sheet/.

In this chapter we will be learning about the *openpyxl* module.

``` bash
pip install --user openpyxl==2.6.2
```

## Open a workbook

```python
import openpyxl

wb = openpyxl.load_workbook('example.xlsx')

print(type(wb))
```

``` 
<class 'openpyxl.workbook.workbook.Workbook'>
```

## Getting sheets from the workbook

   ```python
import openpyxl


wb = openpyxl.load_workbook('example.xlsx')

print(wb.sheetnames)

sheet1 = wb['Sheet1']
print(type(sheet1))
print(sheet1.title)

activesheet = wb.active
print(activesheet.title)
   ```

   ``` 
['Sheet1', 'Sheet2', 'Sheet3']
<class 'openpyxl.worksheet.worksheet.Worksheet'>
Sheet1
Sheet1
   ```

## Getting Cells from Sheets

Once we have a *Worksheet* object, we can access a *Cell* object by its name.

```python
import openpyxl


wb = openpyxl.load_workbook('example.xlsx')

print(wb.sheetnames)

sheet1 = wb['Sheet1']

cell = sheet1['A1']
print(type(cell))
print('Row %s, Column %s is %s' % (cell.row, cell.column, cell.value))
print('Cell %s is %s' % (cell.coordinate, cell.value))
print('Cell %s\'s value has type %s' % (cell.coordinate, type(cell.value)))
```

``` 
['Sheet1', 'Sheet2', 'Sheet3']
<class 'openpyxl.cell.cell.Cell'>
Row 1, Column 1 is 2015-04-05 13:34:02
Cell A1 is 2015-04-05 13:34:02
Cell A1's value has type <class 'datetime.datetime'>
```

OpenPyXL will automatically interpret the dates in the cell value and return them. In the above example, the cell value was correctly read as a datetime value instead of a string.

We can also do this:
```python
import openpyxl


wb = openpyxl.load_workbook('example.xlsx')
sheet1 = wb['Sheet1']

print(sheet1.cell(row=1, column=2))
print(sheet1.cell(row=1, column=2).value)
```

``` 
<Cell 'Sheet1'.B1>
Apples
```

Note:
- It's tricky to specify a column by letter. After column Z, the columns start by using two letters: AA, AB, AC and so on. Therefore it's better to access a cell using the sheet's `cell()` method and passing the integers for its `row` and `column` keyword arguments.
- The first column integer is *1*, not *0*.

```python
import openpyxl


wb = openpyxl.load_workbook('example.xlsx')
sheet1 = wb['Sheet1']

print(sheet1.cell(row=1, column=2))
print(sheet1.cell(row=1, column=2).value)

print('Going through every row..')
for i in range(1, 8, 1):
    print(i, sheet1.cell(row=i, column=2).value)

print('Going through every other row..')
for i in range(1, 8, 2):
    print(i, sheet1.cell(row=i, column=2).value)
```

``` 
<Cell 'Sheet1'.B1>
Apples
Going through every row..
1 Apples
2 Cherries
3 Pears
4 Oranges
5 Apples
6 Bananas
7 Strawberries
Going through every other row..
1 Apples
3 Pears
5 Apples
7 Strawberries
```

## Converting between Column Letters and Numbers

We can get the maximum number of columns in our sheet like this:

```python
import openpyxl


wb = openpyxl.load_workbook('example.xlsx')
sheet1 = wb['Sheet1']

print(sheet1.max_column)
```

``` 
3
```

To convert from number to letters, we can call the `get_colum_letter()` function from `openpyxl.utils` library:

```python
import openpyxl
from openpyxl.utils import get_column_letter, column_index_from_string


print(get_column_letter(1))
print(get_column_letter(2))
print(get_column_letter(100))
print(get_column_letter(900))
```

``` 
A
B
CV
AHP
```

Let's try to get the maximum column from our sheet again, this time we want a column letter instead of a number:

```python
import openpyxl
from openpyxl.utils import get_column_letter, column_index_from_string


wb = openpyxl.load_workbook('example.xlsx')
sheet1 = wb['Sheet1']

print(get_column_letter(sheet1.max_column))
```

``` 
C
```

We can also get column number from string using `column_index_from_string()`:

```python
import openpyxl
from openpyxl.utils import get_column_letter, column_index_from_string


print(column_index_from_string('AAA'))
```

``` 
703
```

## Getting Rows and Columns from the Sheets

We can slice *Worksheet* object to get all the Cells objects in a row, column or rectangular area of the spreadsheet. Then we can also loop over all the cells in the slice.

In the below example, we are creating a slice variable that is of tuple object. The tuple itself contains multiple nested tuples that corresponds to rows of cells. Each of these inner tuples contains *Cell* objects in one row of the rectangular area, from the leftmost cell to the right.

```python
import openpyxl
from openpyxl.utils import get_column_letter, column_index_from_string


wb = openpyxl.load_workbook('example.xlsx')
sheet1 = wb['Sheet1']

slice = tuple(sheet1['A1': 'C3'])

print('This is a slice:')
print(slice)

print('These are the rows:')
for rowOfCells in slice:
    print(rowOfCells)

for rowOfCells in slice:
    for cell in rowOfCells:
        print(cell.coordinate, cell.value)
    print('---End of Row---')
```

``` 
This is a slice:
((<Cell 'Sheet1'.A1>, <Cell 'Sheet1'.B1>, <Cell 'Sheet1'.C1>), (<Cell 'Sheet1'.A2>, <Cell 'Sheet1'.B2>, <Cell 'Sheet1'.C2>), (<Cell 'Sheet1'.A3>, <Cell 'Sheet1'.B3>, <Cell 'Sheet1'.C3>))
These are the rows:
(<Cell 'Sheet1'.A1>, <Cell 'Sheet1'.B1>, <Cell 'Sheet1'.C1>)
(<Cell 'Sheet1'.A2>, <Cell 'Sheet1'.B2>, <Cell 'Sheet1'.C2>)
(<Cell 'Sheet1'.A3>, <Cell 'Sheet1'.B3>, <Cell 'Sheet1'.C3>)
A1 2015-04-05 13:34:02
B1 Apples
C1 73
---End of Row---
A2 2015-04-05 03:41:23
B2 Cherries
C2 85
---End of Row---
A3 2015-04-06 12:46:51
B3 Pears
C3 14
---End of Row---
```

If we want to access the data in one row or column only, we can do this:

```python
import openpyxl
from openpyxl.utils import get_column_letter, column_index_from_string


wb = openpyxl.load_workbook('example.xlsx')
sheet1 = wb['Sheet1']

columnB = list(sheet1.columns)[1]
print(columnB)

for cell in columnB:
    print(cell.value)
```

``` 
(<Cell 'Sheet1'.B1>, <Cell 'Sheet1'.B2>, <Cell 'Sheet1'.B3>, <Cell 'Sheet1'.B4>, <Cell 'Sheet1'.B5>, <Cell 'Sheet1'.B6>, <Cell 'Sheet1'.B7>)
Apples
Cherries
Pears
Oranges
Apples
Bananas
Strawberries
```

Both the *rows* and *columns* attribute of a Worksheet object give us a tuple of tuples. Each of these inner tuples represent cell objects in a single *row* for the *rows* attribute and *column* for the *columns* attribute.

In the below example, there are 7 rows.

```python
import openpyxl
from openpyxl.utils import get_column_letter, column_index_from_string


wb = openpyxl.load_workbook('example.xlsx')
sheet1 = wb['Sheet1']

all_rows = tuple(sheet1.rows)
print(all_rows)
print(len(all_rows))
```

``` 
((<Cell 'Sheet1'.A1>, <Cell 'Sheet1'.B1>, <Cell 'Sheet1'.C1>), (<Cell 'Sheet1'.A2>, <Cell 'Sheet1'.B2>, <Cell 'Sheet1'.C2>), (<Cell 'Sheet1'.A3>, <Cell 'Sheet1'.B3>, <Cell 'Sheet1'.C3>), (<Cell 'Sheet1'.A4>, <Cell 'Sheet1'.B4>, <Cell 'Sheet1'.C4>), (<Cell 'Sheet1'.A5>, <Cell 'Sheet1'.B5>, <Cell 'Sheet1'.C5>), (<Cell 'Sheet1'.A6>, <Cell 'Sheet1'.B6>, <Cell 'Sheet1'.C6>), (<Cell 'Sheet1'.A7>, <Cell 'Sheet1'.B7>, <Cell 'Sheet1'.C7>))
7
```

## Writing Excel Documents

With OpenPyXL, we can also write data i.e create and edit spreadsheet files.

## Create and saving Excel Document

To create a new blank Workbook object, we can do:

```python
import openpyxl
from openpyxl.utils import get_column_letter, column_index_from_string


wb = openpyxl.Workbook() # Create a blank Workbook
print(wb.sheetnames) # It only starts with one sheet

# Let's change the sheet title

wb['Sheet'].title = 'Testing'
print(wb.sheetnames)
```

``` 
['Sheet']
['Testing']
```

We can also create and remove sheets from a workbook:

```python
import openpyxl
from openpyxl.utils import get_column_letter, column_index_from_string


wb = openpyxl.Workbook() # Create a blank Workbook
print(wb.sheetnames) # It only starts with one sheet

# Let's change the sheet title

wb['Sheet'].title = 'Sheet Number One'
print(wb.sheetnames)

wb.create_sheet('Sheet Number Two')
wb.create_sheet()
wb.create_sheet(index=0, title='Automate the Boring stuff')

print(wb.sheetnames)
```

``` 
['Sheet']
['Sheet Number One']
['Automate the Boring stuff', 'Sheet Number One', 'Sheet Number Two', 'Sheet']
```

To delete a sheet from a workbook we simply use the `del` operator.

```python
import openpyxl
from openpyxl.utils import get_column_letter, column_index_from_string


wb = openpyxl.Workbook() # Create a blank Workbook
print(wb.sheetnames) # It only starts with one sheet

# Let's change the sheet title

wb['Sheet'].title = 'Sheet Number One'
print(wb.sheetnames)

wb.create_sheet('Sheet Number Two')
wb.create_sheet()
wb.create_sheet(index=0, title='Automate the Boring stuff')

print(wb.sheetnames)

del wb['Sheet']
print(wb.sheetnames)
```

``` 
['Sheet']
['Sheet Number One']
['Automate the Boring stuff', 'Sheet Number One', 'Sheet Number Two', 'Sheet']
['Automate the Boring stuff', 'Sheet Number One', 'Sheet Number Two']
```

Writing values to Cells is similar to writing values to keys in a dict:

```python
import openpyxl
from openpyxl.utils import get_column_letter, column_index_from_string


wb = openpyxl.Workbook() # Create a blank Workbook
print(wb.sheetnames) # It only starts with one sheet

# Let's change the sheet title

wb['Sheet'].title = 'Sheet Number One'

ws = wb['Sheet Number One']
ws['A1'] = 'Hello world'
print(ws['A1'].value)
```

``` 
['Sheet']
Hello world
```

## Setting Font Style of Cells

We can also emphasize important areas in our spreadsheet by styling the cells/ rows/ columns.

```python
import openpyxl
from openpyxl.utils import get_column_letter, column_index_from_string
from openpyxl.styles import Font

wb = openpyxl.Workbook() # Create a blank Workbook
print(wb.sheetnames) # It only starts with one sheet

# Let's change the sheet title

wb['Sheet'].title = 'Sheet Number One'

italic20font = Font(size=20, italic=True)

ws = wb['Sheet Number One']
ws['A1'] = 'Hello world'
ws['A1'].font = italic20font

wb.save('test.xlsx')
```

[[./images/openpyxlstyling.png]]

## Other stuff

We can also do other sorts of stuff like entering a cell value with formulas, adjusting rows and columns size, freeze them.etc..
# Chapter 16 - Working with CSV Files

Unlike PDF and Word documents that are in binary format which calls for special Python modules to access the data, CSV and JSON filese are just plain-text files. Therefore we can view them from a basic text editor. These files are also easily accessible with some special csv and json modules.

## CSV 

CSV files are simple and lack many features of an Excel spreadsheet. For example, CSV Files:
- Don't have types for their values - everything is a string.
- Don't have fonts.
- Don't have multiple worksheets.
- Don't have cells width and heights.
- Don't have merged cells.
- Cannot have images or charts embedded in them.

The advantage of CSV files is simplicity. They are supported by many types of programs and are a straightforward way to represent data.

Since CSV files are just plain-text files, we might be tempted to read them in as a string and then process that string using purely string manipulation. For example, since each cell in a CSV file is separate by a comma, we might just call the `split(,)` function on each line of text to get the comma separated values. *However, not every comma in a CSV file represents the boudary between two cells*, we may have legitimate commas within the content of cells.

CSV files also have their own set of escape characters to allow commas and other characters to be included as part of the values.  The `split()` function does not handle these. This is why we should always use an actual module like *csv* module for reading and writing CSV files.

### reader objects

To read data from a CSV file with *csv* module we need to create a reader object. A reader object lets us iterate over lines in a CSV file.

```python
import csv

file = open('example.csv')
print(file)

fileReader = csv.reader(file)
print(fileReader)

data = list(fileReader)

for row in data:
    print(row)
```

``` 
<_io.TextIOWrapper name='example.csv' mode='r' encoding='UTF-8'>
<_csv.reader object at 0x7fa17ae07c80>
['4/5/2014 13:34', 'Apples', '73']
['4/5/2014 3:41', 'Cherries', '85']
['4/6/2014 12:46', 'Pears', '14']
['4/8/2014 8:59', 'Oranges', '52']
['4/10/2014 2:07', 'Apples', '152']
['4/10/2014 18:10', 'Bananas', '23']
['4/10/2014 2:40', 'Strawberries', '98']
```

We can create a reader object using the `csv.reader()` function. Note that we don't put a file name directly in the function, we pass a file object.

We can also loop through reader Objects like this:

```python
import csv

file = open('example.csv')
print(file)

fileReader = csv.reader(file)
print(fileReader)

for row in fileReader:
    print('Row #' + str(fileReader.line_num) + str(row))
```

``` 
<_io.TextIOWrapper name='example.csv' mode='r' encoding='UTF-8'>
<_csv.reader object at 0x7f4095204580>
Row #1['4/5/2014 13:34', 'Apples', '73']
Row #2['4/5/2014 3:41', 'Cherries', '85']
Row #3['4/6/2014 12:46', 'Pears', '14']
Row #4['4/8/2014 8:59', 'Oranges', '52']
Row #5['4/10/2014 2:07', 'Apples', '152']
Row #6['4/10/2014 18:10', 'Bananas', '23']
Row #7['4/10/2014 2:40', 'Strawberries', '98']
```

Note: A reader object can only be looped over *only once*. to re-read the CSV file we have to re-call the `csv.reader()` function to create a reader object.

### writer object

A writer obejct lets us write data to a CSV file. To create a writer object we use the `csv.writer()` function.

```python
import csv

file = open('example.csv', 'w', newline='')
print(file)

fileWriter = csv.writer(file)

fileWriter.writerow(['Hello', 'World'])

file.close()
```

### The delimiter and lineterminator keyword argument

CSV file are separated by commas. Say we want to separate cells with a tab character instead of a comma, we also want the rows to be double-spaced.

We can do this:

```python
import csv

file = open('example.tsv', 'w', newline='')

fileWriter = csv.writer(file, delimiter='\t', lineterminator='\n\n')

fileWriter.writerow(['Hello', 'World', 'Hello', 'World', 'Hello', 'World', 'Hello', 'World', 'Hello', 'World'])
fileWriter.writerow(['Hello', 'World', 'Hello', 'World', 'Hello', 'World', 'Hello', 'World', 'Hello', 'World'])
fileWriter.writerow(['Hello', 'World', 'Hello', 'World', 'Hello', 'World', 'Hello', 'World', 'Hello', 'World'])
fileWriter.writerow(['Hello', 'World', 'Hello', 'World', 'Hello', 'World', 'Hello', 'World', 'Hello', 'World'])
fileWriter.writerow(['Hello', 'World', 'Hello', 'World', 'Hello', 'World', 'Hello', 'World', 'Hello', 'World'])

file.close()
```

``` 
Hello	World	Hello	World	Hello	World	Hello	World	Hello	World

Hello	World	Hello	World	Hello	World	Hello	World	Hello	World

Hello	World	Hello	World	Hello	World	Hello	World	Hello	World

Hello	World	Hello	World	Hello	World	Hello	World	Hello	World

Hello	World	Hello	World	Hello	World	Hello	World	Hello	World
```

### DictReader and DictWriter CSV Object

For CSV Files that contain header rows, it's more convenient to work with the *DictReader* and *DictWriter* objects rather than the reader and writer object.

The reader and writer objects read and write to CSV file rows by using lists. The DictReader and DictWriter perform the same functions but use dictionaries instead. They use the *first row* of the CSV file as the keys of these dictionaries.

Let's say we have a CSV file like so:

``` 
Timestamp,Fruit,Quantity
4/5/2014 13:34,Apples,73
4/5/2014 3:41,Cherries,85
4/6/2014 12:46,Pears,14
4/8/2014 8:59,Oranges,52
4/10/2014 2:07,Apples,152
4/10/2014 18:10,Bananas,23
4/10/2014 2:40,Strawberries,98
```

We can read the file like this:
```python
import csv

file = open('exampleWithHeader.csv')
dictReader = csv.DictReader(file)

for row in dictReader:
    print(row)
```

``` 
{'Timestamp': '4/5/2014 13:34', 'Fruit': 'Apples', 'Quantity': '73'}
{'Timestamp': '4/5/2014 3:41', 'Fruit': 'Cherries', 'Quantity': '85'}
{'Timestamp': '4/6/2014 12:46', 'Fruit': 'Pears', 'Quantity': '14'}
{'Timestamp': '4/8/2014 8:59', 'Fruit': 'Oranges', 'Quantity': '52'}
{'Timestamp': '4/10/2014 2:07', 'Fruit': 'Apples', 'Quantity': '152'}
{'Timestamp': '4/10/2014 18:10', 'Fruit': 'Bananas', 'Quantity': '23'}
{'Timestamp': '4/10/2014 2:40', 'Fruit': 'Strawberries', 'Quantity': '98'}
```
The DictReader object sets row to a dictionary object with keys derived from the headers in the first row. 

Using DictReader means that we don't need additional code to skip the first row's header information. Instead we can actually use the header to our advantage and access values from the dict.

If we open a DictReader object with a csv file that does not have column headers in the first row, we have to supply the DictReader function with a second argument containing header names like:

```python
import csv


file = open('example.csv')
fileDictReader = csv.DictReader(file,['column1', 'column2', 'column3'])

```

## JSON

JavaScript Object Notation, a.k.a JSON, is a popular way to format data as a single human-readable string. JSON is the native way that JavaScript programs write their data structure and usually resembles what Python's pprint() function would produce.

JSON is useful to know because many websites offer JSOn content as a way for external programs to interact with the website. This is known as providing an API. Accessing an API is the same as accessing any other web pages via a URL. The difference is that the data returned by an API is formatted for machines, e.g JSON. APIs aren't easy for humans to read.

### The json module

The Python's json module handles all the details of translating between a string with Python data and Python values for the json.loads() and json.dumps() functions.

JSON can't store every kind of Python value, it can contain values of the following data types: strings, integers, floats, Booleans, lists, dictionaries and NoneType. It cannot represent Python objects like reader, writer, regex or WebElement.

Note: *JSON strings always use double quotes*.

These are the useful functions of the json module:

- `json.loads()`: This translate a string containing JSON data into a Python value. The name means "load string".
```python
import json

stringOfJsonData = '''{"name": "Roku", "breed": "Dog", "isCrazy": true,
"IQ": 99, "goodTraits": null}'''

print(type(stringOfJsonData))

jsonData = json.loads(stringOfJsonData)

print(type(jsonData))
print(jsonData)
```

```
: <class 'str'>
: <class 'dict'>
: {'name': 'Roku', 'breed': 'Dog', 'isCrazy': True, 'IQ': 99, 'goodTraits': None}
```
- `json.dumps()`: This dump string i.e translate a Python value into a string of JSON-formatted data.
```python
import json

dictOfPythonData = {"name": "Roku", "breed": "Dog", "isCrazy": True,
"IQ": 99, "goodTraits": None}

print(type(dictOfPythonData))

jsonData = json.dumps(dictOfPythonData)

print(type(jsonData))
print(jsonData)
```

```
: <class 'dict'>
: <class 'str'>
: {"name": "Roku", "breed": "Dog", "isCrazy": true, "IQ": 99, "goodTraits": null}
```
# Chapter 17 - Keeping Time, Scheduling Tasks and Launching Programs

Running programs while we are sitting at the computer is fine however it would also be useful to have programs run without our supervision. We can use our computer's clock to run code at some specified time and date or at regular interval. One example is that we can schedule for a website to be scraped every hour to check for changes.

We can also write programs that launch other programs on a schedule by using `subprocess` and `threading` modules.

```
Often, the fastest way to program is to take advantage of applications that other people have written.
```

## The `time` module

The built-in `time` module allows our Python programs to read the system clock for the current time. The two most useful functions are `time.time()` and `time.sleep()` in the time module.

### The `time.time()` function

```python
import time

print(time.time())
```

```
: 1591106587.4600317
```
The `time.time()` function returns the number of seconds since *the Unix epoch* as a float value. The Unix epoch is a time reference commonly used in programming: 12 AM on January 01, 1970. 

Epoch timestamps can be used to profile code, that is to measure how long a piece of code takes to run. 

```python
import time

def calcProd():
	# Calculatea the product of the first 100,000 number
	product = 1
	for i in range(1, 100000):
		product = product * i
	return product

startTime = time.time()
prod = calcProd()
endTime = time.time()

print('The result is %s digits long.' % (len(str(prod))))
print('Execution of calcProd took %s seconds' % (endTime - startTime))

```

```
: The result is 456569 digits long.
: Execution of calcProd took 2.228208065032959 seconds
```
### The `time.ctime()` function

The return value from `time.time()` is useful but not human-understandable. Instead we can use `time.ctime()` which returns a string description of the current time. It can also take a return value from `time.time()`.

```python
import time

time1 = time.time()

time2 = time.ctime()

print(time1)
print(time2)
print(time.ctime(time1))
```

```
: 1591107070.4035943
: Wed Jun  3 00:11:10 2020
: Wed Jun  3 00:11:10 2020
```
### The `time.sleep()` function

This function is useful if we need to pause our programe for a while. We can pass the number of seconds we want our program to stay paused.

The function will block i.e it will not return and release our program to execute other code until the number of seconds we passed has elapsed.

### Rounding number

When working with times, we'll be working with float values with many decimal points. To make these easier to work with we should use the built-in `round()` function.

```python
import time

now = time.time()

print(now)
print(round(now,2))
print(round(now))
```

```
: 1591107292.9855552
: 1591107292.99
: 1591107293
## The `datetime` module
```
The time module is useful for getting Unix epoch timestamp to work with, however the datetime module is more useful if we want to display date in a more convenient format, or if we want to do arithmetic with dates.

The `datetime` has its own `datetime` data type which represent a specific moment in time.

```python
import datetime

now = datetime.datetime.now()

print(type(now))
print(now)

then = datetime.datetime(2020, 6, 3)
print(then)
```

```
: <class 'datetime.datetime'>
: 2020-06-03 00:22:10.621285
: 2020-06-03 00:00:00
```
We can also convert a Unix epoch timestamp to a `datetime` object with the `datetime.datetime.fromtimestamp` function:
```python
import datetime, time

now = time.time()

print(now)
print(datetime.datetime.fromtimestamp(now))
print(datetime.datetime.fromtimestamp(1000000000))
```

```
: 1591107903.512297
: 2020-06-03 00:25:03.512297
: 2001-09-09 11:46:40
```
We can also compare `datetime` objects with each other using comparison operator to find out which one precedes the other.

```python
import datetime

now = datetime.datetime.now()
then = datetime.datetime.fromtimestamp(100000000)

print(now)
print(then)

print(now > then)
```

```
: 2020-06-03 00:28:16.007089
: 1973-03-03 20:46:40
: True
## The `timedelta` data type
```
The `datetime` module also provides a `timedelta` data type which represents a *duration* of time rather than a *moment* of time.

```python
import datetime

delta = datetime.timedelta(days=11, hours=12, minutes=9, seconds=10)
print(type(delta))
print(delta)
print(delta.days)
print(delta.total_seconds())
```

```
: <class 'datetime.timedelta'>
: 11 days, 12:09:10
: 11
: 994150.0
```
To create a `timedelta` object we simply use the `datetime.timedelta()` function which takes keyword arguments `weeks`, `days`, `hours`, `minutes`. `seconds`, `milliseconds` and `microseconds`. There is no month or year keyword argument because a month or a year is a variable amount of time that is dependent on the particular month or year.

Arithmetic operations can also be used to perform date arithmetics on `datetime` value.

In the below example, we calculate the date that is 1000 days from today:

```python
import datetime

now = datetime.datetime.now()
then = now + datetime.timedelta(days=1000)

print(then)
```

```
: 2023-02-28 00:34:08.559678
## Pausing until a specific date
```
The `time.sleep()` method can be used in conjuction with the `datetime` module.

For example, we can use a `while` loop to let the program sit for until a specific point in time.

```python
import datetime, time

now = datetime.datetime.now()

print('Now is %s' % (now))

then = datetime.datetime(2020, 6, 3, 00, 46, 00)

while datetime.datetime.now() < then:
	time.sleep(1)

print(datetime.datetime.now())
```

```
: Now is 2020-06-03 00:45:53.589940
: 2020-06-03 00:46:00.597140
```
##  Converting `datetime` object into and from strings

Epoch timestamps and datetime object aren't very friendly to the human eyes. We can use the `strftime()` method to display a `datetime` object as a string. The *f* in `strftime` function stands for format. It takes a format string argument that contains the formatting directives.

The full strftime directives can be found here: https://strftime.org/

```python
import datetime

now = datetime.datetime.now()

print(now.strftime('%Y %m %d'))
print(now.strftime('%y, %B, %d %A'))
```

```
: 2020 06 03
: 20, June, 03 Wednesday
```
Conversely, if we have a string of datetime information and need to convert it to a `datetime` object, we can also use the `datetime.datetime.strptime()` function which is the inverse of `strftime()` method. This function also takes a custom format string that uses the same directives as the `strftime()` method, along with the string of course. The *p* stands for parse.

```python
import datetime

a_string = '01 Jan 2020 12:34:56'

a_datetime = datetime.datetime.strptime(a_string, '%d %b %Y %H:%M:%S')

print(a_datetime)


```

```
: 2020-01-01 12:34:56
```
## Launching other programs from Python

Our Python program can start other pgorams on our computer with the `Popen()` function in the built-in `subprocess` module. The P in the name of `Popen()` function stands for process. 

```python
import subprocess

test = subprocess.Popen('/usr/bin/code')

print(type(test))
print(test)
```

```
: <class 'subprocess.Popen'>
: <subprocess.Popen object at 0x7faa6e7a2d90>
```
The return value is Popen object which has two useful methods: `poll()` and `wait()`.

The `poll()` method can be thought of asking our driver "Are we there yet?" over and over until we arrive at the destination. It will return `None` if the process is still running at the time `poll()` is called. If the programe has terminated, it will return the process's integer exit code. 

An exit code of 0 means the process terminated without errors and an exit code of nonzero, most notably being 1 but may vary depending on the programe, means that the process terminater with error.

With the `Popen()` function, we can also pass command line arguments to processes we create. To do this we pass *a list* as the sole argument to `Popen()`. The first string in the list will be the executable filename of the program we want to launch; all the subsequent strings will be the command line arguments to pass to the program when it starts. These subsequent strings are the values of `sys.argv` of the launched program.

We can also open files with default applications. Each operating system has a programe that performs the equivalent of double-clicking on a document file to open it. On Windows, this is the *start* program. On Mac OS, this is the *open* program. On Ubuntu, this is the *see* program.

On Windows, this will open the 'text.txt' file with the default application that is associated with the .txt file extension:

```python
subprocess.Popen(['start', 'text.txt'], shell=True)
```

(The `shell=True` keyword argument is needed only on Windows.)

# Chapter 18 - Sending Email and Text Messages

With Python we can automate a lot of email-related tasks. For example we may have a spreadsheet full of customer records and want to send each customer a different form letter depending on their age and location details. Standard Email applications might not be able to do this for us. However we can write one with Python.

We can also write programs to send emails and SMS texts to notify us of things even when we are away from the computer.

This chapter features the EZGmail module - a simple way to send and read emails from Gmail accounts. It is also a Python module for using the standard SMTP and IMAP email protocols.

## Gmail API
### The Gmail API - Enabling

 Gmail is a big player in the email client market. Most people own at least one Gmail email address. Due to Gmail's additional security and anti-spam measures, it is easier to control a Gmail account through EZGmail module than through smtplib and imapclient.

 EZGmail is actually written by the author of this book. - Al Sweigart.

 First we need a Gmail account to use.

 Then we need to go to https://developers.google.com/gmail/api/quickstart/python/ and click *Enable the Gmail API*.

 After filling up the form we will be able to download a *credentials.json* file which contains authentication information for Gmail. We should treat this like our Gmail password and noot share with anyone.

 Then we can authenticate the app by:
 ```python
 import os, ezgmail

 os.chdir(r'/path/to/credentials_json_file/')
 ezgmail.init()
 ```

 One of the important thing is that we need to set our current working directory to the same folder that *credentials.json* is in and that we are connected to the Internet. The `ezgmail.init()` will open a browser process to a Google sign-in page. After we have logged in, for the first time we'd be asked to authenticate. After we have *allow* our program to use Gmail and close the browser, a *token.json* file will be generated in the same directory as *credentials.json*.

 With both the *credentials.json* and *token.json* files, our Python scripts can send and read emails from our Gmail account withour requiring to include the Gmail password in our source code.

 Note: The `ezgmail.init()` function only opens to the login page of Gmail if it cannot find an existing *token.json* file.

### Gmail API - Sending email

 Once we have done the init authentication, we can send an email like this:

 ```python
 import os, ezgmail

 os.chdir(r'/path/to/credentials_json_file/')

 ezgmail.send('example@example.com', 'Hello Subject', 'Hello body')
 ```

 [[./images/ezgmail1.png]]

 We can alo send an attachment by providing an extra list argument to the `send()` function:

 ```python
 import os, ezgmail

 os.chdir(r'/path/to/credentials_json_file/')

 ezgmail.send(
     'example@example.com', 
     'Hello test attachment', 
     'Please find attachment',
     ['example.csv']
 )
 ```

 [[./images/ezgmail2.png]]

 We can also use the optional keyword *cc* and *bcc* to send carbon copies and blind carbon copies.

 If we need print which Gmail address the *token.json* file is configured for, we can do this:

 ```python
 import os, ezgmail

 os.chdir(r'/path/to/credentials_json_file/')

 print(ezgmail.EMAIL_ADDRESS)
 ```

### Gmail API - Reading mail from a Gmail account

 Gmail organizes emails that are replies to each other into *conversation threads*.

 EZGmail has `GmailThread` and `GmailMessage` objects to represent conversation threads and individual emails respectively. 

 A `GmailThread` has a `message` attribute that holds a list of `GmailMessage` objects. The `unread()` function returns a list of `GmailThread` objects for all unread emails. This list can be passed to `ezgmail.summary()` to print a summary of conversation threads in that list.

 ```python
 import os, ezgmail

 os.chdir(r'/path/to/credentials/and/token/json/files/')

 unreadThreads = ezgmail.unread()

 print(type(unreadThreads))
 print(unreadThreads)
 ```

 ``` 
 <class 'list'>
 [<ezgmail.GmailThread object at 0x7f8657bf0cd0>, <ezgmail.GmailThread object at 0x7f8657bf0c10>, <ezgmail.GmailThread object at 0x7f8657bf0e80>, <ezgmail.GmailThread object at 0x7f8657bf0df0>, <ezgmail.GmailThread object at 0x7f8657bf0d00>, <ezgmail.GmailThread object at 0x7f8657bf0eb0>, <ezgmail.GmailThread object at 0x7f8657bf0e50>, <ezgmail.GmailThread object at 0x7f8657bf0f40>, <ezgmail.GmailThread object at 0x7f8657bf0fd0>, <ezgmail.GmailThread object at 0x7f8657bf9130>, <ezgmail.GmailThread object at 0x7f8657bf90a0>, <ezgmail.GmailThread object at 0x7f8657bf90d0>, <ezgmail.GmailThread object at 0x7f8657bf91c0>, <ezgmail.GmailThread object at 0x7f8657bf9220>, <ezgmail.GmailThread object at 0x7f8657bf9280>, <ezgmail.GmailThread object at 0x7f8657bf92e0>, <ezgmail.GmailThread object at 0x7f8657bf9340>, <ezgmail.GmailThread object at 0x7f8657bf93a0>, <ezgmail.GmailThread object at 0x7f8657bf9400>, <ezgmail.GmailThread object at 0x7f8657bf9460>, <ezgmail.GmailThread object at 0x7f8657bf94c0>, <ezgmail.GmailThread object at 0x7f8657bf9520>, <ezgmail.GmailThread object at 0x7f8657bf9580>, <ezgmail.GmailThread object at 0x7f8657bf95e0>, <ezgmail.GmailThread object at 0x7f8657bf9640>]
 ```

 We can also print a summary of our unread message like this:

 ```python
 print(ezgmail.summary(unreadThreads))
 ```

 The `summary()` function is useful for displaying a quick summary of the email threads. However to access specific messages and part of messages, we want to examine the `messages` attribute of the `GmailThread` object. This attribute contains a list of `GmailMessage` objects that make up the thread. 

 Each of these `GmailMessage` object has `subject`, `body`, `timestamp`, `sender` and `recipient` attributes that describe the email.

 ```python
 import os, ezgmail

 os.chdir(r'/path/to/credentials/and/token/json/files/')

 unreadThreads = ezgmail.unread()

 print(unreadThreads[0].messages[0].subject)
 print(unreadThreads[0].messages[0].sender)
 print(unreadThreads[0].messages[0].timestamp)
 print(unreadThreads[0].messages[0].body)
 print(unreadThreads[0].messages[0].recipient)
 ```

 ``` 
 Security alert
 Google <no-reply@accounts.google.com>
 2020-06-04 00:46:50
 [image: Google]
 Quickstart was granted access to your Google Account


 example@gmail.com

 If you did not grant access, you should check this activity and secure your
 account.
 Check activity
 <https://accounts.google.com/AccountChooser?Email=example@gmail.com&continue=https://myaccount.google.com/alert/nt/1591195610000?rfn%3D127%26rfnc%3D1%26eid%3D41823708300075176%26et%3D0>
 You received this email to let you know about important changes to your
 Google Account and services.
 © 2020 Google LLC, 1600 Amphitheatre Parkway, Mountain View, CA 94043, USA

 example@gmail.com
 ```

 Similar to the `ezgmail.unread()` function, the `ezgmail.recent()` function will return the *25 most recent* threads in the Gmail account. We can also pass an optional `maxResults` keyword argument to change this limit:

 ```python
 import os, ezgmail

 os.chdir(r'/path/to/credentials/and/token/json/files/')

 recentThreads = ezgmail.recent()
 print(len(recentThreads))

 recentThreads = ezgmail.recent(maxResults=200)
 print(len(recentThreads))
 ```

 ``` 
 25
 200
 ```

### Searching Mail from a Gmail account

 In addition to using `ezgmail.unread()` and `ezgmail.recent()`, we can search for specific emails the same way we would if we entered queries into https://gmail.com/ search box by calling `ezgmail.search()`.

 ```python
 import os, ezgmail


 os.chdir(r'/path/to/credentials/and/token/json/files/')

 search = ezgmail.search('Google', maxResults=100)
 print(len(search))

 ```

 ``` 
 100
 ```

 Similarly to `ezgmail.unread()` and `ezgmail.recent()`, `ezgmail.search()` returns a list of `GmailThread` obejcts. Similarly to using the Google Mail search box, we can also pass any of the special search operators to the `search()` function like:
 - 'label:UNREAD'
 - 'from:hello@world.com' 
 ..

### Downloading Attachments from a Gmail account

 The `GmailMessage` objects have an attachments attribute that is a list of filenames for the message's attached files.

 We can pass any of these names to the `GmailMessage` object's `downloadAttachment()` method to download the files. Or, if we want to download all of them we can do `downloadAllAttachments()`. 

 By default, EZGmail saves attachments to the current working directory, however we can also pass an additional `downloadFolder` keyword argument to these functions.

 If a file already exists with the attachment's filename, the downloaded attachments will automatically overwrite the existing file.

## SMTP

### init
 Similarly to how HTTP is the protocol used by computers to send web pages across the internet, Simple Mail Transfer Protocol is the protocol used for sending emails.

 SMTP dictates how email messages should be formatted, encrypted and relayed between mail servers and all other details that our comptuer handles after we click Send.

 These are the things that we do not need to know because Python's `smtplib` module simplifies them into a functions.

 SMTP just deals with sending emails to others.

 In other to SMTP and IMAP, which is the protocol for retrieving emails, most web-based email providers nowadays have other security measures in place to protect users against spam, phishing and other malicious email usage. Although we have only learned how to access the Google API, most other email services have thier own API and spcific Python modules that allow scripts to access them. We just need to follow their online documentation.

 We can init a `SMTP` object by calling the domain name as a string argument then passing the port as an integer argument.

 ```python
 import smtplib


 smtpObj = smtplib.SMTP('outlook.office365.com', 587)

 print(type(smtpObj))
 ```

 ``` 
 <class 'smtplib.SMTP'>
 ```

 We'll need this SMTP object in order to call the methods to log us in and send emails. If the `smtplib.SMTP()` call is not successful, our SMTP server might not support TLS on port 587. In this case we would need to switch to port SSL on 465.

### Greeting
 Once we have a SMTP object, we can "say hello" to the SMTP server by calling an oddly named method `ehlo()`. This greeting is the first step in SMTP and is important for establishing a connection to the server. Althougu we don't need to know exactly what it does, we have to be sure to call the `ehlo()` method first thing after getting the SMTP object or else later method calls will result in errors.

 ```python
 print(smtpObj.ehlo())
 ```
 ``` 
 (250, b'ME1PR01CA0111.outlook.office365.com Hello [43.250.204.83]\nSIZE 157286400\nPIPELINING\nDSN\nENHANCEDSTATUSCODES\nSTARTTLS\n8BITMIME\nBINARYMIME\nCHUNKING\nSMTPUTF8')
 ```

 If the first item returned in the tuple is the integer 250 (the SMTP status code for 'Success'), then the greeting succeeded and we are good to go.

### Starting TLS Encryption

If we are connecting to port 587 on the SMTP server, i.e if we are using TLS encryption, we'll need to call the `starttls()` method next. This is a required step to enable encryption for our connection. This is not needed if we are connected to a SMTP server via port 465 (SSL). If SSL, encryption is already set up and we don't need to `starttls()`.

The `starttls()` method puts our SMTP connection in TLS mode. The 220 in return tells us that the server is ready.
``` 
>>> smtpObj.starttls()
(220, b'2.0.0 SMTP server ready')
```

### Logging in to the SMTP server

Once our encrypted connection to the SMTP server is set up, we can log in with our username and password by calling the `login()` method.

``` 
>>> smtpObj.login('username@domain.org','Password')
(235, b'2.7.0 Authentication successful')
```

### Sending an Email

Once we are logged in to our email provider's SMTP server, we can call the `sendmail()` method to send the email.

The `sendmail()` method requires three arguments:
- Our email address as a string (for the emails "from" address)
- The recipient's email address as a string, or a list of string for multiple recipient (for the "to" address(es))
- The email body as a string. The start of the email body string *must* begins with a Subject in this format: *'Subject:..\n'*. This will be used for the Subject line. The \n newline character separates the subject from the main body of the email.

The return value from sendmail is a dictionary. There will be one key-value pair in the dictionary for each recipient for whom email delivery *failed*. An empty dictionary means all emails were sent to recipients successully.

``` 
>>> result = smtpO.sendmail('hello@outlook.com', 'hithere@gmail.com', 'Subject: Helo World\nHi there, how are you?')
```

### Disconnecting from the SMTP server

When we are done with sending emails, we need to call the `quit()` method.

```
>>> smtpO.quit()
(221, b'2.0.0 Service closing transmission channel')
```

The returned 221 means the session is ending.

## IMAP

Just as SMTP is the protocol for sending email, the *Internet Message Access Protocol* (IMAP) specifies how to communicate with an email provider's server to retrieve email sent to your email address.

Python comes with *imaplib* however the third party [[https://imapclient.readthedocs.io/.][*imapclient*]] is easier to use.

The imapclient module downloads emails from an IMAP server in a rather complicated format. In most situation we'd then want to parse this data and convert them into simple string values. The *pyzmail* module can does the parsing bit.

### Retrieving and deleting emails with imap

Finding and retrieving emails in Python is a multistep process that requires both *imapclient* and *pyzmail* modules.

# Chapter 19 - Manipulating Images
## Pillow 
In Python, we can use *Pillow*. Pillow is a third-party Python module that can be used for interacting with image files. There are several functions in this library that make it easy to crop, resize and edit the content of an image in similar way that we would use with GUI software such as Microsoft Paint or Adobe Photoshop. With Python and Pillow we can automatically edit hundreds or thousands of images with ease.

## Computer Image Fundamentals
### Colors and RGBA Values

A color within a computer image is most often represented as an *RGBA* value by computer programs. An RGBA value is a group of numbers that specify the amount of red, green, blue and alpha in a color. Alpha represents transparency.

Each of RGBA component values is an integer from 0 to 255. These RGBA values are assigned to individual *pixels*. Each pixel is the smallest dot of a single color the computer screen can show. There are millions of pixels on a screen. A single pixel's RGB setting tells it precisely what shade of a color it should display. 

Images also have an alpha value to create RGBA values. The Alpha is used in situation when the image is displayed on the screen over a background image or desktop wallpaper. It determines how much of the background the user can "see through" the image's pixel.

In Pillow, RGBA values are represented by a tuple of *four integer values*. For example, Red is (255, 0, 0, 255), Green is (0, 255, 0, 255). Blue is (0, 0, 255, 255). White is (255, 255, 255, 255) while black is (0, 0, 0, 255).  If a color has an alpha value of 0, it is invisible no matter what the RGB values are.

Pillows offer the `ImageColor.getcolor()` function so we don't have to memorize the RGBA values for the colors we want to use. This function takes two arguments, first is color name string and second is 'RGBA' string and the return value is a RGBA tuple.

```python
from PIL import ImageColor as IC

red = IC.getcolor('red', 'RGBA')
print('Red is', red)

black = IC.getcolor('black', 'RGBA')
print('Black is', black)

chocolate = IC.getcolor('chocolate', 'RGBA')
print('Chocolate is', chocolate)

cornflowerBlue = IC.getcolor('CornflowerBlue', 'RGBA')
print('Cornflower Blue is', cornflowerBlue)

```

```
: Red is (255, 0, 0, 255)
: Black is (0, 0, 0, 255)
: Chocolate is (210, 105, 30, 255)
: Cornflow Blue is (100, 149, 237, 255)
```
Pillow supports [[https://www.w3schools.com/colors/colors_names.asp][140 common HTML color names]]. Color names are case insensitive. Example: 'red', 'Red', 'whitesmoke', 'aliceblue'.

### Coordinates and Box Tuples

Image pixels are addressed with x- and y- coordinates, which respectively specify a pixel's horizontal and vertical locations in an image. The *origin* is the pixel at the top-left corner of the image and is specified with the notation (0,0). 

The first zero represents the x-coordinate which starts at zero at the origin and increases going from left to right. The second zero represents the y-coordinate which starts at zero at the origin and increases going down the image.

[[./images/imagecoor.jpg]]

Many of Pillow's function and methods take a *box tuple* argument which expect a tuple of *four* integer coordinates that represent a *rectangular region* in an image. The four integers are in order as follow:
- *Left*: The x-coordinate of the leftmost edge of the box.
- *Top*: The y-coordinate of the top edge of the box.
- *Right*: The x-coordinate of one pixel to the right of the rightmost edge of the box. This must be greater than left integer.
- *Down*: The y-coordinate of one pixel lower than the bottom edge of the box. This integer must be greater than the top integer.

The box includes the left and top coordinates but only goes upto and not include the right and bottom coordinates.

For example, a box tuple of `(3, 1, 9, 6)` represents the following area:

[[./images/000115.jpg]]

## The Image object

Let's start working on this image:

[[./images/cat.png]]

To load the image, we do this. The `catIm` variable is used to store the image file.

```python
from PIL import Image
import os


# Cd to the directory of this script
pwd = os.path.dirname(os.path.realpath(__file__))
os.chdir(pwd)

catIm = Image.open('cat.jpg')
print(type(catIm))
```

``` 
<class 'PIL.JpegImagePlugin.JpegImageFile
```

Notes:
- Pillow's module name is PIL to make it backward compatible with an older module named Python Imaging Library.
- Because of the way Pillow's creater set up the pillow module, *we must use import statement* from PIL rather than simply import PIL.

## Working with the Image Data Type

An image object has several useful attributes that gives us basic information about the image file it was loaded from, like its width and height, filename and graphic format.

```python
from PIL import Image
import os


# Cd to the directory of this script
pwd = os.path.dirname(os.path.realpath(__file__))
os.chdir(pwd)

catIm = Image.open('cat.jpg')

print(catIm.size)

width, height = catIm.size
print('Width = ', width)
print('Height = ', height)

print(catIm.filename)
print(catIm.format)
print(catIm.format_description)
```
 
``` 
(319, 426)
Width =  319
Height =  426
cat.jpg
JPEG
JPEG (ISO 10918)
```

## Saving image

What we are going to do is to call the `save()` method and on the original image and pass it 'zophie.png' to save a new image. Pillow sees the extension as '.png' and will automatically saves the iamge using the PNG format.

```python
from PIL import Image
import os


# Cd to the directory of this script
pwd = os.path.dirname(os.path.realpath(__file__))
os.chdir(pwd)

catIm = Image.open('cat.jpg')

catIm.save('cat.png')
```

Although the two image files are based on the same image, they are not identical because of their different formats.

## Creating a new Image

We can also use the `Image.new()` function which returns an Image object, much like `Image.open()`, except that the image represented by this new object will be blank.

`Image.new()` takes several arguments. These are:

- The string 'RGBA' which sets the color mode to RGBA. (There are other modes).
- The size, as a two-integer tuple of the new image's width and height.
- The background color that the image should start with as a four integer tuple of an RGBA value. We can use the return of the `ImageColor.getcolor()` for this argument. Alternative `Image.new()` also accepts a string argument of the standard color name. If no color argument is provided, invisible black (0, 0, 0, 0) is used.

## Cropping Images

Cropping an image basically means selecting a rectangular region inside an image and removing outside the rectangle. The `crop()` method on `Image` object takes a box tuple and returns an Image object represent the cropped image.

The cropping does not happen in place. This means the original image is left untouched and the `crop()` method returns a new Image object.

For example, let's come back to our original *cat.png* and crop the head of cat.

```python
from PIL import Image
import os


# Cd to the directory of this script
pwd = os.path.dirname(os.path.realpath(__file__))
os.chdir(pwd)

catIm = Image.open('cat.png')

catHead = catIm.crop((335, 345, 565, 560))
catHead.save('cathead.png')
```

[[./images/cathead.png]]

## Copying and Pasting Images onto Other images

The `copy()` method will return a new Image object with the same image as the Image object it was called on. This is quite useful if we need to make changes to an image but also want to keep the original untouched.

For example,

```python
catIm = Image.open('cat.png')

catCopy = catIm.copy()
```

The *catCopy* and *catIm* variables contain two seperate Image object which is the same image. Now we can do whatever we want with *catCopy*. The original image will remain untouched.

The `paste()` method is called on an Image object. It pastes another image on top of it.

Let's try this,

```python
from PIL import Image
import os


# Cd to the directory of this script
pwd = os.path.dirname(os.path.realpath(__file__))
os.chdir(pwd)

catIm = Image.open('cat.png')

catCopy = catIm.copy()
catFace = catCopy.crop((355, 345, 565, 560))
catCopy.paste(catFace)
catCopy.save('cat2.png')
```

This is *cat2.png*:

[[./images/cat2.png]]

The `paste()` method actually takes two arguments - the source iamge object and a tuple of x- and y- coordinates where we want to paste the image onto. In the above example we didn't use the second argument so the coordinate values were just (0, 0).

Let's try again:

```python
from PIL import Image
import os


# Cd to the directory of this script
pwd = os.path.dirname(os.path.realpath(__file__))
os.chdir(pwd)

catIm = Image.open('cat.png')

catCopy = catIm.copy()
catFace = catCopy.crop((355, 345, 565, 560))
catCopy.paste(catFace, (400, 500))
catCopy.save('cat3.png')
```

[[./images/cat3.png]]
/cat3.png/

We can also tile the cat head image across the entire original image like this:

```python
from PIL import Image
import os


# Cd to the directory of this script
pwd = os.path.dirname(os.path.realpath(__file__))
os.chdir(pwd)

catIm = Image.open('cat.png')
catImWidth, catImHeight = catIm.size 

catFace = catIm.crop((355, 345, 565, 560))
catFaceWidth, catFaceHeight = catFace.size

catCopy = catIm.copy()

for left in range(0, catImWidth, catFaceWidth):
    for top in range(0, catImHeight, catFaceHeight):
        print(f"At ({left}, {top})")
        catCopy.paste(catFace, (left, top))

catCopy.save('cat4.png')
```

[[./images/cat4.png]]
/cat4.png/

## Resizing an Image

To resize an iamge, we can call the `resize()` method on an Image object. The return object will be the original image with the specified width and height.

For example, to resize an image to a third of it:
```python
from PIL import Image
import os


# Cd to the directory of this script
pwd = os.path.dirname(os.path.realpath(__file__))
os.chdir(pwd)

catIm = Image.open('cat.png')
catImWidth, catImHeight = catIm.size 
print(catIm.size)

catIm2 = catIm.resize((int(catImWidth / 3), int(catImHeight / 3)))
print(catIm2.size)
```

``` 
(816, 1088)
(272, 362)
```

*Note:* The argument that you pass to `resize()` has to be a tuple representing the new width and height of the returned image respectively. The `resize()` method only accepts integers in its tuple argument, which is why we need to wrap the the divisions in an `int()` call.

The above resizing keeps the same proportion for the width and height of the original image. This does not have to be the case. The new width and height that `resize()` do not have to be proportional to the original image. However the new image would look stretchy if we decide to do it this way.

`resize()` does *not* edit the image in place. Instead, it returns an image object.

## Rotating and Flipping images

Images can be rotated with the `rotate()` method which returns a new Image object of the rotate image. The `rotate()` method also does not edit the image inplace.

The argument to `rotate()` is a single integer or float representing the number of degrees to rotate the image *counterclockwise*. 

```python
from PIL import Image
catIm = Image.open('cat.png')
catIm.rotate(90).save('rotated90.png')
catIm.rotate(180).save('rotated180.png')
catIm.rotate(270).save('rotated270.png')
```

[[./images/cat-rotate.png]]
/The original image (left) and the image rotated counterclockwise by 90, 180, and 270 degrees/

The `rotate()` method also has an optional keyword argument `expand` that can be set to `True` to enlarge the dimension of the new image *to fit the entire rotated new image* without being cropped.

We can also use the `transpose()` method to get a "mirror flip" of an image, like this:

```python
catIm.transpose(Image.FLIP_LEFT_RIGHT)
catIm.transpose(Image.FLIP_TOP_BOTTOM)
```

The `transpose()` method has to be passed either the `Image.FLIP_LEFT_RIGHT` or `Image.FLIP_TOP_BOTTOM`. 

## Changing individual Pixels

The two `getpixel()` and `putpixel()` methods can be used to retrieve or set a color of an individual pixel. Both of these methods take a tuple representing the x- and y- coordinates of the pixel. The `putpixel()` also takes an additional tuple argument for the color of the pixel that you want to put. This argument is a a four-integer RGBA tuple or a three-integer RGA tuple.



We can use Python to control other applications by sending them virtual keystrokes and mouse click, as if we were sitting at the computer and interacting with the applications ourself. This practice is called *graphical user interface automation* or *GUI Automation*. 

In this chapter, we'll learn to use the module *pyautogui*.

# Chapter 20 - GUI Automation

## Installing & setting up

Of course we have to do a `pip install pyautogui` for our system. For Windows and Mac OS users, this is enough. However for Linux users, we'd first have to install some software that PyAutoGui depends on. These are: `scrot`, `python3-tk`, `python3-dev`.

For Mac OS X, we'd also have to set the programming running our Python script to be an accessibility application. For example, if we are using Mu, IDLE, VSCode, or the Terminal, we need to have the application open, then open System Preferences and go to the Accessibility tab and allow the app to control the computer.

## Staying on track

Before we jump into the art of GUI automation, we should know how to escape problems that may arise. Once we execute the script, Python move our mouse and type keystrokes at an incredible speed that sometimes may be too fast for other programs to keep up with. Moreover, if anything goes wrong, the error could be pretty hard to caught.

Stopping the program can be challenging if the mouse is moving around on its own. However, there are several ways to prevent or recover from GUI automation problems.

### PyAutoGUI's fail-safe feature

Every PyAutoGUI function call has a 1/10 second delay after performing its action to give us enough time to move the mouse to a corner. If PyAutoGUI detects that the mouse cursor is in a corner, it will raise the `pyautogui.FailSafeException` exception. 

If we find ourself in a situation where we need to stop the PyAutoGUI programe, we need to quickly move the mouse towards a corner to stop it.

### Shutting down everything by logging out

One option but we'd lose all unsaved work.

## Controlling Mouse Movement

Before jumping into mouse movement and automation, we need to understand how PyAutoGUI works with coordinates.

The mouse functions of PyAutoGUI use x- and y-coordinates. It's similar to the coordinate system used for images. The origin, where x and y are both zero is at the upper-left corner of the screen. The x-coordinate increase going to the right and the y-coordinate increase going down the screen.

All coordinate are positive.

This image shows the coordinate of a computer screen with 1920x1080 resolution.

[[./images/screencoordinates.jpg]]

```python
import pyautogui
print(pyautogui.size())
```

```
: Size(width=4920, height=1920)
```
### Moving the mouse

Our mouse cursor can be moved to specific screen coordinates with the `pyautogui.moveTo()` function. Integer values of x- and y- coordinates make up the function's first and second arguments respectively. 

There is also an optional argument `duration` integer or float that specifies *the number seconds it should take to move the mouse to the destination*. Without this the movement occurs instantaneously.

We can automate our mouse to move the cursor clockwise in a square pattern 10 times like this:

```python
import pyautogui

for i in range(10):
    pyautogui.moveTo(100, 100, duration=0.1)
    pyautogui.moveTo(200, 100, duration=0.1)
    pyautogui.moveTo(200, 200, duration=0.1)
    pyautogui.moveTo(100, 200, duration=0.1)
```

The `mouseTo()` function moves the cursor to a given pair of coordinates. The `pyautogui.move()` function can also be used to move the mouse cursor relative to its current position.

In the below script, we'll do the same thing which is to move the cursor clockwise in a square pattern 10 times, starting from where our cursor is when we execute the script.

```python
import pyautogui

for i in range(10):
    pyautogui.move(100, 0, duration=0.1)
    pyautogui.move(0, 100, duration=0.1)
    pyautogui.move(-100, 0, duration=0.1)
    pyautogui.move(0, -100, duration=0.1)
```
### Getting the mouse position

We can also call the mouse's current position by calling the `pyautogui.position()` function. It will return a `Point` named tuple of the mouse's cursor x- and y-coordinate at the time the function is called.

```python
import pyautogui

for i in range(5):
    print(i)
    pyautogui.move(100, 0, duration=0.1)
    print(pyautogui.position())
    pyautogui.move(0, 100, duration=0.1)
    print(pyautogui.position())
    pyautogui.move(-100, 0, duration=0.1)
    print(pyautogui.position())
    pyautogui.move(0, -100, duration=0.1)
    print(pyautogui.position())
```

```
0
Point(x=2304, y=983)
Point(x=2304, y=1083)
Point(x=2204, y=1083)
Point(x=2204, y=983)
1
Point(x=2304, y=983)
Point(x=2304, y=1083)
Point(x=2204, y=1083)
Point(x=2204, y=983)
2
Point(x=2304, y=983)
Point(x=2304, y=1083)
Point(x=2204, y=1083)
Point(x=2204, y=983)
3
Point(x=2304, y=983)
Point(x=2304, y=1083)
Point(x=2204, y=1083)
Point(x=2204, y=983)
4
Point(x=2304, y=983)
Point(x=2304, y=1083)
Point(x=2204, y=1083)
Point(x=2204, y=983)
```
### Controlling the Mouse Interaction
#### Clicking the Mouse
```
A virtual mouse click to the computer can be called using the `pyautogui.click()` method. By default, this click uses the left mouse button and takes place wherever the mouse cursor is located. Alternatively if we want the clicking to happen somewhere else, we can pass the x- and y- coordinates as the optional first and second arguments.

There is also an optional keyword argument `button` that takes a value of `left`, `middle` or `right`. 

What a `click()` call does is pushing a mouse button down and then releasing it back up without moving the cursor. We can also perform `mouseDown()` and `mouseUp()` which only releases the button. The `click()` function is actually just a wrapper of these two function calls.

We can also call the `doubleclick()` function which performs two clicks with the left mouse button. We can also use the `rightClick()` or `middleClick()` functions that will perform a right anhd middle mouse buttons respectively. 
#### Dragging the mouse

The dragging action means to move the mouse while holding down one of the mouse buttons. For example we can move files between folders by dragging the folder icons or move appointments around in a calendar app.

This can be done by using the `pyautogui.dragTo()` and `pyautogui.drag()` functions. `dragTo()` and `drag()` are quite similar to `moveTo()` and `drag()`, and also take an optional keyword argument `duration`. 

```python
import pyautogui, time
time.sleep(5)
pyautogui.click()    # Click to make the window active.
distance = 500
change = 20
while distance > 0:
    pyautogui.drag(distance, 0, duration=0.1)   # Move right.
    distance = distance - change
    pyautogui.drag(0, distance, duration=0.1)   # Move down.
    pyautogui.drag(-distance, 0, duration=0.1)  # Move left.
    distance = distance - change
    pyautogui.drag(0, -distance, duration=0.1)  # Move up.
```

We can run the code block above to use python to draw a square spiral in a paint program.

This is the result:

[[./images/pinta.png]]

*Note*: PyAutoGUI may not work with certain programes like antivirus software, to prevent viruses from disabling the software, or video games which uses a different method of receiving mouse and keyboard input.
#### Scrolling the Mouse

We can also use the `pyautogui.scroll()` function that takes an integer argument for how many units we want to scroll the mouse up or down. The size unit is different for each operating system and application so we may have to do a bit of experiment to find the right amount.
### Planning the mouse movement

One of the difficulties of writing a GUI Automation programe is finding the x- and y- coordinate of the spot that we'd need to move our mouse. PyAutoGUI came with a really good tool for this: `pyautogui.mouseInfo()`.

When we call this function from the shell, a small application named *MouseInfo* will be launched like this:


[[./images/mouseInfo.png]]

This useful tool can give us information about the mouse cursor current position as well as other details like color of the pixel underneath it.

We can also record this coordinate or pixel information by clicking the *Copy* or *Log* buttons. After we click these, there will be a 3 second delay between the clicking of the button and the actual copy or logging takes place, if the "3 Sec. Button" delay checkbox remains ticked.

We can also uncheck this box, move the mouse into position and press the F1 to F8 keys to copy or log the mouse position.
## Working with the screen

Our GUI Automation programs don't have to click and type blindly. PyAutoGUI has screenshot features that can create an image file based on the current contents of the screen. These functions can also return a Pillow `Image` object that can be worked with using the tools in Chapter 19.

```python
import pyautogui

image = pyautogui.screenshot()
print(type(image))
print()
print(dir(image))
```

```
: <class 'PIL.PngImagePlugin.PngImageFile'>
: 
: ['_Image__transformer', '_PngImageFile__idat', '_PngImageFile__prepare_idat', '__array_interface__', '__class__', '__copy__', '__del__', '__delattr__', '__dict__', '__dir__', '__doc__', '__enter__', '__eq__', '__exit__', '__format__', '__ge__', '__getattribute__', '__getstate__', '__gt__', '__hash__', '__init__', '__init_subclass__', '__le__', '__lt__', '__module__', '__ne__', '__new__', '__reduce__', '__reduce_ex__', '__repr__', '__setattr__', '__setstate__', '__sizeof__', '__str__', '__subclasshook__', '__weakref__', '_close_exclusive_fp_after_loading', '_copy', '_crop', '_dump', '_ensure_mutable', '_exclusive_fp', '_exif', '_expand', '_getexif', '_min_frame', '_new', '_open', '_repr_png_', '_seek_check', '_size', '_text', 'alpha_composite', 'category', 'close', 'convert', 'copy', 'crop', 'custom_mimetype', 'decoderconfig', 'decodermaxblock', 'draft', 'effect_spread', 'entropy', 'filename', 'filter', 'format', 'format_description', 'fp', 'frombytes', 'fromstring', 'get_format_mimetype', 'getbands', 'getbbox', 'getchannel', 'getcolors', 'getdata', 'getexif', 'getextrema', 'getim', 'getpalette', 'getpixel', 'getprojection', 'height', 'histogram', 'im', 'info', 'load', 'load_end', 'load_prepare', 'load_read', 'map', 'mode', 'offset', 'palette', 'paste', 'png', 'point', 'putalpha', 'putdata', 'putpalette', 'putpixel', 'pyaccess', 'quantize', 'readonly', 'remap_palette', 'resize', 'rotate', 'save', 'seek', 'show', 'size', 'split', 'tell', 'text', 'thumbnail', 'tile', 'tobitmap', 'tobytes', 'toqimage', 'toqpixmap', 'tostring', 'transform', 'transpose', 'verify', 'width']
```
### Analyzing the screenshot

How is the screenshot tool useful?

Let's say that one of the steps in our GUI automation program is to click a gray button. Before we call the `click()` method, what we can do is to take a quick screenshot and analyse the pixel where the script is about to click. If it's not the same gray as the gray button, then our program knows that something is wrong. This happens often, maybe the window moved unexpectedly, or maybe a pop-up dialog has blocked the button.

We can obtain the RGB color value of a particular pixel on the screen with the `pixel()` function like this:

```python
import pyautogui
print(pyautogui.pixel(0,0))
print(pyautogui.pixel(500,500))
```

```
: RGB(red=38, green=38, blue=38)
: RGB(red=40, green=44, blue=52)
```
There is no alpha value because screenshot images are fully opaque.

PyAutoGUI also comes wiht `pixelMatchesColor()` that will return *True* if the pixel at the given x- and y- coordinates on the screen matches the given color:

```python
import pyautogui

print(pyautogui.pixelMatchesColor(500,500, (40, 44, 51)))
print(pyautogui.pixelMatchesColor(500,500, (40, 44, 52)))
```

```
: False
: True
```
The first and second arguments are integers for the x- and y-coordinates and the thirds argument is a tuple of the three RGB values in integers.

If we use the `pixel()` and `pixelMatchesColor()` at specific coordinates x, it could be very useful. We should use the `pixel()` function first to get the RGB and then pass it to the `pixelMatchesColor()` function which should return *True*. This can be called before `click()`.

## Image Recognition

We can also use Image recognition in our GUI automation program. 

If we have previously taken a screenshot to capture the image of the Submit button in 'test.png', the `locateOnScreen()` function will return the coordinates where that image is found.

Like this:

```python
import pyautogui, os


# Cd to the directory of this script
pwd = os.path.dirname(os.path.realpath(__file__))
os.chdir(pwd)

b = pyautogui.locateOnScreen('test.png')
print(b)
```

```
: Box(left=1157, top=641, width=393, height=60)
```
The `b` variable is of `Box` object which is a named tuple that `locateOnScreen()` returns and has the x-coordinate of the left edge, the y-coordinate of the top edge as well as the width and height of the box.

If the image cannot be found, `locateOnScreen()` returns *None*. 

The tricky thing about this is that the image provided has to *exactly match* what's on the screen. Even if a single pixel is off, the `locateOnScreen()` would raise the `ImageNotFoundException` exception. For example, if we have recently changed the scaling in the display settings of our OS, we'd need to take the screenshot again.

If the image can be found on more than one places on the screen, the `locateAllOnScreen()` can return a *Generator* object which is a list object.

### Clicking in the area

The `locateOnScreen()` function returns a box value, how the hell do we click it?

The good thing is that if we pass a box object to the `pyautogui.click()` function which would click in the *center* of the area.

As a shortcut, we can also pass the actual iamge filename directly to the `click()` function. For example, I took a screen shot of the heading 'Image Recognition' and wrote the following script. Look what Python did!

```python
import pyautogui, os


# Cd to the directory of this script
pwd = os.path.dirname(os.path.realpath(__file__))
os.chdir(pwd)

pyautogui.rightClick('imagerecognitionbutton.png')
```

[[./images/locatebutton.png]]


Similarly to the `click()` function above, the `moveTo()` and `dragTo()` functions also except image file name arguments. As a good practice, we should wrap these calls in a `try-except` block incase the image cannot be found.

## Obtaining active Window

PyAutoGui also comes with the `pygetwindow` module that can be used to work with windows on the screen. This, however, only came with Windows, not macOS or Linux.

## Controlling the Keyboard

PyAutoGUI also has functions for sending virtual keypresses to our computer which enables us to fill out forms or enter text into the applications.

### Sending a string from the keyboard

The `pyautogui.write()` function can be used to send virtual keypresses to a computer. We should first send a mouse click to the text field to make sure that the window is actually active and the text-field has focus.

By default, the `write()` function will type the full string instantly. However we can also put an optional second argument to add a short pause between *each character*. The second argument can be an integer or a float value of the number of seconds to pause. This would be useful for slower applications that cannot process keystrokes fast enough to keep up with PyAutoGUI.

### Key Names

Not all keyboard keys can be represented with a single text.

In PyAutoGUI, these keys are represented by short strings instead. For example, `'esc'` for Escape key and `'enter'` for ENTER.

Instead of a single string argument, we can also pass a *list* to `write()` like this:

```python
pyautogui.write(['a', 'b', 'left', 'left', 'X', 'Y'])
```

The above call presses the A key, then the B key then left arrow twice and finally the x and y keys. The end product would be 'XYab' because click the left arrow key moves the keyboard cursor.

The special keys can be examined using this:

```python
import pyautogui

print(pyautogui.KEYBOARD_KEYS)
```

```
: ['\t', '\n', '\r', ' ', '!', '"', '#', '$', '%', '&', "'", '(', ')', '*', '+', ',', '-', '.', '/', '0', '1', '2', '3', '4', '5', '6', '7', '8', '9', ':', ';', '<', '=', '>', '?', '@', '[', '\\', ']', '^', '_', '`', 'a', 'b', 'c', 'd', 'e', 'f', 'g', 'h', 'i', 'j', 'k', 'l', 'm', 'n', 'o', 'p', 'q', 'r', 's', 't', 'u', 'v', 'w', 'x', 'y', 'z', '{', '|', '}', '`', 'accept', 'add', 'alt', 'altleft', 'altright', 'apps', 'backspace', 'browserback', 'browserfavorites', 'browserforward', 'browserhome', 'browserrefresh', 'browsersearch', 'browserstop', 'capslock', 'clear', 'convert', 'ctrl', 'ctrlleft', 'ctrlright', 'decimal', 'del', 'delete', 'divide', 'down', 'end', 'enter', 'esc', 'escape', 'execute', 'f1', 'f10', 'f11', 'f12', 'f13', 'f14', 'f15', 'f16', 'f17', 'f18', 'f19', 'f2', 'f20', 'f21', 'f22', 'f23', 'f24', 'f3', 'f4', 'f5', 'f6', 'f7', 'f8', 'f9', 'final', 'fn', 'hanguel', 'hangul', 'hanja', 'help', 'home', 'insert', 'junja', 'kana', 'kanji', 'launchapp1', 'launchapp2', 'launchmail', 'launchmediaselect', 'left', 'modechange', 'multiply', 'nexttrack', 'nonconvert', 'num0', 'num1', 'num2', 'num3', 'num4', 'num5', 'num6', 'num7', 'num8', 'num9', 'numlock', 'pagedown', 'pageup', 'pause', 'pgdn', 'pgup', 'playpause', 'prevtrack', 'print', 'printscreen', 'prntscrn', 'prtsc', 'prtscr', 'return', 'right', 'scrolllock', 'select', 'separator', 'shift', 'shiftleft', 'shiftright', 'sleep', 'space', 'stop', 'subtract', 'tab', 'up', 'volumedown', 'volumemute', 'volumeup', 'win', 'winleft', 'winright', 'yen', 'command', 'option', 'optionleft', 'optionright']
```

### Pressing and Releasing the Keyboard

Much like the `mouseDown()` and `mouseUp()` functions, `pyautogui.keyDown()` and `pyautogui.keyUp()` can be used to send virtual keypresses and releases to the computer.

The `pyautogui.press()` function can also be used for things that need a single-key command.

The `keyDown()` and `keyUp()` functions can also be used for *Hotkey Combinations* to invoke certain application function.

for example, this would do a copy:
```python
pyautogui.keyDown('ctrl')
pyautogui.keyDown('c')
pyautogui.keyUp('c')
pyautogui.keyUp('ctrl')
```

..however that look kinda complicated. Instead we can actually use the `pyautogui.hotkey()` function which takes multiple keyboard key string arguments, presses them in order and release them in reverse order.

Here's how to do it:
```python
pyautogui.hotkey('ctrl', 'c')
```

## Tips and Tricks

Although GUI automation scripts are a great way to automate applications, writing up the scripts can be pretty finnicky. If a window is in the wrong place or some pop-up appears unexpectedly, our script could be clicking on the wrong thing on the screen.

Here are some tips for writing and setting up a GUI Automation script:

- Use the *same screen resolution* every time we run the script.
- The application window that our script clicks should be maximized so that the buttons and menus are in the same place everytime we run the script.
- Add *generous pauses* while waiting for contents to load.
- Use `locateOnScreen()` to find buttons and menus to click rather than relying XY coordinates. We need to handle these right, if our script can't find the thing it needs to click, stop the program rather than letting blindly  click.
- Use getWindowsWithTitle() to ensure that the application window you think your script is clicking on exists, and use the activate() method to put that window in the foreground. (Windows only)
- Use the `logging` module to keep a log file of what our script has done. This makes it easier to pick up from the middle of an execution after we have had to stop the script.
- *Add as many checks* as we can to the script. We need to be creative and think about how it can possibly fail.
- *Supervise* the script the first times it runs to ensure that it's working properly.


