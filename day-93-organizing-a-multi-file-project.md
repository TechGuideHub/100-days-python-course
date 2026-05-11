# Day 93: Organizing a Multi-File Project

**Focus:** Turning a growing Python program into a clear project folder  
**You will practice:** folder layout, `main.py`, helper modules, a `data` folder, `README.md`, `requirements.txt`, separating logic from interface code, imports between your own files, naming files clearly, and avoiding giant files  
**Estimated time:** 60-75 minutes

## Today's Goal

Today you will learn how to organize a Python project that has more than one file.

Earlier in the course, one file was usually enough.

That was a good starting point. A small script is easier to understand when everything is visible in one place.

But real projects grow.

They collect:

- functions
- saved data
- setup notes
- imports
- small helper files
- maybe a few third-party packages

If all of that lives in one file, the program becomes harder to read and harder to change.

By the end of today, you should be able to:

- sketch a simple project folder layout
- explain why many projects have a `main.py` file
- move reusable logic into helper modules
- keep saved files in a `data` folder
- write a small `README.md`
- explain what belongs in `requirements.txt`
- separate program logic from user interface code
- import functions from nearby files
- choose file names that do not fight Python imports
- recognize when a file is becoming too large
- prepare for Day 94, where you will save project progress with Git and GitHub

The goal is not to make a complicated folder.

The goal is to make every important part of the project easy to find.

## The Big Idea

A project is a folder with a job.

Inside that folder, each file should also have a job.

Here is a small inventory project:

```text
day-93/
  main.py
  inventory.py
  display.py
  storage.py
  data/
    inventory.json
  README.md
  requirements.txt
```

That looks like more work than one file, but the names tell you where things belong.

```text
main.py              starts the program
inventory.py         handles inventory rules
display.py           prints information for the user
storage.py           reads and writes saved data
data/                stores files the program uses
README.md            explains the project to a person
requirements.txt     lists third-party packages, if any
```

This is not the only correct layout.

It is a beginner-friendly layout because it answers a simple question:

```text
Where should this code go?
```

If the code starts the app, put it in `main.py`.

If it changes inventory data, put it in `inventory.py`.

If it prints messages, put it in `display.py`.

If it saves or loads files, put it in `storage.py`.

If it is saved data, put it under `data/`.

If it explains how to run the project, put it in `README.md`.

If it lists installed third-party packages, put it in `requirements.txt`.

## The Mental Model

Think of `main.py` as the front desk.

It does not need to do every job itself.

It should know who to ask.

```text
main.py
  |
  | asks inventory.py to update item counts
  | asks storage.py to load and save data
  | asks display.py to show results
  v
program runs as one project
```

Each helper module is a small workplace.

```text
inventory.py
  logic about inventory

storage.py
  logic about files

display.py
  logic about printed output
```

The files work together through imports.

For example, `main.py` can import the other project files:

```python
import display
import inventory
import storage
```

Those imports mean:

```text
Let main.py use names from display.py, inventory.py, and storage.py.
```

This is the same import idea you learned earlier, but now the whole folder matters.

The project folder is the home base.

## Start With A Tree

Before writing a larger project, draw the folder tree first.

It does not need to be fancy.

For today's practice, use this:

```text
day-93/
  main.py
  inventory.py
  display.py
  storage.py
  data/
    inventory.json
  README.md
  requirements.txt
```

A tree helps you think before you type.

It also helps you notice missing pieces.

For example:

- Where will the saved data live?
- Which file starts the program?
- Which file holds reusable functions?
- How will another person know how to run it?
- Does the project use any third-party packages?

Those questions are easier to answer before a file becomes 300 lines long.

### Keep The Tree Boring

Good project layouts are often boring.

That is a compliment.

Use names that a tired future version of you can understand quickly.

Good beginner names:

```text
main.py
inventory.py
storage.py
display.py
data/
README.md
requirements.txt
```

Risky names:

```text
stuff.py
things.py
helpers2.py
final_final.py
mycode.py
json.py
random.py
```

The risky names are risky for different reasons.

`stuff.py` and `things.py` do not explain what belongs inside.

`helpers2.py` is a sign that the first helper file may already be too vague.

`final_final.py` usually means the project needs better version history. You will start learning that tomorrow.

`json.py` and `random.py` are dangerous because Python already has standard library modules with those names.

