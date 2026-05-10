# Day 35: Looping Through Lists

**Focus:** Visiting each item in a list with a `for` loop  
**You will practice:** loop variables, printing each item, using list items in sentences, counting while looping, filtering with `if`, and reading list loops clearly  
**Estimated time:** 40-50 minutes

## Today's Goal

Today you will learn how to loop through a list.

You already know that a list can hold several values:

```python
tasks = ["make bed", "pack bag", "start timer"]
```

You also know how to get one item by index:

```python
print(tasks[0])
```

That works when you want one specific item. But many programs need to do the same action for every item in a list.

By the end of this lesson, you should be able to:

- write a `for` loop that visits each item in a list
- choose a clear loop variable name
- print each item on its own line
- use each item inside a sentence
- count items while looping
- use `if` inside a list loop
- explain why list loops are useful

The main idea is:

> A list loop lets Python visit each item one at a time.

## The Big Idea

Imagine you have a shopping list:

```python
groceries = ["rice", "milk", "apples"]
```

You could print each item by index:

```python
groceries = ["rice", "milk", "apples"]

print(groceries[0])
print(groceries[1])
print(groceries[2])
```

You should see:

```text
rice
milk
apples
```

That works, but it has two problems.

First, you have to write one line for every item.

Second, if the list grows or shrinks, the code has to change.

A `for` loop is better:

```python
groceries = ["rice", "milk", "apples"]

for grocery in groceries:
    print(grocery)
```

You should see:

```text
rice
milk
apples
```

Read this line:

```python
for grocery in groceries:
```

as:

```text
For each grocery in the groceries list, run the indented code.
```

The loop visits `"rice"` first, then `"milk"`, then `"apples"`.

Each time through the loop, the variable `grocery` holds the current item.

## The Mental Model

Think of a list loop as a worker moving left to right through a row of items.

```text
List:       "rice"    "milk"    "apples"
Current:    grocery
```

On the first loop:

```text
grocery is "rice"
```

On the second loop:

```text
grocery is "milk"
```

On the third loop:

```text
grocery is "apples"
```

The loop variable is a temporary name for one item at a time.

Code:

```python
names = ["Asha", "Ben", "Cara"]

for name in names:
    print("Hello,", name)
```

You should see:

```text
Hello, Asha
Hello, Ben
Hello, Cara
```

The list is named `names`.

The loop variable is named `name`.

That naming is not required, but it is helpful:

```python
for name in names:
```

Read it as:

```text
for one name in the list of names
```

Here are more clear pairs:

```python
for task in tasks:
for score in scores:
for item in inventory:
for grocery in groceries:
```

The loop variable should describe one item from the list.

## Try It Yourself

Create a file named:

```text
day-35/list_loop_practice.py
```

Start with a list of tasks.

Code:

```python
tasks = ["make bed", "pack bag", "start timer"]

for task in tasks:
    print(task)
```

You should see:

```text
make bed
pack bag
start timer
```

Now make the output friendlier.

Code:

```python
tasks = ["make bed", "pack bag", "start timer"]

for task in tasks:
    print("Today I need to", task)
```

You should see:

```text
Today I need to make bed
Today I need to pack bag
Today I need to start timer
```

The loop variable can be used like any other variable inside the loop.

Try the same idea with names.

Code:

```python
names = ["Asha", "Ben", "Cara"]

for name in names:
    print(name, "is on the list.")
```

You should see:

```text
Asha is on the list.
Ben is on the list.
Cara is on the list.
```

Now try a list of numbers.

Code:

```python
scores = [8, 10, 7]

for score in scores:
    print("Score:", score)
```

You should see:

```text
Score: 8
Score: 10
Score: 7
```

The same loop shape works with strings, numbers, and other list items.

### Counting While Looping

Sometimes you want to count as you visit the items.

Code:

```python
tasks = ["make bed", "pack bag", "start timer"]
count = 0

for task in tasks:
    count = count + 1
    print(count, task)

print("Total tasks:", count)
```

You should see:

```text
1 make bed
2 pack bag
3 start timer
Total tasks: 3
```

The variable `count` starts at `0`.

Each time the loop runs, this line adds `1`:

```python
count = count + 1
```

You already know `len(tasks)` can count a whole list. Counting inside a loop is useful when you only want to count some items, or when you want to print a number beside each item.

### Filtering With `if`

A loop can also make a decision for each item.

Code:

```python
scores = [82, 45, 91, 60, 38]

for score in scores:
    if score >= 60:
        print("Passing score:", score)
```

You should see:

```text
Passing score: 82
Passing score: 91
Passing score: 60
```

This loop visits every score.

The `if` statement only prints scores that are at least `60`.

Here is the same idea with a simple inventory.

Code:

