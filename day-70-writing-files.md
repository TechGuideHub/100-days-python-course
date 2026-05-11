# Day 70: Writing Files

**Focus:** Saving text into files from Python  
**You will practice:** `open(..., "w")`, `with`, `.write()`, appending with `"a"`, newline characters, overwrite safety, and simple log files  
**Estimated time:** 45-60 minutes

## Today's Goal

Today you will learn how to write text into files.

So far, most of your programs have shown information with `print()`.

That is useful while a program is running.

But sometimes you want the result to stay after the program ends.

For that, you need a file.

Today you will practice writing plain text files.

After today, you should be able to:

- create a text file from Python
- write text with `.write()`
- use `with` so Python closes the file for you
- understand what `"w"` mode does
- avoid accidentally replacing important file contents
- append new text with `"a"` mode
- use `\n` to put text on separate lines
- save a simple log from a program
- prepare for Day 71, where you will work with paths

The main idea:

```text
print() sends text to the screen.
.write() sends text to a file.
```

Both are useful.

They just send text to different places.

## The Big Idea

Here is a small program that writes a file.

Create a file named:

```text
day-70/write_notes.py
```

Code:

```python
with open("notes.txt", "w") as file:
    file.write("Today I practiced writing files.")

print("Done")
```

When you run the program, you should see:

```text
Done
```

You should also see a new file named:

```text
notes.txt
```

Open that file.

It should contain:

```text
Today I practiced writing files.
```

This line does the main work:

```python
with open("notes.txt", "w") as file:
```

It means:

```text
Open a file named notes.txt.
Open it in write mode.
Give me a file variable while I am inside the with block.
Close the file when the block is finished.
```

The `"w"` means write mode.

Write mode can create a new file.

It can also replace an existing file.

That second part matters.

If `notes.txt` already exists, this code clears the old contents before writing the new text:

```python
with open("notes.txt", "w") as file:
    file.write("New notes")
```

Be careful with `"w"`.

It is useful, but it is not gentle.

For beginner projects, use small practice files while you are learning.

## The Mental Model

Think of a file like a notebook.

Opening a file in `"w"` mode is like opening the notebook to a fresh blank page.

Then `.write()` puts words onto that page.

Example:

```python
with open("todo.txt", "w") as file:
    file.write("Practice Python")
```

The file now contains:

```text
Practice Python
```

But `.write()` does not add a new line automatically.

This code writes two pieces of text:

```python
with open("todo.txt", "w") as file:
    file.write("Practice Python")
    file.write("Review notes")
```

The file contains:

```text
Practice PythonReview notes
```

Python did exactly what you asked.

It wrote the first string.

Then it wrote the second string immediately after it.

If you want the text on separate lines, add newline characters.

Code:

```python
with open("todo.txt", "w") as file:
    file.write("Practice Python\n")
    file.write("Review notes\n")
```

The file contains:

```text
Practice Python
Review notes
```

The `\n` means:

```text
start a new line
```

You will use it often when writing text files.

## Try It Yourself

Create a folder named:

```text
day-70
```

Then create this file:

```text
day-70/write_notes.py
```

Work through the steps one at a time.

### Step 1: Write One Line

Code:

```python
with open("notes.txt", "w") as file:
    file.write("My first saved note.")

print("Note saved")
```

Run the program.

You should see:

```text
Note saved
```

Now open:

```text
notes.txt
```

It should contain:

```text
My first saved note.
```

The program printed one message to the screen.

It wrote a different message into the file.

### Step 2: Write More Than One Line

Change your program to this:

```python
with open("notes.txt", "w") as file:
    file.write("Things I practiced:\n")
    file.write("writing files\n")
    file.write("using with\n")
    file.write("adding new lines\n")

print("Notes saved")
```

Run the program again.

Open `notes.txt`.

You should see:

```text
Things I practiced:
writing files
using with
adding new lines
```

Each `\n` moves the next text to a new line.

### Step 3: Notice Overwrite Mode

Change your program to this:

```python
with open("notes.txt", "w") as file:
    file.write("This replaced the old notes.\n")

print("Notes replaced")
```

Run it.

Open `notes.txt`.

You should see:

```text
This replaced the old notes.
```

The old lines are gone.

That happened because `"w"` means write mode.

Write mode starts from an empty file.

This is useful when you want a fresh file.

It is risky when you meant to keep the old text.

### Step 4: Append Instead Of Replacing

Now create this file:

```text
day-70/append_log.py
```

Code:

```python
with open("practice_log.txt", "a") as file:
    file.write("Practiced writing files\n")

print("Log updated")
```

Run the program once.

Open `practice_log.txt`.

You should see:

```text
Practiced writing files
```

Run the program again.

Open `practice_log.txt` again.

Now you should see:

```text
Practiced writing files
Practiced writing files
```

The `"a"` means append mode.

Append mode adds new text to the end of the file.

It does not clear the old text first.

### Step 5: Save A Simple Log

Create this file:

```text
day-70/save_log.py
```

