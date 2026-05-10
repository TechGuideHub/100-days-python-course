# Day 18: Common Logic Bugs

**Focus:** Finding wrong decisions in code that still runs  
**You will practice:** checking comparisons, choosing `and` or `or`, testing boundary values, and debugging conditions with named booleans  
**Estimated time:** 45-55 minutes

## Today's Goal

Today you will learn how to find and fix logic bugs.

A syntax error stops a program before it runs.

Broken code:

```python
if age >= 18
    print("Adult")
```

Python can see that the colon is missing.

A logic bug is different. The program runs, but it makes the wrong decision.

Example:

```python
age = 16

if age >= 13:
    print("Adult")
else:
    print("Not adult")
```

You should see:

```text
Adult
```

Python did exactly what the code asked. The problem is that the code did not ask the question the programmer meant.

By the end of this lesson, you should be able to:

* recognize common logic bugs in conditions
* fix reversed comparisons
* choose between `and` and `or` more carefully
* notice when an `else` path is missing
* spot indentation that changes a program's meaning
* check that you are using the right variable
* avoid truthy and falsy surprises
* test a condition with more than one example
* debug calmly by breaking a condition into smaller questions

Today is not about never making mistakes. It is about learning what mistakes usually look like.

Broken examples are part of the lesson. Read the rule first, then study why the code does not match it.

## The Big Idea

Many beginner logic bugs are small mismatches between three things:

```text
What the rule says
What the code asks
What your test examples prove
```

Suppose the rule is:

```text
A person can enter if they are at least 18.
```

This code runs:

```python
age = 17

if age <= 18:
    print("Entry allowed.")
else:
    print("Entry denied.")
```

For `age = 17`, the program allows entry.

The bug is not that Python is confused. Python reads the condition as:

```text
Is age less than or equal to 18?
```

For `17`, the answer is `True`.

The comparison is backwards. The rule needs this condition:

```python
age = 17

if age >= 18:
    print("Entry allowed.")
else:
    print("Entry denied.")
```

Good debugging often starts with one slow question:

```text
What is this line actually asking?
```

Not what you hoped it was asking. Not what the variable name reminds you of. What it literally asks Python to check.

## The Mental Model

Think of a condition as a gate with a label on it.

```python
temperature = -3

if temperature < 0:
    print("Freezing")
```

The label on the gate is:

```text
temperature < 0
```

Python does not know that you meant "cold," "dangerous," or "winter weather." It only checks the exact label.

A small change can make the gate open at the wrong time.

```python
temperature = 12

if temperature > 0:
    print("Freezing")
```

That line is legal Python. It is just the wrong question.

When a condition feels confusing, separate the rule from the code.

Example:

```text
Rule:
Show a warning if the battery is below 20 and the phone is not charging.

Python condition:
battery < 20 and not is_charging
```

If the English rule and the Python condition do not match, you have found the bug.

Named booleans can make that match easier to see.

```python
battery = 15
is_charging = False

is_low_battery = battery < 20
should_warn = is_low_battery and not is_charging

print("Low battery?", is_low_battery)
print("Should warn?", should_warn)
```

You should see:

```text
Low battery? True
Should warn? True
```

The extra names slow the code down in a good way. They let you inspect each part of the decision.

## Try It Yourself

Create a file named `day-18/logic_bug_practice.py`.

Code:

```python
score = 48

if score >= 50:
    print("Pass")
else:
    print("Try again")
```

Run it.

You should see:

```text
Try again
```

Now test these values one at a time:

```python
score = 50
score = 51
score = 49
score = 0
score = 100
```

Before each run, say what you expect. Then run the program and compare.

Now break the condition on purpose:

```python
if score > 50:
```

Run the same test values again.

The program now says `50` is not a passing score. That is a logic bug.

The bug is small, but the meaning changed:

```text
score >= 50 means 50 passes.
score > 50 means 50 does not pass.
```

This is why boundary values matter.

A boundary value is a value right on the edge of a rule. For this rule, `50` is the boundary.

Good tests include values below the boundary, at the boundary, and above the boundary.

```text
49
50
51
```

Those three examples teach you more than testing only `75`.

## Common Mistake

Logic bugs often appear in familiar shapes. Once you know the shapes, you can check for them on purpose.

### Mistake 1: Reversing a comparison

Rule:

```text
A person can vote if they are at least 18.
```

Broken code:

```python
age = 16

if age <= 18:
    print("Can vote")
else:
    print("Cannot vote")
```

The comparison is reversed. `age <= 18` includes `16`, so the wrong people pass the check.

Fixed code:

```python
age = 16

if age >= 18:
    print("Can vote")
else:
    print("Cannot vote")
```

Test values that should pass and fail:

```text
16 should fail.
18 should pass.
21 should pass.
```

### Mistake 2: Using `and` when the rule needs `or`

Rule:

```text
A user can sign in with a correct password or a correct backup code.
```

Broken code:

```python
password_correct = False
backup_code_correct = True

if password_correct and backup_code_correct:
    print("Signed in.")
else:
    print("Try again.")
```

You should see:

```text
Try again.
```

The backup code was correct, but `and` requires both sides to be true.

Fixed code:

```python
password_correct = False
backup_code_correct = True

if password_correct or backup_code_correct:
    print("Signed in.")
else:
    print("Try again.")
```

Use `or` when there are multiple ways to pass.

### Mistake 3: Using `or` when the rule needs `and`

Rule:

```text
A person can enter a teen event only if their age is from 13 through 19.
```

Broken code:

```python
age = 8

if age >= 13 or age <= 19:
    print("Teen ticket allowed.")
else:
    print("Teen ticket denied.")
```

You should see:

```text
Teen ticket allowed.
```

For `age = 8`, the second comparison is true:

```text
age <= 19
```

With `or`, one true side is enough.

Fixed code:

```python
age = 8

if age >= 13 and age <= 19:
    print("Teen ticket allowed.")
else:
    print("Teen ticket denied.")
```

For ranges, a chained comparison is often cleaner:

```python
age = 8

if 13 <= age <= 19:
    print("Teen ticket allowed.")
else:
    print("Teen ticket denied.")
```

### Mistake 4: Forgetting what should happen when the condition is false

This program works only when the day is warm.

```python
temperature = 18

if temperature >= 25:
    print("Warm day")
```

For `temperature = 18`, nothing prints.

That might be fine if silence is useful. Often, the user needs a result either way.

Fixed code:

```python
temperature = 18

if temperature >= 25:
    print("Warm day")
else:
    print("Not warm today")
```

When debugging, ask:

```text
What should happen when the condition is false?
```

If the answer is not "nothing," you probably need an `else` or an `elif`.

### Mistake 5: Indenting a line into the wrong place

Indentation decides what belongs inside the condition.

```python
is_member = False

if is_member:
    print("Member discount applied.")
print("Final price updated.")
```

You should see:

```text
Final price updated.
```

The second `print()` is not indented, so it always runs.

If the final price should update only for members, the indentation must show that.

```python
is_member = False

if is_member:
    print("Member discount applied.")
    print("Final price updated.")
```

Now both lines belong to the `if` block.

When in doubt, point to each line and ask:

```text
Is this line supposed to depend on the condition?
```

If yes, it should be indented under that condition.

### Mistake 6: Checking the wrong variable

This bug can hide in code that looks reasonable at a glance.

Broken code:

```python
saved_password = "python123"
typed_password = "wrongpass"

if saved_password == saved_password:
    print("Welcome.")
else:
    print("Try again.")
```

You should see:

```text
Welcome.
```

The program compares `saved_password` to itself, so the condition is always true.

Fixed code:

```python
saved_password = "python123"
typed_password = "wrongpass"

if typed_password == saved_password:
    print("Welcome.")
else:
    print("Try again.")
```

This kind of bug often happens when two variable names look similar. Slow reading helps. So does printing both values.

```python
print("typed_password:", typed_password)
print("saved_password:", saved_password)
```

### Mistake 7: Getting surprised by truthy and falsy values

Python can use non-boolean values in conditions.

These values act like `False`:

```python
False
None
0
""
[]
```

Many other values act like `True`:

```python
1
"hello"
"False"
"0"
[1, 2, 3]
```

That can create surprises.

Example:

```python
is_admin = "False"

if is_admin:
    print("Show admin tools.")
else:
    print("Hide admin tools.")
```

You should see:

```text
Show admin tools.
```

The string `"False"` is not the boolean value `False`. It is text. Because it is a non-empty string, Python treats it as true.

Fixed code:

```python
is_admin = False

if is_admin:
    print("Show admin tools.")
else:
    print("Hide admin tools.")
```

Truthy and falsy checks are useful, but they should match the kind of value you are checking.

