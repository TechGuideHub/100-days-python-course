# Day 99: Capstone Build Day 2

**Focus:** Improving the capstone task tracker with editing, deleting, searching, filtering, due dates, priorities, tests, and stronger error handling  
**You will practice:** working with lists of dictionaries, JSON storage, pure helper functions, validation, date parsing, search, filters, task updates, task deletion, simple `assert` tests, menu organization, and planning final polish  
**Estimated time:** 90-120 minutes

## Today's Goal

Today you will improve the capstone project.

Yesterday, you started a small task tracker. Today, you will turn it into a stronger version that feels closer to a real command-line tool.

The updated tracker will let the user:

- add tasks
- edit tasks
- delete tasks
- search tasks
- filter tasks by status, priority, and overdue state
- give tasks due dates
- give tasks priorities
- mark tasks done
- save tasks to JSON
- load tasks from JSON
- run simple tests for the helper functions

This lesson is self-contained enough that you can use the full code even if your Day 98 file is a little different.

By the end of this lesson, you should be able to:

- describe one task as a dictionary with clear fields
- validate task titles, dates, priorities, and statuses
- update a task without rewriting the whole program
- delete one task by id
- search task text across several fields
- filter tasks with simple rules
- keep input and printing separate from reusable logic where practical
- write small tests for functions that do not use `input()` or `print()`
- handle broken save files with friendly messages
- prepare your capstone for Day 100 review and polish

Today is a build day.

The goal is not to make the largest possible app.

The goal is to make a small app easier to use, easier to test, and easier to improve tomorrow.

## The Big Idea

A capstone project improves in layers.

The first version usually proves the main idea:

```text
I can create a task.
I can list tasks.
I can save tasks.
```

The second version starts making the app more useful:

```text
I can change a task after creating it.
I can remove a task I no longer need.
I can find a task without reading the whole list.
I can focus on the tasks that matter now.
I can test the rules without clicking through the menu.
```

That is today's work.

You will still keep the app beginner-friendly. It will use one main Python file and one small test file.

The important improvement is organization.

Some functions will handle pure task logic:

```text
make_task()
search_tasks()
filter_tasks()
update_task()
delete_task()
```

Those functions do not ask the user for input. They do not print. They receive values, do one job, and return a result.

That makes them easier to test.

Other functions will handle the command-line conversation:

```text
add_task_from_menu()
edit_task_from_menu()
delete_task_from_menu()
main()
```

Those functions are allowed to use `input()` and `print()` because their job is to talk to the user.

That split is the main project habit today.

## The Mental Model

Think of the program as three layers.

```text
task rules
  create, search, filter, edit, delete

storage
  load JSON, validate JSON, save JSON

menu
  ask the user what to do next
```

The task rules should be calm and reusable.

For example, `search_tasks()` should not care whether the search text came from:

- the keyboard
- a test
- a future web form
- a future command-line option

It only needs a list of tasks and a search query.

One task will look like this:

```python
{
    "id": 1,
    "title": "Finish capstone review",
    "status": "todo",
    "due_date": "2026-05-12",
    "priority": "high",
}
```

The fields have clear jobs:

```text
id          a number used to edit or delete the task
title       the human-readable task
status      todo or done
due_date    YYYY-MM-DD, or blank if there is no date
priority    low, medium, or high
```

The `id` matters because titles can change.

If the task is called:

```text
Finish notes
```

and you edit the title to:

```text
Finish project notes
```

the id can stay the same.

That gives the app a stable way to find one task.

## The Project

Create this folder:

```text
day-99
```

Inside it, create these files:

```text
day-99/task_tracker.py
day-99/test_task_tracker.py
```

The app will save task data here:

```text
day-99/tasks.json
```

Your finished project will have this shape:

```text
day-99/
  task_tracker.py
  test_task_tracker.py
  tasks.json
```

The `tasks.json` file will be created when the user saves. It does not need to exist before the first run.

The menu will look like this:

```text
Menu:
1. List tasks
2. Add task
3. Edit task
4. Delete task
5. Search tasks
6. Filter tasks
7. Mark task done
8. Save tasks
9. Load tasks
10. Quit
```

Example session:

