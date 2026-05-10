# Day 53: Refactor Day: Clean Up Old Code

**Focus:** Improving working code without changing what it does  
**You will practice:** repeated print lines, clearer names, duplicated dictionary logic, long conditions, messy menu code, and testing after each small change  
**Estimated time:** 45-60 minutes

## Today's Goal

Today is a refactor day.

You are not learning a big new Python feature. You are practicing a habit that real programmers use all the time:

```text
Make working code easier to read, easier to change, and easier to trust.
```

Refactoring means changing the structure of code without changing its behavior.

That last part matters.

If a program printed three tasks before the refactor, it should still print the same three tasks after the refactor.

If a program accepted menu choice `"2"` before the refactor, it should still accept menu choice `"2"` after the refactor.

If a program calculated a total before the refactor, it should calculate the same total after the refactor.

Today you will clean up small examples from older topics:

- repeated `print()` statements
- unclear variable names
- duplicated dictionary logic
- long conditions
- messy menu code
- small changes followed by small tests

By the end of this lesson, you should be able to look at working code and ask:

```text
What is this code doing?
What part is hard to read?
Can I improve one small part?
Did the behavior stay the same?
```

Tomorrow you will debug broken data programs. Refactoring helps because cleaner code is usually easier to debug.

## The Big Idea

Refactoring is cleanup, not a new feature.

Here is working code:

```python
print("Today's tasks:")
print("- read notes")
print("- practice dictionaries")
print("- review mistakes")
```

You should see:

```text
Today's tasks:
- read notes
- practice dictionaries
- review mistakes
```

The code works, but the repeated `print()` lines are a clue.

The tasks are really a collection of similar values.

After:

```python
tasks = ["read notes", "practice dictionaries", "review mistakes"]

print("Today's tasks:")

for task in tasks:
    print("- " + task)
```

You should see:

```text
Today's tasks:
- read notes
- practice dictionaries
- review mistakes
```

The output stayed the same.

The code became easier to change.

If you want to add another task, you add it to the list:

```python
tasks = [
    "read notes",
    "practice dictionaries",
    "review mistakes",
    "clean up old code"
]

print("Today's tasks:")

for task in tasks:
    print("- " + task)
```

You should see:

```text
Today's tasks:
- read notes
- practice dictionaries
- review mistakes
- clean up old code
```

That is a good refactor:

```text
same idea
same behavior
cleaner shape
easier future change
```

A bad refactor changes the behavior by accident.

If the original program printed lowercase task names in the same order, this is not the same behavior:

```python
tasks = ["read notes", "practice dictionaries", "review mistakes"]

tasks.sort()

print("Today's tasks:")

for task in tasks:
    print("- " + task.upper())
```

You should see:

```text
Today's tasks:
- PRACTICE DICTIONARIES
- READ NOTES
- REVIEW MISTAKES
```

The code still runs, but it changed the order and the capitalization.

That might be useful in some program, but it is not a plain refactor.

When you refactor, protect the behavior first.

## The Mental Model

Think of refactoring as cleaning one shelf at a time.

You do not empty the whole room. You choose one small part, improve it, and check that nothing important moved.

Use this loop:

```text
1. Run the code.
2. Notice what it does.
3. Pick one small cleanup.
4. Change only that part.
5. Run the code again.
6. Compare the behavior.
```

For now, compare behavior by running the program manually.

You do not need a testing library yet.

You can test with a simple note like this:

```text
Before:
choice = "1" prints the task list
choice = "2" adds a task
choice = "3" prints Goodbye

After:
choice = "1" still prints the task list
choice = "2" still adds a task
choice = "3" still prints Goodbye
```

Refactoring is safer when each change is small.

Small cleanup:

```text
Rename one unclear variable.
```

Bigger cleanup:

```text
Rename variables, change the data shape, rewrite the menu, and add a new feature.
```

The bigger cleanup is harder to check.

Today, prefer small cleanup.

What not to refactor yet:

- Do not turn every program into clever one-line code.
- Do not use tools you have not learned just to make code shorter.
- Do not add new features while you are refactoring.
- Do not rewrite a whole working program from scratch unless it is very small.
- Do not refactor broken code before you understand why it is broken.
- Do not force code into functions or classes yet. Those lessons are coming soon.

Good refactoring should make the code calmer to read.

## Try It Yourself

Create a file named:

```text
day-53/refactor_practice.py
```

You can copy one example at a time into that file.

After each refactor, run the code and compare the output.

### Step 1: Replace Repeated Print Lines With A Loop

Before:

```python
print("Shopping list:")
print("- milk")
print("- rice")
print("- apples")
```

You should see:

```text
Shopping list:
- milk
- rice
- apples
```

After:

```python
shopping_list = ["milk", "rice", "apples"]

print("Shopping list:")

for item in shopping_list:
    print("- " + item)
```

You should see:

```text
Shopping list:
- milk
- rice
- apples
```

The behavior stayed the same.

The repeated values moved into a list.

The repeated action moved into a loop.

That is one of the most beginner-friendly refactors.

Try this:

Add `"bread"` to the list and run the program again.

You should only need to change one line:

```python
shopping_list = ["milk", "rice", "apples", "bread"]

print("Shopping list:")

for item in shopping_list:
    print("- " + item)
```

You should see:

```text
Shopping list:
- milk
- rice
- apples
- bread
```

### Step 2: Rename Unclear Variables

Working code can still be hard to read.

Before:

```python
x = "Mina"
y = 3
z = y + 1

print(x)
print(z)
```

You should see:

```text
Mina
4
```

This works, but the names do not help.

After:

```python
student_name = "Mina"
lessons_done = 3
new_lesson_count = lessons_done + 1

print(student_name)
print(new_lesson_count)
```

You should see:

```text
Mina
4
```

The output did not change.

Only the names changed.

Clear names reduce guessing.

Use names that explain what the value means:

```text
x                  student_name
y                  lessons_done
z                  new_lesson_count
```

Do not rename everything at once.

Rename one small group, run the code, then continue.

### Step 3: Remove Duplicated Dictionary Logic

Here is working code with repeated logic.

Before:

```python
student_one = {
    "name": "Maya",
    "score": 88
}

student_two = {
    "name": "Leo",
    "score": 72
}

if student_one["score"] >= 60:
    status_one = "passed"
else:
    status_one = "needs practice"

if student_two["score"] >= 60:
    status_two = "passed"
else:
    status_two = "needs practice"

print(student_one["name"] + ": " + status_one)
print(student_two["name"] + ": " + status_two)
```

You should see:

```text
Maya: passed
Leo: passed
```

The code works.

But notice the repeated pattern:

```text
check score
choose status
print name and status
```

After:

```python
students = [
    {
        "name": "Maya",
        "score": 88
    },
    {
        "name": "Leo",
        "score": 72
    }
]

for student in students:
    if student["score"] >= 60:
        status = "passed"
    else:
        status = "needs practice"

    print(student["name"] + ": " + status)
```

You should see:

```text
Maya: passed
Leo: passed
```

The behavior stayed the same.

The data became a list of dictionaries.

The repeated logic became one loop.

This refactor is useful because adding a third student is now easier:

```python
students = [
    {
        "name": "Maya",
        "score": 88
    },
    {
        "name": "Leo",
        "score": 72
    },
    {
        "name": "Nia",
        "score": 54
    }
]

for student in students:
    if student["score"] >= 60:
        status = "passed"
    else:
        status = "needs practice"

    print(student["name"] + ": " + status)
```

You should see:

```text
Maya: passed
Leo: passed
Nia: needs practice
```

### Step 4: Name Parts Of A Long Condition

Long conditions can be correct and still hard to read.

Before:

```python
age = 16
has_ticket = True
is_blocked = False

if age >= 13 and age <= 18 and has_ticket and not is_blocked:
    print("Entry allowed")
else:
    print("Entry denied")
```

