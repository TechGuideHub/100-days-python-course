# Day 48: Dictionaries of Lists

**Focus:** Storing lists under dictionary keys  
**You will practice:** creating dictionaries of lists, reading one list by key, looping through one list, appending to a list inside a dictionary, and making simple counts and totals  
**Estimated time:** 40-50 minutes

## Today's Goal

Today you will learn how to use a dictionary where the values are lists.

You already know that a dictionary stores values under keys:

```python
profile = {
    "name": "Maya",
    "city": "Pune"
}
```

You also know that a list stores several values:

```python
scores = [88, 92, 95]
```

A dictionary of lists combines those ideas:

```python
gradebook = {
    "Maya": [88, 92, 95],
    "Noah": [76, 84, 90],
    "Iris": [91, 89, 94]
}
```

Each key points to a list.

By the end of this lesson, you should be able to:

- create a dictionary where each value is a list
- read one list by using its key
- loop through one list inside a dictionary
- add a new item to a list inside a dictionary
- count how many items are in one list
- total the numbers in one list
- avoid confusing dictionary keys with list indexes
- recognize missing-key mistakes
- prepare for larger nested data structures

The main idea is:

```text
A dictionary can group several lists under clear labels.
```

This is useful when each label has its own collection.

## The Big Idea

A dictionary value can be any kind of value you already know.

It can be a string:

```python
profile = {
    "name": "Maya"
}
```

It can be a number:

```python
scores = {
    "Maya": 88
}
```

It can also be a list:

```python
gradebook = {
    "Maya": [88, 92, 95],
    "Noah": [76, 84, 90]
}

print(gradebook)
```

You should see:

```text
{'Maya': [88, 92, 95], 'Noah': [76, 84, 90]}
```

Read this dictionary one pair at a time:

```text
The key "Maya" has the value [88, 92, 95].
The key "Noah" has the value [76, 84, 90].
```

Those values are lists.

That means you can use list skills after you use the dictionary key.

Code:

```python
gradebook = {
    "Maya": [88, 92, 95],
    "Noah": [76, 84, 90]
}

print(gradebook["Maya"])
print(gradebook["Maya"][0])
```

You should see:

```text
[88, 92, 95]
88
```

The first line gets the whole list for `"Maya"`.

The second line gets the first item from Maya's list.

Read it in two steps:

```text
gradebook["Maya"]       get Maya's list
gradebook["Maya"][0]    get index 0 from Maya's list
```

The key chooses the list.

The index chooses an item inside that list.

## The Mental Model

Think of a dictionary of lists as labeled shelves.

```text
gradebook

Maya  -> [88, 92, 95]
Noah  -> [76, 84, 90]
Iris  -> [91, 89, 94]
```

The dictionary gives each shelf a label.

Each shelf holds a list.

When you write:

```python
gradebook["Iris"]
```

Python goes to the shelf labeled `"Iris"` and gives you the list:

```text
[91, 89, 94]
```

After that, it behaves like any other list.

You can loop through it:

```python
gradebook = {
    "Maya": [88, 92, 95],
    "Noah": [76, 84, 90],
    "Iris": [91, 89, 94]
}

for score in gradebook["Iris"]:
    print(score)
```

You should see:

```text
91
89
94
```

You can add to it:

```python
gradebook = {
    "Maya": [88, 92, 95],
    "Noah": [76, 84, 90]
}

gradebook["Maya"].append(98)

print(gradebook["Maya"])
```

You should see:

```text
[88, 92, 95, 98]
```

This line has two parts:

```python
gradebook["Maya"].append(98)
```

Read it as:

```text
Find Maya's list.
Append 98 to that list.
```

The dictionary is not storing one score for each student.

It is storing one list of scores for each student.

That is the pattern for today.

## Try It Yourself

Create a file named:

```text
day-48/dictionaries_of_lists.py
```

Write each step slowly. Run the file after each step.

### Step 1: Create A Gradebook

Code:

```python
gradebook = {
    "Maya": [88, 92, 95],
    "Noah": [76, 84, 90],
    "Iris": [91, 89, 94]
}

print(gradebook)
```

You should see:

```text
{'Maya': [88, 92, 95], 'Noah': [76, 84, 90], 'Iris': [91, 89, 94]}
```

