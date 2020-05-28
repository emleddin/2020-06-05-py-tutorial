---
title: "Python Basics"
teaching: 35
exercises: 25
questions:
- "What are Python packages?"
- "How do I use variables?"
- "What are comments and docstrings?"
- "What are if statements, for loops, and counters?"
- "How do I write a function in Python?"
objectives:
- "Create if statements and for loops."
- "Write a Python function."
- "Describe common formatting rules for Python."
- "Import Python packages."
keypoints:
- "Use `import` to load in Python packages."
- "**Python starts indexing at 0 (zero).**"
- "Comments are evoked through `#`, and docstrings are evoked through `\"\"\" \"\"\"`."
- "Indentation levels are very important for Python, and 4 spaces should be used
for indents."
- "The `\\` is a line continuation mark."
---

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

## For Loops and Counters
FIXME

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
