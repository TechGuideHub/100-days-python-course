# Day 17: Truthy and Falsy Values

**Focus:** How Python treats values in conditions  
**You will practice:** Checking strings, numbers, and simple collections, using `bool()`, and choosing clear comparisons  
**Estimated time:** 40-50 minutes

## Today's Goal

Today you will learn how Python decides whether a value counts as true or false in a condition.

You have already seen conditions that use booleans:

```python
is_logged_in = True

if is_logged_in:
    print("Welcome back.")
```

You should see:

```text
Welcome back.
```

Python can also test other kinds of values:

```python
name = ""

if name:
    print("Name entered.")
else:
    print("Name missing.")
```

You should see:

```text
Name missing.
```

That may look strange at first. `name` is a string, not a boolean.

By the end of this lesson, you should be able to:

- explain what truthy and falsy mean
- predict how Python treats empty and non-empty strings
- understand why `0` is falsy and non-zero numbers are truthy
- recognize that empty collections are falsy
- use `bool()` to inspect a value
- use truthiness when checking whether something is present
- use explicit comparisons when the rule needs an exact check
- debug mistakes caused by hidden truthy or falsy values

This lesson is not about writing clever shortcut code. It is about understanding a Python habit you will see often.

Broken examples are labeled clearly. Study them first; run them only when you want to see the problem.

## The Big Idea

Python does not only test `True` and `False`.

When a value appears in a condition, Python asks:

```text
Should this value count as true or false here?
```

Values that count as false are called **falsy**.

Common falsy values include:

```python
False
None
0
0.0
""
[]
{}
()
```

Do not worry about memorizing every item today. Start with these:

```text
An empty string is falsy.
Zero is falsy.
An empty collection is falsy.
```

Most other values are **truthy**.

Examples:

```python
True
1
-3
"hello"
"0"
"False"
[1, 2, 3]
```

The string `"0"` is truthy because it has one character inside it. Python is not asking whether the string means the number zero. It is asking whether the string is empty.

You can check values with `bool()`:

```python
print(bool(""))
print(bool("hello"))
print(bool(0))
print(bool(5))
print(bool("0"))
```

You should see:

```text
False
True
False
True
True
```

## The Mental Model

For beginner code, think of truthiness as a quick presence check.

```text
Empty often means false.
Something present often means true.
```

An empty string has no characters:

```python
name = ""
```

So Python treats it as falsy.

A non-empty string has at least one character:

```python
name = "Maya"
```

So Python treats it as truthy.

This is why you will often see code like this:

```python
if name:
    print("Name entered.")
```

Read it as:

```text
If name has something in it...
```

The same idea works for simple collection checks:

```python
tasks = []

if tasks:
    print("You have tasks.")
else:
    print("No tasks yet.")
```

You should see:

```text
No tasks yet.
```

But truthiness is not the same as equality to `True`.

```python
print(bool("hello"))
print("hello" == True)
```

You should see:

```text
True
False
```

The string `"hello"` is truthy, but it is not the boolean value `True`.

Main habit:

> Use truthiness for presence. Use comparisons for specific rules.

This is clear:

```python
if name:
    print("Name entered.")
```

This is also clear:

```python
if age >= 18:
    print("Adult")
```

This is not a good adult check:

```python
if age:
    print("Adult")
```

That only checks whether `age` is not zero.

## Try It Yourself

Create a file named:

```text
day-17/truthy_checks.py
```

Code:

```python
name = input("Name: ").strip()

if name:
    print("Hello,", name)
else:
    print("No name entered.")
```

Run it three times.

Try this:

```text
Mina
```

Then run it again and press Enter without typing anything.

Then run it a third time, type a few spaces, and press Enter.

Because the program uses `.strip()`, spaces-only input is treated like missing input.

Now add an age check:

```python
age_text = input("Age: ").strip()

if age_text:
    age = int(age_text)
    print("Next year you will be", age + 1)
else:
    print("No age entered.")
```

Try these inputs:

```text
12
0
```

When the user types `0`, `age_text` is:

```python
"0"
```

That is a non-empty string, so it is truthy. The program converts it to the number `0` only after it knows the user typed something.

That order matters:

```python
text = input("Number: ").strip()

if text:
    number = int(text)
    print(number)
else:
    print("No number entered.")
```

First check whether text was entered. Then convert the text to a number.

## Common Mistake

### Mistake 1: Thinking `"False"` is falsy

This string is truthy:

```python
answer = "False"

if answer:
    print("Truthy")
else:
    print("Falsy")
```

You should see:

```text
Truthy
```

Python is not reading the English meaning of the word. It is checking whether the string has characters.

The same is true for:

```python
"no"
"0"
"None"
```

They are all non-empty strings, so they are truthy.

If you need to check what the user typed, compare the text:

```python
answer = input("Continue? yes/no ").strip().lower()

if answer == "yes":
    print("Continuing.")
else:
    print("Stopping.")
```

### Mistake 2: Using truthiness for a specific number rule

Broken code:

```python
age = 12

if age:
    print("Adult")
else:
    print("Not adult")
```

This runs, but it is broken for the rule "adult means at least 18."

You should see:

```text
Adult
```

`12` is truthy because it is not zero. It says nothing about whether the person is an adult.

Fixed code:

```python
age = 12

if age >= 18:
    print("Adult")
else:
    print("Not adult")
```

You should see:

```text
Not adult
```

### Mistake 3: Forgetting that spaces are still characters

This string may look empty:

```python
name = "   "
```

But it is truthy because it contains spaces.

```python
print(bool(name))
print(bool(name.strip()))
```

You should see:

```text
True
False
```

If you want spaces-only input to count as missing, clean it first:

```python
name = input("Name: ").strip()

if name:
    print("Name entered.")
else:
    print("Name missing.")
```

### Mistake 4: Confusing truthiness with `== True`

This condition:

```python
if value:
```

means:

```text
If value passes Python's truth test...
```

It does not mean:

```python
if value == True:
```

For example:

```python
value = "hello"

print(bool(value))
print(value == True)
```

You should see:

```text
True
False
```

Truthy is not the same as literally equal to `True`.

## Debug It

Here is a program with a logic bug.

The rule is:

```text
Only continue if the user typed yes.
```

Broken code:

```python
answer = input("Continue? yes/no ")

if answer:
    print("Continuing.")
else:
    print("Stopping.")
```

Try typing:

```text
no
```

You should see:

```text
Continuing.
```

That is wrong for the rule.

The program only checked whether the user typed something. `"no"` is a non-empty string, so it is truthy.

Fixed code:

```python
answer = input("Continue? yes/no ").strip().lower()

if answer == "yes":
    print("Continuing.")
else:
    print("Stopping.")
```

Now the condition checks the exact answer.

Here is another case to think through:

```python
points = 0

if points:
    print("You have points.")
else:
    print("No points yet.")
```

You should see:

```text
No points yet.
```

This is fine if the rule is:

```text
Say whether the player has any points.
```

It is not fine if the rule is:

```text
Say whether the score exists.
```

The score does exist. Its value is `0`.

When a truthy or falsy check surprises you, print both the value and its truth value:

```python
print("points:", points)
print("bool(points):", bool(points))
```

You should see:

```text
points: 0
bool(points): False
```

That helps you separate two questions:

```text
What is the actual value?
How does Python treat it in a condition?
```

## Read the Docs

Python's official documentation calls this idea **truth value testing**.

Find this page:

```text
https://docs.python.org/3/library/stdtypes.html#truth-value-testing
```

You do not need to understand every detail. Look for the list of values that are considered false, especially:

```python
None
False
0
""
[]
{}
()
```

For now, read the documentation with this beginner model:

```text
False itself is false.
Nothing is false.
Zero is false.
Empty containers are false.
Most other things are true.
```

The docs may mention that objects can define their own truth value. That is for later. Today, focus on strings, numbers, and simple collections.

## Mini Challenge

Create a file named:

```text
day-17/profile_checker.py
```

Build a small profile checker.

Ask for:

```text
Name
Age
Bio
```

For today, assume the age is either blank or a whole number.

The profile is complete when:

- the name is not empty
- the age was entered
- the bio is not empty

Start with this:

```python
name = input("Name: ").strip()
age_text = input("Age: ").strip()
bio = input("Bio: ").strip()
```

Then create clear boolean variables:

```python
has_name = bool(name)
has_age = bool(age_text)
has_bio = bool(bio)
```

Then combine them:

```python
profile_complete = has_name and has_age and has_bio
```

One possible solution:

```python
name = input("Name: ").strip()
age_text = input("Age: ").strip()
bio = input("Bio: ").strip()

has_name = bool(name)
has_age = bool(age_text)
has_bio = bool(bio)

profile_complete = has_name and has_age and has_bio

if profile_complete:
    age = int(age_text)
    print("Profile complete.")
    print("Next year you will be", age + 1)
else:
    print("Profile incomplete.")
```

Test these cases:

| Name | Age | Bio | Result |
| --- | --- | --- | --- |
| `Ari` | `14` | `Learning Python` | Profile complete. |
| empty | `14` | `Learning Python` | Profile incomplete. |
| `Ari` | empty | `Learning Python` | Profile incomplete. |
| `Ari` | `0` | `New here` | Profile complete. |
| spaces only | `14` | `Learning Python` | Profile incomplete. |

The fourth case matters. The user typed `0`, so `age_text` is `"0"`. That is not empty text, so it counts as present.

## Real-World Use

Truthy and falsy values appear in ordinary programs.

Examples:

- a form checks whether a required text field was filled in
- a shopping cart checks whether it has any items
- a search page checks whether the user typed a search term
- a game checks whether the player has any lives left
- a settings page checks whether optional information was provided

You will see patterns like these:

```python
if username:
    print("Username entered.")
```

```python
if tasks:
    print("You have tasks to do.")
```

```python
if not message:
    print("Message is empty.")
```

