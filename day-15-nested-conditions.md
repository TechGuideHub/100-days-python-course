# Day 15: Nested Conditions

**Focus:** Putting one decision inside another decision  
**You will practice:** Writing nested `if` statements, reading indentation, matching `else` blocks, and debugging staged decisions  
**Estimated time:** 40-50 minutes

## Today's Goal

Today you will learn how to put one `if` statement inside another `if` statement.

By the end of this lesson, you should be able to:

- write an `if` statement inside another `if` statement
- explain when the inner condition runs
- use indentation to show which code belongs to which decision
- match an `else` with the correct `if`
- use nesting when a decision happens in stages
- notice when nested code is getting hard to read
- debug common nested condition mistakes

You are not trying to make complicated code today.

You are learning how Python handles decisions that happen one step at a time.

## The Big Idea

A nested condition is an `if` statement inside another `if` statement.

Example:

```python
has_account = True
password_correct = True

if has_account:
    if password_correct:
        print("Welcome back.")
```

You should see:

```text
Welcome back.
```

Python checks `has_account` first.

Because it is `True`, Python goes inside the first `if` block. Then it checks `password_correct`.

If the outer condition is false, Python never reaches the inner condition.

Example:

```python
has_account = False
password_correct = True

if has_account:
    if password_correct:
        print("Welcome back.")
```

This program prints nothing.

The password check is inside the account check, so it is skipped when `has_account` is `False`.

Main idea:

```text
Python only reaches the inside decision after the outside decision lets it in.
```

## The Mental Model

Think of nested conditions like rooms inside rooms.

The first `if` is the outside door. The second `if` is a door inside that room.

```text
Outside door: Do you have an account?
Inside door: Is your password correct?
```

Python cannot reach the inside door unless the outside door opens first.

Example:

```python
has_account = True
password_correct = False

if has_account:
    print("Account found.")

    if password_correct:
        print("Welcome back.")
    else:
        print("Password incorrect.")
else:
    print("No account found.")
```

You should see:

```text
Account found.
Password incorrect.
```

There are two indentation levels here.

This line is inside the outer `if`:

```python
    print("Account found.")
```

These lines are farther inside:

```python
    if password_correct:
        print("Welcome back.")
```

The `if password_correct:` line belongs to the account check.

The `print("Welcome back.")` line belongs to the password check.

Indentation tells Python how deep inside the decision each line is.

## Try It Yourself

Create a file named:

```text
day-15/nested_practice.py
```

Code:

```python
has_key = True
door_is_locked = True

if has_key:
    print("You have the key.")

    if door_is_locked:
        print("You unlock the door.")
    else:
        print("The door is already open.")
else:
    print("You need to find the key first.")
```

Run the file from your course folder:

```bash
python day-15/nested_practice.py
```

If your computer uses `py`, use:

```bash
py day-15/nested_practice.py
```

If your computer uses `python3`, use:

```bash
python3 day-15/nested_practice.py
```

You should see:

```text
You have the key.
You unlock the door.
```

Now change one value:

```python
door_is_locked = False
```

Run the program again.

You should see:

```text
You have the key.
The door is already open.
```

Now change another value:

```python
has_key = False
```

Run the program again.

You should see:

```text
You need to find the key first.
```

Notice what did not happen.

Python did not print anything about the door. When `has_key` is `False`, the inner door check is skipped.

## Common Mistake

### Mistake 1: Forgetting that the inner `if` depends on the outer `if`

Look at this code:

```python
is_member = False
cart_total = 150

if is_member:
    if cart_total >= 100:
        print("You get free shipping.")
```

This program prints nothing.

The cart total is high enough, but the customer is not a member. Because `is_member` is `False`, Python never reaches the cart total check.

If the rule is this:

```text
Members with carts of at least 100 get free shipping.
```

then the code is correct.

If the rule is this:

```text
Anyone with a cart of at least 100 gets free shipping.
```

then the nesting is wrong.

You could write:

```python
cart_total = 150

if cart_total >= 100:
    print("You get free shipping.")
```

Before writing nested code, ask:

```text
Does the inner question really depend on the outer question?
```

### Mistake 2: Putting `else` at the wrong indentation level

Broken code:

```python
has_account = True
password_correct = False

if has_account:
    if password_correct:
        print("Welcome back.")
else:
    print("Wrong password.")
```

This code runs, but it does not say what the writer probably meant.

The `else` belongs to the outer `if`, not the inner `if`. It means:

```text
If has_account is false, print "Wrong password."
```