Each key is a student's name.

Each value is a list of that student's scores.

### Step 2: Read One List By Key

Code:

```python
gradebook = {
    "Maya": [88, 92, 95],
    "Noah": [76, 84, 90],
    "Iris": [91, 89, 94]
}

maya_scores = gradebook["Maya"]

print(maya_scores)
print("First score:", maya_scores[0])
```

You should see:

```text
[88, 92, 95]
First score: 88
```

The key `"Maya"` gives you the list.

The index `0` gives you the first score inside that list.

### Step 3: Loop Through One List

Code:

```python
gradebook = {
    "Maya": [88, 92, 95],
    "Noah": [76, 84, 90],
    "Iris": [91, 89, 94]
}

for score in gradebook["Noah"]:
    print("Noah score:", score)
```

You should see:

```text
Noah score: 76
Noah score: 84
Noah score: 90
```

The loop is not looping through the whole dictionary.

It is looping through one list inside the dictionary:

```python
gradebook["Noah"]
```

### Step 4: Add To A List Inside A Dictionary

Code:

```python
gradebook = {
    "Maya": [88, 92, 95],
    "Noah": [76, 84, 90],
    "Iris": [91, 89, 94]
}

gradebook["Maya"].append(98)

print(gradebook["Maya"])
```

You should see:

```text
[88, 92, 95, 98]
```

This did not replace Maya's old scores.

It added one more score to Maya's list.

### Step 5: Count One Student's Scores

Code:

```python
gradebook = {
    "Maya": [88, 92, 95],
    "Noah": [76, 84, 90],
    "Iris": [91, 89, 94]
}

score_count = len(gradebook["Iris"])

print("Iris score count:", score_count)
```

You should see:

```text
Iris score count: 3
```

`len()` counts the items in Iris's list.

It does not count the whole dictionary.

### Step 6: Total One Student's Scores

Code:

```python
gradebook = {
    "Maya": [88, 92, 95],
    "Noah": [76, 84, 90],
    "Iris": [91, 89, 94]
}

total = 0

for score in gradebook["Maya"]:
    total = total + score

print("Maya total:", total)
```

You should see:

```text
Maya total: 275
```

This is the same loop-total pattern you have used before.

The only new part is where the list comes from:

```python
gradebook["Maya"]
```

### Step 7: Make A Playlist Dictionary

Code:

```python
playlists = {
    "focus": ["Lo-fi Morning", "Deep Work"],
    "walk": ["City Steps", "Fresh Air"],
    "rest": ["Soft Rain"]
}

playlists["focus"].append("Quiet Keys")

for song in playlists["focus"]:
    print("Focus song:", song)

print("Focus song count:", len(playlists["focus"]))
```

You should see:

```text
Focus song: Lo-fi Morning
Focus song: Deep Work
Focus song: Quiet Keys
Focus song count: 3
```

This has the same shape as the gradebook.

The keys are playlist names.

The values are lists of songs.

## Common Mistake

### Mistake 1: Forgetting That The Value Is A List

Broken code:

```python
gradebook = {
    "Maya": [88, 92]
}

gradebook["Maya"] = 95

print(gradebook)
```

You should see:

```text
{'Maya': 95}
```

This code runs, but it replaces the list with one number.

The old scores are gone.

Fixed code:

```python
gradebook = {
    "Maya": [88, 92]
}

gradebook["Maya"].append(95)

print(gradebook)
```

You should see:

```text
{'Maya': [88, 92, 95]}
```

Use `.append()` when you want to add one item to the list.

Use assignment when you really want to replace the whole value.

### Mistake 2: Appending To The Wrong Key

This code runs, but the task goes into the wrong list.

Broken code:

```python
project_tasks = {
    "todo": ["write outline"],
    "done": []
}

project_tasks["done"].append("draft introduction")

print(project_tasks)
```

You should see:

```text
{'todo': ['write outline'], 'done': ['draft introduction']}
```

The new task should be in `"todo"`, not `"done"`.

Fixed code:

```python
project_tasks = {
    "todo": ["write outline"],
    "done": []
}

project_tasks["todo"].append("draft introduction")

print(project_tasks)
```

You should see:

```text
{'todo': ['write outline', 'draft introduction'], 'done': []}
```

