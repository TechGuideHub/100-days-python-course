# Day 04: Variables

**Focus:** Storing information with variable names  
**You will practice:** Creating variables, printing variable values, choosing clear names, and changing values  
**Estimated time:** 30-40 minutes

## Today's Goal

Today you will learn how Python remembers information while a program runs.

By the end of this lesson, you should be able to:

- create variables
- use variables in `print()`
- choose clear variable names
- change a variable's value
- recognize common variable mistakes

The main idea is small, but important:

> Key idea: A variable is a name that refers to a value.

That name lets your program keep track of information and use it again.

## The Big Idea

Programs become useful when they can remember things.

A greeting program needs to remember a name. A game needs to remember a score. A shopping app needs to remember prices, quantities, and totals. A weather app needs to remember a city and a temperature.

Variables are how we give names to those pieces of information.

Example:

```python
name = "Maya"
print(name)
```

You should see:

```text
Maya
```

Read the first line as:

```text
The variable named name refers to the value "Maya".
```

The variable is not shown with quotation marks when it prints because the variable itself is not text. It is a name Python uses to find the value.

## The Mental Model

Think of a variable as a label on a jar.

The value is what is inside the jar. The variable name is the label on the outside.

Example:

```python
favorite_food = "dosa"
print(favorite_food)
```

You should see:

```text
dosa
```

The label is:

```text
favorite_food
```

The value is:

```text
"dosa"
```

Later, when you write `print(favorite_food)`, Python looks at the label, finds the value, and prints it.

This is why names matter. A clear label helps you understand what the value means.

## Create the File

Make a folder for today's work if you are keeping each day separate.

Folder name:

```text
day-04
```

Inside that folder, create a file named:

```text
variables_practice.py
```

Relative path:

```text
day-04/variables_practice.py
```

That path means:

```text
Open the day-04 folder, then open variables_practice.py.
```

Use the short relative path in notes or code comments. It tells you exactly where the file belongs.

## First Program

Type this complete program into `day-04/variables_practice.py`.

Code:

```python
name = "Asha"
age = 14
city = "Hyderabad"

print(name)
print(age)
print(city)
```

Save the file.

Run it from the course folder with whichever command works on your computer:

```bash
python day-04/variables_practice.py
```

```bash
py day-04/variables_practice.py
```

```bash
python3 day-04/variables_practice.py
```

If your terminal is already inside the `day-04` folder, run:

```bash
python variables_practice.py
```

You should see:

```text
Asha
14
Hyderabad
```

Notice that the program has three pieces of information:

- `name` stores text
- `age` stores a number
- `city` stores text

The program can now use those values without typing them again and again.

## Using Variables in Sentences

Variables become more useful when you combine them with other text.

Example:

```python
name = "Asha"
city = "Hyderabad"

print("My name is " + name)
print("I live in " + city)
```

You should see:

```text
My name is Asha
I live in Hyderabad
```

The `+` joins pieces of text together.

This works because both sides are text:

```text
"My name is " + name
```

The first piece is a string. The second piece is a variable that refers to a string. Together, they make one longer string.

## A Small Warning About Numbers

This version works because `age` is printed by itself.

Example:

```python
age = 14
print(age)
```

You should see:

```text
14
```

Broken code:

```python
age = 14
print("I am " + age)
```

Python complains because `"I am "` is text and `age` is a number.

Fixed code:

```python
age = 14
print("I am")
print(age)
```

You should see:

```text
I am
14
```

You will learn cleaner ways to combine text and numbers soon. The important idea today is that variables can refer to different kinds of values.

## Naming Variables Well

Python allows many variable names, but not every allowed name is a good name.

Good names explain the value:

```python
student_name = "Ravi"
total_score = 95
favorite_color = "green"
```

Weak names make you guess:

```python
x = "Ravi"
ts = 95
thing = "green"
```

Short names are sometimes useful later. For now, choose names that explain themselves.

Use these habits:

- use lowercase letters
- use underscores between words
- choose names that describe the value
- avoid names that are too vague
- avoid names that look almost the same

