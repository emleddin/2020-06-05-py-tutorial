---
title: "Python Basics"
teaching: 35
exercises: 25
questions:
- "What are Python packages?"
- "What are comments and docstrings?"
- "How do I use variables?"
- "What are if statements, for loops, and counters?"
- "How do I write a function in Python?"
objectives:
- "Create if statements and for loops."
- "Write a Python function."
- "Describe common formatting rules for Python."
- "Import Python packages."
keypoints:
- "Python can be run interactively, through a script, or in a notebook form."
- "Use `import` to load in Python packages."
- "Comments are evoked through `#`, and docstrings are evoked through `\"\"\" \"\"\"`."
- "**Python starts indexing at 0 (zero).**"
- "Indentation levels are very important for Python, and 4 spaces should be used
for indents. Indent levels are critical for `if` statements and `for` loops."
- "`if` statements and `for` loops should each end the opening line with a `:`
(colon)."
- "It is a common convention to use non-plural/plural pairs for `for` loops."
- "Updating a variable with addition can be achieved through `+=`."
- "The `\\` is a line continuation mark, as well as the escape character."
- "The phrase keyword arguments (for functions) is sometimes shorted to
`**kwargs`."
- "Exit command-line Python with `quit()` or `exit()`, including the parentheses."
---

**Highlights**
* TOC
{:toc}

## Running Python Code
Python code can be run using a Python prompt (likely evoked through `python3`,
but that might be different depending on what versions are installed on your
device).
If you're running a Jupyter Notebook or a Google CoLab Notebook, code
cells will run in the default Python shell (and can be changed to specific
versions).

```
user@host$ python3
Python 3.7.3 (default, Mar 27 2019, 16:54:48)
[Clang 4.0.1 (tags/RELEASE_401/final)] :: Anaconda, Inc. on darwin
Type "help", "copyright", "credits" or "license" for more information.
>>>
```
{: .language-bash}

To run a Python script, you would use that specific prompt command with the
name of the script you are trying to run.

```
user@host$ python3 my_cool_script.py
```
{: .language-bash}

If you're not sure what the Python you're using, but you've installed Anaconda3,
go to `/anaconda3/bin` and see which executables are there.
If you're having issues running the code provided, but know you have Python3
installed, run `which python` to see what version is being sourced.
It is not recommended that you change your default Python installation,
because this can have serious repercussions for your operating system.
Instead, save it to an alias that you call when you need to run Python3.

## Python Packages and the `import` Command
Python has some basic commands (referred to lovingly as "base Python"), but
those are often not enough for what you want to to with Python.
Packages (or modules or libraries) are bundles of code that are designed for
a specific purpose.
They're like a package in a mail sense--if you open a box you got in the mail,
the box was was way to wrap various objects into a neat little unit for shipping.
For instance, `matplotlib` is a library built for data visualization.
Using packages is similar to how `module load` works on an HPC cluster.
When you need to use a package for a specific purpose, you need to
`import` it into Python.

