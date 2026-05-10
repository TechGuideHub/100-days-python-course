# Day 08: Input and Output

**Focus:** Asking for user input and showing clear output  
**You will practice:** `print()`, `input()`, prompts, storing answers, combining text, and reading sample runs  
**Estimated time:** 35-45 minutes

## Today's Goal

Today you will learn how Python programs talk with users.

By the end of this lesson, you should be able to:

- show text on the screen with `print()`
- ask the user a question with `input()`
- store the user's answer in a variable
- use that answer later in the program
- write prompts that are clear and easy to read
- explain why input arrives as text
- spot common input and output mistakes

So far, many of your programs have mostly spoken. They printed messages, showed values, and ran from top to bottom.

Today, your programs begin to listen.

## The Big Idea

Most useful programs do not only produce output. They also receive input.

A weather app needs a city. A login screen needs a username. A calculator needs numbers. A search box needs search text. A game needs the player's choices.

That pattern is everywhere:

```text
input -> program -> output
```

In Python, two beginner tools make this possible:

```python
input()
print()
```

`input()` asks the user for information.

`print()` shows information to the user.

Together, they let you build programs that feel less like a fixed page of instructions and more like a short conversation.

## The Mental Model

Think of a program as someone working at a front desk.

The worker asks:

```text
What is your name?
```

The visitor answers:

```text
Maya
```

The worker writes the name down. Later, the worker says:

```text
Welcome, Maya.
```

Python follows the same pattern.

```python
name = input("What is your name? ")
print("Welcome, " + name + ".")
```

If the user types `Maya`, the program shows:

```text
What is your name? Maya
Welcome, Maya.
```

There are three steps:

1. Ask a question.
2. Store the answer.
3. Use the answer.

That shape appears again and again in beginner programs.

## Create Today's File

If you are keeping each day in its own folder, create a folder named:

```text
day-08
```

Many examples today use relative paths like:

```text
day-08/greeting.py
day-08/profile_questions.py
day-08/interview_program.py
```

A relative path starts from your course folder. You do not need full computer-specific folder paths in lesson notes or code comments.

## Output With `print()`

You have already used `print()`. It shows something on the screen.

Save this as `day-08/output_messages.py`:

```python
print("Welcome to Day 08.")
print("This program shows output.")
print("Each print call can place text on a new line.")
```

You should see:

```text
Welcome to Day 08.
This program shows output.
Each print call can place text on a new line.
```

The text inside quotation marks is a string. Each `print()` call usually appears on its own line in the output.

That lets you control what the user sees step by step.

## Input With `input()`

`input()` pauses the program and waits for the user to type something.

Save this as `day-08/greeting.py`:

```python
name = input("What is your name? ")
print("Hello, " + name + ".")
```

If you type `Asha`, you should see:

```text
What is your name? Asha
Hello, Asha.
```

The text inside `input()` is called the prompt.

This line asks a question, waits for the answer, and stores the answer in `name`:

```python
name = input("What is your name? ")
```

Without the variable, Python still receives the answer, but the program forgets it immediately.

```python
input("What is your name? ")
print("Thanks.")
```

If the user types `Ravi`, the program shows:

```text
What is your name? Ravi
Thanks.
```

That program asks a question, but it cannot use the answer because it did not store it.

Most of the time, you want this shape:

```text
variable = input("clear prompt ")
```

## Prompts Matter

A good prompt is clear enough that the user knows what to type.

```python
favorite_food = input("What is your favorite food? ")
print("Favorite food: " + favorite_food)
```

If the user types `dosa`, the output is:

```text
What is your favorite food? dosa
Favorite food: dosa
```

A short prompt can work:

```python
favorite_food = input("Food: ")
print("Favorite food: " + favorite_food)
```

A fuller prompt is often friendlier:

```python
favorite_food = input("What is your favorite food? ")
print("Favorite food: " + favorite_food)
```

Notice the space after the question mark:

```python
name = input("What is your name? ")
```

That space is not a deep Python rule. It is just care for the person using your program.

Without the space, the answer can look squeezed against the prompt:

```text
What is your name?Maya
```

With the space, it reads cleanly:

```text
What is your name? Maya
```

## Combining Text and Input

Once you store input in a variable, you can combine it with other strings.

One way is with `+`.

```python
name = input("What is your name? ")
print("Nice to meet you, " + name + ".")
```

If the user types `Lina`, the program shows:

```text
What is your name? Lina
Nice to meet you, Lina.
```

Read the second line as:

```text
Print "Nice to meet you, "
then the value stored in name
then "."
```

Another beginner-friendly way is to use commas inside `print()`.

```python
name = input("What is your name? ")
print("Nice to meet you,", name)
```

If the user types `Lina`, the program shows:

```text
What is your name? Lina
Nice to meet you, Lina
```

When you use commas, `print()` automatically adds spaces between the pieces.

Both styles are common. For now, choose the one that makes your code easier to read.

## Input Is Text

There is one important rule:

> `input()` always gives you text.

Even if the user types a number, Python receives it as a string.

Save this as `day-08/age_text.py`:

```python
age = input("How old are you? ")
print("You typed: " + age)
print("Python received that answer as text.")
```

If the user types `12`, the program shows:

```text
How old are you? 12
You typed: 12
Python received that answer as text.
```

If you only want to print the answer, text is fine:

```python
age = input("How old are you? ")
print("You are " + age + " years old.")
```

You should see:

```text
How old are you? 12
You are 12 years old.
```

But if you want to do math, text is not enough.

Broken code:

```python
age = input("How old are you? ")
next_year = age + 1
print(next_year)
```

Python cannot add the text `"12"` and the number `1`.

For math, convert the input first.

Save this as `day-08/next_year.py`:

```python
age = input("How old are you? ")
age = int(age)
next_year = age + 1
print("Next year you will be", next_year)
```

If the user types `12`, the output is:

```text
How old are you? 12
Next year you will be 13
```

You do not need to master conversion today. The main idea is simpler:

> User input arrives as text first.

That one fact explains many beginner bugs.

## A Complete Small Program

Here is a small program that asks several questions and prints a short profile.

Save it as `day-08/profile_questions.py`:

```python
name = input("What is your name? ")
city = input("What city do you live in? ")
hobby = input("What is one hobby you enjoy? ")

print("")
print("Profile")
print("Name: " + name)
print("City: " + city)
print("Hobby: " + hobby)
```

If you type these answers:

```text
Ravi
Hyderabad
chess
```

the run looks like this:

```text
What is your name? Ravi
What city do you live in? Hyderabad
What is one hobby you enjoy? chess

Profile
Name: Ravi
City: Hyderabad
Hobby: chess
```

This line prints a blank line:

```python
print("")
```

Blank lines can make output easier to read.

A program is not only better because it runs. It is also better when its output is readable.

## Try It Yourself

Create a file named:

```text
day-08/favorite_place.py
```

Write a program that asks:

- the user's name
- a place they want to visit
- one thing they want to do there

Starter code:

```python
name = input("What is your name? ")
place = input("What place would you like to visit? ")
activity = input("What would you like to do there? ")

print("")
print("Hello, " + name + ".")
print("I hope you get to visit " + place + " and " + activity + ".")
```

If the user types:

```text
Lina
Kyoto
see the temples
```

the program shows:

```text
What is your name? Lina
What place would you like to visit? Kyoto
What would you like to do there? see the temples

Hello, Lina.
I hope you get to visit Kyoto and see the temples.
```

Run it more than once with different answers.

That is how you test an input program:

1. Choose sample inputs.
2. Run the program.
3. Type the inputs.
4. Read the output carefully.
5. Try a different set of inputs.

The code stays the same, but the output can change. That is what makes input powerful.

## Common Mistake

### Mistake 1: Forgetting to store the input

This code runs, but it does not remember the answer:

```python
input("What is your name? ")
print("Hello!")
```

Better:

```python
name = input("What is your name? ")
print("Hello, " + name)
```

If you need the answer later, store it in a variable.

