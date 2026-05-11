# Day 81: Modules

**Focus:** Splitting Python programs into small files and importing your own code  
**You will practice:** creating modules, importing helper functions, calling code from another file, noticing when top-level code runs, and using a small `if __name__ == "__main__":` guard  
**Estimated time:** 55-70 minutes

## Today's Goal

Today you will learn how to split a Python program across more than one file.

So far, many of your programs have lived in one file. That is fine when the program is small. But as soon as a file starts doing several jobs, it becomes harder to read, test, and change.

A module gives you a clean way to move useful code into another file.

By the end of today, you should be able to:

- explain that a module is a Python file
- create a helper file with functions in it
- import your own module from another file
- call imported functions with the module name
- explain why some code runs as soon as a file is imported
- use `if __name__ == "__main__":` to keep test code from running during import
- prepare for Day 82, where you will practice different import styles

The skill for today is not about making code fancy.

It is about giving each file a clear job.

## The Big Idea

A module is a Python file that another Python file can use.

Create a folder named:

```text
day-81
```

Inside it, create this file:

```text
day-81/helpers.py
```

Code:

```python
def greet(name):
    return f"Hello, {name}."


def make_initials(first_name, last_name):
    first_initial = first_name[0].upper()
    last_initial = last_name[0].upper()
    return f"{first_initial}.{last_initial}."
```

Now create another file:

```text
day-81/main.py
```

Code:

```python
import helpers

message = helpers.greet("Mina")
initials = helpers.make_initials("Mina", "Patel")

print(message)
print(initials)
```

Run:

```text
python day-81/main.py
```

You should see:

```text
Hello, Mina.
M.P.
```

The important line is:

```python
import helpers
```

That line tells Python:

```text
Find helpers.py, run it, and let this file use the names inside it.
```

After importing, you call the functions with the module name:

```python
helpers.greet("Mina")
helpers.make_initials("Mina", "Patel")
```

The module name makes it clear where the function came from.

## The Mental Model

Think of a module as a labeled toolbox.

```text
day-81/
  helpers.py   tools live here
  main.py      the program starts here
```

`helpers.py` holds functions.

`main.py` decides what to do with those functions.

When Python sees:

```python
import helpers
```

it does a few things:

```text
1. Looks for a file named helpers.py.
2. Runs helpers.py from top to bottom.
3. Stores the result as a module object.
4. Gives main.py the name helpers.
```

That second step surprises many beginners.

Python runs the imported file from top to bottom.

Function definitions are quiet when they are created. They do not run until you call them. But normal top-level code, such as `print()`, runs during import.

Try this version.

```text
day-81/helpers.py
```

Code:

```python
print("Loading helpers")


def add_bonus(score):
    return score + 5
```

```text
day-81/main.py
```

Code:

```python
import helpers

print(helpers.add_bonus(80))
```

Run:

```text
python day-81/main.py
```

You should see:

```text
Loading helpers
85
```

The first line printed because `helpers.py` was imported.

That is useful to understand, but it is usually not what you want in a helper module. Helper modules should mostly define functions, constants, or classes. They should not usually do real work just because they were imported.

Here is the beginner-friendly fix.

```text
day-81/helpers.py
```

Code:

```python
def add_bonus(score):
    return score + 5


def demo():
    print(add_bonus(80))


if __name__ == "__main__":
    demo()
```

```text
day-81/main.py
```

Code:

```python
import helpers

print(helpers.add_bonus(90))
```

Run:

```text
python day-81/main.py
```

You should see:

```text
95
```

Now run the helper file directly:

```text
python day-81/helpers.py
```

You should see:

```text
85
```

This line is the guard:

```python
if __name__ == "__main__":
    demo()
```

For now, remember it this way:

- when a file is run directly, `__name__` is `"__main__"`
- when a file is imported, `__name__` is the module name, such as `"helpers"`
- the guard lets you keep small tests in a module without running them every time the module is imported

You do not need to use this guard everywhere today.

Use it when a helper file has demo code, test prints, or practice code at the bottom.

## Try It Yourself

Create this file:

```text
day-81/text_tools.py
```

Code:

```python
def clean_name(name):
    return name.strip().title()


def make_score_line(name, score):
    cleaned = clean_name(name)
    return f"{cleaned}: {score}/100"
```

Now create this file:

```text
day-81/main.py
```

Code:

```python
import text_tools

print(text_tools.make_score_line(" mina ", 88))
print(text_tools.make_score_line("SAM", 91))
print(text_tools.make_score_line(" iris ", 79))
```

Run:

```text
python day-81/main.py
```

You should see:

```text
Mina: 88/100
Sam: 91/100
Iris: 79/100
```

Notice the shape:

```text
text_tools.py defines helper functions
main.py imports text_tools
main.py calls text_tools.make_score_line(...)
```