When a dictionary has several list values, check the key before appending.

### Mistake 3: Adding To A Missing Key

Broken code:

```python
shopping = {
    "produce": ["apples", "carrots"],
    "bakery": ["bread"]
}

shopping["frozen"].append("peas")

print(shopping)
```

This is broken because `"frozen"` is not a key in the dictionary yet.

Python raises a `KeyError`.

Fixed code:

```python
shopping = {
    "produce": ["apples", "carrots"],
    "bakery": ["bread"]
}

shopping["frozen"] = []
shopping["frozen"].append("peas")

print(shopping)
```

You should see:

```text
{'produce': ['apples', 'carrots'], 'bakery': ['bread'], 'frozen': ['peas']}
```

Create the list before appending to it.

### Mistake 4: Confusing Dictionary Keys With List Indexes

Broken code:

```python
gradebook = {
    "Maya": [88, 92],
    "Noah": [76, 84]
}

print(gradebook[0])
```

This is broken because the dictionary does not have a key named `0`.

Fixed code:

```python
gradebook = {
    "Maya": [88, 92],
    "Noah": [76, 84]
}

print(gradebook["Maya"])
print(gradebook["Maya"][0])
```

You should see:

```text
[88, 92]
88
```

Use a dictionary key to choose the list.

Use a list index after that if you need one item from the list.

## Debug It

Read each broken program. Find the dictionary-of-lists mistake, then compare it with the fixed version.

### Debug 1: The Wrong Habit Day

Goal:

```text
Monday habits: ['read', 'walk']
```

Broken code:

```python
habits = {
    "Monday": ["read"],
    "Tuesday": ["stretch"]
}

habits["Tuesday"].append("walk")

print("Monday habits:", habits["Monday"])
```

The problem:

```text
The code appends "walk" to Tuesday's list, but the goal is to add it to Monday's list.
```

Fixed code:

```python
habits = {
    "Monday": ["read"],
    "Tuesday": ["stretch"]
}

habits["Monday"].append("walk")

print("Monday habits:", habits["Monday"])
```

You should see:

```text
Monday habits: ['read', 'walk']
```

### Debug 2: The Missing Shopping Category

Goal:

```text
Cleaning items: ['soap']
```

Broken code:

```python
shopping = {
    "produce": ["apples"],
    "bakery": ["bread"]
}

shopping["cleaning"].append("soap")

print("Cleaning items:", shopping["cleaning"])
```

The problem:

```text
The key "cleaning" does not exist yet, so there is no list to append to.
```

Fixed code:

```python
shopping = {
    "produce": ["apples"],
    "bakery": ["bread"]
}

shopping["cleaning"] = []
shopping["cleaning"].append("soap")

print("Cleaning items:", shopping["cleaning"])
```

You should see:

```text
Cleaning items: ['soap']
```

### Debug 3: The Total Score

Goal:

```text
Maya total: 180
```

Broken code:

```python
grades = {
    "Maya": [88, 92],
    "Noah": [76, 84]
}

total = 0

for score in grades:
    total = total + score

print("Maya total:", total)
```

The problem:

```text
Looping through grades gives the dictionary keys, such as "Maya" and "Noah".
The program needs to loop through Maya's list of scores.
```

Fixed code:

```python
grades = {
    "Maya": [88, 92],
    "Noah": [76, 84]
}

total = 0

for score in grades["Maya"]:
    total = total + score

print("Maya total:", total)
```

You should see:

```text
Maya total: 180
```

When this structure feels confusing, ask two questions:

- Which key chooses the list?
- What do I want to do with that list?

## Read the Docs

Today, look at two official Python documentation pages:

```text
https://docs.python.org/3/library/stdtypes.html#mapping-types-dict
https://docs.python.org/3/tutorial/datastructures.html#more-on-lists
```

You do not need to read both pages fully.

Look for these ideas:

```text
d[key]
key in d
list.append(x)
len(s)
```

The documentation often uses short names.

Read them like this:

```text
d means some dictionary.
key means one key in that dictionary.
list.append(x) means add x to the end of a list.
len(s) means count the items in a collection.
```

In today's lesson, `d[key]` may give back a list:

```python
shopping = {
    "produce": ["apples", "carrots"],
    "bakery": ["bread"]
}

print(shopping["produce"])
print(len(shopping["produce"]))
```