```python
inventory = ["pencil", "notebook", "pen", "charger", "pen"]

for item in inventory:
    if item == "pen":
        print("Found a pen.")
```

You should see:

```text
Found a pen.
Found a pen.
```

The loop checks each item one at a time.

## Common Mistake

### Mistake 1: Forgetting The Colon

Broken code:

```python
tasks = ["wash cup", "open notebook", "start timer"]

for task in tasks
    print(task)
```

The `for` line needs a colon at the end.

Fixed code:

```python
tasks = ["wash cup", "open notebook", "start timer"]

for task in tasks:
    print(task)
```

You should see:

```text
wash cup
open notebook
start timer
```

The colon tells Python that an indented block is coming next.

### Mistake 2: Forgetting To Indent The Loop Body

Broken code:

```python
names = ["Asha", "Ben", "Cara"]

for name in names:
print(name)
```

The line inside the loop must be indented.

Fixed code:

```python
names = ["Asha", "Ben", "Cara"]

for name in names:
    print(name)
```

You should see:

```text
Asha
Ben
Cara
```

Indentation is how Python knows what belongs inside the loop.

### Mistake 3: Printing The Whole List Instead Of The Loop Variable

This code runs, but it does not do what the programmer probably wanted.

Broken code:

```python
groceries = ["rice", "milk", "apples"]

for grocery in groceries:
    print(groceries)
```

You should see:

```text
['rice', 'milk', 'apples']
['rice', 'milk', 'apples']
['rice', 'milk', 'apples']
```

The loop runs three times, but each time it prints the whole list.

Fixed code:

```python
groceries = ["rice", "milk", "apples"]

for grocery in groceries:
    print(grocery)
```

You should see:

```text
rice
milk
apples
```

Inside the loop, use the loop variable when you want the current item.

### Mistake 4: Choosing A Confusing Loop Variable Name

This code works, but it is hard to read.

Code:

```python
scores = [8, 10, 7]

for banana in scores:
    print(banana)
```

You should see:

```text
8
10
7
```

Python does not care that the variable is named `banana`.

People reading the code do care.

A clearer version is:

```python
scores = [8, 10, 7]

for score in scores:
    print(score)
```

Use a loop variable name that describes one item from the list.

## Debug It

Here is a broken program.

Goal:

```text
Task: wash cup
Task: open notebook
Task: start timer
```

Broken code:

```python
tasks = ["wash cup", "open notebook", "start timer"]

for task in tasks:
print("Task:", tasks)
```

There are two problems.

The first problem is indentation. The `print()` line belongs inside the loop, so it must be indented.

The second problem is that the code prints `tasks`, the whole list, instead of `task`, the current item.

Fixed code:

```python
tasks = ["wash cup", "open notebook", "start timer"]

for task in tasks:
    print("Task:", task)
```

You should see:

```text
Task: wash cup
Task: open notebook
Task: start timer
```

Here is another broken program.

It is supposed to print only scores below `60`.

Broken code:

```python
scores = [82, 45, 91, 60, 38]

for score in scores:
    if scores < 60:
        print("Needs practice:", score)
```

The problem is here:

```python
if scores < 60:
```

`scores` is the whole list. The comparison should use `score`, the current item.

Fixed code:

```python
scores = [82, 45, 91, 60, 38]

for score in scores:
    if score < 60:
        print("Needs practice:", score)
```

You should see:

```text
Needs practice: 45
Needs practice: 38
```

When a list loop acts strangely, check these questions:

- Does the `for` line end with a colon?
- Is the loop body indented?
- Am I using the loop variable inside the loop?
- Am I accidentally using the whole list when I meant one item?

## Read the Docs

Python's official tutorial introduces `for` statements here:

```text
https://docs.python.org/3/tutorial/controlflow.html#for-statements
```

You do not need to understand every example on that page today.

For now, look for this shape:

```python
for word in words:
    print(word)
```

The names may change, but the idea is the same:

```text
for one_item in collection:
    do something with one_item
```

Try this small documentation-style example:

```python
words = ["cat", "window", "defenestrate"]

for word in words:
    print(word, len(word))
```

You should see:

```text
cat 3
window 6
defenestrate 12
```

This example prints each word and its length.

The useful reading habit is to identify the collection and the loop variable:

```text
words is the list.
word is one item from that list.
```

## Mini Challenge

Create a file named:

```text
day-35/shopping_list_report.py
```

Build a small shopping list report.

Start with this list:

```python
shopping_list = ["rice", "milk", "apples", "tea"]
```

Your program should:

- print each item on its own line
- print each item inside a sentence
- count the items while looping
- print the total count after the loop
- print a special message if the item is `"milk"`

One possible solution:

```python
shopping_list = ["rice", "milk", "apples", "tea"]
count = 0

for item in shopping_list:
    count = count + 1
    print("Buy:", item)

    if item == "milk":
        print("Check the fridge first.")

print("Total items:", count)
```

