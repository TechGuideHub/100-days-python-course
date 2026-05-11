# Day 77: Reading Documentation

**Focus:** Reading Python documentation without getting overwhelmed  
**You will practice:** finding purpose, parameters, return values, examples, version notes, small experiments, and useful details in docs for `pathlib`, `json`, `csv`, `random`, and `datetime`  
**Estimated time:** 45-60 minutes

## Today's Goal

Today you will learn how to read documentation as a working programmer.

Documentation can look dense at first.

That does not mean you are supposed to understand every sentence on the first pass.

Your goal is smaller and more practical:

```text
Find the piece of information you need right now.
Try it in a tiny program.
Use what you learned.
```

By the end of this lesson, you should be able to:

- open documentation with a clear question
- find what a function, class, or method is for
- identify parameters and optional arguments
- check what a call returns
- use examples without copying blindly
- notice version notes without getting stuck on them
- run small experiments to confirm your understanding
- use documentation as part of debugging
- prepare for Day 78, where external API docs become important

Yesterday, you practiced debugging by slowing down and checking assumptions.

Today, documentation gives you one more way to check those assumptions.

## The Big Idea

Documentation is not a novel.

You do not have to start at the top and read to the bottom.

Most of the time, you are looking for one answer:

```text
What does this tool do, and how do I use it correctly?
```

For example, suppose you see this code:

```python
from pathlib import Path

path = Path("notes.txt")
print(path.exists())
```

You might have questions:

- What does `Path()` create?
- What does `.exists()` return?
- Does `.exists()` create a file?
- Is the result text, a number, or `True`/`False`?

Documentation helps you answer those questions.

But the trick is to read with a target.

Instead of asking:

```text
How do I understand all of pathlib?
```

ask:

```text
What does Path.exists() return?
```

That smaller question is much easier to answer.

## The Mental Model

When you read documentation, look for six things.

```text
1. Purpose
2. Parameters
3. Return value
4. Examples
5. Notes and warnings
6. Version notes
```

Here is what each one means.

| Thing to find | Question it answers |
| --- | --- |
| Purpose | What is this for? |
| Parameters | What do I put inside the parentheses? |
| Return value | What do I get back? |
| Examples | What does normal use look like? |
| Notes and warnings | What mistakes or edge cases should I know about? |
| Version notes | Does this behave differently in some Python versions? |

Start with purpose and return value.

Those two usually tell you enough to run a small experiment.

Example:

```python
from pathlib import Path

path = Path("day-77/docs_notes.txt")

print(path.parent)
print(path.name)
print(path.suffix)
print(path.exists())
```

Run it before creating the file.

You should see something like:

```text
day-77
docs_notes.txt
.txt
False
```

The last line is the important part.

`path.exists()` returns a boolean value.

It checks whether the path exists.

It does not create the file.

That is the kind of detail documentation can help you confirm.

## Try It Yourself

Create a folder named:

```text
day-77
```

Today you will make a few tiny experiment files.

Start with this file:

```text
day-77/path_docs_experiment.py
```

Code:

```python
from pathlib import Path

folder = Path("day-77")
notes_path = folder / "docs_notes.txt"

folder.mkdir(exist_ok=True)
notes_path.write_text("Read with a question.\nTry a small experiment.\n")

print("file name:", notes_path.name)
print("file ending:", notes_path.suffix)
print("parent folder:", notes_path.parent)
print("exists:", notes_path.exists())
print("contents:")
print(notes_path.read_text())
```

Run it.

You should see:

```text
file name: docs_notes.txt
file ending: .txt
parent folder: day-77
exists: True
contents:
Read with a question.
Try a small experiment.
```

This is how documentation becomes less abstract.

You read one method.

Then you test it with one small file.

### Experiment With json.dumps()

The `json` module has two similar-looking tools:

```text
json.dump()
json.dumps()
```

The names are easy to mix up.

A documentation habit helps:

- check the purpose
- check the parameters
- check the return value

Create this file:

```text
day-77/json_docs_experiment.py
```

Code:

```python
import json

profile = {
    "name": "Mina",
    "level": 4,
    "skills": ["files", "json", "debugging"]
}

text = json.dumps(profile, indent=2)

print(type(text))
print(text)
```

Run it.

You should see:

```text
<class 'str'>
{
  "name": "Mina",
  "level": 4,
  "skills": [
    "files",
    "json",
    "debugging"
  ]
}
```

The important detail:

```text
json.dumps() returns a string.
```

That final `s` can remind you:

```text
dumps -> dump string
```

Now compare it with `json.dump()`.

Create this file:

```text
day-77/json_dump_experiment.py
```

Code:

```python
import json
from pathlib import Path

settings = {
    "theme": "light",
    "show_tips": True
}

path = Path("day-77/settings.json")

with path.open("w") as file:
    result = json.dump(settings, file, indent=2)

print("return value:", result)
print("file text:")
print(path.read_text())
```

Run it.

You should see:

```text
return value: None
file text:
{
  "theme": "light",
  "show_tips": true
}
```

That tells you something useful:

```text
json.dump() writes to a file and returns None.
json.dumps() creates a string and returns that string.
```

You did not need to memorize that.

You used documentation and a tiny experiment.

## Common Mistake

A common mistake is treating documentation like a test you must pass.

That makes every unfamiliar word feel urgent.

Instead, read in passes.

First pass:

```text
What is this for?
```

Second pass:

```text
What arguments can I give it?
```

Third pass:

```text
What does it return?
```

Fourth pass:

```text
Is there an example close to what I need?
```

You can ignore advanced details until you need them.

For example, the documentation for `csv.reader` may mention dialects, quoting rules, delimiters, and more.

If your current file is simple comma-separated data, start with the basic example.

Code:

```python
import csv
from pathlib import Path

path = Path("day-77/scores.csv")
path.write_text("name,score\nMina,9\nSam,8\n")

with path.open(newline="") as file:
    reader = csv.DictReader(file)

    for row in reader:
        print(row["name"], row["score"])
```

Run it.

You should see:

```text
Mina 9
Sam 8
```

You do not need every detail of the `csv` module today.

You need the part that helps you read this file correctly.

## Debug It

Here is a broken program.

It is meant to fail so you can practice using documentation as part of debugging.

Broken code:

```python
import random

names = ["Mina", "Sam", "Iris"]

chosen = random.choice(names, 2)

print(chosen)
```

When you run it, Python raises a `TypeError`.

The problem is this line:

```python
chosen = random.choice(names, 2)
```

Use the documentation-reading routine:

```text
1. Search for random.choice.
2. Find the purpose.
3. Check the parameters.
4. Check the return value.
5. Try a smaller experiment.
```

`random.choice()` chooses one item from a non-empty sequence.

It takes one main argument: the sequence.

It returns one item.

Fixed code:

```python
import random

names = ["Mina", "Sam", "Iris"]

chosen = random.choice(names)

print(chosen)
```

The output may be different each time, such as:

```text
Sam
```

If you want more than one item, documentation points you to a different tool.

Code:

```python
import random

names = ["Mina", "Sam", "Iris"]

chosen = random.sample(names, 2)

print(chosen)
```

You should see a list with two different names, such as:

```text
['Iris', 'Mina']
```

The exact names and order may change.

That is normal for `random`.

The debugging lesson is the important part:

```text
The error message told you where to look.
The documentation told you how the function expects to be called.
The tiny experiment confirmed it.
```

## Read the Docs

Now practice reading a documentation page without trying to absorb all of it.

Choose one of these:

```text
pathlib.Path.write_text
json.dumps
csv.DictReader
random.choice
datetime.date.today
```

Use this checklist while reading:

```text
Name:
Purpose:
Parameters:
Return value:
Small example:
One detail I almost missed:
```

Here is a filled-in example for `datetime.date.today`.

```text
Name: datetime.date.today
Purpose: Get the current local date.
Parameters: None.
Return value: A date object.
Small example: date.today()
One detail I almost missed: It gives a date, not a date and time.
```

Turn that into a small experiment.

Code:

```python
from datetime import date

today = date.today()

print(today)
print(type(today))
print(today.year)
print(today.month)
print(today.day)
```

You should see today's date, then:

```text
<class 'datetime.date'>
```

Then you should see the year, month, and day as numbers.

The exact date will depend on when you run the program.

### How To Read Version Notes

Python documentation sometimes includes notes like:

```text
Changed in version 3.x
Added in version 3.x
Deprecated since version 3.x
```

Do not panic when you see them.

Use this simple rule:

```text
Added means older Python versions may not have it.
Changed means behavior may differ from older examples.
Deprecated means avoid using it in new code.
```

For this beginner course, version notes usually mean:

```text
Check your Python version if an example from the docs does not work.
```

You can check your version with:

```python
import sys

print(sys.version)
```

Most of the tools in today's lesson have existed for a long time.

Still, noticing version notes is a good habit.

It matters more as your programs grow.