That is a common pattern.

One file holds the helper logic.

Another file uses it to run the program.

## Common Mistake

A common mistake is importing a module and then calling the function without the module name.

If you write:

```python
import text_tools
```

then use the module name when you call its functions:

```python
print(text_tools.clean_name(" mina "))
```

The prefix matters.

It tells Python, "Use the `clean_name` function that lives inside `text_tools`."

Another common mistake is giving your file the same name as a Python module you may want later.

Avoid names like:

```text
random.py
math.py
json.py
csv.py
pathlib.py
```

Those names already mean something in Python.

For your own files, choose names that describe your project:

```text
text_tools.py
score_helpers.py
price_tools.py
report_builder.py
```

Clear file names make imports easier to read.

## Debug It

This program runs, but it prints more than the main file asked for.

```text
day-81/helpers.py
```

Code:

```python
print("Testing tax helper")


def add_tax(price):
    return round(price * 1.08, 2)


print(add_tax(20))
```

```text
day-81/main.py
```

Code:

```python
import helpers

print(helpers.add_tax(50))
```

Run:

```text
python day-81/main.py
```

You should see:

```text
Testing tax helper
21.6
54.0
```

Ask yourself:

```text
Which file printed the first two lines?
Why did that file run?
Which lines should only run when helpers.py is tested directly?
```

Now change `helpers.py` to this:

```python
def add_tax(price):
    return round(price * 1.08, 2)


def demo():
    print("Testing tax helper")
    print(add_tax(20))


if __name__ == "__main__":
    demo()
```

Run the main file again:

```text
python day-81/main.py
```

You should see:

```text
54.0
```

Then run the helper file directly:

```text
python day-81/helpers.py
```

You should see:

```text
Testing tax helper
21.6
```

The helper file can still test itself.

It just does not interrupt the file that imports it.

## Read the Docs

Documentation is not only something you read on a website.

Your own modules can have tiny pieces of documentation too.

Create this file:

```text
day-81/text_tools.py
```

Code:

```python
def slugify(title):
    """Return a lowercase title with spaces changed to hyphens."""
    return title.strip().lower().replace(" ", "-")
```

Now create this file:

```text
day-81/main.py
```

Code:

```python
import text_tools

print(text_tools.slugify(" My First Module "))
help(text_tools.slugify)
```

Run:

```text
python day-81/main.py
```

The first line should be:

```text
my-first-module
```

After that, Python will show help for the function, including the sentence inside triple quotes.

That sentence is called a docstring.

Docstrings are helpful because they let you explain what a function does right where the function is defined.

When you read Python's module documentation, focus on these ideas first:

- a module is a file
- `import name` loads a module
- the module name becomes a prefix for the things inside it
- a file can behave differently when it is run directly instead of imported

Do not try to memorize every import rule today.

Start with the everyday version:

```python
import module_name
```

Then call:

```python
module_name.function_name()
```

That habit will serve you well.

## Mini Challenge

Build a small price helper module.

Create:

```text
day-81/prices.py
```

Code:

```python
def apply_discount(price, percent):
    discount = price * (percent / 100)
    return price - discount


def add_tax(price, percent):
    tax = price * (percent / 100)
    return price + tax


def format_price(price):
    return f"${price:.2f}"


def demo():
    discounted = apply_discount(40, 10)
    with_tax = add_tax(discounted, 8)
    print(format_price(with_tax))


if __name__ == "__main__":
    demo()
```

Create:

```text
day-81/main.py
```

Code:

```python
import prices

subtotal = 40
discounted = prices.apply_discount(subtotal, 10)
total = prices.add_tax(discounted, 8)

print(prices.format_price(total))
```

Run:

```text
python day-81/main.py
```

You should see:

```text
$38.88
```

Then run:

```text
python day-81/prices.py
```

You should see the same value.

That means:

- `prices.py` works when tested directly
- `main.py` can import and use it
- the demo code stays out of the way during import

## Real-World Use

Real Python projects are usually split into modules.

A small command-line app might look like this:

```text
task_app/
  main.py
  storage.py
  display.py
  validation.py
```

Each file has a job:

- `main.py` starts the program
- `storage.py` reads and writes saved data
- `display.py` formats text for the user
- `validation.py` checks whether input is acceptable

This is easier to work with than one giant file.

If something goes wrong with saved data, you know to look in `storage.py`.

If printed text looks strange, you know to look in `display.py`.

Modules help you find the right part of the program faster.

They also make code easier to reuse.

If `price_tools.py` has a good `format_price()` function, several programs can import it instead of copying the same function again and again.

## Recap

Today you learned that:

- a module is a Python file
- `import helpers` looks for `helpers.py`
- imported functions are called with the module prefix, such as `helpers.greet()`
- top-level code runs when a file is imported
- function bodies do not run until the function is called
- `if __name__ == "__main__":` keeps demo code from running during import
- modules help you split a program by responsibility

