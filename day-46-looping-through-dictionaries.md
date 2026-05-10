# Day 46: Looping Through Dictionaries

**Focus:** Visiting dictionary keys, values, and key-value pairs with a `for` loop  
**You will practice:** looping through keys directly, using `.keys()`, `.values()`, and `.items()`, choosing clear loop variable names, and printing simple reports from dictionaries  
**Estimated time:** 40-50 minutes

## Today's Goal

Today you will learn how to loop through a dictionary.

A dictionary stores values under labels called keys:

```python
profile = {
    "name": "Maya",
    "city": "Pune",
    "learning": "Python"
}

print(profile["name"])
```

You should see:

```text
Maya
```

That works when you want one specific value.

But many programs need to visit every field in a dictionary.

By the end of this lesson, you should be able to:

- loop through dictionary keys directly
- use `.keys()` when you want keys
- use `.values()` when you want values
- use `.items()` when you want keys and values together
- choose clear loop variable names
- print key-value pairs in a simple report
- avoid list-style indexing mistakes with dictionaries

The main idea is:

> A dictionary loop lets Python visit the dictionary one part at a time.

## The Big Idea

Start with a small profile:

```python
profile = {
    "name": "Maya",
    "city": "Pune",
    "learning": "Python"
}
```

When you loop through a dictionary directly, Python gives you the keys:

```python
profile = {
    "name": "Maya",
    "city": "Pune",
    "learning": "Python"
}

for field in profile:
    print(field)
```

You should see:

```text
name
city
learning
```

The loop variable `field` holds one key at a time.

You can use that key to get the matching value:

```python
profile = {
    "name": "Maya",
    "city": "Pune",
    "learning": "Python"
}

for field in profile:
    print(field + ":", profile[field])
```

You should see:

```text
name: Maya
city: Pune
learning: Python
```

This works because each key points to a value:

```text
"name"     -> "Maya"
"city"     -> "Pune"
"learning" -> "Python"
```

Python also gives you dictionary methods that make your intention clearer.

Use `.keys()` when you want the keys:

```python
profile = {
    "name": "Maya",
    "city": "Pune",
    "learning": "Python"
}

for field in profile.keys():
    print(field)
```

You should see:

```text
name
city
learning
```

Looping through the dictionary directly and looping through `.keys()` usually do the same thing.

These two loops both visit the keys:

```python
profile = {
    "name": "Maya",
    "city": "Pune",
    "learning": "Python"
}

for field in profile:
    print(field)

for field in profile.keys():
    print(field)
```

You should see:

```text
name
city
learning
name
city
learning
```

Use the direct version when the code is simple:

```python
for field in profile:
```

Use `.keys()` when it helps the line read more clearly:

```python
for field in profile.keys():
```

Use `.values()` when you only need the values:

```python
scores = {
    "Asha": 9,
    "Ben": 7,
    "Cara": 10
}

for score in scores.values():
    print("Score:", score)
```

You should see:

```text
Score: 9
Score: 7
Score: 10
```

Use `.items()` when you need both the key and the value:

```python
scores = {
    "Asha": 9,
    "Ben": 7,
    "Cara": 10
}

for student, score in scores.items():
    print(student + ":", score)
```

You should see:

```text
Asha: 9
Ben: 7
Cara: 10
```

That is the most common shape for printing a dictionary report.

## The Mental Model

Think of a dictionary as a set of labeled boxes.

```text
profile

name      Maya
city      Pune
learning  Python
```

The keys are the labels:

```text
name
city
learning
```

The values are what the labels point to:

```text
Maya
Pune
Python
```

When you write:

```python
for field in profile:
```

Python hands you one key at a time.

On the first loop:

```text
field is "name"
```

On the second loop:

```text
field is "city"
```

On the third loop:

```text
field is "learning"
```

If you want the value, use the key:

```python
profile[field]
```

If you want Python to hand you both at once, use `.items()`:

```python
profile = {
    "name": "Maya",
    "city": "Pune",
    "learning": "Python"
}

for field, answer in profile.items():
    print(field + ":", answer)
```

Now each loop gives you a pair:

```text
field is "name", answer is "Maya"
field is "city", answer is "Pune"
field is "learning", answer is "Python"
```

The loop variable names should match what one loop step gives you.

Clear names:

```python
for field in profile:
for item, quantity in inventory.items():
for student, score in scores.items():
for setting, choice in settings.items():
```

Less helpful names:

```python
for x in profile:
for a, b in scores.items():
```

Python will accept unclear names, but clear names make the code easier to read.

## Try It Yourself

Create a file named:

```text
day-46/loop_dictionaries.py
```