### Mistake 2: Putting the variable name inside quotes

This code runs, but the greeting is wrong:

```python
name = input("What is your name? ")
print("Hello, name")
```

If the user types `Asha`, Python prints:

```text
What is your name? Asha
Hello, name
```

Python prints the word `name` because it is inside quotation marks. Inside quotes, text is just text.

Fixed code:

```python
name = input("What is your name? ")
print("Hello, " + name)
```

Now Python uses the value stored in the variable.

### Mistake 3: Missing spaces in output

This code runs, but the output looks cramped:

```python
name = input("What is your name? ")
print("Hello," + name)
```

If the user types `Maya`, the program prints:

```text
What is your name? Maya
Hello,Maya
```

Fixed code:

```python
name = input("What is your name? ")
print("Hello, " + name)
```

Now it reads properly:

```text
What is your name? Maya
Hello, Maya
```

Tiny spaces matter. They are part of making the program feel clear.

### Mistake 4: Expecting `input()` to understand numbers automatically

Broken code:

```python
age = input("How old are you? ")
print(age + 1)
```

The value from `input()` is text, not a number.

Fixed code:

```python
age = input("How old are you? ")
age = int(age)
print(age + 1)
```

For today's exercises, most input can stay as text unless the question asks you to do arithmetic.

### Mistake 5: Forgetting parentheses

Broken code:

```python
name = input "What is your name? "
```

Fixed code:

```python
name = input("What is your name? ")
print("Hello, " + name)
```

`input` and `print` are functions. Function calls need parentheses.

## Debug It

The programs in this section are broken on purpose. Read each one, explain the problem, then compare it with the fixed version.

### Bug 1

Broken code:

```python
name = input("What is your name? ")
print("Hello, name")
```

What is wrong?

The program prints the word `name`, not the user's actual name. The variable should not be inside the string.

Fixed code:

```python
name = input("What is your name? ")
print("Hello, " + name)
```

### Bug 2

Broken code:

```python
animal = input("What is your favorite animal? ")
print("Your favorite animal is" + animal)
```

If the user types `tiger`, the output is:

```text
Your favorite animal istiger
```

The code runs, but the output is messy.

Fixed code:

```python
animal = input("What is your favorite animal? ")
print("Your favorite animal is " + animal)
```

Sometimes debugging is not about fixing a crash. Sometimes it is about making the result say what you meant.

### Bug 3

Broken code:

```python
name = input("What is your name? "
print("Hello, " + name)
```

What is wrong?

The first line is missing a closing parenthesis. Python may show an error message that mentions `SyntaxError`.

Fixed code:

```python
name = input("What is your name? ")
print("Hello, " + name)
```

When you see an error, do not try to fix five things at once.

Ask:

- What line does Python point to?
- Are the quotation marks paired?
- Are the parentheses paired?
- Are variable names spelled the same way?
- Did I save the file before running it?

Small checks solve many early problems.

## Read the Docs

Python has official documentation for built-in functions like `input()` and `print()`.

Today, look up either:

```text
Python input function documentation
```

or:

```text
Python print function documentation
```

Do not try to understand every detail.

Find one useful idea:

- `input()` reads a line from the user
- `print()` writes output to the screen

Documentation can be dense. That is normal. Your goal is not to memorize it. Your goal is to become comfortable visiting it.

## Mini Challenge

Create a file named:

```text
day-08/interview_program.py
```

Write a small interview program.

It should ask the user at least five questions, such as:

- What is your name?
- Where are you from?
- What is one thing you enjoy?
- What is one food you like?
- What is something you want to learn?

Starter code:

```python
name = input("What is your name? ")
home = input("Where are you from? ")
interest = input("What is one thing you enjoy? ")
food = input("What is one food you like? ")
goal = input("What is something you want to learn? ")

print("")
print("Interview Summary")
print("Name: " + name)
print("From: " + home)
print("Enjoys: " + interest)
print("Likes eating: " + food)
print("Wants to learn: " + goal)
```

If the user types:

```text
Nina
Pune
drawing
idli
Python
```

the program shows:

```text
What is your name? Nina
Where are you from? Pune
What is one thing you enjoy? drawing
What is one food you like? idli
What is something you want to learn? Python

Interview Summary
Name: Nina
From: Pune
Enjoys: drawing
Likes eating: idli
Wants to learn: Python
```

After that works, improve the output so it sounds more like a paragraph.

```python
name = input("What is your name? ")
home = input("Where are you from? ")
interest = input("What is one thing you enjoy? ")
food = input("What is one food you like? ")
goal = input("What is something you want to learn? ")

print("")
print(name + " is from " + home + ".")
print(name + " enjoys " + interest + " and likes eating " + food + ".")
print("One thing " + name + " wants to learn is " + goal + ".")
```

This prepares you for Day 10. A conversation program is still simple, but it feels more alive when it can ask, remember, and respond.

## Real-World Use

Input and output are everywhere.

When you use a search engine:

- input: your search text
- output: search results

When you use a calculator:

- input: numbers and operations
- output: the answer

When you fill out a form:

- input: your name, email, choices, and comments
- output: a confirmation message or saved record

When you play a game:

- input: movement, choices, typed names, menu selections
- output: the game world changing on screen

The tools may look different, but the pattern is familiar:

```text
Ask for information.
Store it.
Use it.
Show a result.
```

That is what you practiced today.

## Recap

Today you learned:

- `print()` shows output
- `input()` asks the user for input
- input should usually be stored in a variable
- prompts should be clear and readable
- input arrives as text
- variables inside quotes are treated as normal text
- spaces matter when combining strings
- some bugs are crashes, and some bugs are messy output

Main idea:

```text
A program becomes interactive when it can ask, remember, and respond.
```

## Exercises

### Exercise 1

Create a file named:

```text
day-08/hello_user.py
```

Ask the user for their name.

Print:

```text
Hello, NAME.
```

Use the actual name the user typed.

### Exercise 2

Create a file named:

```text
day-08/three_questions.py
```

Ask the user three questions:

- What is your name?
- What is your favorite movie, show, or book?
- Why do you like it?

Print a short summary using all three answers.

### Exercise 3

Fix this program.

Broken code:

```python
name = input("What is your name? ")
print("Nice to meet you, name")
```

The output should use the user's actual name.

### Exercise 4

Fix this spacing mistake.

Broken code:

```python
city = input("What city do you live in? ")
print("You live in" + city)
```

The output should look like this, using whatever city the user typed:

```text
You live in Pune
```

### Exercise 5

Create a file named:

```text
day-08/simple_receipt.py
```

Ask the user for:

- an item name
- the shop name
- the price as text

Then print a simple receipt:

```text
Receipt
Shop: Fresh Mart
Item: Apples
Price: 120
```

For this exercise, the price can stay as text. You do not need to do math.

### Exercise 6

Create a file named:

```text
day-08/next_year.py
```

Ask the user for their age. Convert it to an integer with `int()`, then print how old they will be next year.

Starter code:

```python
age = input("How old are you? ")
age = int(age)
next_year = age + 1
print("Next year you will be", next_year)
```

Run it with at least two different ages.

### Exercise 7

Create a file named:

```text
day-08/two_words.py
```

Write a program that asks for two words.

Then print the two words joined together in three different ways.

Example output:

```text
rainbow cloud
rainbow-cloud
rainbowcloud
```

This is good practice for noticing spaces and punctuation in output.

## Lesson Checklist

Before moving on, check that you can:

- use `print()` to show output
- use `input()` to ask for text
- store input in a variable
- write a prompt with a helpful space at the end
- combine stored input with other strings
- explain why `input()` gives you text first
- convert input with `int()` when simple arithmetic is needed
- fix a quoted variable name
- fix cramped output caused by missing spaces
- read a short sample run of an input program

## Tiny Win

Before today, your programs could show messages.

Now they can ask questions, remember answers, and use those answers later.

That is the beginning of interaction.

## Tomorrow

Tomorrow, you will learn how to read error messages with more confidence, so mistakes become clues instead of walls.
