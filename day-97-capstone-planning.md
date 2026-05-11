# Day 97: Capstone Planning

**Focus:** Turning your final project idea into a buildable beginner capstone  
**You will practice:** choosing a project, limiting features, sketching a data model, planning files, naming functions or classes, designing a CLI or menu, writing test ideas, creating milestones, and preparing a small first version for Day 98  
**Estimated time:** 70-90 minutes

## Today's Goal

Today you will plan your capstone project.

You are not building it yet.

That matters.

The last few days of this course are where many beginners feel pulled in two directions:

```text
I want the final project to feel real.
I also do not want it to become too large to finish.
```

The answer is not to make a giant app.

The answer is to make a small practical tool that is complete enough to use, easy enough to explain, and organized enough that you can keep improving it.

For this capstone, choose one of these projects:

```text
Personal Task Tracker
Study Planner
```

Both projects are useful.

Both can be built with the Python skills you already have:

- dictionaries
- lists
- functions
- files
- JSON
- simple command-line input
- basic tests
- small project organization
- Git commits

By the end of today, you should have a written plan that answers:

- which project you are building
- who the program is for
- what the small first version does
- which features belong in version 1
- which features can wait
- what data your program stores
- which files your project will have
- which functions or classes you plan to write
- what the menu or commands look like
- how you will save data
- which tests you will write first
- what you will build on Days 98, 99, and 100

Create this planning file today:

```text
day-97/capstone_plan.md
```

Do not write the full project today.

Your goal is to make tomorrow easier.

## The Big Idea

A capstone project does not need to be large to be impressive.

It needs to be clear.

A good beginner capstone has these qualities:

- it solves a recognizable problem
- it has a small but useful first version
- it stores real data
- it lets a user perform more than one action
- it is split into understandable files
- it has a few tests for important logic
- it can be explained in a few sentences

That is enough.

The final project is not a test of how many features you can cram into one folder.

It is a chance to show that you can take an idea and guide it through a complete beginner development process:

```text
idea
plan
small version
organized code
tests
polish
```

Planning is the first real project step.

If your plan is clear, Day 98 becomes less mysterious.

Instead of asking:

```text
What should I code?
```

you will ask:

```text
What is the next small part of the plan?
```

That is a much easier question.

## The Mental Model

Think of the capstone as a stack of decisions.

Each decision supports the next one.

```text
Project choice
  What problem am I solving?

User goal
  What should the program help someone do?

Small first version
  What is the smallest useful version?

Data model
  What information needs to be stored?

Actions
  What can the user do with that data?

Files
  Where will each kind of code live?

Tests
  Which rules can I check automatically?

Milestones
  What gets built on each remaining day?
```

Do not start with files.

Start with the user goal.

Files are just containers for the decisions above them.

For example, a task tracker might start with this goal:

```text
Help me keep a short list of tasks, mark tasks as done, and save the list between runs.
```

That goal suggests data:

```text
task id
title
status
due date
notes
```

That data suggests actions:

```text
add a task
list tasks
mark a task done
delete a task
save tasks
load tasks
```

Those actions suggest functions:

```text
add_task()
list_tasks()
mark_task_done()
delete_task()
save_tasks()
load_tasks()
```

Those functions suggest files:

```text
main.py
tasks.py
storage.py
tests/test_tasks.py
```

One decision leads to the next.

That is the planning rhythm.

## Choose Your Capstone

Pick one project today.

Do not try to combine both.

A focused project is easier to finish and easier to explain.

### Option 1: Personal Task Tracker

A Personal Task Tracker helps a user manage everyday tasks.

The user might want to track:

- homework
- chores
- errands
- personal reminders
- small project steps

A simple version could let the user:

- add a task
- list all tasks
- list only unfinished tasks
- mark a task as done
- delete a task
- save tasks to a JSON file
- load tasks when the program starts

This project is a good fit if you like practical tools and simple status changes.

The main idea is:

```text
Keep a list of tasks and update their status over time.
```

### Option 2: Study Planner

A Study Planner helps a learner organize study sessions or topics.

The user might want to track:

- subjects
- topics
- study dates
- time estimates
- priority
- whether a topic is finished

A simple version could let the user:

- add a study item
- list upcoming study items
- mark an item complete
- filter by subject
- show high-priority items
- save the plan to a JSON file
- load the plan when the program starts

This project is a good fit if you want the final project to connect directly to learning habits.

The main idea is:

