# Day 39: Sets

**Focus:** Storing unique values in an unordered collection  
**You will practice:** creating sets, removing duplicates, checking membership with `in`, adding with `add()`, removing with `remove()` and `discard()`, and avoiding common set mistakes  
**Estimated time:** 35-45 minutes

## Today's Goal

Today you will learn how to use sets.

A set is a collection that keeps only unique values.

You have already worked with lists, where order matters:

```python
tasks = ["read", "practice", "review"]
```

A set is different:

```python
tags = {"python", "practice", "review"}
```

The values are grouped together, but Python does not promise to keep them in the order you wrote them.

By the end of this lesson, you should be able to:

- create a set with curly braces
- create an empty set with `set()`
- explain why duplicate values disappear
- check whether a value is in a set
- add one value with `add()`
- remove values with `remove()` and `discard()`
- explain why sets do not use indexes
- recognize when a set is a good choice

The main idea is:

```text
A set is useful when uniqueness matters more than order.
```

## The Big Idea

A list can contain duplicates:

```python
names = ["Asha", "Ben", "Asha", "Cara", "Ben"]

print(names)
print(len(names))
```

You should see:

```text
['Asha', 'Ben', 'Asha', 'Cara', 'Ben']
5
```

The list keeps all five values because lists allow repeated items.

A set removes duplicates:

```python
names = {"Asha", "Ben", "Asha", "Cara", "Ben"}

print(sorted(names))
print(len(names))
```

You should see:

```text
['Asha', 'Ben', 'Cara']
3
```

The repeated `"Asha"` and `"Ben"` values were not kept twice.

The `sorted()` function is used here only to make the printed output predictable. A set itself is still unordered.

You can also make a set from a list:

```python
signups = ["Asha", "Ben", "Asha", "Cara", "Ben"]
unique_signups = set(signups)

print(sorted(unique_signups))
print("Signup count:", len(signups))
print("Unique count:", len(unique_signups))
```

You should see:

```text
['Asha', 'Ben', 'Cara']
Signup count: 5
Unique count: 3
```

This is one of the simplest reasons to use a set:

```text
Start with repeated values.
Keep one copy of each value.
```

## The Mental Model

Think of a set as a bag of labels where each label can appear only once.

This code:

```python
tags = {"python", "beginner", "practice", "python"}
```

means:

```text
Keep the tag "python".
Keep the tag "beginner".
Keep the tag "practice".
Do not keep a second copy of "python".
```

That gives you a collection of unique tags:

```python
tags = {"python", "beginner", "practice", "python"}

print(sorted(tags))
```

You should see:

```text
['beginner', 'practice', 'python']
```

The order in the printed list comes from `sorted()`, not from the set.

That difference matters.

A list has positions:

```text
Index:   0          1          2
Value: "red"    "green"    "blue"
```

A set does not work that way.

For a set, think:

```text
Is this value included?
How many unique values are there?
Can I add this value if it is not already present?
Can I remove this value?
```

The most common set question is membership:

```python
tags = {"python", "beginner", "practice"}

print("python" in tags)
print("advanced" in tags)
```

You should see:

```text
True
False
```

You can use that inside an `if` statement:

```python
tags = {"python", "beginner", "practice"}

if "python" in tags:
    print("This item is tagged with Python.")
else:
    print("This item needs a Python tag.")
```

You should see:

```text
This item is tagged with Python.
```

Sets are good at this kind of question.

They are not good when you need the first item, the second item, or the last item.

## Try It Yourself

Create a file named:

```text
day-39/sets_practice.py
```

Start with a set of tags.

Code:

```python
tags = {"python", "practice", "loops"}

print("Tag count:", len(tags))
print("Has python:", "python" in tags)
print("Has strings:", "strings" in tags)
```

You should see:

```text
Tag count: 3
Has python: True
Has strings: False
```

Now see what happens with duplicates.

Code:

```python
tags = {"python", "practice", "loops", "python", "loops"}

print(sorted(tags))
print("Tag count:", len(tags))
```

You should see:

```text
['loops', 'practice', 'python']
Tag count: 3
```

Even though `"python"` and `"loops"` were written twice, the set kept one copy of each value.

Now create an empty set.

