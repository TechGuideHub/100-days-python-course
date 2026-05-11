# Day 69: Reading Files

**Focus:** Reading text from files with `open()`  
**You will practice:** opening files, using `with`, reading the whole file with `.read()`, reading one line at a time, using relative file names, and handling newline characters  
**Estimated time:** 45-60 minutes

## Today's Goal

Today you will learn how to read text from a file.

So far, most of your programs have worked with information written directly in the code:

```python
notes = ["buy rice", "wash dishes", "practice Python"]

for note in notes:
    print(note)
```

That works for practice.

But real programs often need information that lives outside the program:

```text
a list of tasks
a saved score
a report
a message
a menu
a set of names
```

That information can be stored in a file.

Today you will start with text files.

By the end of this lesson, you should be able to:

- open a text file with `open()`
- read a whole file with `.read()`
- use `with` so Python closes the file for you
- read a file one line at a time
- use relative file names like `day-69/notes.txt`
- understand why newline characters appear
- remove extra line breaks with `.strip()`
- debug a missing-file error
- prepare for writing files tomorrow

The main idea:

```text
A file lets a program use information that was saved outside the code.
```

## The Big Idea

Create a folder named:

```text
day-69
```

Inside it, create a text file named:

```text
notes.txt
```

Put this text inside `notes.txt`:

```text
Buy rice
Wash dishes
Practice Python
```

Now create a Python file named:

```text
day-69/read_notes.py
```

Add this code:

```python
file = open("day-69/notes.txt")
contents = file.read()
file.close()

print(contents)
```

You should see:

```text
Buy rice
Wash dishes
Practice Python
```

This line opens the file:

```python
file = open("day-69/notes.txt")
```

This line reads the text inside the file:

```python
contents = file.read()
```

This line closes the file:

```python
file.close()
```

Closing the file tells Python that you are finished using it.

The code above works, but there is a better habit:

```python
with open("day-69/notes.txt") as file:
    contents = file.read()

print(contents)
```

You should see the same output:

```text
Buy rice
Wash dishes
Practice Python
```

The `with` version is the one you should practice.

It opens the file, lets you use it inside the indented block, and closes it automatically when the block ends.

That means this is the beginner pattern to remember:

```python
with open("file-name.txt") as file:
    contents = file.read()
```

The file name can include a folder:

```python
with open("day-69/notes.txt") as file:
    contents = file.read()
```

That is a relative file name.

It means:

```text
Start from where the program is being run.
Then look for the day-69 folder.
Then look for notes.txt inside it.
```

For this course, use relative file names in your examples.

Do not put your computer's full folder path into beginner code.

## The Mental Model

Think of a text file like a notebook sitting beside your program.

The program does not automatically know what is inside the notebook.

It needs to:

```text
open the notebook
read the words
use the words
close the notebook
```

In Python, that becomes:

```python
with open("day-69/notes.txt") as file:
    contents = file.read()

print(contents)
```

Inside the `with` block, the file is open.

The name `file` is a variable that refers to the open file.

This line:

```python
contents = file.read()
```

takes the file's text and stores it in a string.

After the block ends, Python closes the file.

You can still use `contents` because it is a normal string now:

```python
with open("day-69/notes.txt") as file:
    contents = file.read()

print("File contents:")
print(contents)
print("Characters:", len(contents))
```

You should see something like:

```text
File contents:
Buy rice
Wash dishes
Practice Python
Characters: 37
```

The exact character count can change if your file has an extra blank line at the end.

That is normal.

Text files remember line breaks too.

When you press Enter in a text file, the file stores a newline character.

Python writes that newline character as:

```text
\n
```

You do not need to memorize all the details today.

Just know this:

```text
Lines in a file usually end with a hidden newline character.
```

That matters when you read the file one line at a time.

## Try It Yourself

Create these files:

```text
day-69/notes.txt
day-69/read_notes.py
```

Put this text in `day-69/notes.txt`:

```text
Buy rice
Wash dishes
Practice Python
```

Work through these examples one at a time.

### Step 1: Read The Whole File

Code:

```python
with open("day-69/notes.txt") as file:
    contents = file.read()

print(contents)
```

You should see:

```text
Buy rice
Wash dishes
Practice Python
```

`.read()` gives you the whole file as one string.

That is useful when the file is small and you want all of it at once.

Try this:

```text
Add one more line to notes.txt.
Run the program again.
Notice that the Python code does not need to change.
```

