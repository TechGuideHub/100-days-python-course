# Day 32: Indexing

**Focus:** Getting one item from a list by position  
**You will practice:** zero-based indexing, first and last items, `-1`, off-by-one mistakes, `IndexError`, and reading indexes carefully  
**Estimated time:** 40-50 minutes

## Today's Goal

Today you will learn how to get one specific item from a list.

In Day 31, you started using lists to store more than one value:

```python
tasks = ["study", "walk", "read"]
```

A list keeps its values in order. Indexing is how you ask for one value at a certain position.

By the end of this lesson, you should be able to:

- get the first item from a list
- get the second item from a list
- get the last item with `-1`
- explain why list indexes start at `0`
- avoid the common "one too far" mistake
- understand what `IndexError` means
- use `len()` carefully when thinking about indexes
- connect list indexing to string indexing

The main idea is:

> An index is a position number. In Python, the first position is `0`.

## The Big Idea

Lists store values in order.

Code:

```python
colors = ["red", "green", "blue"]

print(colors[0])
print(colors[1])
print(colors[2])
```

You should see:

```text
red
green
blue
```

The square brackets after the list name choose one item:

```python
colors[0]
```

Read that as:

```text
Get the item at index 0 from colors.
```

The part that feels strange at first is that Python starts counting positions at `0`, not `1`.

For this list:

```python
colors = ["red", "green", "blue"]
```

the indexes are:

```text
Index:   0        1        2
Value: "red"  "green"  "blue"
```

So:

```python
colors[0]
```

means the first item.

```python
colors[1]
```

means the second item.

```python
colors[2]
```

means the third item.

This is called zero-based indexing.

You do not need to love that name. You only need the habit:

```text
First item: index 0
Second item: index 1
Third item: index 2
```

## The Mental Model

Think of a list as a row of labeled boxes.

```text
Index:      0          1          2          3
Value:  "toast"   "eggs"   "fruit"   "tea"
```

The index is the label on the box.

Code:

```python
breakfast = ["toast", "eggs", "fruit", "tea"]

print("First:", breakfast[0])
print("Second:", breakfast[1])
print("Last:", breakfast[-1])
```

You should see:

```text
First: toast
Second: eggs
Last: tea
```

Positive indexes count from the left:

```text
0, 1, 2, 3
```

Negative indexes count from the right:

```text
-4, -3, -2, -1
```

For the same list:

```text
Index:       0          1          2          3
Value:   "toast"   "eggs"   "fruit"   "tea"
Index:      -4         -3         -2         -1
```

That means:

```python
breakfast[-1]
```

gets the last item.

Code:

```python
scores = [72, 85, 91, 68]

print(scores[0])
print(scores[-1])
print(scores[-2])
```

You should see:

```text
72
68
91
```

The most useful negative index is `-1`. It means "the last item" without needing to count how long the list is.

There is one more detail to keep close:

```python
len(scores)
```

tells you how many items are in the list, not the last index.

Code:

```python
scores = [72, 85, 91, 68]

print("Number of scores:", len(scores))
print("Last score:", scores[-1])
print("Last positive index:", len(scores) - 1)
```

You should see:

```text
Number of scores: 4
Last score: 68
Last positive index: 3
```

For a list with 4 items, the positive indexes are:

```text
0, 1, 2, 3
```

That is why the last positive index is `len(list_name) - 1`.

## Try It Yourself

Create a file named:

```text
day-32/indexing_practice.py
```

Code:

```python
todo = ["study Python", "drink water", "take a walk", "read"]

print("First task:", todo[0])
print("Second task:", todo[1])
print("Last task:", todo[-1])
```

Run the file from your course folder:

```bash
python day-32/indexing_practice.py
```

If your computer uses `py`, use:

```bash
py day-32/indexing_practice.py
```

If your computer uses `python3`, use:

```bash
python3 day-32/indexing_practice.py
```

You should see:

```text
First task: study Python
Second task: drink water
Last task: read
```

Now add two more lines:

```python
print("Third task:", todo[2])
print("Second from the end:", todo[-2])
```

You should see:

```text
Third task: take a walk
Second from the end: take a walk
```

Those two lines point to the same item from different directions.

Now try a different list.

Code:

```python
animals = ["cat", "dog", "rabbit", "horse", "fish"]

print(animals[0])
print(animals[4])
print(animals[-1])
```

You should see:

```text
cat
fish
fish
```

Notice that `animals[4]` works because this list has 5 items:

```text
Number of items: 5
Indexes: 0, 1, 2, 3, 4
```

The last index is one less than the number of items.

### A Light Connection To Strings

Strings can also be indexed because strings are ordered sequences of characters.

Code:

```python
word = "Python"

print(word[0])
print(word[1])
print(word[-1])
```

