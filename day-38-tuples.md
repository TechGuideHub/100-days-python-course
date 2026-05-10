# Day 38: Tuples

**Focus:** Storing ordered values that usually should not change  
**You will practice:** creating tuples, reading tuple items by index, unpacking values, choosing between tuples and lists, and avoiding tuple update mistakes  
**Estimated time:** 40-50 minutes

## Today's Goal

Today you will learn about tuples.

A tuple is an ordered collection, like a list, but with a different purpose.

Lists are useful when the collection may change:

```python
tasks = ["study", "walk", "read"]
tasks.append("sleep")

print(tasks)
```

You should see:

```text
['study', 'walk', 'read', 'sleep']
```

Tuples are useful when the collection has a fixed shape:

```python
point = (4, 7)

print(point)
```

You should see:

```text
(4, 7)
```

By the end of this lesson, you should be able to:

- create a tuple
- read tuple items by index
- explain why tuples are useful for fixed pairs and simple records
- unpack a tuple into separate variables
- explain why tuple items cannot be updated directly
- choose between a list and a tuple in simple situations
- avoid common tuple mistakes

The main idea is:

> A tuple is an ordered collection that usually represents values that belong together and should not be changed item by item.

Tomorrow you will learn about sets, which are another kind of collection with a very different job.

## The Big Idea

A tuple can hold several values in one variable.

Code:

```python
coordinates = (10, 25)

print(coordinates)
```

You should see:

```text
(10, 25)
```

The parentheses help you see the tuple.

The comma separates the items.

The order matters. In this tuple:

```python
coordinates = (10, 25)
```

the first value might mean the x position, and the second value might mean the y position.

You can read tuple items by index, just like list items.

Code:

```python
coordinates = (10, 25)

print(coordinates[0])
print(coordinates[1])
```

You should see:

```text
10
25
```

Remember:

```text
Index 0 is the first item.
Index 1 is the second item.
```

Tuples can store strings:

```python
name_pair = ("Asha", "Ben")

print(name_pair)
```

You should see:

```text
('Asha', 'Ben')
```

Tuples can store numbers:

```python
screen_size = (1920, 1080)

print(screen_size)
```

You should see:

```text
(1920, 1080)
```

Tuples can store mixed values:

```python
student = ("Mina", 12, True)

print(student)
```

You should see:

```text
('Mina', 12, True)
```

That tuple could mean:

```text
name
age
is_enrolled
```

This is one reason tuples are useful. They can act like small records when each position has a clear meaning.

## The Mental Model

Think of a tuple as a small fixed row of values.

For example:

```python
point = (4, 7)
```

Read it like this:

```text
point is one value made from two smaller values.
The first value is the x position.
The second value is the y position.
The shape is meant to stay the same.
```

A list often means:

```text
Here are several items. The group may grow, shrink, or change.
```

A tuple often means:

```text
Here are a few values that belong together. Treat them as one fixed thing.
```

Compare these two examples.

Code:

```python
shopping_list = ["rice", "milk", "apples"]
home_position = (12, 4)

print(shopping_list)
print(home_position)
```

You should see:

```text
['rice', 'milk', 'apples']
(12, 4)
```

The shopping list may change:

```text
add bread
remove apples
replace milk
```

The position is usually treated as one fixed pair:

```text
x is 12
y is 4
```

If the position changes, you usually make a new tuple:

```python
position = (12, 4)
new_position = (13, 4)

print(position)
print(new_position)
```

You should see:

```text
(12, 4)
(13, 4)
```

The first tuple did not change. You created a second tuple.

That is the beginner-friendly version of immutability:

```text
You cannot update tuple items directly.
```

You can still make a new tuple and store it in the same variable name.

Code:

```python
position = (12, 4)
position = (13, 4)

print(position)
```

You should see:

```text
(13, 4)
```

This does not edit the old tuple. It points the name `position` at a new tuple.

## Try It Yourself

Create a file named:

```text
day-38/tuples_practice.py
```

Start with a coordinate pair.

Code:

```python
point = (6, 9)

print(point)
```

You should see:

```text
(6, 9)
```

