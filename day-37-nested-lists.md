# Day 37: Nested Lists

**Focus:** Storing lists inside lists  
**You will practice:** reading rows, using two indexes, looping through nested lists, working with small tables and grids, and avoiding index-level mistakes  
**Estimated time:** 40-50 minutes

## Today's Goal

Today you will learn how to put one list inside another list.

You already know that a list can store several values:

```python
tasks = ["read", "practice", "rest"]
```

A nested list stores several lists:

```python
weekly_tasks = [
    ["read", "practice"],
    ["walk", "review"],
    ["rest", "plan"],
]
```

By the end of this lesson, you should be able to:

- explain why nested lists exist
- read a nested list one row at a time
- get a whole inner list
- get one item from an inner list with two indexes
- loop through rows in a nested list
- print a small table or grid
- avoid common index-level mistakes
- notice when inner lists have different lengths

The main idea is:

> A nested list is a list where each item is another list.

This lets one variable hold simple grouped data, such as rows in a table, days in a schedule, or squares in a small grid.

## The Big Idea

Some data naturally comes in groups inside a bigger group.

Example:

```text
a week has days
each day can have tasks
a menu has sections
each section can have choices
a classroom has rows
each row can have seats
```

You could store each day in a separate variable:

```python
monday = ["read", "practice"]
tuesday = ["walk", "review"]
wednesday = ["rest", "plan"]
```

That works, but the days belong together. A nested list keeps the structure in one place.

Code:

```python
weekly_tasks = [
    ["read", "practice"],
    ["walk", "review"],
    ["rest", "plan"],
]

print(weekly_tasks)
```

You should see:

```text
[['read', 'practice'], ['walk', 'review'], ['rest', 'plan']]
```

The outside list holds the whole week.

Each inside list holds one day's tasks.

Read it like this:

```text
weekly_tasks
    row 0 -> ["read", "practice"]
    row 1 -> ["walk", "review"]
    row 2 -> ["rest", "plan"]
```

The word "row" is not special Python syntax. It is just a helpful way to talk about the inner lists.

You can get a whole inner list:

```python
weekly_tasks = [
    ["read", "practice"],
    ["walk", "review"],
    ["rest", "plan"],
]

print(weekly_tasks[0])
print(weekly_tasks[1])
```

You should see:

```text
['read', 'practice']
['walk', 'review']
```

`weekly_tasks[0]` gets the first inner list.

To get one item inside that inner list, use a second index:

```python
weekly_tasks = [
    ["read", "practice"],
    ["walk", "review"],
    ["rest", "plan"],
]

print(weekly_tasks[0][0])
print(weekly_tasks[0][1])
print(weekly_tasks[1][0])
```

You should see:

```text
read
practice
walk
```

Read `weekly_tasks[0][1]` in two steps:

```text
weekly_tasks[0]       get the first inner list
weekly_tasks[0][1]    from that inner list, get index 1
```

The first index chooses the inner list.

The second index chooses the item inside that inner list.

## The Mental Model

Think of a nested list as rows.

```python
seating = [
    ["Asha", "Ben", "Cara"],
    ["Dev", "Eli", "Fia"],
    ["Gia", "Hugo", "Iris"],
]
```

The outer list is the whole seating chart.

Each inner list is one row.

```text
row 0:  ["Asha", "Ben", "Cara"]
row 1:  ["Dev", "Eli", "Fia"]
row 2:  ["Gia", "Hugo", "Iris"]
```

Inside each row, the items still have indexes:

```text
row 0:  index 0 -> "Asha"   index 1 -> "Ben"    index 2 -> "Cara"
row 1:  index 0 -> "Dev"    index 1 -> "Eli"    index 2 -> "Fia"
row 2:  index 0 -> "Gia"    index 1 -> "Hugo"   index 2 -> "Iris"
```

So this code:

```python
seating = [
    ["Asha", "Ben", "Cara"],
    ["Dev", "Eli", "Fia"],
    ["Gia", "Hugo", "Iris"],
]

print(seating[1][2])
```

You should see:

```text
Fia
```

Why?

```text
seating[1] chooses row 1: ["Dev", "Eli", "Fia"]
seating[1][2] chooses index 2 from that row: "Fia"
```

Use this question when reading nested indexes:

```text
Which row first?
Which item inside that row second?
```

The two indexes are not one big number. They are two separate choices.

Code:

```python
grid = [
    ["top left", "top middle", "top right"],
    ["middle left", "center", "middle right"],
    ["bottom left", "bottom middle", "bottom right"],
]

print(grid[0][0])
print(grid[1][1])
print(grid[2][2])
```

You should see:

```text
top left
center
bottom right
```