```text
Task Tracker
No saved tasks found yet.

Menu:
1. List tasks
2. Add task
3. Edit task
4. Delete task
5. Search tasks
6. Filter tasks
7. Mark task done
8. Save tasks
9. Load tasks
10. Quit
Choose an option: 2
Task title: Finish capstone review
Due date (YYYY-MM-DD, optional): 2026-05-12
Priority (low/medium/high, default medium): high
Added task 1.

Menu:
1. List tasks
2. Add task
3. Edit task
4. Delete task
5. Search tasks
6. Filter tasks
7. Mark task done
8. Save tasks
9. Load tasks
10. Quit
Choose an option: 1

Tasks:
1. [todo] Finish capstone review | due: 2026-05-12 | priority: high
```

The exact tasks will depend on what the user types.

## Step-by-Step Build

Build this project in stages.

You can replace your Day 98 `task_tracker.py` with today's full version, or you can compare the pieces and copy over the parts you need.

Because many learners will have slightly different Day 98 files, this lesson gives the full updated code.

### Step 1: Name The Data Shape

Before writing menu code, decide what one task should contain.

Today, one task is a dictionary:

```python
{
    "id": 1,
    "title": "Finish capstone review",
    "status": "todo",
    "due_date": "2026-05-12",
    "priority": "high",
}
```

The app will store many tasks in a list:

```python
tasks = [
    {
        "id": 1,
        "title": "Finish capstone review",
        "status": "todo",
        "due_date": "2026-05-12",
        "priority": "high",
    },
    {
        "id": 2,
        "title": "Write simple tests",
        "status": "todo",
        "due_date": "",
        "priority": "medium",
    },
]
```

Notice that a task can have no due date.

In that case, the app stores an empty string:

```text
""
```

That keeps the JSON easy to read.

### Step 2: Add Validation Helpers

Validation functions protect the rest of the app.

For example:

```python
def validate_priority(raw_priority):
    priority = str(raw_priority).strip().lower()

    if priority == "":
        return "medium"

    if priority not in VALID_PRIORITIES:
        raise ValueError("Priority must be low, medium, or high.")

    return priority
```

This function gives the app one clear place to decide what priorities are allowed.

The menu does not need to repeat that rule every time.

### Step 3: Keep Date Parsing Small

Dates are easy to mistype.

The app will accept dates in this format:

```text
YYYY-MM-DD
```

Examples:

```text
2026-05-12
2026-10-01
2027-01-30
```

This is the function that checks the date:

```python
def parse_due_date(raw_due_date):
    clean = str(raw_due_date).strip()

    if clean == "":
        return ""

    try:
        parsed = date.fromisoformat(clean)
    except ValueError as error:
        raise ValueError("Use the date format YYYY-MM-DD.") from error

    return parsed.isoformat()
```

The blank date is allowed.

Anything else must be a real ISO-style date.

### Step 4: Add Pure Task Functions

The task functions do the project work:

```text
make_task()
find_task_by_id()
search_tasks()
filter_tasks()
update_task()
delete_task()
```

These are good candidates for tests because they do not depend on the user typing into the menu.

For example, `delete_task()` receives a list and an id:

```python
updated_tasks, deleted = delete_task(tasks, 2)
```

It returns:

```text
the new list of tasks
whether anything was deleted
```

That return value is easy to check with `assert`.

### Step 5: Add Storage

The storage functions handle JSON.

`save_tasks()` writes the list of dictionaries to a file.

`load_tasks()` reads the file, checks the shape, and normalizes older saved tasks if possible.

For example, if an older Day 98 task has no priority, today's loader gives it:

```text
medium
```

If an older saved task has no due date, today's loader gives it:

```text
""
```

That makes the upgrade smoother.

### Step 6: Add Menu Actions

The menu action functions talk to the user.

For example:

```python
def add_task_from_menu(tasks):
    title = input("Task title: ").strip()
    due_date = input("Due date (YYYY-MM-DD, optional): ").strip()
    priority = input("Priority (low/medium/high, default medium): ").strip()
```

This function gathers text from the user, then calls `make_task()` to do the validation and task creation.

That keeps the input code thin.

### Step 7: Add Tests

The test file will use plain `assert` statements.

This is enough for today.