You should see:

```text
Entry allowed
```

The condition works, but your eyes have to hold several rules at once.

After:

```python
age = 16
has_ticket = True
is_blocked = False

is_teen = age >= 13 and age <= 18
can_enter = is_teen and has_ticket and not is_blocked

if can_enter:
    print("Entry allowed")
else:
    print("Entry denied")
```

You should see:

```text
Entry allowed
```

The behavior stayed the same.

The rules now have names.

You can test the refactor by changing one value at a time:

```python
age = 12
has_ticket = True
is_blocked = False

is_teen = age >= 13 and age <= 18
can_enter = is_teen and has_ticket and not is_blocked

if can_enter:
    print("Entry allowed")
else:
    print("Entry denied")
```

You should see:

```text
Entry denied
```

Try this:

Change `age`, `has_ticket`, and `is_blocked` one at a time.

The refactored version should make it easier to understand why the answer changes.

### Step 5: Clean Up A Small Menu

Menu code often becomes messy because it mixes display text, choices, and actions.

Start by cleaning only the display text.

Before:

```python
print("Menu:")
print("1. Show tasks")
print("2. Add task")
print("3. Remove task")
print("4. Quit")
```

You should see:

```text
Menu:
1. Show tasks
2. Add task
3. Remove task
4. Quit
```

After:

```python
menu_options = [
    "1. Show tasks",
    "2. Add task",
    "3. Remove task",
    "4. Quit"
]

print("Menu:")

for option in menu_options:
    print(option)
```

You should see:

```text
Menu:
1. Show tasks
2. Add task
3. Remove task
4. Quit
```

This is a small refactor.

It does not change what the menu does.

It only makes the menu text easier to add, remove, or reorder.

Now clean one small piece of choice handling.

Before:

```python
choice = " 2 "

if choice == "1":
    print("Showing tasks")
elif choice == "2":
    print("Adding a task")
elif choice == "3":
    print("Removing a task")
elif choice == "4":
    print("Goodbye")
else:
    print("Unknown choice")
```

You should see:

```text
Unknown choice
```

That behavior may be too strict because the value has spaces.

This next change is not just cleanup. It is a behavior change:

```python
choice = " 2 "
choice = choice.strip()

if choice == "1":
    print("Showing tasks")
elif choice == "2":
    print("Adding a task")
elif choice == "3":
    print("Removing a task")
elif choice == "4":
    print("Goodbye")
else:
    print("Unknown choice")
```

You should see:

```text
Adding a task
```

This can be a good change, but name it honestly:

```text
This is not only a refactor.
It changes how the program handles spaces.
```

When you are practicing refactoring, keep cleanup and behavior changes separate.

## Common Mistake

A common mistake is calling every change a refactor.

Refactoring means the behavior stays the same.

This original code prints items in the order they were written:

```python
items = ["milk", "rice", "apples"]

for item in items:
    print(item)
```

You should see:

```text
milk
rice
apples
```

Broken code:

```python
items = ["milk", "rice", "apples"]

items.sort()

for item in items:
    print(item.upper())
```

You should see:

```text
APPLES
MILK
RICE
```

This code runs, but it is not a safe refactor.

It changed two things:

- the order
- the capitalization

Those might be useful features later.

But if your goal is refactoring, do not sneak them in.

Fixed code:

```python
items = ["milk", "rice", "apples"]

for item in items:
    print(item)
```

You should see:

```text
milk
rice
apples
```

The fixed version keeps the behavior.

If you want sorted uppercase output, make that a separate change and test it separately.

Another common mistake is making the code shorter but harder to understand.

Before:

```python
score = 72

if score >= 60:
    print("passed")
else:
    print("needs practice")
```

You should see:

```text
passed
```

This is already clear.

You do not need to compress it into a clever shape just because you can.

Cleaner code is not always shorter code.

Cleaner code is easier code to understand.

## Debug It

Refactoring can introduce bugs when you move too fast.

Work through these slowly.

