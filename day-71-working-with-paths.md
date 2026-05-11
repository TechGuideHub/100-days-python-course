# Day 71: Working with Paths

**Focus:** Building reliable file and folder paths with `pathlib`  
**You will practice:** relative paths, the current working folder, `Path`, joining paths with `/`, creating folders, checking whether files exist, and reading or writing through path objects  
**Estimated time:** 45-60 minutes

## Today's Goal

Today you will learn how Python finds files.

On Day 69, you read from files.

On Day 70, you wrote to files.

Today is about the part that sits between those two skills:

```text
Where is the file?
```

A program can read and write correctly only when it points to the correct place.

By the end of this lesson, you should be able to:

- explain what a relative path is
- explain the current working folder in beginner terms
- use `Path` from `pathlib`
- build a path like `Path("day-71") / "notes.txt"`
- create a folder before writing a file inside it
- check whether a file or folder exists
- read and write text using path objects
- avoid putting machine-specific folder names into your code
- prepare for Day 72, where files will hold CSV data

The main idea:

```text
A path tells Python where to look.
```

## The Big Idea

A path is a file or folder address.

This is a relative path:

```text
day-71/notes.txt
```

It means:

```text
Start from the folder where the program is running.
Go into the day-71 folder.
Find notes.txt inside it.
```

You can write paths as strings:

```python
with open("day-71/notes.txt") as file:
    contents = file.read()
```

That still works.

But Python also gives you a path tool named `pathlib`.

Here is the same idea with `Path`:

```python
from pathlib import Path

notes_file = Path("day-71") / "notes.txt"

with open(notes_file) as file:
    contents = file.read()

print(contents)
```

This line is the new part:

```python
notes_file = Path("day-71") / "notes.txt"
```

Read it as:

```text
the day-71 folder, then notes.txt inside it
```

The `/` here does not divide numbers.

When the left side is a `Path`, `/` joins path pieces.

That gives you a path object.

A path object is not the file contents.

It is the location of the file.

You can use that location to read, write, check, or create things.

Example:

```python
from pathlib import Path

folder = Path("day-71")
notes_file = folder / "notes.txt"

folder.mkdir(exist_ok=True)
notes_file.write_text("Practice paths\nRead notes\n", encoding="utf-8")

contents = notes_file.read_text(encoding="utf-8")
print(contents)
```

You should see:

```text
Practice paths
Read notes
```

That program:

- builds a folder path
- builds a file path inside that folder
- creates the folder if needed
- writes text to the file
- reads the text back

This is the bridge from Day 69 and Day 70.

You are still reading and writing files.

You are now being more careful about where those files live.

## The Mental Model

Imagine your program standing in one folder.

That folder is the current working folder.

When you use a relative path, Python starts looking from there.

If your code says:

```python
Path("day-71") / "notes.txt"
```

Python does not search your whole computer.

It looks for:

```text
day-71/notes.txt
```

starting from the current working folder.

You can ask Python where it is starting from:

```python
from pathlib import Path

print("Current working folder:")
print(Path.cwd())
```

The exact answer will be different on different computers.

Do not copy that full answer into your beginner programs.

For course practice, keep using relative paths like:

```text
day-71/notes.txt
day-71/report.txt
day-72/students.csv
```

That keeps your code easier to move, share, and understand.

Here is the mental pattern:

```text
current working folder
    day-71
        notes.txt
        report.txt
```

And here is the Python pattern:

```python
from pathlib import Path

folder = Path("day-71")
notes_file = folder / "notes.txt"
report_file = folder / "report.txt"
```

The folder path points to the folder.

The file paths point to files inside that folder.

The path object does not create anything by itself.

This line only describes a place:

```python
folder = Path("day-71")
```

This line actually creates the folder:

```python
folder.mkdir(exist_ok=True)
```

That difference matters.

Building a path is like writing an address on an envelope.

Creating, reading, or writing is when Python actually goes to that address.

## Try It Yourself

Create a folder named:

```text
day-71
```

You can create it by hand, or you can let Python create it in the examples below.

Work through the steps one at a time.

### Step 1: Build A Path

Code:

```python
from pathlib import Path

folder = Path("day-71")
notes_file = folder / "notes.txt"

print(folder.as_posix())
print(notes_file.as_posix())
```

You should see:

```text
day-71
day-71/notes.txt
```

