# Day 98: Capstone Build Day 1

**Focus:** Building the first working version of a personal task tracker and study planner  
**You will practice:** choosing a data model, writing a small `Task` class, saving and loading JSON, adding tasks, listing tasks, completing tasks, menu design, input validation, file error handling, and planning the next version  
**Estimated time:** 85-110 minutes

## Today's Goal

Today you will start the final capstone project.

The project is a personal task tracker and study planner. It will run in the command line and save your tasks in a JSON file so the program can remember them after it closes.

By the end of today, you should be able to:

- describe the data for one task
- decide when a class is useful instead of plain dictionaries everywhere
- create a `Task` class with attributes and methods
- convert a `Task` object into a dictionary for JSON saving
- convert a dictionary back into a `Task` object after JSON loading
- add a new study task from user input
- list all tasks
- list only active tasks
- mark an active task as complete
- save the task list to `day-98/tasks.json`
- load tasks from `day-98/tasks.json`
- handle missing files, invalid JSON, bad menu choices, and invalid numbers
- leave the project ready for Day 99, where you will improve the app

This is the first build day, not the final polish day.

Today the goal is a strong version 1:

```text
start the app
load saved tasks
use the menu
add tasks
list tasks
complete tasks
save tasks
quit
```

If that works, you have a real project.

## The Big Idea

A task tracker is useful because it remembers small commitments.

One task might be:

```text
title: Finish Python review notes
subject: Python
due date: 2026-05-12
estimated minutes: 45
completed: false
```

In Python, you could store that as a dictionary:

```python
task = {
    "title": "Finish Python review notes",
    "subject": "Python",
    "due_date": "2026-05-12",
    "estimated_minutes": 45,
    "completed": False
}
```

That is a good data shape.

But the app also needs behavior:

- display one task in a readable line
- mark one task as complete
- convert one task into a dictionary
- rebuild one task from saved JSON data

That is a useful reason to create a class:

```python
class Task:
    def __init__(self, title, subject, due_date, estimated_minutes, completed=False):
        self.title = title
        self.subject = subject
        self.due_date = due_date
        self.estimated_minutes = estimated_minutes
        self.completed = completed
```

The class gives the project a clear word for one record:

```text
Task
```

The app will still use dictionaries, but only as the bridge to JSON.

The project pattern is:

```text
Task object -> dictionary -> JSON file
JSON file -> dictionary -> Task object
```

That pattern appears in many real Python projects.

## The Mental Model

Think of the app as three layers.

```text
task data
  one Task object

task collection
  a list of Task objects

interface
  the menu that asks the user what to do
```

The `Task` class handles one task:

```text
title
subject
due date
estimated minutes
completed or open
```

The list holds many tasks:

```text
[
    Task(...),
    Task(...),
    Task(...)
]
```

The menu lets the user work with that list:

```text
1. List all tasks
2. List active tasks
3. Add task
4. Complete task
5. Save tasks
6. Load tasks
7. Quit
```

JSON saving is the memory layer.

When the app saves, it writes task dictionaries to:

```text
day-98/tasks.json
```

When the app starts again, it reads that file and recreates `Task` objects.

## Task Class Or Dictionary?

Both choices can work.

For version 1, this lesson uses a `Task` class.

The reason is not that classes are always better. The reason is that one task has both data and behavior.

The data is:

```text
title
subject
due_date
estimated_minutes
completed
```

The behavior is:

```text
turn this task into a dictionary
build this task from a dictionary
show this task as one menu line
mark this task complete
```

That makes `Task` a helpful class.

The app still saves plain dictionaries because JSON understands dictionaries, lists, strings, numbers, booleans, and `null`.

JSON does not understand your custom `Task` object directly.

So the rule for today is:

```text
Use Task objects while the program runs.
Use dictionaries when saving to JSON.
```

## The Project

Create a folder named:

```text
day-98
```

Inside it, create this file:

```text
day-98/task_tracker.py
```

The program will save data here:

```text
day-98/tasks.json
```

Your version 1 app will:

1. Start with a title.
2. Try to load saved tasks from `day-98/tasks.json`.
3. Show a menu.
4. Let the user list all tasks.
5. Let the user list active tasks.
6. Let the user add a task.
7. Let the user complete an active task.
8. Let the user save tasks.
9. Let the user load tasks again.
10. Handle common mistakes without crashing.
11. Keep running until the user chooses quit.

A short session might look like this:

```text
Personal Task Tracker
No saved tasks found yet.

Menu:
1. List all tasks
2. List active tasks
3. Add task
4. Complete task
5. Save tasks
6. Load tasks
7. Quit
Choose an option: 3
Task title: Review functions
Subject or course: Python
Due date (blank for none): 2026-05-12
Estimated minutes: 30
Added Review functions.

Menu:
1. List all tasks
2. List active tasks
3. Add task
4. Complete task
5. Save tasks
6. Load tasks
7. Quit
Choose an option: 1

Tasks:
1. [open] Review functions | Python | due: 2026-05-12 | 30 min

Menu:
1. List all tasks
2. List active tasks
3. Add task
4. Complete task
5. Save tasks
6. Load tasks
7. Quit
Choose an option: 5
Saved 1 task(s) to day-98/tasks.json.

Menu:
1. List all tasks
2. List active tasks
3. Add task
4. Complete task
5. Save tasks
6. Load tasks
7. Quit
Choose an option: 7
Goodbye.
```

The exact tasks will depend on what the user types.

## Step-by-Step Build

Build this app in small pieces.

Do not try to understand the whole file in one glance. A capstone project is supposed to have several parts.

### Step 1: Import The Tools

The app needs JSON support and file path support.

```python
import json
from pathlib import Path
```

`json` reads and writes saved task data.

`Path` gives the save file a clean path.

### Step 2: Add The Save Path

Use one constant for the JSON file.

```python
SAVE_PATH = Path("day-98/tasks.json")
```

Using one name helps because the path appears in several places:

- loading
- saving
- success messages
- debugging

If you change the save file later, you change it once.

### Step 3: Create The Task Class

One task needs five pieces of data.

```python
class Task:
    def __init__(self, title, subject, due_date, estimated_minutes, completed=False):
        self.title = title
        self.subject = subject
        self.due_date = due_date
        self.estimated_minutes = estimated_minutes
        self.completed = completed
```

The `completed=False` part means new tasks are open unless the program says otherwise.

Create one task in your head:

```python
Task("Review functions", "Python", "2026-05-12", 30)
```

That task has:

```text
title: Review functions
subject: Python
due date: 2026-05-12
estimated minutes: 30
completed: False
```

### Step 4: Add A Display Method

The task list needs one readable line for each task.

Add this method inside `Task`:

```python
def display_line(self, number):
    status = "done" if self.completed else "open"
    return (
        f"{number}. [{status}] {self.title} | {self.subject} | "
        f"due: {self.due_date} | {self.estimated_minutes} min"
    )
```

The method receives a number because the menu will show tasks as:

```text
1. [open] Review functions | Python | due: 2026-05-12 | 30 min
```

That number is not saved in the task.

It is only for the current display.

### Step 5: Add A Complete Method

Completing a task changes one attribute.

Add this method inside `Task`:

```python
def mark_complete(self):
    self.completed = True
```

This small method makes the menu code read clearly later:

```python
task.mark_complete()
```

### Step 6: Convert A Task To A Dictionary

JSON cannot save a `Task` object directly.

It can save a dictionary.

Add this method inside `Task`:

```python
def to_dict(self):
    return {
        "title": self.title,
        "subject": self.subject,
        "due_date": self.due_date,
        "estimated_minutes": self.estimated_minutes,
        "completed": self.completed
    }
```

That method turns a task object into this kind of data:

```json
{
    "title": "Review functions",
    "subject": "Python",
    "due_date": "2026-05-12",
    "estimated_minutes": 30,
    "completed": false
}
```