You should see:

```text
P
y
n
```

The idea is the same:

```text
Index 0 gets the first thing.
Index -1 gets the last thing.
```

For now, keep your attention on lists. You will use indexing with lists more often in the next few lessons.

## Common Mistake

### Mistake 1: Using `1` For The First Item

This code runs, but it does not print the first color.

Broken code:

```python
colors = ["red", "green", "blue"]

print("First color:", colors[1])
```

You should see:

```text
First color: green
```

The label says "First color," but `colors[1]` gets the second item.

Fixed code:

```python
colors = ["red", "green", "blue"]

print("First color:", colors[0])
```

You should see:

```text
First color: red
```

When you mean "first item," think:

```text
first item -> index 0
```

### Mistake 2: Using `len()` As The Last Index

This code is clearly broken.

Broken code:

```python
items = ["notebook", "pen", "charger"]

last_index = len(items)
print(items[last_index])
```

You should see an error like:

```text
IndexError: list index out of range
```

The list has 3 items, but the indexes are:

```text
0, 1, 2
```

There is no index `3`.

Fixed code:

```python
items = ["notebook", "pen", "charger"]

last_index = len(items) - 1
print(items[last_index])
```

You should see:

```text
charger
```

An even cleaner way to get the last item is:

```python
items = ["notebook", "pen", "charger"]

print(items[-1])
```

You should see:

```text
charger
```

### Mistake 3: Forgetting That The Index Must Exist

Broken code:

```python
names = ["Mina", "Omar"]

print(names[2])
```

You should see an error like:

```text
IndexError: list index out of range
```

The list has two items:

```text
Index:   0       1
Value: "Mina"  "Omar"
```

Index `2` is outside the list.

Fixed code:

```python
names = ["Mina", "Omar"]

print(names[1])
```

You should see:

```text
Omar
```

When you see `IndexError`, ask:

```text
How many items are in this list?
What indexes actually exist?
Am I accidentally using the item count as an index?
```

## Debug It

Here is a broken program.

It is supposed to print the third snack.

Broken code:

```python
snacks = ["apple", "crackers", "yogurt"]

print("Third snack:", snacks[3])
```

The list has three items, but Python's indexes are:

```text
0, 1, 2
```

So `snacks[3]` is one too far.

Fixed code:

```python
snacks = ["apple", "crackers", "yogurt"]

print("Third snack:", snacks[2])
```

You should see:

```text
Third snack: yogurt
```

Here is another program with a quieter bug.

It runs, but it prints the wrong player.

Broken code:

```python
players = ["Ari", "Bea", "Chen"]
player_number = 1

print("Player 1:", players[player_number])
```

You should see:

```text
Player 1: Bea
```

The variable name `player_number` sounds like a human-friendly number. Humans usually count:

```text
1, 2, 3
```

Python list indexes count:

```text
0, 1, 2
```

If the number is meant for a person to read, convert it before using it as an index.

Fixed code:

```python
players = ["Ari", "Bea", "Chen"]
player_number = 1
index = player_number - 1

print("Player 1:", players[index])
```

You should see:

```text
Player 1: Ari
```

This pattern is common:

```text
Human number 1 -> Python index 0
Human number 2 -> Python index 1
Human number 3 -> Python index 2
```

When a program chooses the item next to the one you wanted, that is often an off-by-one mistake.

## Read the Docs

Python's documentation describes lists and strings as sequence types.

Look up:

```text
https://docs.python.org/3/library/stdtypes.html#common-sequence-operations
```

You do not need to read the whole page. Look for these forms:

```text
s[i]
s[-i]
len(s)
```

The `s` means "some sequence." It could be a list, a string, or another ordered collection.

Code:

```python
letters = ["a", "b", "c", "d"]

print(letters[0])
print(letters[-1])
print(len(letters))
```

You should see:

```text
a
d
4
```

Documentation often uses short names like `s` and `i`.

For today, translate them like this:

```text
s means the sequence.
i means the index.
s[i] means get one item from the sequence at index i.
```

That is enough for now.

## Mini Challenge

Create a file named:

```text
day-32/playlist_picker.py
```

Build a tiny playlist preview.

Start with this list:

```python
songs = ["Morning Light", "Small Steps", "Open Road", "Night Window"]
```

Your program should print:

- the first song
- the second song
- the last song
- the second song from the end
- the number of songs
- the last positive index

The output should look like this:

```text
First song: Morning Light
Second song: Small Steps
Last song: Night Window
Second from the end: Open Road
Number of songs: 4
Last positive index: 3
```

Use indexing for the song names.

Use `len(songs)` for the number of songs.

Use `len(songs) - 1` for the last positive index.

Then add one more song to the list and run the program again. Check which lines still work without changes.