```text
Keep a study list organized by subject, date, and completion status.
```

### How To Choose

Choose the project you can imagine actually using.

Use this quick decision table:

| If you want to build... | Choose... |
| --- | --- |
| A general daily tool | Personal Task Tracker |
| A school or learning tool | Study Planner |
| A project with simple statuses | Personal Task Tracker |
| A project with subjects and priorities | Study Planner |
| The most direct capstone path | Personal Task Tracker |
| A slightly more specific personal tool | Study Planner |

There is no wrong choice here.

The wrong move is trying to build both at once.

## Define The User

Before features, name the user.

Not a huge audience.

One person.

For example:

```text
This task tracker is for a student who wants to remember small assignments and errands.
```

Or:

```text
This study planner is for a beginner learning Python who wants to organize topics across the week.
```

This sentence helps you reject features that do not belong.

If your user is a beginner student, you probably do not need:

- team accounts
- cloud syncing
- password login
- calendar invites
- email reminders
- charts
- a web dashboard

Those are interesting features.

They are not needed for this capstone.

Write the user sentence in your plan:

```text
User:
This project is for ...
```

Then write the main goal:

```text
Goal:
The program helps the user ...
```

Keep both sentences short.

## Choose Version 1 Features

A capstone plan needs boundaries.

Use four buckets:

```text
Must have
Should have
Could have
Will not build now
```

The buckets protect you from building sideways.

Here is a feature plan for the Personal Task Tracker:

| Bucket | Features |
| --- | --- |
| Must have | add task, list tasks, mark task done, save and load JSON |
| Should have | delete task, filter unfinished tasks |
| Could have | edit task title, due dates, priority |
| Will not build now | login, reminders, web interface, recurring tasks |

Here is a feature plan for the Study Planner:

| Bucket | Features |
| --- | --- |
| Must have | add study item, list items, mark complete, save and load JSON |
| Should have | filter by subject, show incomplete items |
| Could have | priority, study date, estimated minutes |
| Will not build now | calendar syncing, charts, spaced repetition system |

Your version 1 should mostly come from the "Must have" bucket.

The "Should have" bucket is useful if Day 99 goes smoothly.

The "Could have" bucket is for polish only.

The "Will not build now" bucket is not a failure.

It is a promise to finish the core project first.

## The Small First Version

The small first version is the first project that deserves to exist.

It is smaller than your full idea, but it still does something useful.

For the Personal Task Tracker, the small first version could be:

```text
The user can add tasks, list tasks, mark a task done, and save tasks to a JSON file.
```

For the Study Planner, the small first version could be:

```text
The user can add study items, list study items, mark an item complete, and save items to a JSON file.
```

That is enough for Day 98.

Notice what is missing:

- editing
- sorting
- search
- pretty colors
- reminders
- advanced date handling
- multiple users

You can add some of those later if the core works.

But the small first version should work without them.

In your plan, write:

```text
Small first version:
By the end of Day 98, the program should be able to ...
```

Be specific.

Avoid:

```text
Make a useful task app.
```

Prefer:

```text
Let the user add a task, list all tasks, mark one task as done, and keep the list in tasks.json.
```

Specific plans are easier to build.

## Data Model

The data model is the shape of the information your program stores.

For this capstone, keep the data model simple.

A list of dictionaries is enough.

You do not need a database.

You do not need a complicated class system.

You can use classes if they help you think clearly, but dictionaries are perfectly fine for this beginner capstone.

### Task Tracker Data

A task can be a dictionary:

```python
task = {
    "id": 1,
    "title": "Finish math worksheet",
    "status": "todo",
    "due_date": "2026-05-18",
    "notes": "Review fractions first",
}
```

The whole task list can be:

```text
[
  task dictionary,
  task dictionary,
  task dictionary
]
```

Useful fields:

| Field | Type | Purpose |
| --- | --- | --- |
| `id` | integer | Finds one task later |
| `title` | string | Describes the task |
| `status` | string | Tracks `todo` or `done` |
| `due_date` | string | Stores a simple date such as `2026-05-18` |
| `notes` | string | Stores optional details |

You can skip `due_date` and `notes` in the smallest version if they slow you down.

The required fields can be:

```text
id
title
status
```

### Study Planner Data

A study item can be a dictionary:

```python
study_item = {
    "id": 1,
    "subject": "Python",
    "topic": "JSON files",
    "status": "planned",
    "study_date": "2026-05-19",
    "priority": "high",
}
```

