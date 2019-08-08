---
title:  "Hello, World!"
date:   2019-08-07 12:00:00
categories: tutorials
tags: [beginner, python]
series: "Python for the Math Major"
---

Today you'll learn how to use the Python interpreter as a calculator and all the fundamental topics that we'll need to move forward.

<!-- end-excerpt -->

Hey folks and welcome back to "Python for the Math Major".
We're picking up right where we left off in the introduction, so I'll assume you have the latest version of Python 3 installed.
Let's jump right into the code.

## Getting into the Interpreter

Open a command prompt/terminal on your machine of choice and enter the text in the code block below. We'll use these blocks to display code through the rest of the series.

On Windows:
```
> python
```

On Linux:
```
$ python3.7
```

Then, wait for

```Python
>>>
```

to appear.
This should only take a few seconds at most.

You're now in the Python Interpreter and we can start coding.
To enter code into the Interpreter we'll type the code after the `>>>`.
The result of the code will display beneath it on a clean line and then the `>>>` prompt will reappear, telling us that the console is ready to receive more code.

## Hello Math

Most tutorials start with a "Hello, World" example -- thus the title of this post -- but that's not very _mathy_ so we'll do the oldest math problem in the book.

```Python
>>> 2+2
4
>>>
```

As you can see, the Python interpreter can be used as a calculator.
A difficult to use, sometimes complicated calculator, but a calculator nonetheless.

Python can handle more complex expressions such as

```python
>>> 30 + 15 * (17 - 35/5)
180.0
>>>
```

Here we can see the four basic math operations in action: `+`, `-`, `*`, `/`.

`+` and `-` are pretty self explanatory: addition and subtraction.
`*` and `/` are multiplication and division operators respectively.

Order of operations is followed by python but by using parentheses `()` we can override this behavior.
To see this in action, you can try the previous example without them and observe the result.

We can also bring exponents into the mix with the `**` operator. For example, 5 squared:

```Python
>>> 5 ** 2
25
>>>
```

## Data Types

We can now write and evaluate mathematical expressions but there are a few more math operators that might be new to you.
Before we get to them, let me bring up the concept of data types.

In mathematics we mostly deal with numbers.
All kinds of numbers.
But we differentiate between natural numbers and integers, real and imaginary numbers, even rational and irrational values.

In programming we also need to differentiate between types of data, not just numbers.
So far we have seen two data types: the _**integer**_ and the _**float**_.

We already know what integers look like.
You probably learned about them in primary school and have studied them in discrete math or number theory classes.
Examples include 2, 17, and 3435 (my favorite number).

Floats on the other hand sound new, but they aren't.
Floats are just rational numbers.
That's it.
Just a different name.

So our previous example:

```python
>>> 30 + 15 * (17 - 35/5)
180.0
>>>
```

has integer inputs, uses math operators, and has a float for an output.

There are many other data types.
We'll cover them at a later date.

### Integer Division and Modulus

Those of you that have taken some discrete math or number theory probably know that when we're working with integers alone, the normal division that we often talk about doesn't make any sense.

_**Integer Division**_, also called remainder division, gives a quotient equal to the number of times the divisor divides the dividend wholly. In Python we represent integer division with double forward slashes `//`.

_**Modulus**_ gives the remainder of an Integer Division. It is represented by the `%` character.

Let's take an example. Let's integer divide 17 by 5 and then get the remainder.

```Python
>>> 17 // 5
3
>>> 17 % 5
2
>>>
```

So we get 5 divides 17 three times with a remainder of 2.
This is powerful in many areas of programming as we'll be using integers pretty often here.

> **Note -- Print()**
>
> Thus far we've just been entering expressions and receiving results in the console.
> Moving forward try to get into the habit of using the `print()` function to send things to the console.
> I'll be using it for the remainder of the examples.


## Variables

In math, we often create variables for the purpose of... varying them.
They are used as place holders for all possible values in the domain of a function.