Code:

```python
favorite_tags = set()

print(len(favorite_tags))
print("python" in favorite_tags)
```

You should see:

```text
0
False
```

Use `set()` for an empty set.

Do not use `{}` for an empty set. You will see why in the Common Mistake section.

Now add values.

Code:

```python
favorite_tags = set()

favorite_tags.add("python")
favorite_tags.add("practice")
favorite_tags.add("python")

print(sorted(favorite_tags))
print("Tag count:", len(favorite_tags))
```

You should see:

```text
['practice', 'python']
Tag count: 2
```

Adding `"python"` twice did not create two copies.

Now remove values.

Code:

```python
items = {"notebook", "pen", "charger"}

items.remove("pen")
items.discard("snacks")

print(sorted(items))
```

You should see:

```text
['charger', 'notebook']
```

`remove("pen")` removed a value that existed.

`discard("snacks")` did nothing because `"snacks"` was not in the set.

That is allowed. `discard()` does not complain when the value is missing.

## Common Mistake

### Mistake 1: Expecting A Set To Stay In Order

This code runs, but the order is not something you can depend on.

Code:

```python
tags = {"python", "practice", "loops"}

print(tags)
```

Python may print those values in a different order on different runs or different computers.

If the order matters, use a list:

```python
tags = ["python", "practice", "loops"]

print(tags[0])
```

You should see:

```text
python
```

If you only need a stable display of set values, sort them before printing:

```python
tags = {"python", "practice", "loops"}

print(sorted(tags))
```

You should see:

```text
['loops', 'practice', 'python']
```

`sorted(tags)` gives you a sorted list. It does not turn the set itself into an ordered collection.

### Mistake 2: Indexing A Set

Broken code:

```python
colors = {"red", "green", "blue"}

print(colors[0])
```

This is broken because a set does not have index positions.

You should see an error like:

```text
TypeError: 'set' object is not subscriptable
```

Fixed code:

```python
colors = {"red", "green", "blue"}

print("red" in colors)
```

You should see:

```text
True
```

If you need indexes, use a list.

If you need unique membership checks, use a set.

### Mistake 3: Using `{}` For An Empty Set

Broken code:

```python
tags = {}

tags.add("python")
```

This is broken because `{}` creates an empty dictionary, not an empty set.

You should see an error like:

```text
AttributeError: 'dict' object has no attribute 'add'
```

Fixed code:

```python
tags = set()

tags.add("python")

print(sorted(tags))
```

You should see:

```text
['python']
```

Use:

```python
set()
```

for an empty set.

Use:

```python
{}
```

later when you want an empty dictionary.

### Mistake 4: Removing A Missing Value With `remove()`

Broken code:

```python
packed_items = {"notebook", "pen", "charger"}

packed_items.remove("water bottle")
```

This is broken because `"water bottle"` is not in the set.

`remove()` expects the value to exist. If it does not exist, Python raises a `KeyError`.

Fixed code with a check:

```python
packed_items = {"notebook", "pen", "charger"}

if "water bottle" in packed_items:
    packed_items.remove("water bottle")
else:
    print("Water bottle was not packed.")

print(sorted(packed_items))
```

You should see:

```text
Water bottle was not packed.
['charger', 'notebook', 'pen']
```

Fixed code with `discard()`:

```python
packed_items = {"notebook", "pen", "charger"}

packed_items.discard("water bottle")

print(sorted(packed_items))
```

You should see:

```text
['charger', 'notebook', 'pen']
```

Use `remove()` when a missing value should be treated as a problem.

Use `discard()` when it is fine if the value is already missing.

## Debug It

Here is a broken program.

Goal:

```text
Unique names: ['Asha', 'Ben', 'Cara']
Unique count: 3
```

Broken code:

```python
names = ["Asha", "Ben", "Asha", "Cara", "Ben"]
unique_names = names

print("Unique names:", sorted(unique_names))
print("Unique count:", len(unique_names))
```

This code runs, but it does not solve the problem.

The variable `unique_names` is still a list with duplicates. It is just another name for the same list.

Fixed code:

```python
names = ["Asha", "Ben", "Asha", "Cara", "Ben"]
unique_names = set(names)

print("Unique names:", sorted(unique_names))
print("Unique count:", len(unique_names))
```