Useful fields:

| Field | Type | Purpose |
| --- | --- | --- |
| `id` | integer | Finds one study item later |
| `subject` | string | Groups items by class or skill |
| `topic` | string | Describes what to study |
| `status` | string | Tracks `planned` or `complete` |
| `study_date` | string | Stores a simple planned date |
| `priority` | string | Tracks `low`, `medium`, or `high` |

The required fields can be:

```text
id
subject
topic
status
```

### Keep IDs Simple

An `id` helps the user choose one item from a list.

For a beginner project, a simple ID rule is enough:

```text
New id = one more than the largest existing id.
```

Example:

```text
Existing ids: 1, 2, 3
Next id: 4
```

If the list is empty:

```text
Next id: 1
```

This rule is easy to test.

It also avoids relying on list positions.

List positions can change when you delete items.

IDs are more stable.

## Files And Folders

Your capstone should have a small project structure.

Use this as a starting point:

```text
capstone/
  README.md
  main.py
  data/
    tasks.json
  src/
    tasks.py
    storage.py
  tests/
    test_tasks.py
```

If you choose the Study Planner, rename the files:

```text
capstone/
  README.md
  main.py
  data/
    study_items.json
  src/
    planner.py
    storage.py
  tests/
    test_planner.py
```

This is a plan, not a command you need to run today.

Write the file tree in `day-97/capstone_plan.md`.

Then write the job of each file.

For the task tracker:

| File | Job |
| --- | --- |
| `README.md` | Explains the project and how to run it |
| `main.py` | Handles the menu or command-line flow |
| `data/tasks.json` | Stores the user's task data |
| `src/tasks.py` | Holds task rules such as adding and completing tasks |
| `src/storage.py` | Loads and saves JSON data |
| `tests/test_tasks.py` | Tests task rules |

For the study planner:

| File | Job |
| --- | --- |
| `README.md` | Explains the project and how to run it |
| `main.py` | Handles the menu or command-line flow |
| `data/study_items.json` | Stores the user's study data |
| `src/planner.py` | Holds study item rules |
| `src/storage.py` | Loads and saves JSON data |
| `tests/test_planner.py` | Tests planner rules |

Keep the structure small.

If a file has no clear job, do not add it yet.

## Functions And Classes

Planning functions before coding helps you avoid one giant `main.py`.

Start by listing actions.

Then turn those actions into function names.

### Personal Task Tracker Function Plan

Possible functions:

```python
def get_next_id(items):
    pass


def add_task(tasks, title, due_date="", notes=""):
    pass


def find_task_by_id(tasks, task_id):
    pass


def mark_task_done(tasks, task_id):
    pass


def delete_task(tasks, task_id):
    pass
```

Those are not the full implementation.

They are names for the jobs your code will need.

The important part today is deciding:

- what each function receives
- what each function returns
- whether the function changes the list
- what should happen if the ID does not exist

Example planning table:

| Function | Receives | Returns | Job |
| --- | --- | --- | --- |
| `get_next_id` | list of items | integer | Finds the next available ID |
| `add_task` | list, title, optional details | new task or updated list | Adds one task |
| `find_task_by_id` | list, ID | task or `None` | Finds one task |
| `mark_task_done` | list, ID | `True` or `False` | Changes one task to done |
| `delete_task` | list, ID | `True` or `False` | Removes one task |

### Study Planner Function Plan

Possible functions:

```python
def get_next_id(items):
    pass


def add_study_item(items, subject, topic, study_date="", priority="medium"):
    pass


def find_item_by_id(items, item_id):
    pass


def mark_item_complete(items, item_id):
    pass


def filter_by_subject(items, subject):
    pass
```

Planning questions:

- Should subjects be case-sensitive?
- Is `Python` the same as `python`?
- Which priority values are allowed?
- Can the study date be blank?
- What happens if the user marks an item that does not exist?

Write answers now.

Even rough answers will help tomorrow.

### Optional Class Plan

You do not need classes for this capstone.

But if you want to practice classes from Days 88 and 89, you can use a small class to represent one item.

Example task sketch:

```python
class Task:
    def __init__(self, task_id, title, status="todo"):
        self.id = task_id
        self.title = title
        self.status = status
```

Use a class only if it makes the project clearer.

If it makes you feel stuck, use dictionaries.

Finishing a clear dictionary-based project is better than abandoning a complicated class-based project.

## CLI Commands Or Menu

