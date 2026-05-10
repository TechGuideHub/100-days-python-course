# Day 02: Setting Up Python

**Focus:** Install or confirm Python, create a course folder, and run a small `.py` file.  
**You will practice:** checking versions, using the terminal, saving a file, running a script, and reading output.  
**Estimated time:** 35-50 minutes

## Today's Goal

Today you will prepare your computer to run Python programs.

By the end of this lesson, you should be able to:

- check whether Python is installed
- open a terminal
- run a simple command
- create a small Python file
- run that file and compare the output with what you expected

Setup is part of programming. Before you can build with Python, you need to confirm that your tools are available and that you know how to run a file.

## The Big Idea

Python code does not run by itself. Your computer needs the Python program installed so it can read your `.py` files and execute the instructions inside them.

Runnable example:

```python
print("Hello, Python!")
```

Expected output:

```text
Hello, Python!
```

> Key idea: Python is the tool that reads your Python code and runs it.

Today has one practical purpose: make sure Python is installed and working.

## The Mental Model

Think of setup as preparing a work area.

- Python runs your code.
- Your code editor is where you write and save code.
- The terminal is where you type commands.
- A `.py` file is a saved Python program.

When those pieces are connected, the workflow becomes simple:

```text
write code -> save the file -> run the file -> read the output
```

That loop will appear again and again throughout the course.

## What You Need

For this course, you need three things:

1. Python
2. A code editor
3. A terminal

### Python

Python runs your programs. For this course, use Python 3.

### Code Editor

A code editor is where you write code. Beginner-friendly options include:

- Visual Studio Code
- PyCharm Community Edition
- Thonny

Use the editor your course, school, or computer already supports. Today, the goal is not to compare editors. The goal is to write and run a small file.

### Terminal

The terminal is where you type commands.

Depending on your computer, it may be called Terminal, PowerShell, Command Prompt, or something similar.

You do not need to master the terminal today. You only need to run a few short commands.

## Step 1: Check Whether Python Is Installed

Open a terminal.

Command:

```bash
python --version
```

Expected output:

```text
Python 3.x.x
```

If that works, Python is installed.

If it does not work, try one of these commands.

Command:

```bash
py --version
```

Command:

```bash
python3 --version
```

Different computers may use different command names. The important result is that one command shows a Python 3 version.

## Step 2: Install Python If Needed

If none of the version commands work, install Python from the official Python website or from the method recommended by your course or school.

During installation, you may see an option named something like this.

Text to look for:

```text
Add Python to PATH
```

If you see that option, turn it on. It helps your terminal find Python later.

After installing Python, close the terminal, open it again, and check the version once more.

Command:

```bash
python --version
```

If needed, try:

```bash
py --version
```

or:

```bash
python3 --version
```

Checkpoint:

```text
One command should show a Python 3 version.
```

## Step 3: Create a Course Folder

Create a folder for your Python work.

Folder name:

```text
python-lessons
```

Inside it, create another folder for today.

Folder path:

```text
day-02/
```

Keeping files organized matters. It makes it easier to find your work, rerun examples, and continue tomorrow without guessing where everything went.

## Step 4: Create Your First Python File

Open your code editor.

Create a new file and save it in the `day-02/` folder.

File path:

```text
day-02/hello.py
```

The `.py` ending tells your editor and your computer that this is a Python file.

Runnable example:

```python
print("Hello, Python!")
print("I am setting up my programming workspace.")
```

Save the file before you run it.

## Step 5: Run the File

Open your terminal in the folder where `hello.py` is saved.

Command:

```bash
python hello.py
```

If your computer uses a different Python command, use the one that worked in Step 1.

Command:

```bash
py hello.py
```

Command:

```bash
python3 hello.py
```

Expected output:

```text
Hello, Python!
I am setting up my programming workspace.
```

You wrote a file, saved it, ran it, and read the result. That is the basic programming loop.

## What Just Happened

This line tells Python to display text on the screen.

Runnable example:

```python
print("Hello, Python!")
```

In programming, `print` usually means:

```text
Show this on the screen.
```

The text inside quotation marks is called a string.

