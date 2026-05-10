# Day 19: Practice Day: Decision Problems

**Focus:** Turning decision rules into working Python programs  
**You will practice:** comparisons, `if`, `elif`, `else`, boolean logic, truthy and falsy checks, nested decisions, and logic debugging  
**Estimated time:** 60-75 minutes

## Today's Goal

Today is a practice day.

You are not learning a new keyword. You are using the decision tools you already know:

- comparisons
- `if`, `else`, and `elif`
- `and`, `or`, and `not`
- nested conditions
- clear boolean variable names
- truthy and falsy values
- debugging habits for logic mistakes

By the end of this lesson, you should be able to:

- read a small decision rule and turn it into code
- choose between an `elif` chain, nested conditions, and one combined condition
- write conditions that match the rule you mean
- test more than the easy case
- find common logic bugs by printing smaller boolean values
- feel ready for tomorrow's quiz game project

The goal is not to get every problem perfect on the first try.

The goal is to practice checking your thinking.

## The Big Idea

Decision code is where a program starts to feel useful.

A program can ask:

```text
Is this answer correct?
Is the user allowed to continue?
Which message should we show?
What should happen when the input is empty?
```

In Python, those questions become conditions:

```python
answer == "paris"
score >= 3
username != ""
has_ticket and not is_banned
```

Then `if`, `elif`, and `else` choose what happens next.

Use this rhythm today:

```text
Understand the rule.
Write the condition.
Predict the result.
Run the code.
Test a few different cases.
Fix the smallest wrong piece.
```

That rhythm matters more than any one answer. It is also exactly what you will need tomorrow when you build a quiz game.

## The Mental Model

Think of decision code as a set of small yes-or-no questions.

Example:

```python
is_correct = answer == "paris"
has_enough_points = score >= 5
name_was_entered = name != ""
```

Once the small questions are clear, the final decision is easier to read:

```python
if is_correct:
    print("Correct.")
else:
    print("Not quite.")
```

When a condition becomes confusing, do not stare at the long line harder. Make it smaller.

Code:

```python
age = 16
has_ticket = True
with_adult = False

is_old_enough = age >= 18
has_supervision = is_old_enough or with_adult
can_enter = has_ticket and has_supervision

print("is_old_enough:", is_old_enough)
print("has_supervision:", has_supervision)
print("can_enter:", can_enter)
```

You should see:

```text
is_old_enough: False
has_supervision: False
can_enter: False
```

Main practice habit:

```text
Name the question. Then test whether the answer matches the rule.
```

## Warm-Up

Before writing new programs, warm up by reading conditions.

For each example, predict the output before running it.

### Warm-Up 1

Code:

```python
score = 7

if score >= 10:
    print("Gold")
elif score >= 5:
    print("Silver")
else:
    print("Keep going")
```

You should see:

```text
Silver
```

`score >= 10` is false, but `score >= 5` is true. Python chooses the first true branch in the chain.

### Warm-Up 2

Code:

```python
answer = ""

if answer:
    print("Answer received.")
else:
    print("No answer yet.")
```

You should see:

```text
No answer yet.
```

An empty string is falsy, so Python treats it like false in an `if` condition.

### Warm-Up 3

Code:

```python
age = 14
has_ticket = True
with_adult = False

if has_ticket and (age >= 16 or with_adult):
    print("Entry allowed.")
else:
    print("Entry denied.")
```

You should see:

```text
Entry denied.
```

The person has a ticket, but they are not at least `16` and they are not with an adult.

This grouped condition is false:

```python
age >= 16 or with_adult
```

Because that part is false, the whole condition is false.

### Warm-Up 4

Code:

```python
has_account = True
password_correct = False

if has_account:
    if password_correct:
        print("Welcome.")
    else:
        print("Wrong password.")
else:
    print("No account found.")
```

You should see:

```text
Wrong password.
```

The outer condition passes, so Python reaches the inner condition. The password is not correct, so the inner `else` runs.

## Practice Problems

For each problem, use the same practice rhythm:

```text
Read the rule.
Write the code.
Predict several cases.
Run the code.
Fix one small thing at a time.
```

Do not rush the prediction step. Prediction is how you learn to think like the interpreter.

### Practice Problem 1: Temperature Label

Create a file named `day-19/temperature_label.py`.

Write a program that labels a temperature.

Rules:

```text
Below 0   -> Freezing
0 to 15   -> Cold
16 to 25  -> Mild
26 to 35  -> Warm
Above 35  -> Hot
```

Start with:

```python
temperature = 22
```

Code:

```python
temperature = 22

if temperature < 0:
    label = "Freezing"
elif temperature <= 15:
    label = "Cold"
elif temperature <= 25:
    label = "Mild"
elif temperature <= 35:
    label = "Warm"
else:
    label = "Hot"

print("Temperature:", temperature)
print("Label:", label)
```

Check these cases:

| Temperature | Label |
| --- | --- |
| `-3` | `Freezing` |
| `0` | `Cold` |
| `15` | `Cold` |
| `16` | `Mild` |
| `25` | `Mild` |
| `26` | `Warm` |
| `36` | `Hot` |

Notice the second condition:

```python
elif temperature <= 15:
```

At that point, Python already knows `temperature < 0` was false. You do not need to write this longer condition:

```python
temperature >= 0 and temperature <= 15
```

If `36` prints `"Warm"`, check the order of your `elif` branches.

If `15` prints `"Mild"`, check whether you used `<` when you meant `<=`.

### Practice Problem 2: Login Message

Create a file named `day-19/login_message.py`.

Write a program that checks a username and password.

Start with:

```python
saved_username = "student"
saved_password = "python123"

typed_username = "student"
typed_password = "python123"
account_locked = False
```

Rules:

```text
If the account is locked, print "Account locked."
Otherwise, if both the username and password are correct, print "Welcome."
Otherwise, print "Login failed."
```

Code:

```python
saved_username = "student"
saved_password = "python123"

typed_username = "student"
typed_password = "python123"
account_locked = False

username_matches = typed_username == saved_username
password_matches = typed_password == saved_password
can_log_in = username_matches and password_matches and not account_locked

if account_locked:
    print("Account locked.")
elif can_log_in:
    print("Welcome.")
else:
    print("Login failed.")
```

Check these cases:

| Username | Password | Locked | Output |
| --- | --- | --- | --- |
| `student` | `python123` | `False` | `Welcome.` |
| `student` | `wrong` | `False` | `Login failed.` |
| `sam` | `python123` | `False` | `Login failed.` |
| `student` | `python123` | `True` | `Account locked.` |

This problem has one high-priority condition:

```python
account_locked
```

If the account is locked, the program should say that before checking the normal login result.

Try this while debugging:

```python
print("username_matches:", username_matches)
print("password_matches:", password_matches)
print("can_log_in:", can_log_in)
```

If the final message surprises you, inspect those three values first.

### Practice Problem 3: Quiz Answer Checker

Create a file named `day-19/quiz_answer_checker.py`.

Write a program that checks one quiz answer.

Start with:

```python
correct_answer = "python"
user_answer = input("What language are you learning? ")
```

Rules:

```text
If the user enters nothing, print "Please type an answer."
If the answer is correct, print "Correct."
Otherwise, print "Not quite."
```

Try this first:

```python
correct_answer = "python"
user_answer = input("What language are you learning? ")

if not user_answer:
    print("Please type an answer.")
elif user_answer == correct_answer:
    print("Correct.")
else:
    print("Not quite.")
```

Check these cases:

| Input | Output |
| --- | --- |
| `python` | `Correct.` |
| `java` | `Not quite.` |
| empty input | `Please type an answer.` |

Now make the answer check friendlier:

```python
correct_answer = "python"
user_answer = input("What language are you learning? ")

clean_answer = user_answer.strip().lower()

if not clean_answer:
    print("Please type an answer.")
elif clean_answer == correct_answer:
    print("Correct.")
else:
    print("Not quite.")
```