If you create your own `json.py`, then this line may import your file instead of the standard library module:

```python
import json
```

That can create very confusing bugs.

## `main.py`

Many Python projects have one file that starts the program.

In this course, call that file:

```text
day-93/main.py
```

`main.py` is a clear name because it tells the reader:

```text
Start here.
```

For a beginner project, `main.py` often does these jobs:

- imports helper modules
- loads starting data
- asks for user input
- calls functions from other files
- prints or displays final results
- saves data before the program ends

It should not usually contain every function in the whole project.

Compare these two layouts.

All-in-one layout:

```text
day-93/
  main.py
```

More organized layout:

```text
day-93/
  main.py
  inventory.py
  display.py
  storage.py
```

The organized layout gives each file a smaller job.

When a bug appears, you have fewer places to search.

## Helper Modules

A helper module is just another Python file.

You use it to hold code that supports the main program.

In this project, `inventory.py` will hold inventory logic.

Create:

```text
day-93/inventory.py
```

Code:

```python
def add_stock(items, name, amount):
    current = items.get(name, 0)
    items[name] = current + amount
    return items


def get_low_stock_items(items, limit):
    low_stock = {}

    for name, count in items.items():
        if count <= limit:
            low_stock[name] = count

    return low_stock
```

This file does not ask for input.

It does not print.

It does not read a file.

It only handles inventory rules:

- adding stock
- finding low-stock items

That makes the functions easier to test by hand.

Here is a small separate check file:

```text
day-93/check_inventory.py
```

Code:

```python
import inventory

items = {
    "notebooks": 5,
    "pens": 12,
}

inventory.add_stock(items, "notebooks", 3)
inventory.add_stock(items, "markers", 4)

print(items)
print(inventory.get_low_stock_items(items, 5))
```

Run:

```text
python day-93/check_inventory.py
```

You should see:

```text
{'notebooks': 8, 'pens': 12, 'markers': 4}
{'markers': 4}
```

That check is small on purpose.

You can see whether the inventory rules work without building the entire app first.

## Separating Logic From Interface

One of the most useful project habits is separating logic from interface code.

Logic means the rules of the program.

Interface code means the part that talks to the user.

In a command-line program, interface code often uses:

```python
input()
print()
```

Inventory logic asks questions like:

```text
What is the new count?
Which items are low?
Is this item already in the dictionary?
```

Interface code asks questions like:

```text
What should the user see?
What should the program ask next?
How should a result be printed?
```

Here is a tangled function:

```python
def add_item_from_user(items):
    name = input("Item name: ")
    amount = int(input("Amount: "))
    items[name] = items.get(name, 0) + amount
    print(f"{name} now has {items[name]}")
```

This function does three jobs:

- gets user input
- changes the inventory
- prints the result

That can work in a tiny script, but it is harder to reuse.

Here is the same idea split into clearer jobs.

`inventory.py` handles the rule:

```python
def add_stock(items, name, amount):
    current = items.get(name, 0)
    items[name] = current + amount
    return items
```

`main.py` can handle the user conversation:

```python
import inventory

items = {
    "notebooks": 5,
    "pens": 12,
}

name = input("Item name: ")
amount = int(input("Amount: "))

inventory.add_stock(items, name, amount)

print(f"{name} now has {items[name]}")
```

The split version is easier to grow.

Later, you could use `inventory.add_stock()` from:

- a command-line app
- a web app
- a test file
- another project

The function does not care where the item name came from.

That is the point.

## Add A Display Module

Create:

```text
day-93/display.py
```

Code:

```python
def print_inventory(items):
    if not items:
        print("No items yet.")
        return

    for name, count in items.items():
        print(f"{name}: {count}")


def print_low_stock(items):
    if not items:
        print("No low-stock items.")
        return

    print("Low stock:")

    for name, count in items.items():
        print(f"- {name}: {count}")
```

This file is allowed to print because printing is its job.

That is different from `inventory.py`.

The split is:

```text
inventory.py    decides which items are low
display.py      decides how to print those items
```

That separation is small, but it matters.

If you later want low-stock items printed differently, you can change `display.py`.

If you later want a different rule for "low", you can change `inventory.py`.

## Add A Data Folder

Many projects need files the program reads or writes.

Those files should not float around randomly.

