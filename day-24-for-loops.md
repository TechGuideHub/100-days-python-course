# Day 24: `for` Loops

**Focus:** Repeating code once for each item in a sequence  
**You will practice:** writing basic `for` loops, choosing loop variable names, reading indentation, and looping through lists and strings  
**Estimated time:** 35-45 minutes

## Today's Goal

Today you will learn how to repeat code once for each item in a group.

You already know that a `while` loop repeats while a condition stays true. A `for` loop has a different job. It moves through a sequence one item at a time.

Example:

```python
for name in ["Asha", "Ben", "Cara"]:
    print("Hello,", name)
```

You should see:

```text
Hello, Asha
Hello, Ben
Hello, Cara
```

By the end of this lesson, you should be able to:

- write a basic `for` loop
- loop through a short group of known items
- explain what the loop variable does
- identify which lines are inside the loop
- fix missing colons and indentation mistakes
- loop through the characters in a string
- choose a `for` loop when you already have the items to process

The main idea is:

> A `for` loop takes one item at a time from a sequence and runs the same indented block for each item.

Broken examples are labeled clearly. Study them first; run them only when you want to see the error or the wrong behavior.

## The Big Idea

Many repeated tasks are not about waiting until something changes. They are about handling a known group of things.

Examples:

```text
For each student, print a welcome message.
For each letter in a word, show the letter.
For each task in a list, mark the task.
```

A `while` loop asks:

```text
Should I keep going?
```

A `for` loop says:

```text
Give me the next item.
```

Here is a small program:

```python
tasks = ["wash cup", "pack bag", "start timer"]

for task in tasks:
    print("Next task:", task)

print("Morning ready.")
```

You should see:

```text
Next task: wash cup
Next task: pack bag
Next task: start timer
Morning ready.
```

The loop runs three times because there are three tasks.

You do not write a counter. You do not write an update line. Python moves through the group for you.

The final line is not indented, so it runs once after the loop finishes.

## The Mental Model

Think of a `for` loop as Python taking one item from a small stack.

The group is:

```python
["Asha", "Ben", "Cara"]
```

On the first trip through the loop, Python puts the first value into the loop variable:

```python
name = "Asha"
```

Then it runs the indented code:

```python
print("Hello,", name)
```

On the next trip, Python reuses the same variable name for the next value:

```python
name = "Ben"
```

The loop variable does not hold every item at once. It holds the current item.

In this loop, `name` is the loop variable:

```python
for name in ["Asha", "Ben", "Cara"]:
    print(name)
```

The basic shape is:

```text
for item in sequence:
    code that uses item
```

You choose the loop variable name. These two loops both work:

```python
for name in ["Asha", "Ben", "Cara"]:
    print(name)
```

```python
for person in ["Asha", "Ben", "Cara"]:
    print(person)
```

Clear names make loops easier to read.

Useful loop variable names usually answer this question:

```text
What is one item from this group?
```

Examples:

```python
for name in names:
    print(name)

for letter in word:
    print(letter)

for price in prices:
    print(price)
```

The plural name often stores the whole group. The singular name often stores one item from the group.

That is not a rule Python enforces. It is a habit that helps humans read the code.

## Try It Yourself

Create a file named:

```text
day-24/for_loop_practice.py
```

Code:

```python
colors = ["red", "green", "blue"]

for color in colors:
    print("I see", color)

print("Done.")
```

Before you run it, predict the output.

Run the file from your course folder:

```bash
python day-24/for_loop_practice.py
```

If your computer uses `py`, use:

```bash
py day-24/for_loop_practice.py
```

If your computer uses `python3`, use:

```bash
python3 day-24/for_loop_practice.py
```

You should see:

```text
I see red
I see green
I see blue
Done.
```

Now change the first line:

```python
colors = ["red", "green", "blue", "yellow"]
```

Run the program again. The loop body did not change, but the output became longer because the group has one more item.

Now try a different group:

```python
foods = ["rice", "beans", "soup"]

for food in foods:
    print("Today I can cook", food)
```

Notice the naming:

```text
foods means the whole group.
food means one item from the group.
```

That pattern is common:

```python
for name in names:
    print(name)

for word in words:
    print(word)

for question in questions:
    print(question)
```

## Common Mistake

### Mistake 1: Forgetting the colon

A `for` loop line ends with a colon.

Broken code:

```python
for name in ["Asha", "Ben", "Cara"]
    print(name)
```

Python expects the colon because the next indented block belongs to the loop.

Fixed code:

```python
for name in ["Asha", "Ben", "Cara"]:
    print(name)
```

### Mistake 2: Forgetting to indent the loop body

Broken code:

```python
for name in ["Asha", "Ben", "Cara"]:
print(name)
```

The line under the loop must be indented.

Fixed code:

```python
for name in ["Asha", "Ben", "Cara"]:
    print(name)
```

Indentation tells Python what repeats.

### Mistake 3: Indenting too much

This program prints the final message once:

```python
for name in ["Asha", "Ben", "Cara"]:
    print("Welcome,", name)

print("All welcomes sent.")
```

You should see:

```text
Welcome, Asha
Welcome, Ben
Welcome, Cara
All welcomes sent.
```

This program repeats the final message:

```python
for name in ["Asha", "Ben", "Cara"]:
    print("Welcome,", name)
    print("All welcomes sent.")
```

You should see:

```text
Welcome, Asha
All welcomes sent.
Welcome, Ben
All welcomes sent.
Welcome, Cara
All welcomes sent.
```

The second program is legal Python, but the indentation changes the meaning. The final message is indented, so it belongs to the loop.

When code repeats more than you expected, check indentation first.

### Mistake 4: Changing the loop variable and expecting the group to change

This program prints uppercase names:

```python
names = ["asha", "ben", "cara"]

for name in names:
    name = name.upper()
    print(name)
```

You should see:

```text
ASHA
BEN
CARA
```

But this does not change the original group:

```python
names = ["asha", "ben", "cara"]

for name in names:
    name = name.upper()

print(names)
```

You should see:

```text
['asha', 'ben', 'cara']
```

The loop variable is a temporary name for the current item. Changing it does not rewrite the list. You will learn how to update lists later.

### Mistake 5: Using a `while` loop when a `for` loop is simpler

This `while` loop prints each name by position:

```python
names = ["Asha", "Ben", "Cara"]
index = 0

while index < 3:
    print(names[index])
    index = index + 1
```

It works, but it has extra pieces to manage:

```text
start the index
check the index
update the index
```

The `for` loop says the idea more directly:

```python
names = ["Asha", "Ben", "Cara"]

for name in names:
    print(name)
```

Use a `for` loop when you already have the items you want to process. Use a `while` loop when the program should continue until a condition changes.

## Debug It

Here is a broken program.

It is supposed to print:

```text
Packing notebook
Packing charger
Packing pencil
Bag ready.
```

Broken code:

```python
items = ["notebook", "charger", "pencil"]

for item in items:
print("Packing", item)

print("Bag ready.")
```

The problem is indentation. The line after the `for` loop must be indented because it is the loop body.

Fixed code:

```python
items = ["notebook", "charger", "pencil"]

for item in items:
    print("Packing", item)

print("Bag ready.")
```

Now look at this program. It runs, but the output is wrong:

```python
items = ["notebook", "charger", "pencil"]

for item in items:
    print("Packing", item)
    print("Bag ready.")
```

You should see:

```text
Packing notebook
Bag ready.
Packing charger
Bag ready.
Packing pencil
Bag ready.
```

The final message should happen once, after the loop.

Fixed code:

```python
items = ["notebook", "charger", "pencil"]

for item in items:
    print("Packing", item)

print("Bag ready.")
```

When debugging a `for` loop, ask:

- What is the sequence?
- What is the loop variable?
- Which lines are indented under the loop?
- Which lines should run once after the loop?

If you are not sure what the loop variable contains, print it:

```python
items = ["notebook", "charger", "pencil"]

for item in items:
    print("Current item:", item)
    print("Packing", item)

print("Bag ready.")
```

Debugging a loop often means making the hidden movement visible.

## Read the Docs

Find Python's official tutorial section about `for` statements:

```text
https://docs.python.org/3/tutorial/controlflow.html#for-statements
```

The documentation describes `for` statements as a way to iterate over the items of a sequence.

For today, read those words this way:

```text
iterate means go through one item at a time
sequence means something Python can move through in order
```

You have already seen a list:

```python
["Asha", "Ben", "Cara"]
```

A string is also a sequence. It is a sequence of characters.

Code:

```python
for letter in "cat":
    print(letter)
```

You should see:

```text
c
a
t
```

You do not need every formal definition yet. Keep the practical idea:

```text
A for loop goes through a sequence one item at a time.
```

## Mini Challenge

Create a file named:

```text
day-24/spelling_helper.py
```

Build a tiny spelling helper.

Start with one word:

```python
word = "python"
```

Use a `for` loop to print each letter:

```python
word = "python"

for letter in word:
    print(letter)
```

Then improve the output:

```python
word = "python"

print("Spelling:", word)

for letter in word:
    print("Letter:", letter)

print("Word complete.")
```

You should see:

```text
Spelling: python
Letter: p
Letter: y
Letter: t
Letter: h
Letter: o
Letter: n
Word complete.
```