You are not learning a full test framework here. You are practicing the test habit:

```text
give a function known input
check that it returns the right value
```

You will test:

- priority validation
- due date parsing
- task creation
- search
- filtering
- updating
- deleting
- overdue checks

### Step 8: Put The Full App Together

Put this code in:

```text
day-99/task_tracker.py
```

```python
import json
from datetime import date
from pathlib import Path


SAVE_PATH = Path("day-99/tasks.json")
VALID_PRIORITIES = ("low", "medium", "high")
VALID_STATUSES = ("todo", "done")


def clean_title(title):
    clean = str(title).strip()

    if clean == "":
        raise ValueError("Task title cannot be blank.")

    return clean


def parse_due_date(raw_due_date):
    clean = str(raw_due_date).strip()

    if clean == "":
        return ""

    try:
        parsed = date.fromisoformat(clean)
    except ValueError as error:
        raise ValueError("Use the date format YYYY-MM-DD.") from error

    return parsed.isoformat()


def validate_priority(raw_priority):
    priority = str(raw_priority).strip().lower()

    if priority == "":
        return "medium"

    if priority not in VALID_PRIORITIES:
        raise ValueError("Priority must be low, medium, or high.")

    return priority


def validate_status(raw_status):
    status = str(raw_status).strip().lower()

    if status == "":
        return "todo"

    if status not in VALID_STATUSES:
        raise ValueError("Status must be todo or done.")

    return status


def next_task_id(tasks):
    highest_id = 0

    for task in tasks:
        task_id = int(task["id"])

        if task_id > highest_id:
            highest_id = task_id

    return highest_id + 1


def make_task(tasks, title, due_date="", priority="medium"):
    return {
        "id": next_task_id(tasks),
        "title": clean_title(title),
        "status": "todo",
        "due_date": parse_due_date(due_date),
        "priority": validate_priority(priority),
    }


def find_task_by_id(tasks, task_id):
    for task in tasks:
        if task["id"] == task_id:
            return task

    return None


def search_tasks(tasks, query):
    clean_query = str(query).strip().lower()

    if clean_query == "":
        return []

    matches = []

    for task in tasks:
        searchable_text = " ".join(
            [
                str(task["id"]),
                task["title"],
                task["status"],
                task["due_date"],
                task["priority"],
            ]
        ).lower()

        if clean_query in searchable_text:
            matches.append(task)

    return matches


def is_overdue(task, today=None):
    if today is None:
        today = date.today()

    if task["status"] == "done":
        return False

    if task["due_date"] == "":
        return False

    return date.fromisoformat(task["due_date"]) < today


def filter_tasks(tasks, status_filter="all", priority_filter="all", overdue_only=False, today=None):
    status_filter = str(status_filter).strip().lower() or "all"
    priority_filter = str(priority_filter).strip().lower() or "all"
    matches = []

    allowed_statuses = ("all",) + VALID_STATUSES
    allowed_priorities = ("all",) + VALID_PRIORITIES

    if status_filter not in allowed_statuses:
        raise ValueError("Status filter must be all, todo, or done.")

    if priority_filter not in allowed_priorities:
        raise ValueError("Priority filter must be all, low, medium, or high.")

    for task in tasks:
        if status_filter != "all" and task["status"] != status_filter:
            continue

        if priority_filter != "all" and task["priority"] != priority_filter:
            continue

        if overdue_only and not is_overdue(task, today):
            continue

        matches.append(task)

    return matches


def update_task(tasks, task_id, title=None, due_date=None, priority=None, status=None):
    new_title = clean_title(title) if title is not None else None
    new_due_date = parse_due_date(due_date) if due_date is not None else None
    new_priority = validate_priority(priority) if priority is not None else None
    new_status = validate_status(status) if status is not None else None

    updated_tasks = []
    updated = False

    for task in tasks:
        task_copy = task.copy()

        if task_copy["id"] == task_id:
            if new_title is not None:
                task_copy["title"] = new_title

            if new_due_date is not None:
                task_copy["due_date"] = new_due_date

            if new_priority is not None:
                task_copy["priority"] = new_priority

            if new_status is not None:
                task_copy["status"] = new_status

            updated = True

        updated_tasks.append(task_copy)

    return updated_tasks, updated


def delete_task(tasks, task_id):
    remaining_tasks = []
    deleted = False

    for task in tasks:
        if task["id"] == task_id:
            deleted = True
        else:
            remaining_tasks.append(task.copy())

    return remaining_tasks, deleted


def task_sort_key(task):
    status_rank = {"todo": 0, "done": 1}
    priority_rank = {"high": 0, "medium": 1, "low": 2}
    due_date = task["due_date"] or "9999-12-31"

    return (
        status_rank[task["status"]],
        priority_rank[task["priority"]],
        due_date,
        task["title"].lower(),
    )


def format_task_line(task):
    due_text = task["due_date"] if task["due_date"] else "no due date"
    return (
        f"{task['id']}. [{task['status']}] {task['title']} "
        f"| due: {due_text} | priority: {task['priority']}"
    )


def load_tasks(path=SAVE_PATH):
    path = Path(path)

    if not path.exists():
        return []

    try:
        with path.open("r", encoding="utf-8") as file:
            data = json.load(file)
    except json.JSONDecodeError as error:
        raise ValueError("The save file is not valid JSON.") from error

    if not isinstance(data, list):
        raise ValueError("The save file should contain a list of tasks.")

    loaded_tasks = []
    seen_ids = set()

    for record in data:
        if not isinstance(record, dict):
            raise ValueError("Each saved task should be a dictionary.")

        try:
            task_id = int(record["id"])
            title = clean_title(record["title"])
            status = validate_status(record.get("status", "todo"))
            due_date = parse_due_date(record.get("due_date", ""))
            priority = validate_priority(record.get("priority", "medium"))
        except (KeyError, TypeError, ValueError) as error:
            raise ValueError("One saved task has missing or invalid fields.") from error

        if task_id <= 0:
            raise ValueError("Task ids must be positive numbers.")

        if task_id in seen_ids:
            raise ValueError("The save file contains a duplicate task id.")

        seen_ids.add(task_id)

        loaded_tasks.append(
            {
                "id": task_id,
                "title": title,
                "status": status,
                "due_date": due_date,
                "priority": priority,
            }
        )

    return loaded_tasks


def save_tasks(tasks, path=SAVE_PATH):
    path = Path(path)
    path.parent.mkdir(parents=True, exist_ok=True)

    with path.open("w", encoding="utf-8") as file:
        json.dump(tasks, file, indent=4)


def ask_for_task_id(prompt):
    raw_id = input(prompt).strip()

    try:
        task_id = int(raw_id)
    except ValueError:
        print("Please enter a whole number for the task id.")
        return None

    if task_id <= 0:
        print("Task id must be a positive number.")
        return None

    return task_id


def show_menu():
    print()
    print("Menu:")
    print("1. List tasks")
    print("2. Add task")
    print("3. Edit task")
    print("4. Delete task")
    print("5. Search tasks")
    print("6. Filter tasks")
    print("7. Mark task done")
    print("8. Save tasks")
    print("9. Load tasks")
    print("10. Quit")


def print_tasks(tasks, heading="Tasks"):
    if not tasks:
        print("No tasks to show.")
        return

    print()
    print(f"{heading}:")

    for task in sorted(tasks, key=task_sort_key):
        print(format_task_line(task))


def add_task_from_menu(tasks):
    title = input("Task title: ").strip()
    due_date = input("Due date (YYYY-MM-DD, optional): ").strip()
    priority = input("Priority (low/medium/high, default medium): ").strip()

    try:
        task = make_task(tasks, title, due_date, priority)
    except ValueError as error:
        print(error)
        return tasks

    print(f"Added task {task['id']}.")
    return tasks + [task]


def edit_task_from_menu(tasks):
    task_id = ask_for_task_id("Task id to edit: ")

    if task_id is None:
        return tasks

    task = find_task_by_id(tasks, task_id)

    if task is None:
        print("No task found with that id.")
        return tasks

    print("Current task:")
    print(format_task_line(task))

    title = input("New title (Enter to keep): ").strip()
    due_date = input("New due date (YYYY-MM-DD, '-' to clear, Enter to keep): ").strip()
    priority = input("New priority (low/medium/high, Enter to keep): ").strip()
    status = input("New status (todo/done, Enter to keep): ").strip()

    title_update = title if title != "" else None

    if due_date == "":
        due_date_update = None
    elif due_date == "-":
        due_date_update = ""
    else:
        due_date_update = due_date

    priority_update = priority if priority != "" else None
    status_update = status if status != "" else None

    try:
        updated_tasks, updated = update_task(
            tasks,
            task_id,
            title=title_update,
            due_date=due_date_update,
            priority=priority_update,
            status=status_update,
        )
    except ValueError as error:
        print(error)
        return tasks

    if updated:
        print("Updated task.")
        return updated_tasks

    print("No task found with that id.")
    return tasks


def delete_task_from_menu(tasks):
    task_id = ask_for_task_id("Task id to delete: ")

    if task_id is None:
        return tasks

    task = find_task_by_id(tasks, task_id)

    if task is None:
        print("No task found with that id.")
        return tasks

    print("Task to delete:")
    print(format_task_line(task))

    confirm = input("Delete this task? (y/n): ").strip().lower()

    if confirm != "y":
        print("Delete canceled.")
        return tasks

    updated_tasks, deleted = delete_task(tasks, task_id)

    if deleted:
        print("Deleted task.")
        return updated_tasks

    print("No task found with that id.")
    return tasks


def search_tasks_from_menu(tasks):
    query = input("Search text: ").strip()

    if query == "":
        print("Search text cannot be blank.")
        return

    matches = search_tasks(tasks, query)
    print_tasks(matches, "Search results")


def filter_tasks_from_menu(tasks):
    status = input("Status (all/todo/done): ").strip() or "all"
    priority = input("Priority (all/low/medium/high): ").strip() or "all"
    overdue_answer = input("Only overdue tasks? (y/n): ").strip().lower()
    overdue_only = overdue_answer == "y"

    try:
        matches = filter_tasks(tasks, status, priority, overdue_only)
    except ValueError as error:
        print(error)
        return

    print_tasks(matches, "Filtered tasks")


def mark_task_done_from_menu(tasks):
    task_id = ask_for_task_id("Task id to mark done: ")

    if task_id is None:
        return tasks

    updated_tasks, updated = update_task(tasks, task_id, status="done")

    if updated:
        print("Marked task done.")
        return updated_tasks

    print("No task found with that id.")
    return tasks


def main():
    tasks = []

    print("Task Tracker")

    try:
        tasks = load_tasks()
    except ValueError as error:
        print(f"Could not load saved tasks: {error}")
    except OSError as error:
        print(f"Could not read the task file: {error}")
    else:
        if tasks:
            print(f"Loaded {len(tasks)} task(s).")
        else:
            print("No saved tasks found yet.")

    while True:
        show_menu()
        choice = input("Choose an option: ").strip()

        if choice == "1":
            print_tasks(tasks)
        elif choice == "2":
            tasks = add_task_from_menu(tasks)
        elif choice == "3":
            tasks = edit_task_from_menu(tasks)
        elif choice == "4":
            tasks = delete_task_from_menu(tasks)
        elif choice == "5":
            search_tasks_from_menu(tasks)
        elif choice == "6":
            filter_tasks_from_menu(tasks)
        elif choice == "7":
            tasks = mark_task_done_from_menu(tasks)
        elif choice == "8":
            try:
                save_tasks(tasks)
            except OSError as error:
                print(f"Could not save tasks: {error}")
            else:
                print(f"Saved {len(tasks)} task(s) to {SAVE_PATH}.")
        elif choice == "9":
            try:
                tasks = load_tasks()
            except ValueError as error:
                print(f"Could not load tasks: {error}")
            except OSError as error:
                print(f"Could not read the task file: {error}")
            else:
                print(f"Loaded {len(tasks)} task(s).")
        elif choice == "10":
            print("Goodbye.")
            break
        else:
            print("Choose a number from 1 to 10.")


if __name__ == "__main__":
    main()
```

