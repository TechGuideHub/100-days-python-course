# Day 74: Exceptions

**Focus:** Understanding Python errors and reading tracebacks  
**You will practice:** recognizing exceptions, finding the line that failed, reading error messages, and identifying `ValueError`, `FileNotFoundError`, `ZeroDivisionError`, and `KeyError`  
**Estimated time:** 45-60 minutes

## Today's Goal

Today you will learn what Python is telling you when a program crashes.

That crash is often called an exception.

An exception is Python saying:

```text
I reached a problem I cannot continue past.
```

You have probably seen red error text before.

Today, that text becomes less mysterious.

After today, you should be able to:

- explain what an exception is
- understand why Python stops a program when an exception happens
- read the most useful parts of a traceback
- find the file line that caused the problem
- identify the exception type
- read the message after the exception type
- recognize common beginner exceptions
- slow down and debug from the actual error instead of guessing
- prepare for Day 75, where you will learn how to handle exceptions

The main skill today is not preventing every error.

The main skill is reading the error clearly.

## The Big Idea

Python runs your program from top to bottom.

If Python reaches a line it cannot complete, it raises an exception.

When an exception is not handled, the program stops.

Example:

```python
print("Before the calculation")

total = 10 / 2

print("Total:", total)
print("After the calculation")
```

You should see:

```text
Before the calculation
Total: 5.0
After the calculation
```

That program works because dividing by `2` is allowed.

Now look at this broken code:

```python
print("Before the calculation")

total = 10 / 0

print("Total:", total)
print("After the calculation")
```

This code is supposed to fail.

You should see the first line:

```text
Before the calculation
```

Then Python stops and shows an error.

The last two `print()` calls do not run.

That happens because `10 / 0` raises a `ZeroDivisionError`.

Python cannot invent a useful answer for division by zero, so it stops the program and tells you what happened.

That message is useful.

It is not just noise.

It is a report.

## The Mental Model

Think of an exception like a stop sign inside your program.

Python reaches a line and tries to do the work.

If the work cannot be done, Python raises an exception.

If nothing handles that exception, Python stops the program and prints a traceback.

A traceback is the path Python followed before the crash.

For beginner programs, you usually need three pieces:

```text
1. The line number
2. The line of code that failed
3. The exception type and message
```

Here is a small broken program:

```python
name = "Mina"
age_text = "twelve"

age = int(age_text)

print(name, "will be", age + 1, "next year")
```

This code is broken because `"twelve"` is not written as digits.

Python may show a traceback like this:

```text
Traceback (most recent call last):
  File "age_check.py", line 4, in <module>
    age = int(age_text)
ValueError: invalid literal for int() with base 10: 'twelve'
```

Read it from the bottom up.

The bottom line says:

```text
ValueError: invalid literal for int() with base 10: 'twelve'
```

That tells you two things:

```text
Exception type: ValueError
Message: invalid literal for int() with base 10: 'twelve'
```

The line above that shows the code that failed:

```python
age = int(age_text)
```

The line above that shows where it failed:

```text
File "age_check.py", line 4, in <module>
```

That means:

```text
Look in age_check.py.
Go to line 4.
Start your debugging there.
```

You do not need to understand every word in a traceback yet.

Start with the bottom line and the line number.

That is already a lot of power.

## Try It Yourself

Create a folder named:

```text
day-74
```

Then create this file:

```text
day-74/traceback_practice.py
```

Work slowly.

The point is to read the error, not rush past it.

### Step 1: Start With Code That Works

Code:

```python
scores = [8, 7, 10]

total = sum(scores)
average = total / len(scores)

print("Total:", total)
print("Average:", average)
print("Done")
```

Run it.

You should see:

```text
Total: 25
Average: 8.333333333333334
Done
```

This works because `scores` has three numbers.

`len(scores)` is `3`, so the division is allowed.

### Step 2: Create A ZeroDivisionError

Now change the first line to an empty list.