Code:

```python
name = input("What did you practice today? ")
minutes = input("How many minutes did you practice? ")

with open("learning_log.txt", "a") as file:
    file.write("Practice: " + name + "\n")
    file.write("Minutes: " + minutes + "\n")
    file.write("---\n")

print("Saved to learning_log.txt")
```

Run it.

Example input:

```text
What did you practice today? files
How many minutes did you practice? 20
```

You should see:

```text
Saved to learning_log.txt
```

Open `learning_log.txt`.

You should see:

```text
Practice: files
Minutes: 20
---
```

Run the program again with different answers.

The new entry should be added below the old one.

That is a small log file.

It is not fancy.

It is just saved text.

That is enough for many useful beginner programs.

## Common Mistake

The most common mistake is using `"w"` when you meant to keep the old file contents.

Example:

```python
with open("practice_log.txt", "w") as file:
    file.write("Practiced loops\n")
```

This creates `practice_log.txt` if it does not exist.

But if the file already exists, the old contents are cleared.

If you want to add a new entry to the end, use `"a"`:

```python
with open("practice_log.txt", "a") as file:
    file.write("Practiced loops\n")
```

A simple rule:

```text
Use "w" when you want a fresh file.
Use "a" when you want to add to the file.
```

Another common mistake is forgetting `\n`.

Broken code:

```python
with open("tasks.txt", "w") as file:
    file.write("Buy rice")
    file.write("Wash dishes")
    file.write("Read")
```

The file contains:

```text
Buy riceWash dishesRead
```

Fixed code:

```python
with open("tasks.txt", "w") as file:
    file.write("Buy rice\n")
    file.write("Wash dishes\n")
    file.write("Read\n")
```

The file contains:

```text
Buy rice
Wash dishes
Read
```

Newline characters are small, but they change the shape of the file.

## Debug It

This program is supposed to save three tasks on three separate lines.

Broken code:

```python
tasks = ["study", "walk", "read"]

with open("tasks.txt", "w") as file:
    for task in tasks:
        file.write(task)

print("Tasks saved")
```

The program runs.

It does not crash.

But `tasks.txt` contains:

```text
studywalkread
```

The bug is that the program writes each task without a newline.

Fix:

```python
tasks = ["study", "walk", "read"]

with open("tasks.txt", "w") as file:
    for task in tasks:
        file.write(task + "\n")

print("Tasks saved")
```

Now `tasks.txt` contains:

```text
study
walk
read
```

Here is another broken program.

It is supposed to keep adding scores to a score log.

Broken code:

```python
score = 8

with open("scores.txt", "w") as file:
    file.write("Score: " + str(score) + "\n")

print("Score saved")
```

The first run looks fine.

The problem appears after several runs.

Each run replaces the old score.

If you want a log, use append mode:

```python
score = 8

with open("scores.txt", "a") as file:
    file.write("Score: " + str(score) + "\n")

print("Score saved")
```

Now each run adds a new score.

When a file-writing program behaves strangely, ask these questions:

- Am I using `"w"` or `"a"`?
- Did I add `\n` where I want a new line?
- Am I writing strings?
- Am I opening the file I think I am opening?

The last question is about paths.

You will handle that more carefully tomorrow.

## Read the Docs

Python's official documentation explains `open()` here:

[Python docs: open](https://docs.python.org/3/library/functions.html#open)

Today, focus on these pieces:

- the file name
- the mode
- `"w"` for writing
- `"a"` for appending
- text files

The documentation also explains file object methods here:

[Python docs: file object methods](https://docs.python.org/3/library/io.html#io.TextIOBase.write)

Today, focus on `.write()`.

You do not need to understand every file option yet.

Try this:

```text
Find the part of the docs that lists file modes.
Find "w".
Find "a".
Write down the difference in your own words.
```

The goal is not to memorize every mode.

The goal is to recognize the two modes you used today.

## Mini Challenge

Build a small mood log.

Create a file named:

```text
day-70/mood_log.py
```

The program should:

- ask the user how they feel
- ask for one short note
- append both answers to `mood_log.txt`
- put each entry on its own small block

Example run:

```text
Mood: focused
Note: finished file practice
Saved
```

Example file contents:

```text
Mood: focused
Note: finished file practice
---
```

Starter code:

```python
mood = input("Mood: ")
note = input("Note: ")

with open("mood_log.txt", "a") as file:
    file.write("Mood: " + mood + "\n")
    file.write("Note: " + note + "\n")
    file.write("---\n")

print("Saved")
```

Run it at least twice.

Then open `mood_log.txt` and check that both entries are still there.

## Real-World Use

Writing files is useful any time a program needs to remember something.

Small examples:

- save a practice log
- save a score history
- save notes from user input
- save a simple receipt
- save a report from a list or dictionary
- save a list of tasks
- save a text summary before closing the program

Example:

```python
items = ["rice", "tea", "apples"]

with open("shopping_list.txt", "w") as file:
    file.write("Shopping List\n")
    file.write("-------------\n")

    for item in items:
        file.write(item + "\n")

print("Shopping list saved")
```

The file contains:

```text
Shopping List
-------------
rice
tea
apples
```

This is the same kind of work you have already done with `print()`.

The difference is the destination.

Instead of sending each line to the screen, you send each line to a file.

That small change makes your program more useful.

## Recap

Today you learned how to write text files.

You used `open()` with write mode:

```python
with open("notes.txt", "w") as file:
    file.write("Hello\n")
```

You used append mode:

```python
with open("log.txt", "a") as file:
    file.write("New entry\n")
```

You learned that:

- `"w"` writes a fresh file
- `"w"` can replace old contents
- `"a"` appends to the end
- `.write()` writes strings
- `.write()` does not add new lines by itself
- `\n` starts a new line
- `with` closes the file for you

The biggest safety habit:

```text
Check the mode before running code that writes to a file.
```

If you want to keep old contents, do not use `"w"` unless you really mean it.

## Lesson Checklist

- [ ] I can open a file in write mode with `"w"`.
- [ ] I can use `with open(...) as file`.
- [ ] I can write text with `.write()`.
- [ ] I can explain why `.write()` is different from `print()`.
- [ ] I can use `\n` to put text on a new line.
- [ ] I can explain why `"w"` can be risky.
- [ ] I can open a file in append mode with `"a"`.
- [ ] I can save a simple log file.
- [ ] I can write lines from a list into a file.
- [ ] I can check a text file after my program runs.

## Exercises

### Exercise 1: Save One Note

Create:

```text
day-70/save_one_note.py
```

Ask the user for one note.

Save it to:

```text
note.txt
```

Example:

```text
Note: review strings
Saved
```

The file should contain:

```text
review strings
```

### Exercise 2: Save Three Tasks

Create:

```text
day-70/save_tasks.py
```

Use this list:

```python
tasks = ["study", "clean", "read"]
```

Write each task to `tasks.txt` on its own line.

The file should contain:

```text
study
clean
read
```

### Exercise 3: Append A Habit Log

Create:

```text
day-70/habit_log.py
```

Ask the user for:

- habit name
- number of minutes

Append the entry to:

```text
habit_log.txt
```

Example file contents after two runs:

```text
Habit: reading
Minutes: 15
---
Habit: walking
Minutes: 20
---
```

### Exercise 4: Fix The Missing Newlines

Broken code:

```python
names = ["Mina", "Sam", "Iris"]

with open("names.txt", "w") as file:
    for name in names:
        file.write(name)
```

Fix it so the file contains:

```text
Mina
Sam
Iris
```

### Exercise 5: Choose The Right Mode

For each situation, write down `"w"` or `"a"`.

```text
Create a fresh report every time.
Add today's practice to a log.
Replace an old shopping list with a new one.
Keep adding scores after each game.
Save one final receipt.
```

Then explain one answer in your own words.

### Exercise 6: Save A Receipt

Create:

```text
day-70/save_receipt.py
```

Use this data:

```python
items = ["rice", "tea", "apples"]
total = 340
```

Write a receipt to `receipt.txt`.

Example file contents:

```text
Receipt
-------
rice
tea
apples
Total: 340
```

### Exercise 7: Save A Quiz Result

Create:

```text
day-70/quiz_result.py
```

Ask the user for:

- name
- score

Append the result to `quiz_results.txt`.

Example file contents:

```text
Name: Mina
Score: 8
---
Name: Sam
Score: 10
---
```

### Exercise 8: Write A Report From A Dictionary

Use this dictionary:

```python
student = {
    "name": "Mina",
    "course": "Python",
    "level": "Beginner",
}
```

Write this file:

```text
student_report.txt
```

Expected file contents:

```text
Student Report
--------------
Name: Mina
Course: Python
Level: Beginner
```

### Exercise 9: Compare Print And Write

Write a program that prints a message to the screen and writes a different message to a file.

Example:

```python
print("This appears on the screen")

with open("message.txt", "w") as file:
    file.write("This appears in the file\n")
```

Run it.

Then explain where each message went.

### Exercise 10: Review Before Running

Before you run this code, answer the questions below it.

```python
with open("journal.txt", "w") as file:
    file.write("Fresh start\n")
```

Questions:

```text
Will this create the file if it does not exist?
Will this keep old text if the file already exists?
What mode would you use to add a new journal entry instead?
```

Then run your own small version with a practice file.

Do not test overwrite behavior on an important file.

## Tiny Win

You can now make a program leave something behind.

That is a quiet but important step.

Your programs are no longer limited to screen output.

They can create notes, logs, receipts, reports, and records.

## Tomorrow

Tomorrow is:

```text
Day 71: Working with Paths
```

Today you used simple file names like:

```text
notes.txt
practice_log.txt
receipt.txt
```

That keeps the focus on writing files.

Tomorrow you will look more carefully at where files are saved, how relative paths work, and how to build file names that point to the right place.