### Step 9: Add The Test File

Put this code in:

```text
day-99/test_task_tracker.py
```

```python
from datetime import date

from task_tracker import (
    delete_task,
    filter_tasks,
    is_overdue,
    make_task,
    parse_due_date,
    search_tasks,
    update_task,
    validate_priority,
)


def assert_raises_value_error(function, *args):
    try:
        function(*args)
    except ValueError:
        return

    raise AssertionError("ValueError was not raised")


def run_tests():
    assert validate_priority("HIGH") == "high"
    assert validate_priority("") == "medium"
    assert parse_due_date("") == ""
    assert parse_due_date("2026-05-12") == "2026-05-12"
    assert_raises_value_error(parse_due_date, "05/12/2026")

    tasks = []
    first = make_task(tasks, "Plan capstone review", "2026-05-12", "high")
    tasks = tasks + [first]
    second = make_task(tasks, "Write simple tests", "", "low")
    tasks = tasks + [second]

    assert first["id"] == 1
    assert second["id"] == 2
    assert search_tasks(tasks, "tests")[0]["title"] == "Write simple tests"
    assert filter_tasks(tasks, priority_filter="high")[0]["id"] == 1

    updated_tasks, updated = update_task(
        tasks,
        1,
        title="Plan final review",
        status="done",
    )

    assert updated is True
    assert updated_tasks[0]["title"] == "Plan final review"
    assert updated_tasks[0]["status"] == "done"
    assert tasks[0]["status"] == "todo"

    remaining_tasks, deleted = delete_task(updated_tasks, 2)

    assert deleted is True
    assert len(remaining_tasks) == 1
    assert is_overdue(
        {
            "id": 3,
            "title": "Submit project",
            "status": "todo",
            "due_date": "2026-05-09",
            "priority": "high",
        },
        today=date(2026, 5, 10),
    )
    assert not is_overdue(
        {
            "id": 4,
            "title": "Finished task",
            "status": "done",
            "due_date": "2026-05-09",
            "priority": "high",
        },
        today=date(2026, 5, 10),
    )

    overdue_matches = filter_tasks(
        [
            {
                "id": 5,
                "title": "Late draft",
                "status": "todo",
                "due_date": "2026-05-09",
                "priority": "medium",
            },
            {
                "id": 6,
                "title": "Future draft",
                "status": "todo",
                "due_date": "2026-05-11",
                "priority": "medium",
            },
        ],
        overdue_only=True,
        today=date(2026, 5, 10),
    )

    assert len(overdue_matches) == 1
    assert overdue_matches[0]["title"] == "Late draft"


if __name__ == "__main__":
    run_tests()
    print("All tests passed.")
```