## Mini Challenge

Read a small part of the documentation for `Path.read_text()`.

Your job is to answer these questions:

```text
What does it do?
Does it need a file to already exist?
What does it return?
```

Then create this file:

```text
day-77/read_text_challenge.py
```

Code:

```python
from pathlib import Path

path = Path("day-77/message.txt")
path.write_text("Documentation gets easier when you test one idea.\n")

message = path.read_text()

print(type(message))
print(message.upper())
```

Run it.

You should see:

```text
<class 'str'>
DOCUMENTATION GETS EASIER WHEN YOU TEST ONE IDEA.
```

Now answer in your own words:

```text
Path.read_text() reads a text file and returns a string.
```

That one sentence is enough for today.

## Real-World Use

Real projects depend on documentation all the time.

You use docs when you need to know:

- how to open a file safely
- which argument name controls indentation
- whether a function returns a new value or changes something in place
- how errors are reported
- whether an example works in your Python version
- what kind of object you should pass into a function

This matters even more when you use tools outside the Python standard library.

For example, an external API might have documentation that tells you:

- which URL to call
- which parameters are required
- what the response data looks like
- what errors can happen
- whether you need an API key
- what limits apply

That is where the next lesson is heading.

Before you can use an external API comfortably, you need today's habit:

```text
Read for one answer.
Try one small experiment.
Then build the real program.
```

## Recap

Documentation is easier when you read it with a question.

Look for:

- purpose
- parameters
- return value
- examples
- notes and warnings
- version notes

When a detail feels unclear, do not stare at the page forever.

Write a tiny experiment.

Print the type.

Print the value.

Change one argument.

Run it again.

That turns documentation from a wall of text into a conversation with the code.

## Lesson Checklist

Before moving on, make sure you can:

- explain why you should read documentation with a specific question
- find the purpose of a function, method, or class
- identify required and optional parameters
- check what a function returns
- use a documentation example carefully
- notice version notes without getting overwhelmed
- write a tiny experiment to test one documentation detail
- explain the difference between `json.dump()` and `json.dumps()`
- use documentation to fix a wrong function call
- connect today's habit to debugging and external APIs

## Exercises

### Exercise 1: Read One Method

Choose one `Path` method you have seen before:

```text
exists
mkdir
write_text
read_text
```

Look it up in the documentation.

Write four notes:

```text
Purpose:
Parameters:
Return value:
Example I tried:
```

Then write a tiny program that tests only that method.

### Exercise 2: Compare Two json Tools

In your own words, explain the difference between:

```text
json.dump()
json.dumps()
```

Then run this code:

```python
import json

data = {"course": "Python", "day": 77}

text = json.dumps(data)

print(text)
print(type(text))
```

You should see:

```text
{"course": "Python", "day": 77}
<class 'str'>
```

### Exercise 3: Find An Optional Argument

Look up `random.randint`.

Answer:

```text
What parameters does it need?
Are both ends included?
What does it return?
```

Then test it:

```python
import random

number = random.randint(1, 3)

print(number)
```

You should see:

```text
1
```

or:

```text
2
```

or:

```text
3
```

If you ever see `0` or `4`, something is wrong.

### Exercise 4: Read A csv Example

Look up `csv.DictReader`.

Then run this:

```python
import csv
from pathlib import Path

path = Path("day-77/books.csv")
path.write_text("title,pages\nMatilda,240\nThe Hobbit,310\n")

with path.open(newline="") as file:
    reader = csv.DictReader(file)

    for row in reader:
        print(row["title"], "has", row["pages"], "pages")
```

You should see:

```text
Matilda has 240 pages
The Hobbit has 310 pages
```

### Exercise 5: Use Docs During Debugging

This code is broken:

Broken code:

```python
from datetime import date

today = date.today("local")

print(today)
```

Read the documentation for `date.today()`.

Then answer:

```text
Does date.today() take an argument?
What does it return?
```

Fixed code:

```python
from datetime import date

today = date.today()

print(today)
```

The output will be the date when you run the program.

## Tiny Win

Today you learned a skill that does not look flashy but changes how you work.

You do not need to memorize every Python tool.

You need to know how to ask a clear question, find the relevant part of the docs, and test your understanding in a small program.

That is what real programmers do every day.

## Tomorrow

Tomorrow you will use these documentation-reading habits with an external API.

The pages may look different from Python's standard documentation, but the reading strategy stays familiar:

```text
What is this for?
What do I send?
What do I get back?
What can go wrong?
```

That is enough to begin.