In programming, variables are places to store values that we'd like to access later.
All variables have a name, a data type, and a value.

Let's say we wanted to reference the number of derivatives we calculated on a homework, set it to our current score, and increment whenever we complete another problem.

```Python
>>> derivatives_calculated = 4
>>> print(derivatives_calculated)
4
>>> derivatives_calculated += 1
>>> print(derivatives_calculated)
5
```

1. We start by naming a variable `derivatives_calculated` and initializing it to `4` with the assignment operator `=`.
2. Then we display the value of `derivatives_calculated` with `print()`.
3. We increment the value using `+=` which is short hand for the clumsy `derivatives_calculated = derivatives_calculated + 1`.
4. Then we display the new value.

### Naming Variables

Naming variables is a delicate process.
Clarity is important but there are also some names to be avoided.

You must --
- start names with a letter or underscore `_`
- use only letters, numbers, and underscores `_` for the remainder of the name
- remember that names are case sensitive

You should --
- use UPPER_CASE for constants and lower_case for everything else
- use descriptive names, not single letters
- avoid using the letters `l` and `O` as they look like the numbers `1` and `0`.

It's also important to avoid using reserved keywords.
These words are used by Python to insert logic into the code and represent common values and functions.
Because they are reserved you shouldn't name a variable after a keyword.
To see a list of reserved names use

```Python
>>> import keyword
>>> print(keyword.kwlist)
```

> **Note -- Comments**
>
> It's often useful to leave notes about your code to your future self or other developers.
> This can be done through _**Comments**_ -- sections of code that are ignored by the program.
> By inserting a hash-tag `#` into your code, you tell the system that the rest of the line is a comment.

### Lists

One of the fundamental variable types we'll work with is the list.
Lists are comparable to one dimensional matrices.
They are ordered, can contain repeated values, and are referenced by indices.

Let's create a list.

```Python
>>> list = [1, 2, 2, 3]
>>> print(list)
[1, 2, 2, 3]
>>>
```

As you can see the repetition of the value `2` is not removed.
Lists are not sets.
Order is also preserved.

We can access elements in a list using their index.
Lists in Python start with an index of 0, as they should.
So to get the third element of our list we use index 2.

```Python
>>> print(list[2])
2
>>>
```

The square brackets `[]` are called accessors.
They allow us to pass an argument to the list in order to request data from it.

We can also assign a new value to the third index in a similar fashion.

```
>>> list[2] = 7
>>> print(list)
[1, 2, 7, 3]
>>>
```

The change in value is done _in place_, meaning that a new list is not created in the process of changing a single value.

An intuitive way of thinking about lists is that they are collections of variables that are all related to each other.
You might create a grocery list which contains a series of food product names each stored in their own variable.
Rather than specifying a name to reference each food item by, you can instead have a single `grocery_list` that can be accessed using indices.

### Strings

Keeping a grocery list with only numerical data is quite difficult.
It would be nice if there were a way to store the names of food products in the list instead.

This can be achieved with the _**String**_.
A string is a series of characters in a specific order.
Something like 'cat', 'dog', "pumpkin", 'Jokulhaups1234X97'.
Strings can be represented with either single quotes `'` or double quotes `"`.

Strings are immutable in Python.
This means that once assigned they can't be changed directly.
We have to reconstruct the string if we want to change it.
This can seem counter intuitive, but the string 'cat' is treated the same way as the integer `7`.
They are independent, unchangeable objects that are only referenced.

Our previous example of a grocery list can now be represented with a list of strings like this.

```Python
>>> grocery_list = ['hamburger', 'milk', 'eggs', 'bread']
>>> print(grocery_list)
['hamburger', 'milk', 'eggs', 'bread']
```

We could now print out the list, check if an item is in the list, or remove items from the list.
But that's best left for another day.

## What's Next?

That's all for this week.
You learned your first bits of Python code: math operators, variables, and data types including lists and strings.

Next time we'll cover the building blocks of logic: conditionals and loops.
