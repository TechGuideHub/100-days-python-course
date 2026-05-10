# Day 36: List Methods

**Focus:** Using common list methods to add, remove, rearrange, and reset list items  
**You will practice:** `append()`, `insert()`, `remove()`, `pop()`, `sort()`, `reverse()`, `clear()`, safe removal, and reading method calls carefully  
**Estimated time:** 40-50 minutes

## Today's Goal

Today you will learn several common actions that lists can do.

You have already seen that a list can store several values:

```python
tasks = ["wash cup", "pack bag", "charge phone"]
```

You have also seen that a list can be changed after it is created.

Today you will give lists clearer instructions by using list methods.

By the end of this lesson, you should be able to:

- add an item to the end of a list with `append()`
- insert an item at a specific index with `insert()`
- remove an item by value with `remove()`
- remove an item by index with `pop()`
- save the value removed by `pop()`
- sort a list with `sort()`
- reverse a list with `reverse()`
- empty a list with `clear()`
- explain that most list methods change the list in place
- avoid common method mistakes

The main idea is:

```text
A list method is an action that belongs to a list.
```

When you write:

```python
tasks.append("leave house")
```

read it as:

```text
Ask the tasks list to append "leave house".
```

The list does the action.

## The Big Idea

You have used functions before.

Example:

```python
names = ["Asha", "Ben", "Cara"]

print(len(names))
```

You should see:

```text
3
```

`len()` is a function. The list goes inside the parentheses.

A method looks different:

```python
names.append("Dev")

print(names)
```

You should see:

```text
['Asha', 'Ben', 'Cara', 'Dev']
```

The method is attached to the list with a dot:

```python
names.append("Dev")
```

This has three parts:

```text
names     the list
.         the dot that connects the list to the method
append()  the action
```

Some methods need information inside the parentheses.

`append()` needs the value to add:

```python
names.append("Dev")
```

`insert()` needs an index and a value:

```python
names.insert(1, "Mina")
```

Some methods do not need extra information.

`reverse()` can reverse the whole list without being told a value:

```python
names.reverse()
```

The parentheses still matter.

They are what make the method run.

## The Mental Model

Think of a list as a small collection that can respond to commands.

Here is a list:

```python
scores = [70, 85, 100]
```

The list has values:

```text
70
85
100
```

The list also has actions it knows how to perform:

```text
append    add to the end
insert    add at an index
remove    remove by value
pop       remove by index and give the removed value back
sort      arrange from low to high or A to Z
reverse   flip the current order
clear     remove everything
```

Most list methods change the list itself.

Code:

```python
scores = [70, 85, 100]

scores.append(95)

print(scores)
```

You should see:

```text
[70, 85, 100, 95]
```

The list named `scores` changed.

Python did not create a second list for you.

That is called changing the list in place.

Here is another example:

```python
numbers = [3, 1, 2]

numbers.sort()

print(numbers)
```

You should see:

```text
[1, 2, 3]
```

The same list was rearranged.

This is different from creating a new value.

Code:

```python
numbers = [3, 1, 2]

sorted_numbers = sorted(numbers)

print("Original:", numbers)
print("Sorted:", sorted_numbers)
```

You should see:

```text
Original: [3, 1, 2]
Sorted: [1, 2, 3]
```

`sorted()` is a function. It creates a new sorted list.

`sort()` is a method. It changes the list in place.

For now, remember this simple difference:

```text
numbers.sort() changes numbers.
sorted(numbers) gives you a new sorted list.
```

## Try It Yourself

Create a file named:

```text
day-36/list_methods.py
```

Start with this list:

```python
tasks = ["pack bag", "charge phone", "wash cup"]

print(tasks)
```

You should see:

```text
['pack bag', 'charge phone', 'wash cup']
```

### Step 1: Add To The End With `append()`

Use `append()` when a new item belongs at the end.

Code:

```python
tasks = ["pack bag", "charge phone", "wash cup"]

tasks.append("leave house")

print(tasks)
```

You should see:

```text
['pack bag', 'charge phone', 'wash cup', 'leave house']
```

Read this line:

```python
tasks.append("leave house")
```

as:

```text
Add "leave house" to the end of tasks.
```

### Step 2: Insert At An Index With `insert()`

Use `insert()` when the new item belongs at a specific position.

Code:

```python
tasks = ["pack bag", "charge phone", "wash cup", "leave house"]

tasks.insert(0, "check calendar")

print(tasks)
```

You should see:

```text
['check calendar', 'pack bag', 'charge phone', 'wash cup', 'leave house']
```

`insert(0, "check calendar")` puts the new item at index `0`.

The old items move one step to the right.

`insert()` does not replace the item at that index.

It makes room.

