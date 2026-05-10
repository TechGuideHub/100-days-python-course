# Day 09: Reading Error Messages

**Focus:** Reading Python errors without panic  
**You will practice:** Finding error names, line numbers, traceback clues, and making one small fix at a time  
**Estimated time:** 40-55 minutes

## Today's Goal

Today you will learn how to read Python error messages as clues.

By the end of this lesson, you should be able to:

* find the last line of a traceback
* identify the error name
* find the line number Python mentions
* recognize `SyntaxError`, `NameError`, and `TypeError`
* check the line just before an error
* fix one problem at a time

You do not need to memorize every possible error.

The goal is simpler:

> When Python stops, you should know where to start looking.

That skill will make every future lesson easier.

## The Big Idea

An error message is not Python being angry.

It is Python saying:

```text
I reached a point where I cannot continue.
```

Sometimes Python cannot understand the code at all. Sometimes it understands the code, starts running it, and then gets stuck. Sometimes the program runs, but the result is not what you wanted.

Those are different problems, but the first move is the same:

> Read the clue before changing the code.

Beginners often see red text and immediately start changing random lines. That usually creates more confusion.

Instead, pause and ask:

* What is the error name?
* What line number is mentioned?
* What code is on that line?
* Could the real mistake be on the line just above it?
* What is the smallest change I can try?

This is the beginning of debugging.

## The Mental Model

Think of Python as a careful reader.

It reads your program from top to bottom. When it finds something it cannot understand or cannot do, it stops and leaves a note.

That note often has three useful parts:

```text
Where Python was looking
What line it was reading
What kind of problem it found
```

Example:

```text
Traceback (most recent call last):
  File "day-09/greeting.py", line 2, in <module>
    print("Hello, " + naem)
NameError: name 'naem' is not defined
```

At first, this can look like a wall of text.

Read it from the bottom upward.

The most useful line is often the last line:

```text
NameError: name 'naem' is not defined
```

That tells you the error name:

```text
NameError
```

It also gives you a message:

```text
name 'naem' is not defined
```

Then look for the line number:

```text
line 2
```

Now you know where to look first.

## Reading a First Traceback

Create a file named:

```text
day-09/error_practice.py
```

Broken code:

```python
name = input("What is your name? ")
print("Hello, " + naem)
```

Run the program.

If you type `Maya`, you might see:

```text
What is your name? Maya
Traceback (most recent call last):
  File "day-09/error_practice.py", line 2, in <module>
    print("Hello, " + naem)
NameError: name 'naem' is not defined
```

Now read it slowly.

The error name is:

```text
NameError
```

That usually means Python saw a name it does not recognize.

The line number is:

```text
line 2
```

The line is:

```python
print("Hello, " + naem)
```

Look closely at the variable name.

The variable was created as `name`, but it was used as `naem`.

Fixed code:

```python
name = input("What is your name? ")
print("Hello, " + name)
```

This is a normal bug. You found a typo, and the error message helped you find it.

## Traceback Basics

A traceback is Python's way of showing the path to an error.

For beginner programs, the traceback is usually short.

Here is another file:

```text
day-09/age_problem.py
```

Broken code:

```python
age = input("How old are you? ")
total = age + 1
print(total)
```

If the user types `12`, Python may show:

```text
How old are you? 12
Traceback (most recent call last):
  File "day-09/age_problem.py", line 2, in <module>
    total = age + 1
TypeError: can only concatenate str (not "int") to str
```

Do not try to understand every word at once.

Use this reading order:

1. Read the last line.
2. Find the error name.
3. Find the line number.
4. Look at that line in your code.
5. Check the line just above it too.

The last line gives the type of error:

```text
TypeError
```

The line number tells you where Python noticed the problem:

```text
line 2
```

The code line shows what Python was trying to run:

```python
total = age + 1
```

That is enough to begin.

Fixed code:

```python
age = input("How old are you? ")
age = int(age)
total = age + 1
print(total)
```

## Line Numbers

Line numbers are one of the kindest parts of an error message.

They narrow the search.

If Python says:

```text
line 5
```

start by reading line 5. Then read line 4.

Many beginner errors are caused by something just before the line Python points to.

Example:

```text
day-09/missing_parenthesis.py
```

Broken code:

```python
name = input("What is your name? "
print("Hello, " + name)
```

Python may point at the second line:

```text
  File "day-09/missing_parenthesis.py", line 2
    print("Hello, " + name)
    ^^^^^
SyntaxError: invalid syntax
```

The real problem is on the first line. It is missing a closing parenthesis.

Fixed code:

```python
name = input("What is your name? ")
print("Hello, " + name)
```

When Python reports a syntax problem, also check the line above for:

* missing closing parentheses
* missing quotation marks
* extra quotation marks
* incomplete expressions

Python points to where it got confused. The cause can be slightly earlier.

## Common Error Names

You will meet many error names over time.

For now, learn these three.

### `SyntaxError`

