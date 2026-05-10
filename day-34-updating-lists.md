# Day 34: Updating Lists

**Focus:** Changing, adding, inserting, and removing list items  
**You will practice:** updating by index, using `append()`, `insert()`, `remove()`, and `pop()`, and checking before changing a list  
**Estimated time:** 40-50 minutes

## Today's Goal

Today you will learn how to change a list after it has already been created.

You have already seen that a list can hold several values in order:

```python
tasks = ["wash cup", "pack bag", "start timer"]
```

You have also seen that each item has a position, called an index.

Today you will use those positions to update the list.

By the end of this lesson, you should be able to:

- change one item by index
- add a new item to the end of a list with `append()`
- insert a new item at a chosen position with `insert()`
- remove an item by value with `remove()`
- remove an item by position with `pop()`
- check before updating or removing
- recognize common list update mistakes

The main idea is:

> A list is not frozen. You can change the values it contains while your program runs.

That makes lists useful for programs where information grows or changes over time.

## The Big Idea

A string value cannot be changed in place.

If you want a different string, you make a different string:

```python
word = "cat"
word = "hat"

print(word)
```

You should see:

```text
hat
```

A list is different. You can keep the same list and change what is inside it.

Example:

```python
groceries = ["bread", "eggs", "rice"]

groceries[1] = "milk"

print(groceries)
```

You should see:

```text
['bread', 'milk', 'rice']
```

This line changed the item at index `1`:

```python
groceries[1] = "milk"
```

Remember:

```text
Index 0 is the first item.
Index 1 is the second item.
Index 2 is the third item.
```

So this list:

```python
["bread", "eggs", "rice"]
```

has these positions:

```text
0 -> bread
1 -> eggs
2 -> rice
```

When you assign to an index that already exists, Python replaces that item.

It does not create a new list. It updates the list you already have.

## The Mental Model

Think of a list as a row of labeled spaces.

```text
Index:   0        1       2
Value: bread    eggs    rice
```

When you write:

```python
groceries[1] = "milk"
```

Python goes to space `1` and replaces the value there.

```text
Index:   0        1       2
Value: bread    milk    rice
```

The list is still named `groceries`. The list still has three items. One value changed.

There are five update actions you will use today.

Change an existing item:

```python
groceries[1] = "milk"
```

Add to the end:

```python
groceries.append("apples")
```

Insert at a position:

```python
groceries.insert(1, "tea")
```

Remove something:

```python
groceries.remove("bread")
```

Or remove by position:

```python
groceries.pop(0)
```

You do not need to memorize every list method today. A later lesson will spend more time on list methods.

For now, focus on this question:

```text
Am I changing an existing spot, adding a new spot, or removing a spot?
```

That question usually tells you which tool to use.

## Try It Yourself

Create a file named:

```text
day-34/updating_lists.py
```

Start with a short list.

Code:

```python
tasks = ["make bed", "pack lunch", "charge phone"]

print(tasks)
```

You should see:

```text
['make bed', 'pack lunch', 'charge phone']
```

### Step 1: Change One Item

Replace the second task.

Code:

```python
tasks = ["make bed", "pack lunch", "charge phone"]

tasks[1] = "fill water bottle"

print(tasks)
```

You should see:

```text
['make bed', 'fill water bottle', 'charge phone']
```

The second item is at index `1`, so this line changes it:

```python
tasks[1] = "fill water bottle"
```

### Step 2: Add To The End With `append()`

Add a new task after the existing tasks.

Code:

```python
tasks = ["make bed", "fill water bottle", "charge phone"]

tasks.append("leave house")

print(tasks)
```

You should see:

```text
['make bed', 'fill water bottle', 'charge phone', 'leave house']
```

`append()` adds one new item to the end of the list.

Read this:

```python
tasks.append("leave house")
```

as:

```text
Add "leave house" to the end of tasks.
```

### Step 3: Insert At A Position

Sometimes the new item belongs in the middle.

Code:

```python
tasks = ["make bed", "fill water bottle", "charge phone", "leave house"]

tasks.insert(1, "check calendar")

print(tasks)
```

You should see:

```text
['make bed', 'check calendar', 'fill water bottle', 'charge phone', 'leave house']
```

This line:

```python
tasks.insert(1, "check calendar")
```

means:

```text
Put "check calendar" at index 1.
Move the old index 1 item and everything after it one step to the right.
```

`insert()` does not replace the item at that index. It makes room.

### Step 4: Remove By Value

If you know the value you want to remove, use `remove()`.

Code:

```python
tasks = ["make bed", "check calendar", "fill water bottle", "charge phone", "leave house"]

tasks.remove("charge phone")

print(tasks)
```

You should see:

```text
['make bed', 'check calendar', 'fill water bottle', 'leave house']
```

`remove()` looks for the value and removes the first match.

### Step 5: Remove By Position

If you know the position you want to remove, use `pop()`.

Code:

```python
tasks = ["make bed", "check calendar", "fill water bottle", "leave house"]

finished_task = tasks.pop(0)

print("Finished:", finished_task)
print("Still left:", tasks)
```

You should see:

```text
Finished: make bed
Still left: ['check calendar', 'fill water bottle', 'leave house']
```

`pop(0)` removes the item at index `0`.

It also gives that removed value back, so you can save it:

```python
finished_task = tasks.pop(0)
```

That is useful when the program needs to know what was removed.

### Step 6: Check Before Updating

If an index might be wrong, check the list length before changing it.

Code:

```python
tasks = ["make bed", "pack lunch"]
index = 1
new_task = "fill water bottle"

if index >= 0 and index < len(tasks):
    tasks[index] = new_task
else:
    print("That index does not exist.")

print(tasks)
```

You should see:

```text
['make bed', 'fill water bottle']
```

`len(tasks)` tells you how many items are in the list.

For this list:

```python
tasks = ["make bed", "pack lunch"]
```

`len(tasks)` is `2`.

The valid indexes are:

```text
0
1
```

So this check protects the update:

```python
if index >= 0 and index < len(tasks):
```

You will not need this check every time. It is useful when the index comes from user input, another part of the program, or a calculation.

## Common Mistake

### Mistake 1: Using The Wrong Index

Broken code:

```python
colors = ["red", "green", "blue"]

colors[3] = "yellow"

print(colors)
```

This list has three items, but the indexes are `0`, `1`, and `2`.

There is no index `3` yet, so Python raises an `IndexError`.

Fixed code:

```python
colors = ["red", "green", "blue"]

colors[2] = "yellow"

print(colors)
```

You should see:

```text
['red', 'green', 'yellow']
```

If you want to add a fourth item, use `append()` instead.

Code:

```python
colors = ["red", "green", "blue"]

colors.append("yellow")

print(colors)
```

You should see:

```text
['red', 'green', 'blue', 'yellow']
```

### Mistake 2: Forgetting Quotes Around Text

Broken code:

```python
groceries = ["bread", "eggs"]

groceries.append(milk)

print(groceries)
```

Python reads `milk` as a variable name. Since no variable named `milk` exists, Python raises a `NameError`.

Fixed code:

```python
groceries = ["bread", "eggs"]

groceries.append("milk")

print(groceries)
```

You should see:

```text
['bread', 'eggs', 'milk']
```

Text values need quotes.

### Mistake 3: Removing A Value That Is Not There

Broken code:

```python
snacks = ["apple", "toast", "nuts"]

snacks.remove("banana")

print(snacks)
```

`remove()` can only remove a value that is already in the list.

Because `"banana"` is not in `snacks`, Python raises a `ValueError`.

Fixed code:

```python
snacks = ["apple", "toast", "nuts"]

if "banana" in snacks:
    snacks.remove("banana")
else:
    print("Banana is not in the snack list.")

print(snacks)
```

You should see:

```text
Banana is not in the snack list.
['apple', 'toast', 'nuts']
```

This line:

```python
if "banana" in snacks:
```

asks whether the list contains `"banana"` before trying to remove it.

That check keeps the program from crashing.

### Mistake 4: Thinking Assignment Adds A New Item

Broken code:

```python
names = ["Asha", "Ben", "Cara"]

names[3] = "Dev"

print(names)
```

This does not add `"Dev"` to the list.

Assignment by index updates an existing position. It cannot create a missing position.

Fixed code:

```python
names = ["Asha", "Ben", "Cara"]

names.append("Dev")

print(names)
```

You should see:

```text
['Asha', 'Ben', 'Cara', 'Dev']
```

Use index assignment when the spot already exists.

