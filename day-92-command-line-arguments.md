# Day 92: Command-Line Arguments

**Focus:** Running Python scripts with information typed into the command  
**You will practice:** `sys.argv`, script names, required arguments, optional arguments, flags, `argparse`, help text, error messages, and converting command-line text into numbers  
**Estimated time:** 60-75 minutes

## Today's Goal

Today you will learn how to give a Python program information before it starts running.

So far, many of your programs have used `input()`:

```python
name = input("Name: ")
```

That works well for interactive programs.

But many real tools are run more like this:

```text
python greet.py Mina
python calculator.py add 10 5
python report.py sales.csv --summary
```

The extra words after the file name are called command-line arguments.

By the end of today, you should be able to:

- explain what command-line arguments are
- read raw arguments with `sys.argv`
- explain why `sys.argv[0]` is the script name
- check whether a required argument was provided
- use default values for optional arguments
- convert argument strings into numbers
- recognize common `sys.argv` mistakes
- use `argparse` for cleaner command-line programs
- create required positional arguments with `argparse`
- create optional named arguments with `--name`
- create true-or-false flags with `action="store_true"`
- read automatic help text
- understand basic command-line error messages
- prepare for Day 93, where you will organize a larger program across multiple files

Today starts with the simplest tool, `sys.argv`.

Then you will learn `argparse`, which is the better choice once a script has more than one or two options.

## The Big Idea

When you run a Python file from the command line, you can type extra words after the file name.

This command:

```text
python greet.py Mina
```

sends one argument to the script:

```text
Mina
```

This command:

```text
python calculator.py add 10 5
```

sends three arguments:

```text
add
10
5
```

Python can read those words from a list named:

```text
sys.argv
```

The name `argv` is short for argument vector.

You do not need to use that phrase in normal conversation. Just remember:

```text
sys.argv is the list of command-line words Python received.
```

The first item is special.

`sys.argv[0]` is the script name.

The arguments typed after the script name start at `sys.argv[1]`.

```text
python greet.py Mina
       ^        ^
       |        |
       |        sys.argv[1]
       sys.argv[0]
```

That one-index difference is a common beginner mistake, so slow down around it.

## The Mental Model

Think of a command as a row of words.

```text
python greet.py Mina
```

The terminal starts Python.

Python runs `greet.py`.

Python gives the script a list that looks similar to this:

```python
["greet.py", "Mina"]
```

If you type more words:

```text
python repeat_greet.py Mina 3
```

the list looks similar to this:

```python
["repeat_greet.py", "Mina", "3"]
```

Notice that `"3"` is a string.

Command-line arguments arrive as text, even when they look like numbers.

If you want to do math with them, you must convert them:

```python
count = int("3")
```

Quotes matter in the terminal too.

This command has two arguments after the script name:

```text
python greet.py Mina Patel
```

Those arguments are:

```text
Mina
Patel
```

This command has one argument after the script name:

```text
python greet.py "Mina Patel"
```

That argument is:

```text
Mina Patel
```

Use quotes when one argument contains spaces.

## Example: Reading `sys.argv`

Create this file:

```text
day-92/show_args.py
```

Add:

```python
import sys

print(sys.argv)
```

Run it with no extra arguments:

```text
python show_args.py
```

You should see a list with the script name:

```text
['show_args.py']
```

Now run it with two extra arguments:

```text
python show_args.py Mina 3
```

You should see something similar to:

```text
['show_args.py', 'Mina', '3']
```

The exact script name can include more path information depending on how you run the file.

The important pattern is:

```text
index 0: the script name
index 1: the first argument after the script name
index 2: the second argument after the script name
```

You can print those pieces separately:

```python
import sys

print(f"Script name: {sys.argv[0]}")

if len(sys.argv) > 1:
    print(f"First argument: {sys.argv[1]}")
else:
    print("No first argument was provided.")
```

Run:

```text
python show_args.py Mina
```

You should see something similar to:

```text
Script name: show_args.py
First argument: Mina
```

Run:

```text
python show_args.py
```

You should see:

```text
Script name: show_args.py
No first argument was provided.
```

The `len(sys.argv) > 1` check prevents an `IndexError`.

## Required Arguments With `sys.argv`

A required argument is an argument the program needs in order to do its job.

Create this file:

```text
day-92/greet.py
```

Add:

```python
import sys

if len(sys.argv) < 2:
    print("Usage: python greet.py NAME")
else:
    name = sys.argv[1]
    print(f"Hello, {name}!")
```

Run it correctly:

```text
python greet.py Mina
```

You should see:

```text
Hello, Mina!
```

Run it without the required argument:

```text
python greet.py
```

You should see:

```text
Usage: python greet.py NAME
```

That usage line is a short reminder showing how the script should be run.

The word `NAME` is not magic. It is just a human-friendly placeholder.

It means:

```text
Put a name here.
```

## Optional Arguments With `sys.argv`

An optional argument has a default value when the user does not provide it.

Create this file:

```text
day-92/friendly_greet.py
```

Add:

```python
import sys

if len(sys.argv) >= 2:
    name = sys.argv[1]
else:
    name = "friend"

print(f"Hello, {name}!")
```

Run:

```text
python friendly_greet.py Mina
```

You should see:

```text
Hello, Mina!
```

Run:

```text
python friendly_greet.py
```

You should see:

```text
Hello, friend!
```

This is fine for one simple optional value.

But as soon as you add several options, manual `sys.argv` checks become harder to read.

That is why Python includes `argparse`, which you will use soon.

## Converting Argument Types

Every value in `sys.argv` is a string.

That means this script does not add numbers:

```python
import sys

left = sys.argv[1]
right = sys.argv[2]

print(left + right)
```

Run:

```text
python add_text.py 2 3
```

You would see:

```text
23
```

Python joined two strings.

To do math, convert the strings first:

```python
import sys

left = int(sys.argv[1])
right = int(sys.argv[2])

print(left + right)
```

Run:

```text
python add_numbers.py 2 3
```

You should see:

```text
5
```

Now make the conversion safer.

Create this file:

```text
day-92/repeat_greet.py
```

Add:

```python
import sys

if len(sys.argv) < 3:
    print("Usage: python repeat_greet.py NAME COUNT")
else:
    name = sys.argv[1]

    try:
        count = int(sys.argv[2])
    except ValueError:
        print("COUNT must be a whole number.")
    else:
        for number in range(count):
            print(f"{number + 1}. Hello, {name}!")
```

Run:

```text
python repeat_greet.py Mina 3
```

You should see:

```text
1. Hello, Mina!
2. Hello, Mina!
3. Hello, Mina!
```

Run:

```text
python repeat_greet.py Mina three
```

You should see:

```text
COUNT must be a whole number.
```

That `try` and `except` protects the program from crashing when the user gives text that cannot become an integer.

## When `sys.argv` Gets Awkward

`sys.argv` is useful because it is direct.

It shows you exactly what Python receives.

But look at what you have to manage yourself:

- checking how many arguments were provided
- writing usage messages
- converting strings to numbers
- deciding which arguments are required
- deciding which arguments are optional
- handling flags like `--loud`
- showing help text
- showing clear error messages

For tiny scripts, `sys.argv` is enough.

For tools that other people might use, reach for `argparse`.

## `argparse` Basics

`argparse` is a standard library module for command-line arguments.

It helps you describe what your program accepts.

Then it does much of the checking for you.

Create this file:

```text
day-92/greet_argparse.py
```

Add:

```python
import argparse

parser = argparse.ArgumentParser(description="Greet someone from the command line.")
parser.add_argument("name", help="the person to greet")

args = parser.parse_args()

print(f"Hello, {args.name}!")
```

Run:

```text
python greet_argparse.py Mina
```

You should see:

```text
Hello, Mina!
```

Now run:

```text
python greet_argparse.py
```

You should see an error similar to:

```text
usage: greet_argparse.py [-h] name
greet_argparse.py: error: the following arguments are required: name
```

You did not write that error message yourself.

`argparse` knew that `name` was required because you added it as a positional argument:

```python
parser.add_argument("name", help="the person to greet")
```

A positional argument is matched by where it appears in the command.

In this command:

```text
python greet_argparse.py Mina
```

`Mina` fills the `name` argument.

## Help Text

`argparse` automatically creates help text.

Run:

```text
python greet_argparse.py --help
```

You should see help similar to:

```text
usage: greet_argparse.py [-h] name

Greet someone from the command line.

positional arguments:
  name        the person to greet

options:
  -h, --help  show this help message and exit
```

Help text matters because command-line programs do not have buttons or menus.

