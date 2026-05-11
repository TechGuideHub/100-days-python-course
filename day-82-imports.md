# Day 82: Imports

**Focus:** Reusing code with imports  
**You will practice:** `import module`, `from module import name`, `import as alias`, standard library imports, import order, avoiding name collisions, spotting circular import problems, and avoiding `from module import *`  
**Estimated time:** 45-60 minutes

## Today's Goal

Today you will learn how Python programs borrow code from other files.

That borrowed code might come from:

- a standard library module that comes with Python
- another file you wrote
- a package installed later in a project

The tool for all of those is `import`.

By the end of today, you should be able to:

- import a whole module with `import module`
- use a value or function through the module name
- import one name with `from module import name`
- use `as` to create a short alias
- recognize imports from the Python standard library
- keep imports in a clear order
- avoid file names and variable names that collide with imports
- understand the warning signs of circular imports
- explain why `from module import *` is usually a bad habit
- prepare for Day 83, where you will use more of the standard library

Imports are not just a shortcut.

They are how larger programs stay organized.

## The Big Idea

Python already includes many useful modules.

A module is usually just a Python file with code in it.

When you import a module, you make its names available to your program.

Here is a small standard library import:

```python
import math

radius = 5
area = math.pi * radius ** 2

print(round(area, 2))
```

You should see:

```text
78.54
```

The line:

```python
import math
```

tells Python:

```text
Find the math module and let me use it in this file.
```

After that, you use names from the module with dot notation:

```text
math.pi
math.sqrt(25)
math.ceil(4.2)
```

The module name stays visible.

That is a good thing. When you see `math.pi`, you know exactly where `pi` came from.

You can also import one name directly:

```python
from math import sqrt

print(sqrt(81))
```

You should see:

```text
9.0
```

This line:

```python
from math import sqrt
```

tells Python:

```text
From the math module, bring the name sqrt into this file.
```

Now you can write `sqrt(81)` instead of `math.sqrt(81)`.

Both styles are useful.

This style keeps the module name:

```python
import math

print(math.sqrt(81))
```

This style brings in one specific name:

```python
from math import sqrt

print(sqrt(81))
```

For beginners, `import module` is often the clearest choice because it shows where each borrowed name came from.

## The Mental Model

Think of each Python file as having its own workspace of names.

Before an import, this file knows about only its own variables, functions, and built-in Python names.

After an import, it also knows about the imported module or imported name.

```text
your file
    |
    | import math
    v
your file can use math.sqrt, math.pi, math.floor, and more
```

The dot means:

```text
Look inside this module for this name.
```

For example:

```python
import math

number = 49

print(math.sqrt(number))
print(math.floor(7.9))
print(math.ceil(7.1))
```

You should see:

```text
7.0
7
8
```

The module keeps its names grouped together.

That grouping prevents confusion.

Compare these two lines:

```python
import math
from math import sqrt
```

With `import math`, you write:

```text
math.sqrt(36)
```

With `from math import sqrt`, you write:

```text
sqrt(36)
```

The second version is shorter, but the first version is often easier to read in a longer file.

### Aliases

Sometimes a module name is long, or there is a common short nickname.

Python lets you use `as` to make an alias.

```python
import statistics as stats

scores = [8, 10, 9, 10]

print(stats.mean(scores))
print(stats.median(scores))
```

You should see:

```text
9.25
9.5
```

The module is still `statistics`.

Inside this file, you are choosing to call it `stats`.

Use aliases when they make the code easier to read.

Do not use aliases just to make every name tiny.

This is clear:

```python
import statistics as stats
```

This is harder to read:

```python
import statistics as s
```

A short name is only helpful if the reader can still guess what it means.

### Import Order

Put imports near the top of the file.

A common order is:

```text
1. Standard library imports
2. Third-party package imports
3. Local project imports
```

For now, you mainly need the first and third groups.

Example:

```text
import random
import statistics as stats
from pathlib import Path

import messages
import report_tools
```

The blank line separates built-in Python modules from your own files.

This makes the file easier to scan.

You do not need to obsess over import order in tiny practice files.

But learning the habit early helps when your programs grow.

### Circular Import Warning

A circular import happens when two files try to import each other.

For example:

```text
helpers.py imports reports.py
reports.py imports helpers.py
```

Python may get stuck halfway through loading one file while the other file is asking for it.

That can lead to confusing import errors.

If you see this pattern, pause:

```text
file A imports file B
file B imports file A
```

Usually the fix is to move the shared code into a third file.

```text
formatters.py
helpers.py imports formatters.py
reports.py imports formatters.py
```

Another good fix is to pass values into functions instead of making files reach back and forth for each other.

You do not need to master circular imports today.

Just learn to recognize the smell: two files depending on each other at the top level.

## Try It Yourself

Create a folder named:

```text
day-82
```

You will make a tiny program with three files.

### Step 1: Create A Local Module

Create this file:

```text
day-82/messages.py
```