A `SyntaxError` means Python could not understand the structure of your code.

Broken code:

```python
print("Hello"
```

The opening parenthesis has no matching closing parenthesis.

Fixed code:

```python
print("Hello")
```

Broken code:

```python
name = input("What is your name? )
```

The string starts with a quotation mark, but it does not end correctly.

Fixed code:

```python
name = input("What is your name? ")
```

When you see `SyntaxError`, check the basic shape:

* quotation marks
* parentheses
* spelling of Python keywords
* whether the line is complete

### `NameError`

A `NameError` means Python saw a name it does not know.

Broken code:

```python
color = "blue"
print(colour)
```

Python knows `color`. It does not know `colour`.

Fixed code:

```python
color = "blue"
print(color)
```

Broken code:

```python
print(message)
message = "Hello"
```

Python reads from top to bottom. When it reaches `print(message)`, the variable does not exist yet.

Fixed code:

```python
message = "Hello"
print(message)
```

When you see `NameError`, ask:

* Did I spell the variable the same way?
* Did I create the variable before using it?
* Did I put quotes around ordinary text?

### `TypeError`

A `TypeError` means Python was asked to do something with the wrong kind of value.

Broken code:

```python
age = input("How old are you? ")
next_year = age + 1
print(next_year)
```

The problem is that `input()` gives you text.

If the user types:

```text
12
```

Python stores it like this:

```text
"12"
```

That is text, not a number. Python cannot add text and a number with `+`.

Fixed code:

```python
age = input("How old are you? ")
age = int(age)
next_year = age + 1
print(next_year)
```

When you see `TypeError`, ask:

* Am I mixing text and numbers?
* Did `input()` give me a string?
* Do I need `int()` before doing math?

## Try It Yourself

Create a file named:

```text
day-09/day_09_errors.py
```

Start with this working program:

```python
name = input("What is your name? ")
age = input("How old are you? ")
age = int(age)

print("Hello, " + name)
print("Next year you will be", age + 1)
```

Run it once and make sure it works.

Then break it on purpose.

Try these one at a time:

1. Change `name` to `naem` in the final `print()` line.
2. Remove the closing parenthesis from the first line.
3. Remove `age = int(age)` and run the program again.

Each time:

* run the program
* read the error message
* write down the error name
* find the line number
* fix only that one problem
* run the program again

Breaking code on purpose may feel odd, but it is useful.

It teaches you what different mistakes look like in a low-pressure way.

## Common Mistake

### Mistake: Fixing five things at once

When a program breaks, beginners often change many lines at the same time.

Then the program still breaks, and the situation becomes harder to understand.

Now you do not know which change helped, which change hurt, and which change did nothing.

Debugging is easier when you move slowly.

Use this pattern:

```text
Read the error.
Make one small change.
Run the program.
Read the new result.
```

One change at a time is not slow. It is clear.

Clarity is what makes debugging possible.

## Common Beginner Reactions

It is worth naming what often happens when a beginner sees an error.

### Reaction 1: "I broke everything."

Probably not.

Most beginner errors are small:

* one misspelled variable
* one missing parenthesis
* one missing quote
* one value that needs `int()`

Small mistakes can create loud messages. The size of the message does not mean the mistake is large.

### Reaction 2: "I should delete it and start over."

Sometimes starting over is fine, but do not make it your first move.

Try reading the last line of the error first. Try checking the line number. Try fixing one small thing.

Starting over too quickly can stop you from learning the clue.

### Reaction 3: "I do not understand every word."

That is normal.

You do not need every word.

At this stage, look for:

* the error name
* the line number
* the code line
* one familiar phrase

You can solve many beginner bugs with only those clues.

## Debug It

Read each broken program.

For each one, answer three questions:

```text
What is the likely error name?
What line should you inspect first?
What is the smallest fix?
```

### Bug 1

Broken code:

```python
name = input("What is your name? ")
print("Hello, " + Name)
```

Likely error:

```text
NameError
```

Why?

Python variable names are case-sensitive. `name` and `Name` are not the same name.

Fixed code:

```python
name = input("What is your name? ")
print("Hello, " + name)
```

### Bug 2

Broken code:

```python
city = input("What city do you live in? ")
print("You live in " + city
```

Likely error:

```text
SyntaxError
```

Why?

The second line is missing a closing parenthesis.

Fixed code:

```python
city = input("What city do you live in? ")
print("You live in " + city)
```

### Bug 3

Broken code:

```python
price = input("Price: ")
total = price + 10
print(total)
```

Likely error:

```text
TypeError
```

Why?

`price` is text because it came from `input()`. The number `10` is an integer. Python cannot add text and an integer.

Fixed code:

```python
price = input("Price: ")
price = int(price)
total = price + 10
print(total)
```

### Bug 4

Broken code:

```python
print("Welcome to the program.")
favorite_food = input("What food do you like? ")
print("You like " + favoritefood)
```

Likely error:

```text
NameError
```

