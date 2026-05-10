# Day 41: Practice Day: Collection Problems

**Focus:** Solving small problems with collections  
**You will practice:** lists, indexing, slicing, updating lists, looping through lists, list methods, nested lists, tuples, sets, and choosing the right collection  
**Estimated time:** 60-75 minutes

## Today's Goal

Today is a practice day.

You are not learning a new collection type. You are using the collection tools you already know:

- lists
- indexes
- slices
- list updates
- list methods
- loops through lists
- nested lists
- tuples
- sets
- collection choice

By the end of this lesson, you should be able to:

- read a small collection problem and decide where to start
- choose a list, tuple, or set for a clear reason
- use indexes when positions matter
- use slices when you need part of a list
- update a list safely
- loop through a list and build a result
- read a nested list one level at a time
- use a tuple for a small fixed record
- use a set for unique values
- prepare for tomorrow's shopping list app

The goal is not to memorize every method.

The goal is to practice asking:

```text
What kind of collection fits this problem?
What action does the program need to take?
What should I check before changing the collection?
```

Those questions will help you build tomorrow's project with less guessing.

## The Big Idea

Most collection problems are built from a few familiar decisions.

Ask:

```text
Do I need the order?
Do I need the first, last, or middle items?
Will the collection change?
Can values repeat?
Do I need only unique values?
Do a few values belong together as one fixed record?
Is there a smaller list inside a bigger list?
```

Those questions point you toward a collection.

Use a list when order matters and the values may change:

```python
shopping_items = ["rice", "tea", "rice"]

shopping_items.append("milk")

print(shopping_items)
```

You should see:

```text
['rice', 'tea', 'rice', 'milk']
```

Use a tuple when values belong together and the shape should stay fixed:

```python
store_visit = ("Corner Market", "evening")

print(store_visit[0])
print(store_visit[1])
```

You should see:

```text
Corner Market
evening
```

Use a set when uniqueness matters more than order:

```python
shopping_items = ["rice", "tea", "rice", "milk", "tea"]
unique_items = set(shopping_items)

print(sorted(unique_items))
```

You should see:

```text
['milk', 'rice', 'tea']
```

The same real-world topic can use more than one collection.

Example:

```python
shopping_items = ["rice", "tea", "rice"]
unique_items = set(shopping_items)
store_visit = ("Corner Market", "evening")

print("Items:", shopping_items)
print("Unique items:", sorted(unique_items))
print("Visit:", store_visit[0], "at", store_visit[1])
```

You should see:

```text
Items: ['rice', 'tea', 'rice']
Unique items: ['rice', 'tea']
Visit: Corner Market at evening
```

The list keeps the shopping items in order.

The set answers the question:

```text
Which different items are on the list?
```

The tuple keeps the store name and time together.

One program can use all three when each one has a clear job.

## The Mental Model

Before writing code, name the shape of the data.

For a list, think:

```text
This is a row of values.
The order matters.
I may add, remove, or replace items.
```

For an index, think:

```text
I want one item at a position.
Index 0 is the first item.
Index -1 is the last item.
```

For a slice, think:

```text
I want a smaller sequence.
The stop position is not included.
```

For a nested list, think:

```text
The outside list holds rows.
Each inside list holds items in that row.
One index gets a row.
Two indexes can get one value inside a row.
```

For a tuple, think:

```text
These values belong together.
Their positions have meaning.
The group is not meant to grow with append().
```

For a set, think:

```text
Only one copy of each value matters.
Order is not the point.
Membership checks are important.
```

Here is a small map:

```text
Need a changing shopping list?       list
Need the first item?                 list index
Need the first three items?          list slice
Need rows of aisle items?            nested list
Need a store name and time pair?     tuple
Need unique item names?              set
```

When you feel stuck, do not start by asking:

```text
Which syntax do I remember?
```

Start by asking:

```text
What is the data shaped like?
What does the program need to do with it?
```

Then choose the collection that matches the job.

## Warm-Up

For each warm-up, predict the output before running the code.

### Warm-Up 1

Code:

```python
items = ["rice", "milk", "apples", "tea"]

print("First:", items[0])
print("Last:", items[-1])
print("Middle:", items[1:3])
```

You should see:

```text
First: rice
Last: tea
Middle: ['milk', 'apples']
```

Debugging prompt:

```text
Which line gets one item?
Which line gets a smaller list?
```

### Warm-Up 2

Code:

```python
tasks = ["read lesson", "run examples"]

tasks.append("fix one bug")
tasks.insert(1, "review notes")
finished = tasks.pop()

print("Tasks:", tasks)
print("Finished:", finished)
```

You should see:

```text
Tasks: ['read lesson', 'review notes', 'run examples']
Finished: fix one bug
```

Debugging prompt:

```text
Which method added to the end?
Which method removed from the end?
```

### Warm-Up 3

Code:

```python
scores = [4, 3, 5]
total = 0

for score in scores:
    total = total + score

print("Total:", total)
print("Average:", total / len(scores))
```

You should see:

```text
Total: 12
Average: 4.0
```

Debugging prompt:

```text
Why does total start before the loop?
Why is the final print after the loop?
```

### Warm-Up 4

Code:

```python
weekly_items = [
    ["rice", "milk"],
    ["apples", "tea"],
]

print(weekly_items[0])
print(weekly_items[1][0])

for row in weekly_items:
    print("Row:", row)
```

You should see:

```text
['rice', 'milk']
apples
Row: ['rice', 'milk']
Row: ['apples', 'tea']
```

Debugging prompt:

```text
What does one index return?
What do two indexes return?
```

### Warm-Up 5

Code:

```python
visit = ("Corner Market", "evening")
tags = {"food", "weekly", "food"}

store, time = visit

print(store)
print(time)
print(sorted(tags))
```

You should see:

```text
Corner Market
evening
['food', 'weekly']
```

Debugging prompt:

```text
Why does "food" appear once in the sorted tags?
```

## Practice Problems

Use this rhythm for each problem:

```text
Read the goal.
Choose the collection.
Write the smallest useful version.
Predict the result.
Run the code.
Test one change.
Fix one thing at a time.
```

### Practice Problem 1: Build A Small Shopping List

Create a file named `day-41/shopping_list_edits.py`.

Start with:

```python
shopping = ["rice", "milk", "apples"]
```

Rules:

```text
Add "tea" to the end.
Replace "milk" with "oat milk".
Remove "apples" if it is on the list.
Print each final item on its own line.
Print the final count.
```

Hint:

```text
This is a list problem because the order matters and the list changes.
```

Code:

```python
shopping = ["rice", "milk", "apples"]

shopping.append("tea")
shopping[1] = "oat milk"

if "apples" in shopping:
    shopping.remove("apples")

for item in shopping:
    print("-", item)

print("Item count:", len(shopping))
```

You should see:

```text
- rice
- oat milk
- tea
Item count: 3
```

Try this:

```text
Change the starting list so "apples" is not included.
Run the program again.
Does the if statement keep remove() safe?
```

Debugging prompt:

```text
What would happen if you called remove("apples") without checking first?
```

### Practice Problem 2: Read The Packed Items

Create a file named `day-41/packed_items.py`.

Start with:

```python
packed = ["notebook", "charger", "snacks", "water bottle", "keys"]
```

Rules:

```text
Print the first packed item.
Print the last packed item.
Print the items from index 1 up to index 4.
Make a copy of the list.
Add "ticket" to the copy.
Print the original list and the copy.
```

Hint:

```text
Use indexing for one item.
Use slicing for part of the list.
Use [:] when you want a copy.
```

Code:

```python
packed = ["notebook", "charger", "snacks", "water bottle", "keys"]

print("First:", packed[0])
print("Last:", packed[-1])
print("For the bus:", packed[1:4])

travel_ready = packed[:]
travel_ready.append("ticket")

print("Original:", packed)
print("Copy:", travel_ready)
```

You should see:

```text
First: notebook
Last: keys
For the bus: ['charger', 'snacks', 'water bottle']
Original: ['notebook', 'charger', 'snacks', 'water bottle', 'keys']
Copy: ['notebook', 'charger', 'snacks', 'water bottle', 'keys', 'ticket']
```

Question to answer:

```text
Why did adding "ticket" to travel_ready not change packed?
```

### Practice Problem 3: Clean Duplicate Requests

Create a file named `day-41/unique_requests.py`.