Your capstone needs a way for the user to interact with it.

Choose one style:

```text
menu style
command style
```

Menu style is usually easier for beginners.

Command style is closer to many developer tools.

Either is fine.

### Menu Style

A task tracker menu might look like this:

```text
Personal Task Tracker

1. Add task
2. List tasks
3. List unfinished tasks
4. Mark task done
5. Delete task
6. Save and quit

Choose an option:
```

A study planner menu might look like this:

```text
Study Planner

1. Add study item
2. List all study items
3. List incomplete items
4. Filter by subject
5. Mark item complete
6. Save and quit

Choose an option:
```

Menu style gives you a natural `while` loop:

```text
load data
repeat until the user quits:
    show menu
    read choice
    run matching action
save data
```

### Command Style

A command-style task tracker might use commands like:

```text
python main.py add "Finish math worksheet"
python main.py list
python main.py done 3
python main.py delete 3
```

A command-style study planner might use commands like:

```text
python main.py add "Python" "JSON files"
python main.py list
python main.py complete 2
python main.py subject "Python"
```

Command style works well with `argparse`, but it takes more setup.

If you are unsure, choose menu style.

The capstone should test your ability to finish, not your ability to make the interface fancy.

## Saving Data

Your project should save user data between runs.

Use JSON.

JSON is a good fit because your data is mostly lists, dictionaries, strings, numbers, and booleans.

Plan two storage functions:

```text
load_items(file_path)
save_items(file_path, items)
```

Decide what happens when the data file does not exist yet.

A beginner-friendly answer:

```text
If the file does not exist, start with an empty list.
```

Decide what happens when the data file is empty or damaged.

For the capstone, you can keep the first version simple:

```text
If JSON loading fails, show a friendly message and start with an empty list.
```

You do not need to solve every file problem today.

You do need to write down the behavior you want.

That way, tomorrow's code has a target.

## Tests To Plan

You have practiced simple tests.

For the capstone, do not try to test the entire menu first.

Start by testing small logic functions.

Good test targets:

- next ID rule
- adding an item
- finding an item by ID
- marking an item complete
- deleting an item
- filtering unfinished items
- filtering by subject

Weak first test targets:

- every printed menu line
- every possible invalid keyboard input
- the entire app from start to finish

Those can wait.

A task tracker test plan might include:

| Test | Given | Check |
| --- | --- | --- |
| next ID with empty list | `[]` | returns `1` |
| next ID with items | IDs `1`, `2`, `5` | returns `6` |
| add task | empty list and title | new task has ID `1` and status `todo` |
| find task | list with task ID `2` | returns that task |
| mark done | list with task ID `2` | status changes to `done` |
| missing ID | list without task ID `99` | function reports failure |

A study planner test plan might include:

| Test | Given | Check |
| --- | --- | --- |
| next ID with empty list | `[]` | returns `1` |
| add item | subject and topic | new item has status `planned` |
| complete item | list with item ID `3` | status changes to `complete` |
| filter by subject | mixed subjects | only matching subject appears |
| incomplete filter | mixed statuses | complete items are not included |
| missing ID | list without item ID `99` | function reports failure |

Here is a small syntax-only example of what later tests might resemble:

```python
sample_tasks = [
    {"id": 1, "title": "Read chapter 4", "status": "todo"},
    {"id": 2, "title": "Submit notes", "status": "done"},
]

todo_titles = [
    task["title"]
    for task in sample_tasks
    if task["status"] == "todo"
]

assert todo_titles == ["Read chapter 4"]
```

You do not need to write the final tests today.

Today, write the test list in your plan.

Tomorrow, start with one or two of the easiest tests.

## Milestones For Days 98-100

A milestone is a visible step forward.

Your capstone has three build days after today.

Use them wisely.

### Day 98: Build The Core

Goal:

```text
Create the project files and make the small first version work.
```

Possible Day 98 tasks:

- create the project folder
- create `main.py`
- create the main logic file
- create the storage file
- create an empty JSON data file or handle a missing one
- add the first data model
- build add, list, and complete actions
- save and load data
- run the program manually
- make the first commit

Day 98 should end with something usable, even if it is plain.

### Day 99: Add Tests And Improve Organization

Goal:

```text
Make the project easier to trust and easier to maintain.
```

Possible Day 99 tasks:

- add tests for the most important logic
- move repeated code into functions
- clean up confusing names
- add one "Should have" feature if the core is stable
- improve error handling for invalid IDs
- improve the README
- make another commit