The `.as_posix()` part is only for display.

It prints the path with `/` so it is easy to read in this lesson.

Most of the time, you can use the path object directly.

### Step 2: Create The Folder

Code:

```python
from pathlib import Path

folder = Path("day-71")

folder.mkdir(exist_ok=True)

print("Folder exists:", folder.exists())
print("Is a folder:", folder.is_dir())
```

You should see:

```text
Folder exists: True
Is a folder: True
```

The `mkdir` name means:

```text
make directory
```

A directory is another word for a folder.

The `exist_ok=True` part means:

```text
If the folder already exists, do not crash.
```

That is useful while practicing because you may run the same program more than once.

### Step 3: Write Text To A Path

Code:

```python
from pathlib import Path

folder = Path("day-71")
notes_file = folder / "notes.txt"

folder.mkdir(exist_ok=True)

notes_file.write_text("Buy rice\nWash dishes\nPractice paths\n", encoding="utf-8")

print("Saved:", notes_file.exists())
print("Is a file:", notes_file.is_file())
```

You should see:

```text
Saved: True
Is a file: True
```

Open this file after running the code:

```text
day-71/notes.txt
```

It should contain:

```text
Buy rice
Wash dishes
Practice paths
```

This line writes the file:

```python
notes_file.write_text("Buy rice\nWash dishes\nPractice paths\n", encoding="utf-8")
```

`write_text()` is a `pathlib` shortcut for writing a whole text file.

It is similar to:

```python
with open(notes_file, "w") as file:
    file.write("Buy rice\nWash dishes\nPractice paths\n")
```

Both are fine.

For short text files, `write_text()` is convenient.

For longer file work, the `with open(...)` pattern is still useful.

### Step 4: Read Text From A Path

Code:

```python
from pathlib import Path

notes_file = Path("day-71") / "notes.txt"

contents = notes_file.read_text(encoding="utf-8")

print("Notes")
print("-----")
print(contents)
```

You should see:

```text
Notes
-----
Buy rice
Wash dishes
Practice paths
```

This line reads the whole file:

```python
contents = notes_file.read_text(encoding="utf-8")
```

The result is a string.

That means you can still use string tools:

```python
from pathlib import Path

notes_file = Path("day-71") / "notes.txt"
contents = notes_file.read_text(encoding="utf-8")

lines = contents.splitlines()

for line in lines:
    print("Note:", line)
```

You should see:

```text
Note: Buy rice
Note: Wash dishes
Note: Practice paths
```

`splitlines()` turns the text into a list of lines without keeping the newline characters.

### Step 5: Check Before Reading

If you try to read a file that does not exist, Python raises an error.

You can check first:

```python
from pathlib import Path

notes_file = Path("day-71") / "notes.txt"

if notes_file.exists():
    contents = notes_file.read_text(encoding="utf-8")
    print(contents)
else:
    print("No notes file yet.")
```

This is useful for programs that may run before a file has been created.

Do not overuse `exists()`.

Sometimes an error is helpful because it tells you your setup is wrong.

But for optional files, checking first is a friendly habit.

### Step 6: Keep Related Files Together

Paths help you organize a small project.

Code:

```python
from pathlib import Path

folder = Path("day-71")
folder.mkdir(exist_ok=True)

notes_file = folder / "notes.txt"
report_file = folder / "report.txt"

notes_file.write_text("Buy rice\nWash dishes\nPractice paths\n", encoding="utf-8")

notes = notes_file.read_text(encoding="utf-8").splitlines()

with open(report_file, "w") as file:
    file.write("Notes Report\n")
    file.write("------------\n")
    file.write("Total notes: " + str(len(notes)) + "\n")

print("Report saved to", report_file.as_posix())
```

You should see:

```text
Report saved to day-71/report.txt
```

Open:

```text
day-71/report.txt
```

It should contain:

```text
Notes Report
------------
Total notes: 3
```

Notice the pattern:

```python
folder = Path("day-71")
notes_file = folder / "notes.txt"
report_file = folder / "report.txt"
```

One folder.

Two files inside it.

That is easier to manage than scattering practice files everywhere.

## Common Mistake

### Mistake 1: Thinking A Path Creates The Folder

Broken code:

```python
from pathlib import Path

notes_file = Path("day-71") / "notes.txt"

notes_file.write_text("Hello\n", encoding="utf-8")
```