Add this code:

```python
def make_welcome(name):
    return f"Welcome, {name}!"


def make_goodbye(name):
    return f"See you next time, {name}."
```

This file does not ask for input.

It does not print anything.

It stores reusable functions.

That makes it a good module.

### Step 2: Import The Whole Module

Create this file:

```text
day-82/main.py
```

Add this code:

```python
import messages

print(messages.make_welcome("Mina"))
print(messages.make_goodbye("Mina"))
```

Run `day-82/main.py`.

You should see:

```text
Welcome, Mina!
See you next time, Mina.
```

Notice the shape:

```text
messages.make_welcome("Mina")
```

That means:

```text
Go to the messages module and use make_welcome.
```

### Step 3: Import One Name

Replace `day-82/main.py` with this:

```python
from messages import make_welcome

print(make_welcome("Mina"))
```

Run it again.

You should see:

```text
Welcome, Mina!
```

Now the function name is available directly.

This is shorter, but it gives less context when you read the line later.

Use this style when you only need one or two names and the meaning is still clear.

### Step 4: Add A Standard Library Import

Create this file:

```text
day-82/report_tools.py
```

Add this code:

```python
import statistics as stats


def average_score(scores):
    return round(stats.mean(scores), 1)
```

The `statistics` module comes with Python.

You did not write it.

You did not install it.

It is part of the standard library.

### Step 5: Import Your Own Module And A Standard Library Module

Replace `day-82/main.py` with this:

```python
import random

import messages
import report_tools

names = ["Mina", "Sam", "Iris"]
scores = [8, 10, 10]

random.seed(2)
student = random.choice(names)

print(messages.make_welcome(student))
print("Average:", report_tools.average_score(scores))
```

Run it.

You should see:

```text
Welcome, Mina!
Average: 9.3
```

This file has two import groups:

```python
import random
```

That is a standard library import.

```text
import messages
import report_tools
```

Those are local imports because they come from files you wrote in `day-82`.

## Common Mistake

A common beginner mistake is naming your own file after a standard library module.

For example, avoid file names like:

```text
random.py
math.py
json.py
statistics.py
datetime.py
```

If you create a file named `random.py`, then write:

```python
import random
```

Python may import your file instead of the standard library's `random` module.

That is confusing because the import line looks correct.

Use names that describe your actual program instead:

```text
random_practice.py
score_tools.py
profile_data.py
date_report.py
```

Another name collision can happen with variables.

This version is clear:

```python
import math

bonus_points = 10

print(math.sqrt(25))
print(bonus_points)
```

You should see:

```text
5.0
10
```

Avoid reusing an imported module name as a variable name.

For example, if you import `math`, do not later create a variable also named `math`.

The variable would cover up the module name in that file.

Good names save you from strange bugs.

## Debug It

You are given two files.

First file:

```text
day-82/formatters.py
```

```python
def make_title(text):
    return text.strip().title()
```

Second file:

```text
day-82/main.py
```

```text
from formatter import make_title

print(make_title(" weekly report "))
```

The program fails because the import name does not match the file name.

The file is named:

```text
formatters.py
```

But the import asks for:

```text
formatter
```

Python import names must match the module file name without the `.py` ending.

Fix `day-82/main.py` like this:

```python
from formatters import make_title

print(make_title(" weekly report "))
```

You should see:

```text
Weekly Report
```

When an import fails, check these things first:

- Is the file name spelled the same way as the import?
- Is the file in the folder Python is running from?
- Did you accidentally add `.py` in the import line?
- Did you name your file after a standard library module?
- Are two files importing each other?

Import errors often look bigger than they are.

Start with the name.

## Read the Docs

The Python documentation has a page for each standard library module.

For today, look up the documentation for:

```text
math
random
statistics
pathlib
```

Do not try to memorize every function.

Practice reading just enough to answer small questions:

- What does this module help with?
- What function name looks useful?
- What arguments does the function need?
- What kind of value does it return?

Try this small documentation scavenger hunt with the `math` module:

```python
import math

print(math.ceil(4.2))
print(math.floor(4.8))
print(math.factorial(5))
```

You should see:

```text
5
4
120
```

Now ask:

```text
What does ceil mean?
What does floor mean?
What does factorial mean?
```

The documentation is not a novel.

Use it like a shelf of tools.

Find the tool you need, read the shape, try a small example, then return to your program.

## Mini Challenge

Create this file:

```text
day-82/password_hint.py
```

Write a small password hint generator using two standard library modules:

```python
import random
import string

random.seed(12)

letters = string.ascii_lowercase
digits = string.digits

first_letter = random.choice(letters)
second_letter = random.choice(letters)
number = random.choice(digits)

hint = first_letter + second_letter + number

print("Password hint:", hint)
```

Run it.

You should see:

```text
Password hint: pi8
```

This program imports:

- `random` for choosing values
- `string` for ready-made strings of letters and digits