Day 99 is not for adding five new ideas.

It is for making the core project stronger.

### Day 100: Polish, Review, And Present

Goal:

```text
Make the project understandable to another person, including future you.
```

Possible Day 100 tasks:

- review the project from start to finish
- test the main user flow
- polish menu text
- update README instructions
- add example data if useful
- remove unused code
- write a short project summary
- make the final commit
- write what you would add next

Day 100 is about finishing well.

## Capstone Plan Template

Copy this template into:

```text
day-97/capstone_plan.md
```

Then fill it in.

````md
# Capstone Plan

## Project Choice

I am building:

- [ ] Personal Task Tracker
- [ ] Study Planner

## User

This project is for:

## Goal

The program helps the user:

## Small First Version

By the end of Day 98, the program should be able to:

- 
- 
- 

## Must Have

- 
- 
- 

## Should Have

- 
- 

## Could Have

- 
- 

## Will Not Build Now

- 
- 

## Data Model

Each item will store:

| Field | Type | Required? | Notes |
| --- | --- | --- | --- |
| id | integer | yes | |
| | | | |
| | | | |

Example item:

```text
Write your example item here.
```

## File Plan

```text
capstone/
  README.md
  main.py
```

| File | Job |
| --- | --- |
| `README.md` | |
| `main.py` | |

## Function Or Class Plan

| Name | Receives | Returns | Job |
| --- | --- | --- | --- |
| | | | |
| | | | |
| | | | |

## Menu Or Commands

I will use:

- [ ] Menu style
- [ ] Command style

Planned menu or commands:

```text
Write the menu or commands here.
```

## Save And Load Plan

Data file:

What happens if the file does not exist?

What happens if the file cannot be read?

## Test Plan

| Test | Given | Check |
| --- | --- | --- |
| | | |
| | | |
| | | |

## Milestones

Day 98:

- 
- 
- 

Day 99:

- 
- 
- 

Day 100:

- 
- 
- 

## Risks

Things that might make the project too large:

- 
- 

How I will keep the project small:

- 
- 

## First Commit Message Ideas

- 
- 
````

The template is longer than your final plan needs to be.

If a section does not matter for your project, keep it short.

The point is not to write a formal report.

The point is to remove tomorrow's guesswork.

## Scope Checklist

Before you accept your plan, check the scope.

Use this checklist:

```text
[ ] I chose one project, not both.
[ ] I can explain the project in one sentence.
[ ] The small first version has 3-5 actions.
[ ] The first version saves and loads data.
[ ] The data model uses simple Python types.
[ ] I know the main file names.
[ ] I know the main functions or class names.
[ ] I have at least 4 test ideas.
[ ] I listed features I will not build now.
[ ] Day 98 has a clear first task.
```

If you cannot check an item, revise the plan.

Do that now while changes are cheap.

## Example Plan: Personal Task Tracker

Here is a short example.

Do not copy it exactly unless it matches your project.

Use it to see the level of detail that is useful.

````md
# Capstone Plan

## Project Choice

Personal Task Tracker

## User

This project is for a student who wants to track small school tasks and personal reminders.

## Goal

The program helps the user add tasks, see what is unfinished, and mark tasks as done.

## Small First Version

By the end of Day 98, the program should let the user:

- add a task
- list all tasks
- mark a task done
- save and load tasks from JSON

## Must Have

- add task
- list tasks
- mark task done
- save and load tasks

## Should Have

- list unfinished tasks
- delete a task

## Could Have

- due dates
- notes
- edit a task title

## Will Not Build Now

- login
- reminders
- web interface
- recurring tasks

## Data Model

Each task stores:

| Field | Type | Required? | Notes |
| --- | --- | --- | --- |
| id | integer | yes | Used to choose one task |
| title | string | yes | Main task text |
| status | string | yes | `todo` or `done` |
| due_date | string | no | Can be blank in version 1 |
| notes | string | no | Can be blank in version 1 |

Example item:

```text
id: 1
title: Finish math worksheet
status: todo
due_date:
notes:
```

## File Plan

```text
capstone/
  README.md
  main.py
  data/
    tasks.json
  src/
    tasks.py
    storage.py
  tests/
    test_tasks.py
```

## Function Plan