You should see:

```text
['apples', 'carrots']
2
```

And `append()` can be used on that list:

```python
shopping = {
    "produce": ["apples", "carrots"],
    "bakery": ["bread"]
}

shopping["produce"].append("spinach")

print(shopping["produce"])
```

You should see:

```text
['apples', 'carrots', 'spinach']
```

The dictionary lookup happens first.

Then the list method runs.

## Mini Challenge

Create a file named:

```text
day-48/playlist_groups.py
```

Build a small playlist manager.

Start with this dictionary:

```python
playlists = {
    "focus": ["Lo-fi Morning", "Deep Work"],
    "walk": ["City Steps", "Fresh Air"],
    "rest": ["Soft Rain"]
}
```

Your program should:

- print the `"focus"` playlist
- add `"Quiet Keys"` to the `"focus"` playlist
- add `"Evening Stretch"` to the `"rest"` playlist
- loop through the `"focus"` playlist and print each song
- print the number of focus songs
- print the number of rest songs

One possible solution:

```python
playlists = {
    "focus": ["Lo-fi Morning", "Deep Work"],
    "walk": ["City Steps", "Fresh Air"],
    "rest": ["Soft Rain"]
}

print("Focus playlist:", playlists["focus"])

playlists["focus"].append("Quiet Keys")
playlists["rest"].append("Evening Stretch")

for song in playlists["focus"]:
    print("Focus song:", song)

print("Focus song count:", len(playlists["focus"]))
print("Rest song count:", len(playlists["rest"]))
```

You should see:

```text
Focus playlist: ['Lo-fi Morning', 'Deep Work']
Focus song: Lo-fi Morning
Focus song: Deep Work
Focus song: Quiet Keys
Focus song count: 3
Rest song count: 2
```

After it works, add a new playlist key named `"study"` with an empty list.

Then append two songs to `"study"` and print the new list.

## Real-World Use

Dictionaries of lists are useful when you have named groups.

Student grades:

```python
grades = {
    "Maya": [88, 92, 95],
    "Noah": [76, 84, 90]
}

print(grades["Maya"])
```

You should see:

```text
[88, 92, 95]
```

Playlist songs:

```python
playlists = {
    "focus": ["Lo-fi Morning", "Deep Work"],
    "rest": ["Soft Rain"]
}

print(playlists["rest"])
```

You should see:

```text
['Soft Rain']
```

Shopping categories:

```python
shopping = {
    "produce": ["apples", "carrots"],
    "bakery": ["bread"],
    "pantry": ["rice", "beans"]
}

shopping["pantry"].append("tea")

print(shopping["pantry"])
```

You should see:

```text
['rice', 'beans', 'tea']
```

Project tasks:

```python
project_tasks = {
    "todo": ["write outline", "collect notes"],
    "doing": ["draft lesson"],
    "done": ["choose topic"]
}

print("Todo count:", len(project_tasks["todo"]))
```

You should see:

```text
Todo count: 2
```

Weekly habits:

```python
habits = {
    "Monday": ["read", "walk"],
    "Tuesday": ["practice Python"],
    "Wednesday": ["review notes", "stretch"]
}

for habit in habits["Wednesday"]:
    print("Wednesday:", habit)
```

You should see:

```text
Wednesday: review notes
Wednesday: stretch
```

In each example, the dictionary answers:

```text
Which group do you want?
```

The list answers:

```text
What items are in that group?
```

That combination shows up in many beginner-friendly programs because it keeps related collections together without making one giant list.

## Recap

Today you learned that:

- a dictionary value can be a list
- a dictionary of lists groups several collections under clear keys
- `dictionary["key"]` can return a whole list
- `dictionary["key"][0]` gets one item from that list
- you can loop through one list with `for item in dictionary["key"]`
- you can add to one list with `dictionary["key"].append(value)`
- `len(dictionary["key"])` counts items in one list
- a loop can total numbers from one list
- missing keys cause `KeyError`
- appending to the wrong key changes the wrong list
- list indexes and dictionary keys are different kinds of lookup

The key pattern is:

```python
dictionary[key].append(new_item)
```

Read it as:

```text
Find the list for this key.
Add this item to that list.
```

## Lesson Checklist

