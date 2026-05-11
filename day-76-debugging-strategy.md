# Day 76: Debugging Strategy

**Focus:** Building a repeatable routine for finding and fixing bugs  
**You will practice:** reproducing bugs, reading messages, reducing problems, printing checkpoints, checking assumptions, isolating input and output, fixing one thing at a time, and retesting  
**Estimated time:** 50-65 minutes

## Today's Goal

Today you will practice debugging as a routine.

Debugging is not guessing harder.

It is slowing down enough to find where your program stopped doing what you thought it was doing.

By the end of today, you should be able to:

- reproduce a bug on purpose
- read the error message before changing code
- reduce a problem to a smaller example
- add print checkpoints in useful places
- check assumptions about values and types
- isolate input, processing, and output
- fix one thing at a time
- retest after each fix
- use exceptions as clues instead of treating them as personal failures
- prepare for Day 77, where you will read documentation more deliberately

The routine for today is:

```text
1. Reproduce the bug.
2. Read the message.
3. Reduce the problem.
4. Add print checkpoints.
5. Check your assumptions.
6. Isolate input and output.
7. Fix one thing.
8. Retest.
```

That routine is simple on purpose.

When a program is confusing, simple steps are exactly what you need.

## The Big Idea

A bug means there is a gap between:

```text
what you expected
```

and:

```text
what actually happened
```

Your job is to make that gap smaller until the cause is visible.

Start with a small program.

Code:

```python
orders = ["tea:2", "rice:1", "apples:4"]


def total_items(order_lines):
    total = 0

    for line in order_lines:
        item, quantity_text = line.split(":")
        quantity = int(quantity_text)
        total += quantity

    return total


print(total_items(orders))
```

You should see:

```text
7
```

This program has three main parts:

```text
input:      ["tea:2", "rice:1", "apples:4"]
process:    split each line, convert the quantity, add it to total
output:     7
```

If the answer is wrong, do not start by rewriting the whole function.

First, find the step where the value becomes wrong.

Add checkpoints:

```python
orders = ["tea:2", "rice:1", "apples:4"]


def total_items(order_lines):
    total = 0

    for line in order_lines:
        print("checking line:", line)

        item, quantity_text = line.split(":")
        print("item:", item)
        print("quantity text:", quantity_text)

        quantity = int(quantity_text)
        print("quantity number:", quantity)

        total += quantity
        print("total so far:", total)

    return total


print("final total:", total_items(orders))
```

You should see the values move through the program one step at a time.

Those prints are not meant to stay forever.

They are temporary lights you turn on while you are looking for the problem.

Once the bug is fixed, remove the noisy checkpoints or keep only the ones that are still useful.

## The Mental Model

Think of debugging like following a package through a few stops.

```text
input -> function -> calculation -> output
```

At each stop, ask:

```text
What value do I have right now?
What type is it?
Is that what I expected?
```

Here is a small function with clear input and output.

Code:

```python
def make_label(name, score):
    return f"{name}: {score}/10"


print(make_label("Mina", 8))
```

You should see:

```text
Mina: 8/10
```

If this printed the wrong thing, you would not need to inspect your whole project.

You could test only this function.

That is isolation.

File programs have the same shape, but there are more places to check.

Code:

```python
from pathlib import Path

path = Path("scores.txt")
path.write_text("Mina,8\nSam,10\nIris,9\n")

for line in path.read_text().splitlines():
    name, score_text = line.split(",")
    score = int(score_text)
    print(f"{name} scored {score}")
```

You should see:

```text
Mina scored 8
Sam scored 10
Iris scored 9
```

If this file program breaks, check the stops:

- Did the file exist?
- Did you read the text you thought you read?
- Did each line have a comma?
- Did `split(",")` produce the number of pieces you expected?
- Was the score text really a number?
- Did the final print use the value you calculated?

Many bugs become less mysterious when you ask one small question at a time.

## Try It Yourself

Create a folder named:

```text
day-76
```

Then create this file:

```text
day-76/debug_routine.py
```

Work through the steps slowly.

### Step 1: Start With A Known Case

Code:

```python
def average(numbers):
    total = 0

    for number in numbers:
        total += number

    return total / len(numbers)


print(average([10, 20, 30]))
```

Run it.

You should see:

```text
20.0
```

This is a good debugging habit even when nothing is broken yet.

Use a small input where you already know the answer.

That gives you something solid to compare against.

### Step 2: Add Checkpoints

Change the program to this:

```python
def average(numbers):
    print("numbers:", numbers)

    total = 0

    for number in numbers:
        print("adding:", number)
        total += number
        print("total so far:", total)

    print("count:", len(numbers))
    return total / len(numbers)


print("average:", average([10, 20, 30]))
```

Run it again.

You should see the list, each number, the running total, the count, and the final average.

These checkpoints answer useful questions:

- Did the function receive the list I expected?
- Did the loop run once for each number?
- Did the total change correctly?
- Did the final division use the right count?

### Step 3: Check A File Program

Now try a file example.

Code:

```python
from pathlib import Path

path = Path("practice_scores.txt")
path.write_text("Mina,8\nSam,10\nIris,9\n")

text = path.read_text()
print("raw text:")
print(text)

for line in text.splitlines():
    print("line:", line)
    name, score_text = line.split(",")
    print("name:", name)
    print("score text:", score_text)
```

This is not the final version of a program.

It is a debugging version.

It proves what the program is reading and how each line is being split.

### Step 4: Remove Noise After You Understand

Once you trust the steps, make the program quieter.

Code:

```python
from pathlib import Path

path = Path("practice_scores.txt")
path.write_text("Mina,8\nSam,10\nIris,9\n")

total = 0
count = 0

for line in path.read_text().splitlines():
    name, score_text = line.split(",")
    total += int(score_text)
    count += 1

print(total / count)
```

You should see:

```text
9.0
```

The checkpoints helped you understand the program.

The final version only keeps the code needed for the result.

## Common Mistake

A common beginner mistake is changing five things at once.

That feels productive, but it makes debugging harder.

If the program starts working, you do not know which change fixed it.

If the program gets worse, you do not know which change caused the new problem.

Use one change, then one retest.

Buggy code:

```python
def price_after_discount(price, percent):
    discount = price - percent
    return discount


print(price_after_discount(200, 10))
```

This runs, but it treats `10` like plain money instead of `10` percent.

It prints:

```text
190
```

For a 10 percent discount on 200, the answer should be 180.

Fix one idea:

```python
def price_after_discount(price, percent):
    discount_amount = price * (percent / 100)
    return price - discount_amount


print(price_after_discount(200, 10))
```

You should see:

```text
180.0
```

Do not also rename variables, change the print, add file reading, and handle exceptions at the same time.

Fix the math first.

Then retest.

Then clean up names if needed.

## Debug It

Here is a broken program.

It is meant to fail so you can practice reading the message.

Broken code:

```python
from pathlib import Path


def read_total(path):
    text = path.read_text()
    total = 0

    for line in text.splitlines():
        parts = line.split(",")
        total += int(parts[2])

    return total


path = Path("orders.txt")
path.write_text("tea,2\nrice,1\napples,4\n")

print(read_total(path))
```

When you run it, Python raises:

```text
IndexError: list index out of range
```

Use the routine.

### 1. Reproduce The Bug

Run the program again without changing anything.

Make sure you can see the same error.

If a bug only happens sometimes, write down the exact input or file contents that caused it.

### 2. Read The Message

The message says:

```text
IndexError
```

That means the code asked for a list position that does not exist.

This line is suspicious:

```python
total += int(parts[2])
```

### 3. Reduce The Problem

You do not need the whole file program to test the split.

Try the smallest version:

```python
line = "tea,2"
parts = line.split(",")

print(parts)
print(len(parts))
```

You should see:

```text
['tea', '2']
2
```

The list has two items.

The indexes are:

```text
parts[0] -> "tea"
parts[1] -> "2"
```

There is no `parts[2]`.

### 4. Fix One Thing

Change only the index.

Fixed code:

```python
from pathlib import Path


def read_total(path):
    text = path.read_text()
    total = 0

    for line in text.splitlines():
        parts = line.split(",")
        total += int(parts[1])

    return total


path = Path("orders.txt")
path.write_text("tea,2\nrice,1\napples,4\n")

print(read_total(path))
```

You should see:

```text
7
```

### 5. Retest With Another Input

Now change the file contents and run again.

Code:

```python
from pathlib import Path


def read_total(path):
    text = path.read_text()
    total = 0

    for line in text.splitlines():
        parts = line.split(",")
        total += int(parts[1])

    return total


path = Path("orders.txt")
path.write_text("notebooks,3\npencils,5\n")

print(read_total(path))
```

You should see:

```text
8
```

Retesting with a second input helps you avoid a fake fix that only works for one case.

### 6. Add A Friendly Exception Later

After the main bug is fixed, you can make the program handle missing files more politely.

Code:

```python
from pathlib import Path


def read_total(path):
    try:
        text = path.read_text()
    except FileNotFoundError:
        print(f"Could not find {path}")
        return 0

    total = 0

    for line in text.splitlines():
        parts = line.split(",")
        total += int(parts[1])

    return total


path = Path("orders.txt")
path.write_text("tea,2\nrice,1\napples,4\n")

print(read_total(path))
```

You should see:

```text
7
```

Notice the order.

First you fixed the wrong index.

Then you added friendlier error handling.

That keeps each change easier to understand.

## Read the Docs

Documentation is easier to read when you bring it a specific question.

Do not open a documentation page and hope your eyes find the answer.

Ask a small question first.

Today, use docs or built-in help to answer questions like:

- What does `Path.read_text()` return?
- What does `str.split(",")` return?
- What happens when `int()` receives text that is not a number?
- Which exception is raised for a missing file?

You can also ask Python for quick help.

Code:

```python
value = "42"
number = int(value)

print(number)
print(type(number))
```

You should see:

```text
42
<class 'int'>
```

Tomorrow you will practice reading documentation more directly.

For today, the main habit is this:

```text
Use docs to answer one clear question at a time.
```

## Mini Challenge

Create this file:

```text
day-76/checker.py
```

Write a program that reads score lines, skips bad lines, and averages the usable scores.

Use this starter version:

```python
from pathlib import Path

path = Path("mini_scores.txt")
path.write_text("Mina,8\nSam,ten\nIris,9\nbad line\n")

total = 0
count = 0

for line in path.read_text().splitlines():
    print("checking:", line)
    parts = line.split(",")

    if len(parts) != 2:
        print("skipping line with wrong shape")
        continue

    name, score_text = parts

    try:
        score = int(score_text)
    except ValueError:
        print("skipping score that is not a number")
        continue

    total += score
    count += 1

if count > 0:
    print("average:", total / count)
else:
    print("no usable scores")
```

You should see messages for each line.

The program should skip:

- `Sam,ten`, because `ten` is not an integer
- `bad line`, because it does not contain a comma

The average should use only Mina and Iris.

When you are done, remove one checkpoint print at a time and run again.

The program should still work.

## Real-World Use

Debugging strategy matters because real programs usually fail in ordinary ways:

- a file is missing
- a line has a different shape than expected
- a number is still text
- a function receives an empty list
- a dictionary key is missing
- a user types something unexpected
- an API sends data in a shape you did not predict

The same routine works for all of those.

Here is a small example with a function you can test by itself:

```python
def normalize_name(name):
    return name.strip().title()


names = [" mina ", "SAM", "iris"]

for name in names:
    print(normalize_name(name))
```

You should see:

```text
Mina
Sam
Iris
```

If a larger contact program prints messy names, isolate the function first.

Test `normalize_name()` with a few inputs.

Then reconnect it to the bigger program.

That is much easier than trying to debug everything at once.

## Recap

Debugging is a skill you can practice.

Today you learned a routine:

- reproduce the bug
- read the message
- reduce the problem
- add print checkpoints
- check values and types
- isolate input, processing, and output
- fix one thing at a time
- retest after each fix

You also saw that exceptions are information.

An error message is not just a complaint.

It is often the shortest path to the exact line that needs your attention.