### Step 10: Run The Tests First

Run the test file:

```bash
python day-99/test_task_tracker.py
```

If your computer uses `py`, use:

```bash
py day-99/test_task_tracker.py
```

If your computer uses `python3`, use:

```bash
python3 day-99/test_task_tracker.py
```

You should see:

```text
All tests passed.
```

If a test fails, fix that before using the menu.

The tests check the reusable rules. The menu is easier to trust when the rule functions already work.

### Step 11: Run The App

Run the app:

```bash
python day-99/task_tracker.py
```

Try this path:

```text
2
Finish capstone review
2026-05-12
high
2
Write simple tests

medium
1
5
tests
6
todo
high
n
7
1
1
8
10
```

That means:

```text
add a high priority task
add a medium priority task with no due date
list tasks
search for tests
filter todo high priority tasks
mark task 1 done
list again
save
quit
```

Then run the app again.

It should load the saved tasks from:

```text
day-99/tasks.json
```

## Try It Yourself

After the full code works, test the features like a user.

Try these short task examples:

```text
Title: Finish capstone review
Due date: 2026-05-12
Priority: high
```

```text
Title: Add README notes
Due date:
Priority:
```

```text
Title: Clean up old experiments
Due date: 2026-05-09
Priority: low
```

The blank priority should become:

```text
medium
```

The blank due date should display as:

```text
no due date
```

Now try invalid inputs:

```text
blank title
priority: urgent
date: 12/05/2026
task id: abc
task id: -4
```

The program should print a friendly message and return to the menu.

It should not crash.

## Common Mistake

A common mistake is putting all the logic directly inside the menu.

For example, this is tempting:

```python
elif choice == "5":
    query = input("Search text: ")
    for task in tasks:
        if query in task["title"]:
            print(task)
```

That can work for a tiny script, but it makes testing harder.

This version is easier to test:

```python
def search_tasks(tasks, query):
    clean_query = str(query).strip().lower()

    if clean_query == "":
        return []

    matches = []

    for task in tasks:
        if clean_query in task["title"].lower():
            matches.append(task)

    return matches
```

Then the menu can call the function:

```python
matches = search_tasks(tasks, query)
print_tasks(matches, "Search results")
```

The split gives you two benefits:

- the menu stays easier to read
- the search rule can be tested without typing through the menu

Another common mistake is using the task title as the only way to edit or delete.

Titles can change. Two tasks can also have similar titles.

Use the task id for edit and delete actions:

```text
Task id to edit: 3
Task id to delete: 3
```

That is why every task has an `id`.

## Debug It

Use these checks when the project does not behave.