This is broken if the `day-71` folder does not already exist.

Building a path does not create the folder.

Fixed code:

```python
from pathlib import Path

folder = Path("day-71")
notes_file = folder / "notes.txt"

folder.mkdir(exist_ok=True)
notes_file.write_text("Hello\n", encoding="utf-8")
```

Create the folder before writing a file inside it.

### Mistake 2: Leaving Out The Folder Name

Broken code:

```python
from pathlib import Path

notes_file = Path("notes.txt")
contents = notes_file.read_text(encoding="utf-8")

print(contents)
```

This may be broken if the file is really here:

```text
day-71/notes.txt
```

Fixed code:

```python
from pathlib import Path

notes_file = Path("day-71") / "notes.txt"
contents = notes_file.read_text(encoding="utf-8")

print(contents)
```

The folder name is part of the path.

### Mistake 3: Joining Pieces By Hand

Broken code:

```python
folder = "day-71"
filename = "notes.txt"

path = folder + filename

print(path)
```

You should see:

```text
day-71notes.txt
```

That is not the path you wanted.

Fixed code:

```python
from pathlib import Path

folder = Path("day-71")
filename = "notes.txt"

path = folder / filename

print(path.as_posix())
```

You should see:

```text
day-71/notes.txt
```

Let `Path` join the pieces.

### Mistake 4: Forgetting Parentheses On `exists`

Broken code:

```python
from pathlib import Path

notes_file = Path("day-71") / "notes.txt"

if notes_file.exists:
    print("The file exists.")
else:
    print("The file is missing.")
```

This code is wrong because `exists` is a method.

You need to call it with parentheses.

Fixed code:

```python
from pathlib import Path

notes_file = Path("day-71") / "notes.txt"

if notes_file.exists():
    print("The file exists.")
else:
    print("The file is missing.")
```

The parentheses mean:

```text
run the check now
```

### Mistake 5: Confusing The Current Working Folder With The File's Folder

A Python file can live in one folder while the program is run from another folder.

Relative paths start from where the program is run.

That is why this path:

```python
Path("day-71") / "notes.txt"
```

means:

```text
Start from the current working folder.
Then look for day-71/notes.txt.
```

When a path that looks correct still fails, check the current working folder:

```python
from pathlib import Path

print(Path.cwd())
```

Use the result for debugging.

Do not paste the full result into your course examples.

## Debug It

Read the goal first.

Then study the broken code and find the problem before looking at the fix.

### Debug 1: Create A Note File

Goal:

```text
Create day-71/debug-note.txt and write one line into it.
```

Broken code:

```python
from pathlib import Path

path = Path("day-71") / "debug-note.txt"
path.write_text("Path practice\n", encoding="utf-8")
```

The problem:

```text
The code writes inside day-71, but it never creates the day-71 folder.
```

Fixed code:

```python
from pathlib import Path

folder = Path("day-71")
path = folder / "debug-note.txt"

folder.mkdir(exist_ok=True)
path.write_text("Path practice\n", encoding="utf-8")
```

### Debug 2: Read The Right File

Goal:

```text
Read day-71/notes.txt.
```

Broken code:

```python
from pathlib import Path

path = Path("notes.txt")
contents = path.read_text(encoding="utf-8")

print(contents)
```

The problem:

```text
The path points to notes.txt in the current working folder, not notes.txt inside day-71.
```

Fixed code:

```python
from pathlib import Path

path = Path("day-71") / "notes.txt"
contents = path.read_text(encoding="utf-8")

print(contents)
```

### Debug 3: Join The Path Correctly

Goal:

```text
Build the path day-71/notes.txt.
```

Broken code:

```python
from pathlib import Path

folder = Path("day-71")
path = folder + "notes.txt"

print(path)
```

The problem:

```text
Path objects do not use + to join a file name.
```

Fixed code:

```python
from pathlib import Path

folder = Path("day-71")
path = folder / "notes.txt"

print(path.as_posix())
```

You should see:

```text
day-71/notes.txt
```

### Debug 4: Check A File The Right Way

Goal:

```text
Print the file contents only if day-71/notes.txt exists.
```

Broken code:

```python
from pathlib import Path

path = Path("day-71") / "notes.txt"

if path.exists:
    print(path.read_text(encoding="utf-8"))
else:
    print("Missing file")
```

