# Day 42: Mini Project: Shopping List App

**Focus:** Building a command-line shopping list app with lists, loops, menu choices, and safe list updates  
**You will practice:** lists, `for` loops, `while` loops, `input()`, `append()`, `remove()`, `pop()`, membership checks with `in`, simple menu choices, and `break`  
**Estimated time:** 60-75 minutes

## Today's Goal

Today you will build a shopping list app.

The app will run in the command line. It will let the user add items, show the current list, remove items, remove the last item, and quit.

By the end of this lesson, you should be able to:

- create an empty list for user-added items
- use a menu inside a loop
- read the user's choice with `input()`
- add items with `append()`
- show every item with a `for` loop
- check whether a list is empty
- check whether an item is already in a list
- remove a known item with `remove()`
- remove the last item with `pop()`
- use `break` to quit a loop
- test a command-line program with planned inputs
- debug common list app mistakes

This mini-project combines the list and loop tools you have been practicing.

The goal is not to build a store checkout system. The goal is to make one small program that remembers a changing list while the user works with it.

## The Project

Create this file:

```text
day-42/shopping_list_app.py
```

The program will:

- start with an empty shopping list
- show a simple menu
- let the user choose an option
- show the current list
- add one item at a time
- avoid adding blank items
- avoid adding the exact same item twice
- remove an item by name
- remove the last item with `pop()`
- keep running until the user chooses quit
- print the final list before closing

Example:

```text
Shopping List App
Build your list one item at a time.

Menu:
1. Show list
2. Add item
3. Remove item by name
4. Remove last item
5. Quit
Choose an option: 2
Item to add: milk
Added: milk

Menu:
1. Show list
2. Add item
3. Remove item by name
4. Remove last item
5. Quit
Choose an option: 2
Item to add: rice
Added: rice

Menu:
1. Show list
2. Add item
3. Remove item by name
4. Remove last item
5. Quit
Choose an option: 1
Shopping list:
1. milk
2. rice
Total items: 2

Menu:
1. Show list
2. Add item
3. Remove item by name
4. Remove last item
5. Quit
Choose an option: 5
Final list:
1. milk
2. rice
Goodbye.
```

The exact list depends on what the user types.

This app has a common command-line shape:

```text
create starting data
while the app is running:
    show choices
    ask for a choice
    run the matching action
    quit if the user chooses quit
```

The loop keeps the app alive. The list stores the changing data.

## The Big Idea

A shopping list app is a program that waits for commands.

Each command does one small job:

```text
show the list
add an item
remove an item
remove the last item
quit
```

The list starts empty:

```python
shopping_list = []
```

When the user adds an item, the app changes the list:

```python
shopping_list.append(item)
```

When the user removes an item by name, the app checks first:

```python
if item in shopping_list:
    shopping_list.remove(item)
else:
    print(item, "is not on the list.")
```

That check matters because `remove()` can only remove a value that exists.

When the user removes the last item, the app uses `pop()`:

```python
removed_item = shopping_list.pop()
```

That also needs a check. Calling `pop()` on an empty list causes an error.

The menu loop will use this shape:

```python
while True:
    choice = input("Choose an option: ").strip()

    if choice == "5":
        break
```

`while True` means:

```text
Keep running until something inside the loop stops it.
```

The `break` statement is the stop.

## The Mental Model

Think of the app as a small notebook with a menu.

The notebook is the list:

```python
shopping_list = []
```

The menu is the set of actions the user can choose:

```text
1. Show list
2. Add item
3. Remove item by name
4. Remove last item
5. Quit
```

Each time through the loop, the app asks:

```text
What does the user want to do next?
```

The answer from `input()` is text.

If the user types `1`, Python stores `"1"`, not the number `1`.

That means menu checks should compare with strings:

```python
if choice == "1":
    print("Show the list.")
```

Do not write this for an `input()` menu:

```python
if choice == 1:
    print("Show the list.")
```

That compares text to a number, so it will not match.

The list changes over time:

```text
start: []
add milk: ["milk"]
add rice: ["milk", "rice"]
remove milk: ["rice"]
```

The program does not need a different variable for every item.

One list can grow, shrink, and be printed again whenever the user asks.

## Step-by-Step Build

Build the app in stages.

Do not start with the full program. A menu app is easier to trust when each action works before you combine all of them.

### Step 1: Create The File

Create this file:

```text
day-42/shopping_list_app.py
```