Put them in a folder with a clear name:

```text
day-93/data/
```

For this project, create:

```text
day-93/data/inventory.json
```

Data:

```json
{
    "notebooks": 5,
    "pens": 12
}
```

The `data` folder tells the reader:

```text
This is not Python code. This is information the program uses.
```

That small distinction helps a lot.

Compare:

```text
day-93/
  main.py
  inventory.json
  inventory.py
```

with:

```text
day-93/
  main.py
  inventory.py
  data/
    inventory.json
```

The second version is easier to scan.

Code files and data files are not mixed together.

## Add A Storage Module

Now create a file that knows how to load and save the JSON data.

Create:

```text
day-93/storage.py
```

Code:

```python
import json
from pathlib import Path


DATA_PATH = Path(__file__).parent / "data" / "inventory.json"


def load_inventory():
    if not DATA_PATH.exists():
        return {}

    text = DATA_PATH.read_text()
    return json.loads(text)


def save_inventory(items):
    DATA_PATH.parent.mkdir(exist_ok=True)
    text = json.dumps(items, indent=4)
    DATA_PATH.write_text(text)
```

This file has one responsibility:

```text
Move inventory data between Python and the JSON file.
```

The line:

```python
DATA_PATH = Path(__file__).parent / "data" / "inventory.json"
```

builds a path to the data file based on the location of `storage.py`.

That is more reliable than assuming the terminal is always opened in the same folder.

You do not need to memorize every detail of this line today.

Read it as:

```text
Start beside this file.
Go into data.
Use inventory.json.
```

The `storage.py` file imports standard library modules:

```python
import json
from pathlib import Path
```

The `main.py` file will import local project modules:

```python
import display
import inventory
import storage
```

Both kinds of imports are normal.

## Put The Project Together

Now create:

```text
day-93/main.py
```

Code:

```python
import display
import inventory
import storage


def main():
    items = storage.load_inventory()

    inventory.add_stock(items, "markers", 3)

    low_stock = inventory.get_low_stock_items(items, 5)

    display.print_inventory(items)
    display.print_low_stock(low_stock)

    storage.save_inventory(items)


if __name__ == "__main__":
    main()
```

Run:

```text
python day-93/main.py
```

You should see:

```text
notebooks: 5
pens: 12
markers: 3
Low stock:
- notebooks: 5
- markers: 3
```

This is a small program, but the organization is already useful.

`main.py` reads almost like a checklist:

```text
load data
change data
find low-stock items
show data
save data
```

The details live in the helper modules.

That is a good sign.

## Imports Between Project Files

When files live in the same folder, a simple import often works:

```python
import inventory
```

Then you use the module name:

```python
inventory.add_stock(items, "markers", 3)
```

This is usually clearer than importing every function directly.

Clear:

```python
import inventory

inventory.add_stock(items, "markers", 3)
```

Also valid:

```python
from inventory import add_stock

add_stock(items, "markers", 3)
```

For beginner projects, the first style is often easier to read because the module name stays visible.

When you see:

```python
storage.load_inventory()
```

you know the function came from `storage.py`.

When you see:

```python
display.print_inventory(items)
```

you know the function came from `display.py`.

The module prefix is a tiny map.

### Avoid Circular Imports

A circular import happens when two files try to import each other.

For example:

```text
main.py imports inventory.py
inventory.py imports main.py
```

That loop can confuse Python.

It can also confuse the reader.

A better direction is:

```text
main.py imports inventory.py
main.py imports display.py
main.py imports storage.py
```

The helper modules should usually not import `main.py`.

Think of `main.py` as the file that coordinates the others.

The helpers should not need to know who called them.

## README.md

A `README.md` is a note for humans.

It explains what the project is and how to run it.

Create:

```text
day-93/README.md
```

Text:

````md
# Inventory Tracker

A small command-line inventory project for practice.

## How To Run

Run this command from the folder above `day-93`:

```text
python day-93/main.py
```

## Files

- `main.py` starts the program.
- `inventory.py` contains inventory rules.
- `display.py` prints inventory information.
- `storage.py` loads and saves JSON data.
- `data/inventory.json` stores the saved inventory.
````

The README does not need to be long.

A useful beginner README answers:

- What is this project?
- How do I run it?
- What are the main files?
- Does it need any packages?

