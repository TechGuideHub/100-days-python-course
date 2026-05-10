# Day 03: Your First Program

**Focus:** Writing and running a small interactive Python program  
**You will practice:** `print()`, `input()`, storing user text, reading output, and fixing small mistakes  
**Estimated time:** 30-40 minutes

## Today's Goal

Today you will write a Python program that asks a question, remembers the answer, and uses that answer in a message.

By the end of this lesson, you should be able to:

- create a Python file
- use `print()` to show text
- use `input()` to ask the user for text
- store the user's answer using a simple name
- run the program from a terminal
- compare expected output with actual output

This is the first lesson where your program responds to what the user types.

## The Big Idea

Many useful programs start with a simple pattern:

1. Ask for information
2. Save the answer
3. Use the answer
4. Show a result

You saw the same shape on Day 1:

```text
Input
Process
Output
```

Today you will turn that idea into Python code.

Example:

```python
name = input("What is your name? ")
print("Hello, " + name + "!")
```

Run it and type a name when the program waits:

```text
What is your name? Maya
Hello, Maya!
```

This program does not print the same message every time. The output changes based on what the user types.

> Key idea: `input()` lets a program pause, receive text from the user, and use that text later.

## The Mental Model

Think of this program as a short conversation.

```text
Computer: What is your name?
User: Maya
Computer: Hello, Maya!
```

In Python, that conversation looks like this:

```python
name = input("What is your name? ")
print("Hello, " + name + "!")
```

The first line asks the question.

The word `name` holds the answer.

The second line joins text together and shows the final message.

For today, think of `name` as a label attached to the user's answer. You will study variables more directly tomorrow.

> Checkpoint: If a program needs to use an answer later, it needs a name to hold that answer.

## Create the File

Make a folder for today's work if you are keeping each day separate.

Folder name:

```text
day-03
```

Inside that folder, create this file:

```text
first_program.py
```

Relative path:

```text
day-03/first_program.py
```

That means:

```text
Open the day-03 folder, then open first_program.py.
```

Make sure the file ends with `.py`, not `.txt`.

## Write the Program

Type this complete program into `day-03/first_program.py`.

```python
print("Welcome to my first program.")

name = input("What is your name? ")

print("Nice to meet you, " + name + ".")
```

Save the file.

Run it from your course folder:

```bash
python day-03/first_program.py
```

If your computer uses `py`, use this command instead:

```bash
py day-03/first_program.py
```

If your computer uses `python3`, use this:

```bash
python3 day-03/first_program.py
```

If your terminal is already inside the `day-03` folder:

```bash
python first_program.py
```

When the program asks for your name, type a name and press Enter.

You should see something like this:

```text
Welcome to my first program.
What is your name? Ravi
Nice to meet you, Ravi.
```

You have now written a program that reacts to user input.

## What Each Line Does

Look again at the full program.

```python
print("Welcome to my first program.")

name = input("What is your name? ")

print("Nice to meet you, " + name + ".")
```

This line shows text:

```python
print("Welcome to my first program.")
```

This line asks a question and stores the answer:

```python
name = input("What is your name? ")
```

This line joins text together and shows the result:

```python
print("Nice to meet you, " + name + ".")
```

The `+` signs join pieces of text.

If `name` contains this text:

```text
Ravi
```

then this expression:

```python
"Nice to meet you, " + name + "."
```

becomes this output:

```text
Nice to meet you, Ravi.
```

Python follows the instructions exactly. It does not guess which spaces or punctuation you meant to include.

## Try It Yourself

Change the program so it asks for a favorite food.

```python
print("Food survey")

food = input("What is your favorite food? ")

print("I like " + food + " too.")
```

Save the file and run it again.

Try different answers:

```text
rice
pizza
mango
noodles
```

Each time, the output should change.

You should see something like this:

```text
Food survey
What is your favorite food? mango
I like mango too.
```

Use the same practice loop each time:

1. edit the file
2. save the file
3. run the file
4. read the output
5. change one thing and try again

## Common Mistake

### Mistake: Putting the stored name inside quotation marks

This code runs, but the greeting is wrong:

```python
name = input("What is your name? ")
print("Hello, name!")
```

If the user types `Asha`, the program prints the word `name` instead of the stored answer.

Actual output:

```text
What is your name? Asha
Hello, name!
```

Why did it happen?

`"Hello, name!"` is one plain piece of text. Python sees the letters `n`, `a`, `m`, and `e` inside quotation marks and treats them as normal text.

To use the stored answer, keep `name` outside the quotation marks.

Fixed code:

```python
name = input("What is your name? ")
print("Hello, " + name + "!")
```

You should see:

```text
What is your name? Asha
Hello, Asha!
```

> Key idea: Text inside quotation marks prints exactly as written. A stored value has to stay outside the quotation marks if you want Python to use it.

## Debug It

Here is a broken program.

Broken code:

```python
name = input("What is your name? ")
print("Hello, " + nam + "!")
```

What is wrong?

The answer was stored using the name `name`, but the second line uses `nam`.

Python treats `name` and `nam` as different names.

Fixed code:

```python
name = input("What is your name? ")
print("Hello, " + name + "!")
```

You should see:

```text
What is your name? Leela
Hello, Leela!
```

Here is another broken program.

Broken code:

```python
name = input("What is your name? ")
print("Hello, " + name + !)
```

What is wrong?

The exclamation mark is text, so it needs quotation marks.

Fixed code:

```python
name = input("What is your name? ")
print("Hello, " + name + "!")
```

You should see:

```text
What is your name? Leela
Hello, Leela!
```

Early bugs are often small:

- one missing quotation mark
- one missing parenthesis
- one misspelled name
- one piece of text placed outside quotation marks
- one stored value placed inside quotation marks

When something breaks, compare what you wrote with what Python needs. Debugging usually starts with careful reading.

## Read the Docs

Today, look up Python's official documentation for `input`.

Do not try to read the entire page. Your task is only to notice this idea:

```text
input() reads a line from the user.
```

That means `input()` waits until the user types something and presses Enter.

Documentation may feel formal at first. Use it as a reference, not a textbook. You are practicing the habit of checking the real source when you need to know what a tool does.

## Mini Challenge

Create a file named `day-03/favorite_place.py`.

Write a program that asks for:

1. the user's name
2. a place the user likes

Then print a sentence using both answers.

Code:

```python
name = input("What is your name? ")
place = input("What place do you like? ")

print(name + " likes " + place + ".")
```

You should see something like this:

```text
What is your name? Leela
What place do you like? the library
Leela likes the library.
```

After it works, change the final sentence.

```python
print(place + " sounds like a good place, " + name + ".")
```

Run it again.

The goal is to practice this pattern:

```text
ask
remember
use
show
```

## Real-World Use

Programs ask for information all the time.

Examples:

- a login page asks for a username
- a search box asks what you want to find
- a food delivery app asks for an address
- a calculator asks for numbers
- a game asks for a player name
- a banking app asks which account you want to view

Those programs are larger, but the pattern is the same:

```text
Ask for input.
Store it.
Use it.
Show something useful.
```

Your first program is a small version of something real programs do constantly.

## Recap

Today you learned:

- `print()` shows text on the screen
- `input()` asks the user for text
- a program can pause and wait for an answer
- a stored answer can be used later
- quotation marks tell Python what should be treated as plain text
- file paths can be written as simple relative paths like `day-03/first_program.py`
- small spelling differences matter in code
- debugging means reading carefully and fixing one issue at a time

Main idea: a program becomes more useful when it can respond to information from the user.

## Exercises

### Exercise 1

Create a file named `day-03/hello_name.py`.

Ask for the user's name and print a greeting.

For example, if the user types `Asha`, the program should print:

```text
Hello, Asha!
```

### Exercise 2

Create a file named `day-03/favorite_color.py`.

Ask for the user's favorite color and print one sentence using the answer.

### Exercise 3

Fix this code.

Broken code:

```python
name = input("Name: ")
print("Hello, " + Name)
```

Hint: Python cares about uppercase and lowercase letters.

### Exercise 4

Fix this code.

Broken code:

```python
city = input("What city do you live in? ")
print("You live in " city)
```

Hint: two pieces of text need to be joined.

### Exercise 5

Write a program that asks three questions:

- What is your name?
- What are you learning?
- What do you want to build?

Then print three sentences using the answers.

Keep the sentences simple.

## Lesson Checklist

Before moving on, check that you can:

- create and run a `.py` file
- use `print()` to show text
- use `input()` to ask for text
- store an answer with a clear name
- join text with `+`
- explain why stored names usually go outside quotation marks
- spot a misspelled stored name
- compare expected output with actual output

## Tiny Win

Yesterday, you ran a file that printed fixed text.

Today, your program listened, saved an answer, and replied with the user's own words.

The program is still small, but it now has the shape of a conversation.

## Tomorrow

Tomorrow, you will learn about variables more directly.

Today you used names like `name`, `food`, and `place` to hold answers. Tomorrow, you will slow down and understand what those names are, how they work, and how to choose them clearly.