### Debug 1: Wrong Variable After Refactoring

The goal is:

```text
Maya: passed
Leo: passed
```

Broken code:

```python
students = [
    {
        "name": "Maya",
        "score": 88
    },
    {
        "name": "Leo",
        "score": 72
    }
]

for student in students:
    if students["score"] >= 60:
        status = "passed"
    else:
        status = "needs practice"

    print(student["name"] + ": " + status)
```

Why it is broken:

```text
students is the whole list.
student is one dictionary from the list.
Only the dictionary has the "score" key.
```

Fixed code:

```python
students = [
    {
        "name": "Maya",
        "score": 88
    },
    {
        "name": "Leo",
        "score": 72
    }
]

for student in students:
    if student["score"] >= 60:
        status = "passed"
    else:
        status = "needs practice"

    print(student["name"] + ": " + status)
```

You should see:

```text
Maya: passed
Leo: passed
```

### Debug 2: A Named Condition Forgot One Rule

The goal is:

```text
Entry denied
```

A blocked person should not be allowed to enter.

Broken code:

```python
age = 16
has_ticket = True
is_blocked = True

is_teen = age >= 13 and age <= 18
can_enter = is_teen and has_ticket

if can_enter:
    print("Entry allowed")
else:
    print("Entry denied")
```

Why it is broken:

```text
The original rule had three parts:
the person is a teen
the person has a ticket
the person is not blocked

The refactored condition forgot the blocked check.
```

Fixed code:

```python
age = 16
has_ticket = True
is_blocked = True

is_teen = age >= 13 and age <= 18
can_enter = is_teen and has_ticket and not is_blocked

if can_enter:
    print("Entry allowed")
else:
    print("Entry denied")
```

You should see:

```text
Entry denied
```

### Debug 3: Menu Text And Choice Values Got Mixed

The goal is:

```text
Adding a task
```

Broken code:

```python
choice = "2"

menu_options = [
    "1. Show tasks",
    "2. Add task",
    "3. Quit"
]

if choice == menu_options[1]:
    print("Adding a task")
else:
    print("Unknown choice")
```

Why it is broken:

```text
choice is "2".
menu_options[1] is "2. Add task".
Those strings are not the same.
```

Fixed code:

```python
choice = "2"

menu_options = [
    "1. Show tasks",
    "2. Add task",
    "3. Quit"
]

if choice == "2":
    print("Adding a task")
else:
    print("Unknown choice")
```

You should see:

```text
Adding a task
```

The menu text is for people.

The choice value is what the program checks.

Keep those ideas separate.

## Read the Docs

Today, practice reading a tiny part of the Python documentation.

Look up the documentation for string methods.

Find these methods:

```text
strip()
lower()
upper()
```

Do not try to read the whole page.

Only answer these questions:

```text
What does strip() remove?
Does lower() change the original string or return a new string?
Does upper() change the original string or return a new string?
```

Then test the idea:

```python
name = "  Mina  "

clean_name = name.strip()
upper_name = clean_name.upper()

print(name)
print(clean_name)
print(upper_name)
```

You should see:

```text
  Mina  
Mina
MINA
```

This matters for refactoring because method names can make code clearer.

But remember:

```text
Adding strip(), lower(), or upper() can change behavior.
Use them on purpose.
```

## Mini Challenge

Refactor this small progress report.

Start with this code:

```python
student_one = {
    "name": "Maya",
    "lessons_done": 12
}

student_two = {
    "name": "Leo",
    "lessons_done": 9
}

student_three = {
    "name": "Nia",
    "lessons_done": 15
}

print(student_one["name"] + ": " + str(student_one["lessons_done"]) + " lessons")
print(student_two["name"] + ": " + str(student_two["lessons_done"]) + " lessons")
print(student_three["name"] + ": " + str(student_three["lessons_done"]) + " lessons")
```

You should see:

```text
Maya: 12 lessons
Leo: 9 lessons
Nia: 15 lessons
```

Your job:

```text
Put the students into a list.
Loop through the list.
Print the same three lines.
Run the program before and after.
Make sure the output stays the same.
```

One possible refactor:

```python
students = [
    {
        "name": "Maya",
        "lessons_done": 12
    },
    {
        "name": "Leo",
        "lessons_done": 9
    },
    {
        "name": "Nia",
        "lessons_done": 15
    }
]

for student in students:
    print(student["name"] + ": " + str(student["lessons_done"]) + " lessons")
```

You should see:

```text
Maya: 12 lessons
Leo: 9 lessons
Nia: 15 lessons
```

Now make one small behavior change after the refactor.

Add one more student:

```python
students = [
    {
        "name": "Maya",
        "lessons_done": 12
    },
    {
        "name": "Leo",
        "lessons_done": 9
    },
    {
        "name": "Nia",
        "lessons_done": 15
    },
    {
        "name": "Asha",
        "lessons_done": 7
    }
]

for student in students:
    print(student["name"] + ": " + str(student["lessons_done"]) + " lessons")
```

You should see:

```text
Maya: 12 lessons
Leo: 9 lessons
Nia: 15 lessons
Asha: 7 lessons
```

Notice the difference:

```text
The first change was a refactor.
The second change added behavior.
```

Keep those two ideas separate in your mind.

## Real-World Use

Refactoring shows up everywhere.

A shopping list program might start with repeated lines. Later, you turn those items into a list and loop through them.

A quiz game might start with separate variables for each question. Later, you turn the questions into a list of dictionaries.

A contact program might start with copied code for each contact. Later, you store contacts as a list of dictionaries and loop through them.

A menu program might start with a long block of text. Later, you store the menu options in a list so the display code is smaller.

In real projects, code often changes in stages:

```text
First, make it work.
Then, make it clearer.
Then, add the next feature.
```

Refactoring is the middle step.

It gives you a cleaner place to stand before you keep building.

This will matter soon.

Day 55 is a contact book project. Contact book code can become messy quickly if names, phone numbers, and menu choices are scattered everywhere.

Small refactoring habits will make that project easier to write and easier to repair.

## Recap

Refactoring means improving code without changing what it does.

Good beginner refactors include:

- replacing repeated print lines with a list and a loop
- renaming unclear variables
- turning repeated dictionary variables into a list of dictionaries
- naming parts of a long condition
- separating menu text from menu choices
- running the program after each small change

The most important rule:

```text
Change one small thing, then test.
```

If the behavior changes, stop and ask:

```text
Did I mean to change the behavior?
Or did my refactor accidentally change it?
```

Both can happen.

The goal is to know which one you are doing.

## Lesson Checklist

Before moving on, make sure you can:

- [ ] explain refactoring in one sentence
- [ ] tell the difference between refactoring and adding a feature
- [ ] replace repeated print lines with a loop
- [ ] rename unclear variables without changing output
- [ ] turn repeated dictionary logic into a loop
- [ ] split a long condition into named boolean values
- [ ] clean one part of menu code at a time
- [ ] run a program after each small change
- [ ] stop when a refactor starts changing behavior by accident

## Exercises

### Exercise 1

Refactor the repeated print lines.

Before:

```python
print("Favorite topics:")
print("- strings")
print("- loops")
print("- dictionaries")
```

Make a list named `topics`.

Use a loop to print the same output.

### Exercise 2

Rename the variables without changing the output.

Before:

```python
a = "rice"
b = 2
c = 5

print(a)
print(b * c)
```

You should still see:

```text
rice
10
```

Use names like:

```text
item_name
quantity
price
```

### Exercise 3

Refactor this code into a list of dictionaries and a loop.

Before:

```python
book_one = {
    "title": "Python Notes",
    "pages": 120
}

book_two = {
    "title": "Small Programs",
    "pages": 85
}

print(book_one["title"] + ": " + str(book_one["pages"]) + " pages")
print(book_two["title"] + ": " + str(book_two["pages"]) + " pages")
```

The output should stay the same.

### Exercise 4