Code:

```python
print("Shopping List App")
print("Build your list one item at a time.")
```

Run it from your course folder:

```bash
python day-42/shopping_list_app.py
```

If your computer uses `py`, use:

```bash
py day-42/shopping_list_app.py
```

If your computer uses `python3`, use:

```bash
python3 day-42/shopping_list_app.py
```

You should see:

```text
Shopping List App
Build your list one item at a time.
```

The file runs. That is the first checkpoint.

### Step 2: Start With An Empty List

The app needs one list to store the items.

Code:

```python
shopping_list = []

print("Shopping List App")
print("Items:", shopping_list)
print("Item count:", len(shopping_list))
```

You should see:

```text
Shopping List App
Items: []
Item count: 0
```

An empty list is not an error.

It means the app is ready, but the user has not added anything yet.

### Step 3: Show The List Nicely

Printing the whole list works, but an app should show one item per line.

Code:

```python
shopping_list = ["milk", "rice", "apples"]

print("Shopping list:")

item_number = 1

for item in shopping_list:
    print(str(item_number) + ".", item)
    item_number = item_number + 1

print("Total items:", len(shopping_list))
```

You should see:

```text
Shopping list:
1. milk
2. rice
3. apples
Total items: 3
```

The loop visits one item at a time.

The `item_number` variable starts at `1` because that is friendlier for a person reading a list.

Python indexes still start at `0`, but your display does not have to.

### Step 4: Handle An Empty List

If the list is empty, the app should say so.

Code:

```python
shopping_list = []

if len(shopping_list) == 0:
    print("Your shopping list is empty.")
else:
    print("Shopping list:")

    item_number = 1

    for item in shopping_list:
        print(str(item_number) + ".", item)
        item_number = item_number + 1

    print("Total items:", len(shopping_list))
```

You should see:

```text
Your shopping list is empty.
```

Now change the first line:

```python
shopping_list = ["milk", "rice"]
```

You should see:

```text
Shopping list:
1. milk
2. rice
Total items: 2
```

This gives the app two clear display paths:

```text
empty list
list with items
```

### Step 5: Add One Item With `append()`

Now ask the user for one item.

Code:

```python
shopping_list = []

item = input("Item to add: ").strip()
shopping_list.append(item)

print("Shopping list:", shopping_list)
```

Try this:

```text
milk
```

You should see:

```text
Item to add: milk
Shopping list: ['milk']
```

The important line is:

```python
shopping_list.append(item)
```

Read it as:

```text
Ask the shopping_list to add item to the end.
```

### Step 6: Reject Blank Items

If the user just presses Enter, the app should not add an empty string.

Code:

```python
shopping_list = []

item = input("Item to add: ").strip()

if item == "":
    print("No item added.")
else:
    shopping_list.append(item)
    print("Added:", item)

print("Shopping list:", shopping_list)
```

Try this:

```text

```

You should see:

```text
Item to add:
No item added.
Shopping list: []
```

Now run it again and type:

```text
bread
```

You should see:

```text
Item to add: bread
Added: bread
Shopping list: ['bread']
```

The `.strip()` call removes extra spaces from the beginning and end of the input.

That means this input:

```text
   bread
```

becomes:

```text
bread
```

### Step 7: Check For Duplicates

For this app, the same exact item should not be added twice.

Code:

```python
shopping_list = ["milk"]

item = input("Item to add: ").strip()

if item == "":
    print("No item added.")
elif item in shopping_list:
    print(item, "is already on the list.")
else:
    shopping_list.append(item)
    print("Added:", item)

print("Shopping list:", shopping_list)
```

Try this:

```text
milk
```

You should see:

```text
Item to add: milk
milk is already on the list.
Shopping list: ['milk']
```

Now try:

```text
eggs
```

You should see:

```text
Item to add: eggs
Added: eggs
Shopping list: ['milk', 'eggs']
```

The membership check is:

```python
item in shopping_list
```

It asks:

```text
Is this exact item already in the list?
```

### Step 8: Build A Small Menu Loop

Now make the app repeat.

Start with only three choices:

```text
1. Show list
2. Add item
3. Quit
```

Code:

```python
shopping_list = []

print("Shopping List App")

while True:
    print("")
    print("Menu:")
    print("1. Show list")
    print("2. Add item")
    print("3. Quit")

    choice = input("Choose an option: ").strip()

    if choice == "1":
        print("Shopping list:", shopping_list)
    elif choice == "2":
        item = input("Item to add: ").strip()

        if item == "":
            print("No item added.")
        else:
            shopping_list.append(item)
            print("Added:", item)
    elif choice == "3":
        print("Goodbye.")
        break
    else:
        print("Please choose 1, 2, or 3.")
```

Try this:

```text
2
milk
1
3
```

You should see the app add `"milk"`, show the list, and quit.

The line that stops the loop is:

```python
break
```

Without `break`, choosing quit would print a message but the menu would keep coming back.

### Step 9: Remove An Item By Name

The app should let the user remove an item by typing its name.

Use `in` before `remove()`.

Code:

```python
shopping_list = ["milk", "rice", "apples"]

item = input("Item to remove: ").strip()

if item in shopping_list:
    shopping_list.remove(item)
    print("Removed:", item)
else:
    print(item, "is not on the list.")

print("Shopping list:", shopping_list)
```

Try this:

```text
rice
```

You should see:

```text
Item to remove: rice
Removed: rice
Shopping list: ['milk', 'apples']
```

Now try:

```text
tea
```

You should see:

```text
Item to remove: tea
tea is not on the list.
Shopping list: ['milk', 'rice', 'apples']
```

The check prevents a `ValueError`.

### Step 10: Remove The Last Item With `pop()`

Sometimes the user may want to undo the last item they added.

Use `pop()` for that.

Code:

```python
shopping_list = ["milk", "rice", "apples"]

if len(shopping_list) == 0:
    print("There is nothing to remove.")
else:
    removed_item = shopping_list.pop()
    print("Removed last item:", removed_item)

print("Shopping list:", shopping_list)
```

You should see:

```text
Removed last item: apples
Shopping list: ['milk', 'rice']
```

Now try the same idea with an empty list:

```python
shopping_list = []

if len(shopping_list) == 0:
    print("There is nothing to remove.")
else:
    removed_item = shopping_list.pop()
    print("Removed last item:", removed_item)

print("Shopping list:", shopping_list)
```

You should see:

```text
There is nothing to remove.
Shopping list: []
```

The check matters because `pop()` needs an item to remove.

### Step 11: Put It Together

Here is the complete program:

```python
shopping_list = []

print("Shopping List App")
print("Build your list one item at a time.")

while True:
    print("")
    print("Menu:")
    print("1. Show list")
    print("2. Add item")
    print("3. Remove item by name")
    print("4. Remove last item")
    print("5. Quit")

    choice = input("Choose an option: ").strip()

    if choice == "1":
        if len(shopping_list) == 0:
            print("Your shopping list is empty.")
        else:
            print("Shopping list:")

            item_number = 1

            for item in shopping_list:
                print(str(item_number) + ".", item)
                item_number = item_number + 1

            print("Total items:", len(shopping_list))

    elif choice == "2":
        item = input("Item to add: ").strip()

        if item == "":
            print("No item added.")
        elif item in shopping_list:
            print(item, "is already on the list.")
        else:
            shopping_list.append(item)
            print("Added:", item)

    elif choice == "3":
        if len(shopping_list) == 0:
            print("There is nothing to remove.")
        else:
            item = input("Item to remove: ").strip()

            if item in shopping_list:
                shopping_list.remove(item)
                print("Removed:", item)
            else:
                print(item, "is not on the list.")

    elif choice == "4":
        if len(shopping_list) == 0:
            print("There is nothing to remove.")
        else:
            removed_item = shopping_list.pop()
            print("Removed last item:", removed_item)

    elif choice == "5":
        print("Final list:")

        if len(shopping_list) == 0:
            print("Your shopping list is empty.")
        else:
            item_number = 1

            for item in shopping_list:
                print(str(item_number) + ".", item)
                item_number = item_number + 1

        print("Goodbye.")
        break

    else:
        print("Please choose 1, 2, 3, 4, or 5.")
```

Run the program several times.

Try a normal run:

```text
2
milk
2
rice
1
5
```

Try duplicate input:

```text
2
milk
2
milk
5
```

Try blank input:

```text
2

5
```

Try removing by name:

```text
2
bread
2
eggs
3
bread
1
5
```

Try removing the last item:

```text
2
tea
2
apples
4
1
5
```

Try a wrong menu choice:

```text
9
5
```

When you test, check more than whether the program crashes.

Also ask:

- Does the menu come back after each normal action?
- Does choice `5` stop the loop?
- Does a blank item stay out of the list?
- Does the exact same item get rejected the second time?
- Does removing a missing item avoid crashing?
- Does `pop()` avoid running on an empty list?
- Does the final list match the actions you took?

That is how you test a menu program with confidence.

## Try It Yourself

Make the app your own.

Start with small changes:

- change the welcome message
- change the menu wording
- let duplicate items be added by removing the duplicate check
- add a choice that only prints the item count
- add a choice that sorts the list before showing it
- add a choice that clears the whole list

If you add a new choice, update three places:

```text
the printed menu
the if / elif block
the invalid-choice message
```

Example:

```python
print("6. Show item count")
```

Then add:

```python
elif choice == "6":
    print("Total items:", len(shopping_list))
```

Then update:

```python
print("Please choose 1, 2, 3, 4, 5, or 6.")
```

Those three pieces belong together.

Try this: make the app ignore extra spaces.

The final program already uses:

```python
item = input("Item to add: ").strip()
```

That means a user can type:

```text
   milk
```

and the app stores:

```text
milk
```

Now test whether the same is true when removing an item.

Add `"milk"`, then remove it by typing:

```text
   milk
```

The item should still be removed because `.strip()` cleans the input.

## Common Mistake

### Mistake 1: Comparing A Menu Choice To A Number

Broken code:

```python
choice = input("Choose an option: ")

if choice == 1:
    print("Show the list.")
else:
    print("Unknown choice.")
```

If the user types `1`, the program prints:

```text
Unknown choice.
```

The problem is that `input()` returns text.

This comparison is really:

```text
"1" == 1
```

Those are different values.

Fixed code:

```python
choice = input("Choose an option: ")

if choice == "1":
    print("Show the list.")
else:
    print("Unknown choice.")
```

Compare menu choices with strings unless you have converted the input.

### Mistake 2: Setting The List Equal To `append()`

Broken code:

```python
shopping_list = []

item = "milk"
shopping_list = shopping_list.append(item)

print(shopping_list)
```

You should see:

```text
None
```

`append()` changes the list in place. It does not give back a new list.

Fixed code:

```python
shopping_list = []

item = "milk"
shopping_list.append(item)

print(shopping_list)
```

You should see:

```text
['milk']
```

Call `append()` on its own line.

### Mistake 3: Removing Without Checking First

Broken code:

```python
shopping_list = ["milk", "rice"]

item = input("Item to remove: ").strip()
shopping_list.remove(item)

print(shopping_list)
```

If the user types:

```text
bread
```

the program crashes because `"bread"` is not in the list.

Fixed code:

```python
shopping_list = ["milk", "rice"]

item = input("Item to remove: ").strip()

if item in shopping_list:
    shopping_list.remove(item)
else:
    print(item, "is not on the list.")

print(shopping_list)
```

Check with `in` before using `remove()` when the value comes from the user.

### Mistake 4: Popping From An Empty List

Broken code:

```python
shopping_list = []

removed_item = shopping_list.pop()

print("Removed:", removed_item)
```

This is broken because there is no last item to remove.

Fixed code:

```python
shopping_list = []

if len(shopping_list) == 0:
    print("There is nothing to remove.")
else:
    removed_item = shopping_list.pop()
    print("Removed:", removed_item)
```

Check that the list has something in it before calling `pop()`.

## Debug It

Debugging this app usually means watching the list and the menu choice.

The examples in this section have bugs. Read the code, find the problem, then compare it with the fix.

### Bug 1: Quit Prints A Message But Does Not Quit

Broken code:

```python
while True:
    choice = input("Choose: ").strip()

    if choice == "q":
        print("Goodbye.")
    else:
        print("Still working.")
```

The problem is that the `q` branch does not stop the loop.

Fixed code:

```python
while True:
    choice = input("Choose: ").strip()

    if choice == "q":
        print("Goodbye.")
        break
    else:
        print("Still working.")
```

Use `break` when a menu choice should end a `while True` loop.

### Bug 2: The Program Adds Blank Items

Broken code:

```python
shopping_list = []

item = input("Item to add: ").strip()
shopping_list.append(item)

print(shopping_list)
```

If the user presses Enter without typing an item, the list gets an empty string.

Fixed code:

```python
shopping_list = []

item = input("Item to add: ").strip()

if item == "":
    print("No item added.")
else:
    shopping_list.append(item)

print(shopping_list)
```