That shape is safe to write into `day-98/tasks.json`.

### Step 7: Build A Task From A Dictionary

Loading goes in the other direction.

The app reads a dictionary from JSON and turns it back into a `Task` object.

Add this class method inside `Task`:

```python
@classmethod
def from_dict(cls, record):
    if not isinstance(record, dict):
        raise ValueError("Each saved task should be a dictionary.")

    try:
        title = str(record["title"]).strip()
        subject = str(record.get("subject", "General")).strip()
        due_date = str(record.get("due_date", "")).strip()
        raw_minutes = record["estimated_minutes"]
        completed = record.get("completed", False)
    except KeyError as error:
        raise ValueError("One saved task is missing a required field.") from error

    if title == "":
        raise ValueError("One saved task has a blank title.")

    if subject == "":
        subject = "General"

    if due_date == "":
        due_date = "No due date"

    if isinstance(raw_minutes, bool):
        raise ValueError("One saved task has invalid minutes.")

    try:
        estimated_minutes = int(raw_minutes)
    except (TypeError, ValueError) as error:
        raise ValueError("One saved task has invalid minutes.") from error

    if estimated_minutes <= 0:
        raise ValueError("One saved task has minutes less than 1.")

    if not isinstance(completed, bool):
        raise ValueError("One saved task has an invalid completed value.")

    return cls(title, subject, due_date, estimated_minutes, completed)
```

This method is careful because saved files can be edited by hand.

If `tasks.json` contains bad data, the app should explain the problem instead of crashing with a confusing traceback.

### Step 8: Save A List Of Tasks

Saving the full project means saving a list of task dictionaries.

```python
def save_tasks(tasks, path):
    path = Path(path)
    path.parent.mkdir(parents=True, exist_ok=True)

    data = []

    for task in tasks:
        data.append(task.to_dict())

    with path.open("w", encoding="utf-8") as file:
        json.dump(data, file, indent=4)
```

The line with `mkdir()` creates the `day-98` folder if it is missing.

The saved file will be easier to read because `json.dump()` uses:

```python
indent=4
```

### Step 9: Load A List Of Tasks

Loading has three jobs:

- return an empty list if no save file exists yet
- read JSON if the file exists
- validate the saved data before using it

```python
def load_tasks(path):
    path = Path(path)

    if not path.exists():
        return []

    try:
        with path.open("r", encoding="utf-8") as file:
            data = json.load(file)
    except json.JSONDecodeError as error:
        raise ValueError("The task file is not valid JSON.") from error

    if not isinstance(data, list):
        raise ValueError("The task file should contain a list of tasks.")

    tasks = []

    for record in data:
        tasks.append(Task.from_dict(record))

    return tasks
```

The function does not print.

It either returns a list of tasks or raises an error that the menu can show.

### Step 10: Print The Menu

Keep menu printing separate from menu decisions.

```python
def show_menu():
    print()
    print("Menu:")
    print("1. List all tasks")
    print("2. List active tasks")
    print("3. Add task")
    print("4. Complete task")
    print("5. Save tasks")
    print("6. Load tasks")
    print("7. Quit")
```

This function only displays choices.

The main loop will decide what each choice means.

### Step 11: List Tasks

The same listing function can handle all tasks or only active tasks.

```python
def list_tasks(tasks, active_only=False):
    if active_only:
        visible_tasks = []

        for task in tasks:
            if not task.completed:
                visible_tasks.append(task)
    else:
        visible_tasks = tasks

    if not visible_tasks:
        if active_only:
            print("No active tasks.")
        else:
            print("No tasks yet.")
        return

    print()
    print("Tasks:")

    for index, task in enumerate(visible_tasks, start=1):
        print(task.display_line(index))
```

The `active_only` argument gives the function a simple switch:

```python
list_tasks(tasks)
list_tasks(tasks, active_only=True)
```

### Step 12: Ask For Minutes

