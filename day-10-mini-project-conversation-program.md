# Day 10: Mini Project: Conversation Program

**Focus:** Building a complete beginner program from familiar pieces  
**You will practice:** `print()`, `input()`, variables, string joining, `int()`, `str()`, testing, and debugging  
**Estimated time:** 45-60 minutes

## Today's Goal

Today you will build your first small project in this course.

The project is a conversation program. It will ask a few questions, remember the answers, and use those answers to print a friendly response.

It will not understand language like a person. It will simply follow the steps you give it. That is enough for today.

By the end of this lesson, you should be able to:

* plan a small program before writing it
* use `print()` to guide the user
* use `input()` to ask questions
* store answers in variables
* combine strings and variables
* convert input with `int()` when you need math
* convert a number with `str()` when you need it inside a sentence
* test a program with different answers
* read simple error messages without panic

This is a project day, so the goal is not to learn many new commands. The goal is to put familiar pieces together.

## The Project

Create this file:

```text
day-10/conversation_program.py
```

The program will ask the user:

* their name
* where they are from
* something they enjoy
* how old they are
* something they want to learn

Then it will print a short conversation-style message using those answers.

A run might look like this:

```text
Welcome to the conversation program.
I will ask a few questions and then make a tiny profile.
What is your name? Maya
Where are you from? Pune
What is something you enjoy? drawing
How old are you? 14
What is something you want to learn? Python

Thanks, Maya.
You are from Pune, and you enjoy drawing.
Next year, you will be 15.
Learning Python sounds like a good next step.
```

The program is small, but it has the shape of many real programs:

```text
ask -> remember -> process -> respond
```

That shape matters more than the size of the program.

## The Big Idea

A beginner project does not need to be large.

A good beginner project gives you a complete path from start to finish. This one starts with a greeting, collects information, does a small calculation, and prints a clear response.

For this project, you will practice:

* showing information with `print()`
* asking questions with `input()`
* storing information in variables
* joining text together
* converting text to a number when you need math
* running the program more than once to check it

You are not trying to impress anyone today. You are learning how to build something that works from beginning to end.

## The Mental Model

Think of the program as a careful interviewer.

A good interviewer does not ask everything at once. They ask one question, listen to the answer, and use that answer later.

In Python, that looks like this:

```python
name = input("What is your name? ")
print("Nice to meet you, " + name + ".")
```

There are three jobs happening:

```text
input()  -> collect information
variable -> remember information
print()  -> show information
```

The variable is the program's notebook.

When you write this:

```python
name = input("What is your name? ")
```

you are telling Python:

```text
Ask the question.
Take the answer.
Store it under the name name.
```

Then the program can use `name` later.

That is how a program starts to feel personal even though it is still simple.

## Step-by-Step Build

Build this project in stages.

Do not write the final version first. A calm process is part of the skill.

### Step 1: Start With a Welcome Message

Create this file:

```text
day-10/conversation_program.py
```

Code:

```python
print("Welcome to the conversation program.")
print("I will ask a few questions and then make a tiny profile.")
```

Run it:

```bash
python day-10/conversation_program.py
```

You should see:

```text
Welcome to the conversation program.
I will ask a few questions and then make a tiny profile.
```

This is not interactive yet. That is fine. First, make sure the file runs.

### Step 2: Ask for the User's Name

Now add one question:

```python
print("Welcome to the conversation program.")
print("I will ask a few questions and then make a tiny profile.")

name = input("What is your name? ")

print("Thanks, " + name + ".")
```

Run it and type a name when the program waits.

Example:

```text
Welcome to the conversation program.
I will ask a few questions and then make a tiny profile.
What is your name? Maya
Thanks, Maya.
```

Notice the pattern:

```text
ask -> store -> use
```

That is the center of today's project.

### Step 3: Add More Questions

Now ask for a few more pieces of information:

```python
print("Welcome to the conversation program.")
print("I will ask a few questions and then make a tiny profile.")

name = input("What is your name? ")
city = input("Where are you from? ")
hobby = input("What is something you enjoy? ")
goal = input("What is something you want to learn? ")

print("")
print("Thanks, " + name + ".")
print("You are from " + city + ", and you enjoy " + hobby + ".")
print("Learning " + goal + " sounds like a good next step.")
```

The blank line here:

```python
print("")
```

makes the final response easier to read.

Output is part of the user's experience. A program can be correct and still feel messy. Blank lines, spaces, and punctuation help.

### Step 4: Add a Number

Now add age.

Remember this rule:

> `input()` always gives you text.

If the user types `14`, Python first receives it as the string `"14"`.

That is fine if you only want to print it. But if you want to calculate next year's age, you need to convert it with `int()`.

Add this after asking for age:

```python
age = input("How old are you? ")
age = int(age)
next_year = age + 1
```