### Step 2: Add A Heading

Code:

```python
with open("day-69/notes.txt") as file:
    contents = file.read()

print("Today's Notes")
print("-------------")
print(contents)
```

You should see:

```text
Today's Notes
-------------
Buy rice
Wash dishes
Practice Python
```

The file gives the program text.

The program can still add its own text around it.

That is one reason files matter.

The saved data and the program logic can stay separate.

### Step 3: Read One Line At A Time

Sometimes you want to handle each line separately.

Code:

```python
with open("day-69/notes.txt") as file:
    for line in file:
        print("Note:", line)
```

You may see extra blank lines:

```text
Note: Buy rice

Note: Wash dishes

Note: Practice Python
```

That happens because each `line` from the file already includes a newline character at the end.

Then `print()` adds another newline after it prints.

So you get two line breaks.

### Step 4: Remove The Extra Line Break

Use `.strip()` to remove extra whitespace from the start and end of a string.

Code:

```python
with open("day-69/notes.txt") as file:
    for line in file:
        clean_line = line.strip()
        print("Note:", clean_line)
```

You should see:

```text
Note: Buy rice
Note: Wash dishes
Note: Practice Python
```

`.strip()` is useful when reading lines from a file.

It removes the newline at the end of each line.

It also removes extra spaces at the start or end of the line, so use it when that is what you want.

### Step 5: Store Lines In A List

You can build a list from the file.

Code:

```python
notes = []

with open("day-69/notes.txt") as file:
    for line in file:
        notes.append(line.strip())

print(notes)
print("First note:", notes[0])
print("Total notes:", len(notes))
```

You should see:

```text
['Buy rice', 'Wash dishes', 'Practice Python']
First note: Buy rice
Total notes: 3
```

This pattern is common:

```text
open a file
loop through each line
clean the line
store or use the line
```

### Step 6: Use The File Text In A Function

You can keep the file-reading part small by putting it in a function.

Code:

```python
def read_notes(filename):
    notes = []

    with open(filename) as file:
        for line in file:
            notes.append(line.strip())

    return notes


notes = read_notes("day-69/notes.txt")

for note in notes:
    print("- " + note)
```

You should see:

```text
- Buy rice
- Wash dishes
- Practice Python
```

The function receives the file name.

It returns a list of clean lines.

The printing happens after the function call.

That keeps the jobs clear.

## Common Mistake

### Mistake 1: Using The Wrong File Name

Broken code:

```python
with open("notes.txt") as file:
    contents = file.read()

print(contents)
```

This may be broken if `notes.txt` is inside the `day-69` folder.

Python looks for exactly the file name you give it.

If the file is here:

```text
day-69/notes.txt
```

then open it like this:

```python
with open("day-69/notes.txt") as file:
    contents = file.read()

print(contents)
```

The path is part of the file name.

When you see an error like:

```text
FileNotFoundError
```

first check the spelling, folder name, and file name.

### Mistake 2: Forgetting That `.read()` Returns A String

Broken code:

```python
with open("day-69/notes.txt") as file:
    contents = file.read()

for note in contents:
    print(note)
```

This code runs, but it prints one character at a time.

That is because `contents` is one string.

Looping over a string gives one character at a time.

If you want one line at a time, loop over the file:

```python
with open("day-69/notes.txt") as file:
    for line in file:
        print(line.strip())
```

Or turn the text into lines:

```python
with open("day-69/notes.txt") as file:
    contents = file.read()

lines = contents.splitlines()

for line in lines:
    print(line)
```

Both versions give you lines instead of characters.

### Mistake 3: Getting Extra Blank Lines

Code:

```python
with open("day-69/notes.txt") as file:
    for line in file:
        print(line)
```

You may see:

```text
Buy rice

Wash dishes

Practice Python
```

This is not a serious problem.

It is a newline problem.

Each line from the file already has a line break.

`print()` adds another one.

Use `.strip()`:

```python
with open("day-69/notes.txt") as file:
    for line in file:
        print(line.strip())
```

You should see:

```text
Buy rice
Wash dishes
Practice Python
```

### Mistake 4: Reading A File Twice And Expecting The Same Result

Code:

```python
with open("day-69/notes.txt") as file:
    first_read = file.read()
    second_read = file.read()

print("First read:")
print(first_read)
print("Second read:")
print(second_read)
```

You should see:

```text
First read:
Buy rice
Wash dishes
Practice Python
Second read:
```

