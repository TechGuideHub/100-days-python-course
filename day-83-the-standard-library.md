# Day 83: The Standard Library

**Focus:** Using Python's built-in modules to solve common problems  
**You will practice:** importing standard library modules, choosing a useful module, reading basic documentation, using `random`, `datetime`, `math`, `pathlib`, `statistics`, and `collections`, and telling the difference between built-in modules and installed packages  
**Estimated time:** 50-65 minutes

## Today's Goal

Today you will learn how to use more of the Python standard library.

The standard library is the collection of modules that comes with Python. You do not need to install these modules with a package manager. If Python is already installed, the standard library is already there too.

By the end of today, you should be able to:

- explain what people mean when they say Python has "batteries included"
- import standard library modules on purpose
- use a few common modules without trying to memorize them
- choose a module based on the problem you are solving
- read a documentation page without getting lost in every detail
- recognize when a tool is built into Python and when it might need installation
- prepare for Day 84, where you will install packages from outside the standard library

You have already used parts of the standard library.

Today is about seeing it as a toolkit.

## The Big Idea

Python includes many useful tools before you install anything extra.

That is the "batteries included" idea.

Instead of writing everything yourself, you can reach for a module that already handles a common job.

For example:

- `random` helps with random choices and shuffled data
- `datetime` helps with dates and times
- `math` helps with numeric calculations
- `pathlib` helps with file and folder paths
- `statistics` helps with averages and medians
- `collections` gives you useful container types like `Counter`

Here is a small sampler:

```python
import math
import random
import statistics
from collections import Counter
from datetime import date, timedelta
from pathlib import Path

random.seed(12)

practice_options = ["write notes", "review flashcards", "solve two exercises", "read docs"]
scores = [72, 85, 91, 91, 100]
votes = ["tea", "coffee", "tea", "water", "coffee", "tea"]

start = date(2026, 5, 10)
review_day = start + timedelta(days=7)
notes_path = Path("day-83") / "notes.txt"

print("Practice:", random.choice(practice_options))
print("Average score:", statistics.mean(scores))
print("Median score:", statistics.median(scores))
print("Square root:", math.sqrt(144))
print("Rounded up:", math.ceil(7.2))
print("Review day:", review_day.isoformat())
print("Notes file:", notes_path.as_posix())
print("Top vote:", Counter(votes).most_common(1)[0])
```

You should see:

```text
Practice: read docs
Average score: 87.8
Median score: 91
Square root: 12.0
Rounded up: 8
Review day: 2026-05-17
Notes file: day-83/notes.txt
Top vote: ('tea', 3)
```

That one program uses six standard library modules.

You do not need to master all six today. The point is simpler:

```text
Before you build a tool from scratch, ask whether Python already includes one.
```

## The Mental Model

Think of the standard library as the workshop that comes with Python.

Your own code is the project on the bench.

Imports are how you take a tool off the wall.

```text
your program
    |
    | import random
    v
your program can use random.choice(), random.randint(), and more
```

Different modules are good at different jobs.

| Problem | Standard library module to check |
| --- | --- |
| Pick one item from a list | `random` |
| Work with calendar dates | `datetime` |
| Calculate square roots or round up | `math` |
| Build file paths cleanly | `pathlib` |
| Find an average or median | `statistics` |
| Count repeated items | `collections` |

You do not need to remember every module name.

You only need to build the habit:

```text
1. Name the problem.
2. Search for a likely standard library module.
3. Import the module.
4. Try one small example.
5. Read only the part of the docs you need right now.
```

The standard library is large. That is a strength, not a homework assignment.

## Try It Yourself

Create this file:

```text
day-83/standard_library_sampler.py
```

Add this code:

```python
import math
import random
import statistics
from collections import Counter
from datetime import date, timedelta
from pathlib import Path

random.seed(12)

practice_options = ["write notes", "review flashcards", "solve two exercises", "read docs"]
scores = [72, 85, 91, 91, 100]
votes = ["tea", "coffee", "tea", "water", "coffee", "tea"]

start = date(2026, 5, 10)
review_day = start + timedelta(days=7)
notes_path = Path("day-83") / "notes.txt"

print("Practice:", random.choice(practice_options))
print("Average score:", statistics.mean(scores))
print("Median score:", statistics.median(scores))
print("Square root:", math.sqrt(144))
print("Rounded up:", math.ceil(7.2))
print("Review day:", review_day.isoformat())
print("Notes file:", notes_path.as_posix())
print("Top vote:", Counter(votes).most_common(1)[0])
```

