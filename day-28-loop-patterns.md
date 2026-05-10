# Day 28: Loop Patterns

**Focus:** Recognizing reusable loop shapes  
**You will practice:** counting, accumulating totals, searching, validating input, repeating until done, and building output gradually  
**Estimated time:** 45-55 minutes

## Today's Goal

Today you will learn common patterns that appear inside loops.

You already know several loop tools:

- `while` loops
- avoiding infinite loops
- `for` loops
- `range()`
- looping through text
- `break`
- `continue`

Now the goal is to recognize the shape of a loop before you write it.

By the end of this lesson, you should be able to:

- use a loop to count repeated events
- use a loop to accumulate a total
- search through text with a loop
- validate input by asking again
- repeat a menu until the user is done
- build a string gradually
- choose a loop pattern for a small problem
- debug beginner mistakes in loop patterns

The main idea is:

> Many loops are familiar patterns with different details.

When you can name the pattern, the code becomes easier to plan.

## The Big Idea

A beginner often sees each loop as a separate puzzle.

Example:

```python
for letter in "python":
    print(letter)
```

Example:

```python
answer = input("Type yes: ")

while answer != "yes":
    answer = input("Type yes: ")
```

These loops do different jobs, but they are both built from a small set of habits:

- start with a useful value
- repeat one clear action
- update something if needed
- use the result after the loop

Here is a counting loop.

Code:

```python
word = "banana"
count = 0

for letter in word:
    count = count + 1

print("Letters:", count)
```

You should see:

```text
Letters: 6
```

Here is another counting loop.

Code:

```python
word = "banana"
vowels = 0

for letter in word:
    if letter == "a" or letter == "e" or letter == "i" or letter == "o" or letter == "u":
        vowels = vowels + 1

print("Vowels:", vowels)
```

You should see:

```text
Vowels: 3
```

The details changed, but the pattern stayed the same:

```text
Start a counter at 0.
Look at one item at a time.
Add 1 when something should count.
Use the counter after the loop.
```

Today you will practice six useful loop patterns:

- counting
- accumulating totals
- searching
- validating input
- repeating until done
- building output gradually

These patterns will appear again when you work with lists, dictionaries, files, projects, and tests.

## The Mental Model

Think of a loop as carrying one small piece of memory from one round to the next.

Sometimes it carries a count:

```python
count = 0
```

Sometimes it carries a total:

```python
total = 0
```

Sometimes it carries whether a search has succeeded:

```python
found = False
```

Sometimes it carries a growing piece of text:

```python
message = ""
```

That carried value is often the clue to the pattern.

### Counting

Use this when you want to know how many.

```text
Start count at 0.
For each item:
    If the item should be counted:
        Add 1 to count.
After the loop, use count.
```

### Accumulating

Use this when you want a total.

```text
Start total at 0.
For each number:
    Add the number to total.
After the loop, use total.
```

### Searching

Use this when you want to know whether something appears.

```text
Start found as False.
For each item:
    If this is the item:
        Set found to True.
        Stop early if there is no reason to keep searching.
After the loop, check found.
```

### Validating Input

Use this when the user must give an acceptable answer.

```text
Ask for input.
While the input is not acceptable:
    Explain the problem.
    Ask again.
Use the acceptable input.
```

### Repeating Until Done

Use this when the program should keep offering work until the user quits.

```text
Set choice to something that is not quit.
While choice is not quit:
    Do one round of work.
    Ask what to do next.
```

### Building Output

Use this when the program creates a new string piece by piece.

```text
Start result as an empty string.
For each piece:
    Add a new piece to result.
After the loop, use result.
```

When you are stuck, ask:

```text
Am I counting?
Adding up?
Searching?
Checking input?
Repeating a menu?
Building something step by step?
```

That question can turn a blank page into a plan.

## Try It Yourself

Create a file named:

```text
day-28/loop_patterns_practice.py
```

Start with a word.

Code:

```python
word = input("Type a word: ")
word = word.strip().lower()
```

### Step 1: Count Characters

Add a counter.

Code:

```python
count = 0

for letter in word:
    count = count + 1

print("Characters:", count)
```

Try this:

```text
apple
```

You should see:

```text
Characters: 5
```

### Step 2: Count One Specific Letter

Count how many times the letter `"a"` appears.

Code:

```python
a_count = 0

for letter in word:
    if letter == "a":
        a_count = a_count + 1

print("Letter a:", a_count)
```

Try this:

```text
banana
```

You should see:

```text
Letter a: 3
```

### Step 3: Search For A Letter

Search for the letter `"x"`.

Code:

```python
has_x = False

for letter in word:
    if letter == "x":
        has_x = True

if has_x:
    print("The word contains x.")
else:
    print("The word does not contain x.")
```

Try this:

```text
box
```

Then try:

```text
banana
```

### Step 4: Build A New String

Build a version of the word with dashes after each letter.

Code:

```python
spaced = ""

for letter in word:
    spaced = spaced + letter + "-"

print(spaced)
```

If the word is:

```text
cat
```

you should see:

```text
c-a-t-
```

The last dash is not polished yet. That is okay. Today the useful pattern is:

