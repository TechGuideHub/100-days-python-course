# Day 13: `else` and `elif`

**Focus:** Choosing between two or more paths in an `if` statement  
**You will practice:** `else`, `elif`, branch order, one-choice decisions, indentation, and debugging decision chains  
**Estimated time:** 40-50 minutes

## Today's Goal

Today you will learn how to give an `if` statement more than one path.

By the end of this lesson, you should be able to:

- use `else` when a program needs a fallback
- use `elif` when a program has several possible choices
- explain why only one branch runs in an `if` / `elif` / `else` chain
- put overlapping conditions in a sensible order
- choose between repeated `if` statements and an `elif` chain
- fix common mistakes with colons, indentation, and `else`

Yesterday, an `if` statement gave your program one possible action.

Today, your program learns what to do when that condition is false, and how to choose from several possible results.

Broken examples are labeled clearly. Read them for practice; run them only when you want to see the error.

## The Big Idea

A plain `if` statement checks one condition.

```python
age = 17

if age >= 18:
    print("You can vote.")
```

For this value, nothing prints. The condition is false, so Python skips the indented line.

Sometimes skipping is not enough. A program often needs a second path:

```text
If this condition is true, do one thing.
Otherwise, do something else.
```

That is what `else` is for.

```python
age = 17

if age >= 18:
    print("You can vote.")
else:
    print("You are not old enough to vote yet.")
```

You should see:

```text
You are not old enough to vote yet.
```

The `else` branch runs only when the `if` condition is false.

Some decisions have more than two paths. A score might become an A, B, C, D, or F. A temperature might be hot, warm, mild, or cold.

For that, use `elif`.

```python
score = 82

if score >= 90:
    grade = "A"
elif score >= 80:
    grade = "B"
elif score >= 70:
    grade = "C"
elif score >= 60:
    grade = "D"
else:
    grade = "F"

print("Grade:", grade)
```

You should see:

```text
Grade: B
```

`elif` means "else if." It gives Python another condition to check only if the earlier condition was false.

## The Mental Model

Think of an `if` / `elif` / `else` chain as one ordered decision.

Python reads the chain from top to bottom:

```text
Try the first condition.
If that is false, try the next condition.
If that is false, try the next condition.
If none are true, use else.
```

The first true branch wins. After Python chooses one branch, it leaves the chain.

Here is the shape:

```text
if first condition:
    run this branch
elif second condition:
    run this branch instead
elif third condition:
    run this branch instead
else:
    run this fallback branch
```

Only one branch in that chain can run.

Example:

```python
temperature = 31

if temperature >= 35:
    print("It is very hot.")
elif temperature >= 25:
    print("It is warm.")
elif temperature >= 15:
    print("It is mild.")
else:
    print("It is cold.")
```

You should see:

```text
It is warm.
```

For `temperature = 31`, this condition is false:

```text
temperature >= 35
```

This condition is true:

```text
temperature >= 25
```

Python prints `It is warm.` and stops checking the chain.

This matters because `31` is also greater than or equal to `15`. Python does not print `It is mild.` because the earlier true branch already won.

Use `elif` when the program should choose one result from a group.

## Try It Yourself

Create a file named:

```text
day-13/ticket_price.py
```

Code:

```python
age = int(input("How old are you? "))

if age < 5:
    price = 0
elif age < 18:
    price = 8
elif age < 65:
    price = 12
else:
    price = 7

print("Ticket price:", price)
```

Run the file from your course folder:

```bash
python day-13/ticket_price.py
```

If your computer uses `py`, use:

```bash
py day-13/ticket_price.py
```

If your computer uses `python3`, use:

```bash
python3 day-13/ticket_price.py
```

Run the program several times.

Try these ages:

```text
3
12
30
70
```

Before each run, predict the price.

For `age = 3`, Python chooses the first branch because `3 < 5` is true. It does not keep checking whether `3 < 18` or `3 < 65`.

For `age = 30`, the first two conditions are false, but `30 < 65` is true, so the price becomes `12`.

The order works because the smallest ages are checked first.

## Common Mistake

### Mistake 1: Adding a condition to `else`

`else` already means "if none of the earlier conditions were true." It does not take its own condition.

Broken code:

```python
password = "sunrise"

if password == "sunrise":
    print("Access granted.")
else password != "sunrise":
    print("Access denied.")
```

Fixed code:

```python
password = "sunrise"

if password == "sunrise":
    print("Access granted.")
else:
    print("Access denied.")
```

You should see:

```text
Access granted.
```

### Mistake 2: Checking broad conditions too early

This code runs, but the order is wrong:

```python
score = 95

if score >= 60:
    grade = "D"
elif score >= 70:
    grade = "C"
elif score >= 80:
    grade = "B"
elif score >= 90:
    grade = "A"
else:
    grade = "F"

print(grade)
```

