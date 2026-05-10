# Day 40: Choosing the Right Collection

**Focus:** Choosing between lists, tuples, and sets  
**You will practice:** comparing order, changeability, uniqueness, membership checks, and explaining collection choices  
**Estimated time:** 40-50 minutes

## Today's Goal

Today you will practice choosing the right kind of collection for a job.

You have already used lists:

```python
shopping_list = ["rice", "beans", "apples"]
```

You will also see tuples and sets in many Python programs:

```python
home_coordinates = (12, 8)
unique_tags = {"python", "beginner", "practice"}
```

By the end of this lesson, you should be able to:

- choose a list when order matters and the collection may change
- choose a tuple when order matters and the collection should stay fixed
- choose a set when uniqueness matters more than order
- explain why a collection choice fits the problem
- avoid common mistakes with unordered sets and fixed tuples

The main idea is:

```text
Choose the collection that matches the job.
```

You do not need to use the fanciest collection. You need to use the one that makes your program clearer.

## The Big Idea

Lists, tuples, and sets can all hold more than one value.

The difference is what they promise.

A list promises order and changeability:

```python
tasks = ["wash cup", "pack bag", "start timer"]

tasks.append("leave house")

print(tasks)
```

You should see:

```text
['wash cup', 'pack bag', 'start timer', 'leave house']
```

A tuple promises order and a fixed shape:

```python
coordinates = (4, 9)

print(coordinates[0])
print(coordinates[1])
```

You should see:

```text
4
9
```

A set promises unique values:

```python
tags = {"python", "practice", "python", "beginner"}

print(sorted(tags))
```

You should see:

```text
['beginner', 'practice', 'python']
```

The set removed the duplicate `"python"`.

`sorted(tags)` turns the set into a sorted list for printing. That keeps the output predictable.

Here is the quick comparison:

```text
list    ordered    changeable    allows duplicates
tuple   ordered    fixed         allows duplicates
set     unordered  changeable    keeps unique values
```

Those three questions usually point you in the right direction:

```text
Does the order matter?
Will the collection change?
Should duplicates be removed?
```

## The Mental Model

Think of a list as a working checklist.

You can add to it, remove from it, and change it as the day changes.

Example:

```python
shopping_list = ["milk", "rice", "eggs"]

shopping_list.append("tea")
shopping_list.remove("rice")

print(shopping_list)
```

You should see:

```text
['milk', 'eggs', 'tea']
```

Think of a tuple as a small fixed record.

The values belong together, and their positions have meaning.

Example:

```python
screen_position = (320, 180)

x = screen_position[0]
y = screen_position[1]

print("x:", x)
print("y:", y)
```

You should see:

```text
x: 320
y: 180
```

Think of a set as a uniqueness filter.

It answers questions like "Have I seen this before?" or "What are the unique values?"

Example:

```python
selected_options = {"email", "sms", "email", "push"}

print("email" in selected_options)
print(sorted(selected_options))
```

You should see:

```text
True
['email', 'push', 'sms']
```

The set keeps one `"email"`, not two.

That is useful when duplicates would only create noise.

## Try It Yourself

Create a file named:

```text
day-40/collection_choices.py
```

You will write a few small examples that use the right collection for the job.

### Step 1: Use A List For Changing Tasks

Code:

```python
tasks = ["open notebook", "write notes", "review lesson"]

tasks.append("practice examples")
tasks[1] = "write clean notes"

print(tasks)
```

You should see:

```text
['open notebook', 'write clean notes', 'review lesson', 'practice examples']
```

This is a list because the tasks are ordered and the program changes them.

### Step 2: Use A Tuple For Coordinates

Code:

```python
button_position = (24, 80)

print("Left:", button_position[0])
print("Top:", button_position[1])
```

You should see:

```text
Left: 24
Top: 80
```

This is a tuple because the two values belong together and should not be edited like a task list.

### Step 3: Use A Set For Unique Tags

Code:

```python
tags = {"python", "practice", "python", "lists", "practice"}

print(sorted(tags))
print("python" in tags)
```

You should see:

```text
['lists', 'practice', 'python']
True
```

This is a set because each tag should appear only once.

### Step 4: Use A List For Scores When Order Matters

Code:

```python
scores = [80, 95, 80, 100]

print(scores)
print("First score:", scores[0])
print("Latest score:", scores[-1])
```

You should see:

```text
[80, 95, 80, 100]
First score: 80
Latest score: 100
```

This is a list because the order tells you when each score happened. The duplicate `80` is not a problem. It represents two real scores.

### Step 5: Use A Set For Selected Options

Code:

```python
selected_options = {"dark mode", "email alerts", "dark mode"}

if "email alerts" in selected_options:
    print("Email alerts are on.")

print(sorted(selected_options))
```

You should see:

```text
Email alerts are on.
['dark mode', 'email alerts']
```

This is a set because an option is either selected or not selected. Selecting `"dark mode"` twice does not need to create two copies.

