# Day 33: Slicing

**Focus:** Taking smaller pieces from lists and strings  
**You will practice:** using `start:stop`, leaving out the start or stop, copying a list with `[:]`, reading slice results, and debugging off-by-one mistakes  
**Estimated time:** 35-45 minutes

## Today's Goal

Today you will learn how to take part of a list.

Yesterday's topic was indexing. Indexing lets you get one item:

```python
colors = ["red", "green", "blue", "yellow"]

print(colors[1])
```

You should see:

```text
green
```

Slicing lets you get a section:

```python
colors = ["red", "green", "blue", "yellow"]

print(colors[1:3])
```

You should see:

```text
['green', 'blue']
```

By the end of this lesson, you should be able to:

- take a slice from the middle of a list
- explain why the stop position is not included
- leave out the start position
- leave out the stop position
- copy a list with `[:]`
- read simple string slices
- debug slices that are one item too short or one item too long

The main idea is:

```text
Indexing gets one item.
Slicing gets a smaller sequence.
```

## The Big Idea

A slice uses this shape:

```python
items[start:stop]
```

The slice starts at `start`.

The slice stops before `stop`.

That second part matters. The stop position is not included.

Example:

```python
names = ["Asha", "Ben", "Cara", "Dev", "Eli"]

print(names[1:4])
```

You should see:

```text
['Ben', 'Cara', 'Dev']
```

The slice starts at index `1`, so it includes `"Ben"`.

The slice stops before index `4`, so it does not include `"Eli"`.

It includes the items at indexes `1`, `2`, and `3`.

This can feel strange at first, but it is the same idea you already saw with `range()`.

Code:

```python
for number in range(1, 4):
    print(number)
```

You should see:

```text
1
2
3
```

`range(1, 4)` stops before `4`.

`names[1:4]` also stops before `4`.

## The Mental Model

When slicing feels confusing, think about the spaces between items.

Here is a list:

```python
scores = [80, 90, 75, 100]
```

The item indexes look like this:

```text
index:    0    1    2    3
items:   80   90   75   100
```

For slicing, it can help to imagine cut points around the items:

```text
cut:    0    1    2    3     4
        | 80 | 90 | 75 | 100 |
```

The slice `scores[1:3]` means:

```text
Start at cut 1.
Stop at cut 3.
Take what is between them.
```

Code:

```python
scores = [80, 90, 75, 100]

print(scores[1:3])
```

You should see:

```text
[90, 75]
```

The slice starts before `90` and stops before `100`.

That is why the stop number is not included.

You can also leave out one side of the slice.

Code:

```python
scores = [80, 90, 75, 100]

print(scores[:2])
print(scores[2:])
```

You should see:

```text
[80, 90]
[75, 100]
```

Read these as:

```text
scores[:2]    from the beginning up to, but not including, index 2
scores[2:]    from index 2 through the end
```

There is one more useful slice.

```python
scores = [80, 90, 75, 100]
copy_of_scores = scores[:]

print(copy_of_scores)
```

You should see:

```text
[80, 90, 75, 100]
```

That means:

```text
Start at the beginning.
Stop at the end.
Make a new list with the same items.
```

You will care more about that tomorrow, when you start updating lists.

## Try It Yourself

Create a file named:

```text
day-33/slicing_practice.py
```

Start with this list:

```python
scores = [82, 95, 71, 88, 100]

print("All scores:", scores)
print("First two:", scores[:2])
print("Middle three:", scores[1:4])
print("Last two:", scores[3:])
print("Copy:", scores[:])
```

You should see:

```text
All scores: [82, 95, 71, 88, 100]
First two: [82, 95]
Middle three: [95, 71, 88]
Last two: [88, 100]
Copy: [82, 95, 71, 88, 100]
```

Now try the same idea with words.

Code:

```python
tasks = ["read", "practice", "walk", "review", "rest"]

print("Morning:", tasks[:3])
print("Later:", tasks[3:])
```

You should see:

```text
Morning: ['read', 'practice', 'walk']
Later: ['review', 'rest']
```

Now try a string.

Code:

```python
word = "python"

print(word[0:2])
print(word[:3])
print(word[3:])
```

You should see:

```text
py
pyt
hon
```

Lists and strings can both be sliced because they are ordered sequences.

The result matches the kind of thing you sliced:

```text
Slicing a list gives a list.
Slicing a string gives a string.
```

## Common Mistake

### Mistake 1: Expecting The Stop Position To Be Included