This is enough grid thinking for today. You do not need matrix math. You only need to read the structure carefully.

## Try It Yourself

Create a file named:

```text
day-37/nested_lists.py
```

Start with a small schedule.

Code:

```python
schedule = [
    ["math", "reading"],
    ["science", "art"],
    ["history", "music"],
]

print(schedule)
```

You should see:

```text
[['math', 'reading'], ['science', 'art'], ['history', 'music']]
```

Now print one whole row.

Code:

```python
schedule = [
    ["math", "reading"],
    ["science", "art"],
    ["history", "music"],
]

print("First day:", schedule[0])
print("Second day:", schedule[1])
```

You should see:

```text
First day: ['math', 'reading']
Second day: ['science', 'art']
```

Now print one subject from inside a row.

Code:

```python
schedule = [
    ["math", "reading"],
    ["science", "art"],
    ["history", "music"],
]

print("First subject on first day:", schedule[0][0])
print("Second subject on first day:", schedule[0][1])
print("First subject on second day:", schedule[1][0])
```

You should see:

```text
First subject on first day: math
Second subject on first day: reading
First subject on second day: science
```

Now loop through the rows.

Code:

```python
schedule = [
    ["math", "reading"],
    ["science", "art"],
    ["history", "music"],
]

for day in schedule:
    print("Day:", day)
```

You should see:

```text
Day: ['math', 'reading']
Day: ['science', 'art']
Day: ['history', 'music']
```

In this loop, `day` is one inner list at a time.

Now loop through each row and each item.

Code:

```python
schedule = [
    ["math", "reading"],
    ["science", "art"],
    ["history", "music"],
]

for day in schedule:
    for subject in day:
        print(subject)
```

You should see:

```text
math
reading
science
art
history
music
```

This is a nested loop:

```text
The outer loop gets one row.
The inner loop gets one item from that row.
```

Finally, print each row on one line.

Code:

```python
schedule = [
    ["math", "reading"],
    ["science", "art"],
    ["history", "music"],
]

for day in schedule:
    print(day[0], "and", day[1])
```

You should see:

```text
math and reading
science and art
history and music
```

This works because every row has two items.

## Common Mistake

### Mistake 1: Using One Index When You Need Two

This code runs, but it prints a whole inner list.

Broken code:

```python
seating = [
    ["Asha", "Ben"],
    ["Cara", "Dev"],
]

print("Name:", seating[0])
```

You should see:

```text
Name: ['Asha', 'Ben']
```

The programmer wanted one name, but `seating[0]` means the whole first row.

Fixed code:

```python
seating = [
    ["Asha", "Ben"],
    ["Cara", "Dev"],
]

print("Name:", seating[0][0])
```

You should see:

```text
Name: Asha
```

Use one index for a row. Use two indexes for an item inside a row.

### Mistake 2: Using Too Many Indexes

Broken code:

```python
seating = [
    ["Asha", "Ben"],
    ["Cara", "Dev"],
]

print(seating[0][1][0])
```

`seating[0][1]` gets the string `"Ben"`.

Adding `[0]` after that asks for the first character of the string, so this code prints:

```text
B
```

Python allows it because strings can be indexed. But it is probably not what the programmer meant.

Fixed code:

```python
seating = [
    ["Asha", "Ben"],
    ["Cara", "Dev"],
]

print(seating[0][1])
```

You should see:

```text
Ben
```

Stop indexing when you have reached the value you wanted.

### Mistake 3: Reversing Row And Item

This code runs, but it chooses the wrong value.

Broken code:

```python
grid = [
    ["top left", "top right"],
    ["bottom left", "bottom right"],
]

print(grid[0][1])
```

You should see:

```text
top right
```

If the goal was `"bottom left"`, the row and item indexes are reversed.

Fixed code:

```python
grid = [
    ["top left", "top right"],
    ["bottom left", "bottom right"],
]

print(grid[1][0])
```

You should see:

```text
bottom left
```

Read nested indexes from left to right:

```text
grid[1][0]
row 1 first
item 0 inside that row second
```

### Mistake 4: Assuming Every Row Has The Same Length

Some nested lists are uneven.

Code:

```python
task_groups = [
    ["read", "practice"],
    ["walk"],
    ["review", "plan", "rest"],
]

for group in task_groups:
    print(group)
```

You should see:

```text
['read', 'practice']
['walk']
['review', 'plan', 'rest']
```

This is allowed. Python does not require every inner list to have the same length.

But this code is broken:

```python
task_groups = [
    ["read", "practice"],
    ["walk"],
    ["review", "plan", "rest"],
]

for group in task_groups:
    print(group[1])
```

