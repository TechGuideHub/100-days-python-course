# Day 86: List Comprehensions

**Focus:** Building new lists from existing lists with compact, readable syntax  
**You will practice:** transforming lists, filtering lists, reading `[expression for item in items]`, adding an optional `if`, choosing a normal loop when code needs more steps, and avoiding cramped one-line code  
**Estimated time:** 45-60 minutes

## Today's Goal

In the last stretch, you worked around the Python program: environments, project setup, installed tools, and the files that support a project.

Today you come back inside core Python.

A list comprehension is a short way to build a new list from an existing list.

By the end of today, you should be able to:

- read the basic syntax `[expression for item in items]`
- transform every value in a list
- filter a list with an optional `if`
- combine a simple transform with a simple filter
- rewrite a basic append loop as a list comprehension
- decide when a normal loop is easier to read
- avoid list comprehensions that try to do too much
- prepare for Day 87, where the same idea will build dictionaries

List comprehensions are not a new kind of data.

They are a cleaner way to create a list when the pattern is simple.

## The Big Idea

Start with a familiar loop.

```python
numbers = [1, 2, 3, 4]

squares = []

for number in numbers:
    squares.append(number * number)

print(squares)
```

You should see:

```text
[1, 4, 9, 16]
```

That loop has a common shape:

```text
make an empty list
loop over another list
append one new value each time
```

A list comprehension writes that same idea more directly.

```python
numbers = [1, 2, 3, 4]

squares = [number * number for number in numbers]

print(squares)
```

You should see:

```text
[1, 4, 9, 16]
```

The shape is:

```text
[expression for item in items]
```

In this example:

- `number * number` is the expression
- `number` is the current item
- `numbers` is the list being read

The expression is the value that goes into the new list.

The `for` part says where the values come from.

## The Mental Model

Read a list comprehension in this order:

```text
[what to make for one item in many items]
```

For example:

```python
names = ["mina", "sam", "iris"]

clean_names = [name.title() for name in names]

print(clean_names)
```

You should see:

```text
['Mina', 'Sam', 'Iris']
```

Read it as:

```text
For each name in names, make name.title().
Put each result into a new list.
```

The original list does not change.

```python
names = ["mina", "sam", "iris"]

clean_names = [name.title() for name in names]

print(names)
print(clean_names)
```

You should see:

```text
['mina', 'sam', 'iris']
['Mina', 'Sam', 'Iris']
```

The comprehension builds a new list.

That is useful because you can keep the original data and the changed data separate.

### Transforming A List

Transforming means every item is changed into a new value.

```python
prices = [10, 25, 40]

sale_prices = [price * 0.9 for price in prices]

print(sale_prices)
```

You should see:

```text
[9.0, 22.5, 36.0]
```

Here are a few more transformations.

```python
words = ["python", "lists", "practice"]

lengths = [len(word) for word in words]

print(lengths)
```

You should see:

```text
[6, 5, 8]
```

```python
temperatures_c = [0, 10, 20, 30]

temperatures_f = [(temp * 9 / 5) + 32 for temp in temperatures_c]

print(temperatures_f)
```

You should see:

```text
[32.0, 50.0, 68.0, 86.0]
```

```python
prices = [4.5, 10, 2.75]

labels = [f"${price:.2f}" for price in prices]

print(labels)
```

You should see:

```text
['$4.50', '$10.00', '$2.75']
```

In each case, the new list has the same number of items as the old list.

Each item was changed into something else.

### Filtering A List

Filtering means keeping only some items.

Add an `if` at the end:

```text
[expression for item in items if condition]
```

Example:

```python
scores = [42, 71, 88, 59, 100]

passing_scores = [score for score in scores if score >= 60]

print(passing_scores)
```

You should see:

```text
[71, 88, 100]
```

The final `if` decides whether the item is included.

It does not change the item.

This comprehension:

```python
numbers = [1, 2, 3, 4, 5, 6]

even_numbers = [number for number in numbers if number % 2 == 0]

print(even_numbers)
```

You should see:

```text
[2, 4, 6]
```

Read it as:

```text
For each number in numbers, keep number if number is even.
```

### Transforming And Filtering Together

You can transform and filter in the same comprehension when both parts are easy to read.

```python
words = ["apple", "fig", "banana", "kiwi"]

long_words = [word.upper() for word in words if len(word) >= 5]

print(long_words)
```

You should see:

```text
['APPLE', 'BANANA']
```

Read it as:

```text
For each word in words, if the word has at least 5 letters, add word.upper().
```

The expression comes first:

```text
word.upper()
```

The filter comes last:

```text
if len(word) >= 5
```

This order feels backwards at first.

Practice reading the `for` part first, then the expression.

## Try It Yourself

Create a folder named:

```text
day-86
```

You can put today's practice files there.

### Step 1: Rewrite A Loop

Create this file:

```text
day-86/squares.py
```

Start with the loop version:

```python
numbers = [2, 4, 6, 8]

squares = []

for number in numbers:
    squares.append(number * number)

print(squares)
```

You should see:

```text
[4, 16, 36, 64]
```

Now replace the loop with a list comprehension:

```python
numbers = [2, 4, 6, 8]

squares = [number * number for number in numbers]

print(squares)
```

You should see the same result.

### Step 2: Clean Names

Create this file:

```text
day-86/clean_names.py
```

Add this code:

```python
raw_names = ["  mina", "SAM  ", " iris "]

clean_names = [name.strip().title() for name in raw_names]

print(clean_names)
```

You should see:

```text
['Mina', 'Sam', 'Iris']
```

This is a good use of a list comprehension because each item gets one clear transformation.

### Step 3: Keep Passing Scores

Create this file:

```text
day-86/passing_scores.py
```

Add this code:

```python
scores = [55, 72, 91, 48, 67]

passing_scores = [score for score in scores if score >= 60]

print(passing_scores)
```

You should see:

```text
[72, 91, 67]
```

This is filtering.

The expression is just `score` because you are keeping the original score.

### Step 4: Work With Project File Names

Environment work often has you looking at project files such as Python files, text files, and settings files.

The list comprehension is still just core Python.

Create this file:

```text
day-86/project_files.py
```

Add this code:

```python
file_names = ["main.py", ".env", "README.md", "test_app.py", "notes.txt"]

python_files = [name for name in file_names if name.endswith(".py")]

print(python_files)
```

You should see:

```text
['main.py', 'test_app.py']
```

The environment may contain many kinds of files.

Your Python code can still filter a plain list of names.

### Step 5: Use Two Lines When It Helps

Sometimes one comprehension can work, but two clear steps are better for beginners.

Create this file:

```text
day-86/shopping_list.py
```

Add this code:

```python
raw_items = [" apples ", "", "RICE", "  ", "tea"]

cleaned_items = [item.strip().lower() for item in raw_items]
shopping_items = [item for item in cleaned_items if item]

print(shopping_items)
```

You should see:

```text
['apples', 'rice', 'tea']
```

The first comprehension transforms every string.

The second comprehension filters out empty strings.

That is easier to read than trying to do everything at once.

### When A Normal Loop Is Better

Use a normal `for` loop when the work has several steps.

That includes code that:

- prints while it loops
- writes to a file
- catches errors
- uses `continue` or `break`
- updates more than one list or counter
- needs several named intermediate values

This belongs in a normal loop:

```python
prices = [12, 0, "unknown", 5]

totals = []

for price in prices:
    if not isinstance(price, (int, float)):
        print(f"Skipping {price}")
        continue

    with_tax = price * 1.08
    totals.append(round(with_tax, 2))

print(totals)
```

You should see:

```text
Skipping unknown
[12.96, 0.0, 5.4]
```

A list comprehension is best when the reader can understand it in one breath.

If you need to explain the line out loud twice, it probably wants to be a normal loop.

## Common Mistake

A common mistake is writing a condition as the expression when you meant to filter.

```python
names = ["Mina", "", "Sam"]

result = [name != "" for name in names]

print(result)
```

You should see:

```text
[True, False, True]
```

That code asks:

```text
Is each name not empty?
```