Ask this debugging question:

```text
What should count as a real item?
```

Then check for that before changing the list.

### Bug 3: The List Prints Repeatedly Instead Of Each Item

Broken code:

```python
shopping_list = ["milk", "rice", "apples"]

for item in shopping_list:
    print(shopping_list)
```

You should see:

```text
['milk', 'rice', 'apples']
['milk', 'rice', 'apples']
['milk', 'rice', 'apples']
```

The loop runs once for each item, but it prints the whole list every time.

Fixed code:

```python
shopping_list = ["milk", "rice", "apples"]

for item in shopping_list:
    print(item)
```

You should see:

```text
milk
rice
apples
```

Inside a list loop, use the loop variable when you want the current item.

### Bug 4: The Wrong Message Appears After Removing

Broken code:

```python
shopping_list = ["milk", "rice"]
item = "milk"

if item in shopping_list:
    shopping_list.remove(item)

if item in shopping_list:
    print("Removed:", item)
else:
    print(item, "is not on the list.")
```

You should see:

```text
milk is not on the list.
```

That message is confusing because the item was removed successfully.

The problem is that the second `if` checks the list after the removal.

Fixed code:

```python
shopping_list = ["milk", "rice"]
item = "milk"

if item in shopping_list:
    shopping_list.remove(item)
    print("Removed:", item)
else:
    print(item, "is not on the list.")
```

Print the success message inside the branch where the success happens.

## Read the Docs

Today, look up Python's official tutorial section about list methods:

```text
https://docs.python.org/3/tutorial/datastructures.html#more-on-lists
```

Look for these method shapes:

```python
list.append(x)
list.remove(x)
list.pop([i])
```

The word `list` means "some list."

In your own code, you use your variable name:

```python
shopping_list.append("milk")
shopping_list.remove("milk")
shopping_list.pop()
```

Also review the official tutorial section for `break`:

```text
https://docs.python.org/3/tutorial/controlflow.html#break-and-continue-statements
```

For today, remember:

- `append(x)` adds `x` to the end of a list
- `remove(x)` removes the first matching value
- `pop()` removes and returns the last item
- `break` exits the nearest loop
- `input()` gives text, so menu choices like `"1"` are strings

Documentation often shows more than you need right away.

Read it with one practical question:

```text
What does this tool change, return, or stop?
```

## Mini Challenge

Create this file:

```text
day-42/bonus_shopping_list.py
```

Build a second version of the app with two lists:

```python
shopping_list = []
bought_items = []
```

Add a menu choice named:

```text
Mark item as bought
```

When the user marks an item as bought:

- ask for the item name
- check whether it is in `shopping_list`
- remove it from `shopping_list`
- append it to `bought_items`
- print both lists

Start with this small version before adding it to the full menu:

```python
shopping_list = ["milk", "rice", "apples"]
bought_items = []

item = input("Item bought: ").strip()

if item in shopping_list:
    shopping_list.remove(item)
    bought_items.append(item)
    print("Bought:", item)
else:
    print(item, "is not on the shopping list.")

print("Still to buy:", shopping_list)
print("Bought items:", bought_items)
```

Try this:

```text
rice
```

You should see:

```text
Item bought: rice
Bought: rice
Still to buy: ['milk', 'apples']
Bought items: ['rice']
```

This is still beginner-friendly because it uses only two lists.

Later, you will learn a cleaner way to connect extra information to an item.

## Real-World Use

Shopping list apps are small versions of many real programs.

Examples:

- a shopping cart stores products before checkout
- a task app stores tasks before they are done
- a playlist stores songs before they are played
- a packing app stores items before a trip
- a command-line tool shows a menu until the user quits
- a form checks input before saving it

The project uses several useful patterns:

```text
start with empty data
show a menu
ask for a choice
validate the input
change a list
show the result
repeat until quit
```

Those patterns appear in many small tools.

A shopping list is a good beginner project because the data changes in ways you can see immediately.

When the list on the screen matches the actions you took, the program's logic is working.

## Recap

Today you built a complete shopping list app.

You practiced:

- creating an empty list
- adding values with `append()`
- showing list items with a `for` loop
- counting items with `len()`
- using `input()` for menu choices
- remembering that input starts as text
- using `strip()` to clean input
- checking for blank items
- checking membership with `in`
- removing values with `remove()`
- removing the last value with `pop()`
- checking before `remove()` and `pop()`
- using `while True` for a menu loop
- using `break` to quit
- testing a program with planned input sequences