Now change the word to your own name or another short word. The loop should still work.

Think carefully about indentation:

```text
Should "Spelling:" print once or once for every letter?
Should "Word complete." print once or once for every letter?
```

The answer should guide where those lines belong.

## Real-World Use

`for` loops are common because real programs often work with collections of things.

Examples:

- for each email address, send one email
- for each file in a folder, check its name
- for each score, add it to a total
- for each product in a cart, show the price
- for each character in a password, check whether it is allowed
- for each line in a file, read the line
- for each question in a quiz, ask it

In these situations, the program already has the items. The job is to visit each one and do a clear action.

Later in the course, you will use `for` loops with lists, dictionaries, files, and data from outside a program.

For now, practice seeing the pattern:

```text
Here is a group.
Here is one item from the group.
Here is what to do with each item.
```

## Recap

Today you learned that:

- a `for` loop repeats once for each item in a sequence
- the loop variable holds the current item
- the loop variable is reused each time through the loop
- the indented block is the part that repeats
- unindented code after the loop runs once
- strings can be looped through one character at a time
- `for` loops are useful when you already have the items to process
- clear loop variable names make code easier to read

The key shape is:

```text
for item in sequence:
    code that uses item
```

Read it as:

```text
For each item in this sequence, do this action.
```

## Lesson Checklist

Before moving on, check that you can:

- write a `for` loop with a colon
- indent the loop body
- explain what the loop variable contains
- choose a clear loop variable name
- predict how many times a loop will run
- tell which lines repeat and which lines run after the loop
- loop through a list of strings
- loop through the letters in a string
- fix a `for` loop with missing indentation

## Exercises

### Exercise 1

Predict the output before running the code.

```python
animals = ["cat", "dog", "rabbit"]

for animal in animals:
    print(animal)
```

### Exercise 2

Predict the output.

```python
animals = ["cat", "dog", "rabbit"]

for animal in animals:
    print("Animal:", animal)

print("Done")
```

Which lines repeat? Which line runs once?

### Exercise 3

Write a `for` loop that prints each name:

```python
names = ["Asha", "Ben", "Cara", "Dev"]
```

The output should look like:

```text
Hello, Asha
Hello, Ben
Hello, Cara
Hello, Dev
```

### Exercise 4

Fix the missing colon.

Broken code:

```python
for color in ["red", "green", "blue"]
    print(color)
```

### Exercise 5

Fix the indentation.

Broken code:

```python
for snack in ["apple", "toast", "nuts"]:
print("Snack:", snack)
```

### Exercise 6

This program runs, but `"List finished."` prints too many times. Fix it so the message prints once.

```python
tasks = ["wash cup", "open notebook", "start timer"]

for task in tasks:
    print("Task:", task)
    print("List finished.")
```

### Exercise 7

Loop through this word:

```python
word = "loop"
```

Print each letter on its own line. Then change the word to:

```python
word = "Python"
```

Run the program again. What changed? What stayed the same?

### Exercise 8

Write a loop for these prices:

```python
prices = [3, 5, 2]
```

The program should print:

```text
Price: 3
Price: 5
Price: 2
```

Do not add the prices yet. Just practice visiting each item.

### Exercise 9

Now add the prices.

Start with:

```python
prices = [3, 5, 2]
total = 0
```

Inside the loop, add each price to `total`.

Hint:

```python
total = total + price
```

After the loop, print:

```text
Total: 10
```

Think about indentation. Should the final total print inside the loop or after it?

### Exercise 10

Choose the better first loop for each situation: `while` or `for`.

Situation:

```text
Keep asking for a password until it is correct.
```

Situation:

```text
Print a thank-you message for each name in a guest list.
```

Explain your choice for each one.

### Exercise 11

Debug this program by adding one line inside the loop:

```python
letters = "abc"

for letter in letters:
    print(letter)
```

Add:

```python
print("Current letter:", letter)
```

Run it. What does the debug line show you?

### Exercise 12

Write a small program that loops through three chores:

```python
chores = ["make bed", "wash plate", "pack bag"]
```

For each chore, print:

```text
Next chore: CHORE
```

After the loop, print:

```text
Morning ready.
```

## Tiny Win

You can now write a program that walks through a group of items without copying the same line again and again.

That is a real step forward. Your code can now work with many things, not just one thing.

## Tomorrow

Tomorrow you will learn `range()`.

Today, your `for` loops used sequences you could see:

```python
for name in ["Asha", "Ben", "Cara"]:
    print(name)
```

Tomorrow, you will use `range()` to create number sequences:

```python
for number in range(5):
    print(number)
```

That will help you repeat an action a specific number of times without writing each item by hand.