Now these inputs should also work:

| Input | Output |
| --- | --- |
| `Python` | `Correct.` |
| ` PYTHON ` | `Correct.` |
| spaces only | `Please type an answer.` |

`strip()` removes extra spaces from the beginning and end of a string.

`lower()` changes letters to lowercase.

Together, they make answer checking friendlier without changing the decision pattern.

If `" PYTHON "` does not count as correct, print:

```python
print("user_answer:", user_answer)
print("clean_answer:", clean_answer)
```

Look carefully at the value being compared.

### Practice Problem 4: Checkout Decision

Create a file named `day-19/checkout_decision.py`.

Write a program that decides whether an order can be placed.

Start with:

```python
cart_total = 42
items_in_cart = 3
payment_method = "card"
shipping_country = "India"
```

Rules:

```text
The order can be placed if:

The cart has at least one item.
The cart total is greater than 0.
There is a payment method.
The shipping country is not empty.
```

Code:

```python
cart_total = 42
items_in_cart = 3
payment_method = "card"
shipping_country = "India"

has_items = items_in_cart > 0
has_positive_total = cart_total > 0
has_payment_method = bool(payment_method)
has_shipping_country = bool(shipping_country)

can_place_order = (
    has_items
    and has_positive_total
    and has_payment_method
    and has_shipping_country
)

if can_place_order:
    print("Order placed.")
else:
    print("Order cannot be placed.")
```

Check these cases:

| Items | Total | Payment | Country | Output |
| --- | --- | --- | --- | --- |
| `3` | `42` | `"card"` | `"India"` | `Order placed.` |
| `0` | `42` | `"card"` | `"India"` | `Order cannot be placed.` |
| `3` | `0` | `"card"` | `"India"` | `Order cannot be placed.` |
| `3` | `42` | `""` | `"India"` | `Order cannot be placed.` |
| `3` | `42` | `"card"` | `""` | `Order cannot be placed.` |

Empty strings are falsy. This:

```python
bool(payment_method)
```

becomes `False` when `payment_method` is an empty string.

You could also write:

```python
has_payment_method = payment_method != ""
```

Both versions are reasonable at this stage.

If the program places an order with an empty payment method, print:

```python
print("payment_method:", payment_method)
print("has_payment_method:", has_payment_method)
```

Then check whether your final condition actually uses `has_payment_method`.

### Practice Problem 5: Staged Package Pickup

Create a file named `day-19/staged_package_pickup.py`.

This problem is best written with nested conditions because each step depends on the previous step.

Start with:

```python
has_pickup_code = True
name_matches = True
package_ready = False
```

Rules:

```text
First, check the pickup code.
If the pickup code is present, check whether the name matches.
If the name matches, check whether the package is ready.
```

Code:

```python
has_pickup_code = True
name_matches = True
package_ready = False

if has_pickup_code:
    print("Pickup code accepted.")

    if name_matches:
        print("Name confirmed.")

        if package_ready:
            print("Package ready.")
        else:
            print("Package not ready yet.")
    else:
        print("Name does not match.")
else:
    print("Pickup code needed.")
```

Check the final message for each case:

| Pickup code | Name matches | Package ready | Final message |
| --- | --- | --- | --- |
| `True` | `True` | `True` | `Package ready.` |
| `True` | `True` | `False` | `Package not ready yet.` |
| `True` | `False` | `True` | `Name does not match.` |
| `False` | `True` | `True` | `Pickup code needed.` |

This is a staged decision. If there is no pickup code, the program should not talk about whether the package is ready. That is why nesting fits.

If a message appears in the wrong situation, ask:

```text
Which if does this else belong to?
Is this message indented under the correct condition?
```

With nested code, indentation is part of the meaning.

## Try It Yourself

Now choose one of these small decision problems and write it without looking at a solution first.

### Option A: Simple Badge System

Rules:

```text
90 or higher -> Gold
70 or higher -> Silver
50 or higher -> Bronze
Below 50     -> No badge yet
```

Use:

```python
points = 74
```

Test:

```text
95
70
50
49
```

Question to ask:

```text
Should the highest point checks come first or last?
```

### Option B: Form Checker

Rules:

```text
If the name is empty, print "Name required."
Else if the email is empty, print "Email required."
Else if the password is shorter than 8 characters, print "Password too short."
Else print "Form complete."
```

Use:

```python
name = "Asha"
email = ""
password = "python123"
```

Test:

```text
empty name
empty email
short password
all fields filled correctly
```

Question to ask:

```text
Which problem should the program report first?
```

### Option C: Small Game Door

Rules:

```text
The player can open the door if:

They have the key.
They are not out of energy.
```

If they do not have the key, print:

```text
You need the key.
```

If they have the key but energy is `0`, print:

```text
You are too tired to open the door.
```

Otherwise, print:

```text
The door opens.
```

Use:

```python
has_key = True
energy = 2
```

Question to ask:

```text
Would this be clearer with boolean logic, nesting, or an elif chain?
```

There is not always only one correct shape. Choose the shape that makes the rule easiest to read.

## Common Mistake

Practice days are good days to notice bug habits.

### Mistake 1: Using `or` like English shorthand

Broken code:

```python
answer = "b"

if answer == "a" or "b":
    print("Valid answer")
```

This condition always acts true because the string `"b"` is truthy.

Fixed code:

```python
answer = "b"

if answer == "a" or answer == "b":
    print("Valid answer")
```

At this stage, use this rule:

```text
Each side of or should be a complete yes-or-no question.
```

### Mistake 2: Putting `elif` branches in the wrong order

Broken code:

```python
score = 95

if score >= 50:
    print("Bronze")
elif score >= 70:
    print("Silver")
elif score >= 90:
    print("Gold")
```

You should see:

```text
Bronze
```

For overlapping ranges, put the highest or most specific condition first.

Fixed code:

```python
score = 95

if score >= 90:
    print("Gold")
elif score >= 70:
    print("Silver")
elif score >= 50:
    print("Bronze")
```

### Mistake 3: Forgetting that input is text

Broken code:

```python
age = input("Age: ")

if age >= 18:
    print("Adult")
```

`input()` gives you a string. Comparing that string with the number `18` causes an error.

Fixed code:

```python
age = int(input("Age: "))

if age >= 18:
    print("Adult")
```

Convert input before comparing it with a number.

### Mistake 4: Treating empty input like real input

This code compares the answer before checking whether the answer exists:

```python
answer = input("Answer: ")

if answer == "python":
    print("Correct")
else:
    print("Wrong")
```

That is not always wrong. But for a quiz game, an empty answer may deserve its own message.

Code:

```python
answer = input("Answer: ").strip().lower()

if not answer:
    print("Please type an answer.")
elif answer == "python":
    print("Correct")
else:
    print("Wrong")
```

### Mistake 5: Debugging the whole condition at once

This line is hard to inspect:

```python
if age >= 18 and has_ticket and not is_banned and (is_member or has_coupon):
    print("Special entry allowed.")
```

When it behaves strangely, split it:

```python
is_adult = age >= 18
has_valid_entry = has_ticket and not is_banned
has_special_status = is_member or has_coupon
can_enter = is_adult and has_valid_entry and has_special_status
```

Then print the pieces:

```python
print("is_adult:", is_adult)
print("has_valid_entry:", has_valid_entry)
print("has_special_status:", has_special_status)
print("can_enter:", can_enter)
```

Small booleans are easier to debug than one crowded line.

## Debug It

These programs are intentionally broken. Read the rule first, predict what the broken code does, then study the fix.

### Debug It 1: Weekend Checker

The rule is:

```text
Print "Weekend" only for Saturday or Sunday.
Otherwise print "Weekday".
```

Broken code:

```python
day = "Monday"

if day == "Saturday" or "Sunday":
    print("Weekend")
else:
    print("Weekday")
```

You should see:

```text
Weekend
```

That is wrong for `"Monday"`.

`"Sunday"` is a non-empty string, so it is truthy. The condition always acts true.