The seed is there so your result matches the lesson.

In a real password program, you would not use a fixed seed like this.

For practice, it makes the example easier to check.

Now change the program:

- choose four letters instead of two
- choose two digits instead of one
- print the final hint

Keep the imports at the top.

## Real-World Use

Imports are everywhere in real Python projects.

A small app might import:

- `json` to load settings
- `pathlib` to work with file paths
- `datetime` to handle dates
- local modules for business rules
- local modules for formatting output

Here is a short settings example:

```python
import json
from pathlib import Path

settings = {
    "theme": "light",
    "font_size": 14,
    "show_tips": True
}

path = Path("day-82/settings.json")
path.write_text(json.dumps(settings, indent=4))

loaded = json.loads(path.read_text())

print(loaded["theme"])
print(loaded["font_size"])
```

You should see:

```text
light
14
```

That one short program uses two standard library modules:

- `json` handles structured data
- `pathlib` handles the file path

You could write all of that behavior yourself, but you should not.

Good Python programmers reuse reliable tools.

Imports are how they reach those tools.

## Recap

Today you learned that imports let one Python file use code from another place.

The main forms are:

```text
import math
```

Use names through the module:

```text
math.sqrt(25)
```

Import one name:

```text
from math import sqrt
```

Use it directly:

```text
sqrt(25)
```

Create an alias:

```text
import statistics as stats
```

Use the alias:

```text
stats.mean([8, 10, 9])
```

You also learned these habits:

- keep imports near the top of the file
- group standard library imports before local imports
- avoid naming your files after modules like `random`, `math`, or `json`
- avoid reusing imported module names as variables
- be careful when two files import each other
- avoid `from module import *` in normal program files

About that last point:

```text
from math import *
```

This imports many names at once.

It may feel convenient, but it hides where names came from.

It can also overwrite names you already had.

In beginner projects, prefer one of these:

```text
import math
```

or:

```text
from math import sqrt
```

Being a little more specific makes your code easier to debug.

## Lesson Checklist

Before moving on, make sure you can:

- explain what a module is
- import a standard library module
- use a function through a module name
- import one function from a module
- use `as` to create a readable alias
- create a small local module
- import your local module into `main.py`
- keep standard library imports above local imports
- avoid common module name collisions
- explain why circular imports are risky
- explain why `from module import *` is usually avoided

## Exercises

### Exercise 1: Math Tools

Create this file:

```text
day-82/math_practice.py
```

Write a program that:

- imports `math`
- stores a number in a variable
- prints the square root of the number
- prints the number rounded up with `math.ceil()`
- prints the number rounded down with `math.floor()`

Starter code:

```python
import math

number = 42.7

print(math.sqrt(number))
print(math.ceil(number))
print(math.floor(number))
```

### Exercise 2: Choose A Lunch

Create this file:

```text
day-82/lunch_picker.py
```

Write a program that:

- imports `random`
- stores at least four lunch options in a list
- uses `random.choice()` to pick one
- prints the choice

Starter code:

```python
import random

lunches = ["rice bowl", "sandwich", "soup", "noodles"]

random.seed(5)
choice = random.choice(lunches)

print("Lunch:", choice)
```

### Exercise 3: Build A Formatter Module

Create this file:

```text
day-82/name_tools.py
```

Add this code:

```python
def clean_name(name):
    return name.strip().title()
```

Then create this file:

```text
day-82/use_name_tools.py
```

Add this code:

```python
import name_tools

raw_name = "  mina patel "
cleaned = name_tools.clean_name(raw_name)

print(cleaned)
```

You should see:

```text
Mina Patel
```

### Exercise 4: Try A Direct Import

Change `day-82/use_name_tools.py` to use `from name_tools import clean_name`.

Your file should look like this:

```python
from name_tools import clean_name

raw_name = "  mina patel "
cleaned = clean_name(raw_name)

print(cleaned)
```

Run it and make sure the result is the same.

### Exercise 5: Spot The Import Problem

Read this file list:

```text
day-82/random.py
day-82/main.py
```

Then read this import:

```text
import random
```

What problem might happen?

Answer in one sentence.

Then rename the practice file in your own project to something clearer, such as:

```text
day-82/random_practice.py
```

### Exercise 6: Avoid The Star

Read this import:

```text
from math import *
```

Rewrite it in two safer ways:

```text
import math
```

and:

```text
from math import sqrt
```

Then write one sentence explaining why the star import is harder to debug.

## Tiny Win

You can now split code across files and bring it back together with imports.

That is one of the first steps from writing single-file scripts toward writing real projects.

Even better, you can now look at the top of a Python file and understand some of its dependencies before reading the rest.

That is a serious reading skill.

## Tomorrow

Tomorrow you will continue with the standard library.

You have already used modules like `math`, `random`, `statistics`, `json`, and `pathlib`.

Day 83 will focus on choosing useful standard library tools and reading their documentation without feeling like you need to memorize everything.
