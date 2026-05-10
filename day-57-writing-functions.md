# Day 57: Writing Functions

**Focus:** Defining and calling simple functions with no parameters  
**You will practice:** `def`, function names, parentheses, colons, indentation, calling functions, and spotting common function mistakes  
**Estimated time:** 45-60 minutes

## Today's Goal

Today you will write your first Python functions.

A function is a named group of code that you can run when you need it.

By the end of this lesson, you should be able to:

- write a function with `def`
- choose a clear function name
- use parentheses after the name
- add a colon at the end of the function definition line
- indent the code that belongs to the function
- call the function by writing its name with parentheses
- explain the difference between defining a function and calling a function
- use simple functions to avoid repeating the same lines again and again

Today's functions will not take extra information yet.

That means you will write functions like this:

```python
def greet_user():
    print("Hello!")
    print("Welcome back.")

greet_user()
```

You should see:

```text
Hello!
Welcome back.
```

Tomorrow, you will learn how to pass information into a function.

For today, the goal is simpler:

```text
Give a small action a name.
Then call that name when you want the action to happen.
```

## The Big Idea

A function lets you store a few lines of code under one name.

Without a function, repeated code can look like this:

```python
print("--------------------")
print("Daily Tasks")
print("--------------------")

print("1. Add task")
print("2. View tasks")
print("3. Quit")

print("--------------------")
print("End")
print("--------------------")
```

You should see:

```text
--------------------
Daily Tasks
--------------------
1. Add task
2. View tasks
3. Quit
--------------------
End
--------------------
```

The divider line is useful, but writing it again and again gets noisy.

A function gives that repeated action a name:

```python
def print_divider():
    print("--------------------")

print_divider()
print("Daily Tasks")
print_divider()

print("1. Add task")
print("2. View tasks")
print("3. Quit")

print_divider()
print("End")
print_divider()
```

You should see:

```text
--------------------
Daily Tasks
--------------------
1. Add task
2. View tasks
3. Quit
--------------------
End
--------------------
```

The output is the same.

The code is clearer because `print_divider()` tells you what that repeated line is for.

Here is the basic shape:

```python
def function_name():
    print("Something")
```

Read it like this:

```text
Define a function named function_name.
When this function is called, run the indented code inside it.
```

The line that starts with `def` creates the function.

The indented lines are the body of the function.

The call runs the function:

```python
function_name()
```

The parentheses matter in both places.

## The Mental Model

Think of a function as a named routine.

First, you teach Python the routine:

```python
def say_hello():
    print("Hello!")
```

That only defines the function.

It does not print anything yet.

Then you call the routine:

```python
say_hello()
```

Now Python runs the indented code inside the function.

Put together:

```python
def say_hello():
    print("Hello!")

say_hello()
say_hello()
```

You should see:

```text
Hello!
Hello!
```

This is the first important difference:

```text
Definition: tells Python what the function is.
Call: tells Python to run the function now.
```

Example:

```python
def show_menu():
    print("Menu")
    print("1. Add item")
    print("2. View items")
    print("3. Quit")

print("Starting program...")
show_menu()
print("Program ready.")
```

You should see:

```text
Starting program...
Menu
1. Add item
2. View items
3. Quit
Program ready.
```

Python reads the file from top to bottom.

When it sees the function definition, it remembers the function.

When it sees `show_menu()`, it jumps into the function, runs the indented lines, then comes back to the next line after the call.

That is why this code prints `"Program ready."` after the menu.

## Try It Yourself

Create a file named:

```text
day-57/writing_functions.py
```

Use this section to practice writing and calling small functions.

### Step 1: A Greeting Function

Code:

```python
def greet_user():
    print("Hello!")
    print("Welcome to the program.")

greet_user()
```

You should see:

```text
Hello!
Welcome to the program.
```

The function has three parts:

```text
def greet_user():
```

That line defines the function.

```text
    print("Hello!")
    print("Welcome to the program.")
```

Those indented lines belong to the function.

```text
greet_user()
```

That line calls the function.

### Step 2: Call The Same Function More Than Once