You should see:

```text
D
```

That is not the grade we wanted. Since `95 >= 60` is true, Python chooses the first branch and stops.

For grading code, check the highest scores first:

```python
score = 95

if score >= 90:
    grade = "A"
elif score >= 80:
    grade = "B"
elif score >= 70:
    grade = "C"
elif score >= 60:
    grade = "D"
else:
    grade = "F"

print(grade)
```

You should see:

```text
A
```

When conditions overlap, put the most specific or highest-priority condition first.

### Mistake 3: Using separate `if` statements for one choice

Sometimes more than one condition can be true.

```python
temperature = 31

if temperature >= 35:
    print("It is very hot.")
if temperature >= 25:
    print("It is warm.")
if temperature >= 15:
    print("It is mild.")
else:
    print("It is cold.")
```

You should see:

```text
It is warm.
It is mild.
```

The first three checks are separate questions, so Python can answer yes to more than one of them.

If you want one temperature message, use one chain:

```python
temperature = 31

if temperature >= 35:
    print("It is very hot.")
elif temperature >= 25:
    print("It is warm.")
elif temperature >= 15:
    print("It is mild.")
else:
    print("It is cold.")
```

You should see:

```text
It is warm.
```

Repeated `if` statements are useful when you want to check several independent facts. Use `elif` when the program should choose one path.

### Mistake 4: Forgetting colons or indentation

Broken code:

```python
weather = "rain"

if weather == "rain"
print("Take an umbrella.")
else:
    print("Enjoy the day.")
```

There are two problems:

- the `if` line needs a colon
- the `print()` line inside the `if` branch needs indentation

Fixed code:

```python
weather = "rain"

if weather == "rain":
    print("Take an umbrella.")
else:
    print("Enjoy the day.")
```

You should see:

```text
Take an umbrella.
```

The `if`, `elif`, and `else` lines all end with a colon. The code inside each branch is indented.

## Debug It

Here is a program that runs, but gives the wrong badge.

```python
points = 82

if points >= 50:
    print("Bronze")
if points >= 70:
    print("Silver")
if points >= 90:
    print("Gold")
else:
    print("No badge yet")
```

The programmer wanted:

```text
Silver
```

But the program prints:

```text
Bronze
Silver
No badge yet
```

Why does `No badge yet` appear?

The `else` belongs only to the nearest `if`:

```text
if points >= 90:
```

Since `82 >= 90` is false, that final `else` runs. The earlier `if` statements are separate decisions.

The fix is to use one chain, ordered from highest badge to lowest:

```python
points = 82

if points >= 90:
    print("Gold")
elif points >= 70:
    print("Silver")
elif points >= 50:
    print("Bronze")
else:
    print("No badge yet")
```

You should see:

```text
Silver
```

When decision code surprises you, ask:

- Which value is being checked?
- Which condition is checked first?
- Can more than one condition be true?
- Should the program choose one branch or several separate branches?
- Does an `else` belong to the `if` you think it belongs to?

You can add small print statements while debugging:

```python
points = 82

print("points:", points)
print("points >= 90:", points >= 90)
print("points >= 70:", points >= 70)
print("points >= 50:", points >= 50)

if points >= 90:
    print("Gold")
elif points >= 70:
    print("Silver")
elif points >= 50:
    print("Bronze")
else:
    print("No badge yet")
```

The extra prints help you see the same true-or-false answers Python is using.

## Read the Docs

Find Python's official tutorial section about `if` statements:

```text
https://docs.python.org/3/tutorial/controlflow.html#if-statements
```

Look for an example that uses:

```text
if
elif
else
```

Notice two details:

- Python uses `elif`, not `else if`
- each branch header ends with a colon

You do not need to read the whole page today. Your goal is to recognize the shape of the decision chain in official documentation.

## Mini Challenge

Create a file named:

```text
day-13/daily_decision.py
```

Write a program that asks how much free time the user has.

Use these rules:

```text
less than 10 minutes   -> Take a short walk.
less than 30 minutes   -> Read a few pages.
less than 60 minutes   -> Practice Python.
60 minutes or more     -> Build something small.
```

One possible solution:

```python
minutes = int(input("How many free minutes do you have? "))

if minutes < 10:
    print("Take a short walk.")
elif minutes < 30:
    print("Read a few pages.")
elif minutes < 60:
    print("Practice Python.")
else:
    print("Build something small.")
```

Run it with:

```text
5
20
45
90
```

Then change the messages to make the program your own. Keep the decision structure the same.

## Real-World Use

`else` and `elif` appear whenever a program sorts one situation into one result.

Examples:

- a checkout program chooses a shipping price
- a game chooses a message based on the player's score
- a school system turns a score into a grade
- a calendar app labels an event as past, today, or upcoming
- a bank app chooses whether to approve, review, or reject a transaction
- a music app chooses what message to show when a playlist is empty, short, or long

The details change, but the pattern stays familiar:

```text
Check the first possibility.
If that is not right, check the next.
If none match, use the fallback.
```

Programs feel more useful when they can choose a path based on the situation.

## Recap

Today you learned:

- `else` gives an `if` statement a fallback path
- `elif` means "else if"
- `elif` checks another condition in the same chain
- only one branch runs in an `if` / `elif` / `else` chain
- Python checks branches from top to bottom
- order matters when conditions overlap
- repeated `if` statements are different from an `elif` chain
- `if`, `elif`, and `else` lines need colons
- the code inside each branch must be indented
- `else` does not take a condition

Main idea:

```text
Use else and elif when a program needs to choose one path from several possibilities.
```

## Lesson Checklist

Before moving on, check that you can:

- write an `if` / `else` statement
- write an `if` / `elif` / `else` chain
- explain when the `else` branch runs
- explain why an `else` line has no condition
- predict which branch will run first
- put overlapping conditions in the right order
- choose `elif` when only one result should happen
- fix missing colons and indentation problems
- debug a surprising result by checking each condition

## Exercises

### Exercise 1

Create a file named:

```text
day-13/even_or_odd.py
```

Start with:

```python
number = 12
```

Use `if` and `else` to print whether the number is even or odd.

Hint:

```text
number % 2 == 0
```

Try at least two different numbers.

### Exercise 2

Create a file named:

```text
day-13/weather_advice.py
```

Start with:

```python
weather = "rain"
```

Write an `if` / `elif` / `else` chain:

- if the weather is `"rain"`, print `Take an umbrella.`
- if the weather is `"sun"`, print `Wear sunglasses.`
- if the weather is `"snow"`, print `Wear warm shoes.`
- otherwise, print `Check the weather again.`

Change the value of `weather` and run the program several times.

### Exercise 3

Predict the output before running this code:

```python
level = 4

if level >= 5:
    print("Expert")
elif level >= 3:
    print("Intermediate")
elif level >= 1:
    print("Beginner")
else:
    print("New")
```

Then run it and check your prediction.

### Exercise 4

Fix this code.

Broken code:

```python
age = 16

if age >= 18:
    print("Adult")
else age < 18:
    print("Not adult")
```

The corrected program should print:

```text
Not adult
```

### Exercise 5

Fix this code so it chooses only one message:

```python
points = 82

if points >= 50:
    print("Bronze")
if points >= 70:
    print("Silver")
if points >= 90:
    print("Gold")
else:
    print("No badge yet")
```

For `points = 82`, the corrected program should print:

```text
Silver
```

### Exercise 6

Create a file named:

```text
day-13/simple_login.py
```

Ask the user for a password.

If the password is `"python123"`, print:

```text
Welcome.
```

Otherwise, print:

```text
Try again.
```

Use `input()`, `if`, and `else`.

### Exercise 7

Create a file named:

```text
day-13/restaurant_rating.py
```

Start with:

```python
rating = 4
```

Write a program that prints:

```text
Excellent
```

for `5`,

```text
Good
```

for `4`,

```text
Okay
```

for `3`, and:

```text
Needs review
```

for anything else.

Use `if`, `elif`, and `else`.

### Exercise 8

Write a program that asks for a number of items in a cart.

Use these rules:

```text
0 items       -> Your cart is empty.
1 item        -> You have one item.
2 to 5 items  -> You have a few items.
more than 5   -> You have several items.
```

Test it with:

```text
0
1
3
8
```

Pay attention to the order of your conditions.

### Exercise 9

Start with:

```python
hour = 14
```

Write an `if` / `elif` / `else` chain that prints:

```text
Good morning.
```

for hours before `12`,

```text
Good afternoon.
```

for hours before `18`, and:

```text
Good evening.
```

for all later hours.

Try the program with `9`, `14`, and `20`.

### Exercise 10

Look at this code:

```python
score = 72

if score >= 90:
    print("A")
elif score >= 80:
    print("B")
elif score >= 70:
    print("C")
elif score >= 60:
    print("D")
else:
    print("F")
```

Answer these questions before running it:

- Which conditions are false?
- Which condition is true first?
- Which grade prints?
- What changes if `score` becomes `58`?

Then run the code and compare it with your answers.

## Tiny Win

Before today, an `if` statement gave your program one possible action.

Now your program can choose between paths and use a fallback when none of the earlier conditions fit.

That is a real step toward programs that respond to the situation instead of doing the same thing every time.

## Tomorrow

Tomorrow, you will learn boolean logic.

That will let you combine conditions with words like:

```text
and
or
not
```