Name the parts of this condition.

Before:

```python
score = 82
submitted_project = True
missing_assignments = 0

if score >= 60 and submitted_project and missing_assignments == 0:
    print("Passed")
else:
    print("Needs review")
```

Create boolean names such as:

```text
has_passing_score
has_submitted_project
has_no_missing_assignments
passes_course
```

The output should stay the same.

### Exercise 5

Clean the menu display code.

Before:

```python
print("Contact Book")
print("1. Show contacts")
print("2. Add contact")
print("3. Search contacts")
print("4. Quit")
```

Put the menu option lines in a list.

Loop through the list.

The output should stay the same.

### Exercise 6

This refactor accidentally changed behavior.

Original:

```python
names = ["Maya", "Leo", "Nia"]

for name in names:
    print(name)
```

Changed version:

```python
names = ["Maya", "Leo", "Nia"]

names.reverse()

for name in names:
    print(name)
```

Write one sentence explaining why this is not a plain refactor.

### Exercise 7

Refactor the repeated status logic.

Before:

```python
task_one = {
    "title": "Read notes",
    "done": True
}

task_two = {
    "title": "Practice",
    "done": False
}

if task_one["done"]:
    status_one = "done"
else:
    status_one = "not done"

if task_two["done"]:
    status_two = "done"
else:
    status_two = "not done"

print(task_one["title"] + ": " + status_one)
print(task_two["title"] + ": " + status_two)
```

Put both tasks in a list.

Loop through the list.

The output should stay the same.

### Exercise 8

Fix the broken refactor.

Broken code:

```python
contacts = [
    {
        "name": "Mina",
        "phone": "555-0104"
    },
    {
        "name": "Dev",
        "phone": "555-0199"
    }
]

for contact in contacts:
    print(contacts["name"] + ": " + contacts["phone"])
```

The goal is:

```text
Mina: 555-0104
Dev: 555-0199
```

### Exercise 9

Create a small test list before refactoring menu code.

Use this menu rule:

```text
choice "1" shows tasks
choice "2" adds a task
choice "3" quits
any other choice is unknown
```

Write the choices you should test:

```text
1
2
3
9
blank input
input with spaces
```

You do not need to write the full menu yet.

Just practice naming the behavior before changing the code.

### Exercise 10

Choose one old program from Days 31-52.

Look for one of these:

```text
repeated print lines
unclear names
copied dictionary code
a long condition
a menu section that is hard to read
```

Refactor only one small part.

Run the program before and after.

Write down whether the behavior stayed the same.

### Exercise 11

Explain the difference between these two changes.

Change A:

```text
Rename x to score.
The output stays the same.
```

Change B:

```text
Add a new message when the score is 100.
The output changes for score 100.
```

Which one is a refactor?

Which one is a new feature?

### Exercise 12

Prepare for tomorrow.

Take this broken code and do not fix it yet.

Broken code:

```python
students = [
    {
        "name": "Maya",
        "score": 88
    },
    {
        "name": "Leo",
        "score": 72
    }
]

print(students["name"])
```

Write answers to these questions:

```text
What is students?
What is one item inside students?
Should the code use an index, a key, or a loop?
What error do you think Python will show?
```

Tomorrow you will practice this kind of debugging directly.

## Tiny Win

You practiced improving code that already works.

That is different from just making Python accept your code.

Today you practiced reading code with a calmer eye:

```text
This part repeats.
This name is vague.
This condition is crowded.
This menu is doing too much at once.
This change needs a quick test.
```

That is a real step forward.

Clean code is not perfect code.

Clean code is code you can come back to without feeling lost.

## Tomorrow

Tomorrow is:

```text
Day 54: Debugging Day: Broken Data Programs
```

Today you cleaned working code.

Tomorrow you will practice reading code that does not work yet.

The same habits will help:

```text
slow down
check the data shape
read one line at a time
test one small change
```

Refactoring and debugging are different skills, but they support each other.

Cleaner code makes bugs easier to see.