You will practice the three common dictionary loop shapes.

### Step 1: Loop Through Keys Directly

Code:

```python
profile = {
    "name": "Maya",
    "city": "Pune",
    "learning": "Python"
}

for field in profile:
    print(field)
```

You should see:

```text
name
city
learning
```

The loop visits the keys.

### Step 2: Use Each Key To Get Its Value

Code:

```python
profile = {
    "name": "Maya",
    "city": "Pune",
    "learning": "Python"
}

for field in profile:
    print(field + ":", profile[field])
```

You should see:

```text
name: Maya
city: Pune
learning: Python
```

The key is stored in `field`.

The value is found with:

```python
profile[field]
```

### Step 3: Loop Through Values Only

Code:

```python
inventory = {
    "notebooks": 4,
    "pens": 12,
    "markers": 3
}

for quantity in inventory.values():
    print("Quantity:", quantity)
```

You should see:

```text
Quantity: 4
Quantity: 12
Quantity: 3
```

This is useful when the keys do not matter for the current task.

### Step 4: Loop Through Keys And Values Together

Code:

```python
inventory = {
    "notebooks": 4,
    "pens": 12,
    "markers": 3
}

for item, quantity in inventory.items():
    print(item + ":", quantity)
```

You should see:

```text
notebooks: 4
pens: 12
markers: 3
```

This is usually the cleanest way to print dictionary contents.

### Step 5: Print A Settings Report

Code:

```python
settings = {
    "theme": "dark",
    "autosave": "on",
    "language": "English"
}

print("Settings")

for setting, choice in settings.items():
    print(setting + ":", choice)
```

You should see:

```text
Settings
theme: dark
autosave: on
language: English
```

This is a simple report.

The dictionary stores the data.

The loop controls how the data is displayed.

## Common Mistake

### Mistake 1: Expecting List-Style Indexes

Broken code:

```python
profile = {
    "name": "Maya",
    "city": "Pune"
}

print(profile[0])
```

This is broken because dictionaries use keys, not list-style positions.

There is no key named `0` in this dictionary.

Fixed code:

```python
profile = {
    "name": "Maya",
    "city": "Pune"
}

print(profile["name"])
```

You should see:

```text
Maya
```

If you want every key, loop through the dictionary:

```python
profile = {
    "name": "Maya",
    "city": "Pune"
}

for field in profile:
    print(field)
```

You should see:

```text
name
city
```

Use keys to read dictionary values.

Use indexes for lists.

### Mistake 2: Forgetting `.items()` When You Need Both Parts

Broken code:

```python
scores = {
    "Asha": 9,
    "Ben": 7,
    "Cara": 10
}

for student, score in scores:
    print(student + ":", score)
```

This is broken because looping through `scores` directly gives one key at a time.

It does not give a student-score pair.

Fixed code:

```python
scores = {
    "Asha": 9,
    "Ben": 7,
    "Cara": 10
}

for student, score in scores.items():
    print(student + ":", score)
```

You should see:

```text
Asha: 9
Ben: 7
Cara: 10
```

When you need both the key and value, reach for `.items()`.

### Mistake 3: Using `.values()` When You Still Need The Key

Broken code:

```python
settings = {
    "theme": "dark",
    "notifications": "on"
}

for choice in settings.values():
    print(setting + ":", choice)
```

This is broken because `choice` only holds a value like `"dark"` or `"on"`.

The variable `setting` was never created.

Fixed code:

```python
settings = {
    "theme": "dark",
    "notifications": "on"
}

for setting, choice in settings.items():
    print(setting + ":", choice)
```

You should see:

```text
theme: dark
notifications: on
```

Use `.values()` only when the values are enough.

Use `.items()` when the key still matters.

### Mistake 4: Choosing Unclear Loop Variable Names

This code works, but it is hard to read.

Code:

```python
inventory = {
    "notebooks": 4,
    "pens": 12,
    "markers": 3
}

for x, y in inventory.items():
    print(x, y)
```

You should see:

```text
notebooks 4
pens 12
markers 3
```

Python does not care that the names are vague.

People reading the code do.

A clearer version is:

```python
inventory = {
    "notebooks": 4,
    "pens": 12,
    "markers": 3
}

for item, quantity in inventory.items():
    print(item + ":", quantity)
```

You should see:

```text
notebooks: 4
pens: 12
markers: 3
```

Choose names that describe one key and one value.

## Debug It

Here is a broken program.

Goal:

```text
Inventory Report
notebooks: 4
pens: 12
markers: 3
Total item types: 3
```

Broken code:

```python
inventory = {
    "notebooks": 4,
    "pens": 12,
    "markers": 3
}

print("Inventory Report")

for item, quantity in inventory:
    print(item + ":", quantity)

print("Total item types:", len(inventory))
```

The problem is this line:

```python
for item, quantity in inventory:
```

Looping through a dictionary directly gives one key at a time.

The program needs both the key and the value, so it should use `.items()`.

Fixed code:

```python
inventory = {
    "notebooks": 4,
    "pens": 12,
    "markers": 3
}

print("Inventory Report")

for item, quantity in inventory.items():
    print(item + ":", quantity)

print("Total item types:", len(inventory))
```

You should see:

```text
Inventory Report
notebooks: 4
pens: 12
markers: 3
Total item types: 3
```

Here is another broken program.

Goal:

```text
theme: dark
notifications: on
font size: medium
```

Broken code:

```python
settings = {
    "theme": "dark",
    "notifications": "on",
    "font size": "medium"
}

for setting in settings.values():
    print(setting + ":", settings[setting])
```

The problem is that `settings.values()` gives the values:

```text
dark
on
medium
```

Those values are not the keys.

The code then tries to use each value as if it were a key:

```python
settings[setting]
```

Fixed code:

```python
settings = {
    "theme": "dark",
    "notifications": "on",
    "font size": "medium"
}

for setting, choice in settings.items():
    print(setting + ":", choice)
```

You should see:

```text
theme: dark
notifications: on
font size: medium
```

When a dictionary loop is confusing, ask:

- Do I need keys only?
- Do I need values only?
- Do I need keys and values together?
- Do my loop variable names describe what I am getting?

## Read the Docs

Python's official documentation describes dictionaries under mapping types:

```text
https://docs.python.org/3/library/stdtypes.html#mapping-types-dict
```

You do not need to read the whole page today.

Look for these dictionary ideas:

```text
len(d)
d[key]
d.keys()
d.values()
d.items()
```

The documentation often uses `d` to mean "some dictionary."

Read those examples like this:

```text
d[key] gets the value for one key.
d.keys() gives the dictionary keys.
d.values() gives the dictionary values.
d.items() gives key-value pairs.
```

Try this small documentation-style example:

```python
settings = {
    "theme": "dark",
    "autosave": "on"
}

print(list(settings.keys()))
print(list(settings.values()))
print(list(settings.items()))
```

You should see:

```text
['theme', 'autosave']
['dark', 'on']
[('theme', 'dark'), ('autosave', 'on')]
```

The `list()` calls are only there to make the output easier to see.

In everyday code, you can usually loop over the dictionary view directly:

```python
settings = {
    "theme": "dark",
    "autosave": "on"
}

for setting, choice in settings.items():
    print(setting + ":", choice)
```

You should see:

```text
theme: dark
autosave: on
```

## Mini Challenge

Create a file named:

```text
day-46/score_report.py
```

Build a small score report.

Start with this dictionary:

```python
scores = {
    "Maya": 88,
    "Noah": 95,
    "Iris": 91,
    "Leo": 72
}
```

Your program should:

- print a title
- print each student and score
- count how many scores are at least `90`
- print the number of students
- print the number of high scores

One possible solution:

```python
scores = {
    "Maya": 88,
    "Noah": 95,
    "Iris": 91,
    "Leo": 72
}

high_scores = 0

print("Score Report")

for student, score in scores.items():
    print(student + ":", score)

    if score >= 90:
        high_scores = high_scores + 1

print("Students:", len(scores))
print("High scores:", high_scores)
```

You should see:

```text
Score Report
Maya: 88
Noah: 95
Iris: 91
Leo: 72
Students: 4
High scores: 2
```

After it works, add another student to the dictionary.

Run the program again.

The loop should print the new student without needing another `print()` line.

## Real-World Use

Dictionary loops are useful when a program stores labeled information and needs to show or check each part.

A profile can store fields about one person:

```python
profile = {
    "name": "Maya",
    "city": "Pune",
    "learning": "Python"
}

for field, answer in profile.items():
    print(field + ":", answer)
```

You should see:

```text
name: Maya
city: Pune
learning: Python
```

An inventory can store item names and quantities:

```python
inventory = {
    "apples": 6,
    "bread": 2,
    "milk": 1
}

print("Stock Report")

for item, quantity in inventory.items():
    print(item + ":", quantity)
```

You should see:

```text
Stock Report
apples: 6
bread: 2
milk: 1
```

A settings screen can store option names and selected choices:

```python
settings = {
    "theme": "dark",
    "notifications": "on",
    "text size": "large"
}

for setting, choice in settings.items():
    print(setting + ":", choice)
```

