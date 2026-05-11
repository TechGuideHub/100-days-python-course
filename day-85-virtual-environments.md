# Day 85: Virtual Environments

**Focus:** Keeping each Python project in its own environment  
**You will practice:** `venv`, `python -m venv .venv`, activating on Windows, macOS, and Linux, using `python -m pip`, installing packages, writing `requirements.txt`, installing from `requirements.txt`, and leaving an environment with `deactivate`  
**Estimated time:** 50-65 minutes

## Today's Goal

Today you will learn how to give each Python project its own small workspace.

That workspace is called a virtual environment.

By the end of today, you should be able to:

- explain what a virtual environment is
- explain why one environment per project is a good habit
- create an environment with `python -m venv .venv`
- activate it on Windows, macOS, or Linux
- notice when an environment is active
- install packages with `python -m pip`
- save installed package names in `requirements.txt`
- install packages from `requirements.txt`
- leave the environment with `deactivate`
- recognize common environment mistakes
- prepare for Day 86, where you will return to lists and learn list comprehensions

This lesson is not about writing clever Python code.

It is about setting up a clean place where your code can run.

## The Big Idea

A virtual environment is a project-specific Python setup.

It gives one project its own:

- Python command
- package installer
- folder for installed packages

The standard library module that creates it is named `venv`.

The command is:

```text
python -m venv .venv
```

That means:

```text
Use the Python I am running now.
Run its venv module.
Create a virtual environment named .venv.
```

The `.venv` folder usually lives inside your project folder:

```text
day-85/
  .venv/
  main.py
  requirements.txt
```

You normally do not edit files inside `.venv` by hand.

You use commands to create it, activate it, install packages into it, and leave it.

### Why This Matters

Without virtual environments, packages can pile up in one shared Python installation.

That can create problems like:

```text
Project A needs package version 1.
Project B needs package version 2.
Both projects are using the same shared package folder.
Now one project can break the other.
```

A per-project environment avoids that mess.

Each project gets its own package folder:

```text
project-a/
  .venv/
  requirements.txt

project-b/
  .venv/
  requirements.txt
```

Now Project A can install what it needs.

Project B can install what it needs.

They do not have to agree.

That is the main value of virtual environments: they keep project dependencies separate.

## The Mental Model

Think of your computer as having a main Python installation.

That main Python can create smaller project environments.

```text
main Python
  |
  | python -m venv .venv
  v
project folder
  .venv/
    project Python
    project pip
    project packages
```

When the environment is not active, your terminal may use your normal Python.

When the environment is active, your terminal uses the Python inside `.venv`.

You may see the environment name at the start of the prompt:

```text
(.venv)
```

The prompt is a hint, not the whole truth.

The best habit is to run package commands through the Python you mean:

```text
python -m pip
```

This says:

```text
Use pip that belongs to this Python.
```

That is clearer than running `pip` by itself, especially when a computer has more than one Python installed.

## Create And Activate An Environment

Start inside your project folder.

For this lesson, create a folder named:

```text
day-85
```

Then move into it before creating the environment.

The environment command is the same idea on every operating system:

```text
python -m venv .venv
```

This creates a folder named:

```text
.venv
```

The activation command depends on your terminal.

### Windows PowerShell

Use:

```text
.\.venv\Scripts\Activate.ps1
```

After activation, your prompt may begin with:

```text
(.venv)
```

If PowerShell says scripts are disabled, see the debugging section later in this lesson.

### Windows Command Prompt

Use:

```text
.venv\Scripts\activate.bat
```

After activation, your prompt may begin with:

```text
(.venv)
```

### macOS Or Linux

Use:

```text
source .venv/bin/activate
```

After activation, your prompt may begin with:

```text
(.venv)
```

### If Your Computer Uses python3

This course writes commands with `python`.

Some macOS and Linux setups use `python3` instead.

If `python` is not found, use the same pattern with `python3`:

```text
python3 -m venv .venv
python3 -m pip --version
```

Once the environment is active, `python` often works inside that terminal because the environment has adjusted the command search path.

## Try It Yourself

Work through this slowly.

Do not create the environment in a random folder. The location matters.

### Step 1: Create A Practice Folder

Create:

```text
day-85
```

Move into it.