### Mistake 8: Testing only one easy example

This program looks fine if you test only `85`.

```python
score = 85

if score > 50:
    print("Pass")
else:
    print("Try again")
```

For `85`, it works.

But if the rule is:

```text
50 or more is passing.
```

then `50` should pass too.

The code gets `50` wrong because it uses `>` instead of `>=`.

Good tests include different kinds of examples:

```text
A normal passing value: 85
A normal failing value: 42
The boundary value: 50
Just below the boundary: 49
Just above the boundary: 51
```

Testing the edge of the rule often reveals the bug.

## Debug It

Here is a program that looks correct for one test case but fails for another.

Rule:

```text
A person can get a student discount if they are a student and their age is 25 or younger.
```

Code:

```python
is_student = False
age = 30

if is_student or age <= 25:
    print("Student discount applied.")
else:
    print("No student discount.")
```

For these exact values, the output looks right:

```text
No student discount.
```

Now test another case:

```python
is_student = False
age = 20

if is_student or age <= 25:
    print("Student discount applied.")
else:
    print("No student discount.")
```

You should see:

```text
Student discount applied.
```

The person is not a student, so that result is wrong.

The condition uses `or`, but the rule requires both facts to be true.

Fixed code:

```python
is_student = False
age = 20

if is_student and age <= 25:
    print("Student discount applied.")
else:
    print("No student discount.")
```

When a condition is confusing, use this debugging pattern.

Step 1: Write the rule in plain English.

```text
A person gets a student discount if they are a student and they are 25 or younger.
```

Step 2: Split the condition into named pieces.

```python
is_student = False
age = 20

is_young_enough = age <= 25
gets_discount = is_student and is_young_enough
```

Step 3: Print the pieces.

```python
print("is_student:", is_student)
print("is_young_enough:", is_young_enough)
print("gets_discount:", gets_discount)
```

You should see:

```text
is_student: False
is_young_enough: True
gets_discount: False
```

Step 4: Test more than one case.

| `is_student` | `age` | Expected result |
| --- | ---: | --- |
| `True` | `20` | discount |
| `True` | `26` | no discount |
| `False` | `20` | no discount |
| `False` | `30` | no discount |

The third row catches the bug.

Debugging is not guessing harder. It is making the program show you what it is doing.

## Read the Docs

Python's official documentation has a section called "Truth Value Testing."

```text
https://docs.python.org/3/library/stdtypes.html#truth-value-testing
```

You do not need every detail today. Look for the values that Python considers false, including:

```python
False
None
0
""
[]
{}
```

Then try this in your own file:

```python
print(bool(""))
print(bool("False"))
print(bool(0))
print(bool("0"))
print(bool([]))
print(bool([0]))
```

You should see:

```text
False
True
False
True
False
True
```

`bool()` shows how Python treats a value in a condition. That is useful when a condition behaves differently than you expected.

## Mini Challenge

Create a file named `day-18/movie_ticket_checker.py`.

Rules:

```text
A customer can buy a student movie ticket if:

They are a student
and
they are at least 13 years old
and
they are not banned from the theater.
```

Start with these values:

```python
is_student = True
age = 12
is_banned = False
```

Your program should:

* create at least two clearly named boolean variables
* use one final `if` statement
* print `"Student ticket allowed."` or `"Student ticket denied."`
* test at least four different sets of values

Suggested tests:

| `is_student` | `age` | `is_banned` | Expected result |
| --- | ---: | --- | --- |
| `True` | `13` | `False` | allowed |
| `True` | `12` | `False` | denied |
| `False` | `16` | `False` | denied |
| `True` | `20` | `True` | denied |

After each test, ask:

```text
Did the result match the rule?
```

If not, print the smaller boolean values and inspect them one at a time.

## Real-World Use

Logic bugs matter because many programs make decisions.

Small conditions can decide whether:

* a form is complete
* a user can sign in
* a discount applies
* a warning appears
* a message is sent
* a game character can move
* a file should be saved

The code may be only one line:

```python
if has_permission and not account_locked:
```

But that line can control an important path.

Careful programmers do not only ask:

```text
Does the program run?
```

They also ask:

```text
Does the program choose the right path for different examples?
```

That second question is where logic gets stronger.

## Recap

Today you learned that logic bugs happen when a program runs but makes the wrong decision.

You saw common causes:

* reversed comparisons like `<=` and `>=`
* choosing `and` when the rule needs `or`
* choosing `or` when the rule needs `and`
* forgetting what should happen when a condition is false
* indenting a line into the wrong block
* checking the wrong variable
* getting surprised by truthy and falsy values
* testing only one easy example

You also practiced a useful debugging pattern:

```text
Write the rule in English.
Split the condition into smaller booleans.
Print the smaller booleans.
Test boundary values and other important cases.
Fix one thing at a time.
```

Main idea:

```text
A program can run correctly as Python code and still make the wrong choice.
```

## Lesson Checklist

Before moving on, check that you can:

* explain the difference between a syntax error and a logic bug
* read a condition as a plain-English question
* fix a reversed comparison
* choose `and` when all parts of a rule must be true
* choose `or` when any one part of a rule is enough
* use an `else` when the false path needs a response
* identify which lines belong inside an `if` block
* spot a condition that compares the wrong variable
* explain why `"False"` is truthy
* test below, at, and above a boundary value

## Exercises

### Exercise 1

Fix the comparison.

Rule:

```text
A person can enter if they are 18 or older.
```

Broken code:

```python
age = 17

if age <= 18:
    print("Entry allowed.")
else:
    print("Entry denied.")
```

Test your fixed code with:

```text
17
18
19
```

### Exercise 2

Fix the `and` or `or` bug.

Rule:

```text
A user can reset their password if they know their email or they know their phone number.
```

Broken code:

```python
knows_email = True
knows_phone = False

if knows_email and knows_phone:
    print("Password reset allowed.")
else:
    print("Password reset denied.")
```

### Exercise 3

Fix the range check.

Rule:

```text
A score is valid if it is from 0 through 100.
```

Broken code:

```python
score = 150

if score >= 0 or score <= 100:
    print("Valid score")
else:
    print("Invalid score")
```

Write the fixed version using `and`. Then write another fixed version using a chained comparison.

### Exercise 4

Add a useful `else`.

Current code:

```python
has_messages = False

if has_messages:
    print("You have new messages.")
```

Update it so the program also prints a message when there are no new messages.

### Exercise 5

Fix the indentation.

Rule:

```text
Both lines should print only if the user is logged in.
```

Broken code:

```python
is_logged_in = False

if is_logged_in:
    print("Loading dashboard.")
print("Showing account details.")
```

### Exercise 6

Find the wrong variable.

Broken code:

```python
correct_pin = "1234"
typed_pin = "9999"

if correct_pin == correct_pin:
    print("Unlocked.")
else:
    print("Locked.")
```

Fix it so the typed PIN is checked correctly.

### Exercise 7

Explain the truthy and falsy surprise.

What does this program print?

```python
is_member = "False"

if is_member:
    print("Member price")
else:
    print("Regular price")
```

Why?

Then fix the program by storing a real boolean value.

### Exercise 8

Test with more examples.

Rule:

```text
A package gets free shipping if the total is at least 50.
```

Code:

```python
total = 50

if total > 50:
    print("Free shipping")
else:
    print("Shipping added")
```

Find the bug. Then test with:

```text
49
50
51
```

### Exercise 9

Debug this program using named booleans.

Rule:

```text
Show a low battery warning if the battery is below 20 and the device is not charging.
```

Broken code:

```python
battery = 80
is_charging = False

if battery < 20 or not is_charging:
    print("Low battery warning")
else:
    print("Battery okay")
```

Create these boolean variables:

```python
is_low_battery
should_warn
```

Print both values before the final `if`. Then fix the condition.

### Exercise 10

Write your own small logic checker.

Choose one topic:

```text
a homework deadline
a game door
a library checkout
a snack machine
a quiz score
a concert ticket
```

Your program should have:

* at least three starting variables
* at least two named boolean variables
* one final `if` / `else`
* at least four test cases written in comments or a small table

After you write it, deliberately break one comparison or one `and` / `or`. Run your tests again and find the bug.

## Tiny Win

You can now look at a wrong decision without panicking.

You have a method:

```text
Slow down.
Read the exact condition.
Print the smaller pieces.
Test the edge cases.
```

That is real debugging.

## Tomorrow

Tomorrow is a practice day for decision problems.

You will use comparisons, `if`, `elif`, `else`, boolean logic, truthy and falsy values, and the debugging habits from today.

The goal will not be to learn a new symbol. The goal will be to solve small problems carefully and check that your programs make the right decisions.