Tomorrow, when you start Git and GitHub, `README.md` will matter even more.

It is often the first file another person reads in a project.

## requirements.txt

A `requirements.txt` file lists third-party packages a project needs.

This inventory project uses only the Python standard library:

- `json`
- `pathlib`

Those do not need to be installed with `pip`.

So for this project, create:

```text
day-93/requirements.txt
```

Text:

```text
# This project currently uses only the Python standard library.
```

That comment is allowed.

If a later version used the third-party package `rich`, the file might contain:

```text
rich
```

Then someone could install the project requirements with:

```text
python -m pip install -r requirements.txt
```

The important idea is:

```text
README.md explains the project to people.
requirements.txt helps recreate the Python package setup.
```

They solve different problems.

## Avoid Giant Files

A file is getting too large when you feel lost inside it.

There is no magic line number.

A 40-line file can be messy.

A 200-line file can be clear.

Instead of counting lines first, ask:

- Does this file have more than one main job?
- Are there functions here that could be reused elsewhere?
- Do I keep scrolling to find one small helper?
- Are input, printing, file saving, and data rules all mixed together?
- Would a clear file name describe a group of these functions?

If the answer is yes, split carefully.

For example, this group probably belongs in `storage.py`:

```text
load_inventory
save_inventory
DATA_PATH
```

This group probably belongs in `inventory.py`:

```text
add_stock
remove_stock
get_low_stock_items
```

This group probably belongs in `display.py`:

```text
print_inventory
print_low_stock
print_error
```

When you split a file, do not split randomly.

Split by responsibility.

## Naming Files Well

Good file names are short, specific, and boring.

Use lowercase letters and underscores:

```text
inventory.py
storage.py
display.py
date_tools.py
text_tools.py
score_report.py
```

Avoid spaces:

```text
score report.py
```

Avoid hyphens in Python file names:

```text
score-report.py
```

Hyphens are fine in folders and markdown files, but they are awkward in Python imports.

This is easy to import:

```python
import score_report
```

This is not a normal Python import:

```text
import score-report
```

Also avoid names that match common standard library modules:

```text
json.py
random.py
math.py
pathlib.py
statistics.py
csv.py
```

Those names can hide the real modules you meant to import.

When in doubt, make the name more specific:

```text
json_practice.py
random_picker.py
math_notes.py
csv_report.py
```

## Try It Yourself

Build the inventory project in small steps.

Do not write every file at once.

### Step 1: Create The Folder Tree

Create this layout:

```text
day-93/
  main.py
  inventory.py
  display.py
  storage.py
  data/
    inventory.json
  README.md
  requirements.txt
```

Start with empty Python files.

Then add the JSON data:

```json
{
    "notebooks": 5,
    "pens": 12
}
```

### Step 2: Add Inventory Logic

Put this in `day-93/inventory.py`:

```python
def add_stock(items, name, amount):
    current = items.get(name, 0)
    items[name] = current + amount
    return items


def get_low_stock_items(items, limit):
    low_stock = {}

    for name, count in items.items():
        if count <= limit:
            low_stock[name] = count

    return low_stock
```

### Step 3: Add Display Code

Put this in `day-93/display.py`:

```python
def print_inventory(items):
    if not items:
        print("No items yet.")
        return

    for name, count in items.items():
        print(f"{name}: {count}")


def print_low_stock(items):
    if not items:
        print("No low-stock items.")
        return

    print("Low stock:")

    for name, count in items.items():
        print(f"- {name}: {count}")
```

### Step 4: Add Storage Code

Put this in `day-93/storage.py`:

```python
import json
from pathlib import Path


DATA_PATH = Path(__file__).parent / "data" / "inventory.json"


def load_inventory():
    if not DATA_PATH.exists():
        return {}

    text = DATA_PATH.read_text()
    return json.loads(text)


def save_inventory(items):
    DATA_PATH.parent.mkdir(exist_ok=True)
    text = json.dumps(items, indent=4)
    DATA_PATH.write_text(text)
```

### Step 5: Add The Main Program

Put this in `day-93/main.py`:

```python
import display
import inventory
import storage


def main():
    items = storage.load_inventory()

    inventory.add_stock(items, "markers", 3)

    low_stock = inventory.get_low_stock_items(items, 5)

    display.print_inventory(items)
    display.print_low_stock(low_stock)

    storage.save_inventory(items)


if __name__ == "__main__":
    main()
```