Your project should look like this at first:

```text
day-85/
```

### Step 2: Create The Environment

Run:

```text
python -m venv .venv
```

Now the project should look like this:

```text
day-85/
  .venv/
```

The `.venv` folder may contain many files.

That is normal.

Do not write your Python scripts inside `.venv`.

Your own code should live beside it:

```text
day-85/
  .venv/
  main.py
```

### Step 3: Activate It

Choose the command for your terminal.

Windows PowerShell:

```text
.\.venv\Scripts\Activate.ps1
```

Windows Command Prompt:

```text
.venv\Scripts\activate.bat
```

macOS or Linux:

```text
source .venv/bin/activate
```

Look for:

```text
(.venv)
```

near the start of your prompt.

If you do not see it, do not panic. Some terminals show prompts differently.

Check with:

```text
python -m pip --version
```

The printed path should mention `.venv`.

### Step 4: Check Python And pip

Run:

```text
python --version
python -m pip --version
```

The exact version numbers will depend on your computer.

The important habit is this:

```text
python -m pip
```

That keeps pip connected to the Python you are currently using.

### Step 5: Install A Package

Install a small third-party package:

```text
python -m pip install rich
```

`rich` is a package for styled terminal output.

Now create this file:

```text
day-85/hello_rich.py
```

Add:

```python
from rich import print

print("[bold green]Virtual environment ready[/bold green]")
```

Run:

```text
python hello_rich.py
```

You should see:

```text
Virtual environment ready
```

Depending on your terminal, the text may be styled or colored.

The important part is that the import works.

### Step 6: See Installed Packages

Run:

```text
python -m pip list
```

You should see `rich` somewhere in the list.

You may also see packages that `rich` depends on.

That is normal. Some packages bring helpers with them.

### Step 7: Save requirements.txt

A virtual environment folder is not the thing you usually share with another person.

It can be large.

It also belongs to your machine.

Instead, projects usually share a package list.

Create that list with:

```text
python -m pip freeze > requirements.txt
```

Now the project should look like this:

```text
day-85/
  .venv/
  hello_rich.py
  requirements.txt
```

Open `requirements.txt`.

It should contain package names and version numbers, similar to:

```text
rich==...
```

The exact version number may be different when you run it.

### Step 8: Install From requirements.txt

On another computer, or in a fresh environment, the setup command would be:

```text
python -m pip install -r requirements.txt
```

That tells pip:

```text
Read the package list from requirements.txt.
Install those packages into the active environment.
```

This is why `requirements.txt` matters.

It gives someone else a repeatable setup step.

### Step 9: Leave The Environment

When you are done working in that terminal, run:

```text
deactivate
```

This does not delete `.venv`.

It only tells your current terminal to stop using it.

The next time you work on the project, activate it again.

## requirements.txt Basics

A `requirements.txt` file is a plain text list of packages.

Each package usually gets its own line.

Simple version:

```text
rich
requests
```

More specific version:

```text
rich==13.7.1
requests==2.31.0
```

The double equals sign means:

```text
Install exactly this version.
```

Exact versions make a project easier to reproduce.

Loose names make it easier to get newer versions.

For beginner projects, this command is a practical start:

```text
python -m pip freeze > requirements.txt
```

It records what is installed in the active environment.

Later, you can rebuild from that list:

```text
python -m pip install -r requirements.txt
```

Read that command as:

```text
Use this Python's pip.
Install from the requirements file.
```

That pattern is common in real projects.

## Common Mistake

One common mistake is creating the environment in the wrong folder.

If you meant to create:

```text
day-85/.venv
```

but you were one folder too high, you might end up with:

```text
.venv
day-85/
```

That is not what you wanted for this lesson.

Before running:

```text
python -m venv .venv
```

check that your terminal is inside the project folder.

Another common mistake is installing packages before activating the environment.

If you run:

```text
python -m pip install rich
```

while the wrong Python is active, the package goes into the wrong place.

That can lead to this confusing situation:

```text
pip says rich is installed.
python says No module named rich.
```

The fix is to use the same Python for both actions:

```text
python -m pip install rich
python hello_rich.py
```

A third mistake is committing or sharing the whole `.venv` folder.

In most projects, share:

```text
requirements.txt
```