Run it:

```text
python day-83/standard_library_sampler.py
```

You should see:

```text
Practice: read docs
Average score: 87.8
Median score: 91
Square root: 12.0
Rounded up: 8
Review day: 2026-05-17
Notes file: day-83/notes.txt
Top vote: ('tea', 3)
```

Now change one thing at a time:

- add another item to `practice_options`
- change the date
- add another score
- add more votes
- change `math.ceil(7.2)` to `math.floor(7.2)`

Small changes are the best way to learn a new module.

## Common Mistake

A common mistake is trying to install a module that already comes with Python.

For example, these are standard library modules:

```text
random
datetime
math
pathlib
statistics
collections
```

You import them directly:

```python
import random
import math
from pathlib import Path
```

You do not install them first.

Another common mistake is naming your own file after a standard library module.

Avoid file names like:

```text
random.py
datetime.py
math.py
statistics.py
collections.py
```

If your file is named `random.py`, then this line may import your file instead of Python's real `random` module:

```python
import random
```

Use clearer practice names:

```text
random_picker.py
date_practice.py
stats_summary.py
```

Names matter because imports search for names.

## Debug It

Here is a small program with a mistake:

```python
from pathlib import Path

notes_path = "day-83/notes.txt"

print(notes_path.name)
```

The problem is that `notes_path` is a string.

Strings do not have the same path tools as `Path` objects.

Fix it by creating a real `Path` object:

```python
from pathlib import Path

notes_path = Path("day-83") / "notes.txt"

print(notes_path.name)
print(notes_path.suffix)
print(notes_path.parent.as_posix())
```

You should see:

```text
notes.txt
.txt
day-83
```

The import was correct.

The bug was the type of value stored in the variable.

## Read the Docs

The standard library is too large to memorize.

Documentation is not a book you must read from start to finish. It is a map you open when you need a tool.

When you read a standard library page, look for four things:

- the module name
- the short description near the top
- one function or class that matches your problem
- one tiny example you can adapt

You can also ask Python for a short description from inside a script:

```python
import random

print(random.choice.__doc__)
```

You should see:

```text
Choose a random element from a non-empty sequence.
```

That tells you three useful things:

- `choice` belongs to `random`
- it chooses one element
- the sequence cannot be empty

That last point matters.

This works:

```python
import random

colors = ["red", "green", "blue"]

print(random.choice(colors))
```

This raises an error:

```python
import random

colors = []

print(random.choice(colors))
```

When documentation says "non-empty sequence," it is warning you about that empty-list case.

Good programmers do not memorize every detail.

They get better at knowing where to look.

## Mini Challenge

Create this file:

```text
day-83/random_picker.py
```

Write a program that:

- stores at least five options in a list
- uses `random.choice()` to pick one option
- uses `datetime.date.today()` to get today's date
- prints the date and the chosen option

Starter code:

```python
import random
from datetime import date

options = ["walk", "read", "stretch", "code", "tidy"]

today = date.today()
choice = random.choice(options)

print("Date:", today.isoformat())
print("Choice:", choice)
```

Your output will depend on the current date and the random choice.

If you want repeatable practice while learning, add a seed:

```python
import random
from datetime import date

random.seed(3)

options = ["walk", "read", "stretch", "code", "tidy"]

today = date.today()
choice = random.choice(options)

print("Date:", today.isoformat())
print("Choice:", choice)
```

The date can still change, but the random choice will be easier to repeat.

## Real-World Use

The standard library shows up everywhere in real Python projects.

A script might use:

- `pathlib` to find files in a project folder
- `datetime` to stamp a report with today's date
- `statistics` to summarize survey scores
- `collections.Counter` to count repeated words
- `random` to pick a sample record for testing
- `math` for numeric rules that are clearer than hand-written formulas

Here is a practical counting example:

```python
from collections import Counter

responses = ["yes", "no", "yes", "maybe", "yes", "no"]
counts = Counter(responses)

print(counts["yes"])
print(counts.most_common(2))
```

