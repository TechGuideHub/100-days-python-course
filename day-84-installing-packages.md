# Day 84: Installing Packages

**Focus:** Adding third-party Python tools to a project safely  
**You will practice:** understanding third-party packages, PyPI, `pip`, `python -m pip`, activating a project environment, installing a small package, checking installed packages, and avoiding global installs  
**Estimated time:** 45-60 minutes

## Today's Goal

Today you will learn how Python projects use code written by other people.

Python already comes with a standard library. You used that in recent lessons with modules like `json`, `pathlib`, `random`, and `urllib`.

But Python programmers also use third-party packages.

A third-party package is code that does not come built into Python and was not written inside your own project. It is installed into your project so your program can import it.

By the end of today, you should be able to:

- explain what a third-party package is
- explain what PyPI is
- use `pip` as Python's package installer
- prefer `python -m pip` when installing packages
- explain why packages should go inside a project environment
- activate a project environment before installing
- read a simple install command without being intimidated
- check whether a package is installed
- understand how this prepares you for Day 85 on virtual environments

The goal is not to collect packages.

The goal is to install carefully, understand where the package goes, and keep each project tidy.

## The Big Idea

Python can use code from three main places:

```text
1. Your own files
2. The Python standard library
3. Third-party packages
```

You already know the first two.

Your own file might look like this:

```text
day-84/text_tools.py
```

The standard library might look like this:

```python
import json
from pathlib import Path
```

A third-party package might look like this:

```python
import rich
```

The difference is that `rich` does not come with Python by default.

Before your program can import it, the package must be installed.

That is where `pip` comes in.

`pip` is Python's package installer.

It can download a package and put it into the Python environment your project is using.

Most packages come from PyPI, which stands for the Python Package Index.

Think of PyPI as a public catalog of Python packages.

You do not copy code from PyPI by hand. Usually you ask `pip` to install a package by name.

For example:

```text
python -m pip install rich
```

That command means:

```text
Use this Python interpreter.
Run its pip module.
Install the package named rich.
```

The package name in the install command is usually the name shown on PyPI.

After installation, your Python code can import the package:

```python
import rich
```

Installing is a setup step.

Importing is a coding step.

Do not mix those up.

## The Mental Model

Imagine a project as a small workshop.

Your Python files are the work you are building.

The standard library is a shelf of tools that came with the workshop.

Third-party packages are extra tools you bring in when you need them.

The important question is:

```text
Where did I put the extra tool?
```

If you install packages globally, they may end up in the main Python installation on your computer.

That can cause problems:

- two projects may need different versions of the same package
- old practice packages can pile up
- a program may work on your computer but fail somewhere else
- it becomes harder to know what a project really depends on

The cleaner habit is to use a project environment.

A project environment is a private place for one project's installed packages.

In this course, you may see a project environment named:

```text
.venv
```

That name is common, but the idea matters more than the name.

When the environment is active, package commands affect the project environment instead of your whole computer.

The safe rhythm is:

```text
1. Go to the project folder.
2. Activate the project environment.
3. Install the package with python -m pip.
4. Import the package in your Python file.
5. Keep a note of what the project needs.
```

Day 85 will focus on creating and understanding virtual environments.

Today, you only need the habit:

```text
Activate the project environment before installing packages.
```

## Example

Suppose you want to use a package named `rich` to print styled terminal text.

First, activate your project environment.

On Windows PowerShell, the command usually looks like this:

```text
.venv\Scripts\Activate.ps1
```

On macOS or Linux, the command usually looks like this:

```text
source .venv/bin/activate
```

After the environment is active, install the package:

```text
python -m pip install rich
```

Then create a small file:

```text
day-84/rich_demo.py
```

Code:

```python
from rich import print

print("[bold green]Package install worked.[/bold green]")
print("This line was printed using a third-party package.")
```

Run it:

```text
python day-84/rich_demo.py
```

If `rich` is installed in the active environment, the program should print styled terminal text.

If it is not installed, Python will raise an error like:

```text
ModuleNotFoundError: No module named 'rich'
```

That error does not mean your Python syntax is bad.

It usually means Python cannot find the package in the environment it is using.

## Try It Yourself

Today is mostly about reading package commands and understanding what they do.

You do not need to install anything just to read this lesson.

If you do practice the commands, use a project environment first.

### Step 1: Check Pip

Run:

```text
python -m pip --version
```

You should see a line that includes:

```text
pip
```

It will also show the Python version or location that `pip` belongs to.

The exact text depends on your computer.

The useful question is:

```text
Does this pip belong to the Python I am using for this project?
```