Runnable example:

```python
"Hello, Python!"
```

Runnable example:

```python
"I am learning step by step."
```

> Key idea: Quotation marks tell Python where a piece of text starts and ends.

You will learn strings in more detail later. For today, it is enough to know that text values need quotation marks.

## Try It Yourself

Change `day-02/hello.py` so it prints three lines.

Runnable example:

```python
print("My name is Sam.")
print("Today I ran my first Python file.")
print("I am learning one step at a time.")
```

Use your own name or a made-up name.

Run the file again.

Command:

```bash
python hello.py
```

Practice this loop:

1. edit the file
2. save the file
3. run the file
4. read the output
5. fix anything that looks wrong

## Common Mistake

### Mistake: Forgetting to save the file

Beginners often change the code, run the program, and wonder why the output did not change.

The usual reason is simple.

```text
The file was not saved.
```

Before you run a program, save the file.

> Checkpoint: If your output does not match your code, save the file and run it again before changing anything else.

## Debug It

Broken by design:

```python
print("Hello, Python!)
```

What is wrong?

The string starts with a quotation mark, but it does not end with one.

Fixed version:

```python
print("Hello, Python!")
```

Broken by design:

```python
prin("Hello, Python!")
```

What is wrong?

The command should be `print`, not `prin`.

Fixed version:

```python
print("Hello, Python!")
```

Most early errors are small:

- missing quotation marks
- missing parentheses
- misspelled words
- using uppercase when Python expects lowercase
- running the file from the wrong folder
- forgetting to save

Small errors are normal when you are learning the exactness of code.

## Read the Docs

Look up Python's official documentation for `print`.

Do not try to understand the whole page today. Your task is only to notice three things:

- `print` is a built-in function
- official documentation can look dense at first
- you can still learn one useful detail from a dense page

Documentation is not a novel. Use it like a reference.

Today, find `print`, read one small piece, and move on.

## Mini Challenge

Create a file named `about_me.py` inside `day-02/`.

File path:

```text
day-02/about_me.py
```

Write a program that prints five lines about you.

Runnable example:

```python
print("My name is Asha.")
print("I am learning Python.")
print("I like solving problems.")
print("Today I created my first Python file.")
print("Tomorrow I will write my first small program.")
```

Run the file from the terminal.

Command:

```bash
python about_me.py
```

If it works, change one line, save the file, and run it again.

## Real-World Use

Every Python project starts with setup.

Professional programmers still:

- install tools
- check versions
- create folders
- run small test files
- fix setup problems
- verify that the project runs before adding more code

Setup is normal engineering work. The more often you do it, the easier it becomes to recognize what is working and what needs attention.

## Recap

Today you learned that:

- Python must be installed before your computer can run Python code
- the terminal lets you type commands
- a `.py` file is a Python file
- `print()` shows text on the screen
- quotation marks mark text strings
- saving before running matters
- setup problems are common and fixable

Main idea:

```text
A working setup turns code in a file into instructions your computer can run.
```

## Exercises

### Exercise 1

Check your Python version.

Write down the command that worked on your computer.

Command options:

```text
python --version
py --version
python3 --version
```

### Exercise 2

Create a file named `favorite_things.py` inside `day-02/`.

Make it print three things you like.

### Exercise 3

Create a file named `future_goal.py` inside `day-02/`.

Make it print one sentence about something you may want to build with Python.

### Exercise 4

Fix this code.

Broken by design:

```python
print("I am learning Python"
```

### Exercise 5

Fix this code.

Broken by design:

```python
Print("Python is working!")
```

Hint:

```text
Python cares about uppercase and lowercase letters.
```

## Lesson Checklist

Before you finish, confirm that you can:

- open a terminal
- check your Python version
- create a `day-02/` folder
- save a file named `hello.py`
- run `hello.py` from the terminal
- explain what `print()` does
- fix a missing quotation mark
- save changes before running a file again

## Tiny Win

Yesterday, you learned that programming means writing careful instructions.

Today, you prepared a place where your computer can follow those instructions.

## Tomorrow

Tomorrow, you will write your first small program and start using Python more directly.