```text
Start with an empty string.
Add a little more each time.
```

You will learn cleaner ways to combine text later.

## Common Mistake

### Mistake 1: Starting The Carried Value Inside The Loop

Broken code:

```python
word = "banana"

for letter in word:
    count = 0
    count = count + 1

print(count)
```

You should see:

```text
1
```

The problem is that `count` resets to `0` every time through the loop.

Fixed code:

```python
word = "banana"
count = 0

for letter in word:
    count = count + 1

print(count)
```

You should see:

```text
6
```

If a value needs to remember progress, create it before the loop.

### Mistake 2: Printing Too Early

This code runs, but it prints the running count instead of one final report.

Broken code:

```python
word = "banana"
vowels = 0

for letter in word:
    if letter == "a":
        vowels = vowels + 1
    print("Vowels:", vowels)
```

You should see:

```text
Vowels: 0
Vowels: 1
Vowels: 1
Vowels: 2
Vowels: 2
Vowels: 3
```

That can be useful while debugging, but it is not the final answer.

Fixed code:

```python
word = "banana"
vowels = 0

for letter in word:
    if letter == "a":
        vowels = vowels + 1

print("Vowels:", vowels)
```

You should see:

```text
Vowels: 3
```

Indentation answers this question:

```text
Should this happen every time, or once after the loop?
```

### Mistake 3: Forgetting To Ask Again In An Input Loop

Broken code:

```python
answer = input("Type yes: ")

while answer != "yes":
    print("Please type yes.")
```

If the user does not type `"yes"` first, this loop cannot recover. The answer never changes.

Fixed code:

```python
answer = input("Type yes: ")

while answer != "yes":
    print("Please type yes.")
    answer = input("Type yes: ")
```

A validation loop must give the user another chance inside the loop.

### Mistake 4: Using The Wrong Starting Value

Broken code:

```python
total = 1

for number in range(1, 4):
    total = total + number

print(total)
```

You should see:

```text
7
```

But `1 + 2 + 3` should be `6`. The total started at `1`, so the program added an extra point before the loop even began.

Fixed code:

```python
total = 0

for number in range(1, 4):
    total = total + number

print(total)
```

You should see:

```text
6
```

For counting and adding, the usual starting value is `0`.

## Debug It

Here is a broken program. It should count digits in a piece of text.

Goal:

```text
Text: room 204
Digits: 3
```

Broken code:

```python
text = input("Text: ")

for character in text:
    digit_count = 0

    if character >= "0" and character <= "9":
        digit_count = digit_count + 1

print("Digits:", digit_count)
```

The bug is here:

```python
digit_count = 0
```

It is inside the loop, so the count restarts for every character.

Fixed code:

```python
text = input("Text: ")
digit_count = 0

for character in text:
    if character >= "0" and character <= "9":
        digit_count = digit_count + 1

print("Digits:", digit_count)
```

When a counting loop gives a number that is too small, ask:

```text
Did I reset the counter inside the loop?
```

Here is another broken program. It should keep asking for a number from `1` to `5`.

Broken code:

```python
choice = input("Choose a number from 1 to 5: ")

while choice < "1" or choice > "5":
    print("That is not from 1 to 5.")

print("You chose:", choice)
```

There are two problems.

First, the loop never asks again. If the first answer is invalid, `choice` never changes.

Second, the code is comparing strings with `<` and `>`. For single digits, that can look like it works, but it is a fragile habit when you mean choices.

A clear beginner-safe fix is to check the exact allowed text values.

Fixed code:

```python
choice = input("Choose a number from 1 to 5: ")

while choice != "1" and choice != "2" and choice != "3" and choice != "4" and choice != "5":
    print("That is not from 1 to 5.")
    choice = input("Choose a number from 1 to 5: ")

print("You chose:", choice)
```

This is longer than you might expect. That is fine. Clear code is a good first goal.

The validation pattern is:

```text
Ask once before the loop.
While the answer is invalid:
    explain the problem
    ask again
Use the valid answer after the loop.
```

## Read the Docs

Today, look up Python's documentation for `range()`.

You have already used `range()` to repeat a known number of times. While reading, look for examples like these:

```python
range(5)
range(1, 6)
range(2, 11, 2)
```

Connect each one to a loop pattern.

Code:

```python
for number in range(5):
    print(number)
```

This is useful when you need a fixed number of repeats.

Code:

```python
total = 0

for number in range(1, 6):
    total = total + number

print(total)
```

This is the accumulating pattern.

Code:

```python
for number in range(2, 11, 2):
    print(number)
```

This is counting with a step.

You do not need to memorize every detail today. Notice that `range()` is often the tool you reach for when the loop is about numbers or a known count.

## Mini Challenge

Create a file named:

```text
day-28/secret_word_helper.py
```

Build a small secret word helper.

The program should:

- ask for a word
- count how many letters it has
- count how many vowels it has
- check whether it contains the letter `"e"`
- build a hidden version where vowels become `"*"`
- print the final report

Example:

```text
Secret word: lemon

Letters: 5
Vowels: 2
Contains e: yes
Hidden word: l*m*n
```

Use these starting values:

```python
letter_count = 0
vowel_count = 0
contains_e = False
hidden_word = ""
```

Then use one loop:

```python
for letter in word:
```

Inside that loop, decide what each variable needs:

```text
letter_count counts every letter.
vowel_count counts only vowels.
contains_e remembers whether the search succeeded.
hidden_word grows one character at a time.
```

Try to write your own version before looking back at the earlier examples.

## Real-World Use

Loop patterns appear in ordinary programs all the time.

Counting:

```text
How many unread messages does the user have?
How many failed login attempts happened?
How many answers were correct?
```

Accumulating:

```text
What is the total price?
What is the final score?
How many minutes are on the playlist?
```

Searching:

```text
Does this username already exist?
Does this text contain a blocked word?
Did any answer match the correct answer?
```

Validating input:

```text
Ask until the name is not empty.
Ask until the menu choice is allowed.
Ask until the user confirms yes or no.
```

Repeating until done:

```text
Keep showing a menu until the user quits.
Keep taking orders until the customer is finished.
Keep playing rounds until the player stops.
```

Building output:

```text
Build a receipt line by line.
Create a cleaned version of a message.
Make a simple progress bar.
Hide part of a secret word.
```

The details change. The loop shapes repeat.

That is why patterns are useful: they help you recognize familiar structure inside new problems.

## Recap

Today you learned that loops often follow reusable patterns.

You practiced:

- counting with a counter
- accumulating with a total
- searching with a `found` flag
- validating input with a `while` loop
- repeating until the user chooses to stop
- building a string gradually
- placing starting values before the loop
- deciding what belongs inside the loop and what belongs after it

The most useful question is:

```text
What value does this loop carry from one round to the next?
```

If you can answer that, the loop is already easier to understand.

## Lesson Checklist

Before moving on, check that you can:

- explain why counters usually start before the loop
- write a loop that counts matching characters
- write a loop that adds numbers to a total
- use a boolean flag to remember whether something was found
- write a validation loop that asks again
- keep a menu running until the user chooses to quit
- build a new string one piece at a time
- spot when a value is reset in the wrong place
- decide whether a line should run inside the loop or after it

## Exercises

### Exercise 1

Predict the output.

```python
count = 0

for number in range(1, 5):
    count = count + 1

print(count)
```

Then run it. Why is the answer not `5`?

### Exercise 2

Write a loop that prints:

```text
1
2
3
4
5
```

Use `range()`.

### Exercise 3

Write a loop that adds the numbers from `1` through `10`.

Start with:

```python
total = 0
```

Print the total after the loop.

### Exercise 4

Ask the user for a word. Count how many times the letter `"s"` appears.

Test it with:

```text
mississippi
```

You should get:

```text
4
```

### Exercise 5

Ask the user for a word. Search for the letter `"q"`.

Print:

```text
Found q.
```

or:

```text
No q found.
```

Use a variable named:

```python
found_q
```

### Exercise 6

Write a validation loop.

Keep asking the user to type `"yes"` or `"no"` until they type one of those exact answers.

When the answer is valid, print:

```text
Answer accepted.
```

### Exercise 7

Write a menu loop with three choices:

```text
1. Print hello
2. Print Python
3. Quit
```

Keep showing the menu until the user chooses `"3"`.

Print this after the loop ends:

```text
Goodbye.
```

### Exercise 8

Build a simple line of stars.

Ask the user for a number from `1` to `5`. Then build a string with that many stars.

Example:

```text
How many stars? 4
****
```

You can keep this beginner-safe by checking exact text choices:

```python
if amount == "1":
    repeats = 1
```

Write the other choices the same way.

### Exercise 9

Debug this program.

It should print the total of `1 + 2 + 3`, which is `6`.

```python
for number in range(1, 4):
    total = 0
    total = total + number

print(total)
```

Move only one line.

### Exercise 10

Write a word cleaner.

Ask for a word. Build a new string that skips the letter `"a"`.

Example:

```text
Word: banana
bnn
```

Use `continue` if you want:

```python
if letter == "a":
    continue
```

Or use an `else`. Both are good practice.

### Exercise 11

Write a search loop that stops early.

Ask for a word. Search for the first `"!"`.

If you find it, print:

```text
Exclamation found.
```

Then use `break` to stop searching.

After the loop, print whether it was found.

### Exercise 12

Choose one of your older programs from this course.

Look for repeated code. Write down which loop pattern might help:

```text
counting
accumulating
searching
validating input
repeating until done
building output
```

You do not have to rewrite the program yet. Just practice recognizing the pattern.

## Tiny Win

You can now look at a loop and ask what job it is doing.

Loops are no longer only syntax. They are reusable shapes:

```text
count
total
search
validate
repeat
build
```

That makes the next practice day easier to approach.

## Tomorrow

Tomorrow is a practice day:

```text
Day 29: Practice Day: Repetition Problems
```

You will solve small problems that mix `while`, `for`, `range()`, text loops, `break`, `continue`, and the patterns from today.

Before writing code, ask:

```text
Which loop pattern is this?
What value needs to be remembered?
What changes each time through the loop?
When should the loop stop?
```

Those questions are often enough to get started.