### Step 3: Remove By Value With `remove()`

Use `remove()` when you know the value you want to remove.

Code:

```python
tasks = ["check calendar", "pack bag", "charge phone", "wash cup", "leave house"]

tasks.remove("wash cup")

print(tasks)
```

You should see:

```text
['check calendar', 'pack bag', 'charge phone', 'leave house']
```

`remove()` searches for the value and removes the first match.

That means this line:

```python
tasks.remove("wash cup")
```

does not mean "remove index 3."

It means find the value `"wash cup"` and remove it.

### Step 4: Remove By Index With `pop()`

Use `pop()` when you know the position you want to remove.

Code:

```python
tasks = ["check calendar", "pack bag", "charge phone", "leave house"]

next_task = tasks.pop(0)

print("Next:", next_task)
print("Later:", tasks)
```

You should see:

```text
Next: check calendar
Later: ['pack bag', 'charge phone', 'leave house']
```

`pop(0)` removes the item at index `0`.

It also gives the removed item back.

That is why you can save it:

```python
next_task = tasks.pop(0)
```

If you call `pop()` without an index, it removes the last item.

Code:

```python
tasks = ["pack bag", "charge phone", "leave house"]

last_task = tasks.pop()

print("Removed:", last_task)
print("Still left:", tasks)
```

You should see:

```text
Removed: leave house
Still left: ['pack bag', 'charge phone']
```

### Step 5: Sort A List With `sort()`

Use `sort()` to arrange the list.

Code:

```python
names = ["Cara", "Asha", "Ben"]

names.sort()

print(names)
```

You should see:

```text
['Asha', 'Ben', 'Cara']
```

For strings, `sort()` arranges values alphabetically.

For numbers, it arranges them from low to high.

Code:

```python
scores = [40, 100, 75, 60]

scores.sort()

print(scores)
```

You should see:

```text
[40, 60, 75, 100]
```

`sort()` changes the list in place.

Do the sorting first.

Then print the list.

### Step 6: Reverse The Current Order With `reverse()`

Use `reverse()` to flip the current order of a list.

Code:

```python
steps = ["wake up", "brush teeth", "make tea"]

steps.reverse()

print(steps)
```

You should see:

```text
['make tea', 'brush teeth', 'wake up']
```

`reverse()` does not sort.

It only flips whatever order the list already has.

Code:

```python
numbers = [10, 5, 20]

numbers.reverse()

print(numbers)
```

You should see:

```text
[20, 5, 10]
```

The list did not become `[20, 10, 5]`.

It simply flipped from front to back.

### Step 7: Empty A List With `clear()`

Use `clear()` when you want to keep the list variable, but remove all its items.

Code:

```python
cart = ["notebook", "pen", "folder"]

cart.clear()

print(cart)
```

You should see:

```text
[]
```

An empty list is still a list.

It just has no items right now.

## Common Mistake

### Mistake 1: Forgetting The Parentheses

Broken code:

```python
tasks = ["stretch", "drink water"]

tasks.append

print(tasks)
```

This code runs, but it does not add anything.

`tasks.append` only points to the method.

It does not call the method.

Fixed code:

```python
tasks = ["stretch", "drink water"]

tasks.append("start work")

print(tasks)
```

You should see:

```text
['stretch', 'drink water', 'start work']
```

The parentheses make the action happen.

### Mistake 2: Removing A Value That Is Not There

Broken code:

```python
guests = ["Asha", "Ben", "Cara"]

guests.remove("Dev")

print(guests)
```

`remove()` can only remove a value that is already in the list.

Because `"Dev"` is not in `guests`, Python raises a `ValueError`.

Fixed code:

```python
guests = ["Asha", "Ben", "Cara"]

if "Dev" in guests:
    guests.remove("Dev")
else:
    print("Dev is not on the guest list.")

print(guests)
```

You should see:

```text
Dev is not on the guest list.
['Asha', 'Ben', 'Cara']
```

Checking with `in` before `remove()` is a good safety habit.

### Mistake 3: Expecting `sort()` To Print The Sorted List Directly

Broken code:

```python
scores = [80, 100, 70]

print(scores.sort())
```

You might expect this to print the sorted list.

Instead, you should see:

```text
None
```

`sort()` changes the list in place.

It does not hand back a new sorted list for `print()` to show.

Fixed code:

```python
scores = [80, 100, 70]

scores.sort()

print(scores)
```

You should see:

```text
[70, 80, 100]
```

If you want a new sorted list, use `sorted()`:

```python
scores = [80, 100, 70]

sorted_scores = sorted(scores)

print(sorted_scores)
print(scores)
```

You should see:

```text
[70, 80, 100]
[80, 100, 70]
```

### Mistake 4: Confusing Index And Value

