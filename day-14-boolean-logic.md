# Day 14: Boolean Logic

**Focus:** Combining yes-or-no answers with `and`, `or`, and `not`  
**You will practice:** Writing clear conditions, grouping comparisons, using boolean variables, and debugging logic mistakes  
**Estimated time:** 45-55 minutes

## Today's Goal

Today you will learn how to combine more than one condition.

You already know that comparisons produce boolean values:

```python
age = 18
password = "python"
score = 82

print(age >= 18)
print(password == "python")
print(score < 100)
```

You should see:

```text
True
True
True
```

Boolean logic lets you combine those yes-or-no answers with three words:

```text
and
or
not
```

By the end of this lesson, you should be able to:

* use `and` when two things must both be true
* use `or` when at least one thing must be true
* use `not` to reverse a boolean value
* combine comparisons inside an `if` statement
* use parentheses to make grouped logic clear
* split a confusing condition into smaller boolean variables

Today is not about writing clever conditions. It is about writing conditions that say what you actually mean.

Broken examples are labeled clearly. Study them first; run them only when you want to see the error or the wrong behavior.

## The Big Idea

A single comparison asks one question.

```python
age = 20

print(age >= 18)
```

You should see:

```text
True
```

Real programs often need to ask more than one question before making a choice.

```text
Is the user old enough, and do they have an ID?
Is the password correct, or does the user have a backup code?
Is the account not locked?
```

Python gives you boolean logic for this:

```python
age = 20
has_id = True
password = "open123"
backup_code = "0000"
is_locked = False

can_enter = age >= 18 and has_id
can_log_in = password == "open123" or backup_code == "8821"
account_is_available = not is_locked

print(can_enter)
print(can_log_in)
print(account_is_available)
```

You should see:

```text
True
True
True
```

Each final answer is still just one boolean value. That final `True` or `False` decides whether an `if` block runs.

## The Mental Model

Think of a condition as a small checklist.

`and` means every required item must pass.

```python
has_ticket = True
is_old_enough = False

print(has_ticket and is_old_enough)
```

You should see:

```text
False
```

The person has a ticket, but they are not old enough. With `and`, one failed item makes the whole condition false.

`or` means there is more than one way to pass.

```python
has_ticket = False
has_guest_pass = True

print(has_ticket or has_guest_pass)
```

You should see:

```text
True
```

The person does not have a normal ticket, but the guest pass is enough.

`not` flips the answer.

```python
is_locked = False

print(not is_locked)
```

You should see:

```text
True
```

The door is not locked, so `not is_locked` is true.

Here are the same rules in a compact form:

| Expression | Meaning | When it is true |
| --- | --- | --- |
| `a and b` | both must pass | `a` is true and `b` is true |
| `a or b` | one or both may pass | `a` is true, `b` is true, or both are true |
| `not a` | reverse the answer | `a` is false |

When a condition gets longer, parentheses help you show which question belongs together.

```python
age = 12
has_ticket = True
with_adult = True

can_watch = has_ticket and (age >= 13 or with_adult)

print(can_watch)
```

You should see:

```text
True
```

Read the condition in two parts:

```text
The person needs a ticket.
The person also needs to be at least 13 or with an adult.
```

The parentheses make the age-or-adult part clear.

## Try It Yourself

Create a file named:

```text
day-14/access_check.py
```

Code:

```python
age = int(input("How old are you? "))
ticket_answer = input("Do you have a ticket? yes/no ")

has_ticket = ticket_answer == "yes"

if age >= 13 and has_ticket:
    print("You can watch the movie.")
else:
    print("You cannot watch the movie.")
```

Run it a few times with different answers:

```text
12, yes
13, yes
15, no
20, yes
```

Now change the rule:

```text
The person can watch the movie if they have a ticket and either:

* they are at least 13
* they are with an adult
```

Add these lines after the ticket question:

```python
adult_answer = input("Are you with an adult? yes/no ")
with_adult = adult_answer == "yes"
```

Then update the condition:

```python
if has_ticket and (age >= 13 or with_adult):
    print("You can watch the movie.")
else:
    print("You cannot watch the movie.")
```

The ticket is outside the parentheses because it is always required.

If you wrote this instead:

```python
if (has_ticket and age >= 13) or with_adult:
    print("You can watch the movie.")
else:
    print("You cannot watch the movie.")
```

then someone with no ticket could enter just because they are with an adult. That might not be the rule you meant.

Small changes in grouping can change the meaning of a program.

## Common Mistake

### Mistake 1: Leaving out part of a comparison

This sounds natural in English, but it is not valid Python.

Broken code:

```python
age = 14

if age >= 13 and <= 19:
    print("Teenager")
```

Python needs a complete yes-or-no question on both sides of `and`.

Fixed code:

```python
age = 14

if age >= 13 and age <= 19:
    print("Teenager")
```

You should see:

```text
Teenager
```

### Mistake 2: Forgetting to repeat the comparison with `or`

This code runs, but the condition does not mean what it looks like it means.

Broken code:

```python
day = "Monday"

if day == "Saturday" or "Sunday":
    print("Weekend")
else:
    print("Weekday")
```

You might expect it to print `Weekday`, but it prints `Weekend`.

The problem is this part:

```python
or "Sunday"
```

That is a string, not a full comparison.

Fixed code:

```python
day = "Monday"

if day == "Saturday" or day == "Sunday":
    print("Weekend")
else:
    print("Weekday")
```

You should see:

```text
Weekday
```

For now, use this rule: each side of `and` or `or` should be a complete yes-or-no question.

## Debug It

Here is a program with a logic bug.

The rule is supposed to be:

```text
A person can enter if they have a ticket and they are either an adult or they have permission.
```

Broken code:

```python
age = 20
has_ticket = False
has_permission = False

if age >= 18 or has_permission and has_ticket:
    print("Entry allowed.")
else:
    print("Entry denied.")
```

You should see:

```text
Entry allowed.
```

That is wrong. The person is an adult, but they do not have a ticket.

The fix is to group the age-or-permission question and keep the ticket as a separate requirement.

Fixed code:

```python
age = 20
has_ticket = False
has_permission = False

if has_ticket and (age >= 18 or has_permission):
    print("Entry allowed.")
else:
    print("Entry denied.")
```

You should see:

```text
Entry denied.
```

When a condition is hard to read, break it into named pieces.

```python
age = 20
has_ticket = False
has_permission = False

is_adult = age >= 18
has_age_or_permission = is_adult or has_permission
can_enter = has_ticket and has_age_or_permission

print("is_adult:", is_adult)
print("has_age_or_permission:", has_age_or_permission)
print("can_enter:", can_enter)

if can_enter:
    print("Entry allowed.")
else:
    print("Entry denied.")
```

You should see:

```text
is_adult: True
has_age_or_permission: True
can_enter: False
Entry denied.
```

Printing the smaller boolean values helps you see which part of the logic is doing what.

## Read the Docs

Find Python's official documentation for boolean operations:

```text
https://docs.python.org/3/library/stdtypes.html#boolean-operations-and-or-not
```

Look for these forms:

```text
x and y
x or y
not x
```

For today, read them this way:

```text
x and y    both must pass
x or y     at least one must pass
not x      reverse the answer
```

The documentation may mention details about values that are not exactly `True` or `False`. You will study that later. Today, keep your practice focused on comparisons and boolean variables.

## Mini Challenge

Create a file named:

```text
day-14/door_checker.py
```

Write a simple door checker.

Ask the user four questions:

```text
What is your age?
Do you have a ticket? yes/no
Are you a VIP? yes/no
Are you banned? yes/no
```

Rules:

```text
A person can enter if they are not banned and either:

* they are a VIP
* they have a ticket and are at least 18
```

Start with this:

```python
age = int(input("What is your age? "))

ticket_answer = input("Do you have a ticket? yes/no ")
vip_answer = input("Are you a VIP? yes/no ")
banned_answer = input("Are you banned? yes/no ")

has_ticket = ticket_answer == "yes"
is_vip = vip_answer == "yes"
is_banned = banned_answer == "yes"
```

Create a boolean variable named `can_enter`, then print one of these messages:

```text
Entry allowed.
Entry denied.
```

One possible solution:

```python
age = int(input("What is your age? "))

ticket_answer = input("Do you have a ticket? yes/no ")
vip_answer = input("Are you a VIP? yes/no ")
banned_answer = input("Are you banned? yes/no ")

has_ticket = ticket_answer == "yes"
is_vip = vip_answer == "yes"
is_banned = banned_answer == "yes"

can_enter = not is_banned and (is_vip or (has_ticket and age >= 18))

if can_enter:
    print("Entry allowed.")
else:
    print("Entry denied.")
```

Test your program with these cases:

| Age | Ticket | VIP | Banned | Result |
| --- | --- | --- | --- | --- |
| 20 | yes | no | no | Entry allowed. |
| 16 | yes | no | no | Entry denied. |
| 16 | no | yes | no | Entry allowed. |
| 30 | yes | yes | yes | Entry denied. |

If your program gives a different answer, print `has_ticket`, `is_vip`, `is_banned`, and `can_enter`.

## Real-World Use

Boolean logic appears anywhere a program has rules.

Examples:

* allow login if the password is correct and the account is not locked
* give free shipping if the cart total is high enough or the user has a coupon
* show a warning if the battery is low and the device is not charging
* end a game if the player has no lives left or the timer reaches zero
* send a reminder if a task is due today and it is not complete

Most useful programs are full of small decisions. Boolean logic is how those decisions become precise.

## Recap

Today you learned:

* `and` means both sides must be true
* `or` means at least one side must be true
* `not` reverses a boolean value
* comparisons can be combined into larger conditions
* parentheses make grouped logic easier to read
* named boolean variables can make long conditions clearer
* many bugs come from conditions that do not match the rule you intended

Main idea:

```text
Make each part of a condition a clear yes-or-no question.
```

## Lesson Checklist

Before moving on, check that you can:

* explain what `and`, `or`, and `not` do
* predict the result of simple boolean expressions
* combine comparisons inside an `if` statement
* use parentheses to group a condition
* explain why `has_ticket and (age >= 18 or with_adult)` is different from `(has_ticket and age >= 18) or with_adult`
* fix a condition that forgets to repeat the variable
* split a long condition into smaller boolean variables

## Exercises

### Exercise 1

Predict the output before running this code:

```python
age = 19
has_id = True

print(age >= 18 and has_id)
print(age < 18 or has_id)
print(not has_id)
```

Then run it and check your prediction.

### Exercise 2

Write a condition that prints `"Valid score"` only when `score` is between `0` and `100`, including both ends.

Starter:

```python
score = 87

if ____________________:
    print("Valid score")
else:
    print("Invalid score")
```

### Exercise 3

Fix this code.

Broken code:

```python
day = "Saturday"

if day == "Saturday" or "Sunday":
    print("Weekend")
else:
    print("Weekday")
```

### Exercise 4

Write a program that checks whether a person can vote.

Rules:

```text
The person can vote if they are at least 18 and they are registered.
```

Use these variables:

```python
age = 21
is_registered = True
```

### Exercise 5

Write a program that checks whether a store should give a discount.

Rules:

```text
Give a discount if the customer is a member or the cart total is at least 100.
```

Use these variables:

```python
is_member = False
cart_total = 120
```

### Exercise 6

Make this condition easier to read by creating smaller boolean variables:

```python
if age >= 18 and has_ticket and not is_banned and (is_member or has_coupon):
    print("Special entry allowed.")
```

Possible names:

```text
is_adult
can_use_discount
can_use_special_entry
```

### Exercise 7

Create a login checker.

Rules:

```text
Login succeeds if the username is correct, the password is correct, and the account is not locked.
```

Use:

```python
username = "student"
password = "python"
is_locked = False
```

### Exercise 8

Write your own truth table for this expression:

```python
a and not b
```

Try all four combinations:

```text
a is True, b is True
a is True, b is False
a is False, b is True
a is False, b is False
```

Then check your answers in Python.

## Tiny Win

You can now write conditions with more than one requirement.

That is a real step forward. A program no longer has to ask only:

```text
Is this one thing true?
```

It can ask:

```text
Are all the required things true?
Is at least one allowed path true?
Is this problem not present?
```

That is the beginning of real program logic.

## Tomorrow

Tomorrow you will learn about nested conditions.

That means putting one decision inside another decision. Boolean logic helps you combine questions in one condition. Nested conditions help you handle decisions that happen in stages.