The most useful pattern from today is:

```text
Put reusable functions in a helper module.
Import that module from the main program.
Keep the helper module mostly quiet when imported.
```

## Lesson Checklist

Before moving on, make sure you can:

- [ ] create two Python files in the same folder
- [ ] define a function in one file
- [ ] import that file from another file
- [ ] call a function with `module_name.function_name()`
- [ ] explain why a top-level `print()` runs during import
- [ ] add a small `demo()` function to a module
- [ ] use `if __name__ == "__main__":` to protect demo code
- [ ] choose a clear file name for a module

## Exercises

### Exercise 1: Create A Temperature Module

Create:

```text
day-81/temperature.py
```

Code:

```python
def to_celsius(fahrenheit):
    return (fahrenheit - 32) * 5 / 9


def to_fahrenheit(celsius):
    return (celsius * 9 / 5) + 32
```

Create:

```text
day-81/main.py
```

Code:

```python
import temperature

print(round(temperature.to_celsius(68), 1))
print(round(temperature.to_fahrenheit(20), 1))
```

You should see:

```text
20.0
68.0
```

### Exercise 2: Add A Demo Guard

Add this to the bottom of `temperature.py`:

```python
def demo():
    print(round(to_celsius(68), 1))
    print(round(to_fahrenheit(20), 1))


if __name__ == "__main__":
    demo()
```

Run both files:

```text
python day-81/temperature.py
python day-81/main.py
```

Both should still work.

The difference is that `main.py` should not print extra demo lines just because it imported `temperature`.

### Exercise 3: Move Repeated Logic

Start with this one-file program:

```python
def clean_word(word):
    return word.strip().lower()


print(clean_word("  Tea "))
print(clean_word("RICE  "))
print(clean_word(" Apples"))
```

Move `clean_word()` into:

```text
day-81/word_tools.py
```

Then import `word_tools` from `main.py` and call:

```python
word_tools.clean_word("  Tea ")
```

### Exercise 4: Check The Module Name

Create:

```text
day-81/name_probe.py
```

Code:

```python
print(__name__)
```

Run it directly:

```text
python day-81/name_probe.py
```

You should see:

```text
__main__
```

Now create:

```text
day-81/main.py
```

Code:

```python
import name_probe
```

Run:

```text
python day-81/main.py
```

You should see:

```text
name_probe
```

That is the reason the guard works.

### Exercise 5: Keep The Import Quiet

Create:

```text
day-81/report_tools.py
```

Code:

```python
def make_heading(title):
    return title.upper()


print(make_heading("daily report"))
```

Create:

```text
day-81/main.py
```

Code:

```python
import report_tools

print(report_tools.make_heading("weekly report"))
```

Run `main.py`.

Then change `report_tools.py` so the daily report print only runs when `report_tools.py` is run directly.

### Exercise 6: Add A Docstring

Create:

```text
day-81/score_tools.py
```

Code:

```python
def is_passing(score):
    """Return True when score is 60 or higher."""
    return score >= 60
```

Create:

```text
day-81/main.py
```

Code:

```python
import score_tools

print(score_tools.is_passing(72))
print(score_tools.is_passing(41))
help(score_tools.is_passing)
```

Read the help text and find your docstring.

### Exercise 7: Use One Module From Another Program

Create:

```text
day-81/labels.py
```

Code:

```python
def name_tag(name, role):
    return f"{name} - {role}"
```

Create:

```text
day-81/main.py
```

Code:

```python
import labels

print(labels.name_tag("Mina", "Developer"))
print(labels.name_tag("Sam", "Designer"))
```

Then create another file:

```text
day-81/event.py
```

Code:

```python
import labels

print(labels.name_tag("Iris", "Host"))
```

Both `main.py` and `event.py` can use the same helper module.

### Exercise 8: Prepare For Tomorrow

In one of your `main.py` files, find every place you wrote a module prefix, such as:

```python
prices.format_price(total)
```

Write a short note:

```text
The module prefix tells me where the function came from.
```

Tomorrow you will learn another import style that lets you bring one function name directly into a file.

For today, prefer the clear version:

```python
import prices
```

and:

```python
prices.format_price(total)
```

## Tiny Win

You can now split a program into more than one file.

That is a real step forward.

A single file can only stay comfortable for so long. Modules let you give code a home, reuse helper functions, and keep the main program easier to read.

You also learned why imported files sometimes print things unexpectedly.

That one detail saves a lot of confusion.

## Tomorrow

Tomorrow is:

```text
Day 82: Imports
```

Today you used the clearest import pattern:

```python
import module_name
```

Tomorrow you will compare import styles, including `from module import name`, aliases, and when a shorter import helps or hurts readability.