The second group has only one item, so `group[1]` does not exist for that row.

Fixed code:

```python
task_groups = [
    ["read", "practice"],
    ["walk"],
    ["review", "plan", "rest"],
]

for group in task_groups:
    if len(group) > 1:
        print(group[1])
    else:
        print("No second item")
```

You should see:

```text
practice
No second item
plan
```

When inner lists may be uneven, check the length before using a specific index.

## Debug It

Here is a broken program.

Goal:

```text
Center: empty
```

Broken code:

```python
board = [
    ["empty", "empty", "empty"],
    ["empty", "empty", "empty"],
    ["empty", "empty", "empty"],
]

print("Center:", board[1])
```

The problem is the index level.

`board[1]` gets the whole middle row:

```text
['empty', 'empty', 'empty']
```

To get the center item, choose row `1`, then item `1` inside that row.

Fixed code:

```python
board = [
    ["empty", "empty", "empty"],
    ["empty", "empty", "empty"],
    ["empty", "empty", "empty"],
]

print("Center:", board[1][1])
```

You should see:

```text
Center: empty
```

Here is another broken program.

Goal:

```text
Seat: Cara
```

Broken code:

```python
rows = [
    ["Asha", "Ben"],
    ["Cara", "Dev"],
]

print("Seat:", rows[0][1])
```

You should see:

```text
Seat: Ben
```

The code runs, but it uses the wrong row.

`"Cara"` is in row `1`, item `0`.

Fixed code:

```python
rows = [
    ["Asha", "Ben"],
    ["Cara", "Dev"],
]

print("Seat:", rows[1][0])
```

You should see:

```text
Seat: Cara
```

When nested list code prints the wrong value, write the row numbers first:

```text
row 0: ["Asha", "Ben"]
row 1: ["Cara", "Dev"]
```

Then write the item numbers inside the row:

```text
row 1 item 0 -> "Cara"
```

That usually reveals the mistake.

## Read the Docs

Find Python's official tutorial section about lists:

```text
https://docs.python.org/3/tutorial/introduction.html#lists
```

Look for examples where a list contains other lists.

The documentation may show a nested list like this:

```python
letters = [["a", "b"], ["c", "d"]]
```

For today, read it in layers:

```text
letters is the outer list.
letters[0] is the first inner list.
letters[0][1] is one item inside the first inner list.
```

Try this small documentation-style example:

```python
letters = [["a", "b"], ["c", "d"]]

print(letters[0])
print(letters[0][1])
print(letters[1][0])
```

You should see:

```text
['a', 'b']
b
c
```

You do not need more than two levels today.

Nested lists can go deeper, but beginner code is easier to read when the structure stays small and named clearly.

## Mini Challenge

Create a file named:

```text
day-37/classroom_rows.py
```

Build a small classroom seating chart.

Start with this nested list:

```python
rows = [
    ["Asha", "Ben", "Cara"],
    ["Dev", "Eli", "Fia"],
    ["Gia", "Hugo", "Iris"],
]
```

Your program should:

- print the first row
- print the second student in the first row
- print the last student in the last row
- loop through each row and print the row
- loop through each row and each student, printing every student name

One possible solution:

```python
rows = [
    ["Asha", "Ben", "Cara"],
    ["Dev", "Eli", "Fia"],
    ["Gia", "Hugo", "Iris"],
]

print("First row:", rows[0])
print("Second student in first row:", rows[0][1])
print("Last student in last row:", rows[-1][-1])

for row in rows:
    print("Row:", row)

for row in rows:
    for student in row:
        print("Student:", student)
```

You should see:

```text
First row: ['Asha', 'Ben', 'Cara']
Second student in first row: Ben
Last student in last row: Iris
Row: ['Asha', 'Ben', 'Cara']
Row: ['Dev', 'Eli', 'Fia']
Row: ['Gia', 'Hugo', 'Iris']
Student: Asha
Student: Ben
Student: Cara
Student: Dev
Student: Eli
Student: Fia
Student: Gia
Student: Hugo
Student: Iris
```

Before running it, point to each index and say what it chooses.

## Real-World Use

Nested lists are useful when your data has simple rows.

Examples:

- a weekly schedule where each day has tasks
- a small menu where each section has options
- a seating chart where each row has names
- a board game where each row has squares
- a grade book where each student has a few scores
- a table where each row has related values

Example:

```python
grade_book = [
    ["Asha", 9, 10],
    ["Ben", 7, 8],
    ["Cara", 10, 10],
]

for student in grade_book:
    name = student[0]
    first_score = student[1]
    second_score = student[2]

    print(name, "scores:", first_score, second_score)
```

You should see:

```text
Asha scores: 9 10
Ben scores: 7 8
Cara scores: 10 10
```

This is a simple table:

```text
name   score 1   score 2
Asha   9         10
Ben    7         8
Cara   10        10
```

Nested lists are not always the best structure for named information. Later, dictionaries will make examples like this easier to read.

For now, nested lists are useful because they let you practice a simple idea:

```text
one collection can hold smaller collections
```

## Recap

Today you learned that:

- a nested list is a list inside another list
- the outer list holds the whole structure
- each inner list can act like a row
- one index gets one inner list
- two indexes get one item inside an inner list
- `items[0][1]` means row `0`, then item `1`
- a loop through a nested list gives you one inner list at a time
- a nested loop can visit every item inside every row
- inner lists can have different lengths
- uneven inner lists need careful length checks before indexing

The key reading habit is:

```text
Read nested indexes from left to right.
Choose the row first.
Choose the item inside the row second.
```

## Lesson Checklist

Before moving on, check that you can:

- create a list that contains other lists
- explain which list is the outer list
- explain which lists are inner lists
- get the first inner list with one index
- get one item with two indexes
- read `rows[1][0]` out loud in two steps
- loop through rows in a nested list
- use a nested loop to print every item
- spot when code prints a whole row instead of one item
- avoid adding an extra index after reaching the value you wanted
- check `len()` before indexing into uneven inner lists

## Exercises

### Exercise 1

Predict the output.

```python
groups = [
    ["red", "blue"],
    ["green", "yellow"],
]

print(groups[0])
print(groups[1])
```

Then run it.

### Exercise 2

Predict the output.

```python
groups = [
    ["red", "blue"],
    ["green", "yellow"],
]

print(groups[0][1])
print(groups[1][0])
```

Then run it.

### Exercise 3

Create a nested list named `meals`.

It should hold three inner lists:

```text
breakfast foods
lunch foods
dinner foods
```

Put two foods in each inner list.

Print the whole nested list.

### Exercise 4

Use your `meals` list.

Print:

- the first meal list
- the first food in the first meal list
- the second food in the third meal list

### Exercise 5

Predict the output.

```python
board = [
    ["x", "o", "x"],
    ["o", "x", "o"],
    ["x", "empty", "o"],
]

print(board[2][1])
```

Which row is chosen first?

Which item is chosen second?

### Exercise 6

Loop through the rows.

Start with:

```python
rows = [
    ["Asha", "Ben"],
    ["Cara", "Dev"],
    ["Eli", "Fia"],
]
```

Write a `for` loop that prints each row.

### Exercise 7

Use the same `rows` list.

Write a nested loop that prints every name on its own line.

### Exercise 8

Fix this program.

Broken code:

```python
rows = [
    ["Asha", "Ben"],
    ["Cara", "Dev"],
]

print("Student:", rows[1])
```

The goal is:

```text
Student: Cara
```

### Exercise 9

Fix this program.

Broken code:

```python
rows = [
    ["Asha", "Ben"],
    ["Cara", "Dev"],
]

print(rows[0][1][0])
```

The goal is:

```text
Ben
```

Remove the extra index.

### Exercise 10

Work with an uneven nested list.

Start with:

```python
task_groups = [
    ["read", "practice"],
    ["walk"],
    ["review", "plan", "rest"],
]
```

Write a loop that prints each group and its length.

You should see:

```text
['read', 'practice'] has 2 items
['walk'] has 1 items
['review', 'plan', 'rest'] has 3 items
```

### Exercise 11

Use the same `task_groups` list.

Write a loop that prints the second item only when the group has a second item.

If it does not, print:

```text
No second item
```

### Exercise 12

Create a small table of products.

Start with:

```python
products = [
    ["notebook", 3],
    ["pencil", 1],
    ["folder", 2],
]
```

Loop through the table and print:

```text
notebook costs 3
pencil costs 1
folder costs 2
```

Use clear variable names inside the loop:

```python
for product in products:
```

Then get the name and price with indexes.

## Tiny Win

You can now read a list that contains smaller lists.

That is an important step because real data often has shape. It is not always one flat row of values. Sometimes it is rows, groups, sections, days, or small tables.

The beginner win is not memorizing every possible nested structure. It is being able to pause, read the layers, and choose the right index one step at a time.

## Tomorrow

Tomorrow you will learn:

```text
Day 38: Tuples
```

Today's nested lists can change because lists are mutable. You can update an item inside an inner list:

```python
row = ["Asha", "Ben"]
row[1] = "Dev"

print(row)
```

You should see:

```text
['Asha', 'Dev']
```

Tomorrow's collection, the tuple, looks a little different and is usually used when a small group of values should stay together without being changed.
