# Day 12: `if` Statements

**Focus:** Making code run only when a condition is true  
**You will practice:** Writing basic `if` statements, using comparisons, indenting blocks, and fixing common condition mistakes  
**Estimated time:** 35-45 minutes

## Today's Goal

Today you will learn how to make a Python program choose whether to run a piece of code.

By the end of this lesson, you should be able to:

- write a simple `if` statement
- use a comparison as a condition
- place the colon at the end of the `if` line
- indent the code that belongs inside the `if` statement
- explain why an unindented line runs normally after the `if` block
- fix common `if` statement mistakes

The main idea is:

> If this condition is true, run this indented block.

Broken examples are labeled clearly. Study them first; run them only when you want to see the error.

## The Big Idea

So far, many of your programs have run from top to bottom.

Example:

```python
print("Welcome.")
print("Loading account.")
print("Done.")
```

You should see:

```text
Welcome.
Loading account.
Done.
```

An `if` statement changes that pattern. It lets Python ask a yes-or-no question before running some code.

Example:

```python
age = 18

if age >= 18:
    print("You can vote.")
```

You should see:

```text
You can vote.
```

The condition is:

```text
age >= 18
```

That condition asks:

```text
Is age greater than or equal to 18?
```

The answer is either `True` or `False`. Because `age` is `18`, the condition is `True`, so Python runs the indented line.

If the condition is `False`, Python skips the indented line.

## The Mental Model

Think of an `if` statement like a gate.

The condition is the question at the gate:

```text
Is this allowed?
```

If the answer is yes, Python goes through the gate and runs the indented code.

If the answer is no, Python walks past the gate and continues after the block.

Example:

```python
age = 16

if age >= 18:
    print("You can vote.")

print("Program finished.")
```

You should see:

```text
Program finished.
```

The line inside the `if` statement did not run because the condition was `False`.

This line still ran:

```python
print("Program finished.")
```

It is not indented, so it does not belong to the `if` statement.

Indentation is how Python knows what is inside the gate.

The basic shape is:

```text
if condition:
    code that runs when the condition is true
```

There are three pieces to notice:

- `if` starts the decision
- the condition must give a yes-or-no answer
- the colon tells Python that an indented block comes next

Example:

```python
is_raining = True

if is_raining:
    print("Take an umbrella.")
```

You should see:

```text
Take an umbrella.
```

Here, the condition is already a boolean value. Since `is_raining` is `True`, the indented line runs.

## Try It Yourself

Create a file named:

```text
day-12/if_practice.py
```

Code:

```python
temperature = 32

if temperature > 30:
    print("It is hot today.")

print("Weather check complete.")
```

Run the file from your course folder:

```bash
python day-12/if_practice.py
```

If your computer uses `py`, use:

```bash
py day-12/if_practice.py
```

If your computer uses `python3`, use:

```bash
python3 day-12/if_practice.py
```

You should see:

```text
It is hot today.
Weather check complete.
```

Now change the first line:

```python
temperature = 22
```

Run the program again.

You should see:

```text
Weather check complete.
```

The final line still runs because it is not indented. Only this line depends on the condition:

```python
print("It is hot today.")
```

That is the most important thing to notice today.

## Common Mistake

### Mistake 1: Forgetting the colon

Broken code:

```python
age = 18

if age >= 18
    print("You can vote.")
```

Python expects a colon at the end of the `if` line.

Fixed code:

```python
age = 18

if age >= 18:
    print("You can vote.")
```

The colon means:

```text
The indented block starts next.
```

### Mistake 2: Forgetting indentation

Broken code:

```python
is_member = True

if is_member:
print("Welcome back.")
```

The line after the `if` statement must be indented if it belongs inside the `if`.

Fixed code:

```python
is_member = True

if is_member:
    print("Welcome back.")
```

Python uses indentation as part of the language. It is not decoration.

### Mistake 3: Using `=` instead of `==`

Broken code:

```python
password = "python"

if password = "python":
    print("Access granted.")
```

One equals sign stores a value. Two equals signs compare values.

Fixed code:

```python
password = "python"

if password == "python":
    print("Access granted.")
```

Read the condition as:

```text
Is password equal to "python"?
```

That question can be answered with `True` or `False`.

### Mistake 4: Indenting too much

This code runs, but the indentation changes the meaning:

```python
temperature = 22

if temperature > 30:
    print("It is hot today.")
    print("Weather check complete.")
```

You might expect the program to print `Weather check complete.` every time, but it does not. That line is indented, so it also belongs to the `if` statement.

Fixed code:

```python
temperature = 22

if temperature > 30:
    print("It is hot today.")

print("Weather check complete.")
```

Now the final line runs no matter what the temperature is.

## Debug It

Here is a broken program.

Broken code:

```python
score = 85

if score >= 70
print("You passed.")
```

There are two problems:

- the `if` line is missing a colon
- the `print()` line needs to be indented

Fixed code:

```python
score = 85

if score >= 70:
    print("You passed.")
```

You should see:

```text
You passed.
```

Here is another broken program.

Broken code:

```python
username = "maya"

if username = "maya":
    print("Hello, Maya.")
```