Since `has_account` is `True`, the outer `else` is skipped. The program prints nothing.

Fixed code:

```python
has_account = True
password_correct = False

if has_account:
    if password_correct:
        print("Welcome back.")
    else:
        print("Wrong password.")
else:
    print("No account found.")
```

You should see:

```text
Wrong password.
```

With nested conditions, indentation decides which `if` an `else` belongs to.

### Mistake 3: Nesting too deeply

This code works, but it takes effort to read:

```python
has_account = True
password_correct = True
is_locked = False
has_two_factor_code = True

if has_account:
    if password_correct:
        if not is_locked:
            if has_two_factor_code:
                print("Login successful.")
```

You should see:

```text
Login successful.
```

Four levels of indentation is a warning sign.

It does not mean the code is always wrong. It means you should pause and ask whether there is a clearer way to write it.

For today, just notice the shape:

```text
inside
    inside
        inside
            inside
```

The deeper code goes, the more carefully you need to read it.

## Debug It

Here is a broken program.

Broken code:

```python
has_ticket = True
age = 16

if has_ticket:
print("Ticket found.")
    if age >= 18:
        print("You can enter.")
    else:
        print("You are not old enough.")
else:
    print("You need a ticket.")
```

The problem is this line:

```python
print("Ticket found.")
```

It belongs inside the `if has_ticket:` block, so it needs to be indented.

Fixed code:

```python
has_ticket = True
age = 16

if has_ticket:
    print("Ticket found.")

    if age >= 18:
        print("You can enter.")
    else:
        print("You are not old enough.")
else:
    print("You need a ticket.")
```

You should see:

```text
Ticket found.
You are not old enough.
```

Here is another program with a logic bug.

Broken code:

```python
has_coupon = False
cart_total = 120

if has_coupon:
    if cart_total >= 100:
        print("Discount applied.")
else:
    print("Cart total is too low.")
```

You should see:

```text
Cart total is too low.
```

That message is misleading. The cart total is not too low. The real reason is that `has_coupon` is `False`.

The `else` belongs to the outer `if`, so the message should match the outer condition.

Fixed code:

```python
has_coupon = False
cart_total = 120

if has_coupon:
    if cart_total >= 100:
        print("Discount applied.")
    else:
        print("Cart total is too low.")
else:
    print("You need a coupon.")
```

You should see:

```text
You need a coupon.
```

When debugging nested conditions, ask:

- Which `if` does this `else` belong to?
- Is the inner condition being reached at all?
- Does each message match the condition that failed?
- Would printing the values help?

Small print statements can show which path Python is taking:

```python
print("has_coupon:", has_coupon)
print("cart_total:", cart_total)
```

## Read the Docs

Find Python's official tutorial section about `if` statements:

```text
https://docs.python.org/3/tutorial/controlflow.html#if-statements
```

You may see `if`, `elif`, and `else` together.

For today, look for this basic shape:

```text
if condition:
    statement
```

Then remember:

```text
The statement inside an if can be another if statement.
```

Python does not need a special keyword for nested conditions. It uses the same `if` statement and the indentation you already know.

## Mini Challenge

Create a file named:

```text
day-15/package_pickup.py
```

Write a program that checks whether someone can pick up a package.

Use these variables:

```python
has_pickup_code = True
name_matches_order = False
package_is_ready = True
```

Rules:

```text
First, the person must have the pickup code.
If they have the pickup code, check whether their name matches the order.
If the name matches, check whether the package is ready.
```

Print helpful messages for each result:

```text
Pickup code accepted.
Name confirmed.
Your package is ready.
Your package is not ready yet.
The name does not match the order.
You need the pickup code.
```

One possible solution:

```python
has_pickup_code = True
name_matches_order = False
package_is_ready = True

if has_pickup_code:
    print("Pickup code accepted.")

    if name_matches_order:
        print("Name confirmed.")

        if package_is_ready:
            print("Your package is ready.")
        else:
            print("Your package is not ready yet.")
    else:
        print("The name does not match the order.")
else:
    print("You need the pickup code.")
```

With the starter values, you should see:

```text
Pickup code accepted.
The name does not match the order.
```

Then test these cases:

| Pickup code | Name matches | Package ready | Final message |
| --- | --- | --- | --- |
| `True` | `True` | `True` | `Your package is ready.` |
| `True` | `True` | `False` | `Your package is not ready yet.` |
| `True` | `False` | `True` | `The name does not match the order.` |
| `False` | `True` | `True` | `You need the pickup code.` |