Start with:

```python
requests = ["rice", "tea", "rice", "apples", "tea", "milk"]
```

Rules:

```text
Print the number of original requests.
Create a set of unique requests.
Print the number of unique requests.
Print the unique requests in sorted order.
Check whether "milk" is included.
```

Hint:

```text
This is a set problem because repeated values should become one value.
```

Code:

```python
requests = ["rice", "tea", "rice", "apples", "tea", "milk"]
unique_requests = set(requests)

print("Original count:", len(requests))
print("Unique count:", len(unique_requests))
print("Unique requests:", sorted(unique_requests))

if "milk" in unique_requests:
    print("Milk is on the list.")
else:
    print("Milk is missing.")
```

You should see:

```text
Original count: 6
Unique count: 4
Unique requests: ['apples', 'milk', 'rice', 'tea']
Milk is on the list.
```

Try this:

```text
Add another "rice" to requests.
The original count should change.
The unique count should not change.
```

### Practice Problem 4: Read Aisle Rows

Create a file named `day-41/aisle_rows.py`.

Start with this nested list:

```python
aisles = [
    ["produce", "apples", "bananas"],
    ["dairy", "milk", "yogurt"],
    ["pantry", "rice", "tea"],
]
```

Rules:

```text
Each inner list starts with an aisle name.
The rest of that inner list contains items in that aisle.
Print the aisle name.
Print how many items are in that aisle.
Print each item under the aisle.
```

Hint:

```text
Use aisle[0] for the aisle name.
Use aisle[1:] for the items.
```

Code:

```python
aisles = [
    ["produce", "apples", "bananas"],
    ["dairy", "milk", "yogurt"],
    ["pantry", "rice", "tea"],
]

for aisle in aisles:
    aisle_name = aisle[0]
    items = aisle[1:]

    print(aisle_name + ":", len(items), "items")

    for item in items:
        print("-", item)
```

You should see:

```text
produce: 2 items
- apples
- bananas
dairy: 2 items
- milk
- yogurt
pantry: 2 items
- rice
- tea
```

Debugging prompt:

```text
What does aisle hold on each loop turn?
Why is aisle[1:] a slice instead of one item?
```

### Practice Problem 5: Use A Tuple For One Item Record

Create a file named `day-41/item_record.py`.

Start with:

```python
item_record = ("rice", 2, "pantry")
```

Rules:

```text
Unpack the tuple into item name, quantity, and aisle.
Print each value clearly.
Create a new tuple with the quantity increased by 1.
Print the new tuple.
```

Hint:

```text
Use a tuple because the record has a fixed shape:
name, quantity, aisle.
```

Code:

```python
item_record = ("rice", 2, "pantry")

name, quantity, aisle = item_record

print("Item:", name)
print("Quantity:", quantity)
print("Aisle:", aisle)

updated_record = (name, quantity + 1, aisle)

print("Updated:", updated_record)
```

You should see:

```text
Item: rice
Quantity: 2
Aisle: pantry
Updated: ('rice', 3, 'pantry')
```

Question to answer:

```text
Why did the code make a new tuple instead of changing item_record[1]?
```

### Practice Problem 6: Use Three Collections Together

Create a file named `day-41/collection_mix.py`.

Rules:

```text
Use a list for shopping items.
Use a tuple for store information.
Use a set for visited store sections.
Add one item to the shopping list.
Print the next item to buy.
Print the store name.
Print the unique visited sections in sorted order.
Print the shopping item count.
```

Hint:

```text
Each collection should have one clear job.
```

Code:

```python
shopping_list = ["rice", "milk"]
store_location = ("Corner Market", "Aisle 3")
visited_sections = {"produce", "dairy", "produce"}

shopping_list.append("tea")

print("Next item:", shopping_list[0])
print("Store:", store_location[0])
print("Sections:", sorted(visited_sections))
print("Item count:", len(shopping_list))
```

You should see:

```text
Next item: rice
Store: Corner Market
Sections: ['dairy', 'produce']
Item count: 3
```

Debugging prompt:

```text
Which collection changed?
Which collection removed a duplicate?
Which collection used an index?
```

### Practice Problem 7: Check Required Items

Create a file named `day-41/required_items.py`.