The user types text.

The app needs a positive whole number.

```python
def ask_for_minutes(prompt):
    raw_value = input(prompt).strip()

    try:
        minutes = int(raw_value)
    except ValueError:
        print("Please enter a whole number of minutes.")
        return None

    if minutes <= 0:
        print("Minutes must be at least 1.")
        return None

    return minutes
```

Returning `None` lets the menu stop the current action and return to the menu.

The whole app does not need to stop because one entry was bad.

### Step 13: Add A Task From The Menu

Adding a task is mostly input checking.

```python
def add_task_from_menu(tasks):
    title = input("Task title: ").strip()

    if title == "":
        print("Task title cannot be blank.")
        return

    subject = input("Subject or course: ").strip()

    if subject == "":
        subject = "General"

    due_date = input("Due date (blank for none): ").strip()

    if due_date == "":
        due_date = "No due date"

    estimated_minutes = ask_for_minutes("Estimated minutes: ")

    if estimated_minutes is None:
        return

    task = Task(title, subject, due_date, estimated_minutes)
    tasks.append(task)
    print(f"Added {task.title}.")
```

Version 1 does not require a date parser.

That is intentional.

The app stores the due date as text so the beginner project can focus on data flow first.

Day 99 can make dates smarter if you choose that improvement.

### Step 14: Complete A Task

The complete feature should show only active tasks.

A completed task should not appear in the completion list.

```python
def get_active_tasks(tasks):
    active_tasks = []

    for task in tasks:
        if not task.completed:
            active_tasks.append(task)

    return active_tasks
```

Now complete one active task by number.

```python
def complete_task_from_menu(tasks):
    active_tasks = get_active_tasks(tasks)

    if not active_tasks:
        print("No active tasks to complete.")
        return

    list_tasks(active_tasks)

    raw_choice = input("Task number to complete: ").strip()

    try:
        task_number = int(raw_choice)
    except ValueError:
        print("Please enter a task number.")
        return

    if task_number < 1 or task_number > len(active_tasks):
        print("Choose a number from the active task list.")
        return

    task = active_tasks[task_number - 1]
    task.mark_complete()
    print(f"Completed {task.title}.")
```

This works because `active_tasks` contains the same task objects as `tasks`.

When you mark one task complete in `active_tasks`, you are changing the same object that lives in the main list.

### Step 15: Build The Main Loop

The main loop ties the project together.

It loads tasks at startup, shows the menu, runs the selected action, and handles save/load errors.

```python
def main():
    print("Personal Task Tracker")

    try:
        tasks = load_tasks(SAVE_PATH)
    except ValueError as error:
        print(f"Could not load saved tasks: {error}")
        tasks = []
    except OSError as error:
        print(f"Could not read the task file: {error}")
        tasks = []
    else:
        if tasks:
            print(f"Loaded {len(tasks)} task(s).")
        else:
            print("No saved tasks found yet.")

    while True:
        show_menu()
        choice = input("Choose an option: ").strip()

        if choice == "1":
            list_tasks(tasks)
        elif choice == "2":
            list_tasks(tasks, active_only=True)
        elif choice == "3":
            add_task_from_menu(tasks)
        elif choice == "4":
            complete_task_from_menu(tasks)
        elif choice == "5":
            try:
                save_tasks(tasks, SAVE_PATH)
            except OSError as error:
                print(f"Could not save tasks: {error}")
            else:
                print(f"Saved {len(tasks)} task(s) to {SAVE_PATH}.")
        elif choice == "6":
            try:
                tasks = load_tasks(SAVE_PATH)
            except ValueError as error:
                print(f"Could not load tasks: {error}")
            except OSError as error:
                print(f"Could not read the task file: {error}")
            else:
                if tasks:
                    print(f"Loaded {len(tasks)} task(s).")
                else:
                    print("No saved tasks found yet.")
        elif choice == "7":
            print("Goodbye.")
            break
        else:
            print("Choose a number from 1 to 7.")
```