Now the program can do a tiny piece of math.

### Step 5: Put It Together

Here is the complete program:

```python
print("Welcome to the conversation program.")
print("I will ask a few questions and then make a tiny profile.")

name = input("What is your name? ")
city = input("Where are you from? ")
hobby = input("What is something you enjoy? ")
age = input("How old are you? ")
goal = input("What is something you want to learn? ")

age = int(age)
next_year = age + 1

print("")
print("Thanks, " + name + ".")
print("You are from " + city + ", and you enjoy " + hobby + ".")
print("Next year, you will be " + str(next_year) + ".")
print("Learning " + goal + " sounds like a good next step.")
```

Run it at least three times with different answers.

Testing a program means trying it, reading what happens, and asking:

```text
Did the program do what I expected?
```

Here is one full run:

```text
Welcome to the conversation program.
I will ask a few questions and then make a tiny profile.
What is your name? Asha
Where are you from? Chennai
What is something you enjoy? music
How old are you? 13
What is something you want to learn? animation

Thanks, Asha.
You are from Chennai, and you enjoy music.
Next year, you will be 14.
Learning animation sounds like a good next step.
```

The age line works because the program first does math:

```python
next_year = age + 1
```

Then it converts the answer back into text for the sentence:

```python
print("Next year, you will be " + str(next_year) + ".")
```

You may have first written this instead:

```python
print("Next year, you will be", next_year)
```

That version is useful while learning, but it does not add the period at the end:

```text
Next year, you will be 14
```

You could try this:

```python
print("Next year, you will be", next_year, ".")
```

But that prints an extra space before the period:

```text
Next year, you will be 14 .
```

A cleaner version is:

```python
print("Next year, you will be " + str(next_year) + ".")
```

The important idea is:

* use `int()` when you need number math
* use `str()` when you need to join a number into a string

## Try It Yourself

Change the program so it asks different questions.

Choose at least five:

* What is your name?
* What city do you live in?
* What is your favorite food?
* What is one hobby you enjoy?
* What is one place you want to visit?
* What is one skill you want to learn?
* What is one subject you like?
* How many hours did you sleep last night?
* How many books did you read this month?

If you ask for a number and want to do math with it, convert it:

```python
books = input("How many books did you read this month? ")
books = int(books)
next_month = books + 1
```

If you only want to print the answer, it can stay as text.

Example:

```python
food = input("What is your favorite food? ")
print("I hope you get to eat " + food + " soon.")
```

Build slowly:

1. Add one question.
2. Run the program.
3. Read the output.
4. Add another question.
5. Run the program again.

That rhythm catches mistakes early.

## Common Mistake

### Mistake: Writing the Whole Program Before Running It

Beginners often write many lines before testing anything.

Then, if something breaks, there may be five possible causes.

Try this:

```text
write 2 or 3 lines
run the program
read the output
fix anything small
continue
```

This is not slow. It is steady.

Another common mistake is forgetting that input is text.

Broken code:

```python
age = input("How old are you? ")
next_year = age + 1
print(next_year)
```

This breaks because Python cannot add text and a number.

Fixed code:

```python
age = input("How old are you? ")
age = int(age)
next_year = age + 1
print(next_year)
```

If you remember one thing from this section, remember:

> Convert input only when you need it to behave like a number.

## Debug It

Debugging is part of this project.

Read each broken example before looking at the fix.

### Bug 1: The Variable Is Inside Quotes

Broken code:

```python
name = input("What is your name? ")
print("Hello, name.")
```

If the user types `Ravi`, the program prints this:

```text
Hello, name.
```

The program prints the word `name` because it is inside quotes.

Fixed code:

```python
name = input("What is your name? ")
print("Hello, " + name + ".")
```

Inside quotes, text is just text. Outside quotes, Python looks for the variable.

### Bug 2: A Missing Space

Broken code:

```python
city = input("Where are you from? ")
print("You are from" + city + ".")
```

If the user types `Delhi`, the output is cramped:

```text
You are fromDelhi.
```

Fixed code:

```python
city = input("Where are you from? ")
print("You are from " + city + ".")
```

Spaces inside strings matter.

### Bug 3: Text and Numbers Are Mixed

Broken code:

```python
age = input("How old are you? ")
next_year = age + 1
print("Next year you will be " + next_year + ".")
```

This can cause an error because `age` starts as text.

Fixed code:

```python
age = input("How old are you? ")
age = int(age)
next_year = age + 1
print("Next year you will be " + str(next_year) + ".")
```

There are two conversions:

```python
age = int(age)
```

This changes the input into a number so Python can do math.

```python
str(next_year)
```

This changes the number into text so Python can join it into a sentence.

### Bug 4: The User Types a Word for Age

Try this small program:

```python
age = input("How old are you? ")
age = int(age)
```