You should see:

```text
Buy: rice
Buy: milk
Check the fridge first.
Buy: apples
Buy: tea
Total items: 4
```

After it works, change the list.

Add another item by editing the list:

```python
shopping_list = ["rice", "milk", "apples", "tea", "bread"]
```

Run the program again.

The loop should handle the longer list without needing another `print()` line.

## Real-World Use

List loops are useful because programs often need to do the same thing to every item in a collection.

Examples:

- print every item in a shopping list
- show every task in a task app
- check every score in a quiz
- look through a small inventory
- greet every name in a guest list
- find items that match a condition
- count items that need attention

Without a loop, the program needs one line per item:

```python
print(tasks[0])
print(tasks[1])
print(tasks[2])
```

With a loop, the program can work with a list of almost any length:

```python
for task in tasks:
    print(task)
```

That is why list loops matter.

They let your code work with the collection, not just one hand-picked position.

## Recap

Today you learned how to loop through lists.

You practiced:

- writing `for item in items:`
- choosing a clear loop variable name
- printing each item
- using each item inside a sentence
- counting while looping
- using `if` inside a loop
- filtering list items by a condition
- debugging indentation, colon, and variable-name mistakes

The basic shape is:

```python
for item in items:
    print(item)
```

Read it as:

```text
For each item in the list, run the indented code.
```

The list keeps all the values.

The loop variable holds one value at a time.

## Lesson Checklist

Before moving on, check that you can:

- write a `for` loop that loops through a list
- explain what the loop variable does
- choose a loop variable name that describes one item
- print every item in a list
- use each item inside a sentence
- count items while a loop runs
- use `if` inside a list loop
- print only items that match a condition
- explain why the loop body must be indented
- explain why the `for` line needs a colon
- tell the difference between the list variable and the loop variable

## Exercises

### Exercise 1

Predict the output.

```python
colors = ["red", "green", "blue"]

for color in colors:
    print(color)
```

Then run it.

### Exercise 2

Create a list named `favorite_foods` with three foods.

Use a `for` loop to print each food on its own line.

### Exercise 3

Use each item inside a sentence.

Start with:

```python
names = ["Maya", "Noah", "Iris"]
```

Print:

```text
Maya is invited.
Noah is invited.
Iris is invited.
```

### Exercise 4

Loop through these scores:

```python
scores = [9, 7, 10, 8]
```

Print each score like this:

```text
Score: 9
```

### Exercise 5

Count while looping.

Start with:

```python
tasks = ["read", "practice", "walk", "review"]
count = 0
```

Increase `count` by `1` inside the loop.

After the loop, print:

```text
Task count: 4
```

### Exercise 6

Print only passing scores.

Start with:

```python
scores = [72, 55, 90, 40, 61]
```

Use a loop and an `if` statement to print only scores that are at least `60`.

### Exercise 7

Print only long task names.

Start with:

```python
tasks = ["read", "wash dishes", "walk", "practice Python"]
```

Use `len(task)` inside the loop.

Print only tasks longer than `6` characters.

### Exercise 8

Debug this program.

Broken code:

```python
items = ["pen", "notebook", "charger"]

for item in items
    print(item)
```

What is missing from the `for` line?

### Exercise 9

Debug this program.

Broken code:

```python
names = ["Asha", "Ben", "Cara"]

for name in names:
print("Hello,", name)
```

What line needs indentation?

### Exercise 10

Debug this program.

It should print one item at a time.

Broken code:

```python
groceries = ["rice", "milk", "apples"]

for grocery in groceries:
    print(groceries)
```

Which variable should be printed inside the loop?

### Exercise 11

Count items that match a condition.

Start with:

```python
inventory = ["pen", "pencil", "pen", "notebook", "pen"]
pen_count = 0
```

Loop through `inventory`.

Each time the item is `"pen"`, add `1` to `pen_count`.

After the loop, print:

```text
Pens: 3
```

### Exercise 12

Build a simple task report.

Start with:

```python
tasks = ["email teacher", "practice Python", "pack bag"]
```

Your program should print:

```text
Task 1: email teacher
Task 2: practice Python
Task 3: pack bag
Total tasks: 3
```

Use a counter that starts at `0` and increases inside the loop.

## Tiny Win

You can now make Python visit every item in a list.

That is one of the most practical patterns in beginner Python. Lists hold groups of values. Loops let you work through those groups without writing one line for each position.

## Tomorrow

Tomorrow you will learn more list methods.

Today you used a list loop to visit each item:

```python
for task in tasks:
    print(task)
```

Tomorrow you will add more tools for working with lists, such as counting, finding positions, sorting, and reversing.

The habit from today will still matter:

```text
Work with one item at a time.
Use clear names.
Read the list and the loop variable separately.
```