Before moving on, check that you can:

- create a dictionary with at least two list values
- explain why each value is a list
- read one list by key
- read one item from a list inside a dictionary
- loop through one list inside a dictionary
- append to a list inside a dictionary
- count the items in one list with `len()`
- total numbers from one list with a loop
- create a new key with an empty list before appending to it
- spot when code replaces a list instead of appending to it
- spot when code appends to the wrong key
- explain why `dictionary[0]` is usually wrong

## Exercises

### Exercise 1

Create this dictionary:

```python
grades = {
    "Asha": [9, 10, 8],
    "Ben": [7, 8, 9]
}
```

Print Asha's list of grades.

### Exercise 2

Use the same `grades` dictionary.

Print Ben's first grade.

### Exercise 3

Use this dictionary:

```python
playlists = {
    "morning": ["Wake Up", "Fresh Start"],
    "evening": ["Slow Walk"]
}
```

Append one song to the `"evening"` playlist.

Print the evening playlist.

### Exercise 4

Use this dictionary:

```python
shopping = {
    "produce": ["apples", "spinach"],
    "bakery": ["bread"]
}
```

Loop through the `"produce"` list and print each item.

### Exercise 5

Use this dictionary:

```python
tasks = {
    "todo": ["read lesson", "write code"],
    "done": ["open editor"]
}
```

Print how many tasks are in `"todo"`.

### Exercise 6

Use this dictionary:

```python
grades = {
    "Asha": [9, 10, 8]
}
```

Use a loop to total Asha's grades.

Print:

```text
Total: 27
```

### Exercise 7

Create a dictionary named `habits`.

Use days of the week as keys.

Each value should be a list of habits for that day.

Print one day's habit list.

### Exercise 8

Add a new category to this shopping dictionary:

```python
shopping = {
    "produce": ["apples"],
    "bakery": ["bread"]
}
```

Create a key named `"drinks"` with an empty list.

Append `"water"` to `"drinks"`.

Print the drinks list.

### Exercise 9

Fix the broken code.

Broken code:

```python
grades = {
    "Asha": [9, 10]
}

grades["Asha"] = 8

print(grades)
```

The goal is to keep the old grades and add `8`.

### Exercise 10

Fix the broken code.

Broken code:

```python
project_tasks = {
    "todo": ["write notes"],
    "done": []
}

project_tasks["done"].append("practice examples")

print(project_tasks["todo"])
```

The goal is to add `"practice examples"` to `"todo"`.

### Exercise 11

Fix the broken code.

Broken code:

```python
shopping = {
    "produce": ["apples"]
}

shopping["snacks"].append("crackers")

print(shopping["snacks"])
```

The goal is to create a snacks list and add `"crackers"`.

### Exercise 12

Predict the output, then run the code.

```python
habits = {
    "Monday": ["read", "walk"],
    "Tuesday": ["practice Python"]
}

print(habits["Monday"][1])
print(len(habits["Tuesday"]))
```

### Exercise 13

Write a small report from this dictionary:

```python
grades = {
    "Maya": [88, 92, 95],
    "Noah": [76, 84, 90]
}
```

Your program should print:

```text
Maya has 3 scores.
Noah has 3 scores.
```

You may write two `print()` lines.

Looping through the whole dictionary is optional today.

### Exercise 14

Choose whether each line needs a dictionary key, a list index, or both.

```text
Get the whole focus playlist.
Get the first song in the focus playlist.
Add one song to the rest playlist.
Count the tasks in todo.
Get the whole Wednesday habit list.
```

Then write the Python expression for each one using your own dictionary name.

## Tiny Win

You can now store grouped collections with labels.

That means one variable can hold data like:

```text
each student and their scores
each playlist and its songs
each shopping category and its items
each day and its habits
```

This is a practical step toward real data because real programs often need both ideas:

```text
a label for the group
a list of values inside that group
```

## Tomorrow

Tomorrow is:

```text
Day 49: Nested Data
```

Today you used one nested shape:

```python
gradebook = {
    "Maya": [88, 92, 95],
    "Noah": [76, 84, 90]
}
```

A dictionary contains lists.

Tomorrow you will zoom out and practice reading nested data more generally.

That will include the same habit you used today:

```text
Read the structure one layer at a time.
```