The problem is in the condition. The code uses `=`, which assigns a value. A condition needs `==` to compare values.

Fixed code:

```python
username = "maya"

if username == "maya":
    print("Hello, Maya.")
```

You should see:

```text
Hello, Maya.
```

When you debug an `if` statement, check these first:

- Does the `if` line end with a colon?
- Is the code inside the `if` statement indented?
- Does the condition use `==` when comparing values?
- Are only the lines that depend on the condition indented?

## Read the Docs

Find Python's official tutorial section about `if` statements:

```text
https://docs.python.org/3/tutorial/controlflow.html#if-statements
```

You may see examples with `elif` and `else`. You do not need those yet.

For today, look only for the basic shape:

```text
if condition:
    statement
```

The documentation may use formal words such as "compound statement" or "suite." For now, translate that into:

```text
An if statement controls an indented block of code.
```

## Mini Challenge

Create a file named:

```text
day-12/snack_checker.py
```

Write a program that decides whether someone has enough money to buy a snack.

Use these variables:

```python
snack_name = "muffin"
snack_price = 3
money_available = 5
```

If `money_available` is greater than or equal to `snack_price`, print:

```text
You can buy the muffin.
```

One possible solution:

```python
snack_name = "muffin"
snack_price = 3
money_available = 5

if money_available >= snack_price:
    print("You can buy the " + snack_name + ".")
```

Run the program. Then change `money_available` to `2` and run it again.

This time, nothing should print. That may feel unfinished, but it is exactly how a plain `if` statement works.

Tomorrow you will learn how to give Python a second path for when the condition is false.

## Real-World Use

Real programs use `if` statements constantly.

Examples:

- a website shows a logout button if the user is logged in
- a game ends if the player's health reaches zero
- a store shows a warning if an item is out of stock
- a bank app blocks a transfer if the balance is too low
- a school app marks an assignment late if it is submitted after the deadline
- a music app shows a download button if a song is available offline

In each case, the program checks a condition. If the condition is true, it runs a specific piece of code.

That is how programs begin to respond to the situation instead of doing the same thing every time.

## Recap

Today you learned:

- an `if` statement lets a program make a decision
- the condition must give a `True` or `False` answer
- comparisons are often used as conditions
- an `if` line ends with a colon
- the code inside the `if` statement must be indented
- indented lines run only when the condition is `True`
- unindented lines after the block run normally
- `=` assigns a value, while `==` compares values

Main idea:

```text
An if statement runs an indented block only when its condition is true.
```

## Lesson Checklist

Before moving on, check that you can:

- write a simple `if` statement
- explain what the condition is checking
- use `>`, `<`, `>=`, `<=`, `==`, or `!=` in a condition
- remember the colon at the end of the `if` line
- indent the lines that belong inside the `if` statement
- leave later lines unindented when they should always run
- fix a missing colon, missing indentation, or `=`/`==` mistake

## Exercises

### Exercise 1

Write a program with this variable:

```python
age = 20
```

If `age` is greater than or equal to `18`, print:

```text
Adult
```

Change `age` to `12` and run the program again.

### Exercise 2

Fix this code.

Broken code:

```python
is_sunny = True

if is_sunny
    print("Wear sunglasses.")
```

### Exercise 3

Fix this code.

Broken code:

```python
has_ticket = True

if has_ticket:
print("You may enter.")
```

### Exercise 4

Fix this code.

Broken code:

```python
favorite_color = "blue"

if favorite_color = "blue":
    print("That is my favorite too.")
```

### Exercise 5

Predict the output before running the code:

```python
points = 9

if points > 10:
    print("Bonus unlocked.")

print("Score checked.")
```

Then run it and check your prediction.

### Exercise 6

Write a program that stores:

```python
temperature = 5
```

If the temperature is less than `10`, print:

```text
Bring a jacket.
```

Then try the program with `temperature = 15`.

### Exercise 7

Create a variable:

```python
password = "python"
```

Write an `if` statement that prints:

```text
Access granted.
```

only if the password is equal to `"python"`.

Then change the password and run the program again.

### Exercise 8

Write a program about a book, game, movie, or song.

Create one boolean variable about it.

Examples:

```python
is_available = True
is_finished = False
has_downloaded = True
```

Use an `if` statement to print a message only when the boolean is `True`.

### Exercise 9

Write a small program with this variable:

```python
battery_percent = 18
```

If the battery percent is less than `20`, print:

```text
Low battery.
```

Then change the number to `75` and run it again.

### Exercise 10

Look at this code:

```python
level = 3

if level >= 2:
    print("New area unlocked.")
    print("Keep going.")

print("Game saved.")
```

Answer these questions before running it:

- Which lines belong inside the `if` statement?
- Which line runs no matter what?
- What changes if `level` becomes `1`?

Then run the code and compare it with your answers.

## Tiny Win

Today, your programs gained a new ability.

They can skip code when a condition is false.

That small idea is the beginning of choice in Python.

## Tomorrow

Tomorrow, you will learn `else` and `elif`.

That will let your programs choose between multiple paths instead of only asking:

```text
Should I run this block or skip it?
```
