# Day 16: Cleaner Conditions

**Focus:** Making condition code easier to read and debug  
**You will practice:** Naming booleans, simplifying long conditions, reducing nesting, using chained comparisons, and debugging boolean logic  
**Estimated time:** 40-50 minutes

## Today's Goal

Today you will learn how to make condition code easier to read.

You already know how to write `if`, `else`, and `elif`. You also know how to combine conditions with `and`, `or`, and `not`.

Now the goal is to make those conditions clearer.

By the end of this lesson, you should be able to:

- split a long condition into smaller named booleans
- choose boolean names that read like yes-or-no questions
- reduce nesting when several checks belong to one rule
- avoid repeating the same comparison again and again
- use chained comparisons for simple ranges
- debug a confusing condition by printing smaller boolean values
- keep the program's behavior the same while making the code easier to read

The main idea is:

> Name the question before you depend on the answer.

Broken examples are labeled clearly. Study them first; run them only when you want to see the problem.

## The Big Idea

A condition should answer one clear yes-or-no question.

This condition works:

```python
age = 17
is_registered = True
is_waitlisted = False
has_paid = False
has_scholarship = True

if age >= 16 and is_registered and not is_waitlisted and (has_paid or has_scholarship):
    print("You can join the workshop.")
else:
    print("You cannot join yet.")
```

You should see:

```text
You can join the workshop.
```

The code is correct, but the `if` line asks several questions at once:

```text
Is the person old enough?
Did the person register?
Is the person not on the waitlist?
Has payment been handled somehow?
```

You can make the same rule easier to read by naming the smaller questions.

Example:

```python
age = 17
is_registered = True
is_waitlisted = False
has_paid = False
has_scholarship = True

is_old_enough = age >= 16
has_confirmed_spot = is_registered and not is_waitlisted
has_payment_covered = has_paid or has_scholarship

can_join = is_old_enough and has_confirmed_spot and has_payment_covered

if can_join:
    print("You can join the workshop.")
else:
    print("You cannot join yet.")
```

You should see:

```text
You can join the workshop.
```

The program did not become more powerful. It became easier to inspect.

Good refactoring should protect the meaning of the code while making that meaning easier to see.

## The Mental Model

Think of a condition as a sentence.

This is a long sentence:

```text
if age >= 18 and has_ticket and not is_banned and (is_member or has_coupon):
    print("Special entry allowed.")
```

It is legal Python, but a reader has to hold a lot in their head at once.

Cleaner code turns the long sentence into smaller sentences:

```python
age = 20
has_ticket = True
is_banned = False
is_member = False
has_coupon = True

is_adult = age >= 18
has_valid_entry = has_ticket and not is_banned
has_special_access = is_member or has_coupon

can_use_special_entry = is_adult and has_valid_entry and has_special_access

if can_use_special_entry:
    print("Special entry allowed.")
else:
    print("Special entry denied.")
```

You should see:

```text
Special entry allowed.
```

The final `if` now reads like a summary:

```text
if can_use_special_entry:
    print("Special entry allowed.")
```

Boolean names often begin with words like:

- `is`
- `has`
- `can`
- `should`
- `needs`

Examples:

```python
age = 18
ticket_count = 2
attempts_left = 1

is_adult = age >= 18
has_ticket = ticket_count > 0
can_enter = is_adult and has_ticket
should_show_warning = attempts_left == 1

print(can_enter)
print(should_show_warning)
```

You should see:

```text
True
True
```

A clear boolean name says what the answer means.

This is hard to read:

```python
age = 18
ticket_count = 2

check = age >= 18 and ticket_count > 0

if check:
    print("Entry allowed.")
```

This is clearer:

```python
age = 18
ticket_count = 2

is_adult = age >= 18
has_ticket = ticket_count > 0
can_enter = is_adult and has_ticket

if can_enter:
    print("Entry allowed.")
```

You should see:

```text
Entry allowed.
```

Cleaner conditions can also reduce unnecessary nesting.

Nested code is useful when one decision truly belongs inside another. But if several checks are really one rule, a named boolean can be easier to follow.

Example:

```python
age = 20
has_ticket = True
is_banned = False

if age >= 18:
    if has_ticket:
        if not is_banned:
            print("Entry allowed.")
        else:
            print("Entry denied.")
    else:
        print("Entry denied.")
else:
    print("Entry denied.")
```

You should see:

```text
Entry allowed.
```

The rule is simpler than the indentation suggests:

```text
The person can enter if they are an adult,
have a ticket,
and are not banned.
```