Those are useful when the program cares about presence.

Real programs also need exact rules:

```python
if password == correct_password:
    print("Login successful.")
```

```python
if cart_total >= 50:
    print("Free shipping offer available.")
```

Knowing the difference is what makes truthiness safe to use.

## Recap

Today you learned:

- Python can test many values in conditions, not only `True` and `False`
- values that count as true are called truthy
- values that count as false are called falsy
- an empty string `""` is falsy
- a non-empty string is truthy, even `"0"` or `"False"`
- the number `0` is falsy
- non-zero numbers are truthy
- empty collections like `[]` are falsy
- non-empty collections are truthy
- `bool(value)` shows how Python treats a value in a condition
- `if value:` is not the same as `if value == True:`
- truthiness is best for checking presence
- explicit comparisons are clearer for exact rules

Main idea:

```text
Ask whether you mean "is something present?" or "does this match a specific rule?"
```

## Lesson Checklist

Before moving on, check that you can:

- explain truthy and falsy in your own words
- name at least three falsy values
- predict the truth value of `""`, `"0"`, `0`, `5`, `[]`, and `["task"]`
- use `bool()` to inspect a value
- use `.strip()` before checking user-entered text
- explain why `"False"` is truthy
- explain why `if age:` is not the same as `if age >= 18:`
- choose between truthiness and an explicit comparison
- fix the broken examples from the Common Mistake and Debug It sections

## Exercises

### Exercise 1

Predict the output before running the code.

```python
print(bool(""))
print(bool("python"))
print(bool(0))
print(bool(1))
print(bool("0"))
```

### Exercise 2

Create a file named:

```text
day-17/username_check.py
```

Ask for a username. If the username is not empty, print:

```text
Username saved.
```

Otherwise, print:

```text
Username missing.
```

Use `.strip()` so spaces-only input counts as missing.

### Exercise 3

Explain why this prints `Continuing`:

```python
answer = "no"

if answer:
    print("Continuing")
else:
    print("Stopping")
```

Then write a fixed version that only continues when `answer` is `"yes"`.

### Exercise 4

Predict the output.

```python
message = " "

print(bool(message))
print(bool(message.strip()))
```

Why are the answers different?

### Exercise 5

Fix this program.

The rule is:

```text
Print "Adult" only if age is at least 18.
```

Broken code:

```python
age = 12

if age:
    print("Adult")
else:
    print("Not adult")
```

### Exercise 6

Write a small cart program using:

```python
items_in_cart = 0
```

Print:

```text
Cart has items.
```

when the cart has at least one item.

Print:

```text
Cart is empty.
```

when it has none.

You may use:

```python
if items_in_cart:
```

or:

```python
if items_in_cart > 0:
```

Which version feels clearer for this rule?

### Exercise 7

Use `bool()` to inspect these values:

```python
print(bool("False"))
print(bool("None"))
print(bool([]))
print(bool(["task"]))
print(bool(-1))
```

Before running the code, write down what you expect.

### Exercise 8

Debug this program.

The rule is:

```text
Only print "Login successful" if the typed password matches the correct password.
```

Broken code:

```python
correct_password = "python123"
typed_password = "wrong"

if typed_password:
    print("Login successful")
else:
    print("Password missing")
```

Write a fixed version.

### Exercise 9

Create a file named:

```text
day-17/search_term.py
```

Ask for a search term. If the search term is empty, print:

```text
Please enter a search term.
```

Otherwise, print:

```text
Searching for: <term>
```

Make sure spaces-only input counts as empty.

### Exercise 10

Read this code:

```python
age_text = input("Age: ").strip()

if age_text:
    age = int(age_text)
    print("Age entered:", age)
else:
    print("No age entered.")
```

What happens if the user types:

```text
0
```

Explain the difference between:

```python
age_text = "0"
```

and:

```python
age = 0
```

in terms of truthiness.

### Exercise 11

Write a small program that checks whether a profile has optional contact information.

Ask for:

```text
Email
Phone number
```

If either one is present, print:

```text
Contact info provided.
```

Otherwise, print:

```text
No contact info provided.
```

Use clear boolean names:

```python
has_email
has_phone
has_contact_info
```

### Exercise 12

Choose one condition from a previous lesson.

Ask:

```text
Is this checking presence, or is it checking a specific rule?
```

If it checks presence, try writing it with truthiness.

If it checks a specific rule, keep or add an explicit comparison.

Run the program to make sure the behavior still makes sense.

## Tiny Win

You now understand why this works:

```python
if name:
    print("Name entered.")
```

That line means Python is checking whether `name` has a truthy value.

You also know when not to use it. That judgment matters more than memorizing a list.

## Tomorrow

Tomorrow you will learn about common logic bugs.

Truthy and falsy values are useful, but they can create surprises:

```python
if answer:
    print("Continuing.")
```

That condition accepts `"yes"`, but it also accepts `"no"`, `"maybe"`, and any other non-empty string.

Tomorrow is about catching mistakes like that before they quietly change what your program does.