The line using `songs[-1]` should still find the last song. That is one reason `-1` is useful.

## Real-World Use

Indexing appears whenever order matters.

Examples:

- the first item in a shopping list
- the latest message in a small message list
- the last score in a game
- the selected option from a menu
- the first row of simple data
- the current page in a list of pages

Many programs use lists because the order carries meaning.

Code:

```python
temperatures = [71, 73, 70, 68]

morning_temperature = temperatures[0]
latest_temperature = temperatures[-1]

print("Morning:", morning_temperature)
print("Latest:", latest_temperature)
```

You should see:

```text
Morning: 71
Latest: 68
```

The list is small, but the idea is real:

```text
Use the index when the position matters.
```

## Recap

Today you learned that:

- an index is a position number
- Python lists start at index `0`
- `list_name[0]` gets the first item
- `list_name[1]` gets the second item
- `list_name[-1]` gets the last item
- `len(list_name)` gives the number of items
- the last positive index is `len(list_name) - 1`
- `IndexError` means you asked for a position that does not exist
- off-by-one mistakes happen when human counting and Python indexing get mixed together
- strings can be indexed too, but lists are today's main focus

The key habit:

```text
Before using an index, pause and count the positions Python's way.
```

## Lesson Checklist

Before moving on, check that you can:

- explain what an index is
- explain why the first list item uses index `0`
- get the first item from a list
- get the second item from a list
- get the last item with `-1`
- find the last positive index with `len(list_name) - 1`
- recognize an off-by-one mistake
- explain what `IndexError: list index out of range` means
- read a small index diagram from left to right
- convert a human-friendly number into a Python index by subtracting `1`

## Exercises

### Exercise 1

Predict the output before running the code.

```python
fruits = ["apple", "banana", "cherry"]

print(fruits[0])
print(fruits[2])
```

### Exercise 2

Write a list of three favorite foods.

Print the first food using index `0`.

### Exercise 3

Write a list of four cities.

Print:

- the first city
- the second city
- the last city

Use `-1` for the last city.

### Exercise 4

Predict the output.

```python
letters = ["a", "b", "c", "d"]

print(letters[-1])
print(letters[-2])
```

Then run it.

### Exercise 5

Fix this program.

Broken code:

```python
animals = ["cat", "dog", "rabbit"]

print("First animal:", animals[1])
```

It should print:

```text
First animal: cat
```

### Exercise 6

Fix this program.

Broken code:

```python
tools = ["hammer", "wrench", "saw"]

print(tools[3])
```

It should print:

```text
saw
```

### Exercise 7

Use `len()` to print the last positive index.

Start with:

```python
books = ["Poems", "Python Basics", "Clean Code", "Tiny Stories"]
```

The answer should be:

```text
3
```

### Exercise 8

Use the last positive index to print the last book.

Start with:

```python
books = ["Poems", "Python Basics", "Clean Code", "Tiny Stories"]
last_index = len(books) - 1
```

Print:

```text
Tiny Stories
```

### Exercise 9

Convert a human-friendly number into a Python index.

Start with:

```python
colors = ["red", "green", "blue"]
choice_number = 2
```

Create a variable named `choice_index` by subtracting `1` from `choice_number`.

Then print the chosen color.

You should see:

```text
green
```

### Exercise 10

Index a string lightly.

Start with:

```python
word = "lists"
```

Print:

- the first character
- the last character

Use the same indexing ideas you used with lists.

### Exercise 11

Debug this program.

It should print the second day.

Broken code:

```python
days = ["Monday", "Tuesday", "Wednesday"]

print("Second day:", days[2])
```

The correct answer is:

```text
Second day: Tuesday
```

### Exercise 12

Write a small menu list:

```python
options = ["Start", "Settings", "Quit"]
```

Print:

- `Option 1: Start`
- `Option 2: Settings`
- `Option 3: Quit`

Use indexes to get the values from the list.

Then write down why the printed option numbers are different from the Python indexes.

## Tiny Win

You can now ask a list for exactly one item.

That may seem small, but it changes how you read lists. A list is no longer just a group of values. It is an ordered group where each position can be named.

The beginner habit to keep:

```text
Count indexes from 0.
Use -1 for the last item.
Pause when len() appears near an index.
```

## Tomorrow

Tomorrow you will learn slicing.

Indexing gets one item:

```python
colors = ["red", "green", "blue", "yellow"]

print(colors[1])
```

You should see:

```text
green
```

Slicing gets part of a list:

```python
colors = ["red", "green", "blue", "yellow"]

print(colors[1:3])
```

You should see:

```text
['green', 'blue']
```

Do not worry about the `1:3` yet. Today, just notice the difference:

```text
Indexing chooses one item.
Slicing chooses a range of items.
```