Code:

```python
age = 20
has_ticket = True
is_banned = False

is_adult = age >= 18
can_enter = is_adult and has_ticket and not is_banned

if can_enter:
    print("Entry allowed.")
else:
    print("Entry denied.")
```

You should see:

```text
Entry allowed.
```

Cleaner conditions can also remove repeated checks.

Example:

```python
age = 16
has_permission = True

is_minor = age < 18

if is_minor and has_permission:
    print("You can join with permission.")
elif is_minor:
    print("You need permission.")
else:
    print("You can join.")
```

You should see:

```text
You can join with permission.
```

The comparison `age < 18` now appears once. The name `is_minor` carries that idea through the rest of the decision.

For ranges, Python also gives you chained comparisons.

Example:

```python
score = 87

is_valid_score = 0 <= score <= 100

if is_valid_score:
    print("Valid score")
else:
    print("Invalid score")
```

You should see:

```text
Valid score
```

Read this line from left to right:

```text
is_valid_score = 0 <= score <= 100
```

It means:

```text
score is at least 0 and no more than 100
```

That usually reads better than:

```text
is_valid_score = score >= 0 and score <= 100
```

Both versions work. Use the one that is easiest to read.

## Try It Yourself

Create a file named:

```text
day-16/clean_access_check.py
```

Code:

```python
age = int(input("Age: "))
ticket_answer = input("Do you have a ticket? yes/no ")
banned_answer = input("Are you banned? yes/no ")

has_ticket = ticket_answer == "yes"
is_banned = banned_answer == "yes"

is_adult = age >= 18
can_enter = is_adult and has_ticket and not is_banned

if can_enter:
    print("Entry allowed.")
else:
    print("Entry denied.")
```

Run the file from your course folder:

```bash
python day-16/clean_access_check.py
```

If your computer uses `py`, use:

```bash
py day-16/clean_access_check.py
```

If your computer uses `python3`, use:

```bash
python3 day-16/clean_access_check.py
```

Test these cases:

| Age | Ticket | Banned | You should see |
| --- | --- | --- | --- |
| 20 | yes | no | Entry allowed. |
| 17 | yes | no | Entry denied. |
| 20 | no | no | Entry denied. |
| 20 | yes | yes | Entry denied. |

After each run, ask:

```text
Which smaller boolean made can_enter become True or False?
```

That question is useful when a condition does not behave the way you expected.

## Common Mistake

### Mistake 1: Comparing a boolean to `True`

This works, but it is noisy:

```python
is_member = True

if is_member == True:
    print("Discount applied.")
```

Use the boolean directly:

```python
is_member = True

if is_member:
    print("Discount applied.")
```

You should see:

```text
Discount applied.
```

The variable `is_member` already holds either `True` or `False`.

For the opposite case, this works but is also noisy:

```python
is_member = False

if is_member == False:
    print("No discount.")
```

Use `not` instead:

```python
is_member = False

if not is_member:
    print("No discount.")
```

You should see:

```text
No discount.
```

### Mistake 2: Using a vague boolean name

This code runs, but the name does not help much:

```python
age = 20
has_ticket = True

ok = age >= 18 and has_ticket

if ok:
    print("Entry allowed.")
```

The name `ok` does not say what is okay.

Use a name that describes the answer:

```python
age = 20
has_ticket = True

can_enter = age >= 18 and has_ticket

if can_enter:
    print("Entry allowed.")
```

You should see:

```text
Entry allowed.
```

### Mistake 3: Hiding too much inside one condition

This condition is legal, but it is tiring to inspect:

```python
age = 20
has_ticket = True
is_banned = False
is_vip = False
has_coupon = True
attempts_left = 2

if age >= 18 and has_ticket and not is_banned and (is_vip or has_coupon) and attempts_left > 0:
    print("Entry allowed.")
else:
    print("Entry denied.")
```

Break the rule into smaller questions:

```python
age = 20
has_ticket = True
is_banned = False
is_vip = False
has_coupon = True
attempts_left = 2

is_adult = age >= 18
has_valid_entry = has_ticket and not is_banned
has_bonus_access = is_vip or has_coupon
can_still_try = attempts_left > 0

can_enter = is_adult and has_valid_entry and has_bonus_access and can_still_try

if can_enter:
    print("Entry allowed.")
else:
    print("Entry denied.")
```

You should see:

```text
Entry allowed.
```

Long conditions are not automatically bad. But if you cannot explain the condition in one simple sentence, it may need smaller names.

## Debug It

Here is a program with a logic bug.