| Name | Receives | Returns | Job |
| --- | --- | --- | --- |
| get_next_id | tasks | integer | Choose the next ID |
| add_task | tasks, title | task | Create a task |
| find_task_by_id | tasks, task_id | task or None | Find one task |
| mark_task_done | tasks, task_id | True or False | Complete a task |
| load_items | path | list | Read JSON |
| save_items | path, items | None | Write JSON |

## Menu

```text
1. Add task
2. List tasks
3. List unfinished tasks
4. Mark task done
5. Save and quit
```

## Test Plan

| Test | Given | Check |
| --- | --- | --- |
| Next ID empty | empty task list | returns 1 |
| Next ID existing | IDs 1 and 2 | returns 3 |
| Add task | title "Read" | task has status todo |
| Mark done | task ID 1 | status becomes done |
| Missing task | task ID 99 | function returns False |

## Milestones

Day 98:

- create files
- build add and list
- build mark done
- save and load JSON

Day 99:

- add tests
- add unfinished filter
- clean up repeated code

Day 100:

- polish README
- run final checks
- write project summary
````

Notice how ordinary this plan is.

That is good.

The project is clear enough to build.

## Example Plan: Study Planner

Here is a second example.

````md
# Capstone Plan

## Project Choice

Study Planner

## User

This project is for a learner who wants to organize study topics for the next week.

## Goal

The program helps the user add study topics, group them by subject, and mark them complete.

## Small First Version

By the end of Day 98, the program should let the user:

- add a study item
- list all study items
- mark a study item complete
- save and load study items from JSON

## Must Have

- add study item
- list study items
- mark item complete
- save and load items

## Should Have

- filter by subject
- show incomplete items

## Could Have

- priority
- study date
- estimated minutes

## Will Not Build Now

- calendar syncing
- charts
- automatic schedules

## Data Model

Each study item stores:

| Field | Type | Required? | Notes |
| --- | --- | --- | --- |
| id | integer | yes | Used to choose one item |
| subject | string | yes | Example: Python |
| topic | string | yes | Example: JSON files |
| status | string | yes | `planned` or `complete` |
| study_date | string | no | Can be blank |
| priority | string | no | `low`, `medium`, or `high` |

## File Plan

```text
capstone/
  README.md
  main.py
  data/
    study_items.json
  src/
    planner.py
    storage.py
  tests/
    test_planner.py
```

## Function Plan

| Name | Receives | Returns | Job |
| --- | --- | --- | --- |
| get_next_id | items | integer | Choose the next ID |
| add_study_item | items, subject, topic | item | Create one item |
| find_item_by_id | items, item_id | item or None | Find one item |
| mark_item_complete | items, item_id | True or False | Complete one item |
| filter_by_subject | items, subject | list | Find matching subject |

## Menu

```text
1. Add study item
2. List study items
3. List incomplete items
4. Filter by subject
5. Mark item complete
6. Save and quit
```

## Test Plan

| Test | Given | Check |
| --- | --- | --- |
| Add item | subject and topic | status is planned |
| Complete item | item ID 2 | status becomes complete |
| Filter subject | Python and Math items | only Python items appear |
| Missing item | item ID 99 | function returns False |
````

This version has a little more filtering.

It is still small enough for a beginner capstone.

## Try It Yourself

Create this file:

```text
day-97/capstone_plan.md
```

Then complete these steps.

### Step 1: Pick One Project

Write:

```text
I am building a Personal Task Tracker.
```

or:

```text
I am building a Study Planner.
```

Do not write "maybe both."

### Step 2: Write The User And Goal

Write two short sections:

```text
User:

Goal:
```

Make the goal practical.

The goal should describe what the program helps someone do.

### Step 3: Choose Features

Make four lists:

```text
Must have:
Should have:
Could have:
Will not build now:
```

Put at least three items in "Will not build now."

That list protects your project.

### Step 4: Define The Small First Version

Write one sentence:

```text
By the end of Day 98, the program should be able to ...
```

Limit this to 3-5 actions.

### Step 5: Sketch The Data Model

Make a table with fields.

Include:

- field name
- type
- whether it is required
- notes

Then write one example item in a text block.

### Step 6: Plan The Files

Write a small folder tree.

Include:

- `README.md`
- `main.py`
- one data file
- one logic file
- one storage file
- one test file

### Step 7: Plan Functions Or Classes

Write at least five planned function names.

For each one, answer:

- what does it receive?
- what does it return?
- what job does it do?

If you want to use a class, describe the class too.

### Step 8: Plan The Interface