Do not share:

```text
.venv/
```

The `.venv` folder is a local working folder.

The requirements file is the recipe for rebuilding it.

Another mistake is thinking `deactivate` removes the environment.

It does not.

This command:

```text
deactivate
```

only changes the current terminal session.

The `.venv` folder remains on disk until you delete it yourself.

## Debug It

Virtual environment problems are usually location problems.

Start by asking:

```text
Which folder am I in?
Which Python am I using?
Which environment is active?
Which package list did I install from?
```

### Problem 1: No module named rich

You run:

```text
python hello_rich.py
```

and see an error like:

```text
ModuleNotFoundError: No module named 'rich'
```

Check whether the environment is active.

Then run:

```text
python -m pip install rich
```

Try the script again:

```text
python hello_rich.py
```

If it still fails, check where pip is connected:

```text
python -m pip --version
```

The printed path should mention `.venv`.

### Problem 2: python Is Not Found

If this command fails:

```text
python -m venv .venv
```

try:

```text
python3 -m venv .venv
```

Then continue with the same activation command for your operating system.

After activation, check:

```text
python --version
python -m pip --version
```

If `python` still does not work, use `python3` consistently for that project.

### Problem 3: PowerShell Blocks Activation

On Windows PowerShell, you may see a message saying scripts are disabled.

That is a PowerShell policy issue, not a Python syntax issue.

One common current-user fix is:

```text
Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope CurrentUser
```

Then try activation again:

```text
.\.venv\Scripts\Activate.ps1
```

If you are on a managed school or work computer, you may not be allowed to change that setting.

In that case, use Windows Command Prompt with:

```text
.venv\Scripts\activate.bat
```

### Problem 4: requirements.txt Is Empty Or Strange

This command writes the packages from the active environment:

```text
python -m pip freeze > requirements.txt
```

If `requirements.txt` is empty, you may not have installed any third-party packages in that environment yet.

Install one:

```text
python -m pip install rich
```

Then run:

```text
python -m pip freeze > requirements.txt
```

again.

If `requirements.txt` contains a huge list, you may have used a Python environment that already had many packages installed.

For beginner projects, that is a clue to create a fresh `.venv` for the project.

### Problem 5: The Prompt Does Not Show (.venv)

Some terminals customize the prompt.

Do not rely only on the prompt.

Run:

```text
python -m pip --version
```

If the path mentions `.venv`, your package installer is using the virtual environment.

## Read the Docs

For today, read only enough documentation to answer practical setup questions.

Useful pages:

```text
https://docs.python.org/3/library/venv.html
https://packaging.python.org/en/latest/guides/installing-using-pip-and-virtual-environments/
https://pip.pypa.io/en/stable/user_guide/#requirements-files
```

Look for these ideas:

- `venv` creates virtual environments
- activation changes the shell so `python` and `pip` point at the environment
- `python -m pip` runs pip through a specific Python
- `requirements.txt` can be used with `python -m pip install -r requirements.txt`

You can also ask the tools themselves for help:

```text
python -m venv --help
python -m pip --help
```

Documentation is easier when your question is small.

For example:

```text
What command creates the environment?
What command activates it on my terminal?
What command installs from requirements.txt?
```

Those are enough for today.

## Mini Challenge

Create a tiny project setup note for your future self.

In your `day-85` folder, create:

```text
day-85/setup_notes.txt
```

Write the steps in your own words:

```text
1. Create the environment.
2. Activate it.
3. Install packages.
4. Save requirements.txt.
5. Deactivate when finished.
```

Under each step, add the exact command for your operating system.

Then answer these questions:

```text
Why should .venv stay local?
Why should requirements.txt be shared?
Why is python -m pip safer than pip by itself?
```

This is not busywork.

You are building your own checklist for the next time a project needs packages.

## Real-World Use

Most serious Python projects use some kind of project environment.

A web app may need:

```text
flask
python-dotenv
requests
```

A data project may need:

```text
pandas
matplotlib
jupyter
```

A command-line tool may need:

```text
rich
click
```

Those package lists should not all be mixed into one shared Python.

Each project should have its own environment and its own setup instructions.

A typical project might include:

```text
my-tool/
  .venv/
  main.py
  helpers.py
  requirements.txt
```