Start with:

```python
shopping_list = ["rice", "tea", "apples"]
required_items = {"rice", "milk", "apples"}
```

Rules:

```text
Build a list named missing.
Loop through the required items in sorted order.
If a required item is not in the shopping list, add it to missing.
Print a friendly message.
```

Hint:

```text
Use a list for missing because you are building an ordered report.
Use a set for required_items because each required item should appear once.
```

Code:

```python
shopping_list = ["rice", "tea", "apples"]
required_items = {"rice", "milk", "apples"}
missing = []

for item in sorted(required_items):
    if item not in shopping_list:
        missing.append(item)

if len(missing) == 0:
    print("All required items are on the list.")
else:
    print("Missing items:", missing)
```

You should see:

```text
Missing items: ['milk']
```

Try this:

```text
Add "milk" to shopping_list.
The final message should change.
```

This problem is close to a real shopping list app feature:

```text
Compare what the user has with what the user still needs.
```

## Try It Yourself

Choose one option and write it without looking back at the earlier solutions first.

### Option A: Shopping List Summary

Create a file named `day-41/shopping_summary.py`.

Start with:

```python
shopping = ["rice", "milk", "tea"]
new_item = "apples"
```

Rules:

```text
Add new_item to shopping.
Print the first item.
Print the last item.
Print the whole list.
Print the number of items.
Loop through the list and print each item with a dash.
```

Hint:

```text
This is list, indexing, append(), len(), and a for loop.
```

One run should show that `"apples"` was added.

### Option B: Unique Item Types

Create a file named `day-41/unique_item_types.py`.

Start with:

```python
cart = ["rice", "tea", "rice", "milk", "tea", "apples"]
```

Rules:

```text
Print the cart.
Print the cart length.
Create a set from cart.
Print the number of unique item types.
Print the unique item types with sorted().
```

Hint:

```text
The list keeps repeated cart entries.
The set answers how many different item names appear.
```

### Option C: Weekly Shopping Rows

Create a file named `day-41/weekly_rows.py`.

Start with:

```python
weekly = [
    ["Monday", "rice", "milk"],
    ["Tuesday", "apples"],
    ["Wednesday", "tea", "bread"],
]
```

Rules:

```text
Loop through each row.
The first value is the day.
The rest of the row is that day's shopping list.
Print the day.
Print each item under that day.
```

Hint:

```text
Use row[0] for the day.
Use row[1:] for the items.
```

Choose the option that makes you pause for a moment.

That pause is a good practice target.

## Common Mistake

Practice days are good days to notice habits that create collection bugs.

### Mistake 1: Saving The Result Of `append()`

Broken code:

```python
shopping = ["rice", "milk"]

shopping = shopping.append("tea")

print(shopping)
```

This code runs, but it does not keep the list.

`append()` changes the list in place. It does not give back a new list to save.

You should see:

```text
None
```

Fixed code:

```python
shopping = ["rice", "milk"]

shopping.append("tea")

print(shopping)
```

You should see:

```text
['rice', 'milk', 'tea']
```

Read the fixed line as:

```text
Ask the shopping list to append "tea".
```

### Mistake 2: Removing Before Checking

Broken code:

```python
items = ["rice", "milk"]

items.remove("tea")

print(items)
```

This is broken because `"tea"` is not in the list.

`remove()` expects the value to exist.

Fixed code:

```python
items = ["rice", "milk"]

if "tea" in items:
    items.remove("tea")
else:
    print("Tea was not on the list.")

print(items)
```

You should see:

```text
Tea was not on the list.
['rice', 'milk']
```

Check before removing when a missing value is possible.

### Mistake 3: Stopping At The Row

This code runs, but it does not reach the item.

Code:

```python
aisles = [
    ["produce", "apples"],
    ["dairy", "milk"],
]

print(aisles[1])
```

You should see:

```text
['dairy', 'milk']
```

That is the whole row.

Fixed code:

```python
aisles = [
    ["produce", "apples"],
    ["dairy", "milk"],
]

print(aisles[1][1])
```

You should see:

```text
milk
```

With nested lists, one index gets an inner list. Two indexes can reach one value inside that inner list.

### Mistake 4: Using A Set When Repeated Items Matter

This code runs, but it loses information:

```python
cart = {"rice", "tea", "rice"}

print(sorted(cart))
```

You should see:

```text
['rice', 'tea']
```

The repeated `"rice"` disappeared.

That is useful for unique item names, but not for a cart where two entries may mean two quantities.

Fixed code:

```python
cart = ["rice", "tea", "rice"]

print(cart)
print("Item entries:", len(cart))
```

You should see:

```text
['rice', 'tea', 'rice']
Item entries: 3
```

Use a list when repeated values still mean something.

## Debug It

These programs are intentionally broken or do not meet their stated goal. Read the goal first, predict what the code does, then study the fix.

### Debug 1: Three Shopping Items

Goal:

```text
Items: ['rice', 'milk', 'tea']
Count: 3
Has milk: True
```

Broken code:

```python
shopping = ["rice" "milk", "tea"]

print("Items:", shopping)
print("Count:", len("shopping"))
print("Has milk:", "milk" in shopping)
```

There are two problems.

The first problem is missing a comma between `"rice"` and `"milk"`.

The second problem is `len("shopping")`. That counts the letters in the string `"shopping"`, not the items in the list.

Fixed code:

```python
shopping = ["rice", "milk", "tea"]

print("Items:", shopping)
print("Count:", len(shopping))
print("Has milk:", "milk" in shopping)
```

You should see:

```text
Items: ['rice', 'milk', 'tea']
Count: 3
Has milk: True
```

Debugging prompt:

```text
When a list has fewer items than expected, where should you look first?
```

### Debug 2: First Two Items

Goal:

```text
['rice', 'milk']
```

Broken code:

```python
items = ["rice", "milk", "apples", "tea"]

first_two = items[0:1]

print(first_two)
```

The slice stops before index `1`, so it only includes index `0`.

Fixed code:

```python
items = ["rice", "milk", "apples", "tea"]

first_two = items[0:2]

print(first_two)
```

You should see:

```text
['rice', 'milk']
```

Debugging prompt:

```text
Does the stop value mean "include this index" or "stop before this index"?
```

### Debug 3: Last Added Item

Goal:

```text
tea
```

Broken code:

```python
shopping = ["rice", "milk"]

shopping.append("tea")

print(shopping[3])
```

The list has three items, but the valid indexes are:

```text
0
1
2
```

Index `3` is one step too far.

Fixed code:

```python
shopping = ["rice", "milk"]

shopping.append("tea")

print(shopping[-1])
```

You should see:

```text
tea
```

Debugging prompt:

```text
When you want the last item, why is -1 safer than guessing the final positive index?
```

### Debug 4: Uneven Rows

Goal:

```text
Print the second item from each row if it exists.
If a row has no second item, print a helpful message.
```

Broken code:

```python
weekly = [
    ["rice", "milk"],
    ["apples"],
]

for row in weekly:
    print(row[1])
```

The first row has a second item.

The second row does not.

Fixed code:

```python
weekly = [
    ["rice", "milk"],
    ["apples"],
]

for row in weekly:
    if len(row) > 1:
        print(row[1])
    else:
        print("No second item in this row.")
```

You should see:

```text
milk
No second item in this row.
```

Debugging prompt:

```text
Before indexing into a row, how can len(row) help?
```

## Read the Docs

Today, revisit the official Python documentation for the collection tools you have been using.

List methods:

```text
https://docs.python.org/3/tutorial/datastructures.html#more-on-lists
```

Tuples:

```text
https://docs.python.org/3/tutorial/datastructures.html#tuples-and-sequences
```

Set types:

```text
https://docs.python.org/3/library/stdtypes.html#set-types-set-frozenset
```

You do not need to read every detail.

Look for these names:

```text
append
insert
remove
pop
sort
reverse
tuple
set
add
discard
```

Try this documentation-style list method practice:

```python
items = ["tea", "rice", "apples"]

items.sort()
print(items)

items.reverse()
print(items)
```

You should see:

```text
['apples', 'rice', 'tea']
['tea', 'rice', 'apples']
```

The useful reading habit is simple:

```text
Find the method name.
Read one small example.
Try the method on your own small list.
```

Documentation gets easier when you connect it to code you have already written.

## Mini Challenge

