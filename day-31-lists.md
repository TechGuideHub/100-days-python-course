# Day 31: Lists

**Focus:** Storing several related values in one ordered collection  
**You will practice:** creating lists, printing lists, storing different value types, using empty lists, checking length with `len()`, and checking membership with `in`  
**Estimated time:** 40-50 minutes

## Today's Goal

Today you will learn how to store more than one value in a single variable.

So far, many variables have held one value:

```python
name = "Asha"
score = 9
is_ready = True
```

A list lets one variable hold a group of values:

```python
names = ["Asha", "Ben", "Cara"]
scores = [9, 7, 10]
ready_checks = [True, False, True]
```

By the end of this lesson, you should be able to:

- explain what a list is
- create a list with square brackets
- print a whole list
- store strings, numbers, and booleans in lists
- create an empty list
- use `len()` to count the items in a list
- use `in` to check whether a value is in a list
- avoid a few common list mistakes

The main idea is:

> A list is an ordered collection of values.

Today you will work with whole lists. Tomorrow you will learn how to get one specific item from a list.

## The Big Idea

A program often needs to remember more than one thing.

Example:

```text
three chores
five quiz scores
a few grocery items
a list of usernames
several true-or-false answers
```

Without lists, you might write separate variables:

```python
task_1 = "wash cup"
task_2 = "open notebook"
task_3 = "start timer"
```

That works for a tiny example, but it does not scale well. The tasks belong together, so Python gives you a way to keep them together.

Code:

```python
tasks = ["wash cup", "open notebook", "start timer"]

print(tasks)
```

You should see:

```text
['wash cup', 'open notebook', 'start timer']
```

The square brackets show that the value is a list.

The commas separate the items.

The order matters. This list starts with `"wash cup"`, then `"open notebook"`, then `"start timer"`.

Lists can store strings:

```python
names = ["Asha", "Ben", "Cara"]

print(names)
```

You should see:

```text
['Asha', 'Ben', 'Cara']
```

Lists can store numbers:

```python
scores = [8, 10, 7]

print(scores)
```

You should see:

```text
[8, 10, 7]
```

Lists can store booleans:

```python
checks = [True, False, True]

print(checks)
```

You should see:

```text
[True, False, True]
```

You can also create an empty list:

```python
messages = []

print(messages)
```

You should see:

```text
[]
```

An empty list is still a list. It just has no items yet.

## The Mental Model

Think of a list as a row of values kept under one name.

This code:

```python
groceries = ["milk", "rice", "apples"]
```

means:

```text
groceries is the name for the whole collection.
"milk", "rice", and "apples" are the items inside it.
The items stay in order.
```

The list is not three separate variables. It is one collection.

That matters because you can ask questions about the whole collection.

How many items are in it?

Code:

```python
groceries = ["milk", "rice", "apples"]

print(len(groceries))
```

You should see:

```text
3
```

Is a value in it?

Code:

```python
groceries = ["milk", "rice", "apples"]

print("rice" in groceries)
print("bread" in groceries)
```

You should see:

```text
True
False
```

`len(groceries)` counts the items in the list.

`"rice" in groceries` checks whether `"rice"` is one of the items in the list.

You can use `in` inside an `if` statement too.

Code:

```python
supplies = ["notebook", "pencil", "charger"]

if "charger" in supplies:
    print("Charger packed.")
else:
    print("Pack the charger.")
```

You should see:

```text
Charger packed.
```

This is one reason lists matter. They let programs ask useful questions about a group:

```text
How many are there?
Is this item included?
What should I do if it is missing?
```

Tomorrow you will ask a different kind of question:

```text
Which item is first?
Which item is second?
Which item is last?
```

That is indexing. Today, stay with the whole list.

## Try It Yourself

Create a file named:

```text
day-31/lists_practice.py
```

Start with a list of strings.

Code:

```python
snacks = ["fruit", "toast", "nuts"]

print(snacks)
```

You should see:

```text
['fruit', 'toast', 'nuts']
```

Now add a list of numbers.

Code:

```python
scores = [8, 10, 7]

print(scores)
```

You should see:

```text
[8, 10, 7]
```

Now add a list of booleans.

Code:

```python
completed = [True, False, True]

print(completed)
```

You should see:

```text
[True, False, True]
```

Create an empty list.

Code:

```python
future_tasks = []

print(future_tasks)
print("Future task count:", len(future_tasks))
```

You should see:

```text
[]
Future task count: 0
```

Now count a list that already has items.

Code:

```python
chores = ["make bed", "wash plate", "pack bag"]

print("Chores:", chores)
print("Chore count:", len(chores))
```

You should see:

```text
Chores: ['make bed', 'wash plate', 'pack bag']
Chore count: 3
```

Finally, check whether values are in a list.

Code:

```python
supplies = ["notebook", "pencil", "charger"]

print("notebook" in supplies)
print("water bottle" in supplies)
```

You should see:

```text
True
False
```

Now make the output friendlier.

Code:

```python
supplies = ["notebook", "pencil", "charger"]

if "water bottle" in supplies:
    print("Water bottle packed.")
else:
    print("Water bottle missing.")
```

You should see:

```text
Water bottle missing.
```

Change the list so it includes `"water bottle"`, then run the program again.

The condition should change because the list changed.

## Common Mistake

### Mistake 1: Forgetting commas between strings

Broken code:

```python
colors = ["red" "green" "blue"]

print(colors)
print(len(colors))
```

You should see:

```text
['redgreenblue']
1
```

This is legal Python, but it is not the list you meant. Python joined the string pieces into one string because there were no commas.

Fixed code:

```python
colors = ["red", "green", "blue"]

print(colors)
print(len(colors))
```

You should see:

```text
['red', 'green', 'blue']
3
```

Use commas to separate list items.

### Mistake 2: Forgetting quotes around strings

Broken code:

```python
names = [Asha, Ben, Cara]

print(names)
```

Python reads `Asha`, `Ben`, and `Cara` as variable names. Those variables do not exist, so the program crashes.

Fixed code:

```python
names = ["Asha", "Ben", "Cara"]

print(names)
```

You should see:

```text
['Asha', 'Ben', 'Cara']
```

Strings still need quotes inside a list.

### Mistake 3: Putting the variable name in quotes with `len()`

Broken code:

```python
tasks = ["wash cup", "open notebook", "start timer"]

print(len("tasks"))
```

You should see:

```text
5
```

That counts the letters in the string `"tasks"`.

Fixed code:

```python
tasks = ["wash cup", "open notebook", "start timer"]

print(len(tasks))
```

You should see:

```text
3
```

When you want the variable's value, do not put the variable name in quotes.

### Mistake 4: Checking for a value with different spelling or capitalization

This code runs, but the answer may surprise you.

Code:

```python
names = ["Asha", "Ben", "Cara"]

print("asha" in names)
```

You should see:

```text
False
```

`"asha"` and `"Asha"` are different strings.

Fixed code:

```python
names = ["Asha", "Ben", "Cara"]

print("Asha" in names)
```

You should see:

```text
True
```

Membership checks are exact.

### Mistake 5: Thinking an empty list is a mistake

This is fine:

```python
new_messages = []

print(new_messages)
print(len(new_messages))
```

You should see:

```text
[]
0
```

An empty list is useful when a program has nothing to store yet.

Later, you will learn how to add items to a list. For today, just know that `[]` means a real list with zero items.

## Debug It

Here is a broken program.

Goal:

```text
Supplies: ['notebook', 'pencil', 'charger']
Supply count: 3
Pencil packed: True
```

Broken code:

```python
supplies = ["notebook" "pencil", "charger"]

print("Supplies:", supplies)
print("Supply count:", len("supplies"))
print("Pencil packed:", "pencil" in supplies)
```

There are two bugs.

The first bug is here:

```python
["notebook" "pencil", "charger"]
```

There should be a comma between `"notebook"` and `"pencil"`.

Without the comma, Python makes one string:

```text
"notebookpencil"
```

The second bug is here:

```python
len("supplies")
```

That counts the letters in the string `"supplies"`, not the items in the list.

Fixed code:

```python
supplies = ["notebook", "pencil", "charger"]

print("Supplies:", supplies)
print("Supply count:", len(supplies))
print("Pencil packed:", "pencil" in supplies)
```

You should see:

```text
Supplies: ['notebook', 'pencil', 'charger']
Supply count: 3
Pencil packed: True
```

When a list looks too short, check the commas.

When `len()` gives a strange answer, check whether you accidentally put quotes around the variable name.

Here is another broken program.

It is supposed to check whether the score `10` is in the list.

Broken code:

```python
scores = ["8", "10", "7"]

print(10 in scores)
```

You should see:

```text
False
```

The list stores strings, not numbers. `"10"` and `10` are different values.

Fixed code:

```python
scores = [8, 10, 7]

print(10 in scores)
```

You should see:

```text
True
```

Another fixed version is to check for the string:

```python
scores = ["8", "10", "7"]

print("10" in scores)
```

You should see:

```text
True
```

Both versions are valid. The important habit is to keep the value you search for the same kind of value that the list stores.

## Read the Docs

Find Python's official tutorial section about lists:

```text
https://docs.python.org/3/tutorial/introduction.html#lists
```

You do not need to understand the whole page today. Documentation often shows several ideas at once.

For today, look for these parts:

```text
lists use square brackets
items are separated by commas
lists keep items in order
len() can count list items
```

The documentation also shows indexing and slicing. You can skim those examples, but do not worry about them yet.

Indexing is tomorrow's lesson.

Try this small documentation-style example:

```python
letters = ["a", "b", "c"]

print(letters)
print(len(letters))
```

You should see:

```text
['a', 'b', 'c']
3
```

The practical reading for today is:

```text
A list is a sequence of values written with square brackets.
```

## Mini Challenge

Create a file named:

```text
day-31/backpack_check.py
```

Build a small backpack checker.