The `.venv` folder lets you run the project on your machine.

The `requirements.txt` file helps someone else prepare the same kind of environment.

That is why virtual environments are not just a setup detail.

They are part of making projects portable.

## Recap

Today you learned that a virtual environment is a separate Python workspace for one project.

The creation command is:

```text
python -m venv .venv
```

Activation depends on your terminal.

Windows PowerShell:

```text
.\.venv\Scripts\Activate.ps1
```

Windows Command Prompt:

```text
.venv\Scripts\activate.bat
```

macOS or Linux:

```text
source .venv/bin/activate
```

Install packages with:

```text
python -m pip install package_name
```

Save the active environment's package list with:

```text
python -m pip freeze > requirements.txt
```

Install from that list with:

```text
python -m pip install -r requirements.txt
```

Leave the environment with:

```text
deactivate
```

The main habit is:

```text
One project, one environment, one requirements file.
```

That habit keeps projects easier to run and easier to share.

## Lesson Checklist

Before moving on, make sure you can:

- explain what `.venv` is
- explain why projects should not all share one package folder
- create a virtual environment with `python -m venv .venv`
- activate the environment for your terminal
- check package tools with `python -m pip --version`
- install a package with `python -m pip install`
- run a script that imports an installed package
- save installed packages to `requirements.txt`
- install packages from `requirements.txt`
- explain why `.venv` is local but `requirements.txt` is useful to share
- leave the environment with `deactivate`

## Exercises

### Exercise 1: Explain The Problem

Write three sentences:

```text
What problem does a virtual environment solve?
Why can different projects need different packages?
Why is .venv usually kept inside the project folder?
```

Keep the answer practical.

Imagine you are explaining it to someone who has only written single-file Python scripts so far.

### Exercise 2: Create And Activate

Create:

```text
day-85
```

Inside it, create:

```text
.venv
```

with:

```text
python -m venv .venv
```

Activate it using the command for your terminal.

Then run:

```text
python --version
python -m pip --version
```

Write down whether the pip path mentions `.venv`.

### Exercise 3: Install And Import

With the environment active, run:

```text
python -m pip install rich
```

Create:

```text
day-85/check_rich.py
```

Add:

```python
from rich import print

print("[bold]Rich is installed.[/bold]")
```

Run:

```text
python check_rich.py
```

If the import works, the environment is doing its job.

### Exercise 4: Save requirements.txt

With the environment active, run:

```text
python -m pip freeze > requirements.txt
```

Open:

```text
day-85/requirements.txt
```

Find the line for `rich`.

Then answer:

```text
Why is this file easier to share than the whole .venv folder?
```

### Exercise 5: Read A requirements.txt

Read this file:

```text
rich==13.7.1
requests==2.31.0
```

Answer:

```text
How many packages are listed?
What does == mean?
What command installs from this file?
```

The install command is:

```text
python -m pip install -r requirements.txt
```

### Exercise 6: Spot The Mistake

Read this project layout:

```text
day-85/
  main.py

.venv/
```

The learner meant the environment to belong to `day-85`.

What probably happened?

Write one sentence.

Then write the better layout:

```text
day-85/
  .venv/
  main.py
```

### Exercise 7: Debug The Missing Package

Suppose this script fails:

```python
import rich

print("Ready")
```

The error says:

```text
ModuleNotFoundError: No module named 'rich'
```

Write the three commands you would try first:

```text
python -m pip --version
python -m pip install rich
python script_name.py
```

Then explain why the first command is useful.

### Exercise 8: Practice Deactivation

Activate your environment.

Run:

```text
python -m pip --version
```

Then run:

```text
deactivate
```

Now answer:

```text
Did deactivate delete .venv?
What did it change?
What will you need to do next time you return to this project?
```

## Tiny Win

You can now set up a Python project without mixing its packages into every other project.

That is a practical professional habit.

It may feel like setup work, but it protects your future programs from strange package conflicts.

Clean environments make debugging calmer.

## Tomorrow

Tomorrow is:

```text
Day 86: List Comprehensions
```

You will return to core Python syntax and learn a compact way to build a new list from an existing list.

The setup habit from today still matters.

From now on, some projects may need outside packages, and virtual environments give those packages a clear home.