Broken code:

```python
scores = []

total = sum(scores)
average = total / len(scores)

print("Total:", total)
print("Average:", average)
print("Done")
```

This code is supposed to fail.

You should see an error ending with something like:

```text
ZeroDivisionError: division by zero
```

Now answer these questions:

```text
What line caused the crash?
What exception type did Python name?
What was Python trying to divide by?
Which print calls ran before the crash?
```

The key detail is that `len(scores)` is `0`.

The line:

```python
average = total / len(scores)
```

turns into:

```text
average = 0 / 0
```

That is why Python raises `ZeroDivisionError`.

### Step 3: Create A ValueError

Replace the file contents with this:

Broken code:

```python
age_text = "twenty"

age = int(age_text)

print("Next year:", age + 1)
```

This code is supposed to fail.

You should see an error ending with something like:

```text
ValueError: invalid literal for int() with base 10: 'twenty'
```

Python can convert `"20"` into the integer `20`.

Python cannot convert `"twenty"` into an integer with `int()`.

Read the traceback and find the exact line.

### Step 4: Create A KeyError

Replace the file contents with this:

Broken code:

```python
student = {
    "name": "Mina",
    "score": 9,
}

print(student["grade"])
```

This code is supposed to fail.

You should see an error ending with something like:

```text
KeyError: 'grade'
```

The dictionary has keys named `"name"` and `"score"`.

It does not have a key named `"grade"`.

Python stops because this line asks for a key that is not there:

```python
print(student["grade"])
```

### Step 5: Create A FileNotFoundError

Replace the file contents with this:

Broken code:

```python
with open("missing_notes.txt", "r") as file:
    contents = file.read()

print(contents)
```

This code is supposed to fail unless that file already exists.

You should see an error ending with something like:

```text
FileNotFoundError: [Errno 2] No such file or directory: 'missing_notes.txt'
```

The message is direct:

```text
Python tried to open a file, but it could not find it.
```

Today, do not worry about handling this error.

Just practice reading what Python reports.

## Common Mistake

A common mistake is reading only the first line of the traceback.

This line appears often:

```text
Traceback (most recent call last):
```

That line tells you a traceback is starting.

It does not tell you what caused the crash.

The most useful line is usually the bottom line.

Example:

```text
ValueError: invalid literal for int() with base 10: 'abc'
```

That line tells you:

```text
Python expected a value it could convert to an integer.
It received 'abc' instead.
```

Another common mistake is changing random parts of the program before reading the line number.

Slow down.

Use this order:

```text
1. Read the bottom line.
2. Name the exception type.
3. Read the message.
4. Find the line number.
5. Look at the code on that line.
6. Ask what value made that line fail.
```

Here is a broken example:

```python
items = {"apples": 3, "rice": 1}

print(items["tea"])
```

The useful clue is not just that the program crashed.

The useful clue is:

```text
KeyError: 'tea'
```

That means Python looked for the key `"tea"` and did not find it.

## Debug It

For each broken snippet, read the code and identify:

```text
Exception type
Line that fails
Reason it fails
```

Do not fix these with exception handling yet.

Tomorrow you will learn how to respond to exceptions in code.

Today, practice reading them.

### Debug 1

Broken code:

```python
number_text = "7.5"
number = int(number_text)

print(number * 2)
```

Answer:

```text
Exception type: ValueError
Line that fails: number = int(number_text)
Reason: int() cannot convert the string "7.5" directly into an integer.
```

One simple correction would be:

```python
number_text = "7"
number = int(number_text)

print(number * 2)
```

### Debug 2

Broken code:

```python
cart = {
    "notebook": 2,
    "pen": 5,
}

print(cart["pencil"])
```

Answer:

```text
Exception type: KeyError
Line that fails: print(cart["pencil"])
Reason: "pencil" is not a key in the dictionary.
```

One simple correction would be:

```python
cart = {
    "notebook": 2,
    "pen": 5,
}

print(cart["pen"])
```