This code runs, but it does not include `"Dev"`.

Broken code:

```python
names = ["Asha", "Ben", "Cara", "Dev"]

print(names[1:3])
```

You should see:

```text
['Ben', 'Cara']
```

The programmer wanted `"Ben"`, `"Cara"`, and `"Dev"`.

The problem is that index `3` is the stop position, so it is not included.

Fixed code:

```python
names = ["Asha", "Ben", "Cara", "Dev"]

print(names[1:4])
```

You should see:

```text
['Ben', 'Cara', 'Dev']
```

Another good fix is:

```python
names = ["Asha", "Ben", "Cara", "Dev"]

print(names[1:])
```

You should see:

```text
['Ben', 'Cara', 'Dev']
```

If you want the slice to continue to the end, leave the stop position empty.

### Mistake 2: Confusing One Item With A Slice

This gets one item:

```python
colors = ["red", "green", "blue"]

print(colors[1])
```

You should see:

```text
green
```

This gets a list containing one item:

```python
colors = ["red", "green", "blue"]

print(colors[1:2])
```

You should see:

```text
['green']
```

Both are correct, but they are different.

Use an index when you want one item.

Use a slice when you want a smaller list.

### Mistake 3: Thinking `[:]` Is The Same As `=`

This line does not copy the list:

```python
tasks = ["read", "practice", "rest"]
backup = tasks
```

It gives the same list another name.

This line makes a new list with the same items:

```python
tasks = ["read", "practice", "rest"]
backup = tasks[:]
```

That difference will matter more tomorrow, when you change list values.

For today, remember this simple rule:

```text
Use [:] when you want a basic copy of the whole list.
```

## Debug It

Here is a broken program.

Goal:

```text
First three: ['Asha', 'Ben', 'Cara']
```

Broken code:

```python
names = ["Asha", "Ben", "Cara", "Dev", "Eli"]

first_three = names[0:2]

print("First three:", first_three)
```

You should see:

```text
First three: ['Asha', 'Ben']
```

The slice stops before index `2`, so it only includes index `0` and index `1`.

Fixed code:

```python
names = ["Asha", "Ben", "Cara", "Dev", "Eli"]

first_three = names[0:3]

print("First three:", first_three)
```

You should see:

```text
First three: ['Asha', 'Ben', 'Cara']
```

An even cleaner version is:

```python
names = ["Asha", "Ben", "Cara", "Dev", "Eli"]

first_three = names[:3]

print("First three:", first_three)
```

When a slice is one item short, ask:

```text
Did I forget that the stop position is not included?
```

Here is another broken program.

Goal:

```text
Remaining tasks: ['walk', 'review', 'rest']
```

Broken code:

```python
tasks = ["read", "practice", "walk", "review", "rest"]

remaining_tasks = tasks[3:]

print("Remaining tasks:", remaining_tasks)
```

You should see:

```text
Remaining tasks: ['review', 'rest']
```

The programmer wanted everything after the first two tasks.

The first two tasks use indexes `0` and `1`, so the remaining tasks start at index `2`.

Fixed code:

```python
tasks = ["read", "practice", "walk", "review", "rest"]

remaining_tasks = tasks[2:]

print("Remaining tasks:", remaining_tasks)
```

You should see:

```text
Remaining tasks: ['walk', 'review', 'rest']
```

When debugging slices, write the indexes above the list:

```text
index:   0          1           2       3         4
tasks:   read       practice    walk    review    rest
```

Then ask:

```text
Where should the slice start?
Where should it stop?
Should the stop item be included? No.
```

## Read the Docs

Find Python's official documentation for common sequence operations:

```text
https://docs.python.org/3/library/stdtypes.html#common-sequence-operations
```

Look for this form:

```text
s[i:j]
```

For today, read that as:

```text
Take a slice from i up to, but not including, j.
```

The documentation has more forms than you need right now. Focus on these:

```python
items[1:4]
items[:4]
items[2:]
items[:]
```

You do not need slice steps today.

The useful habit is to connect documentation language to code you can read:

```text
s[i]      one item
s[i:j]    a slice
```

## Mini Challenge

Create a file named:

```text
day-33/playlist_preview.py
```

Build a small playlist preview.

Start with this list:

```python
songs = [
    "Morning Light",
    "Small Steps",
    "Open Window",
    "Steady Rain",
    "Notebook",
    "Goodnight",
]
```

Your program should print:

- the first two songs
- the middle two songs
- the last two songs
- a copy of the full playlist