You should see:

```text
theme: dark
notifications: on
text size: large
```

These examples all have the same shape:

```text
label -> value
label -> value
label -> value
```

When your data has that shape, `.items()` often gives you the cleanest loop.

## Recap

Today you learned how to loop through dictionaries.

You practiced:

- looping through a dictionary directly to get keys
- using `.keys()` to make a keys-only loop explicit
- using `.values()` to get values only
- using `.items()` to get key-value pairs
- printing dictionary reports
- choosing loop variable names that describe the data
- avoiding list-style indexes with dictionaries
- debugging loops that use the wrong dictionary method

The basic choices are:

```python
for key in dictionary:
    print(key)
```

```python
for value in dictionary.values():
    print(value)
```

```python
for key, value in dictionary.items():
    print(key, value)
```

Use the shape that matches what you need.

## Lesson Checklist

Before moving on, check that you can:

- explain what happens when you loop through a dictionary directly
- use `.keys()` to loop through keys
- use `.values()` to loop through values
- use `.items()` to loop through key-value pairs
- print a dictionary as a simple report
- choose clear names like `student`, `score`, `item`, and `quantity`
- explain why `dictionary[0]` is usually wrong
- explain why `.items()` is needed when the loop needs both parts
- tell the difference between a key and a value while reading a loop
- fix a dictionary loop that uses the wrong variable

## Exercises

### Exercise 1

Predict the output.

```python
profile = {
    "name": "Maya",
    "city": "Pune"
}

for field in profile:
    print(field)
```

Then run it.

### Exercise 2

Create a dictionary named `favorite_foods`.

Use food names as keys and simple ratings as values.

Loop through the keys and print each food name.

### Exercise 3

Loop through this inventory with `.keys()`:

```python
inventory = {
    "notebooks": 4,
    "pens": 12,
    "markers": 3
}
```

Print each item name.

### Exercise 4

Loop through this inventory with `.values()`:

```python
inventory = {
    "notebooks": 4,
    "pens": 12,
    "markers": 3
}
```

Print each quantity.

### Exercise 5

Loop through this score dictionary with `.items()`:

```python
scores = {
    "Asha": 9,
    "Ben": 7,
    "Cara": 10
}
```

Print each line like this:

```text
Asha: 9
```

### Exercise 6

Create a settings dictionary with three settings.

Example keys:

```text
theme
notifications
language
```

Use `.items()` to print a settings report.

### Exercise 7

Fix the broken code.

Broken code:

```python
profile = {
    "name": "Maya",
    "city": "Pune"
}

print(profile[0])
```

The goal is to print the name.

### Exercise 8

Fix the broken code.

Broken code:

```python
scores = {
    "Asha": 9,
    "Ben": 7,
    "Cara": 10
}

for student, score in scores:
    print(student + ":", score)
```

The goal is to print each student and score.

### Exercise 9

Rewrite this loop with clearer variable names.

```python
inventory = {
    "notebooks": 4,
    "pens": 12
}

for x, y in inventory.items():
    print(x, y)
```

Choose names that describe the key and the value.

### Exercise 10

Build a simple report from this dictionary:

```python
book = {
    "title": "Python Notes",
    "pages": 45,
    "status": "draft"
}
```

Print:

```text
Book Report
title: Python Notes
pages: 45
status: draft
```

### Exercise 11

Count values while looping.

Start with:

```python
inventory = {
    "notebooks": 4,
    "pens": 12,
    "markers": 3,
    "erasers": 8
}
```

Use `.values()` to add all the quantities into a variable named `total`.

Print:

```text
Total items: 27
```

### Exercise 12

Prepare for tomorrow.

Start with one dictionary:

```python
student = {
    "name": "Maya",
    "score": 88,
    "passed": True
}
```

Use `.items()` to print every field and value.

Tomorrow, you will put several dictionaries like this inside a list.

## Tiny Win

You can now turn labeled data into readable output.

That is a useful step because many real programs store information as pairs:

```text
name -> Maya
score -> 88
theme -> dark
item -> quantity
```

Once you can loop through those pairs, dictionaries become much more practical.

## Tomorrow

Tomorrow is:

```text
Day 47: Lists of Dictionaries
```

Today you worked with one dictionary at a time.

Tomorrow you will work with a list that holds several dictionaries:

```python
students = [
    {"name": "Maya", "score": 88},
    {"name": "Noah", "score": 95},
    {"name": "Iris", "score": 91}
]
```

That structure lets a program store several records at once.

Today's `.items()` loops will help you read each dictionary clearly when it appears inside a larger collection.