Start with this list:

```python
packed_items = ["notebook", "pencil", "charger"]
```

Your program should:

- print the whole list
- print how many items are packed
- check whether `"notebook"` is packed
- check whether `"water bottle"` is packed
- print a friendly message for each check

Start like this:

```python
packed_items = ["notebook", "pencil", "charger"]

print("Packed items:", packed_items)
print("Item count:", len(packed_items))
```

Then add this:

```python
packed_items = ["notebook", "pencil", "charger"]

if "notebook" in packed_items:
    print("Notebook packed.")
else:
    print("Notebook missing.")
```

Write a second `if` statement for `"water bottle"`.

The first run should report that the water bottle is missing.

Then change the list by hand:

```python
packed_items = ["notebook", "pencil", "charger", "water bottle"]
```

Run the program again.

The message should change because the list now contains `"water bottle"`.

## Real-World Use

Lists show up whenever a program needs to keep related values together.

Examples:

- a shopping cart keeps product names
- a quiz keeps possible answers
- a music app keeps songs in a playlist
- a weather program keeps daily temperatures
- a game keeps player scores
- a website keeps unread notifications
- a classroom program keeps student names

The order can matter:

```text
playlist order
steps in a recipe
tasks for the morning
scores from several rounds
```

The length can matter:

```text
How many items are in the cart?
How many messages are unread?
How many tasks are left?
```

Membership can matter:

```text
Is this username already taken?
Is this item packed?
Is this answer one of the allowed choices?
```

Even before you know every list tool, you can already write useful code with three ideas:

```text
make the list
count the list
check whether something is in the list
```

## Recap

Today you learned that:

- a list stores several values under one name
- lists are written with square brackets
- list items are separated by commas
- lists keep values in order
- a list can store strings, numbers, or booleans
- an empty list is written as `[]`
- `print()` can show a whole list
- `len()` counts how many items are in a list
- `in` checks whether a value is in a list
- membership checks must match spelling, capitalization, and value type

The basic shape is:

```python
items = ["first", "second", "third"]
```

Read it as:

```text
items is one variable that holds an ordered collection.
```

## Lesson Checklist

Before moving on, check that you can:

- create a list of strings
- create a list of numbers
- create a list of booleans
- create an empty list
- explain why commas matter in a list
- print a whole list
- use `len()` with a list variable
- use `in` to check for a value
- use `in` inside an `if` statement
- explain why `"10"` and `10` are different values
- explain why `"asha"` and `"Asha"` do not match

## Exercises

### Exercise 1

Predict the output.

```python
colors = ["red", "green", "blue"]

print(colors)
```

Then run it.

### Exercise 2

Predict the output.

```python
colors = ["red", "green", "blue"]

print(len(colors))
```

Why is the answer `3`?

### Exercise 3

Create a list named `favorite_foods` with three foods.

Print the whole list.

### Exercise 4

Create a list named `lucky_numbers` with four numbers.

Print the whole list, then print its length.

### Exercise 5

Create a list named `daily_checks` with three boolean values.

Use only:

```python
True
False
```

Print the list.

### Exercise 6

Create an empty list named `ideas`.

Print the list, then print its length.

You should see the length `0`.

### Exercise 7

Predict the output.

```python
animals = ["cat", "dog", "rabbit"]

print("dog" in animals)
print("bird" in animals)
```

Then run it.

### Exercise 8

Use an `if` statement with `in`.

Start with:

```python
tools = ["pen", "notebook", "lamp"]
```

If `"notebook"` is in `tools`, print:

```text
Ready to study.
```

Otherwise, print:

```text
Find the notebook.
```

### Exercise 9

Debug this program.

It should print a list with three items and a length of `3`.

Broken code:

```python
animals = ["cat" "dog", "rabbit"]

print(animals)
print(len(animals))
```

What comma is missing?

### Exercise 10

Debug this program.

It should count the items in the list, not the letters in the word `"players"`.

Broken code:

```python
players = ["Maya", "Noah", "Iris"]

print(len("players"))
```

Fix one line.

### Exercise 11

Predict the output.

```python
scores = ["8", "10", "7"]

print(10 in scores)
print("10" in scores)
```

Why are the answers different?

### Exercise 12

Build a simple allowed-choice checker.

Start with:

```python
choices = ["start", "help", "quit"]
user_choice = "help"
```

Use `in` to print:

```text
Choice allowed.
```

or:

```text
Unknown choice.
```

Then change `user_choice` to:

```python
user_choice = "pause"
```

Run it again.

## Tiny Win

You can now keep related values together under one name.

That is a big practical step. Programs rarely work with only one value at a time. Lists let your code hold a group, count it, print it, and ask whether something is included.

## Tomorrow

Tomorrow you will learn:

```text
Day 32: Indexing
```

Today you treated a list as one whole collection.

Tomorrow you will learn how to pick out one item from a list:

```text
the first item
the second item
the last item
```

That will make lists feel much more useful, but the foundation is already here:

```text
square brackets
commas
order
length
membership
```