Use `append()` when you want a new item at the end.

Use `insert()` when you want a new item in the middle.

## Debug It

Here is a broken program.

Goal:

```text
Original: ['math', 'science', 'history']
Updated: ['math', 'computer science', 'history', 'art']
```

Broken code:

```python
subjects = ["math", "science", "history"]

subjects[1] = computer science
subjects[3] = "art"

print("Updated:", subjects)
```

There are two problems.

First, `"computer science"` is text, so it needs quotes.

Second, `subjects[3] = "art"` tries to change index `3`, but that position does not exist yet.

Fixed code:

```python
subjects = ["math", "science", "history"]

print("Original:", subjects)

subjects[1] = "computer science"
subjects.append("art")

print("Updated:", subjects)
```

You should see:

```text
Original: ['math', 'science', 'history']
Updated: ['math', 'computer science', 'history', 'art']
```

Now look at this program.

It runs, but it removes the wrong item.

Broken code:

```python
queue = ["Asha", "Ben", "Cara", "Dev"]

next_person = queue.pop(1)

print("Next:", next_person)
print("Queue:", queue)
```

You should see:

```text
Next: Ben
Queue: ['Asha', 'Cara', 'Dev']
```

If this is a line, the next person should be the first person, not the second person.

Fixed code:

```python
queue = ["Asha", "Ben", "Cara", "Dev"]

next_person = queue.pop(0)

print("Next:", next_person)
print("Queue:", queue)
```

You should see:

```text
Next: Asha
Queue: ['Ben', 'Cara', 'Dev']
```

When a list update gives the wrong result, ask:

- Did I count indexes from `0`?
- Am I replacing an existing item or adding a new one?
- Do I know the value I want to remove, or the position?
- Should I check that the item or index exists first?

## Read the Docs

Today, look up Python's official tutorial section about lists.

Find the part that introduces these four list operations:

```python
append()
insert()
remove()
pop()
```

Do not try to memorize the whole page. Read only enough to answer these questions:

- Which operation adds to the end?
- Which operation puts a value at a specific position?
- Which operation removes by value?
- Which operation removes by position and gives the removed value back?

The documentation may show method names like this:

```python
list.append(x)
list.insert(i, x)
list.remove(x)
list.pop(i)
```

The word `list` there means "some list." In your own code, you use your variable name:

```python
tasks.append("leave house")
tasks.insert(1, "check calendar")
tasks.remove("charge phone")
tasks.pop(0)
```

Documentation often uses short names like `x` and `i`.

For today, read them as:

```text
x means the value.
i means the index.
```

That is enough.

## Mini Challenge

Create a file named:

```text
day-34/playlist_update.py
```

Build a small playlist updater.

Start with this list:

```python
songs = ["Morning Light", "Small Steps", "Old Tune"]
```

Your program should:

- print the original playlist
- replace `"Old Tune"` with `"New Song"`
- add `"Evening Walk"` to the end
- insert `"Coffee Break"` at index `1`
- remove `"Small Steps"`
- pop the first song and save it in a variable named `played_song`
- print the played song
- print the final playlist

One possible result:

```text
Original: ['Morning Light', 'Small Steps', 'Old Tune']
Played: Morning Light
Final: ['Coffee Break', 'New Song', 'Evening Walk']
```

Write the program slowly.

After each update, you may print the list to check what changed:

```python
print(songs)
```

Those check prints are useful while learning. You can remove them when the program works.

## Real-World Use

Programs update lists whenever they keep track of changing information.

Examples:

- a shopping app adds an item to a cart
- a task app marks a task by changing its text
- a playlist app removes a song from the queue
- a sign-up form inserts a new name into a waiting list
- a quiz program removes questions that have already been asked
- a game adds collected items to an inventory

The important idea is that a list can represent a small changing collection.

That collection may start with a few items:

```python
cart = ["notebook", "pen"]
```

Then the program can update it as things happen:

```python
cart.append("folder")
cart.remove("pen")

print(cart)
```

You should see:

```text
['notebook', 'folder']
```

Later, you will combine list updates with loops. That is when lists start to feel much more practical.

## Recap

Today you learned how to update lists.

You practiced:

- replacing an existing item with index assignment
- adding to the end with `append()`
- inserting at a specific position with `insert()`
- removing by value with `remove()`
- removing by position with `pop()`
- saving the value returned by `pop()`
- checking the index before changing an item
- checking with `in` before using `remove()`
- choosing the right update for the job