Code:

```python
def print_warning():
    print("Save your work.")

print_warning()
print_warning()
print_warning()
```

You should see:

```text
Save your work.
Save your work.
Save your work.
```

Calling the same function three times runs the function body three times.

You do not need to rewrite the `print()` line each time.

### Step 3: A Divider Function

Code:

```python
def print_divider():
    print("====================")

print("Report")
print_divider()
print("Status: complete")
print("Tasks: 4")
print_divider()
```

You should see:

```text
Report
====================
Status: complete
Tasks: 4
====================
```

This is a good use for a no-parameter function.

The divider does the same thing every time, so it does not need any extra information.

### Step 4: A Menu Function

Code:

```python
def show_menu():
    print("Task Menu")
    print("1. Add task")
    print("2. View tasks")
    print("3. Mark task done")
    print("4. Quit")

show_menu()
```

You should see:

```text
Task Menu
1. Add task
2. View tasks
3. Mark task done
4. Quit
```

Menus often make good functions because the same menu may appear many times in a program.

### Step 5: A Simple Report Printer

Code:

```python
def print_daily_report():
    print("Daily Report")
    print("Tasks completed: 3")
    print("Tasks remaining: 2")
    print("Mood: focused")

print_daily_report()
```

You should see:

```text
Daily Report
Tasks completed: 3
Tasks remaining: 2
Mood: focused
```

This report uses fixed values for now.

That is okay.

Tomorrow you will learn how to pass changing values into a function.

### Step 6: Use Several Small Functions Together

Code:

```python
def print_divider():
    print("--------------------")

def greet_user():
    print("Hello!")
    print("Choose an option below.")

def show_menu():
    print("1. Add note")
    print("2. View notes")
    print("3. Quit")

print_divider()
greet_user()
print_divider()
show_menu()
print_divider()
```

You should see:

```text
--------------------
Hello!
Choose an option below.
--------------------
1. Add note
2. View notes
3. Quit
--------------------
```

Each function handles one small job.

That makes the bottom of the program easier to read:

```python
print_divider()
greet_user()
print_divider()
show_menu()
print_divider()
```

Those lines read almost like a short plan.

## Common Mistake

Functions are simple, but the syntax is strict.

Most beginner function bugs come from one missing symbol or one indentation problem.

### Mistake 1: Defining But Not Calling

Broken code:

```python
def greet_user():
    print("Hello!")
    print("Welcome back.")
```

This code is not broken with an error message.

But it will not print anything.

The function was defined, but it was never called.

Fixed code:

```python
def greet_user():
    print("Hello!")
    print("Welcome back.")

greet_user()
```

You should see:

```text
Hello!
Welcome back.
```

Remember:

```text
Defining a function stores it.
Calling a function runs it.
```

### Mistake 2: Forgetting Parentheses When Calling

Broken code:

```python
def show_menu():
    print("Menu")
    print("1. Start")
    print("2. Quit")

show_menu
```

This code does not call the function.

The name `show_menu` points to the function, but the parentheses are what run it.

Fixed code:

```python
def show_menu():
    print("Menu")
    print("1. Start")
    print("2. Quit")

show_menu()
```

You should see:

```text
Menu
1. Start
2. Quit
```

### Mistake 3: Forgetting The Colon

Broken code:

```python
def print_divider()
    print("--------------------")

print_divider()
```

This is broken because the first line needs a colon:

```text
def print_divider():
```

Python may show:

```text
SyntaxError: expected ':'
```

Fixed code:

```python
def print_divider():
    print("--------------------")

print_divider()
```

You should see:

```text
--------------------
```

### Mistake 4: Wrong Indentation

Broken code:

```python
def greet_user():
print("Hello!")
print("Welcome back.")

greet_user()
```

This is broken because the body of the function must be indented.

Python may show:

```text
IndentationError: expected an indented block
```

Fixed code:

```python
def greet_user():
    print("Hello!")
    print("Welcome back.")

greet_user()
```

You should see:

```text
Hello!
Welcome back.
```