That is one reason `python -m pip` is helpful.

It ties `pip` to the same `python` command.

### Step 2: Activate The Project Environment

Before installing, activate the environment for the current project.

Windows PowerShell:

```text
.venv\Scripts\Activate.ps1
```

macOS or Linux:

```text
source .venv/bin/activate
```

After activation, many terminals show the environment name near the prompt.

You might see something like:

```text
(.venv)
```

The prompt style is different on different systems, so do not worry if it does not look exactly the same.

### Step 3: Install One Small Package

With the project environment active, a package install command has this shape:

```text
python -m pip install rich
```

Read it from left to right:

```text
python        use Python
-m pip        run the pip module
install       install something
rich          package name
```

The package name goes at the end.

### Step 4: Check The Package

After installing, you can ask `pip` for information about the package:

```text
python -m pip show rich
```

You can also list installed packages:

```text
python -m pip list
```

That second command can show many packages.

Do not try to memorize the list.

Use it to answer a specific question:

```text
Is the package I need installed in this environment?
```

### Step 5: Import The Package

Create:

```text
day-84/package_check.py
```

Code:

```python
import rich

print("rich imported successfully")
```

Run:

```text
python day-84/package_check.py
```

If the package is installed in the active environment, the import should work.

If Python says the module is missing, check these things:

- did you activate the project environment?
- did you install the package in that same environment?
- are you running the file with the same `python` command?
- did you spell the package or import name correctly?

The fix is often about the environment, not the code.

## Common Mistake

A common beginner mistake is installing a package with one Python and running code with another Python.

For example, a learner might run:

```text
pip install rich
```

Then run:

```text
python day-84/package_check.py
```

If `pip` and `python` point to different Python installations, the program may still fail.

That is why this course prefers:

```text
python -m pip install rich
```

This asks the current `python` command to run its own `pip`.

Another common mistake is installing packages globally because it feels quick.

Try not to use commands like this as your normal habit:

```text
pip install rich
```

And avoid forcing a package into your main Python installation unless you clearly understand why you are doing it.

Project environments keep practice work contained.

They make mistakes easier to clean up.

## Debug It

Read this situation.

The learner activates a project environment and installs `rich`:

```text
python -m pip install rich
```

Then this file fails:

```text
day-84/main.py
```

Code:

```python
import Rich

print("Ready")
```

The problem is capitalization.

Python imports are case-sensitive.

The import should be:

```python
import rich

print("Ready")
```

Here is another situation.

The learner installs a package, but the program still says:

```text
ModuleNotFoundError: No module named 'rich'
```

Use this checklist:

- run `python -m pip --version`
- run `python -m pip show rich`
- confirm the project environment is active
- run the Python file from the same project
- check the spelling of the import

If `python -m pip show rich` says the package is not found, install it in the active environment.

If `pip show` finds the package but Python still cannot import it, you are probably using two different Python commands or environments.

## Read the Docs

When you use a third-party package, read a little before you install it.

For a package on PyPI, look for:

- the package name
- the install command
- the basic import example
- the project description
- the supported Python versions
- the release history
- the link to documentation or source code

You do not need to become an expert before installing a small practice package.

But do not install random packages blindly.

Good questions to ask:

```text
What problem does this package solve?
How do I install it?
What import name does it use?
Is it still maintained?
Does it have a simple first example?
```

Some packages have different install and import names.

For example, a package might be installed with one name but imported with another.

The package documentation should tell you.

If an import fails after installation, check the documentation for the exact import line.

## Mini Challenge

Choose one package you have heard about or seen in code.

Do not install it yet.

Write a short note in:

```text
day-84/package_notes.md
```

Answer these questions:

```text
Package name:
What it helps with:
Install command:
Import line:
One tiny example:
Would I use this in a beginner project? Why or why not?
```

For example:

```text
Package name: rich
What it helps with: styled terminal output
Install command: python -m pip install rich
Import line: from rich import print
One tiny example: print("[bold]Hello[/bold]")
Would I use this in a beginner project? Yes, if terminal output needs to be easier to read.
```

This challenge is about research and judgment.

Installing a package is easy.

Choosing a package thoughtfully is the real skill.

## Real-World Use

Third-party packages are one reason Python is so useful.

Real projects use packages for work such as:

- making HTTP requests
- building web apps
- reading spreadsheets
- creating charts
- testing code
- formatting terminal output
- working with images
- connecting to databases
- building command-line tools

For example, a later project might use a package to create cleaner terminal output.

The code might start like this:

```python
from rich.console import Console

console = Console()
console.print("Inventory updated", style="green")
```

That import only works if the package is installed in the environment running the project.

This is why project setup matters.

The code and the environment belong together.

When someone shares a Python project, they usually need to share two kinds of information:

```text
1. The project files
2. The packages needed to run those files
```

You will learn more about tracking those packages as your projects grow.

For now, remember:

```text
If a program imports a third-party package, the environment must have that package installed.
```

## Recap

Today you learned that third-party packages are extra Python tools installed into a project.

You learned these terms:

- PyPI is a public catalog of Python packages.
- `pip` is Python's package installer.
- `python -m pip` runs `pip` through the Python interpreter you are using.
- A project environment keeps installed packages separate from your main Python installation.

You also learned the basic workflow:

```text
activate the project environment
python -m pip install package-name
import the package in Python code
run the program with the same Python environment
```

And you learned a useful debugging clue:

```text
ModuleNotFoundError often means Python cannot find the package in the current environment.
```

That is different from a syntax error.

It is usually a setup problem.

## Lesson Checklist

Before moving on, make sure you can:

- [ ] explain what a third-party package is
- [ ] explain what PyPI is
- [ ] explain what `pip` does
- [ ] run or read `python -m pip --version`
- [ ] explain why `python -m pip` is clearer than plain `pip`
- [ ] activate a project environment before installing
- [ ] read an install command like `python -m pip install rich`
- [ ] check a package with `python -m pip show package-name`
- [ ] explain why global installs can cause confusion
- [ ] recognize `ModuleNotFoundError` as a possible environment issue

## Exercises

### Exercise 1: Label The Source

For each import, write whether it is likely from your project, the standard library, or a third-party package.

```python
import json
import text_tools
import rich
from pathlib import Path
import requests
```

Possible answers:

```text
json: standard library
text_tools: your project, if you created text_tools.py
rich: third-party package
pathlib: standard library
requests: third-party package
```

### Exercise 2: Read The Command

Explain this command in one sentence:

```text
python -m pip install rich
```

Your answer should mention:

- Python
- pip
- installing
- the package name

### Exercise 3: Fix The Install Habit

Rewrite this command in the style used by this course:

```text
pip install rich
```

Answer:

```text
python -m pip install rich
```

Then write one sentence explaining why the rewritten version is clearer.

### Exercise 4: Check Before Importing

Write the command that checks whether `rich` is installed:

```text
python -m pip show rich
```

Then write the command that lists installed packages:

```text
python -m pip list
```

Which command is better when you only care about one package?

### Exercise 5: Spot The Missing Step

Read this workflow:

```text
1. Open the project folder.
2. Run python -m pip install rich.
3. Run python day-84/main.py.
```

What step is missing?

Answer:

```text
Activate the project environment before installing.
```

### Exercise 6: Fix The Import

This file fails:

```python
import Rich

print("Ready")
```

Fix the capitalization:

```python
import rich

print("Ready")
```

### Exercise 7: Read A Package Page

Choose a package page on PyPI.

Find these details:

- package name
- install command
- import line
- one sentence about what it does
- one example from the documentation

Write your notes in:

```text
day-84/package_notes.md
```

Use your own words.

### Exercise 8: Explain The Error

Read this error:

```text
ModuleNotFoundError: No module named 'rich'
```

Write two possible causes:

```text
1. The package was not installed.
2. The package was installed in a different Python environment.
```

Then write one command that helps investigate:

```text
python -m pip show rich
```

### Exercise 9: Compare Built-In And Installed Tools

Write a short comparison:

```text
json does not need installation because it is in the standard library.
rich needs installation because it is a third-party package.
```

Then add one more pair of examples:

```text
pathlib: standard library
requests: third-party package
```

### Exercise 10: Prepare For Day 85

Answer these questions in your own words:

```text
Why should one project have its own environment?
What could go wrong if every project shared the same installed packages?
Why is activation part of the setup habit?
```

Keep the answers short.

Tomorrow will make the environment idea much clearer.

## Tiny Win

You now know what happens before a third-party import works.

That matters.

Many beginners see `ModuleNotFoundError` and think the program itself is mysterious.

Now you can separate the questions:

```text
Is the code written correctly?
Is the package installed?
Is it installed in the environment this project is using?
```

That is a practical debugging skill.

## Tomorrow

Tomorrow is:

```text
Day 85: Virtual Environments
```

Today you used the idea of an active project environment.

Tomorrow you will slow down and look directly at what virtual environments are, why they exist, how to create one, how to activate one, and how they keep projects from stepping on each other.