The second read is empty because the file has already been read to the end.

For now, keep it simple:

```text
Read the file once.
Save the result in a variable.
Use that variable as many times as you need.
```

## Debug It

Read each goal first.

Then study the broken code and find the problem before looking at the fix.

### Debug 1: Missing Folder In The File Name

Goal:

```text
Print the contents of day-69/notes.txt.
```

Broken code:

```python
with open("notes.txt") as file:
    contents = file.read()

print(contents)
```

The problem:

```text
The file is inside the day-69 folder.
The code only looks for notes.txt in the current folder.
```

Fixed code:

```python
with open("day-69/notes.txt") as file:
    contents = file.read()

print(contents)
```

### Debug 2: Extra Blank Lines

Goal:

```text
Note: Buy rice
Note: Wash dishes
Note: Practice Python
```

Broken code:

```python
with open("day-69/notes.txt") as file:
    for line in file:
        print("Note:", line)
```

The problem:

```text
Each line already has a newline at the end.
print() adds another newline.
```

Fixed code:

```python
with open("day-69/notes.txt") as file:
    for line in file:
        print("Note:", line.strip())
```

You should see:

```text
Note: Buy rice
Note: Wash dishes
Note: Practice Python
```

### Debug 3: Character By Character Output

Goal:

```text
Buy rice
Wash dishes
Practice Python
```

Broken code:

```python
with open("day-69/notes.txt") as file:
    contents = file.read()

for line in contents:
    print(line)
```

The problem:

```text
contents is one string.
Looping over a string gives one character at a time.
```

Fixed code:

```python
with open("day-69/notes.txt") as file:
    for line in file:
        print(line.strip())
```

You should see:

```text
Buy rice
Wash dishes
Practice Python
```

### Debug 4: Code Outside The `with` Block

Goal:

```text
Read the file safely and print the contents.
```

Broken code:

```python
with open("day-69/notes.txt") as file:
    contents = file.read()
    print(contents)
```

This code works.

The problem is not a crash.

The problem is that the printing does not need the file to stay open.

A cleaner version reads the file inside the `with` block, then prints after the file is closed:

```python
with open("day-69/notes.txt") as file:
    contents = file.read()

print(contents)
```

This keeps the file work in one small place.

Use the open file only while you need it.

Use the text after that.

## Read the Docs

Python's official documentation explains `open()` here:

```text
https://docs.python.org/3/library/functions.html#open
```

You do not need to understand every option.

Today, look for the simple shape:

```python
open(file)
```

The word `file` in the docs means the file name or path you want to open.

In this lesson, that looks like:

```python
open("day-69/notes.txt")
```

You may also see examples that include a mode:

```python
open("day-69/notes.txt", "r")
```

The `"r"` means read mode.

Read mode is the default, so these two lines mean the same thing for today's work:

```python
open("day-69/notes.txt")
open("day-69/notes.txt", "r")
```

You may also want to read about file objects:

```text
https://docs.python.org/3/tutorial/inputoutput.html#reading-and-writing-files
```

For today, focus on:

- `open()`
- `with`
- `.read()`
- looping over a file

Leave writing files for tomorrow.

## Mini Challenge

Create this file:

```text
day-69/tasks.txt
```

Put at least four tasks in it:

```text
Review strings
Practice loops
Read a file
Take a break
```

Then create:

```text
day-69/task_report.py
```

Write a program that:

- reads every line from `day-69/tasks.txt`
- removes the newline from each line
- stores the clean tasks in a list
- prints a short report

One possible solution:

```python
tasks = []

with open("day-69/tasks.txt") as file:
    for line in file:
        tasks.append(line.strip())

print("Task Report")
print("-----------")
print("Total tasks:", len(tasks))

for task in tasks:
    print("- " + task)
```

You should see:

```text
Task Report
-----------
Total tasks: 4
- Review strings
- Practice loops
- Read a file
- Take a break
```

After it works, add one more line to `tasks.txt`.

Run the program again.

Notice that the program can handle the new file content without changing the Python code.

## Real-World Use

Files matter because they let information survive outside a running program.

If a program only stores data in variables, the data disappears when the program ends.

Files give the program a way to use saved information later.

Programs read files for many reasons:

- loading settings
- showing saved notes
- reading a list of names
- opening a report
- checking saved scores
- importing data from another program
- reading a menu or message

Example:

```python
with open("day-69/message.txt") as file:
    message = file.read()

print("Saved message:")
print(message)
```