The loop is long, but it is readable because the helper functions do the smaller jobs.

### Step 16: Put The Full Program Together

Here is the full `day-98/task_tracker.py` for version 1.

```python
import json
from pathlib import Path


SAVE_PATH = Path("day-98/tasks.json")


class Task:
    def __init__(self, title, subject, due_date, estimated_minutes, completed=False):
        self.title = title
        self.subject = subject
        self.due_date = due_date
        self.estimated_minutes = estimated_minutes
        self.completed = completed

    def display_line(self, number):
        status = "done" if self.completed else "open"
        return (
            f"{number}. [{status}] {self.title} | {self.subject} | "
            f"due: {self.due_date} | {self.estimated_minutes} min"
        )

    def mark_complete(self):
        self.completed = True

    def to_dict(self):
        return {
            "title": self.title,
            "subject": self.subject,
            "due_date": self.due_date,
            "estimated_minutes": self.estimated_minutes,
            "completed": self.completed
        }

    @classmethod
    def from_dict(cls, record):
        if not isinstance(record, dict):
            raise ValueError("Each saved task should be a dictionary.")

        try:
            title = str(record["title"]).strip()
            subject = str(record.get("subject", "General")).strip()
            due_date = str(record.get("due_date", "")).strip()
            raw_minutes = record["estimated_minutes"]
            completed = record.get("completed", False)
        except KeyError as error:
            raise ValueError("One saved task is missing a required field.") from error

        if title == "":
            raise ValueError("One saved task has a blank title.")

        if subject == "":
            subject = "General"

        if due_date == "":
            due_date = "No due date"

        if isinstance(raw_minutes, bool):
            raise ValueError("One saved task has invalid minutes.")

        try:
            estimated_minutes = int(raw_minutes)
        except (TypeError, ValueError) as error:
            raise ValueError("One saved task has invalid minutes.") from error

        if estimated_minutes <= 0:
            raise ValueError("One saved task has minutes less than 1.")

        if not isinstance(completed, bool):
            raise ValueError("One saved task has an invalid completed value.")

        return cls(title, subject, due_date, estimated_minutes, completed)


def save_tasks(tasks, path):
    path = Path(path)
    path.parent.mkdir(parents=True, exist_ok=True)

    data = []

    for task in tasks:
        data.append(task.to_dict())

    with path.open("w", encoding="utf-8") as file:
        json.dump(data, file, indent=4)


def load_tasks(path):
    path = Path(path)

    if not path.exists():
        return []

    try:
        with path.open("r", encoding="utf-8") as file:
            data = json.load(file)
    except json.JSONDecodeError as error:
        raise ValueError("The task file is not valid JSON.") from error

    if not isinstance(data, list):
        raise ValueError("The task file should contain a list of tasks.")

    tasks = []

    for record in data:
        tasks.append(Task.from_dict(record))

    return tasks


def show_menu():
    print()
    print("Menu:")
    print("1. List all tasks")
    print("2. List active tasks")
    print("3. Add task")
    print("4. Complete task")
    print("5. Save tasks")
    print("6. Load tasks")
    print("7. Quit")


def list_tasks(tasks, active_only=False):
    if active_only:
        visible_tasks = []

        for task in tasks:
            if not task.completed:
                visible_tasks.append(task)
    else:
        visible_tasks = tasks

    if not visible_tasks:
        if active_only:
            print("No active tasks.")
        else:
            print("No tasks yet.")
        return

    print()
    print("Tasks:")

    for index, task in enumerate(visible_tasks, start=1):
        print(task.display_line(index))


def ask_for_minutes(prompt):
    raw_value = input(prompt).strip()

    try:
        minutes = int(raw_value)
    except ValueError:
        print("Please enter a whole number of minutes.")
        return None

    if minutes <= 0:
        print("Minutes must be at least 1.")
        return None

    return minutes


def add_task_from_menu(tasks):
    title = input("Task title: ").strip()

    if title == "":
        print("Task title cannot be blank.")
        return

    subject = input("Subject or course: ").strip()

    if subject == "":
        subject = "General"

    due_date = input("Due date (blank for none): ").strip()

    if due_date == "":
        due_date = "No due date"

    estimated_minutes = ask_for_minutes("Estimated minutes: ")

    if estimated_minutes is None:
        return

    task = Task(title, subject, due_date, estimated_minutes)
    tasks.append(task)
    print(f"Added {task.title}.")


def get_active_tasks(tasks):
    active_tasks = []

    for task in tasks:
        if not task.completed:
            active_tasks.append(task)

    return active_tasks


def complete_task_from_menu(tasks):
    active_tasks = get_active_tasks(tasks)

    if not active_tasks:
        print("No active tasks to complete.")
        return

    list_tasks(active_tasks)

    raw_choice = input("Task number to complete: ").strip()

    try:
        task_number = int(raw_choice)
    except ValueError:
        print("Please enter a task number.")
        return

    if task_number < 1 or task_number > len(active_tasks):
        print("Choose a number from the active task list.")
        return

    task = active_tasks[task_number - 1]
    task.mark_complete()
    print(f"Completed {task.title}.")


def main():
    print("Personal Task Tracker")

    try:
        tasks = load_tasks(SAVE_PATH)
    except ValueError as error:
        print(f"Could not load saved tasks: {error}")
        tasks = []
    except OSError as error:
        print(f"Could not read the task file: {error}")
        tasks = []
    else:
        if tasks:
            print(f"Loaded {len(tasks)} task(s).")
        else:
            print("No saved tasks found yet.")

    while True:
        show_menu()
        choice = input("Choose an option: ").strip()

        if choice == "1":
            list_tasks(tasks)
        elif choice == "2":
            list_tasks(tasks, active_only=True)
        elif choice == "3":
            add_task_from_menu(tasks)
        elif choice == "4":
            complete_task_from_menu(tasks)
        elif choice == "5":
            try:
                save_tasks(tasks, SAVE_PATH)
            except OSError as error:
                print(f"Could not save tasks: {error}")
            else:
                print(f"Saved {len(tasks)} task(s) to {SAVE_PATH}.")
        elif choice == "6":
            try:
                tasks = load_tasks(SAVE_PATH)
            except ValueError as error:
                print(f"Could not load tasks: {error}")
            except OSError as error:
                print(f"Could not read the task file: {error}")
            else:
                if tasks:
                    print(f"Loaded {len(tasks)} task(s).")
                else:
                    print("No saved tasks found yet.")
        elif choice == "7":
            print("Goodbye.")
            break
        else:
            print("Choose a number from 1 to 7.")


if __name__ == "__main__":
    main()
```