The rule is supposed to be:

```text
A customer gets free shipping if:

the order total is at least 50
and
the account is active
and
the shipping address is in the country.
```

Broken code:

```python
order_total = 40
account_active = True
in_country = True

if order_total >= 50 and account_active or in_country:
    print("Free shipping")
else:
    print("Shipping fee added")
```

You should see:

```text
Free shipping
```

That is wrong. The order total is only `40`.

Python reads the condition like this:

```text
if (order_total >= 50 and account_active) or in_country:
    print("Free shipping")
```

Because `in_country` is `True`, the whole condition becomes `True`.

Fixed code:

```python
order_total = 40
account_active = True
in_country = True

has_enough_total = order_total >= 50
can_receive_shipping = account_active and in_country
gets_free_shipping = has_enough_total and can_receive_shipping

print("has_enough_total:", has_enough_total)
print("can_receive_shipping:", can_receive_shipping)
print("gets_free_shipping:", gets_free_shipping)

if gets_free_shipping:
    print("Free shipping")
else:
    print("Shipping fee added")
```

You should see:

```text
has_enough_total: False
can_receive_shipping: True
gets_free_shipping: False
Shipping fee added
```

When a condition behaves strangely:

1. Give each important question a name.
2. Print those names.
3. Find the answer that surprises you.
4. Fix the small question before rewriting the whole program.

Debugging conditions is often easier when you make the invisible answers visible.

## Read the Docs

Read these sections of the Python documentation:

```text
https://docs.python.org/3/reference/expressions.html#boolean-operations
https://docs.python.org/3/reference/expressions.html#comparisons
```

For today, look for these boolean operations:

```text
x and y
x or y
not x
```

Also look for this comparison shape:

```text
x < y <= z
```

That second form is called a chained comparison.

You do not need to understand every detail on the page. Official documentation often includes advanced cases.

For now, translate the useful parts into beginner language:

```text
and means both sides must pass.
or means at least one side must pass.
not flips a boolean answer.
chained comparisons can make simple ranges easier to read.
```

## Mini Challenge

Create a file named:

```text
day-16/free_shipping_checker.py
```

Build a cleaner checkout checker.

Ask the user:

```text
What is the order total?
Is the account active? yes/no
Is the shipping address in the country? yes/no
Does the customer have a free shipping coupon? yes/no
```

Rules:

```text
The customer gets free shipping if:

the account is active
and
the shipping address is in the country
and
either the order total is at least 50 or the customer has a coupon.
```

Start with:

```python
order_total = float(input("Order total: "))

active_answer = input("Is the account active? yes/no ")
country_answer = input("Is the shipping address in the country? yes/no ")
coupon_answer = input("Does the customer have a free shipping coupon? yes/no ")

account_active = active_answer == "yes"
in_country = country_answer == "yes"
has_coupon = coupon_answer == "yes"
```

Then create clear boolean variables before the final `if`.

Possible names:

```text
has_enough_total
can_receive_shipping
has_free_shipping_offer
gets_free_shipping
```

One possible solution:

```python
order_total = float(input("Order total: "))

active_answer = input("Is the account active? yes/no ")
country_answer = input("Is the shipping address in the country? yes/no ")
coupon_answer = input("Does the customer have a free shipping coupon? yes/no ")

account_active = active_answer == "yes"
in_country = country_answer == "yes"
has_coupon = coupon_answer == "yes"

has_enough_total = order_total >= 50
can_receive_shipping = account_active and in_country
has_free_shipping_offer = has_enough_total or has_coupon

gets_free_shipping = can_receive_shipping and has_free_shipping_offer

if gets_free_shipping:
    print("Free shipping")
else:
    print("Shipping fee added")
```

Test your program with these cases:

| Total | Active | In country | Coupon | You should see |
| --- | --- | --- | --- | --- |
| 60 | yes | yes | no | Free shipping |
| 30 | yes | yes | yes | Free shipping |
| 30 | yes | yes | no | Shipping fee added |
| 80 | no | yes | yes | Shipping fee added |
| 80 | yes | no | yes | Shipping fee added |

If your result is wrong, print each boolean variable before the final `if`.

## Real-World Use

Cleaner conditions show up anywhere a program has rules.

Examples:

- a login system checks whether the password is correct and the account is active
- a store checks whether a discount or shipping rule applies
- a game checks whether a level is complete
- a form checks whether required fields were filled in
- a calendar app checks whether a reminder should appear

In real programs, rules change often.

Someone might say:

```text
VIP customers can skip the minimum order total.
Students need parent permission if they are under 13.
Locked accounts can only be opened by support staff.
```

If your conditions have clear names, those changes are easier to make. You can look for the exact question that needs to change.

## Recap

Today you learned:

- cleaner conditions are easier to read, test, and debug
- long conditions can often be split into named boolean variables
- good boolean names often start with `is`, `has`, `can`, `should`, or `needs`
- unnecessary nesting can sometimes be replaced with one clear combined condition
- repeated comparisons can often be named once and reused
- chained comparisons are useful for readable ranges like `0 <= score <= 100`
- comparing a boolean to `True` or `False` is usually unnecessary
- printing smaller boolean values is a good way to debug confusing logic

Main idea:

```text
Name the question before you depend on the answer.
```

## Lesson Checklist

Before moving on, check that you can:

- split a crowded condition into smaller boolean variables
- choose boolean names that explain the yes-or-no answer
- use `not` instead of comparing a boolean to `False`
- combine related checks without unnecessary nesting
- name a repeated comparison instead of writing it several times
- use a chained comparison for a simple range
- print boolean variables to debug a confusing condition
- explain why a refactor should keep the same behavior

## Exercises

### Exercise 1

Predict the output before running the code.

```python
age = 15
has_permission = True

is_minor = age < 18
can_join = not is_minor or has_permission

print(is_minor)
print(can_join)
```

### Exercise 2

Make this condition easier to read by creating smaller boolean variables:

```python
age = 20
has_ticket = True
is_banned = False

if age >= 18 and has_ticket and not is_banned:
    print("Entry allowed.")
else:
    print("Entry denied.")
```

Possible names:

```text
is_adult
can_enter
```

### Exercise 3

Rewrite this range check using a chained comparison:

```python
score = 87

if score >= 0 and score <= 100:
    print("Valid score")
```

### Exercise 4

Clean up this code by avoiding the repeated comparison:

```python
age = 12
has_parent_permission = False

if age < 13 and has_parent_permission:
    print("Allowed with permission.")
elif age < 13 and not has_parent_permission:
    print("Needs permission.")
else:
    print("Allowed.")
```

Create a boolean named:

```text
is_under_13
```

### Exercise 5

Reduce the unnecessary nesting.

```python
has_username = True
has_password = True
account_locked = False

if has_username:
    if has_password:
        if not account_locked:
            print("Login ready.")
        else:
            print("Login blocked.")
    else:
        print("Login blocked.")
else:
    print("Login blocked.")
```

Write a cleaner version using a boolean named:

```text
can_try_login
```

### Exercise 6

Fix the unnecessary boolean comparison.

```python
is_subscribed = True

if is_subscribed == True:
    print("Show newsletter.")
else:
    print("Hide newsletter.")
```

### Exercise 7

Debug this condition.

The rule is supposed to be:

```text
Show the warning if the battery is below 20
and
the device is not charging.
```

Broken code:

```python
battery = 75
is_charging = False

if battery < 20 or not is_charging:
    print("Low battery warning")
else:
    print("Battery okay")
```

Why is it wrong? Write a fixed version.

### Exercise 8

Create clear boolean names for this rule:

```text
A student passes if:

their score is at least 60
and
they submitted the project
and
they have no missing assignments.
```

Use these starting variables:

```python
score = 72
submitted_project = True
missing_assignments = 0
```

Possible names:

```text
has_passing_score
has_complete_work
passes_course
```

### Exercise 9

Write a small program that checks whether a password change is allowed.

Rules:

```text
The password can be changed if:

the old password is correct
and
the new password is at least 8 characters long
and
the account is not locked.
```

You may start with:

```python
old_password = "python123"
typed_old_password = "python123"
new_password = "betterpass"
account_locked = False
```

Use boolean variables with clear names before your final `if`.

### Exercise 10

Choose one program from Days 12, 13, 14, or 15.

Look for one condition that feels crowded.

Clean it by doing at least one of these:

```text
Name a boolean.
Remove unnecessary nesting.
Avoid a repeated comparison.
Use a chained comparison for a range.
```

Run the program again to make sure the behavior stayed the same.

## Tiny Win

You can now make a condition easier to read without changing what it does.

That is one of the first real refactoring skills.

## Tomorrow

Tomorrow you will learn about truthy and falsy values.

So far, most of your conditions have used clear boolean values:

```text
True
False
```

But Python can also make decisions with other values:

```python
name = ""

if name:
    print("Name entered")
else:
    print("Name missing")
```

Why does an empty string act like false?

That is tomorrow's question.
