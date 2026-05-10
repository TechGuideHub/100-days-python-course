# Day 02: Setting Up Python

**Focus:** Install or confirm Python, create a course folder, and run a small `.py` file.  
**You will practice:** checking versions, using the terminal, saving a file, running a script, and reading output.  
**Estimated time:** 35-50 minutes

## Today's Goal

Today you will get Python ready and run one small file from your own folder.

By the end of this lesson, you should be able to:

- check whether Python is installed
- open a terminal
- run a simple command
- create a small Python file
- run that file and compare the output with what you expected

This is not busywork. If you can create a file, run it, and understand the output, you have the basic loop you will use for the rest of the course.

## The Big Idea

Python code does not run by itself. Your computer needs the Python program installed so it can read your `.py` files and execute the instructions inside them.

Code:

```python
print("Hello, Python!")
```

You should see:

```text
Hello, Python!
```

Python is the tool that reads your Python code and runs it. Today's job is simply to make sure that tool works on your computer.

## The Mental Model

Think of setup as getting a small workbench ready.

- Python runs your code.
- Your code editor is where you write and save code.
- The terminal is where you type commands.
- A `.py` file is a saved Python program.

Once those pieces are connected, the workflow is:

```text
write code -> save the file -> run the file -> read the output
```

You will repeat that loop constantly, so it is worth making it comfortable now.

## What You Need

For this course, you need three things:

1. Python
2. A code editor
3. A terminal

### Python

Python runs your programs. Use Python 3 for this course.

### Code Editor

A code editor is where you write and save code. Beginner-friendly options include:

- Visual Studio Code
- PyCharm Community Edition
- Thonny

Use the editor your course, school, or computer already supports. Today is not about choosing the perfect editor. It is about getting one file to run.

### Terminal

The terminal is where you type commands.

Depending on your computer, it may be called Terminal, PowerShell, Command Prompt, or something similar.

You do not need to master it today. You only need a few short commands.

## Step 1: Check Whether Python Is Installed

Open a terminal and try:

```bash
python --version
```

You should see something like:

```text
Python 3.x.x
```

If that works, Python is installed.

If it does not work, try these:

```bash
py --version
```

```bash
python3 --version
```

Different computers use different command names. You only need one of them to show a Python 3 version.

## Step 2: Install Python If Needed

If none of the version commands work, install Python from the official Python website or from the method recommended by your course or school.

During installation, you may see this option:

```text
Add Python to PATH
```

Turn it on if you see it. It helps your terminal find Python later.

After installing Python, close the terminal, open it again, and check the version once more:

```bash
python --version
```

If that command is not the one your computer uses, try:

```bash
py --version
```

or:

```bash
python3 --version
```

Before moving on, make sure one command shows a Python 3 version.

## Step 3: Create a Course Folder

Create a folder for your Python work:

```text
python-lessons
```

Inside it, create another folder for today:

```text
day-02/
```

Keeping files organized saves future frustration. You will be able to find your work, rerun examples, and continue tomorrow without hunting around.

## Step 4: Create Your First Python File

Open your code editor.

Create a new file and save it here:

```text
day-02/hello.py
```

The `.py` ending tells your editor and your computer that this is a Python file.

Code:

```python
print("Hello, Python!")
print("I am setting up my programming workspace.")
```

Save the file before you run it.

## Step 5: Run the File

Open your terminal in the folder where `hello.py` is saved.

Run it:

```bash
python hello.py
```

If your computer uses a different Python command, use the one that worked in Step 1:

```bash
py hello.py
```

```bash
python3 hello.py
```

You should see:

```text
Hello, Python!
I am setting up my programming workspace.
```

You wrote a file, saved it, ran it, and read the result. That is the basic programming loop.

## What Just Happened

This line tells Python to display text on the screen.

Code:

```python
print("Hello, Python!")
```

In programming, `print` usually means:

```text
Show this on the screen.
```

The text inside quotation marks is called a string.

Here are two strings:

```python
"Hello, Python!"
```

```python
"I am learning step by step."
```

Quotation marks tell Python where a piece of text starts and ends.

You will learn strings in more detail later. For today, it is enough to know that text values need quotation marks.

## Try It Yourself

Change `day-02/hello.py` so it prints three lines.

Code:

```python
print("My name is Sam.")
print("Today I ran my first Python file.")
print("I am learning one step at a time.")
```

Use your own name or a made-up name.

Run the file again.

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

The usual reason is simple:

```text
The file was not saved.
```

Before you run a program, save the file.

If your output does not match your code, save the file and run it again before changing anything else.

## Debug It

Broken code:

```python
print("Hello, Python!)
```

What is wrong?

The string starts with a quotation mark, but it does not end with one.

Fixed code:

```python
print("Hello, Python!")
```

Broken code:

```python
prin("Hello, Python!")
```

What is wrong?

The command should be `print`, not `prin`.

Fixed code:

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

Do not try to understand the whole page today. Just notice three things:

- `print` is a built-in function
- official documentation can look dense at first
- you can still learn one useful detail from a dense page

Documentation is not a novel. Use it like a reference.

Find `print`, read one small piece, and move on.

## Mini Challenge

Create a file named `about_me.py` inside `day-02/`.

Save it here:

```text
day-02/about_me.py
```

Write a program that prints five lines about you.

Code:

```python
print("My name is Asha.")
print("I am learning Python.")
print("I like solving problems.")
print("Today I created my first Python file.")
print("Tomorrow I will write my first small program.")
```

Run the file from the terminal.

```bash
python about_me.py
```

If it works, change one line, save the file, and run it again.

## Real-World Use

Every Python project starts with setup.

Even experienced programmers still:

- install tools
- check versions
- create folders
- run small test files
- fix setup problems
- verify that the project runs before adding more code

Setup is normal engineering work. The more often you do it, the faster you recognize what is working and what needs attention.

## Recap

Today you learned that:

- Python must be installed before your computer can run Python code
- the terminal lets you type commands
- a `.py` file is a Python file
- `print()` shows text on the screen
- quotation marks mark text strings
- saving before running matters
- setup problems are common and fixable

The main idea:

```text
A working setup turns code in a file into instructions your computer can run.
```

## Exercises

### Exercise 1

Check your Python version.

Write down the command that worked on your computer.

Try these if you need them:

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

Broken code:

```python
print("I am learning Python"
```

### Exercise 5

Fix this code.

Broken code:

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