If the user types this:

```text
twelve
```

Python cannot convert that word into an integer.

You may see an error that includes:

```text
ValueError
```

For now, you do not need to prevent this error.

Just understand what happened:

```text
The program expected digits like 12.
The user typed a word like twelve.
int() could not convert it.
```

Later, you will learn better ways to handle that situation. Today, the useful habit is reading the clue.

## Read the Docs

Look up Python's official documentation for built-in functions:

```text
https://docs.python.org/3/library/functions.html
```

Find `int()` and `str()`.

You do not need to read the whole page. Look for these simple facts:

* `int()` can convert a suitable value into an integer
* `str()` can convert a value into a string

Documentation often contains more detail than you need at the beginning. That is normal.

Your job today is to practice looking up a tool when you meet it.

## Mini Challenge

Create a second version of the program:

```text
day-10/conversation_program_v2.py
```

This version should ask:

* the user's name
* their favorite place
* their favorite activity
* their age
* how many years from now they want to imagine

Then print a small future message.

Example:

```text
What is your name? Noor
What is your favorite place? the beach
What is an activity you enjoy? swimming
How old are you? 15
How many years from now should we imagine? 5

Noor, in 5 years you will be 20.
Maybe you will still enjoy swimming at the beach.
```

The key lines will look like this after you have collected and converted the numbers:

```python
future_years = input("How many years from now should we imagine? ")
future_years = int(future_years)

future_age = age + future_years
```

You will need to convert both `age` and `future_years` before adding them.

## Real-World Use

This project is simple, but the pattern is real.

Many programs collect information, store it, and respond:

* a sign-up form asks for your name and email
* a banking app asks which account you want to view
* a delivery app asks for an address
* a game asks for a player name
* a school form asks for student details
* a calculator asks for numbers

The interface may look different, but the basic flow is familiar:

```text
Ask for information.
Store the answers.
Use the answers.
Show a result.
```

Today's project is a small version of that flow.

## Recap

Today you built a complete beginner project.

You practiced:

* using `print()` for messages
* using `input()` for questions
* storing answers in variables
* combining strings and variables
* converting input with `int()` when you need math
* converting numbers with `str()` when you need string joining
* checking output for spacing and punctuation
* reading errors as clues
* testing with different inputs

The main idea:

> A small program becomes useful when it asks, remembers, and responds clearly.

## Lesson Checklist

Before moving on, check that you can:

* create and run `day-10/conversation_program.py`
* build a program in small stages
* use `input()` to collect several answers
* store each answer in a clear variable
* join strings and variables into readable sentences
* use `int()` before doing math with input
* use `str()` when joining a number into a string
* test the same program with different answers
* fix missing spaces, quoted variable names, and mixed text-number problems

## Exercises

### Exercise 1

Create this file:

```text
day-10/daily_check_in.py
```

Ask the user:

* their name
* how they feel today
* one thing they plan to do

Print a short check-in summary.

### Exercise 2

Create this file:

```text
day-10/favorite_things.py
```

Ask the user for three favorite things:

* a food
* a song, movie, or book
* a place

Print a friendly paragraph using all three answers.

### Exercise 3

Fix this program:

```python
name = input("What is your name? ")
hobby = input("What is your hobby? ")
print(name + " enjoys hobby.")
```

The output should use the value stored in `hobby`, not the word `hobby`.

### Exercise 4

Fix the spacing in this program:

```python
name = input("What is your name? ")
city = input("Where do you live? ")
print("Hello," + name + "from" + city)
```

The output should look like this, using whatever name and city the user typed:

```text
Hello, Maya from Pune
```

### Exercise 5

Create this file:

```text
day-10/next_birthday.py
```

Ask the user for their age.

Convert the age to an integer.

Print how old they will be on their next birthday.

### Exercise 6

Create this file:

```text
day-10/two_number_story.py
```

Ask the user for:

* their name
* their current age
* a number of years to imagine

Then print:

```text
NAME, in YEARS years you will be AGE.
```

Example:

```text
Riya, in 3 years you will be 16.
```

### Exercise 7

Run your conversation program three times.

Use different answers each time.

Write down one thing you noticed:

* a sentence that looked good
* a sentence that needed better spacing
* an error message you fixed
* a prompt you made clearer

This is manual testing. Manual testing is still testing.

## Tiny Win

You have now built a complete program that asks questions, stores answers, does a small calculation, and prints a personalized response.

That is a small project, not just a loose code example.

You are starting to combine pieces into something with a beginning, middle, and end.

## Tomorrow

Tomorrow, you will begin comparisons.

Comparisons let a program ask questions like:

```python
age >= 18
```

or:

```python
answer == "yes"
```

That will prepare you for `if` statements, where programs can choose different paths instead of always doing the same thing.