Run:

```text
python day-93/main.py
```

You should see:

```text
notebooks: 5
pens: 12
markers: 3
Low stock:
- notebooks: 5
- markers: 3
```

Run it a second time.

You may see:

```text
notebooks: 5
pens: 12
markers: 6
Low stock:
- notebooks: 5
```

Why did `markers` change?

Because the program saves the updated inventory back to:

```text
day-93/data/inventory.json
```

That is real project behavior.

The program remembers something between runs.

### Step 6: Add Project Notes

Put this in `day-93/README.md`:

````md
# Inventory Tracker

A small command-line inventory project for practice.

## How To Run

Run this command from the folder above `day-93`:

```text
python day-93/main.py
```

## Files

- `main.py` starts the program.
- `inventory.py` contains inventory rules.
- `display.py` prints inventory information.
- `storage.py` loads and saves JSON data.
- `data/inventory.json` stores the saved inventory.
````

Put this in `day-93/requirements.txt`:

```text
# This project currently uses only the Python standard library.
```

Now the folder has both code and project notes.

That is the shape you want before learning Git.

## Common Mistake

The most common mistake is splitting files without giving each file a clear job.

For example:

```text
helpers.py
helpers_more.py
helpers_final.py
```

Those names do not tell you much.

The project may be split into files, but it is not truly organized.

Better:

```text
inventory.py
storage.py
display.py
```

Each name gives the file a purpose.

### Mistake 1: Doing Real Work During Import

This is risky in a helper module:

```python
print("Loading inventory")


def add_stock(items, name, amount):
    items[name] = items.get(name, 0) + amount
    return items
```

If `main.py` imports this file, the print line runs immediately.

Helper modules should usually define functions, constants, or classes.

They should not start the app just because they were imported.

Use the main guard when a file has demo code:

```python
def demo():
    items = {"pens": 10}
    add_stock(items, "pens", 2)
    print(items)


if __name__ == "__main__":
    demo()
```

### Mistake 2: Letting Helpers Import `main.py`

This direction is usually good:

```text
main.py imports inventory.py
```

This direction is usually suspicious:

```text
inventory.py imports main.py
```

When helper files import the starter file, the project can become tangled.

Keep `main.py` as the coordinator.

Let helper modules do their own smaller jobs.

### Mistake 3: Naming A File After A Module

Avoid this:

```text
day-93/json.py
```

If another file says:

```python
import json
```

Python may find your local `json.py` before the standard library `json` module.

Use a clearer practice name:

```text
day-93/json_notes.py
```

or:

```text
day-93/inventory_json_practice.py
```

## Debug It

Multi-file projects create a few new beginner errors.

The good news is that the errors usually point to the kind of problem you have.

### Problem 1: Python Cannot Find Your Module

You might see:

```text
ModuleNotFoundError: No module named 'inventory'
```

Check these things:

- Is `inventory.py` spelled correctly?
- Is it in the same folder as `main.py`?
- Did you name it `Inventory.py` with a capital letter by accident?
- Are you running the intended file?

For today's project, this command should work from the folder above `day-93`:

```text
python day-93/main.py
```

### Problem 2: The JSON File Cannot Be Found

You might see:

```text
FileNotFoundError
```

Check the tree:

```text
day-93/
  storage.py
  data/
    inventory.json
```

The folder name should be:

```text
data
```

The file name should be:

```text
inventory.json
```

Also check that `storage.py` uses this path pattern:

```python
DATA_PATH = Path(__file__).parent / "data" / "inventory.json"
```

That points to the `data` folder beside `storage.py`.

### Problem 3: A File Runs Too Early

If a helper file prints text just because you imported it, look for top-level code.

Top-level code is code that is not inside a function, class, or main guard.

This runs during import:

```python
print("Checking inventory")
```

This waits until the function is called:

```python
def check_inventory():
    print("Checking inventory")
```

This runs only when the file is run directly:

```python
if __name__ == "__main__":
    check_inventory()
```

### Problem 4: Two Files Import Each Other

You might see an import error that mentions a partially initialized module.

That can happen when files import each other in a circle.

Look for a pattern like this:

```text
main.py imports inventory.py
inventory.py imports main.py
```