## Try It Yourself

Run the app from the folder that contains `day-98`:

```bash
python day-98/task_tracker.py
```

If your computer uses `py`, use:

```bash
py day-98/task_tracker.py
```

If your computer uses `python3`, use:

```bash
python3 day-98/task_tracker.py
```

Try this menu path:

```text
3
Read JSON notes
Python
2026-05-12
25
3
Practice loops
Python

20
1
4
1
1
5
7
```

That means:

```text
add a task
add another task with no due date
list all tasks
complete the first active task
list all tasks again
save
quit
```

After saving, open:

```text
day-98/tasks.json
```

You should see a JSON list with your task data.

Run the app again.

It should load the saved tasks at startup.

## Common Mistake

A common mistake is trying to save task objects directly.

This will not work:

```python
tasks = [
    Task("Review functions", "Python", "2026-05-12", 30)
]

with open("day-98/tasks.json", "w", encoding="utf-8") as file:
    json.dump(tasks, file)
```

Python does not know how to turn a custom `Task` object into JSON by itself.

Save dictionaries instead:

```python
data = []

for task in tasks:
    data.append(task.to_dict())

with open("day-98/tasks.json", "w", encoding="utf-8") as file:
    json.dump(data, file, indent=4)
```

Another common mistake is completing a task by number from one list while using a different list.