The main idea:

> A menu loop lets the user choose repeated actions, and a list lets the program remember what changed.

## Lesson Checklist

Before moving on, check that you can:

- create and run `day-42/shopping_list_app.py`
- explain why the shopping list starts as `[]`
- add one item with `append()`
- reject a blank item
- use `in` to check whether an item is already listed
- print each item with a `for` loop
- count items with `len()`
- remove an item by value with `remove()`
- check before using `remove()`
- remove the last item with `pop()`
- check before using `pop()`
- compare menu choices with strings like `"1"`
- write a `while True` menu loop
- use `break` to quit the loop
- test adding, showing, removing, invalid choices, and quitting

## Exercises

### Exercise 1

Create this file:

```text
day-42/add_one_item.py
```

Write a program that:

- starts with an empty list named `shopping_list`
- asks for one item
- adds it with `append()`
- prints the list

### Exercise 2

Reject blank input.

Start with:

```python
shopping_list = []
item = input("Item to add: ").strip()
```

If `item` is empty, print:

```text
No item added.
```

Otherwise, append it and print the list.

### Exercise 3

Print a list one item at a time.

Start with:

```python
shopping_list = ["milk", "rice", "apples"]
```

Use a `for` loop to print:

```text
Buy: milk
Buy: rice
Buy: apples
```

### Exercise 4

Add item numbers.

Use this list:

```python
shopping_list = ["milk", "rice", "apples"]
```

Print:

```text
1. milk
2. rice
3. apples
```

Use a counter that starts at `1`.

### Exercise 5

Fix the menu choice.

Broken code:

```python
choice = input("Choose: ")

if choice == 2:
    print("Add item.")
```

The user should be able to type `2` and see:

```text
Add item.
```

### Exercise 6

Fix the append mistake.

Broken code:

```python
shopping_list = []

shopping_list = shopping_list.append("milk")

print(shopping_list)
```

The goal is:

```text
['milk']
```

### Exercise 7

Write a safe removal.

Start with:

```python
shopping_list = ["milk", "rice", "apples"]
item = input("Item to remove: ").strip()
```

If the item is in the list, remove it.

Otherwise, print:

```text
That item is not on the list.
```

### Exercise 8

Write a safe `pop()`.

Start with:

```python
shopping_list = []
```

If the list is empty, print:

```text
There is nothing to remove.
```

Otherwise, pop the last item and print it.

Then test again with:

```python
shopping_list = ["milk", "rice"]
```

### Exercise 9

Build a tiny menu with two choices:

```text
1. Say hello
2. Quit
```

Use `while True`.

If the user chooses `1`, print:

```text
Hello.
```

If the user chooses `2`, print:

```text
Goodbye.
```

Then use `break`.

### Exercise 10

Add an invalid-choice message to your tiny menu.

If the user types anything except `1` or `2`, print:

```text
Please choose 1 or 2.
```

### Exercise 11

Add a count-only choice to the final shopping list app.

The new menu choice should print:

```text
Total items: 3
```

Use `len(shopping_list)`.

Remember to update the printed menu and the invalid-choice message.

### Exercise 12

Write three test runs before running your program.

Include:

- adding two items and showing the list
- trying to remove an item that is not there
- trying a wrong menu choice and then quitting

For each test, write:

```text
Inputs:
What should happen:
What actually happened:
```

If the result is different from what you expected, debug one branch at a time.

## Tiny Win

You built a complete command-line app.

It keeps data in a list, shows a menu, responds to user choices, protects risky list operations, and quits cleanly.

That is a useful project shape. You can reuse it for tasks, packing lists, playlists, reading lists, practice trackers, and small personal tools.

## Tomorrow

Tomorrow you start dictionaries.

The next lesson is:

```text
Day 43: Dictionaries
```

Today, each shopping item was only a string:

```python
shopping_list = ["milk", "rice", "apples"]
```

That works for a simple list, but real shopping lists often need extra information:

```text
milk -> 1
rice -> 2
apples -> 6
```

A dictionary lets one value point to another value:

```python
shopping_counts = {
    "milk": 1,
    "rice": 2,
    "apples": 6,
}
```

That will let future programs connect an item name to a quantity, price, category, or status.

Today you learned how to manage a changing list.

Tomorrow you will learn how to connect names to details.