### Mistake 5: Indenting Too Much

Broken code:

```python
def say_done():
    print("Done")
    say_done()
```

This code calls `say_done()` inside itself.

That means the function keeps calling itself again and again.

You are not learning that pattern yet.

For now, the function call should usually line up with the `def` line:

Fixed code:

```python
def say_done():
    print("Done")

say_done()
```

You should see:

```text
Done
```

## Debug It

Read each broken example before looking at the fix.

Ask:

```text
Was the function defined?
Was the function called?
Are the parentheses there?
Is the colon there?
Is the function body indented?
```

### Debug 1

Broken code:

```python
def print_header():
    print("Notes App")
    print("--------")
```

The goal is to print the header.

What is missing?

Fixed code:

```python
def print_header():
    print("Notes App")
    print("--------")

print_header()
```

You should see:

```text
Notes App
--------
```

The missing line was the function call.

### Debug 2

Broken code:

```python
def show_menu():
    print("1. Add")
    print("2. View")
    print("3. Quit")

show_menu
```

The goal is to show the menu.

What is missing?

Fixed code:

```python
def show_menu():
    print("1. Add")
    print("2. View")
    print("3. Quit")

show_menu()
```

You should see:

```text
1. Add
2. View
3. Quit
```

The missing part was `()` after the function name.

### Debug 3

Broken code:

```python
def print_status():
    print("Checking status")
print("Status: ready")

print_status()
```

The goal is for both print lines to belong to the function.

This code runs, but it runs in a surprising order.

Because the second `print()` line is not indented, it is outside the function.

Fixed code:

```python
def print_status():
    print("Checking status")
    print("Status: ready")

print_status()
```

You should see:

```text
Checking status
Status: ready
```

Indentation decides what belongs inside the function.

### Debug 4

Broken code:

```python
def print_footer():
    print("End of report")
    print("Thank you")

    print_footer()
```

The goal is to call the function once.

This is broken because the call is indented inside the function.

Fixed code:

```python
def print_footer():
    print("End of report")
    print("Thank you")

print_footer()
```

You should see:

```text
End of report
Thank you
```

The call should line up with `def` when you want it to happen after the function is defined.

## Read the Docs

Python's official tutorial has a section about defining functions.

You do not need to understand every part yet.

For today, look for this pattern:

```python
def name():
    print("Something")
```

When you read examples in the docs, ask:

```text
Where is the function defined?
Where is it called?
Which lines are indented inside the function?
```

You will understand more of the docs after tomorrow's lesson on parameters.

## Mini Challenge

Create a file named:

```text
day-57/simple_app_screen.py
```

Build a small program screen using functions.

Your program should have these functions:

```text
print_divider
print_title
show_menu
print_tip
```

Each function should print something.

None of the functions should use parameters yet.

Try this:

```python
def print_divider():
    print("====================")

def print_title():
    print("Notes App")

def show_menu():
    print("1. Add note")
    print("2. View notes")
    print("3. Quit")

def print_tip():
    print("Tip: Save your notes before quitting.")

print_divider()
print_title()
print_divider()
show_menu()
print_divider()
print_tip()
```

You should see:

```text
====================
Notes App
====================
1. Add note
2. View notes
3. Quit
====================
Tip: Save your notes before quitting.
```

After it works, change only the text inside one function.

Run the program again.

Notice how the main part of the program can stay the same.

## Real-World Use

Functions help you organize repeated actions.

In small programs, you might use functions for:

- greeting the user
- printing a divider line
- showing a menu
- printing help text
- printing a report
- showing a goodbye message
- grouping the setup steps at the start of a program

Example:

```python
def print_header():
    print("Budget Tracker")
    print("--------------")

def show_menu():
    print("1. Add expense")
    print("2. View total")
    print("3. Quit")

def print_goodbye():
    print("Goodbye!")

print_header()
show_menu()
print_goodbye()
```

You should see:

```text
Budget Tracker
--------------
1. Add expense
2. View total
3. Quit
Goodbye!
```

This program does not do much yet.

But its shape is useful:

```text
print_header()
show_menu()
print_goodbye()
```

That is easier to scan than one long block of print statements.

As programs grow, functions help you find the part you want to change.

If the menu text needs to change, you look in `show_menu()`.

If the header needs to change, you look in `print_header()`.

## Recap

A function is a named block of code.

You define a function with `def`:

```python
def greet_user():
    print("Hello!")
```

You call a function with its name and parentheses:

```python
greet_user()
```

The colon starts the function body.

The indentation shows which lines belong inside the function.

The definition does not run the body by itself.

The call runs the body.

For now, your functions use empty parentheses:

```python
def show_menu():
    print("1. Start")
    print("2. Quit")
```

The empty parentheses mean:

```text
This function does not need extra information yet.
```

## Lesson Checklist

Before moving on, make sure you can:

- write a function using `def`
- put `()` after the function name
- add `:` at the end of the definition line
- indent the function body
- call a function after defining it
- explain why defining and calling are different
- use a function to avoid repeating a divider line
- write a function that displays a menu
- fix missing parentheses, missing colons, and indentation mistakes

## Exercises

### Exercise 1

Write a function named `say_hello`.

It should print:

```text
Hello, learner!
```

Call the function once.

### Exercise 2

Write a function named `print_divider`.

It should print:

```text
--------------------
```

Call it three times.

### Exercise 3

Write a function named `show_menu`.

It should print:

```text
1. Add item
2. View items
3. Quit
```

Call the function once.

### Exercise 4

Write a function named `print_reminder`.

It should print the same reminder message twice.

Call the function twice.

### Exercise 5

Write a function named `print_report`.

It should print:

```text
Weekly Report
Items finished: 5
Items left: 2
```

Call the function once.

### Exercise 6

Fix the broken code.

Broken code:

```python
def say_ready():
    print("Ready")
```

The goal is to print:

```text
Ready
```

### Exercise 7

Fix the broken code.

Broken code:

```python
def print_line()
    print("==========")

print_line()
```

The goal is to print the line.

### Exercise 8

Fix the broken code.

Broken code:

```python
def show_title():
print("My Program")

show_title()
```

The goal is to print the title.

### Exercise 9

Fix the broken code.

Broken code:

```python
def show_help():
    print("Choose a number from the menu.")

show_help
```

The goal is to print the help message.

### Exercise 10

Write three functions:

```text
print_header
show_menu
print_footer
```

Call them in that order.

Each function should print at least one line.

### Exercise 11

Write a small program that uses these functions:

```text
print_divider
print_daily_report
print_goodbye
```

Call `print_divider()` before and after the report.

### Exercise 12

Look at an older program from this course.

Find two or more repeated `print()` lines.

Write a function that could replace the repeated lines.

You do not need to rewrite the whole old program yet.

Just practice spotting a useful function.

### Exercise 13

Write a function named `show_app_start`.

It should print:

```text
Starting app...
Loading menu...
Ready.
```

Call it once at the start of a program.

### Exercise 14

Write a function named `print_blank_line`.

It should print an empty line.

Use it between two sections of output.

### Exercise 15

Write a function named `print_todo_summary`.

For now, it should print fixed values:

```text
Todo Summary
Open: 4
Done: 2
```

Call it once.

Then add a comment above the function call that says what the call does.

## Tiny Win

You can now name a small action and run it whenever you need it.

That changes how your programs are organized.

Before functions, your programs were mostly one line after another.

Now you can write code like this:

```python
print_header()
show_menu()
print_goodbye()
```

Those calls make the program easier to read.

They also make repeated code easier to change.

## Tomorrow

Tomorrow is:

```text
Day 58: Parameters
```

Today's functions always did the same thing.

That is useful for greetings, dividers, menus, repeated messages, and fixed reports.

But sometimes a function needs extra information.

For example, instead of writing a greeting that always says the same thing, you may want:

```python
greet_user("Mina")
greet_user("Sam")
greet_user("Iris")
```

That is what parameters are for.

Tomorrow you will learn how to write functions that receive values and use them inside the function body.