A simple fix is often:

```text
Move shared helper code into a third file.
Let main.py coordinate the helpers.
```

For example:

```text
main.py imports inventory.py
main.py imports display.py
inventory.py does not import main.py
display.py does not import main.py
```

### Problem 5: The Project Works Once, Then Shows Different Data

In today's project, that may be normal.

The program saves updated data.

If `markers` increases after each run, check this line in `main.py`:

```python
inventory.add_stock(items, "markers", 3)
```

Every run adds 3 more markers and saves the result.

That is not an import problem.

It is the program doing exactly what you asked it to do.

For practice, you can reset `day-93/data/inventory.json` to:

```json
{
    "notebooks": 5,
    "pens": 12
}
```

## Read the Docs

Today, use the documentation to answer small questions.

You do not need to read an entire page.

Look up one idea at a time.

Find the Python documentation for modules and answer:

```text
What is a module?
```

Then find the `pathlib` documentation and answer:

```text
What kind of object does Path(__file__).parent create?
What does Path.exists() check?
What does Path.write_text() do?
```

Finally, look at a real project README from any Python project you like.

Find these parts:

- project name
- short description
- install or setup notes
- run command
- file or feature explanation

Do not worry if the project is more advanced than yours.

You are only studying the shape of the documentation.

## Mini Challenge

Create a tiny book tracker project.

Use this layout:

```text
day-93/book_tracker/
  main.py
  books.py
  display.py
  data/
    books.json
  README.md
  requirements.txt
```

Put this in `day-93/book_tracker/data/books.json`:

```json
[
    {
        "title": "The Hobbit",
        "finished": true
    },
    {
        "title": "A Wrinkle in Time",
        "finished": false
    }
]
```

In `books.py`, write:

```python
def count_finished(books):
    total = 0

    for book in books:
        if book["finished"]:
            total += 1

    return total
```

In `display.py`, write:

```python
def print_summary(total_books, finished_books):
    print(f"Books tracked: {total_books}")
    print(f"Books finished: {finished_books}")
```

In `main.py`, load the JSON file, call the helper functions, and print the summary.

Use `day-93/storage.py` from the inventory project as a guide, but change the file name and data shape.

When it works, add a short README.

The win is not the book tracker itself.

The win is creating a second project with the same organized thinking.

## Real-World Use

Most useful Python projects are folders, not single files.

A small command-line tool might look like:

```text
task_tool/
  main.py
  tasks.py
  storage.py
  display.py
  data/
    tasks.json
  README.md
  requirements.txt
```

A small data cleanup project might look like:

```text
sales_cleanup/
  main.py
  clean_rows.py
  reports.py
  data/
    raw_sales.csv
    cleaned_sales.csv
  README.md
  requirements.txt
```

A small API project might look like:

```text
movie_lookup/
  main.py
  api_client.py
  formatters.py
  storage.py
  data/
    last_search.json
  README.md
  requirements.txt
```

The exact names change.

The habit stays the same:

```text
Put related code together.
Give each file a job.
Keep setup notes close to the project.
Keep data files in a clear place.
```

This organization also prepares the project for Git.

Git works best when the project has a clear folder shape.

Tomorrow, you will learn how to save snapshots of a project as it changes.

When your files are named clearly, those snapshots are easier to understand.

## Recap

Today you learned that a Python project is usually a folder with several related files.

A clear beginner layout can look like this:

```text
day-93/
  main.py
  inventory.py
  display.py
  storage.py
  data/
    inventory.json
  README.md
  requirements.txt
```

You learned these roles:

- `main.py` starts and coordinates the program
- helper modules hold focused code
- `data/` stores files the program reads or writes
- `README.md` explains the project to people
- `requirements.txt` lists third-party packages

You also practiced separating:

```text
logic code
```

from:

```text
interface code
```

For today's inventory project:

```text
inventory.py    handles rules
display.py      handles printed output
storage.py      handles saved data
main.py         connects the pieces
```

That is the main skill.

You are not just writing more files.

You are giving the project a shape.

## Lesson Checklist

Before moving on, make sure you can:

- [ ] draw a small project tree
- [ ] explain why `main.py` is a useful starting file
- [ ] create a helper module beside `main.py`
- [ ] import your own project module
- [ ] call a helper function with `module_name.function_name()`
- [ ] explain the difference between logic code and interface code
- [ ] keep saved data in a `data` folder
- [ ] explain what `README.md` is for
- [ ] explain what `requirements.txt` is for
- [ ] avoid naming files `json.py`, `random.py`, or `math.py`
- [ ] recognize a circular import warning sign
- [ ] split a file by responsibility instead of by random line count

## Exercises

### Exercise 1: Label The Files

Read this tree:

```text
day-93/
  main.py
  scores.py
  display.py
  storage.py
  data/
    scores.json
  README.md
  requirements.txt
```

Write one sentence for each file or folder:

- What belongs in `main.py`?
- What belongs in `scores.py`?
- What belongs in `display.py`?
- What belongs in `storage.py`?
- What belongs in `data/`?
- What belongs in `README.md`?
- What belongs in `requirements.txt`?

### Exercise 2: Split The Jobs

This function does too many jobs:

```python
def add_score(scores):
    name = input("Name: ")
    score = int(input("Score: "))
    scores[name] = score
    print(f"Saved {name}: {score}")
```

Write a new logic function that does not use `input()` or `print()`:

```python
def save_score(scores, name, score):
    scores[name] = score
    return scores
```

Then write a short `main.py` example that asks for input and calls `save_score()`.

### Exercise 3: Choose Better Names

Rewrite these file names as clearer project file names:

```text
helpers.py
things.py
final.py
json.py
random.py
more_helpers.py
```

Possible answers:

```text
storage.py
display.py
main.py
json_notes.py
random_picker.py
score_tools.py
```

Your answers can be different if they are specific.

### Exercise 4: Build A Small Project Tree

Design a project tree for a recipe app.

It should include:

- `main.py`
- at least two helper modules
- a `data` folder
- a README
- a requirements file

Write your tree as a text block.

Example shape:

```text
day-93/recipe_app/
  main.py
  recipes.py
  storage.py
  data/
    recipes.json
  README.md
  requirements.txt
```

### Exercise 5: Find The Circular Import

Read this import map:

```text
main.py imports display.py
main.py imports inventory.py
inventory.py imports storage.py
storage.py imports main.py
```

Which line is suspicious?

Answer:

```text
storage.py imports main.py
```

Write one sentence explaining why helper modules usually should not import `main.py`.

### Exercise 6: Add A README

Create a README for one practice project.

Include:

- project name
- one-sentence description
- how to run it
- short file list

Keep it short.

Five to ten lines is enough.

### Exercise 7: Explain requirements.txt

Answer these questions:

- What is `requirements.txt` for?
- Does `json` need to be listed there?
- Does `pathlib` need to be listed there?
- Would a third-party package like `rich` belong there?

Use one sentence for each answer.

### Exercise 8: Move One Function

Find an older program from this course that has at least two functions.

Move one reusable function into a helper file.

For example:

```text
day-93/text_tools.py
day-93/main.py
```

Then import the helper file from `main.py`.

Use the clear style:

```python
import text_tools
```

and call:

```python
text_tools.some_function()
```

### Exercise 9: Reset The Data

Run the inventory project twice.

Watch `markers` increase.

Then reset `day-93/data/inventory.json` to:

```json
{
    "notebooks": 5,
    "pens": 12
}
```

Run the project again.

Write one sentence explaining why saved data changed the program output.

### Exercise 10: Prepare For Git

Before tomorrow, look at your `day-93` folder and answer:

- Which files are code?
- Which files are data?
- Which file explains the project?
- Which file describes package requirements?
- Which file should someone run first?

These answers will make Git easier to understand because Git tracks files.

Knowing what each file is for makes each saved project snapshot more meaningful.

## Tiny Win

You can now look at a small pile of Python code and give it a home.

That is a practical milestone.

A project with several files can feel intimidating at first, but the pattern is simple:

```text
main.py starts
helpers help
data stores
README explains
requirements records packages
```

Once you know that pattern, a project folder stops looking like a mess of files.

It starts looking like a map.

## Tomorrow

Tomorrow is:

```text
Day 94: Git and GitHub Basics
```

Today you organized a project folder.

Tomorrow you will learn how to save project milestones with Git.

You will also see how GitHub can hold a copy of a project online.

The folder layout from today matters because Git tracks files.

Clear files make clear history.