You should see:

```text
Unique names: ['Asha', 'Ben', 'Cara']
Unique count: 3
```

When you want unique values from a list, use `set(list_name)`.

Here is another broken program.

Goal:

```text
Packed item count: 3
Has charger: True
```

Broken code:

```python
packed_items = {}

packed_items.add("notebook")
packed_items.add("pen")
packed_items.add("charger")

print("Packed item count:", len(packed_items))
print("Has charger:", "charger" in packed_items)
```

The problem is the first line.

This:

```python
packed_items = {}
```

creates an empty dictionary.

The program needs an empty set.

Fixed code:

```python
packed_items = set()

packed_items.add("notebook")
packed_items.add("pen")
packed_items.add("charger")

print("Packed item count:", len(packed_items))
print("Has charger:", "charger" in packed_items)
```

You should see:

```text
Packed item count: 3
Has charger: True
```

When an empty collection uses curly braces by itself, pause and ask:

```text
Do I mean an empty dictionary or an empty set?
```

For an empty set, write `set()`.

## Read the Docs

Find Python's official documentation for set types:

```text
https://docs.python.org/3/library/stdtypes.html#set-types-set-frozenset
```

You do not need to read the whole page today.

Look for these ideas:

```text
set
len(s)
x in s
set.add(x)
set.remove(x)
set.discard(x)
```

The documentation often uses short names.

Read them like this:

```text
s means some set.
x means some value.
x in s means check whether x is in the set.
```

You may also see `frozenset`. You can ignore that for now.

Today's useful documentation habit is simply to connect the method names to code you already understand:

```python
tags = {"python", "practice"}

tags.add("loops")
tags.discard("practice")

print("loops" in tags)
print(sorted(tags))
```

You should see:

```text
True
['loops', 'python']
```

## Mini Challenge

Create a file named:

```text
day-39/unique_tags.py
```

Build a small tag cleaner.

Start with this list:

```python
raw_tags = ["python", "practice", "python", "loops", "practice", "sets"]
```

Your program should:

- create a set from `raw_tags`
- print the original number of tags
- print the number of unique tags
- check whether `"python"` is included
- add `"beginner"`
- discard `"old"`
- print the final tags in sorted order

One possible solution:

```python
raw_tags = ["python", "practice", "python", "loops", "practice", "sets"]
unique_tags = set(raw_tags)

print("Original count:", len(raw_tags))
print("Unique count:", len(unique_tags))
print("Has python:", "python" in unique_tags)

unique_tags.add("beginner")
unique_tags.discard("old")

print("Final tags:", sorted(unique_tags))
```

You should see:

```text
Original count: 6
Unique count: 4
Has python: True
Final tags: ['beginner', 'loops', 'practice', 'python', 'sets']
```

After it works, change `raw_tags` by adding more repeated values.

The original count should change.

The unique count should only change when you add a value that was not already there.

## Real-World Use

Sets are useful when a program cares about whether something is included, but not where it appears.

Examples:

- unique usernames from a signup list
- tags on an article
- items already collected in a game
- email addresses that should not receive the same message twice
- words found in a short piece of text
- product categories selected in a filter
- names of students who attended today

A set is especially useful for simple yes-or-no checks.

Code:

```python
completed_lessons = {"lists", "indexing", "slicing", "sets"}

if "sets" in completed_lessons:
    print("Sets lesson complete.")
else:
    print("Keep practicing sets.")
```

You should see:

```text
Sets lesson complete.
```

Sets also help when repeated values would make your program noisy.

Code:

```python
cart_items = ["pen", "notebook", "pen", "charger", "notebook"]
unique_items = set(cart_items)

print("Different item types:", len(unique_items))
print(sorted(unique_items))
```

You should see:

```text
Different item types: 3
['charger', 'notebook', 'pen']
```

This does not replace the shopping cart list. The list may still matter if you need quantities or order.

The set answers a different question:

```text
Which different item names appear at least once?
```

That is the kind of question sets are built for.

## Recap

Today you learned that:

- a set stores unique values
- sets are written with curly braces when they already have items
- duplicate values are removed
- sets are unordered
- sets do not use indexes
- `set()` creates an empty set
- `{}` creates an empty dictionary, not an empty set
- `in` checks whether a value is in a set
- `add()` adds one value
- adding the same value twice still keeps one copy
- `remove()` removes a value and raises an error if it is missing
- `discard()` removes a value if it exists and does nothing if it is missing
- `sorted(set_name)` is useful when you want predictable printed output

The basic shape is:

```python
items = {"first", "second", "third"}
```

Read it as:

```text
items is a collection of unique values.
The order is not the point.
```

## Lesson Checklist

Before moving on, check that you can:

- create a set with values inside it
- create an empty set with `set()`
- explain why `{}` is not an empty set
- explain what happens to duplicate values
- use `len()` to count unique values
- use `in` to check membership
- use `add()` to add a value
- explain why adding the same value twice does not create a duplicate
- use `remove()` when a value should exist
- use `discard()` when a missing value is okay
- explain why sets do not use indexes
- use `sorted()` when you need predictable output for display
- name one situation where a set is better than a list

## Exercises

### Exercise 1

Predict the output.

```python
colors = {"red", "green", "red", "blue"}

print(len(colors))
```

Then run it.

Why is the answer not `4`?

### Exercise 2

Create a set named `favorite_foods` with three food names.

Print the foods with `sorted(favorite_foods)`.

### Exercise 3

Create an empty set named `visited_pages`.

Add:

```text
home
about
home
contact
```

Print the length of the set.

### Exercise 4

Predict the output.

```python
allowed_choices = {"start", "help", "quit"}

print("help" in allowed_choices)
print("pause" in allowed_choices)
```

Then run it.

### Exercise 5

Use an `if` statement with a set.

Start with:

```python
packed_items = {"notebook", "charger", "pen"}
```

If `"charger"` is in the set, print:

```text
Charger packed.
```

Otherwise, print:

```text
Pack the charger.
```

### Exercise 6

Fix the broken code.

Broken code:

```python
tags = {}

tags.add("python")
```

The goal is to create an empty set and add `"python"`.

### Exercise 7

Fix the broken code.

Broken code:

```python
names = {"Asha", "Ben", "Cara"}

print(names[0])
```

The goal is to check whether `"Asha"` is in the set.

### Exercise 8

Fix the broken code.

Broken code:

```python
items = {"pen", "notebook"}

items.remove("charger")

print(sorted(items))
```

Use `discard()` or an `if` check so the program does not crash.

### Exercise 9

Turn this list into a set:

```python
raw_names = ["Mina", "Omar", "Mina", "Iris", "Omar"]
```

Print:

```text
Original count: 5
Unique count: 3
Unique names: ['Iris', 'Mina', 'Omar']
```

Use `sorted()` for the final line.

### Exercise 10

Choose list or set for each situation.

Situation:

```text
You need the first song in a playlist.
```

Situation:

```text
You need to know whether a username has already been used.
```

Situation:

```text
You need to keep steps in a recipe in order.
```

Situation:

```text
You need one copy of each tag on a post.
```

Write one sentence explaining each choice.

### Exercise 11

Build a small attendance checker.

Start with:

```python
present = {"Asha", "Ben", "Cara"}
```

Then:

- add `"Dev"`
- add `"Asha"` again
- print the sorted set
- print the number of present students
- check whether `"Dev"` is present

### Exercise 12

Write a short answer in your own words.

What does this sentence mean?

```text
A set is unordered.
```

Your answer should mention why this code is a mistake:

```python
tags = {"python", "practice", "sets"}

print(tags[0])
```

## Tiny Win

You can now keep one copy of each value.

That is a small idea with many uses. Programs often need to know whether something has already appeared, whether something is included, or how many different values exist.

Sets give you a clean tool for those questions.

## Tomorrow

Tomorrow you will learn:

```text
Day 40: Choosing the Right Collection
```

You have now seen several collection types:

```text
lists
tuples
sets
```

Each one has a different job.

Tomorrow you will practice choosing between them.

The short preview is:

```text
Use a list when order matters and values may change.
Use a tuple when order matters and the group should stay fixed.
Use a set when uniqueness and membership matter more than order.
```