Testing different cases is how you make sure each path works.

## Real-World Use

Nested conditions appear when a program has to check one thing before another thing.

Examples:

- if a user is logged in, check whether they have permission to view a page
- if a payment method exists, check whether the payment succeeds
- if a game character has a key, check whether the door is locked
- if a file exists, check whether it has the data the program needs
- if a student submitted an assignment, check whether it was submitted on time
- if a customer is in the delivery area, check whether a delivery slot is available

In each case, the second question only makes sense after the first question passes.

That is the best reason to nest conditions.

## Recap

Today you learned:

- a nested condition is an `if` statement inside another `if` statement
- the outer condition is checked first
- the inner condition only runs if Python reaches it
- each indentation level means the code is deeper inside a decision
- an `else` belongs to the matching `if` at the same indentation level
- nesting is useful for staged decisions
- too much nesting can make code hard to read
- debugging nested conditions often means checking which path Python actually took

Main idea:

```text
Nested conditions let a program ask the next question only after the first question passes.
```

## Lesson Checklist

Before moving on, check that you can:

- write an `if` statement inside another `if` statement
- explain when the inner `if` runs
- identify the outer condition and the inner condition
- use indentation to show which code belongs inside each block
- match an `else` with the correct `if`
- explain why a nested condition might print nothing
- fix a nested indentation problem
- recognize when nesting is making code harder to read

## Exercises

### Exercise 1

Predict the output before running this code:

```python
has_account = True
password_correct = True

if has_account:
    if password_correct:
        print("Welcome.")
    else:
        print("Wrong password.")
else:
    print("No account found.")
```

Then run it and check your prediction.

### Exercise 2

Change the values and predict the output again:

```python
has_account = True
password_correct = False
```

Then try:

```python
has_account = False
password_correct = True
```

What happens to the inner `if` when `has_account` is `False`?

### Exercise 3

Write a program with these variables:

```python
has_ticket = True
age = 17
```

Rules:

```text
If the person has a ticket, check their age.
If they are at least 18, print "Entry allowed."
Otherwise, print "You are not old enough."
If they do not have a ticket, print "You need a ticket."
```

### Exercise 4

Fix the indentation.

Broken code:

```python
is_raining = True
has_umbrella = False

if is_raining:
print("It is raining.")
    if has_umbrella:
        print("You can stay dry.")
    else:
        print("You might get wet.")
else:
    print("No umbrella needed.")
```

### Exercise 5

Which `if` does the `else` belong to?

```python
has_key = True
door_is_locked = False

if has_key:
    if door_is_locked:
        print("Unlocking door.")
    else:
        print("Door is already open.")
else:
    print("Find the key first.")
```

Write your answer in plain English. Then run the code.

### Exercise 6

Write a nested condition for a homework checker.

Use:

```python
submitted = True
submitted_on_time = False
```

Rules:

```text
If the homework was submitted, check whether it was on time.
If it was on time, print "Submitted on time."
Otherwise, print "Submitted late."
If it was not submitted, print "Missing homework."
```

### Exercise 7

Rewrite this nested condition using `and`:

```python
has_badge = True
is_employee = True

if has_badge:
    if is_employee:
        print("Access granted.")
```

Your rewritten program should still print the same message only when both values are true.

### Exercise 8

Rewrite this `and` condition as nested `if` statements:

```python
has_username = True
has_password = True

if has_username and has_password:
    print("Login form complete.")
```

### Exercise 9

Find the misleading message in this program and fix it:

```python
has_invitation = False
is_on_guest_list = True

if has_invitation:
    if is_on_guest_list:
        print("Welcome to the event.")
else:
    print("You are not on the guest list.")
```

The message should explain the condition that actually failed.

### Exercise 10

Write a small nested program about a topic you choose.

Ideas:

```text
a game door
a school assignment
a bank withdrawal
a movie ticket
a library checkout
a phone battery warning
```

Your program should have:

- at least two boolean variables
- one `if` statement inside another `if` statement
- at least one `else`
- messages that explain which path happened

After writing it, test at least three different sets of values.

## Tiny Win

Today, your programs learned to make decisions in stages.

They can now say:

```text
First this must be true.
Then, inside that situation, check the next thing.
```

That is how many real rules are built.

## Tomorrow

Tomorrow you will learn how to make conditions cleaner.

Nested conditions are useful, but they can become hard to read when they grow too deep.

Next, you will practice turning tangled decision code into clearer code with better names and simpler shapes.