Why?

The variable was created as `favorite_food`, but it was used as `favoritefood`.

The underscore matters.

Fixed code:

```python
print("Welcome to the program.")
favorite_food = input("What food do you like? ")
print("You like " + favorite_food)
```

## Read the Docs

Today, practice using documentation as a place to check meaning.

Search for:

```text
Python exceptions documentation
```

Find Python's official documentation page about built-in exceptions.

You do not need to read the whole page.

Look for these names:

```text
SyntaxError
NameError
TypeError
```

For each one, read just enough to notice that Python gives names to different kinds of problems.

Documentation may feel dense. That is fine.

Today you are practicing this habit:

> When I see an unfamiliar Python word, I can look it up slowly.

That habit matters more than memorizing the page.

## Mini Challenge

Create a file named:

```text
day-09/error_journal.py
```

Write this working program:

```python
name = input("What is your name? ")
age = input("How old are you? ")
age = int(age)

print("")
print("Error Journal")
print("Name: " + name)
print("Age next year:", age + 1)
```

Now make a tiny error journal in a comment at the bottom of the file.

Break the program three different ways, one at a time.

After each error, write a short note:

```python
# Error 1:
# What I changed:
# Error name:
# Line number:
# Fix:
```

Example journal note:

```python
# Error 1:
# What I changed: I typed naem instead of name.
# Error name: NameError
# Line number: 7
# Fix: I changed naem back to name.
```

The goal is not to create mistakes forever.

The goal is to learn what clues look like.

## Real-World Use

Every programmer reads error messages.

People who build websites, games, phone apps, data tools, banking systems, and school software all spend time reading errors.

The difference is not that experienced programmers avoid mistakes.

The difference is that they know how to investigate.

They read the message. They find the line. They make one change. They run the program again.

That loop is part of real programming work.

The earlier you get comfortable with it, the less mysterious programming becomes.

## Recap

Today you learned:

* an error message is a clue, not a judgment
* a traceback shows where Python noticed a problem
* the last line often contains the most useful information
* line numbers tell you where to look first
* `SyntaxError` means Python could not understand the code structure
* `NameError` often means a name was misspelled or used too early
* `TypeError` often means the wrong kind of value was used
* `input()` gives text, so math may require `int()`
* debugging works best when you fix one thing at a time

The main idea:

```text
Error messages are part of the conversation between you and Python.
```

They are not always friendly, but they are useful.

## Exercises

### Exercise 1

Look at this program.

Broken code:

```python
name = input("What is your name? ")
print("Hello, " + nmae)
```

Answer:

```text
What is the likely error name?
Which line should you inspect first?
What is the fix?
```

Then run the broken version and compare your answer with Python's message.

### Exercise 2

Fix this program.

Broken code:

```python
print("Favorite Color Program"
color = input("What is your favorite color? ")
print("Your favorite color is " + color)
```

Before fixing it, predict the likely error name.

Then run it and check.

### Exercise 3

Fix this program.

Broken code:

```python
age = input("How old are you? ")
next_year = age + 1
print("Next year you will be", next_year)
```

The program should ask for an age and print the age next year.

Hint:

```text
int()
```

### Exercise 4

This program has two mistakes.

Fix only one mistake first. Run the program again. Then fix the next mistake.

Broken code:

```python
food = input("What food do you like? "
print("You like " + Food)
```

Write down:

```text
First error name:
First fix:
Second error name:
Second fix:
```

This is practice in not rushing.

### Exercise 5

Create a file named:

```text
day-09/debug_three_inputs.py
```

Write a working program that asks for:

* your name
* your city
* your favorite number

Convert the favorite number to an integer.

Then print:

```text
Hello, NAME from CITY.
Your favorite number plus 5 is RESULT.
```

After it works, break it once on purpose and fix it using the error message.

### Exercise 6

Find a previous program from Days 03 to 08.

Run it again.

If it works, introduce one small mistake on purpose:

* misspell a variable
* remove one parenthesis
* remove `int()` before doing math

Run it. Read the error. Fix it. Then put the program back in its working state.

### Exercise 7

Write your own debugging checklist with five questions.

Start with:

```text
1. What is the error name?
2. What line number does Python mention?
```

Add three more questions that would help you slow down and inspect the code carefully.

## Lesson Checklist

Before moving on, check that you can:

* read the last line of a traceback
* name the error type from the last line
* find the line number Python mentions
* explain why the real problem may be on the line above
* recognize simple `SyntaxError`, `NameError`, and `TypeError` examples
* fix one small problem and run the program again

## Tiny Win

Before today, an error message may have looked like a wall.

Now you know how to find a door:

* read the last line
* find the error name
* find the line number
* inspect the code
* fix one thing
* run again

That is a real programming skill.

## Tomorrow

Tomorrow, you will use the pieces from Days 01 to 09 to build a small conversation program.

It will ask questions, remember answers, print a response, and give you more practice reading the messages Python gives back.