### Debug 3

Broken code:

```python
completed_tasks = 0
total_tasks = 0

percent = completed_tasks / total_tasks * 100

print(percent)
```

Answer:

```text
Exception type: ZeroDivisionError
Line that fails: percent = completed_tasks / total_tasks * 100
Reason: total_tasks is 0, so the code tries to divide by zero.
```

One simple correction would be:

```python
completed_tasks = 0
total_tasks = 5

percent = completed_tasks / total_tasks * 100

print(percent)
```

### Debug 4

Broken code:

```python
with open("daily_plan.txt", "r") as file:
    plan = file.read()

print(plan)
```

Answer:

```text
Exception type: FileNotFoundError
Line that fails: with open("daily_plan.txt", "r") as file:
Reason: Python cannot find a file named daily_plan.txt in the place it is looking.
```

One simple correction would be to create the file before reading it.

Another correction would be to check the file name carefully.

## Read the Docs

Python's official tutorial has a section about errors and exceptions:

[Python docs: Errors and Exceptions](https://docs.python.org/3/tutorial/errors.html)

Python's official reference also lists built-in exception types:

[Python docs: Built-in Exceptions](https://docs.python.org/3/library/exceptions.html)

Today, focus on these names:

- `ValueError`
- `FileNotFoundError`
- `ZeroDivisionError`
- `KeyError`

You do not need to memorize the entire page.

Try this:

```text
Open the built-in exceptions page.
Find ValueError.
Read the first sentence or two.
Then find KeyError.
Write one short example in your own words.
```

The goal is to connect the official name to a situation you recognize.

## Mini Challenge

Build an error reading notebook in comments.

Create:

```text
day-74/error_notes.py
```

Paste this broken code:

```python
profile = {
    "name": "Iris",
    "city": "Pune",
}

print(profile["email"])
```

Run it once.

Then add three comments above the broken line:

```python
profile = {
    "name": "Iris",
    "city": "Pune",
}

# Exception type:
# Line that fails:
# Reason:
print(profile["email"])
```

Fill in the comments from the traceback.

Do not make the code work yet.

This challenge is about reading the crash report accurately.

When you are done, you should be able to say:

```text
The program crashed because it asked for a dictionary key that does not exist.
```

## Real-World Use

Exceptions show up in ordinary programs all the time.

Here are a few real situations:

- A user types `"ten"` when the program expects a number: `ValueError`
- A program tries to read a file that has not been created: `FileNotFoundError`
- A calculator divides by a value that turned out to be `0`: `ZeroDivisionError`
- A dictionary lookup uses the wrong key name: `KeyError`

This working program avoids those problems by using values that make sense:

```python
user = {
    "name": "Mina",
    "minutes": "30",
}

minutes = int(user["minutes"])
sessions = 3
average = minutes / sessions

print(user["name"])
print("Total minutes:", minutes)
print("Average per session:", average)
```

You should see:

```text
Mina
Total minutes: 30
Average per session: 10.0
```

Now imagine these changes:

```text
If "minutes" was "thirty", int(user["minutes"]) would raise ValueError.
If the dictionary did not have "minutes", user["minutes"] would raise KeyError.
If sessions was 0, minutes / sessions would raise ZeroDivisionError.
```

That is how exceptions help you find the real weak spot in your data or logic.

They point to the line where your assumption stopped being true.

## Recap

Today you learned that an exception is an error Python raises when it cannot continue normally.

When an exception is not handled, Python stops the program and prints a traceback.

You practiced reading:

- the exception type
- the error message
- the line number
- the line of code that failed

You saw four common exceptions:

```text
ValueError: a value has the right general type, but the wrong contents
FileNotFoundError: Python cannot find the file it was asked to open
ZeroDivisionError: code tried to divide by zero
KeyError: code asked a dictionary for a missing key
```

Your debugging habit for today:

```text
Start with the bottom line of the traceback.
Then go to the line number Python gives you.
```

That habit will save you a lot of guessing.

## Lesson Checklist

- [ ] I can explain what an exception is.
- [ ] I can explain why a program stops when an unhandled exception happens.
- [ ] I can find the exception type in a traceback.
- [ ] I can find the error message in a traceback.
- [ ] I can find the line number that caused the crash.
- [ ] I can recognize a `ValueError`.
- [ ] I can recognize a `FileNotFoundError`.
- [ ] I can recognize a `ZeroDivisionError`.
- [ ] I can recognize a `KeyError`.
- [ ] I can debug from the traceback instead of guessing randomly.

## Exercises

### Exercise 1: Read A ValueError

Create:

```text
day-74/read_value_error.py
```

Use this broken code:

```python
quantity_text = "five"
quantity = int(quantity_text)

print(quantity)
```

Run it.

Write down:

```text
Exception type:
Line that fails:
Message:
Reason:
```

### Exercise 2: Read A ZeroDivisionError

Create:

```text
day-74/read_zero_division.py
```

Use this broken code:

```python
points = 12
games = 0

average = points / games

print(average)
```

Run it and read the traceback.

Then explain the error in one sentence.

### Exercise 3: Read A KeyError

Create:

```text
day-74/read_key_error.py
```

Use this broken code:

```python
book = {
    "title": "Python Basics",
    "pages": 120,
}

print(book["author"])
```

Run it.

Find the missing key name in the traceback.

### Exercise 4: Read A FileNotFoundError

Create:

```text
day-74/read_file_error.py
```

Use this broken code:

```python
with open("notes_for_today.txt", "r") as file:
    notes = file.read()

print(notes)
```

Run it only if you do not already have a file with that name.

Find the file name inside the error message.

### Exercise 5: Match The Exception

Match each situation to the exception name.

```text
A. int("abc")
B. scores["math"] when "math" is not a key
C. open("missing.txt", "r")
D. 40 / 0
```

Names:

```text
ValueError
KeyError
FileNotFoundError
ZeroDivisionError
```

### Exercise 6: What Runs Before The Crash?

Read this broken code:

```python
print("Start")

number = int("nope")

print("Middle")
print("End")
```

Before running it, answer:

```text
Which print calls run?
Which print calls do not run?
Why does the program stop?
```

Then run it and check your answer.

### Exercise 7: Fix One Value

This code is broken:

```python
price_text = "12"
quantity_text = "two"

price = int(price_text)
quantity = int(quantity_text)

print(price * quantity)
```

First, identify the exception type and failing line.

Then change only one value so the program works.

### Exercise 8: Find The Bad Assumption

This code is broken:

```python
student = {
    "name": "Sam",
    "score": 8,
}

print(student["Score"])
```

Answer:

```text
What key exists?
What key did the code ask for?
Why does capitalization matter here?
```

### Exercise 9: Read Before Fixing

Choose one broken program from today's lesson.

Run it again.

Before changing any code, write:

```text
The exception type is ...
The message says ...
The failing line is ...
The value that caused the problem is ...
```

Then make the smallest correction you can.

### Exercise 10: Build A Tiny Error Log

In a notebook or comments in a file, make a list like this:

```text
Exception: ValueError
Example line: int("hello")
Meaning: Python could not convert the text into an integer.
```

Add one entry each for:

```text
ValueError
FileNotFoundError
ZeroDivisionError
KeyError
```

Use your own words.

## Tiny Win

You can now look at a Python crash and find the first useful clue.

That is a real debugging skill.

Instead of thinking "it broke somewhere," you can ask better questions:

```text
What exception happened?
What line failed?
What value made that line fail?
```

Those questions turn a scary wall of text into a trail you can follow.

## Tomorrow

Tomorrow is:

```text
Day 75: Handling Exceptions
```

Today you learned how to read exceptions.

Tomorrow you will learn how to respond when they happen, using `try` and `except`.