The problem:

```text
The code uses path.exists instead of path.exists().
```

Fixed code:

```python
from pathlib import Path

path = Path("day-71") / "notes.txt"

if path.exists():
    print(path.read_text(encoding="utf-8"))
else:
    print("Missing file")
```

## Read the Docs

Python's official documentation explains `pathlib` here:

[Python docs: pathlib](https://docs.python.org/3/library/pathlib.html)

You do not need to read the whole page today.

Look for these names:

- `Path`
- `Path.cwd()`
- `Path.exists()`
- `Path.is_file()`
- `Path.is_dir()`
- `Path.mkdir()`
- `Path.read_text()`
- `Path.write_text()`

The documentation also shows many advanced path tools.

Leave those for later.

For now, focus on this small beginner set:

```python
from pathlib import Path

folder = Path("day-71")
file_path = folder / "notes.txt"

folder.mkdir(exist_ok=True)

if file_path.exists():
    print(file_path.read_text(encoding="utf-8"))
```

That is enough for many small programs.

## Mini Challenge

Build a small practice folder.

Create a program that:

- creates a folder named `day-71`
- creates a file named `day-71/summary.txt`
- writes three lines into it
- reads the file back
- prints each line with a number

One possible solution:

```python
from pathlib import Path

folder = Path("day-71")
summary_file = folder / "summary.txt"

folder.mkdir(exist_ok=True)

summary_file.write_text(
    "I practiced relative paths\n"
    "I used pathlib\n"
    "I checked whether files exist\n",
    encoding="utf-8",
)

contents = summary_file.read_text(encoding="utf-8")
lines = contents.splitlines()

for index, line in enumerate(lines, start=1):
    print(str(index) + ". " + line)
```

You should see:

```text
1. I practiced relative paths
2. I used pathlib
3. I checked whether files exist
```

After it works, change the file name to:

```text
day-71/second-summary.txt
```

Run the program again.

You should now have two files inside the same folder.

## Real-World Use

Paths matter because real programs usually have more than one file.

A small program might have:

```text
data/input.txt
reports/summary.txt
logs/practice-log.txt
```

A path lets the program say exactly which file it means.

That becomes more important when files have similar names.

Example:

```text
day-71/notes.txt
day-71/report.txt
day-72/students.csv
```

Each path points to a different file.

The file name alone is not always enough.

The folder gives the file context.

Here is a simple report example:

```python
from pathlib import Path

folder = Path("day-71")
folder.mkdir(exist_ok=True)

source_file = folder / "notes.txt"
report_file = folder / "report.txt"

source_file.write_text("read files\nwrite files\nuse paths\n", encoding="utf-8")

topics = source_file.read_text(encoding="utf-8").splitlines()

with open(report_file, "w") as file:
    file.write("Practice Topics\n")
    file.write("---------------\n")

    for topic in topics:
        file.write("- " + topic + "\n")

print("Created", report_file.as_posix())
```

You should see:

```text
Created day-71/report.txt
```

This is the same read-and-write work from Days 69 and 70.

The new habit is keeping the file locations clear.

Tomorrow, the files will contain comma-separated values.

Those files will still need paths.

Before Python can read rows from a CSV file, it still needs to know where that CSV file is:

```python
from pathlib import Path

csv_file = Path("day-72") / "students.csv"
```

That one line will feel familiar because of today's practice.

## Recap

Today you learned how to work with paths.

You practiced:

- using relative paths
- thinking about the current working folder
- importing `Path` from `pathlib`
- joining path pieces with `/`
- creating a folder with `mkdir`
- using `exist_ok=True`
- checking files and folders with `exists()`, `is_file()`, and `is_dir()`
- writing text with `write_text()`
- reading text with `read_text()`
- using path objects with `open()`
- keeping related files inside a folder

The main pattern:

```python
from pathlib import Path

folder = Path("day-71")
file_path = folder / "notes.txt"

folder.mkdir(exist_ok=True)
file_path.write_text("Hello\n", encoding="utf-8")
```

The reading pattern:

```python
from pathlib import Path

file_path = Path("day-71") / "notes.txt"
contents = file_path.read_text(encoding="utf-8")

print(contents)
```

The safety check:

```python
if file_path.exists():
    print("Found it")
else:
    print("Missing file")
```

The main habit:

```text
Use relative paths and build them carefully.
```

## Lesson Checklist

- [ ] I can explain what a path is.
- [ ] I can explain what a relative path is.
- [ ] I can explain the current working folder.
- [ ] I can import `Path` from `pathlib`.
- [ ] I can create a folder path with `Path("day-71")`.
- [ ] I can build a file path with `Path("day-71") / "notes.txt"`.
- [ ] I can create a folder with `mkdir`.
- [ ] I can use `exist_ok=True` when creating a practice folder.
- [ ] I can check whether a path exists with `exists()`.
- [ ] I can check whether a path is a file with `is_file()`.
- [ ] I can check whether a path is a folder with `is_dir()`.
- [ ] I can write text using `write_text()`.
- [ ] I can read text using `read_text()`.
- [ ] I can use a path object with `open()`.
- [ ] I can avoid full machine-specific paths in beginner code.

## Exercises

### Exercise 1: Build A Path

Write a program that creates this path object:

```text
day-71/colors.txt
```

Print it with:

```python
print(path.as_posix())
```

You should see:

```text
day-71/colors.txt
```

### Exercise 2: Create A Folder

Write a program that creates:

```text
day-71
```

Then print:

```text
Folder ready
```

Use `mkdir(exist_ok=True)`.

### Exercise 3: Write A Colors File

Create:

```text
day-71/colors.txt
```

Write three colors into it, one per line.

Use `write_text()`.

### Exercise 4: Read The Colors File

Read:

```text
day-71/colors.txt
```

Print the whole file.

Then use `splitlines()` and print each color like this:

```text
Color: blue
```

### Exercise 5: Check Before Reading

Write a program that checks whether this file exists:

```text
day-71/missing.txt
```

If it exists, read it.

If it does not exist, print:

```text
No file yet
```

### Exercise 6: Fix The Missing Folder

Broken code:

```python
from pathlib import Path

path = Path("day-71") / "tasks.txt"
path.write_text("study\nclean\nread\n", encoding="utf-8")
```

Fix it so the folder is created before the file is written.

### Exercise 7: Fix The Wrong Path

Broken code:

```python
from pathlib import Path

path = Path("tasks.txt")
print(path.read_text(encoding="utf-8"))
```

The file is named:

```text
day-71/tasks.txt
```

Fix the path.

### Exercise 8: Build Two Files In One Folder

Create paths for:

```text
day-71/input.txt
day-71/output.txt
```

Write a few words to `input.txt`.

Read `input.txt`.

Write this to `output.txt`:

```text
Copied text:
```

Then write the text you read from `input.txt`.

### Exercise 9: Use A Function

Write a function named `read_text_file`.

It should receive a path.

It should:

- check whether the path exists
- return the file contents if it exists
- return an empty string if it does not exist

Try it with:

```python
path = Path("day-71") / "notes.txt"
text = read_text_file(path)
print(text)
```

### Exercise 10: Practice Current Working Folder

Write this program:

```python
from pathlib import Path

print(Path.cwd())
```

Run it.

In your own words, write down what folder Python starts from when it runs your program.

Do not paste the full folder path into your course code.

### Exercise 11: Make A Simple Report

Create:

```text
day-71/books.txt
```

Put three book titles in it.

Read the titles.

Create:

```text
day-71/book-report.txt
```

The report should contain:

```text
Book Report
-----------
Total books: 3
```

### Exercise 12: Preview Tomorrow

Create this path object:

```text
day-72/students.csv
```

Print it with `.as_posix()`.

Do not worry about CSV code yet.

Just practice building the path:

```python
from pathlib import Path

csv_file = Path("day-72") / "students.csv"
print(csv_file.as_posix())
```

You should see:

```text
day-72/students.csv
```

## Tiny Win

You can now tell Python where files belong.

That may sound small, but it makes your file programs much less fragile.

Reading and writing are the actions.

Paths are the directions.

When the directions are clear, the rest of the file work becomes easier to trust.

## Tomorrow

Tomorrow is:

```text
Day 72: CSV Files
```

Today, you learned how to point Python to the right file.

Tomorrow, you will use that skill with CSV files.

A CSV file is a plain text file that stores table-shaped data.

The path part will look familiar:

```python
from pathlib import Path

csv_file = Path("day-72") / "students.csv"
```

The new part will be reading and writing rows instead of plain paragraphs.