The key difference is:

```text
list[index] = value changes an existing item.
append(value) adds to the end.
insert(index, value) adds at a position.
remove(value) removes by value.
pop(index) removes by position.
```

When you are not sure what to use, ask:

```text
Do I have a position or a value?
Am I adding, replacing, or removing?
```

## Lesson Checklist

Before moving on, check that you can:

- explain why the first list index is `0`
- replace the second item in a list
- add one item to the end of a list
- insert one item near the beginning of a list
- remove an item by its value
- remove an item by its index
- save the item returned by `pop()`
- explain why `names[3] = "Dev"` does not work on a three-item list
- use `len()` to check whether a positive index exists
- check whether a value is in a list before removing it
- read simple documentation examples that use `x` and `i`

## Exercises

### Exercise 1

Predict the output.

```python
animals = ["cat", "dog", "rabbit"]

animals[0] = "hamster"

print(animals)
```

Then run it.

### Exercise 2

Add `"orange"` to the end of this list:

```python
fruits = ["apple", "banana"]
```

Print the list after the update.

### Exercise 3

Insert `"toast"` between `"tea"` and `"fruit"`.

Start with:

```python
breakfast = ["tea", "fruit"]
```

The final list should be:

```text
['tea', 'toast', 'fruit']
```

### Exercise 4

Remove `"dust desk"` from this list:

```python
chores = ["wash cup", "dust desk", "take out trash"]
```

Print the list after the update.

### Exercise 5

Use `pop()` to remove the last item from this list:

```python
steps = ["open laptop", "write code", "shut down"]
```

Save the removed value in a variable named `last_step`.

Print:

```text
Removed: shut down
```

Then print the updated list.

### Exercise 6

Fix the broken code.

Broken code:

```python
colors = ["red", "blue"]

colors[2] = "green"

print(colors)
```

The goal is to add `"green"` as a new third item.

### Exercise 7

Fix the broken code.

Broken code:

```python
foods = ["rice", "soup"]

foods.append(noodles)

print(foods)
```

The goal is:

```text
['rice', 'soup', 'noodles']
```

### Exercise 8

Fix the broken code.

Broken code:

```python
books = ["poems", "stories", "notes"]

books.remove("novel")

print(books)
```

Add a check so the program only removes `"novel"` if it is in the list.

### Exercise 9

Write a small packing list program.

Start with:

```python
packing = ["shirt", "socks"]
```

Then:

- append `"charger"`
- insert `"passport"` at index `0`
- replace `"socks"` with `"warm socks"`
- remove `"shirt"`
- print the final list

### Exercise 10

Predict each list after the update.

```python
numbers = [10, 20, 30]
numbers[1] = 25
```

```python
numbers = [10, 20, 30]
numbers.append(40)
```

```python
numbers = [10, 20, 30]
numbers.insert(1, 15)
```

```python
numbers = [10, 20, 30]
removed = numbers.pop(2)
```

Check your predictions by printing `numbers` after each one.

### Exercise 11

Write a safe removal.

Start with:

```python
guests = ["Asha", "Ben", "Cara"]
```

If `"Dev"` is in the list, remove it.

Otherwise, print:

```text
Dev is not on the guest list.
```

Then print the guest list.

### Exercise 12

Choose the right update tool for each situation.

Situation:

```text
Change the first score from 8 to 10.
```

Situation:

```text
Add a new message to the end of an inbox.
```

Situation:

```text
Put an urgent task at the beginning of a task list.
```

Situation:

```text
Remove "done" from a list of labels.
```

Situation:

```text
Take the first person out of a line and save their name.
```

Write the Python operation you would use for each one.

## Tiny Win

You can now make a list change while the program is running.

That is a practical step. A program can keep a task list, playlist, cart, queue, or set of choices and update it one action at a time.

The list is no longer just something you read. It is something your program can maintain.

## Tomorrow

Tomorrow you will loop through lists.

Today, you changed one item at a time:

```python
tasks[0] = "make bed"
tasks.append("leave house")
```

Tomorrow, you will use loops to visit every item in a list:

```python
for task in tasks:
    print(task)
```

That will let you print, search, count, and process list items without writing one line for each position.