For example, if the app shows only active tasks, the number should be checked against the active task list:

```python
active_tasks = get_active_tasks(tasks)
task = active_tasks[task_number - 1]
```

That is what today's code does.

The user sees the active list, so the user chooses from the active list.

## Debug It

Use these checks when the app does not behave the way you expect.

### Problem 1: The App Says There Are No Saved Tasks

Check whether this file exists:

```text
day-98/tasks.json
```

If it does not exist yet, that is normal before the first save.

Add a task, choose save, then check again.

### Problem 2: The JSON File Exists But Loading Fails

The file may not contain valid JSON.

For today's app, the top-level shape should be a list:

```json
[
    {
        "title": "Review functions",
        "subject": "Python",
        "due_date": "2026-05-12",
        "estimated_minutes": 30,
        "completed": false
    }
]
```

Common JSON mistakes:

- missing commas
- single quotes instead of double quotes
- `False` instead of `false`
- extra text before or after the JSON
- a dictionary at the top level instead of a list

### Problem 3: A Completed Task Still Appears

Completed tasks should still appear when you list all tasks.

That is intended.

They should not appear when you list active tasks.

Check which menu option you chose:

```text
1. List all tasks
2. List active tasks
```

### Problem 4: The App Does Not Save After Adding

In version 1, adding a task changes the task list in memory.

It does not write the JSON file until you choose:

```text
5. Save tasks
```

That separation helps you see saving clearly.

Day 99 can add automatic saving if you want the app to feel safer.

### Problem 5: A Number Input Returns To The Menu

If you type:

```text
twenty
```

for estimated minutes, the app prints a message and returns to the menu.

That comes from:

```python
return None
```

inside `ask_for_minutes()`.

The app does not crash because the menu action stops early.

## Read the Docs

Today, use the Python documentation to answer targeted questions.