> ## Additional Resources for Getting Started with Python
>
> * [MolSSI Python Scripting for Computational Molecular Science](http://education.molssi.org/python_scripting_cms/)
> * [MolSSI Python for Data Analysis](https://education.molssi.org/python-data-analysis/)
> * [Python Crash Course Cheat Sheets](https://ehmatthes.github.io/pcc/cheatsheets/README.html)
> * [Software Carpentry Programming with Python](http://swcarpentry.github.io/python-novice-inflammation)
> * [Software Carpentry Plotting and Programming in Python](http://swcarpentry.github.io/python-novice-gapminder)
>
{: .callout}

## Comments and Docstrings

If you're familiar with writing code, hopefully the importance of adding
comments has been stressed to you.
If this is your first time dabbling in coding, comments are arguably more
important than the code itself.
Comments provide information and reasoning for the actual code itself.
They are offset from the rest of the code with a specific symbol (or symbols).
In Python, a comment is made with the `#` (pound/hashtag/octothrope) symbol.

```
# This is my first comment
```
{: .language-python}

The nice thing about Python is that you can stack those symbols into your own
personal commentary style, or use the `#` symbol to create fancy comment blocks.

```
## I comment almost everything with 2 # symbols. It makes it clear to me that
## it's a comment.
## Note: the # symbol is only for single-line comments, so each line needs
## its own mark!!!!

#-----------------------------------------#
#      Insert pretty comment block        #
#-----------------------------------------#
```
{: .language-python}

Multiline commenting is possible in Python, but through something known as a
docstring.
They're called docstrings because they are strings used for documentation
purposes.
Most projects (open and not) require coders to write docstrings for their
functions, though they may have their own formatting for those docstrings.
A docstring is generated through either three single or double quotes that both
begin and end the docstring.

~~~
"""
This is a docstring
"""

'''
This is also docstring
'''

"""I can even do them in-line, but I don't know what I'd want to."""

'''The only rules are that you be consistent and escape characters other times
that you\'d want them.'''
~~~
{: .language-python}

The last segment of the above example talks about using an escape character.
In Python, the escape character is `\`.

## Data Types

There are a number of different data types in Python, but a few robustly
used types.
This is by no means an exhaustive list, as new data types
[can be created](https://docs.python.org/3/extending/newtypes.html).

| Data Type | Common Word | Brief explanation |
|-----------|-------------|------------------------|
| str       | string      | Strings are things like filenames or text. `x = "Thing"` |
| int       | integer     | A typical integer. `x = 1`  |
| float     | float       | Floats are real numbers. `x = 1.` and `x = 1.0` are both floats. |
| bool      | boolean     | `True` or `False` |
| dict      | dictionary  | Useful for holding data that needs to be paired, like school and abbreviation. These are known as key-value pairs.  |
| list      | list        | Similar to an array, but of undefined length. They can be changed. |
| tuple     | tuple       | Like a list, but cannot be changed. |

The `type()` command will return the type of a variable.
```
x = 5
type(x)
```
{: .language-python}

```
<class 'int'>
```
{: .output}

There are times where you need to change a data type, like needing a
number input option to be read as an integer.
This is done with the "Data Type" specified above.
You can either resave the value of that variable as the new type, or use
it as part of a different command for a temporary change.

```
x = "5"
x = int(x)

y = 1
y = float(y)
```
{: .language-python}

> ## Trouble Spot: Integers and Floats
>
> One easy way to get tripped up in Python is to use an integer when a float
> is needed and vice versa.
> If you input `1.`, then you need a float input, and Python will complain
> about receiving an integer input.
>
> ~~~
> >>> x = 5.
> >>> for i in range(x):
> >>>     print(i)
> Traceback (most recent call last):
>   File "<stdin>", line 1, in <module>
> TypeError: 'float' object cannot be interpreted as an integer
> ~~~
> {: .output}
>
> Now, it will render as expected by forcing `x` to be an integer for the loop.
>
> ~~~
> >>> for i in range(int(x)):
> >>>    print(i)
> 0
> 1
> 2
> 3
> 4
> ~~~
> {: .output}
{: .callout}

## Variables

Variables are your friend! They're a means to store data or information.
In Python, you typically just make a named object `=` before whatever you're
trying to store as a variable.

```
x = "Thing"

print(x)
```
{: .language-python}

```
Thing
```
{: .output}

## Print Statements and If Statements

Printing is useful for so many things in coding, from giving you the result to
sharing information at specific checkpoints in the code.

In Python, the command to print is simply `print`.
```
print("Hello world")
```
{: .language-python}

```
Hello world
```
{: .output}

> ## Python 3 Print Statements are Finicky
>
> Python changed substantially between Python 2 and Python 3.
> In Python 2, you could make print statements without parenthesis.
> In Python 3, however, this will trigger an error message.
>
> ~~~
> print x,y
> ~~~
> {: .language-python}
>
> ~~~
>    File "<stdin>", line 1
>     print x,y
>           ^
> SyntaxError: Missing parentheses in call to 'print'. Did you mean print(x,y)?
> ~~~
> {: .output}
{: .callout}

We can use an `if` statement to print things only when a specific condition is
met.
These statements are often used with booleans, meaning variables marked as
`True` or `False`.

On days that you've had your morning coffee, you are in a decent mood.
But the days that start without coffee can leave you cranky.
This can be written as an `if` statement.
Python is **very** particular about indentation levels, and by convention, and
indent should be 4 spaces.
That said, as long as you're consistent throughout, tabs can be used.
```
morning_coffee = True

if morning_coffee == True:
    print("Hello world! What a wonderful day it is!")
else:
    print("I'm not talking to you until I've had my morning coffee.")
```
{: .language-python}

```
Hello world! What a wonderful day it is!
```
{: .output}

If we reset the `morning_coffee` variable to `False`, we get a different output.
```
morning_coffee = False

if morning_coffee == True:
    print("Hello world! What a wonderful day it is!")
else:
    print("I'm not talking to you until I've had my morning coffee.")
```
{: .language-python}

```
I'm not talking to you until I've had my morning coffee.
```
{: .output}

We aren't limited to booleans, which makes our `if` criteria more complex.
Grades can be assigned using an `if` statement.
```
final_grade_percent = 87.4

if final_grade_percent >90. and <=100.:
    final_letter_grade = 'A'
elif final_grade_percent >80. and <=90.:
    final_letter_grade = 'B'
elif final_grade_percent >70. and <=80.:
    final_letter_grade = 'C'
elif final_grade_percent >60. and <=70.:
    final_letter_grade = 'D'    
else:
    final_letter_grade = 'F'

print("The final percent grade of {} yields {} as a letter\
 grade.".format{final_grade_percent,final_letter_grade})
```
{: .language-python}

```
The final percent grade of 87.4 yields B as a letter grade.
```
{: .output}

Some notes about what happened there:
- Integers differ from floats with the extra `.`
- The `\` character is a line continuation mark. It is a good practice to keep
lines under 80 characters.
- Python **will** complain if the `:` (colon) is not there.

`elif` and `else` are not required for every `if statement`.
Say we had a Python script that wrote to the file `file123.txt`.
Users that use a file named `file123.txt` as an input, will overwrite their
input file with the script's output, and that could be frustrating.
So, we may want to give the output file a different name, but only when the
input name matches what the output name would otherwise be.

```
# Pretend that output_file = "file123.txt" is up here
# somewhere where we don't see it and aren't planning on editing it

input_file = "some_input.txt"

if input_file == "file123.txt":
    output_file = "output_file123.txt"

print(output_file)
```
{: .language-python}

```
output_file = file123.txt
```
{: .output}

Another important word is `continue`.
`continue` is great if you know when you *don't* want something to happen in
one specific case, but you do need it for every other case.

```
## Give a mouse a cookie, but only if they haven't already have a cookie

if cookie == True:
    continue
else:
    cookie == True
```
{: .language-python}

Similarly, if you need to exit out of the statements and move on in the code
when something specific happens (like receiving an input that would crash a
program), you can use `break`.

## For Loops and Counters

`for` loops control iterations.
In Python, `for` loops start use indents to keep the information within the
loop contained.
Typically, these look like `for x in y:`.
Again, Python **will** complain if there isn't a colon.
```
coin_list = ["quarter", "dime", "nickel", "penny", "half-dollar",
    "golden dollar"]

for coin in coin_list:
    print(coin)
```
{: .language-python}

```
quarter
dime
nickel
penny
half-dollar
golden dollar
```
{: .output}

In the above example, the `for` loop was initiated with `for coin in coin_list:`.
However, the use of `coin` is irrelevant--it was just a placeholder variable.
Many people like to use `i` for their `for` loop indexing, and it could have
just as easily been `for i in coin_list`.
However, in that case, swapping out `coin` for `i` must also be done within
the `for` loop itself.
Otherwise, you'll get a `name is not defined` error.

```
>>> coin_list = ["quarter", "dime", "nickel", "penny", "half-dollar",
...     "golden dollar"]
>>>
>>> for i in coin_list:
...     print(coin)
...
Traceback (most recent call last):
  File "<stdin>", line 2, in <module>
NameError: name 'coin' is not defined
```
{: .output}

The other common initiation of a `for` loop in Python is with the `range()`
command.

```
for x in range(5):
    print(x)
```
{: .language-python}

```
0
1
2
3
4
```
{: .output}

Sometimes it is necessary to keep a count within code, or otherwise update
a variable through addition or substration.
After setting a variable to an initial value, you can update it with `+=`
or `-=`.
This means that  `x += 1` can take the place of `x = x + 1` (spaces optional).

```
y = 0
for x in range(5):
    y += 1
print(y)
```
{: .language-python}

```
5
```
{: .output}

> ## Combining Ifs and Fors
>
> Write a for loop that reads in a list of 5 items and does not print anything
> for one of them.
>
> > ## One Solution for Combining Ifs and Fors
> >
> > There are many, many ways to write code. This is just one solution.
> >
> > ~~~
> > MD_programs = ['AMBER', 'CHARMM', 'GROMACS', 'LAMMPS', 'TINKER']
> >
> > for program in MD_programs:
> >     if program == "TINKER":
> >         continue
> >     else:
> >         print("You don't have to convert from {} format to XYZ. Yet.".format(program))
> > ~~~
> > {: .language-python}
> >
> > ~~~
> > You don't have to convert from AMBER format to XYZ. Yet.
> > You don't have to convert from CHARMM format to XYZ. Yet.
> > You don't have to convert from GROMACS format to XYZ. Yet.
> > You don't have to convert from LAMMPS format to XYZ. Yet.
> > ~~~
> > {: .output}
> {: .solution}
{: .challenge}

## Functions

`def` stands for definition. Callable functions are created with the `def`
command.
Whatever you name your variable in the function call does not have to be what
was in the definition line.

We can turn the earlier grades `if` statement into a function.

```
def assign_grade(final_grade_percent):
    if final_grade_percent >90. and <=100.:
        final_letter_grade = 'A'
    elif final_grade_percent >80. and <=90.:
        final_letter_grade = 'B'
    elif final_grade_percent >70. and <=80.:
        final_letter_grade = 'C'
    elif final_grade_percent >60. and <=70.:
        final_letter_grade = 'D'    
    else:
        final_letter_grade = 'F'
    return final_letter_grade
```
{: .language-python}

To later use this function, we would assign a value to `final_grade_percent`
and call
```
final_letter_grade = assign_grade(final_grade_percent)
```
{: .language-python}

> ## Pizza Cost
>
> Write a function that determines the cost of a pizza based off of the cost
> of individual toppings.
>
> > ## One Solution for Pizza Cost
> >
> > There are many, many ways to write code. This is just one solution.
> >
> > ~~~
> > plain_pizza = 10.
> >
> > toppings = ['pineapple', 'pepperoni', 'anchovies', 'olives']
> >
> > def pizza_price(plain_pizza, toppings):
> >     for topping in toppings:
> >         if topping == 'pepperoni':
> >             plain_pizza += 2.
> >         else:
> >             plain_pizza += 1.
> >     return plain_pizza
> >
> > plain_pizza = pizza_price(plain_pizza, toppings)
> >
> > print("The pizza costs ${:.2f}".format(plain_pizza))
> > ~~~
> > {: .language-python}
> {: .solution}
{: .challenge}

## Importing and Using `numpy`

One of the most common packags is `numpy`.
Python is really nice in that you can give these modules a "nickname" so it's
easier to refer to them. You'll often see `np` as a "nickname" for `numpy`.
Once it is loaded in, the functions that it contains are accessible using the
nickname (or the module name, if simply `import numpy` is used).

```
import numpy as np
x = 35
y = 493545435
thing = np.divide(x, y)
print("thing:", thing)
```
{: .language-python}

```
thing: 7.091545685150548e-08
```
{: .output}

The above code uses the `numpy` version of division, which may be faster or
give different significance depending on the operation being performed.

Division is something included in "base" Python (Python without any
imported modules). Because we've already defined `x` and `y` in a previous cell,
we can continue.
```
new_thing = x/ y
print(new_thing)
```
{: .language-python}

```
7.091545685150548e-08
```
{: .output}

In this case, the numbers are the same.

> ## **Python starts indexing at 0 (zero).**
>
> When working with arrays or lists, the very first position is not 1,
> but 0.
> This is arguably the **most** important thing to know about Python.
>
> ~~~
> import numpy as np
> x_list = np.arange(0,10,1)
> print(x_list)
> for x in x_list:
>     print(f"I am number {x} of {len(x_list)}.")
> ~~~
> {: .language-python}
> ~~~
> [ 0 1 2 3 4 5 6 7 8 9]
> I am number 0 of 10.
> I am number 1 of 10.
> I am number 2 of 10.
> I am number 3 of 10.
> I am number 4 of 10.
> I am number 5 of 10.
> I am number 6 of 10.
> I am number 7 of 10.
> I am number 8 of 10.
> I am number 9 of 10.
> ~~~
> {: .output}
{: .callout}

{% include links.md %}