Create a file named `day-41/shopping_list_prep.py`.

Build a small shopping list preparation report.

Your program should use:

- a list named `shopping_list`
- a tuple named `store_visit`
- a set named `unique_items`
- a nested list named `aisles`

Rules:

```text
Start with three shopping items.
Add one more item.
Unpack the store tuple into store name and visit time.
Print the first shopping item.
Print the last shopping item.
Create unique_items from shopping_list.
Print unique_items in sorted order.
Loop through the aisle rows.
Print a final ready message.
```

One possible solution:

```python
shopping_list = ["rice", "milk", "apples"]
store_visit = ("Corner Market", "evening")
aisles = [
    ["produce", "apples"],
    ["pantry", "rice", "tea"],
]

shopping_list.append("tea")
unique_items = set(shopping_list)

store_name, visit_time = store_visit

print("Shopping list:", shopping_list)
print("Store:", store_name)
print("Time:", visit_time)
print("First item:", shopping_list[0])
print("Last item:", shopping_list[-1])
print("Unique items:", sorted(unique_items))

for index, aisle in enumerate(aisles, start=1):
    aisle_name = aisle[0]
    items = aisle[1:]
    print("Aisle", str(index) + ":", aisle_name, "-", ", ".join(items))

print("Ready for Day 42.")
```

You should see:

```text
Shopping list: ['rice', 'milk', 'apples', 'tea']
Store: Corner Market
Time: evening
First item: rice
Last item: tea
Unique items: ['apples', 'milk', 'rice', 'tea']
Aisle 1: produce - apples
Aisle 2: pantry - rice, tea
Ready for Day 42.
```

After it works, change the starting list:

```text
Add a repeated item.
Remove one item.
Change the store tuple.
Add another aisle row.
```

Run the program after each small change.

That is how tomorrow's project will grow too: one behavior at a time.

## Real-World Use

Collection practice is not only for examples.

A shopping list app needs several of today's habits:

- store the user's items in a list
- add a new item with `append()`
- remove an item after checking that it exists
- show each item with a loop
- count the items with `len()`
- show the first or last item with indexing
- show part of the list with slicing
- avoid duplicate display with a set when needed
- store a small fixed pair, such as store name and visit time, with a tuple
- organize grouped rows with nested lists when the data has sections

The app tomorrow will probably start with one main list.

That is enough for a useful first version:

```text
show the list
add an item
remove an item
quit the app
```

Extra collections become useful only when the program asks extra questions:

```text
Which item types are unique?
Which aisle does this item belong to?
Which store visit is planned?
Which required items are missing?
```

Good collection choice keeps the code close to the real problem.

## Recap

Today you practiced:

- creating and reading lists
- using index `0` for the first item
- using index `-1` for the last item
- slicing with `start:stop`
- remembering that the stop index is not included
- updating a list by index
- adding with `append()`
- inserting with `insert()`
- removing with `remove()` and `pop()`
- checking before removing
- looping through lists
- building a carried value such as `total` or `missing`
- reading nested lists one row at a time
- unpacking tuples
- creating sets from lists
- printing sets with `sorted()` for predictable display
- choosing a collection based on the job

The main practice questions were:

```text
Does order matter?
Will the collection change?
Are repeated values meaningful?
Do I need one item, part of the list, or every item?
Is this a fixed record?
Is this a unique group?
```

If you can answer those questions, you can usually start the problem.

## Lesson Checklist

Before moving on, check that you can:

- create a list with several strings
- print the first list item
- print the last list item
- take a slice from a list
- explain why `items[0:2]` gets two items
- update one list item by index
- add one item with `append()`
- insert one item with `insert()`
- remove one item with `remove()`
- remove and save one item with `pop()`
- loop through a list
- keep a total, count, or missing list while looping
- read a nested list row
- get one value from a nested list with two indexes
- create and unpack a tuple
- explain why tuples do not use `append()`
- create a set from a list
- explain why sets remove duplicates
- print a set with `sorted()`
- choose a list, tuple, or set for a simple problem

## Exercises

### Exercise 1

Predict the output.

```python
items = ["rice", "milk", "tea"]

print(items[0])
print(items[-1])
```

Then run it.

### Exercise 2

Fix the broken code.

Goal:

```text
Print milk.
```

Broken code:

```python
items = ["rice", "milk", "tea"]

print(items[2])
```

Which index should you use?

### Exercise 3

Predict the output.

```python
items = ["rice", "milk", "apples", "tea"]

print(items[0:2])
print(items[2:])
```

Then explain why `"apples"` appears in the second slice.

### Exercise 4

Create a list named `shopping` with three items.

Then:

```text
Replace the second item.
Add one item to the end.
Print the final list.
```

### Exercise 5

Start with:

```python
tasks = ["check fridge", "write list", "go to store"]
```

Insert `"grab bag"` at index `2`.

Print the final list.

### Exercise 6

Fix the broken code.

Goal:

```text
Remove "tea" only if it is in the list.
```

Broken code:

```python
items = ["rice", "milk"]

items.remove("tea")

print(items)
```

Use an `if` statement with `in`.

### Exercise 7

Write a loop that prints each item with a number.

Start with:

```python
items = ["rice", "milk", "tea"]
number = 1
```

The program should print:

```text
1 rice
2 milk
3 tea
```

Hint:

```text
Increase number inside the loop.
```

### Exercise 8

Start with:

```python
prices = [3, 5, 2]
```

Use a loop to calculate and print:

```text
Total: 10
```

### Exercise 9

Read this nested list:

```python
aisles = [
    ["produce", "apples"],
    ["pantry", "rice"],
    ["drinks", "tea"],
]
```

Write code that prints:

```text
rice
```

Use two indexes.

### Exercise 10

Loop through the same `aisles` list from Exercise 9.

For each row, print the aisle name and item:

```text
produce: apples
pantry: rice
drinks: tea
```

### Exercise 11

Create this tuple:

```python
store_visit = ("Corner Market", "morning")
```

Unpack it into `store_name` and `visit_time`.

Print:

```text
Corner Market in the morning
```

### Exercise 12

Fix the broken code.

Broken code:

```python
store_visit = ("Corner Market", "morning")

store_visit.append("Saturday")
```

The goal is to store three values that may grow later.

Should this be a tuple or a list?

### Exercise 13

Create a set from this list:

```python
items = ["rice", "tea", "rice", "milk", "tea"]
```

Print:

```text
Unique count: 3
Unique items: ['milk', 'rice', 'tea']
```

Use `sorted()`.

### Exercise 14

Choose `list`, `tuple`, or `set` for each situation.

```text
A shopping list where items can be added and removed.
A store visit with a store name and time.
A group of coupon codes where duplicates should disappear.
A playlist where song order matters.
A small coordinate pair such as x and y.
A group of usernames that must be unique.
```

Write one sentence explaining each answer.

### Exercise 15

Build a missing-item checker.

Start with:

```python
shopping_list = ["rice", "tea", "apples"]
required_items = {"rice", "milk", "apples"}
```

Rules:

```text
Create an empty list named missing.
Loop through sorted(required_items).
If the required item is not in shopping_list, append it to missing.
Print missing.
```

You should see:

```text
['milk']
```

### Exercise 16

Choose one program from today's lesson and add temporary debug prints.

Show:

```text
the collection before it changes
the value being checked inside the loop
the collection after it changes
```

Then remove the debug prints when the program makes sense.

Debugging is not a sign that you are behind. It is how you make the program visible.

## Tiny Win

You practiced collections as problem-solving tools.

That means you can now look at a small task and decide whether you need:

```text
a changing ordered list
a fixed record
a unique group
a row inside a bigger table
```

That is the skill behind tomorrow's project.

## Tomorrow

Tomorrow you will build:

```text
Day 42: Mini Project: Shopping List App
```

You already have the main pieces:

- a list to store shopping items
- `append()` to add an item
- `remove()` to remove an item
- `in` to check before removing
- a loop to show each item
- `len()` to count items
- clear collection choices when the program grows

The project will turn those pieces into one small program the user can actually use.

Before tomorrow, make sure this idea feels familiar:

```python
shopping_list = []

shopping_list.append("rice")
shopping_list.append("milk")

for item in shopping_list:
    print("-", item)
```

You should see:

```text
- rice
- milk
```

That is the heart of a shopping list app:

```text
start with a list
change the list
show the list clearly
```