You should see:

```text
3
[('yes', 3), ('no', 2)]
```

Without `Counter`, you would need to write your own counting loop.

With `Counter`, the intent is visible right away:

```text
Count repeated values.
```

That is one reason standard library modules are worth learning. They often make your code shorter and easier to read.

## Recap

The standard library is Python's built-in collection of useful modules.

Today you used a few of them:

- `random` for choices
- `datetime` for dates
- `math` for numeric helpers
- `pathlib` for paths
- `statistics` for averages and medians
- `collections` for helpful containers like `Counter`

The deeper lesson is not that you must memorize all of these.

The deeper lesson is that Python already includes a lot of tools, and part of growing as a programmer is learning to check what already exists before writing your own version.

## Lesson Checklist

Before moving on, make sure you can:

- explain the phrase "batteries included"
- import a standard library module
- use dot notation to call a function from a module
- name at least four useful standard library modules
- use `random.choice()` with a non-empty list
- use `date` and `timedelta` from `datetime`
- use `Path` from `pathlib`
- use `statistics.mean()` or `statistics.median()`
- use `Counter` to count repeated values
- avoid naming your own files after standard library modules
- explain why documentation is something you consult, not memorize

## Exercises

### Exercise 1: Choose A Module

For each task, write the standard library module you would check first.

```text
1. Pick a random winner from a list.
2. Find the median score.
3. Create a path for a notes file.
4. Count how many times each word appears.
5. Add seven days to a date.
```

Possible answers:

```text
1. random
2. statistics
3. pathlib
4. collections
5. datetime
```

### Exercise 2: Random Study Picker

Create this file:

```text
day-83/study_picker.py
```

Write a program that:

- imports `random`
- stores at least five study tasks in a list
- picks one task
- prints it in a sentence

Starter code:

```python
import random

tasks = ["review notes", "write flashcards", "solve a quiz", "read docs", "refactor code"]

random.seed(8)
task = random.choice(tasks)

print("Study task:", task)
```

### Exercise 3: Date Calculator

Create this file:

```text
day-83/date_calculator.py
```

Write a program that:

- imports `date` and `timedelta` from `datetime`
- stores a fixed starting date
- adds 30 days
- prints both dates

Starter code:

```python
from datetime import date, timedelta

start = date(2026, 5, 10)
finish = start + timedelta(days=30)

print("Start:", start.isoformat())
print("Finish:", finish.isoformat())
```

### Exercise 4: Score Summary

Create this file:

```text
day-83/score_summary.py
```

Write a program that:

- imports `statistics`
- stores at least six scores in a list
- prints the mean
- prints the median

Starter code:

```python
import statistics

scores = [81, 92, 75, 88, 92, 100]

print("Mean:", statistics.mean(scores))
print("Median:", statistics.median(scores))
```

### Exercise 5: Path Parts

Create this file:

```text
day-83/path_parts.py
```

Write a program that:

- imports `Path` from `pathlib`
- creates a path for `day-83/notes.txt`
- prints the full path as text
- prints the file name
- prints the suffix

Starter code:

```python
from pathlib import Path

notes_path = Path("day-83") / "notes.txt"

print(notes_path.as_posix())
print(notes_path.name)
print(notes_path.suffix)
```

### Exercise 6: Count Votes

Create this file:

```text
day-83/vote_counter.py
```

Write a program that:

- imports `Counter` from `collections`
- stores a list with repeated values
- counts the values
- prints the most common value

Starter code:

```python
from collections import Counter

votes = ["tea", "coffee", "tea", "water", "coffee", "tea"]
counts = Counter(votes)

print(counts)
print(counts.most_common(1))
```

## Tiny Win

You can now look outside your own file for help without leaving Python's built-in toolkit.

That is a big step.

It means your first question can become:

```text
Does Python already have a module for this?
```

Often, the answer is yes.

## Tomorrow

Tomorrow you will step beyond the standard library.

Some tools do not come with Python. Those are external packages, and they need to be installed into a project before you can import them.

Day 84 will introduce package installation, `pip`, and the difference between:

```text
import a module that comes with Python
```

and:

```text
install a package first, then import it
```

Today was the built-in toolkit.

Tomorrow is how Python projects add more tools.