## Lesson Checklist

Before you move on, make sure you can:

- [ ] reproduce a bug before changing code
- [ ] read an error message and identify the exception type
- [ ] reduce a problem to a smaller example
- [ ] add print checkpoints to inspect values
- [ ] check both value and type when needed
- [ ] separate input, processing, and output while debugging
- [ ] fix one thing at a time
- [ ] retest with at least one more input
- [ ] remove temporary debug prints after the bug is understood

## Exercises

### Exercise 1: Write The Bug Report

Pick any small program you wrote recently.

Write down:

```text
What I expected:
What happened:
Input I used:
Error message, if any:
```

This takes less than a minute, but it makes debugging calmer.

### Exercise 2: Read The Error

This code is intentionally broken.

Broken code:

```python
name = "Mina"
print(score)
```

Before fixing it, answer:

```text
What exception type appears?
Which name is Python complaining about?
What is the smallest possible fix?
```

Then fix it by defining `score` before the print.

### Exercise 3: Reduce A File Problem

Run this small version before using a real file.

Code:

```python
lines = ["tea,2", "rice,1", "apples,4"]

for line in lines:
    item, quantity_text = line.split(",")
    print(item, quantity_text)
```

Then explain why this is easier to debug than reading from a file immediately.

### Exercise 4: Add Checkpoints

Start with this working function.

Code:

```python
def total_prices(prices):
    total = 0

    for price in prices:
        total += price

    return total


print(total_prices([12, 8, 5]))
```

Add prints for:

- the original list
- each price
- the total after each addition

Run it again.

### Exercise 5: Check A Type Assumption

Run this:

```python
raw_score = " 9 "
print(int(raw_score))
```

Then try:

```text
"9"
" 9 "
"nine"
"9.5"
```

Write down which ones convert cleanly with `int()` and which ones do not.

### Exercise 6: Isolate A Parser

Write and test this function by itself.

Code:

```python
def parse_score_line(line):
    name, score_text = line.split(",")
    return name, int(score_text)


print(parse_score_line("Mina,8"))
```

Then try at least two more lines.

One should work.

One should fail.

Read the message before you fix anything.

### Exercise 7: Handle One Exception

Code:

```python
def to_number(text):
    try:
        return int(text)
    except ValueError:
        return None


print(to_number("8"))
print(to_number("eight"))
```

Add two more test values.

Use `print(type(result))` if you are unsure what the function returns.

### Exercise 8: Fix One Thing At A Time

This code is intentionally broken in more than one way.

Broken code:

```python
def average(numbers):
    total = 0

    for number in numbers:
        total = number

    return total / count


print(average([10, 20, 30]))
```

Do not rewrite it all at once.

Use this order:

```text
1. Run it and read the first message.
2. Fix only the first message.
3. Run it again.
4. Check whether the answer is correct.
5. Fix only the next problem.
```

The correct answer should be:

```text
20.0
```

### Exercise 9: Debug A File Reader

Run this working version first.

Code:

```python
from pathlib import Path

path = Path("exercise_scores.txt")
path.write_text("Mina,8\nSam,10\n")

for line in path.read_text().splitlines():
    name, score_text = line.split(",")
    print(name, int(score_text))
```

Then change one line in the file text to:

```text
Iris,nine
```

Run it again and read the message.

Add a `try` and `except ValueError` block so the program skips that one bad score.

### Exercise 10: Keep A Debug Journal

For one bug today, write three sentences:

```text
The symptom was:
The cause was:
The fix was:
```

This helps you remember patterns.

Many bugs come back in new clothes later.

## Tiny Win

You now have a debugging routine you can reuse.

That matters.

When code breaks, you do not have to panic or randomly poke at it.

You can reproduce, inspect, reduce, fix, and retest.

That is how you turn confusion into information.

## Tomorrow

Tomorrow is:

```text
Day 77: Reading Documentation
```

Today you used documentation as a way to answer focused questions.

Tomorrow you will slow down and practice reading docs directly: function signatures, examples, return values, exceptions, and the small details that help you keep learning without waiting for someone else to explain every line.