Broken code:

```python
foods = ["rice", "soup", "fruit"]

foods.remove(1)

print(foods)
```

This code tries to remove the value `1`.

It does not remove the item at index `1`.

Because the list does not contain the value `1`, Python raises a `ValueError`.

If you want to remove the value `"soup"`, use `remove()`:

```python
foods = ["rice", "soup", "fruit"]

foods.remove("soup")

print(foods)
```

You should see:

```text
['rice', 'fruit']
```

If you want to remove the item at index `1`, use `pop()`:

```python
foods = ["rice", "soup", "fruit"]

removed_food = foods.pop(1)

print("Removed:", removed_food)
print(foods)
```

You should see:

```text
Removed: soup
['rice', 'fruit']
```

Ask this question when you choose:

```text
Do I have the value, or do I have the index?
```

## Debug It

Here is a broken program.

Goal:

```text
Done: buy milk
Tasks: ['call doctor', 'pack bag', 'pay bill', 'wash cup']
```

Broken code:

```python
tasks = ["wash cup", "buy milk", "pack bag"]

tasks.append
tasks.insert("call doctor", 1)
done_task = tasks.remove("buy milk")
tasks.sort

print("Done:", done_task)
print("Tasks:", tasks)
```

There are four problems.

First, `tasks.append` is missing parentheses and the value to add.

Second, `insert()` needs the index first and the value second.

Third, `remove()` removes a value, but it does not give that value back. If you need to save the removed value, use `pop()`.

Fourth, `tasks.sort` is missing parentheses, so the list is not sorted.

Fixed code:

```python
tasks = ["wash cup", "buy milk", "pack bag"]

tasks.append("pay bill")
tasks.insert(1, "call doctor")
done_task = tasks.pop(2)
tasks.sort()

print("Done:", done_task)
print("Tasks:", tasks)
```

You should see:

```text
Done: buy milk
Tasks: ['call doctor', 'pack bag', 'pay bill', 'wash cup']
```

Why does `pop(2)` remove `"buy milk"`?

After the insert, the list looks like this:

```text
Index 0: wash cup
Index 1: call doctor
Index 2: buy milk
Index 3: pack bag
Index 4: pay bill
```

So index `2` is the task we want to save as done.

When a list method gives a surprising result, slow down and ask:

- Did I include the parentheses?
- Did I put the arguments in the right order?
- Am I using a value or an index?
- Does this method give a value back, or does it only change the list?
- Did I print the list after changing it?

## Read the Docs

Today, look up Python's official tutorial section about list methods:

```text
https://docs.python.org/3/tutorial/datastructures.html#more-on-lists
```

Do not try to memorize the whole page.

Look for these method shapes:

```python
list.append(x)
list.insert(i, x)
list.remove(x)
list.pop([i])
list.sort()
list.reverse()
list.clear()
```

The word `list` means "some list."

In your own code, you use your list variable name:

```python
items.append("new item")
items.insert(0, "first item")
items.remove("old item")
items.pop(0)
items.sort()
items.reverse()
items.clear()
```

Documentation often uses short names:

```text
x means the value.
i means the index.
```

The docs show `pop([i])`.

Those square brackets do not mean you should type square brackets.

They mean the index is optional.

Both of these are valid:

```python
items.pop()
items.pop(0)
```

For today, read the docs with these questions:

- Which methods add items?
- Which methods remove items?
- Which methods rearrange the list?
- Which method removes everything?
- Which method gives a removed value back?

That is enough.

## Mini Challenge

Create a file named:

```text
day-36/playlist_methods.py
```

Build a small playlist manager.

Start with this list:

```python
songs = ["Lemon Sky", "River Road", "Old Tune"]
```

Your program should:

- print the original playlist
- append `"Night Walk"`
- insert `"First Light"` at index `0`
- remove `"Old Tune"`
- pop the last song and save it in a variable named `up_next`
- sort the remaining playlist
- reverse the remaining playlist
- print the song that is up next
- print the final playlist

One possible result:

```text
Original: ['Lemon Sky', 'River Road', 'Old Tune']
Up next: Night Walk
Final: ['River Road', 'Lemon Sky', 'First Light']
```

Write one method call at a time.

After each method call, you can print the list to see what changed:

```python
print(songs)
```

Those check prints help while you are learning.

When the program works, you can remove the extra check prints and keep only the final output.

## Real-World Use

List methods are useful when a program keeps track of changing information.

Examples:

- a shopping cart app uses `append()` when a customer adds an item
- a reminder app uses `insert()` for an urgent task
- a playlist app uses `remove()` when a song is deleted
- a line or queue uses `pop(0)` to take the next person
- a score program uses `sort()` to arrange scores
- a photo gallery uses `reverse()` to show newest items first
- a form can use `clear()` to reset temporary choices