One possible solution:

```python
songs = [
    "Morning Light",
    "Small Steps",
    "Open Window",
    "Steady Rain",
    "Notebook",
    "Goodnight",
]

first_two = songs[:2]
middle_two = songs[2:4]
last_two = songs[4:]
playlist_copy = songs[:]

print("First two:", first_two)
print("Middle two:", middle_two)
print("Last two:", last_two)
print("Copy:", playlist_copy)
```

You should see:

```text
First two: ['Morning Light', 'Small Steps']
Middle two: ['Open Window', 'Steady Rain']
Last two: ['Notebook', 'Goodnight']
Copy: ['Morning Light', 'Small Steps', 'Open Window', 'Steady Rain', 'Notebook', 'Goodnight']
```

Before running it, point to each slice and predict which songs it will include.

## Real-World Use

Slicing is useful when a program needs part of an ordered thing.

Examples:

- show the first few search results
- take the next group of tasks from a list
- preview the beginning of a message
- split a playlist into sections
- copy a list before making changes
- take the first few characters of a code or label

Slicing is also common when you want to show a small preview instead of the whole collection.

Example:

```python
messages = ["Welcome", "Check email", "Pack bag", "Start timer"]

preview = messages[:2]

print("Preview:", preview)
```

You should see:

```text
Preview: ['Welcome', 'Check email']
```

The full list is still there. The slice gives you the part you asked for.

## Recap

Today you learned that slicing takes part of a list or string.

You practiced:

- `items[start:stop]`
- stopping before the stop position
- `items[:stop]`
- `items[start:]`
- `items[:]`
- slicing strings
- checking slices for off-by-one mistakes

The most important rule is:

```text
The start position is included.
The stop position is not included.
```

That one rule explains most beginner slicing bugs.

## Lesson Checklist

Before moving on, check that you can:

- explain what `items[1:4]` means
- remember that the stop position is not included
- take the first few items with `items[:3]`
- take everything from a position with `items[2:]`
- copy a list with `items[:]`
- tell the difference between `items[1]` and `items[1:2]`
- slice a short string
- debug a slice that is one item too short
- write indexes above a list to reason about a slice

## Exercises

### Exercise 1

Predict the output.

```python
letters = ["a", "b", "c", "d", "e"]

print(letters[1:4])
```

Then run it. Which indexes were included?

### Exercise 2

Predict the output.

```python
numbers = [10, 20, 30, 40, 50]

print(numbers[:3])
print(numbers[3:])
```

### Exercise 3

Write a slice that prints only:

```text
['blue', 'yellow']
```

Start with:

```python
colors = ["red", "green", "blue", "yellow", "purple"]
```

### Exercise 4

Write a slice that prints the first three tasks.

Start with:

```python
tasks = ["wake", "wash", "eat", "pack", "leave"]
```

The result should be:

```text
['wake', 'wash', 'eat']
```

### Exercise 5

Write a slice that prints everything after the first two tasks.

Use the same list:

```python
tasks = ["wake", "wash", "eat", "pack", "leave"]
```

The result should be:

```text
['eat', 'pack', 'leave']
```

### Exercise 6

Read this program.

It prints the first four scores.

Code:

```python
scores = [5, 10, 15, 20, 25, 30]

first_four = scores[:4]

print(first_four)
```

This one is not actually broken. Explain why `:4` gives four items even though index `4` is not included.

### Exercise 7

Now debug this program.

It should print the first four scores, but it only prints three.

Broken code:

```python
scores = [5, 10, 15, 20, 25, 30]

first_four = scores[:3]

print(first_four)
```

Write the fixed slice.

### Exercise 8

Slice a string.

Start with:

```python
word = "keyboard"
```

Write slices that print:

```text
key
board
```

### Exercise 9

What is the difference between these two lines?

```python
items[2]
items[2:3]
```

Write a short answer in your own words.

### Exercise 10

Create a list of six foods.

Use slicing to print:

- the first two foods
- the last three foods
- a copy of the full list

Do not change the list yet. Tomorrow you will start changing lists on purpose.

## Tiny Win

You can now ask Python for a section of a list instead of pulling out one item at a time.

That makes lists easier to preview, split, copy, and reason about.

## Tomorrow

Tomorrow you will learn how to update lists.

Today you took pieces out of a list without changing the original list.

Tomorrow you will change list values on purpose:

```text
replace an item
add an item
remove an item
```

Slicing helps because it gives you a better sense of where items live before you start changing them.