## Common Mistake

### Mistake 1: Using A Set When Order Matters

Broken code:

```python
tasks = {"wake up", "brush teeth", "leave house"}

print(tasks[0])
```

This is broken because sets do not use positions.

A set is unordered, so Python cannot give you "the first task" by index.

Fixed code:

```python
tasks = ["wake up", "brush teeth", "leave house"]

print(tasks[0])
```

You should see:

```text
wake up
```

Use a list when the order carries meaning.

### Mistake 2: Using A Tuple For Something That Needs To Change

Broken code:

```python
shopping_list = ("milk", "rice", "eggs")

shopping_list.append("tea")

print(shopping_list)
```

This is broken because tuples do not have `append()`.

Fixed code:

```python
shopping_list = ["milk", "rice", "eggs"]

shopping_list.append("tea")

print(shopping_list)
```

You should see:

```text
['milk', 'rice', 'eggs', 'tea']
```

Use a list when the collection needs to grow, shrink, or change.

### Mistake 3: Using A Set When Duplicates Matter

Broken code:

```python
scores = {80, 95, 80, 100}

print(sorted(scores))
```

This code runs, but it loses information.

The two `80` scores become one `80`.

Fixed code:

```python
scores = [80, 95, 80, 100]

print(scores)
```

You should see:

```text
[80, 95, 80, 100]
```

Use a list when repeated values are meaningful.

### Mistake 4: Expecting Printed Sets To Stay In A Certain Order

Broken code:

```python
tags = {"urgent", "home", "python"}

print(tags)
```

The code is not a syntax error, but the output order is not something you should depend on.

Fixed code:

```python
tags = {"urgent", "home", "python"}

print(sorted(tags))
```

You should see:

```text
['home', 'python', 'urgent']
```

When you need a predictable display order, use `sorted()`.

## Debug It

Read each broken program. Decide what collection fits the job, then fix the code.

### Debug 1: The First Task

The program should print the first task.

Broken code:

```python
tasks = {"pack bag", "charge phone", "leave house"}

print(tasks[0])
```

The problem:

```text
The code uses a set, but then asks for item 0.
```

Fixed code:

```python
tasks = ["pack bag", "charge phone", "leave house"]

print(tasks[0])
```

You should see:

```text
pack bag
```

### Debug 2: Adding One More Item

The program should add `"bananas"` to a shopping collection.

Broken code:

```python
shopping = ("bread", "milk", "apples")

shopping.append("bananas")

print(shopping)
```

The problem:

```text
The code uses a tuple, but the shopping collection needs to change.
```

Fixed code:

```python
shopping = ["bread", "milk", "apples"]

shopping.append("bananas")

print(shopping)
```

You should see:

```text
['bread', 'milk', 'apples', 'bananas']
```

### Debug 3: Unique Labels

The program should show each label only once.

Broken code:

```python
labels = ["new", "sale", "new", "popular", "sale"]

print(labels)
```

The problem:

```text
The code uses a list, so duplicates are kept.
```

Fixed code:

```python
labels = {"new", "sale", "new", "popular", "sale"}

print(sorted(labels))
```

You should see:

```text
['new', 'popular', 'sale']
```

## Read the Docs

Today, look at Python's official documentation for the built-in types:

```text
https://docs.python.org/3/library/stdtypes.html
```

Search the page for these names:

```text
list
tuple
set
```

You do not need to read the whole page.

Look for these ideas:

```text
Lists are mutable sequences.
Tuples are immutable sequences.
Sets are unordered collections of distinct objects.
```

The documentation uses the word `mutable` to mean "can be changed."

It uses `immutable` to mean "cannot be changed after it is created."

That gives you a more official version of today's comparison:

```text
list    mutable sequence
tuple   immutable sequence
set     unordered collection of distinct values
```

## Mini Challenge

Build a small collection-choice program.

Create a file named:

```text
day-40/study_tracker.py
```

Start with these collections:

```python
tasks = ["read lesson", "run examples", "answer exercises"]
study_spot = ("desk", "evening")
completed_topics = {"lists", "tuples", "sets", "lists"}
```

Then write code that:

- adds `"review mistakes"` to `tasks`
- prints the first task
- prints the place from `study_spot`
- checks whether `"sets"` is in `completed_topics`
- prints the unique completed topics with `sorted()`

One possible version:

```python
tasks = ["read lesson", "run examples", "answer exercises"]
study_spot = ("desk", "evening")
completed_topics = {"lists", "tuples", "sets", "lists"}

tasks.append("review mistakes")

print("First task:", tasks[0])
print("Place:", study_spot[0])

if "sets" in completed_topics:
    print("Sets have been practiced.")

print("Topics:", sorted(completed_topics))
```

You should see:

```text
First task: read lesson
Place: desk
Sets have been practiced.
Topics: ['lists', 'sets', 'tuples']
```

## Real-World Use