These examples all have the same shape:

```text
Start with a collection.
Something happens.
Change the collection.
```

Code:

```python
cart = ["notebook", "pen"]

cart.append("folder")
cart.remove("pen")
cart.sort()

print(cart)
```

You should see:

```text
['folder', 'notebook']
```

The list starts as a small cart.

Then the program changes it one action at a time.

## Recap

Today you learned that list methods are actions a list can do.

You practiced:

- `append()` to add one item to the end
- `insert()` to add one item at an index
- `remove()` to remove a value
- `pop()` to remove an index and get the removed value back
- `sort()` to arrange a list in place
- `reverse()` to flip the current order
- `clear()` to empty a list
- checking with `in` before removing a value
- telling the difference between a value and an index
- remembering that most list methods change the original list

The most useful question is:

```text
What action do I want the list to do?
```

Then choose the method:

```text
Add to the end: append()
Add at an index: insert()
Remove by value: remove()
Remove by index: pop()
Arrange: sort()
Flip: reverse()
Empty: clear()
```

## Lesson Checklist

Before moving on, check that you can:

- call a list method with dot syntax
- explain why method parentheses matter
- add an item with `append()`
- insert an item with `insert()`
- remove a known value with `remove()`
- check whether a value exists before using `remove()`
- remove an item by position with `pop()`
- save the value returned by `pop()`
- sort a list and then print it
- explain why `print(scores.sort())` prints `None`
- reverse a list with `reverse()`
- empty a list with `clear()`
- choose between a value and an index

## Exercises

### Exercise 1

Predict the output.

```python
colors = ["red", "blue"]

colors.append("green")

print(colors)
```

Then run it.

### Exercise 2

Insert `"tea"` at the beginning of this list:

```python
drinks = ["water", "juice"]
```

Print the list after the insert.

### Exercise 3

Remove `"dust desk"` from this list:

```python
chores = ["wash cup", "dust desk", "fold clothes"]
```

Print the list after the removal.

### Exercise 4

Use `pop()` to remove the first item from this list:

```python
line = ["Asha", "Ben", "Cara"]
```

Save the removed name in a variable named `next_person`.

Print:

```text
Next: Asha
```

Then print the updated list.

### Exercise 5

Use `pop()` with no index to remove the last item:

```python
tabs = ["home", "search", "settings"]
```

Save the removed value in a variable named `closed_tab`.

Print the closed tab and the remaining list.

### Exercise 6

Sort this list:

```python
numbers = [5, 2, 9, 1]
```

Print the list after sorting.

### Exercise 7

Reverse this list:

```python
steps = ["start", "middle", "end"]
```

Print the list after reversing.

### Exercise 8

Fix the broken code.

Broken code:

```python
tasks = ["open laptop", "write notes"]

tasks.append

print(tasks)
```

The goal is:

```text
['open laptop', 'write notes', 'save file']
```

### Exercise 9

Fix the broken code.

Broken code:

```python
guests = ["Asha", "Ben"]

guests.remove("Cara")

print(guests)
```

Add a check so the program only removes `"Cara"` if it is in the list.

Otherwise, print:

```text
Cara is not invited.
```

### Exercise 10

Fix the broken code.

Broken code:

```python
scores = [90, 70, 100]

print(scores.sort())
```

The goal is:

```text
[70, 90, 100]
```

### Exercise 11

Choose the right method for each situation.

Situation:

```text
Add "milk" to the end of a grocery list.
```

Situation:

```text
Put "urgent email" at the beginning of a task list.
```

Situation:

```text
Remove the value "spam" from a list of messages.
```

Situation:

```text
Take the first person out of a line and save the name.
```

Situation:

```text
Put scores from lowest to highest.
```

Write one Python line for each situation.

### Exercise 12

Write a small list method program.

Start with:

```python
books = ["Poems", "Notes", "Stories"]
```

Then:

- append `"Guide"`
- insert `"Diary"` at index `1`
- remove `"Notes"`
- pop the last book and save it as `checked_out`
- sort the remaining books
- print the checked-out book
- print the final list

## Tiny Win

You can now make a list do useful work with method calls.

That means a list is no longer just a container you print or read. It is something your program can update, rearrange, and reset as the program runs.

## Tomorrow

Tomorrow you will learn about nested lists.

A nested list is a list that contains other lists:

```python
rows = [
    ["Asha", 90],
    ["Ben", 85],
    ["Cara", 100]
]
```

Today matters because nested lists still use the same list ideas:

```text
Lists have items.
Items have indexes.
Lists can be changed with methods.
```

Tomorrow, each item can be a list of its own.