Now read each item by index.

Code:

```python
point = (6, 9)

print("x:", point[0])
print("y:", point[1])
```

You should see:

```text
x: 6
y: 9
```

Now use a tuple with strings.

Code:

```python
name = ("Asha", "Rao")

print("First name:", name[0])
print("Last name:", name[1])
```

You should see:

```text
First name: Asha
Last name: Rao
```

You can also use `len()` with a tuple.

Code:

```python
colors = ("red", "green", "blue")

print("Colors:", colors)
print("Color count:", len(colors))
```

You should see:

```text
Colors: ('red', 'green', 'blue')
Color count: 3
```

You can use `in` with a tuple too.

Code:

```python
allowed_sizes = ("small", "medium", "large")

print("medium" in allowed_sizes)
print("extra large" in allowed_sizes)
```

You should see:

```text
True
False
```

Now try tuple unpacking.

Code:

```python
point = (6, 9)
x, y = point

print("x:", x)
print("y:", y)
```

You should see:

```text
x: 6
y: 9
```

This line:

```python
x, y = point
```

means:

```text
Put the first tuple item into x.
Put the second tuple item into y.
```

Unpacking is useful when each position has a clear name.

Try it with a simple record.

Code:

```python
student = ("Mina", 12, "piano")
name, age, hobby = student

print(name)
print(age)
print(hobby)
```

You should see:

```text
Mina
12
piano
```

The number of variable names must match the number of tuple items. You will see that mistake later in the lesson.

## Common Mistake

### Mistake 1: Trying To Append To A Tuple

Broken code:

```python
sizes = ("small", "medium")

sizes.append("large")

print(sizes)
```

This is broken because tuples do not have an `append()` method.

The error will say something like:

```text
AttributeError: 'tuple' object has no attribute 'append'
```

If the collection needs to grow, use a list.

Fixed code:

```python
sizes = ["small", "medium"]

sizes.append("large")

print(sizes)
```

You should see:

```text
['small', 'medium', 'large']
```

Use a tuple when the shape should stay steady.

Use a list when the collection should change over time.

### Mistake 2: Trying To Change One Tuple Item

Broken code:

```python
point = (4, 7)

point[0] = 5

print(point)
```

This is broken because you cannot replace one item inside a tuple.

The error will say something like:

```text
TypeError: 'tuple' object does not support item assignment
```

If you want a different point, make a new tuple.

Fixed code:

```python
point = (4, 7)
point = (5, 7)

print(point)
```

You should see:

```text
(5, 7)
```

The variable name can point to a new tuple. The old tuple was not edited item by item.

### Mistake 3: Forgetting The Comma In A One-Item Tuple

This looks like a tuple, but it is not:

```python
favorite = ("Python")

print(favorite)
print(type(favorite))
```

You should see:

```text
Python
<class 'str'>
```

Parentheses around one value do not create a tuple by themselves.

For a one-item tuple, the comma matters.

Fixed code:

```python
favorite = ("Python",)

print(favorite)
print(type(favorite))
```

You should see:

```text
('Python',)
<class 'tuple'>
```

The comma is the signal that this is a tuple with one item.

### Mistake 4: Unpacking Into The Wrong Number Of Variables

Broken code:

```python
student = ("Mina", 12, "piano")

name, age = student

print(name)
print(age)
```

This is broken because the tuple has three items, but the code only provides two variable names.

The error will say something like:

```text
ValueError: too many values to unpack
```

Fixed code:

```python
student = ("Mina", 12, "piano")

name, age, hobby = student

print(name)
print(age)
print(hobby)
```

You should see:

```text
Mina
12
piano
```

When unpacking, count both sides:

```text
3 tuple items
3 variable names
```

## Debug It

Here is a broken program.

Goal:

```text
Original point: (10, 20)
Moved point: (15, 20)
```

Broken code:

```python
point = (10, 20)

print("Original point:", point)

point[0] = 15

print("Moved point:", point)
```

The problem is this line:

```python
point[0] = 15
```

That kind of update works with lists, but not with tuples.

Fixed code:

```python
point = (10, 20)

print("Original point:", point)

point = (15, point[1])

print("Moved point:", point)
```

You should see:

```text
Original point: (10, 20)
Moved point: (15, 20)
```

This line creates a new tuple:

```python
point = (15, point[1])
```

Read it as:

```text
Make a new point.
Use 15 as the first item.
Reuse the old second item.
```

Here is another broken program.

Goal:

```text
Name: Asha
City: Pune
Score: 9
```

Broken code:

```python
player = ("Asha", "Pune", 9)

name, city = player

print("Name:", name)
print("City:", city)
print("Score:", score)
```

There are two problems.

First, the tuple has three items, but the code only unpacks two names:

```python
name, city = player
```

Second, the code tries to print `score`, but no variable named `score` was created.

Fixed code:

```python
player = ("Asha", "Pune", 9)

name, city, score = player

print("Name:", name)
print("City:", city)
print("Score:", score)
```

You should see:

```text
Name: Asha
City: Pune
Score: 9
```

When unpacking feels confusing, write the positions above the tuple:

```text
Index:     0       1      2
Value:  "Asha"  "Pune"   9
Name:    name    city   score
```

That little map can make the code much easier to read.

## Read the Docs

Find Python's official tutorial section about tuples:

```text
https://docs.python.org/3/tutorial/datastructures.html#tuples-and-sequences
```

You do not need to read the whole page today. Look for these ideas:

- tuples can be written as comma-separated values
- tuples are often shown with parentheses
- tuples can be unpacked into variables
- tuples are sequences, so indexing works

Documentation may show an example like this:

```python
t = 12345, 54321, "hello"
```

That is a tuple even without parentheses.

In this course, you should usually write the parentheses:

```python
t = (12345, 54321, "hello")
```

The parentheses make the code easier to recognize while you are learning.

Try this documentation-style example:

```python
record = ("Asha", 9)
name, score = record

print(name)
print(score)
```

You should see:

```text
Asha
9
```

For today, the practical reading is:

```text
A tuple can group related values, keep them in order, and unpack them into names.
```

## Mini Challenge

Create a file named:

```text
day-38/coordinate_card.py
```

Build a small coordinate display.

Start with this tuple:

```python
position = (8, 3)
```

Your program should:

- print the whole tuple
- print the x value
- print the y value
- unpack the tuple into `x` and `y`
- create a new tuple named `moved_position`
- print the moved tuple

The output should look like this:

```text
Position: (8, 3)
x: 8
y: 3
Moved position: (9, 5)
```

Start like this:

```python
position = (8, 3)

print("Position:", position)
print("x:", position[0])
print("y:", position[1])
```

Then add unpacking:

```python
x, y = position
```

Then create a new tuple:

```python
moved_position = (x + 1, y + 2)
```

Do not try this:

```python
position[0] = 9
```

That line is broken because tuple items cannot be changed directly.

## Real-World Use

Tuples are useful when a few values naturally belong together.

Examples:

- a coordinate like `(x, y)`
- a screen size like `(width, height)`
- a color value like `(red, green, blue)`
- a name pair like `(first_name, last_name)`
- a simple record like `(name, score)`
- a returned pair from a function, which you will learn later

The important part is not the parentheses. The important part is the meaning:

```text
These values travel together.
Their positions have meaning.
The group is not meant to grow with append().
```

Code:

```python
screen_size = (1920, 1080)
width, height = screen_size

print("Width:", width)
print("Height:", height)
```

You should see:

```text
Width: 1920
Height: 1080
```

This reads well because the tuple has a clear shape:

```text
first item -> width
second item -> height
```

A list would be better for a changing collection:

```python
scores = [8, 10, 7]
scores.append(9)

print(scores)
```

You should see:

```text
[8, 10, 7, 9]
```

A tuple is better for a fixed shape:

```python
score_record = ("Asha", 9)

print(score_record)
```

You should see:

```text
('Asha', 9)
```

One simple rule is:

```text
Use a list when the number of items may change.
Use a tuple when the positions have a fixed meaning.
```

## Recap

Today you learned that:

- a tuple stores several values under one name
- tuples are ordered
- tuples are usually written with parentheses
- tuple items are separated by commas
- indexing works with tuples
- `len()` works with tuples
- `in` works with tuples
- unpacking puts tuple items into separate variables
- tuple items cannot be updated directly
- tuples do not use `append()` to grow
- a one-item tuple needs a comma
- lists are better for changing collections
- tuples are better for fixed pairs, coordinates, and simple records

The basic shape is:

```python
point = (4, 7)
```

Read it as:

```text
point is one fixed pair of ordered values.
```

## Lesson Checklist

Before moving on, check that you can:

- create a tuple with two or more items
- explain why commas matter in a tuple
- read the first tuple item with index `0`
- read the second tuple item with index `1`
- use `len()` with a tuple
- use `in` with a tuple
- unpack a two-item tuple into two variables
- unpack a three-item tuple into three variables
- explain why `point[0] = 5` does not work
- explain why `items.append(value)` does not work on a tuple
- create a one-item tuple with a comma
- choose a list for changing data
- choose a tuple for a fixed pair or simple record

## Exercises

### Exercise 1

Predict the output.

```python
point = (2, 5)

print(point)
```

Then run it.

### Exercise 2

Predict the output.

```python
point = (2, 5)

print(point[0])
print(point[1])
```

Why does `point[0]` print the first value?

### Exercise 3

Create a tuple named `screen_size` with two numbers:

```python
screen_size = (1366, 768)
```

Print:

```text
Width: 1366
Height: 768
```

Use indexing.

### Exercise 4

Unpack this tuple:

```python
book = ("Python Basics", "Mina")
```

Create variables named `title` and `author`, then print both values.

### Exercise 5

Predict the output.

```python
colors = ("red", "green", "blue")

print(len(colors))
print("green" in colors)
print("yellow" in colors)
```

Then run it.

### Exercise 6

Fix the broken code.

Broken code:

```python
size = ("small", "medium")

size.append("large")

print(size)
```

The goal is to build a changing collection of sizes.

Should this be a tuple or a list?

### Exercise 7

Fix the broken code.

Broken code:

```python
point = (4, 9)

point[1] = 10

print(point)
```

The goal is to create a new point:

```text
(4, 10)
```

Do not change the tuple item directly. Make a new tuple instead.

### Exercise 8

Create a one-item tuple named `single_score` that stores the number `10`.

Print the tuple and its type.

You should see:

```text
(10,)
<class 'tuple'>
```

### Exercise 9

Predict the output.

```python
single_score = (10)

print(single_score)
print(type(single_score))
```

Why is this not a tuple?

### Exercise 10

Debug this unpacking code.

Broken code:

```python
pet = ("dog", "Riley", 4)

kind, name = pet

print(kind)
print(name)
```

Fix the unpacking so all three values have variable names.

### Exercise 11

Choose a list or a tuple for each situation.

Situation:

```text
A shopping cart that gains and removes products.
```

Situation:

```text
A map coordinate with x and y values.
```

Situation:

```text
A playlist that may add new songs.
```

Situation:

```text
A color written as red, green, and blue numbers.
```

Write `list` or `tuple` for each one, then explain your choice in one sentence.

### Exercise 12

Build a simple score record.

Start with this tuple:

```python
score_record = ("Asha", 9)
```

Unpack it into `name` and `score`.

Print:

```text
Asha scored 9
```

Then create a new tuple for an updated score:

```python
updated_record = (name, 10)
```

Print the updated tuple.

You should see:

```text
('Asha', 10)
```

## Tiny Win

You can now group values when the shape of the group matters.

That is a useful step. Lists helped you store collections that can change. Tuples give you another choice: a small ordered group where the positions have meaning and the items are not meant to be edited directly.

## Tomorrow

Tomorrow you will learn:

```text
Day 39: Sets
```

Tuples keep values in order:

```python
point = (4, 7)
```

The position matters:

```text
first item
second item
last item
```

Sets are different. A set is useful when you care about whether something is included and whether values are unique.

Tomorrow's question will be:

```text
What if order does not matter, but uniqueness does?
```