Fixed code:

```python
day = "Monday"

if day == "Saturday" or day == "Sunday":
    print("Weekend")
else:
    print("Weekday")
```

Test it with:

```text
Monday
Saturday
Sunday
Friday
```

### Debug It 2: Quiz Score Message

The rule is:

```text
3 correct answers -> Perfect
1 or 2 correct answers -> Nice work
0 correct answers -> Try again
```

Broken code:

```python
correct_count = 3

if correct_count >= 1:
    print("Nice work")
elif correct_count == 3:
    print("Perfect")
else:
    print("Try again")
```

You should see:

```text
Nice work
```

That is wrong because `3` should be perfect.

For `correct_count = 3`, this condition is already true:

```python
correct_count >= 1
```

Python enters that branch and stops. The `correct_count == 3` branch never gets a turn.

Fixed code:

```python
correct_count = 3

if correct_count == 3:
    print("Perfect")
elif correct_count >= 1:
    print("Nice work")
else:
    print("Try again")
```

Test it with:

```text
3
2
1
0
```

When an `elif` chain gives the wrong result, ask:

```text
Did an earlier condition catch the value too soon?
```

## Read the Docs

Today, read documentation in a very small way.

Python's official documentation has a section called "Truth Value Testing."

```text
https://docs.python.org/3/library/stdtypes.html#truth-value-testing
```

Look for examples of values that count as false, especially:

```python
False
None
0
""
[]
```

You do not need to understand every value on the page yet.

For this course right now, the most useful idea is:

```text
Empty values often behave like false in conditions.
```

Then search for an official Python tutorial example that uses `if`, `elif`, and `else`.

Notice the shape:

```python
if condition:
    ...
elif another_condition:
    ...
else:
    ...
```

Documentation is not a place you have to read like a novel. It is a place you visit to confirm one small detail.

## Mini Challenge

Create a file named `day-19/tiny_quiz_round.py`.

Build a tiny quiz round. The program should ask three questions, count how many answers are correct, and print a final message.

Use these questions or write your own:

```text
1. What keyword starts a condition in Python?
2. What value means true in Python?
3. Which operator checks equality?
```

Answers:

```text
if
True
==
```

Starter code:

```python
score = 0

answer_one = input("What keyword starts a condition in Python? ").strip().lower()

if answer_one == "if":
    print("Correct.")
    score = score + 1
else:
    print("Not quite.")

answer_two = input("What value means true in Python? ").strip()

if answer_two == "True":
    print("Correct.")
    score = score + 1
else:
    print("Not quite.")

answer_three = input("Which operator checks equality? ").strip()

if answer_three == "==":
    print("Correct.")
    score = score + 1
else:
    print("Not quite.")

print("Score:", score)

if score == 3:
    print("Perfect round.")
elif score >= 1:
    print("Good practice round.")
else:
    print("Try the round again.")
```

After it works, improve one part:

```text
If the user enters an empty answer, print "No answer entered."
Do not give a point for an empty answer.
```

Try this pattern for one question:

```python
if not answer_one:
    print("No answer entered.")
elif answer_one == "if":
    print("Correct.")
    score = score + 1
else:
    print("Not quite.")
```

Tomorrow's quiz game will use this same core pattern several times:

```text
Ask a question.
Clean the answer.
Check the answer.
Update the score.
Print a final result.
```

## Real-World Use

Decision problems show up in almost every small program.

Examples:

- a quiz checks whether an answer is correct
- a form checks whether required fields are filled
- a shop checks whether an order can be placed
- a game checks whether a player can open a door
- a login page checks whether an account is locked
- a school app turns a score into a grade

The details change, but the pattern stays familiar:

```text
Check facts.
Choose a path.
Handle the fallback.
Test more than one case.
```

Good decision code is not just code that runs. It is code that says the rule clearly enough that you can check it.

## Recap

Today you practiced:

- using comparisons to ask yes-or-no questions
- choosing one branch with `if`, `elif`, and `else`
- combining conditions with `and`, `or`, and `not`
- using nested conditions for staged decisions
- using truthy and falsy values, especially empty strings
- naming boolean variables to make conditions easier to read
- testing boundary cases like `0`, `1`, exact limits, and empty input
- debugging conditions by printing smaller boolean values
- watching for common bugs in ordering, indentation, and incomplete comparisons

Main idea:

```text
A decision problem becomes easier when you turn it into small questions and test each path.
```

## Lesson Checklist

Before moving on, check that you can:

- turn a plain-English rule into an `if` statement
- use `elif` when several outcomes are possible
- decide when a nested condition makes the order of checks clearer
- use `and`, `or`, and `not` to combine small questions
- use truthiness to check whether text was entered
- use explicit comparisons for exact rules
- test below, at, and above a boundary value
- explain why `answer == "a" or "b"` is wrong
- debug a long condition by printing named boolean values
- run a small program with more than one test case

## Exercises

### Exercise 1

Predict the output before running the code:

```python
points = 50

if points > 50:
    print("Above 50")
elif points == 50:
    print("Exactly 50")
else:
    print("Below 50")
```

Then run it.

Change `points` to:

```text
49
51
```

Predict again before each run.

### Exercise 2

Fix this condition:

```python
choice = "yes"

if choice == "yes" or "y":
    print("Continuing")
else:
    print("Stopping")
```

It should print `"Continuing"` only for `"yes"` or `"y"`.

### Exercise 3

Write a program that checks whether a password is long enough.

Rules:

```text
Empty password         -> "Password required."
Less than 8 characters -> "Password too short."
8 or more characters   -> "Password accepted."
```

Use:

```python
password = "python"
```

Then test:

```text
""
"cat"
"python123"
```

### Exercise 4

Create a program that labels a number.

Rules:

```text
negative -> "Negative"
zero     -> "Zero"
positive -> "Positive"
```

Use `if`, `elif`, and `else`.

### Exercise 5

Write a program that checks whether someone can borrow a library book.

Rules:

```text
They can borrow the book if:

They have a library card.
The book is available.
They have fewer than 3 books already borrowed.
```

Use clear boolean variable names before the final `if`.

### Exercise 6

Rewrite this nested code as one condition using `and`:

```python
has_ticket = True
age = 20

if has_ticket:
    if age >= 18:
        print("Entry allowed.")
```

### Exercise 7

Rewrite this one-line condition as nested conditions with helpful messages:

```python
if has_account and password_correct:
    print("Welcome.")
else:
    print("Login failed.")
```

Your nested version should be able to print:

```text
No account found.
Wrong password.
Welcome.
```

### Exercise 8

Debug this program.

The rule is:

```text
Print "Valid score" only when score is between 0 and 100, including both ends.
```

Broken code:

```python
score = 120

if score >= 0 or score <= 100:
    print("Valid score")
else:
    print("Invalid score")
```

Why is it wrong?

Write a fixed version.

### Exercise 9

Write a small quiz question checker.

Ask:

```text
What symbol is used for comments in Python?
```

Correct answer:

```text
#
```

Rules:

```text
Empty answer -> "No answer entered."
Correct answer -> "Correct."
Wrong answer -> "Not quite."
```

### Exercise 10

Choose one program from today's lesson.

Add at least four test cases in comments at the bottom.

Example:

```python
# Test cases:
# score = 3 -> Perfect round.
# score = 2 -> Good practice round.
# score = 0 -> Try the round again.
```

Then run the program with each case.

Testing several paths is part of writing decision code.

## Tiny Win

Today you practiced turning rules into code.

That is a real programming skill.

You did not just write conditions. You checked whether the conditions matched the rule.

That habit will help you more than any single syntax trick.

## Tomorrow

Tomorrow you will build a mini project:

```text
Quiz Game
```

You already have the pieces:

```text
input()
comparisons
if / elif / else
truthy and falsy checks
score counting
final messages
debugging with test cases
```

Tomorrow you will put those pieces together into one small program that asks questions, checks answers, keeps score, and prints a result.