Choose menu style or command style.

Then write the planned menu or command list.

The user should be able to see how the program works without reading your code.

### Step 9: Plan Tests

Write at least four test ideas.

Use this format:

```text
Test:
Given:
Check:
```

At least one test should cover a missing ID.

At least one test should cover an empty list.

### Step 10: Plan The Milestones

Write tasks for:

```text
Day 98
Day 99
Day 100
```

Make Day 98 focus on the small first version.

Make Day 99 focus on tests and cleanup.

Make Day 100 focus on polish and review.

## Common Mistake

The most common mistake today is planning a project that belongs to a future version of you.

That plan often sounds like this:

```text
I will make a complete productivity system with accounts, reminders, recurring tasks,
calendar integration, graphs, smart suggestions, tags, themes, and cloud backup.
```

That is not a beginner capstone.

That is a product roadmap.

A better plan sounds like this:

```text
I will make a task tracker that stores tasks in JSON, lets the user add and list tasks,
and lets the user mark tasks as done.
```

The smaller plan can actually become finished software.

Once the core works, you can add one extra feature.

But a project with no working core and many half-started features is frustrating.

Choose finished over huge.

## Debug It

Read each planning problem below and decide how to fix it.

### Problem 1: The Feature List Is Too Large

Plan:

```text
Must have:
- add tasks
- edit tasks
- delete tasks
- recurring tasks
- email reminders
- categories
- priorities
- due dates
- search
- charts
- login
- cloud sync
```

Fix:

Move most of those features into "Could have" or "Will not build now."

A better "Must have" list:

```text
Must have:
- add tasks
- list tasks
- mark tasks done
- save and load tasks
```

### Problem 2: The Data Model Has No ID

Plan:

```text
Each task has a title and status.
```

Question:

```text
How will the user mark the third task done if two tasks have the same title?
```

Fix:

Add an ID field.

```text
id
title
status
```

### Problem 3: The Menu Does Not Match The Features

Plan:

```text
Must have:
- add task
- list tasks
- mark task done
- save and load tasks

Menu:
1. Add task
2. Quit
```

Fix:

The menu should expose the planned actions:

```text
1. Add task
2. List tasks
3. Mark task done
4. Save and quit
```

### Problem 4: The Tests Are Too Broad

Plan:

```text
Test that the whole app works.
```

That is too vague.

Fix:

Write smaller test ideas:

```text
Test: next ID for empty list
Given: []
Check: returns 1

Test: missing ID
Given: a list with IDs 1 and 2
Check: searching for ID 99 returns None
```

### Problem 5: The First Version Depends On Dates

Plan:

```text
The first version sorts tasks by date, warns about overdue tasks,
and calculates how many days are left.
```

That can become a date-handling project.

Fix:

Store dates as simple strings in version 1.

You can display them without calculating with them.

```text
due_date: 2026-05-18
```

Later, if the rest of the project works, you can add smarter date behavior.

## Read the Docs

Today, read just enough documentation to support your plan.

You do not need to memorize it.

Look up these Python standard library pages when you are ready:

- `json` for saving and loading lists of dictionaries
- `pathlib` for working with file paths
- `argparse` if you choose command style
- `unittest` if you want to organize tests with the standard library

While reading, ask:

```text
Which part of this do I need for my small first version?
```

For JSON, you likely only need:

```text
json.load()
json.dump()
```

For `pathlib`, you likely only need:

```text
Path
exists()
```

For `argparse`, you may only need it if you choose command style.

Menu style can use `input()` and a loop.

## Mini Challenge

Write a one-page capstone pitch.

Use this format:

```text
Project name:

One-sentence goal:

The user can:
1.
2.
3.

The program stores:

The first version will not include:

The hardest part will probably be:

My first Day 98 task will be:
```

Keep it under 200 words.

This is not marketing.

It is a clarity exercise.

If you cannot describe the project briefly, the plan may still be too fuzzy.

## Real-World Use

Real projects often start this way.

Professional developers may use more formal tools, but the core questions are familiar:

- What problem are we solving?
- Who is the user?
- What is version 1?
- What data do we store?
- What actions does the user need?
- What can wait?
- How will we know it works?

Beginners sometimes think planning is separate from programming.

It is not.

Planning is programming before the syntax starts.

It helps you choose names, files, tests, and order.

The better your plan, the less time you spend staring at an empty file.

## Recap

Today you planned the final project before building it.

You practiced:

- choosing between two practical capstone ideas
- writing a user and goal statement
- limiting features with four scope buckets
- defining a small first version
- sketching a data model
- planning files and folders
- naming functions or classes
- choosing a menu or command interface
- planning JSON storage
- writing test ideas
- creating milestones for Days 98-100

The main lesson is simple:

```text
A finished small project is better than an unfinished large one.
```

Tomorrow's job is not to invent the project from scratch.

Tomorrow's job is to build the first version of the plan.

## Lesson Checklist

Before you stop today, make sure you can check these off:

```text
[ ] I chose Personal Task Tracker or Study Planner.
[ ] I wrote a user statement.
[ ] I wrote a goal statement.
[ ] I listed must-have features.
[ ] I listed features I will not build now.
[ ] I wrote a small first version.
[ ] I sketched the data model.
[ ] I planned the project files.
[ ] I named the main functions or classes.
[ ] I chose menu style or command style.
[ ] I wrote at least four test ideas.
[ ] I wrote milestones for Days 98, 99, and 100.
```

If the checklist feels too long, do not panic.

Most entries can be short.

The plan should be useful, not fancy.

## Exercises

### Exercise 1: Name The Project

Choose one:

```text
Personal Task Tracker
Study Planner
```

Then give it a simple project name.

Examples:

```text
Simple Tasks
Study Board
Focus List
Course Planner
```

Avoid names that make the project sound larger than it is.

### Exercise 2: Write The One-Sentence Goal

Write one sentence that starts with:

```text
This program helps the user ...
```

Make sure the sentence mentions the main action.

Examples:

```text
This program helps the user track tasks and mark them done.
This program helps the user plan study topics by subject.
```

### Exercise 3: Cut The Scope

Write ten possible features.

Then sort them into:

```text
Must have
Should have
Could have
Will not build now
```

Only 3-5 features should stay in "Must have."

### Exercise 4: Design One Item

Write one example item for your project.

For a task tracker:

```text
id:
title:
status:
due_date:
notes:
```

For a study planner:

```text
id:
subject:
topic:
status:
study_date:
priority:
```

Fill in realistic values.

### Exercise 5: Write The File Tree

Write the file tree for your capstone.

Keep it small.

Include no more than:

- one main file
- one or two logic files
- one storage file
- one data folder
- one tests folder
- one README

### Exercise 6: Name Seven Functions

Write seven possible function names.

At least three should be about the data rules.

At least one should be about saving or loading.

At least one should handle finding an item by ID.

Example:

```text
get_next_id
add_task
find_task_by_id
mark_task_done
delete_task
load_items
save_items
```

### Exercise 7: Choose The Interface

Choose:

```text
menu style
```

or:

```text
command style
```

Then write the menu or command list.

Check that every must-have feature appears in the interface.

### Exercise 8: Write Six Test Ideas

Write six test ideas using:

```text
Test:
Given:
Check:
```

Include:

- an empty list case
- a missing ID case
- a successful add case
- a successful complete case
- a save or load case
- one filter case

### Exercise 9: Plan Your First Commit

Write three commit messages you might use during the capstone.

Examples:

```text
Create capstone project structure
Add task creation and listing
Add JSON save and load
```

Commit messages should describe what changed.

Avoid messages like:

```text
stuff
updates
final
```

### Exercise 10: Write Tomorrow's First Ten Minutes

Write exactly what you will do first on Day 98.

Example:

```text
1. Create the capstone folder.
2. Add README.md, main.py, src/tasks.py, src/storage.py, and tests/test_tasks.py.
3. Write the data model comment in src/tasks.py.
4. Write the get_next_id function.
5. Test get_next_id with an empty list and a list with two tasks.
```

This removes friction.

Starting is easier when the first few actions are already chosen.

## Tiny Win

You turned the final project from a vague idea into a buildable plan.

That is real progress.

Tomorrow, you will not be opening a blank file and hoping inspiration appears.

You will be following a map you wrote yourself.

## Tomorrow

Tomorrow is Day 98: Capstone Build Day 1.

You will create the project files and build the small first version.

Bring your plan from:

```text
day-97/capstone_plan.md
```

Your Day 98 goal will be simple:

```text
Make the core project work before adding extras.
```

That means:

- create the file structure
- build the core data functions
- connect the menu or commands
- save and load JSON
- run the first manual checks

If your plan is clear, tomorrow becomes a series of small steps.

That is exactly where you want to be.