Programmers choose collections all the time.

A shopping app might use a list for the cart:

```python
cart = ["rice", "tea", "notebook"]
```

The order can matter because the user added items one by one. The cart can also change.

A map program might use a tuple for coordinates:

```python
location = (17.44, 78.38)
```

The two values belong together. The first value means one thing, and the second value means another thing.

A blog or note app might use a set for tags:

```python
tags = {"python", "beginner", "practice"}
```

Tags should usually be unique. If the user adds `"python"` twice, the program probably still wants one `"python"` tag.

A game might use a list for scores:

```python
scores = [10, 20, 10, 30]
```

The duplicate `10` matters because it may represent two separate rounds.

A settings screen might use a set for selected options:

```python
selected_options = {"dark mode", "email alerts"}
```

An option is either selected or not selected. A set fits that idea well.

When you can explain the collection choice, your code becomes easier to read.

## Recap

Today you practiced choosing between lists, tuples, and sets.

Use a list when:

- order matters
- the collection may change
- duplicates might be meaningful

Use a tuple when:

- order matters
- the shape should stay fixed
- the values form a small record, like coordinates

Use a set when:

- uniqueness matters
- membership checks are important
- order does not matter

Ask these decision questions:

```text
Do I need the first, second, or last item?
Will I add, remove, or replace values?
Are duplicate values meaningful?
Do I only care whether something is included?
Should this group of values stay fixed?
```

Those questions are more useful than memorizing a rule.

## Lesson Checklist

Before moving on, check that you can:

- explain the difference between a list, tuple, and set
- choose a list for an ordered changing collection
- choose a tuple for a small fixed collection
- choose a set for unique values
- explain why sets are not used for indexing
- explain why tuples do not use `append()`
- use `sorted()` before printing a set when order matters for display
- choose a collection for shopping items, coordinates, tags, scores, tasks, and selected options
- explain your choice in one or two sentences

## Exercises

### Exercise 1

Choose a collection for a shopping list that will change during the week.

Write the collection and explain your choice.

### Exercise 2

Choose a collection for the coordinate pair:

```text
x = 10
y = 25
```

Write the collection and explain your choice.

### Exercise 3

Choose a collection for tags where duplicates should be removed:

```text
python
practice
python
beginner
```

Write the collection and print it with `sorted()`.

### Exercise 4

Choose a collection for quiz scores:

```text
8
10
8
9
```

Should the duplicate `8` stay? Explain why.

### Exercise 5

Choose a collection for selected options in a settings screen:

```text
dark mode
email alerts
dark mode
```

Print the unique selected options in sorted order.

### Exercise 6

Fix the broken code.

Broken code:

```python
chores = {"wash cup", "fold towel", "pack bag"}

print(chores[0])
```

The goal is to print the first chore.

### Exercise 7

Fix the broken code.

Broken code:

```python
coordinates = [12, 8]

coordinates.append(99)

print(coordinates)
```

The goal is to represent one fixed coordinate pair. Choose a better collection and remove the line that does not fit the goal.

### Exercise 8

Fix the broken code.

Broken code:

```python
selected = ["email", "sms", "email"]

print(selected)
```

The goal is to keep each selected option once.

### Exercise 9

For each situation, write `list`, `tuple`, or `set`.

```text
A playlist where song order matters.
A home location stored as latitude and longitude.
A group of usernames that must be unique.
A task list where items can be added and removed.
A pair of dice rolls where two matching numbers still matter.
A set of labels on a note where duplicates should disappear.
```

Then write one sentence explaining each answer.

### Exercise 10

Write a small program with three collections:

- a list named `tasks`
- a tuple named `window_size`
- a set named `unique_topics`

Your program should:

- add one task to `tasks`
- print the first task
- print both values from `window_size`
- check whether `"sets"` is in `unique_topics`
- print `unique_topics` with `sorted()`

### Exercise 11

Predict the output.

```python
numbers = {3, 1, 3, 2}

print(sorted(numbers))
print(3 in numbers)
print(4 in numbers)
```

Then run it.

### Exercise 12

Explain the best collection choice for each variable name:

```text
daily_steps
birth_date_parts
blocked_usernames
recent_scores
button_position
packed_items
```

There can be more than one reasonable answer. What matters is whether your explanation matches the job.

## Tiny Win

You can now choose a collection for a reason.

That is a practical step beyond writing correct syntax. Real programs are full of choices like this:

```text
Should this keep order?
Should this change?
Should this remove duplicates?
```

When you ask those questions, your code starts to match the real thing it represents.

## Tomorrow

Tomorrow is:

```text
Day 41: Practice Day: Collection Problems
```

Today you compared the main collection choices.

Tomorrow you will solve mixed problems where you decide what to use:

```text
lists for ordered changing data
tuples for fixed grouped data
sets for unique data
```

The goal will not be to memorize names. The goal will be to read a problem and choose a clear shape for the data.