It does not keep the names.

To filter the list, put the condition after the `for` part:

```python
names = ["Mina", "", "Sam"]

result = [name for name in names if name != ""]

print(result)
```

You should see:

```text
['Mina', 'Sam']
```

Another mistake is putting the transformation in the wrong place.

```python
numbers = [1, 2, 3]

doubled = [number for number in numbers * 2]

print(doubled)
```

You should see:

```text
[1, 2, 3, 1, 2, 3]
```

That doubled the list itself.

It did not double each number.

This is the version you wanted:

```python
numbers = [1, 2, 3]

doubled = [number * 2 for number in numbers]

print(doubled)
```

You should see:

```text
[2, 4, 6]
```

One more habit to avoid:

```text
[print(name) for name in names]
```

That uses a comprehension for printing.

Use a normal loop for actions.

Use a comprehension for building a new list.

## Debug It

This program tries to clean a list and remove blank entries.

```python
raw_words = [" tea ", "   ", "rice"]

clean_words = [word.strip() for word in raw_words if word]

print(clean_words)
```

You should see:

```text
['tea', '', 'rice']
```

The blank-looking string `"   "` passed the filter because it was not empty before `.strip()` ran.

One beginner-friendly fix is to use two steps:

```python
raw_words = [" tea ", "   ", "rice"]

stripped_words = [word.strip() for word in raw_words]
clean_words = [word for word in stripped_words if word]

print(clean_words)
```

You should see:

```text
['tea', 'rice']
```

This version is not the shortest possible code.

It is clear.

Clear code is allowed.

## Read the Docs

The Python documentation explains list comprehensions in the data structures section.

When you read it, look for these pieces first:

- the square brackets
- the expression at the start
- the `for` clause
- the optional `if` clause

You may also see examples with more than one `for` clause.

Those are called nested comprehensions.

You do not need nested comprehensions today.

Focus on the everyday shape:

```text
[expression for item in items]
```

and:

```text
[expression for item in items if condition]
```

Try this small documentation-style example:

```python
numbers = [1, 2, 3, 4]

pairs = [(number, number * number) for number in numbers]

print(pairs)
```

You should see:

```text
[(1, 1), (2, 4), (3, 9), (4, 16)]
```

The new list contains tuples.

That is fine because the expression can create any value: a number, string, tuple, list, dictionary, or object.

For now, keep your expressions small.

## Mini Challenge

Build a clean task list.

Create this file:

```text
day-86/task_list.py
```

Add this code:

```python
raw_tasks = ["  email team", "", "Review notes ", "  ", "pay invoice"]

cleaned_tasks = [task.strip().lower() for task in raw_tasks]
tasks = [task for task in cleaned_tasks if task]
numbered_tasks = [f"{number}. {task.title()}" for number, task in enumerate(tasks, start=1)]

for task in numbered_tasks:
    print(task)
```

You should see:

```text
1. Email Team
2. Review Notes
3. Pay Invoice
```

This challenge uses three ideas:

- transform raw text
- filter empty strings
- transform the cleaned tasks into display labels

If `enumerate()` feels new, read this part as:

```text
Give me a number and a task for each task in the list.
Start counting at 1.
```

## Real-World Use

List comprehensions show up whenever a program receives a list and needs a cleaner list.

For example, an API response might give you a list of dictionaries.

```python
weather_rows = [
    {"city": "Tokyo", "temperature": 24},
    {"city": "Oslo", "temperature": 9},
    {"city": "Nairobi", "temperature": 26}
]

city_names = [row["city"] for row in weather_rows]
warm_cities = [row["city"] for row in weather_rows if row["temperature"] >= 20]

print(city_names)
print(warm_cities)
```

You should see:

```text
['Tokyo', 'Oslo', 'Nairobi']
['Tokyo', 'Nairobi']
```

Or imagine a tool that shows installed package lines:

```python
installed_lines = ["requests==2.32.3", "pytest==8.3.4", "rich==13.9.4"]

package_names = [line.split("==")[0] for line in installed_lines]

print(package_names)
```

You should see:

```text
['requests', 'pytest', 'rich']
```

This is the bridge from environment work back to core Python:

```text
The environment gives your project tools and files.
Your Python code still needs to clean, filter, and reshape lists.
```

List comprehensions are one of the common tools for that reshaping.

## Recap

Today you learned that a list comprehension builds a new list.

The basic syntax is:

```text
[expression for item in items]
```

Use it to transform a list:

```python
numbers = [1, 2, 3]

doubled = [number * 2 for number in numbers]

print(doubled)
```

You should see:

```text
[2, 4, 6]
```

Use an optional `if` to filter:

```python
numbers = [1, 2, 3, 4, 5]

odd_numbers = [number for number in numbers if number % 2 == 1]

print(odd_numbers)
```

You should see:

```text
[1, 3, 5]
```

Good list comprehensions are short and readable.

Use a normal loop when the work needs several steps, side effects, error handling, or extra explanation.

The goal is not to write the fewest lines.

The goal is to make the list-building pattern easy to see.

## Lesson Checklist

Before moving on, make sure you can:

- [ ] explain what a list comprehension creates
- [ ] read `[expression for item in items]`
- [ ] transform a list of numbers
- [ ] transform a list of strings
- [ ] filter a list with `if`
- [ ] tell the difference between a filter and a boolean expression
- [ ] rewrite a simple append loop as a comprehension
- [ ] split a messy comprehension into two clearer steps
- [ ] choose a normal loop when the work has several actions

## Exercises

### Exercise 1: Double The Numbers

Start with:

```text
numbers = [3, 6, 9, 12]
```

Use a list comprehension to create:

```text
[6, 12, 18, 24]
```

### Exercise 2: Add Tax

Start with:

```text
prices = [3, 8, 12]
```

Use a list comprehension with `round()` to create:

```text
[3.24, 8.64, 12.96]
```

### Exercise 3: Clean Usernames

Start with:

```text
raw_usernames = ["  mina", "SAM  ", " Iris "]
```

Use a list comprehension to create:

```text
['mina', 'sam', 'iris']
```

### Exercise 4: Keep Passing Scores

Start with:

```text
scores = [38, 60, 72, 59, 91]
```

Use a list comprehension to keep scores that are `60` or higher.

Your result should be:

```text
[60, 72, 91]
```

### Exercise 5: Find Python Files

Start with:

```text
file_names = ["app.py", "notes.txt", "config.env", "test_app.py", "README.md"]
```

Use a list comprehension to keep only names ending with `.py`.

Your result should be:

```text
['app.py', 'test_app.py']
```

### Exercise 6: Fix The Condition

This code runs, but it checks the wrong thing:

```python
names = ["Mina", "Jo", "Samuel", "Iris"]

long_names = [name for name in names if len(names) > 3]

print(long_names)
```

You should see:

```text
['Mina', 'Jo', 'Samuel', 'Iris']
```

Fix the condition so it keeps names longer than 3 characters.

The corrected result should be:

```text
['Mina', 'Samuel', 'Iris']
```

### Exercise 7: Choose The Clearer Tool

Read this task:

```text
Loop over prices.
Skip values that are not numbers.
Print a message for each skipped value.
Add tax to the valid prices.
Store the final prices in a list.
```

Should this be a list comprehension or a normal loop?

Write one sentence explaining your choice.

### Exercise 8: Prepare For Dictionaries

Start with:

```text
names = ["Mina", "Sam", "Iris"]
```

Use a list comprehension to create a list of name lengths:

```text
[4, 3, 4]
```

Tomorrow you will use a similar idea to create a dictionary where each name points to its length.

## Tiny Win

You can now read and write one of Python's most common list-building patterns.

That makes other people's code less mysterious.

It also gives you a clean tool for everyday work: take a list, change it, filter it, and keep the result.

Small syntax, big usefulness.

## Tomorrow

Tomorrow is:

```text
Day 87: Dictionary Comprehensions
```

The shape will feel familiar:

```text
{key_expression: value_expression for item in items}
```

Today you built lists.

Tomorrow you will build dictionaries.