Good:

```python
first_name = "Leela"
final_price = 250
player_score = 10
```

Not as good:

```python
n = "Leela"
price2 = 250
scorething = 10
```

A variable name is a note to your future self. Make it clear.

## Variable Name Rules

Python has a few rules for variable names.

Variable names can contain:

- letters
- numbers
- underscores

But they cannot start with a number.

Valid Python names:

```python
name = "Maya"
name2 = "Arjun"
favorite_food = "rice"
```

Broken code:

```python
2name = "Arjun"
favorite food = "rice"
favorite-food = "rice"
```

Why?

- `2name` starts with a number
- `favorite food` has a space
- `favorite-food` uses a hyphen

Use underscores instead of spaces.

Code:

```python
favorite_food = "rice"
```

Python also cares about uppercase and lowercase letters.

These are three different names:

```python
name = "Maya"
Name = "Asha"
NAME = "Ravi"
```

Do not do that on purpose right now. It is confusing. Use lowercase names unless you have a special reason not to.

## Reassignment

A variable can be given a new value.

This is called reassignment.

Example:

```python
score = 0
print(score)

score = 10
print(score)
```

You should see:

```text
0
10
```

At first, `score` refers to `0`. Later, `score` refers to `10`. The old value is replaced.

This pattern appears in many programs.

Example:

```python
score = 0
score = score + 5
print(score)
```

You should see:

```text
5
```

This line may look strange at first:

```text
score = score + 5
```

It means:

```text
Take the current value of score.
Add 5.
Store the result back in score.
```

If `score` starts as `0`, then `score + 5` becomes `5`, and `score` now refers to `5`.

> Checkpoint: Read assignment from right to left. First Python works out the value on the right, then it stores that result in the name on the left.

In a beginner-friendly shorthand:

```text
new score = old score + 5
```

## Example

Here is a complete program for `day-04/game_score.py`.

Code:

```python
player_name = "Nina"
score = 0

print(player_name)
print(score)

score = score + 10
print(score)

score = score + 5
print(score)
```

You should see:

```text
Nina
0
10
15
```

The program starts with a player and a score. Then the score changes twice.

The variable name stays the same, but the value it refers to changes. That is why variables are useful: they let a program carry information forward.

## Try It Yourself

Create a file named:

```text
score_tracker.py
```

If you keep it inside today's folder, its relative path is:

```text
day-04/score_tracker.py
```

Write this starter program.

Code:

```python
player_name = "Sam"
score = 0

print(player_name)
print(score)

score = score + 1
print(score)

score = score + 1
print(score)
```

Run it.

Then change:

- the player's name
- the starting score
- how much the score increases

Run the file after each change.

The habit you are practicing is watching how a variable changes over time.

## Common Mistake

### Mistake: Putting quotation marks around the variable name

Look at this program.

Example:

```python
name = "Maya"
print("name")
```

You should see:

```text
name
```

Python prints the word `name` because quotation marks mean:

```text
Treat this as text exactly as written.
```

If you want the value inside the variable, remove the quotation marks.

Fixed code:

```python
name = "Maya"
print(name)
```

You should see:

```text
Maya
```

Small difference, big meaning.

Compare the two:

```python
name = "Maya"

print("name")
print(name)
```

You should see:

```text
name
Maya
```

## Debug It

Broken code:

```python
user name = "Isha"
print(user name)
```

What is wrong?

Variable names cannot contain spaces.

Fixed code:

```python
user_name = "Isha"
print(user_name)
```

Broken code:

```python
favorite_color = "blue"
print(favourite_color)
```

What is wrong?

The variable was created with one spelling:

```text
favorite_color
```

But printed with another spelling:

```text
favourite_color
```

Python sees those as different names.

Fixed code:

```python
favorite_color = "blue"
print(favorite_color)
```

If you see an error like:

```text
NameError: name 'favourite_color' is not defined
```

read it as:

```text
Python does not know any variable with that name.
```

When that happens, check:

- Did you spell the variable the same way both times?
- Did you create the variable before using it?
- Did you accidentally change uppercase or lowercase letters?
- Did you put quotation marks where you did not mean to?

Debugging variables is often careful reading.

## Read the Docs

Today, look up Python's official tutorial section about using Python as a calculator.

You do not need to read the whole page. Find one example where a name is assigned a value with `=`.

The goal is to notice that official examples use the same basic idea:

```text
variable_name = value
```

Documentation becomes easier when you connect it to something you already understand.

## Mini Challenge

Create a file named:

```text
profile_card.py
```

If you keep it inside today's folder, its relative path is:

```text
day-04/profile_card.py
```

Write a program that stores information about a person in variables, then prints a simple profile.

Use at least four variables:

```python
name = "Anika"
age = 13
city = "Pune"
hobby = "drawing"
```

Your first output can be simple:

```text
Anika
13
Pune
drawing
```

Then improve it by adding labels.

Starter code:

```python
name = "Anika"
age = 13
city = "Pune"
hobby = "drawing"

print("Name:")
print(name)
print("Age:")
print(age)
print("City:")
print(city)
print("Hobby:")
print(hobby)
```

You should see:

```text
Name:
Anika
Age:
13
City:
Pune
Hobby:
drawing
```

Keep it simple. The point is to practice storing values with clear names and printing them in a useful order.

## Real-World Use

Variables are everywhere in real programs.

A music app might use variables like:

```python
song_title = "River"
artist_name = "Asha"
is_playing = True
volume = 70
```

A game might use:

```python
player_name = "Nina"
health = 100
score = 0
level = 1
```

A shopping program might use:

```python
item_name = "notebook"
price = 40
quantity = 3
```

The programs are different, but the idea is the same:

> Key idea: Give important values clear names so the program can use them later.

When code has good variable names, it becomes easier to read. You can often understand the story of a program just by reading its names.

## Recap

Today you learned:

- variables are names that refer to values
- `=` assigns a value to a variable
- variables can store text, numbers, and other kinds of values
- good variable names make code easier to understand
- Python variable names cannot contain spaces or hyphens
- Python variable names cannot start with a number
- Python cares about uppercase and lowercase letters
- variables can be reassigned
- `print(name)` and `print("name")` do different things
- a `NameError` often means Python cannot find the variable name you used
- relative paths like `day-04/profile_card.py` are enough for lesson notes

The main idea:

```text
Variables let a program remember information by name.
```

## Exercises

### Exercise 1

Create three variables:

```python
first_name = "..."
favorite_food = "..."
home_city = "..."
```

Print each one.

### Exercise 2

Create a variable named `score` and set it to `0`.

Then increase it three times.

Starter idea:

```python
score = 0

score = score + 10
print(score)

score = score + 10
print(score)

score = score + 10
print(score)
```

### Exercise 3

Broken code:

```python
favorite color = "red"
2nd_place = "Amit"
user-name = "Lina"
```

Fix these variable names before running them. Write corrected versions using valid Python names.

### Exercise 4

What will this program print?

```python
animal = "cat"
print("animal")
print(animal)
```

Write the output before you run it. Then run it and check your answer.

### Exercise 5

Broken code:

```python
movie_title = "The Blue Door"
print(movie)
```

Find and fix the mistake.

### Exercise 6

Write a small program that stores:

- a book title
- the author's name
- the number of pages

Print each value with a short label.

Example output:

```text
Title:
The Secret Garden
Author:
Frances Hodgson Burnett
Pages:
352
```

## Lesson Checklist

Before you move on, make sure you can:

- explain what a variable is
- create a variable with `name = value`
- print a variable's value without quotation marks
- choose clear lowercase variable names with underscores
- fix a variable name that has spaces, hyphens, or inconsistent spelling
- describe what happens when a variable is reassigned

## Tiny Win

Before today, values may have felt like loose pieces of information.

Now you can name them, reuse them, and change them.

That is the first step toward programs that keep track of real information.

## Tomorrow

Tomorrow, you will work more carefully with numbers and learn how Python handles arithmetic.