### Problem 1: The Test File Opens The App Menu

If running the test file starts the menu, check the bottom of `task_tracker.py`.

It should use this guard:

```python
if __name__ == "__main__":
    main()
```

That line means:

```text
Run the menu only when task_tracker.py is started directly.
```

When the test file imports functions from `task_tracker.py`, the menu should not start.

### Problem 2: A Date Fails

The accepted date format is:

```text
YYYY-MM-DD
```

This works:

```text
2026-05-12
```

This does not:

```text
05/12/2026
```

The app uses:

```python
date.fromisoformat(clean)
```

That function expects the ISO date shape.

### Problem 3: Search Finds Too Much Or Too Little

Search checks more than the title.

It checks:

```text
id
title
status
due_date
priority
```

So searching for:

```text
high
```

can find every high priority task.

Searching for:

```text
done
```

can find completed tasks.

That is intentional.

If you only want title search later, change `search_tasks()` so it checks only:

```python
task["title"]
```

### Problem 4: Delete Seems To Do Nothing

The delete feature asks for confirmation:

```text
Delete this task? (y/n):
```

Only `y` deletes the task.

Typing anything else cancels the delete.

That is a small safety check because deletion removes data from the current list.

The task is not removed from `tasks.json` until you save.

### Problem 5: Loading Removes Unsaved Work

The load option replaces the current task list with the saved file.

That means this sequence can lose unsaved changes:

```text
add a task
choose load before saving
```

For today's version, that is acceptable.

Day 100 is a good place to add a warning such as:

```text
You have unsaved changes. Load anyway?
```

## Read the Docs

Today, use documentation to answer narrow questions.

Python `datetime` documentation:

[Python documentation: `datetime`](https://docs.python.org/3/library/datetime.html)

Look for:

- `date`
- `date.today()`
- `date.fromisoformat()`
- `.isoformat()`

Python `json` documentation:

[Python documentation: `json`](https://docs.python.org/3/library/json.html)

Look for:

- `json.load()`
- `json.dump()`
- `json.JSONDecodeError`

Python `pathlib` documentation:

[Python documentation: `pathlib`](https://docs.python.org/3/library/pathlib.html)

Look for:

- `Path`
- `.exists()`
- `.open()`
- `.parent`
- `.mkdir()`

Python tutorial section on errors:

[Python documentation: Errors and Exceptions](https://docs.python.org/3/tutorial/errors.html)

Look for:

- `try`
- `except`
- `raise`
- `ValueError`

Do not try to memorize all of these pages.

Use them to answer the questions this project raises.

## Mini Challenge

Add a due-today filter.

Start with this pure function:

```python
def is_due_today(task, today=None):
    if today is None:
        today = date.today()

    if task["status"] == "done":
        return False

    if task["due_date"] == "":
        return False

    return date.fromisoformat(task["due_date"]) == today
```

Then add one test:

```python
assert is_due_today(
    {
        "id": 7,
        "title": "Practice final demo",
        "status": "todo",
        "due_date": "2026-05-10",
        "priority": "high",
    },
    today=date(2026, 5, 10),
)
```

After the function and test work, decide where the feature belongs in the menu.

One simple option is to add a new menu choice:

```text
11. Show due today
```

Do not add ten features at once.

Add one small feature, test the pure rule, then connect it to the menu.

## Real-World Use

Task apps are common because the basic problem is everywhere.

People need to track:

- assignments
- support tickets
- chores
- repairs
- project steps
- follow-up messages
- review tasks

Real task systems may use databases, accounts, web pages, notifications, and calendars.

But the beginner core is still recognizable:

```text
one task
many tasks
add
edit
delete
search
filter
save
load
test the rules
```

The capstone is not only about tasks.

It is about seeing how a project grows without becoming one giant tangle.

That habit transfers to many other projects.

## Recap

Today you improved the capstone task tracker.

You added:

- task ids
- due dates
- priorities
- editing
- deleting
- searching
- filtering
- overdue checks
- JSON validation
- tests for pure helper functions

You also practiced a cleaner project shape:

```text
rules first
storage second
menu last
```

The most important idea:

```text
Put reusable rules in functions that can be tested without the menu.
```

That makes tomorrow's final polish much easier.

## Lesson Checklist

Before moving on, make sure you can:

- explain the fields in one task dictionary
- explain why each task has an id
- validate a blank title before saving it
- validate a due date with `date.fromisoformat()`
- use `low`, `medium`, and `high` as priority values
- edit one task by id
- delete one task by id
- search tasks by text
- filter tasks by status and priority
- explain what an overdue task means
- save tasks to JSON
- load tasks from JSON
- explain why `test_task_tracker.py` can import `task_tracker.py` without starting the menu
- write a simple `assert` test for a pure function

## Exercises

### Exercise 1: Add A Created Date

Add a new field:

```text
created_date
```

When a task is created, store today's date:

```python
date.today().isoformat()
```

Update:

- `make_task()`
- `load_tasks()`
- `format_task_line()`
- the tests

For older saved tasks, use a blank created date or today's date. Choose one and write down why.

### Exercise 2: Add A Reopen Option

Add a menu option that changes a done task back to todo.

You already have most of the logic:

```python
updated_tasks, updated = update_task(tasks, task_id, status="todo")
```

Build a small menu function around it.

### Exercise 3: Add Title-Only Search

Right now, search checks several fields.

Write a new function:

```python
def search_titles(tasks, query):
```

It should return only tasks whose title contains the query.

Add at least two tests:

- one that finds a title
- one that returns an empty list

### Exercise 4: Improve Priority Sorting

The current sort shows:

```text
todo tasks before done tasks
high priority before medium and low
earlier due dates before later due dates
```

Change the sort so tasks with due dates always appear before tasks without due dates.

Then test with three tasks:

- one high priority with no due date
- one medium priority due tomorrow
- one low priority due today

Decide which order feels most useful.

### Exercise 5: Warn Before Loading

Add a confirmation prompt before loading saved tasks from the menu:

```text
Loading will replace the current list. Continue? (y/n):
```

Only load if the user types `y`.

This is good Day 100 polish practice.

### Exercise 6: Add Autosave On Quit

When the user chooses quit, ask:

```text
Save before quitting? (y/n):
```

If the user types `y`, call `save_tasks(tasks)` before saying goodbye.

Handle `OSError` the same way the save menu option does.

### Exercise 7: Add A README Draft

Create a short README for your capstone.

Include:

- project name
- what the app does
- how to run the app
- how to run the tests
- where tasks are saved
- one known limitation

Keep it short.

Day 100 will polish this.

### Exercise 8: Write A Manual Test Plan

Write five manual test cases.

Use this format:

```text
Case:
Steps:
Result:
```

Include at least one invalid input case.

Good candidates:

- add a blank title
- edit a task date
- delete a task and cancel
- filter high priority tasks
- save, quit, and load again

## Tiny Win

You turned a first capstone draft into a project with real editing power.

The app can now change, remove, find, and focus tasks.

Just as important, the code has testable rules.

That means tomorrow is not a scramble to make everything work at once.

You now have something you can review, polish, and explain.

## Tomorrow

Tomorrow is:

```text
Day 100: Capstone Polish, Review, And Demo
```

You will slow down and make the project presentable.

Good Day 100 work might include:

- running the tests
- fixing rough messages
- adding a README
- checking the save file behavior
- cleaning up unused code
- adding one small final feature
- writing a short demo script
- reflecting on what you built across the course

Do not plan a huge rewrite for Day 100.

The final day is for making the capstone clear, reliable, and explainable.