A user needs a quick way to ask:

```text
How do I run this?
```

The standard answer is:

```text
--help
```

Your `description` becomes the sentence near the top.

Your argument `help` text becomes the explanation beside the argument.

Good help text is short and practical.

## Optional Named Arguments

In `argparse`, a required positional argument usually looks like this:

```text
name
```

An optional named argument usually starts with dashes:

```text
--times
```

Update `day-92/greet_argparse.py`:

```python
import argparse

parser = argparse.ArgumentParser(description="Greet someone from the command line.")
parser.add_argument("name", help="the person to greet")
parser.add_argument("--times", type=int, default=1, help="how many greetings to print")

args = parser.parse_args()

for number in range(args.times):
    print(f"{number + 1}. Hello, {args.name}!")
```

Run:

```text
python greet_argparse.py Mina
```

You should see:

```text
1. Hello, Mina!
```

Run:

```text
python greet_argparse.py Mina --times 3
```

You should see:

```text
1. Hello, Mina!
2. Hello, Mina!
3. Hello, Mina!
```

This line does two useful things:

```python
parser.add_argument("--times", type=int, default=1, help="how many greetings to print")
```

It gives the option a default:

```text
1
```

It also converts the value to an integer:

```text
type=int
```

If the user types a value that cannot become an integer:

```text
python greet_argparse.py Mina --times many
```

`argparse` shows an error similar to:

```text
usage: greet_argparse.py [-h] [--times TIMES] name
greet_argparse.py: error: argument --times: invalid int value: 'many'
```

Again, you did not have to write that error message by hand.

## Flags

A flag is an option that is either on or off.

For example:

```text
--excited
```

The user does not type a value after it.

The flag itself means `True`.

Update `day-92/greet_argparse.py` again:

```python
import argparse

parser = argparse.ArgumentParser(description="Greet someone from the command line.")
parser.add_argument("name", help="the person to greet")
parser.add_argument("--times", type=int, default=1, help="how many greetings to print")
parser.add_argument("--excited", action="store_true", help="add an exclamation point")

args = parser.parse_args()

ending = "!" if args.excited else "."

for number in range(args.times):
    print(f"{number + 1}. Hello, {args.name}{ending}")
```

Run:

```text
python greet_argparse.py Mina
```

You should see:

```text
1. Hello, Mina.
```

Run:

```text
python greet_argparse.py Mina --excited
```

You should see:

```text
1. Hello, Mina!
```

Run:

```text
python greet_argparse.py Mina --times 2 --excited
```

You should see:

```text
1. Hello, Mina!
2. Hello, Mina!
```

This part creates the flag:

```python
parser.add_argument("--excited", action="store_true", help="add an exclamation point")
```

`action="store_true"` means:

```text
If the user includes this flag, store True.
If the user leaves it out, store False.
```

Flags are useful for settings like:

```text
--verbose
--dry-run
--summary
--save
--debug
```

## A Small Calculator With `argparse`

Now build a small calculator.

Create this file:

```text
day-92/calculator.py
```

Add:

```python
import argparse

parser = argparse.ArgumentParser(description="Do one simple calculation.")
parser.add_argument("left", type=float, help="the first number")
parser.add_argument("operation", choices=["add", "sub", "mul", "div"], help="the operation")
parser.add_argument("right", type=float, help="the second number")
parser.add_argument("--round", type=int, default=None, help="number of decimal places")

args = parser.parse_args()

if args.operation == "add":
    result = args.left + args.right
elif args.operation == "sub":
    result = args.left - args.right
elif args.operation == "mul":
    result = args.left * args.right
else:
    if args.right == 0:
        parser.error("right number cannot be 0 when using div")

    result = args.left / args.right

if args.round is not None:
    result = round(result, args.round)

print(result)
```

Run:

```text
python calculator.py 10 add 5
```

You should see:

```text
15.0
```

Run:

```text
python calculator.py 10 div 4
```

You should see:

```text
2.5
```

Run:

```text
python calculator.py 10 div 3 --round 2
```

You should see:

```text
3.33
```

The `choices` setting limits the operation:

```python
parser.add_argument("operation", choices=["add", "sub", "mul", "div"], help="the operation")
```

If the user types an operation you did not allow:

```text
python calculator.py 10 power 2
```

`argparse` shows an error similar to:

```text
calculator.py: error: argument operation: invalid choice: 'power'
```

That is better than letting a strange value travel deeper into the program.

The division-by-zero check uses:

```python
parser.error("right number cannot be 0 when using div")
```

That prints a normal command-line error and stops the program.

## Script Name And Program Name

With `sys.argv`, the script name is:

```python
sys.argv[0]
```

With `argparse`, the parser also knows the program name.

Usually you do not need to set it.

It will use the script name in help and error output:

```text
usage: calculator.py [-h] [--round ROUND] left {add,sub,mul,div} right
```

If you ever need to customize the name shown in help, you can pass `prog`:

```python
parser = argparse.ArgumentParser(
    prog="calc",
    description="Do one simple calculation."
)
```

Then the help text starts with:

```text
usage: calc ...
```

For beginner scripts, the default is usually fine.

The bigger point is to remember that the script name is separate from the arguments the user provides.

## Try It Yourself

Create a folder named:

```text
day-92
```

Inside it, create these files one at a time:

```text
day-92/show_args.py
day-92/greet.py
day-92/repeat_greet.py
day-92/greet_argparse.py
day-92/calculator.py
```

Run each file from inside the `day-92` folder.

For `show_args.py`, try:

```text
python show_args.py
python show_args.py red blue green
python show_args.py "red blue" green
```

For `greet.py`, try:

```text
python greet.py Mina
python greet.py
```

For `repeat_greet.py`, try:

```text
python repeat_greet.py Mina 3
python repeat_greet.py Mina three
```

For `greet_argparse.py`, try:

```text
python greet_argparse.py Mina
python greet_argparse.py Mina --times 3
python greet_argparse.py Mina --times 2 --excited
python greet_argparse.py --help
```

For `calculator.py`, try:

```text
python calculator.py 10 add 5
python calculator.py 10 div 3 --round 2
python calculator.py 10 power 2
python calculator.py 10 div 0
python calculator.py --help
```

Some of those commands are supposed to show errors.

That is part of the practice.

You are learning how a command-line tool explains what went wrong.

## Common Mistake

The most common `sys.argv` mistake is reading an argument that was not provided.

This code has a problem:

```python
import sys

name = sys.argv[1]
print(f"Hello, {name}!")
```

If the user runs:

```text
python greet.py
```

there is no `sys.argv[1]`.

Python raises an error similar to:

```text
IndexError: list index out of range
```

Check the length first:

```python
import sys

if len(sys.argv) < 2:
    print("Usage: python greet.py NAME")
else:
    name = sys.argv[1]
    print(f"Hello, {name}!")
```

Another common mistake is forgetting that arguments are strings.

This code joins text:

```python
import sys

print(sys.argv[1] + sys.argv[2])
```

Run:

```text
python add.py 2 3
```

You would see:

```text
23
```

Convert first:

```python
import sys

left = int(sys.argv[1])
right = int(sys.argv[2])

print(left + right)
```

A third common mistake is writing a flag as if it needs a value.

With this argument:

```python
parser.add_argument("--excited", action="store_true")
```

run:

```text
python greet_argparse.py Mina --excited
```

Do not run:

```text
python greet_argparse.py Mina --excited yes
```

The flag itself is the value.

It means:

```text
excited is True
```

## Debug It

When command-line arguments feel confusing, print what the program received.

For `sys.argv`, add:

```python
print(sys.argv)
```

near the top of the file.

Then run the command again.

This helps you answer:

- How many arguments did Python receive?
- Did the script name take index `0`?
- Did a value with spaces get split into multiple arguments?
- Did I forget quotes around a multi-word value?

For `argparse`, start with help:

```text
python script_name.py --help
```

That shows:

- which positional arguments are required
- which named options exist
- which flags exist
- what each argument is called

### Problem 1: Missing Required Argument

Command:

```text
python greet_argparse.py
```

Possible message:

```text
greet_argparse.py: error: the following arguments are required: name
```

Meaning:

```text
The parser expected a positional argument named name.
```

Fix:

```text
python greet_argparse.py Mina
```

### Problem 2: Invalid Number

Command:

```text
python greet_argparse.py Mina --times many
```

Possible message:

```text
greet_argparse.py: error: argument --times: invalid int value: 'many'
```

Meaning:

```text
The parser tried to convert many with int(), but that is not a whole number.
```

Fix:

```text
python greet_argparse.py Mina --times 3
```

### Problem 3: Invalid Choice

Command:

```text
python calculator.py 10 power 2
```

Possible message:

```text
calculator.py: error: argument operation: invalid choice: 'power'
```

Meaning:

```text
The operation must be one of the choices you listed.
```

Fix:

```text
python calculator.py 10 mul 2
```

### Problem 4: Multi-Word Argument Split Apart

Command:

```text
python greet_argparse.py Mina Patel
```

Possible message:

```text
greet_argparse.py: error: unrecognized arguments: Patel
```

Meaning:

```text
The parser used Mina as the name, then did not know what to do with Patel.
```

Fix:

```text
python greet_argparse.py "Mina Patel"
```

## Read the Docs

For today, read documentation with one small question in mind:

```text
How does Python receive command-line arguments?
How does argparse define arguments?
How does argparse create help text?
```

Useful pages:

```text
https://docs.python.org/3/library/sys.html#sys.argv
https://docs.python.org/3/library/argparse.html
```

In the `argparse` documentation, look for:

- `ArgumentParser`
- `add_argument`
- positional arguments
- optional arguments
- `type`
- `default`
- `choices`
- `store_true`

You do not need every advanced feature.

For beginner command-line tools, these are enough:

```python
parser = argparse.ArgumentParser(description="...")
parser.add_argument("name")
parser.add_argument("--times", type=int, default=1)
parser.add_argument("--excited", action="store_true")
args = parser.parse_args()
```

That small pattern can carry many useful scripts.

## Mini Challenge

Create this file:

```text
day-92/profile_card.py
```

Write a command-line program with `argparse`.

It should accept:

- a required `name`
- an optional `--city` value with a default of `"Unknown"`
- an optional `--age` value converted with `int`
- a `--student` flag

Starter code:

```python
import argparse

parser = argparse.ArgumentParser(description="Print a small profile card.")
parser.add_argument("name", help="the person's name")
parser.add_argument("--city", default="Unknown", help="the person's city")
parser.add_argument("--age", type=int, default=None, help="the person's age")
parser.add_argument("--student", action="store_true", help="mark the person as a student")

args = parser.parse_args()

print(f"Name: {args.name}")
print(f"City: {args.city}")

if args.age is not None:
    print(f"Age: {args.age}")

if args.student:
    print("Student: yes")
else:
    print("Student: no")
```

Try:

```text
python profile_card.py Mina --city Pune --age 21 --student
python profile_card.py Leo
python profile_card.py --help
```

Then add one more optional value of your own.

For example:

```text
--favorite-language
--role
--team
```

Use a clear help message for it.

## Real-World Use

Command-line arguments are everywhere in developer tools.

You have already seen commands shaped like this:

```text
python -m pip install requests
python -m venv .venv
```

Those commands are full of arguments.

Other tools use the same idea:

```text
git commit -m "Add greeting script"
python script.py --help
python report.py data.csv --summary
```

Command-line arguments are useful when:

- you want to run the same script with different inputs
- you want a script to work in automation
- you do not want the program to stop and ask for `input()`
- you want clear help text for other users
- you want a small program to feel like a real tool

A script that asks for input is fine for a human sitting at the keyboard.

A script with command-line arguments is easier to reuse from another command, a schedule, a batch file, a shell script, or a larger project.

That matters more as your programs grow.

## Recap

Command-line arguments are values typed after the script name.

`sys.argv` gives you the raw list.

`sys.argv[0]` is the script name.

`sys.argv[1]` is the first argument after the script name.

Every value in `sys.argv` is a string.

Use `int()` or `float()` when you need numbers.

Check `len(sys.argv)` before reading indexes that might not exist.

Use `argparse` when your script needs required arguments, optional named arguments, flags, automatic help text, automatic type conversion, or cleaner error messages.

With `argparse`, this creates a required positional argument:

```python
parser.add_argument("name")
```

This creates an optional named argument:

```python
parser.add_argument("--times", type=int, default=1)
```

This creates a flag:

```python
parser.add_argument("--excited", action="store_true")
```

This reads the user's command:

```python
args = parser.parse_args()
```

## Lesson Checklist

Before moving on, make sure you can:

- explain what command-line arguments are
- inspect raw arguments with `sys.argv`
- explain why `sys.argv[0]` is the script name
- read `sys.argv[1]` only after checking the list length
- write a simple usage message
- explain why command-line values arrive as strings
- convert an argument with `int()` or `float()`
- catch a bad conversion with `ValueError`
- create an `ArgumentParser`
- add a required positional argument
- add an optional named argument with a default value
- add a flag with `action="store_true"`
- use `type=int` or `type=float`
- use `choices` to limit allowed values
- run a script with `--help`
- understand a basic `argparse` error message

## Exercises

### Exercise 1: Inspect Arguments

Create this file:

```text
day-92/inspect_args.py
```

Write a program that prints:

- the whole `sys.argv` list
- the script name
- the number of arguments after the script name

Starter code:

```python
import sys

print(f"All arguments: {sys.argv}")
print(f"Script name: {sys.argv[0]}")
print(f"Extra argument count: {len(sys.argv) - 1}")
```

Try:

```text
python inspect_args.py
python inspect_args.py one two three
python inspect_args.py "one two" three
```

### Exercise 2: Required Favorite Color

Create this file:

```text
day-92/favorite_color.py
```

Use `sys.argv`.

If the user provides a color, print:

```text
Your favorite color is blue.
```

If the user does not provide a color, print:

```text
Usage: python favorite_color.py COLOR
```

Test both cases.

### Exercise 3: Add Two Numbers With `sys.argv`

Create this file:

```text
day-92/add_two.py
```

Use `sys.argv` to read two required numbers.

Convert them with `float()`.

Print the sum.

If either value cannot become a number, print:

```text
Both values must be numbers.
```

Try:

```text
python add_two.py 2 3
python add_two.py 2.5 3.5
python add_two.py two 3
```

### Exercise 4: Greeting With `argparse`

Create this file:

```text
day-92/greeting_tool.py
```

Use `argparse`.

The script should accept:

- required `name`
- optional `--times` as an integer with default `1`
- optional `--loud` flag

If `--loud` is included, print the greeting in uppercase.

Try:

```text
python greeting_tool.py Mina
python greeting_tool.py Mina --times 3
python greeting_tool.py Mina --times 2 --loud
python greeting_tool.py --help
```

### Exercise 5: Temperature Converter

Create this file:

```text
day-92/convert_temp.py
```

Use `argparse`.

Accept:

- a required number named `temperature`
- a required choice named `unit` that can be `c` or `f`

If the unit is `c`, convert Celsius to Fahrenheit.

If the unit is `f`, convert Fahrenheit to Celsius.

Formulas:

```text
fahrenheit = celsius * 9 / 5 + 32
celsius = (fahrenheit - 32) * 5 / 9
```

Try:

```text
python convert_temp.py 0 c
python convert_temp.py 32 f
python convert_temp.py 100 x
```

The last command should show an `argparse` choice error.

### Exercise 6: Better Help Text

Open one of your `argparse` scripts.

Improve:

- the parser `description`
- each argument's `help` text

Then run:

```text
python script_name.py --help
```

Check whether a beginner could understand how to use the script.

Short help text is usually better than long help text.

### Exercise 7: Limit Choices

Create this file:

```text
day-92/task_filter.py
```

Use `argparse`.

Accept a required argument named `status`.

Limit it to these choices:

```text
todo
doing
done
```

Print:

```text
Showing tasks with status: todo
```

Try a valid status and an invalid status.

Notice how `argparse` handles the invalid one.

### Exercise 8: Explain The Difference

In your own words, answer:

- When would `sys.argv` be enough?
- When would `argparse` be better?
- Why is `--help` useful?
- Why do command-line numbers need conversion?

Keep each answer to one or two sentences.

## Tiny Win

You can now write scripts that behave more like real command-line tools.

That is a practical step forward.

Instead of changing code every time you want a different input, you can pass the input when you run the program.

That makes your scripts easier to reuse, test by hand, and combine with other tools.

## Tomorrow

Tomorrow is:

```text
Day 93: Organizing a Multi-File Project
```

Today your scripts stayed in one file.

On Day 93, you will take the next step: separating a program into smaller files with clear jobs.

For example, a command-line app might grow into pieces like:

```text
day-93/
  main.py
  arguments.py
  calculator.py
  display.py
```

The command-line argument parsing can live near the program entrance.

The real work can live in helper modules.

That separation makes larger projects easier to read, test, and change.