[Python documentation: `json`](https://docs.python.org/3/library/json.html)

Look for:

- `json.dump()`
- `json.load()`
- `json.JSONDecodeError`

[Python documentation: `pathlib`](https://docs.python.org/3/library/pathlib.html)

Look for:

- `Path`
- `.exists()`
- `.open()`
- `.parent`
- `.mkdir()`

[Python documentation: classes](https://docs.python.org/3/tutorial/classes.html)

Look for:

- class definitions
- instance attributes
- methods
- class methods

Do not try to memorize the whole page.

Use the documentation to connect names from today's code to their official descriptions.

## Mini Challenge

Add a simple priority field.

Use three priority values:

```text
low
medium
high
```

Start by updating the `Task` class:

```python
def __init__(
    self,
    title,
    subject,
    due_date,
    estimated_minutes,
    completed=False,
    priority="medium"
):
    self.title = title
    self.subject = subject
    self.due_date = due_date
    self.estimated_minutes = estimated_minutes
    self.completed = completed
    self.priority = priority
```

Then update:

- `to_dict()`
- `from_dict()`
- `display_line()`
- `add_task_from_menu()`

Keep the validation simple:

```python
if priority not in ["low", "medium", "high"]:
    priority = "medium"
```

Do not rebuild the whole app.

Add one field carefully and test the save file.

## Real-World Use

Task trackers, study planners, issue trackers, and project boards all share the same core ideas.

They store records.

They show filtered views.

They let the user change the status of a record.

They save data somewhere outside the running program.

The storage can change:

```text
JSON file
CSV file
SQLite database
web API
cloud database
```

The beginner pattern still matters:

```text
define the data
load the data
change the data
show the data
save the data
handle bad input
```

Today's app uses the smallest useful version of that pattern.

That is exactly what a version 1 should be.

## Recap

Today you built the first version of a capstone project.

The app uses:

- a `Task` class for one task
- a list for many tasks
- dictionaries as the JSON bridge
- `json.dump()` to save tasks
- `json.load()` to load tasks
- a menu loop for user actions
- helper functions for listing, adding, completing, saving, and loading
- input checks for blank titles, bad numbers, and invalid menu choices
- file error handling for missing files, broken JSON, and read/write problems

The most important design choice was:

```text
Task objects while the app runs.
Dictionaries when saving or loading JSON.
```

That one choice keeps the app readable while still using a simple file format.

## Lesson Checklist

Before moving on, make sure you can:

- [ ] explain what data one task stores
- [ ] explain why this version uses a `Task` class
- [ ] explain why JSON needs dictionaries instead of custom objects
- [ ] write a `to_dict()` method
- [ ] write or read a `from_dict()` class method
- [ ] save a list of dictionaries with `json.dump()`
- [ ] load a list of dictionaries with `json.load()`
- [ ] handle a missing save file
- [ ] handle broken JSON with `json.JSONDecodeError`
- [ ] add a task from user input
- [ ] list all tasks
- [ ] list only active tasks
- [ ] complete a task by choosing a number
- [ ] explain why saving does not happen until the save option is chosen
- [ ] name at least two improvements for Day 99

## Exercises

### Exercise 1: Draw The Data Model

Write the data for one task as a text block.

Include:

```text
title
subject
due_date
estimated_minutes
completed
```

Then write the same task as a Python dictionary.

### Exercise 2: Explain The Class Choice

Answer in three or four sentences:

```text
Why does version 1 use a Task class instead of only dictionaries?
```

Your answer should mention:

- attributes
- methods
- JSON saving
- `to_dict()`

### Exercise 3: Add Two Tasks And Save

Run the app.

Add two tasks:

```text
Review functions
Practice file reading
```

Save the tasks.

Open `day-98/tasks.json` and check that both tasks are in the saved list.

### Exercise 4: Complete One Task

Run the app again.

Complete one active task.

List all tasks and active tasks.

Write one sentence explaining why the completed task appears in one list but not the other.

### Exercise 5: Test Bad Minute Input

Try adding a task with each bad value:

```text
zero
0
-5
ten
```

For each one, write the message the app shows.

Then add a valid task with:

```text
15
```

### Exercise 6: Break The JSON On Purpose

Make a copy of your working `tasks.json` first if you want to keep it.

Then put this invalid text in `day-98/tasks.json`:

```text
not json
```

Run the app.

Write down the loading message.

Then fix the file by saving again from the app or restoring your copied JSON.

### Exercise 7: Add A Count Summary

Add a function:

```python
def print_summary(tasks):
    active_count = 0
    completed_count = 0

    for task in tasks:
        if task.completed:
            completed_count += 1
        else:
            active_count += 1

    print(f"Active tasks: {active_count}")
    print(f"Completed tasks: {completed_count}")
```

Add a menu option that calls it.

### Exercise 8: Plan Day 99 Improvements

Choose three improvements for tomorrow.

Pick from this list or invent your own:

```text
edit a task
delete a task
sort by due date text
filter by subject
show total study minutes
auto-save after changes
warn before quitting with unsaved changes
add priorities
add a README
split the project into multiple files
add simple tests
```

For each improvement, write:

- why it helps the user
- which functions or data fields might change
- how you would test it by hand

## Tiny Win

You now have a capstone project that can remember real data.

It is still small enough to understand, but it already has the main parts of a useful command-line app:

```text
data model
user interface
saved file
error handling
repeatable workflow
```

That is a solid Day 98 result.

## Tomorrow

Tomorrow is:

```text
Day 99: Capstone Build Day 2
```

You will improve this project instead of starting over.

Good Day 99 directions include:

- edit existing tasks
- delete tasks
- add priorities
- filter by subject
- show total active study minutes
- save automatically after changes
- warn before quitting with unsaved changes
- split the app into multiple files
- add a small README
- add basic tests for the task and storage logic

Today you built the working core.

Tomorrow you will make it feel more like a finished tool.