If `day-69/message.txt` contains:

```text
Remember to practice for ten minutes.
```

the program should show:

```text
Saved message:
Remember to practice for ten minutes.
```

The message lives in the file.

The program decides what to do with it.

That separation becomes more important as programs grow.

Today, your program reads saved text.

Tomorrow, your program will create or change saved text.

## Recap

Today you learned how to read text files.

You practiced:

- opening a file with `open()`
- using `with` to close the file automatically
- reading the whole file with `.read()`
- storing file contents in a string
- looping through a file one line at a time
- using relative file names
- understanding why extra blank lines appear
- using `.strip()` to remove newline characters
- building a list from file lines
- spotting `FileNotFoundError`

The key pattern:

```python
with open("day-69/notes.txt") as file:
    contents = file.read()
```

The line-by-line pattern:

```python
with open("day-69/notes.txt") as file:
    for line in file:
        print(line.strip())
```

The main habit:

```text
Use a relative file name, read the file inside the with block, then work with the text.
```

## Lesson Checklist

Before moving on, check that you can:

- explain why programs use files
- create a small `.txt` file for a program to read
- open a file with `open()`
- read a whole file with `.read()`
- use `with open(...) as file`
- explain why `with` is helpful
- use a relative file name like `day-69/notes.txt`
- tell the difference between reading the whole file and reading one line at a time
- loop over a file
- remove newline characters with `.strip()`
- store clean lines in a list
- debug a wrong file name
- recognize `FileNotFoundError`
- avoid full computer-specific paths in beginner examples

## Exercises

### Exercise 1

Create a file named:

```text
day-69/colors.txt
```

Add three colors, one per line.

Write a program that reads the whole file with `.read()` and prints it.

### Exercise 2

Change your program from Exercise 1 so it prints a heading before the file contents.

Example heading:

```text
Favorite Colors
---------------
```

### Exercise 3

Create a file named:

```text
day-69/friends.txt
```

Add at least four names.

Write a program that prints each name with:

```text
Hello,
```

Example output:

```text
Hello, Mina
Hello, Sam
```

Use `.strip()` so the output does not have extra blank lines.

### Exercise 4

Read `day-69/friends.txt` and store the clean names in a list.

Print the list.

Then print:

```text
Total friends:
```

followed by the number of names.

### Exercise 5

Create a file named:

```text
day-69/scores.txt
```

Add numbers, one per line:

```text
10
20
15
```

Read each line, convert it to an integer with `int()`, and add it to a total.

Print the total.

### Exercise 6

Fix the broken code.

Broken code:

```python
with open("colors.txt") as file:
    contents = file.read()

print(contents)
```

The file is named:

```text
day-69/colors.txt
```

### Exercise 7

Fix the extra blank lines.

Broken code:

```python
with open("day-69/friends.txt") as file:
    for line in file:
        print("Friend:", line)
```

Use `.strip()`.

### Exercise 8

Predict what this program prints:

```python
with open("day-69/notes.txt") as file:
    contents = file.read()

print(type(contents))
print(len(contents) > 0)
```

Then run it and check your prediction.

### Exercise 9

Write a function named `read_lines`.

It should receive a file name.

It should return a list of clean lines.

Use it with:

```python
notes = read_lines("day-69/notes.txt")
print(notes)
```

### Exercise 10

Create a file named:

```text
day-69/quote.txt
```

Add one short quote or sentence.

Read the file and print:

```text
Quote of the day:
```

Then print the quote.

### Exercise 11

Create a file named:

```text
day-69/menu.txt
```

Add three food items.

Write a program that prints:

```text
Menu
----
1. first item
2. second item
3. third item
```

Hint:

```text
Use a counter variable that starts at 1.
```

### Exercise 12

Review one older program that uses a list written directly in Python.

Move the list items into a text file.

Then change the program so it reads the items from the file.

Do this slowly:

```text
make the text file
read the file
print the lines
then rebuild the old output
```

## Tiny Win

You can now make a program read information that is not written directly inside the code.

That is a quiet but important step.

Variables remember information while the program runs.

Files let information wait outside the program until the program needs it.

## Tomorrow

Tomorrow is:

```text
Day 70: Writing Files
```

Today, you opened a file and read saved text from it.

Tomorrow, you will go the other direction.

You will use Python to write text into a file.

That means your programs will be able to save notes, reports, results, and other text for later.
