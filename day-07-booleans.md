# Day 07: Booleans

**Focus:** Boolean values, clear boolean names, and simple comparisons  
**You will practice:** writing `True` and `False`, storing yes-or-no facts, and reading comparison results  
**Estimated time:** 35-45 minutes

## Today's Goal

Today you will learn how Python stores yes-or-no answers.

In Python, those answers are called booleans. A boolean can be only one of two values:

```python
True
False
```

By the end of this lesson, you should be able to:

* recognize `True` and `False`
* store booleans in variables
* choose variable names that sound like yes-or-no questions
* understand that comparisons produce boolean answers
* avoid capitalization and quotation mark mistakes
* see how booleans prepare a program to make decisions

You do not need to master `if` statements today. Those are coming later.

For now, your job is to understand the kind of value a program needs before it can choose what to do next.

Broken examples are labeled clearly. Study them first; run them only when you want to see the error.

## The Big Idea

Programs often need to answer yes-or-no questions.

```text
Is the user logged in?
Is the password correct?
Is the cart empty?
Is the game over?
Is the temperature below freezing?
```

Each question has two possible answers:

```text
yes or no
```

Python writes those answers as:

```python
True
False
```

A boolean is Python's way of storing a yes-or-no answer.

That may sound small, but it matters. Without booleans, a program could remember information, but it would have a hard time deciding what to do with that information.

## The Mental Model

Think of a boolean like a light switch.

The switch can be:

```text
on
off
```

A boolean can be:

```python
True
False
```

Now connect the value to a clear variable name:

```python
is_light_on = True
is_door_locked = False
```

The variable name describes the question. The boolean value gives the answer.

```python
is_light_on = True
```

means:

```text
Is the light on? Yes.
```

Good boolean names often begin with words like:

* `is`
* `has`
* `can`
* `should`

```python
is_raining = True
has_ticket = False
can_vote = True
should_continue = False

print(is_raining)
print(has_ticket)
print(can_vote)
print(should_continue)
```

It prints:

```text
True
False
True
False
```

These names read almost like tiny questions. That makes the code easier to understand before you even run it.

## The Two Boolean Values

Python has two boolean values:

```python
True
False
```

Notice the capital letters.

```python
is_open = True
is_finished = False

print(is_open)
print(is_finished)
```

Python prints:

```text
True
False
```

Broken code:

```python
is_open = true
is_finished = false
```

Python cares about uppercase and lowercase letters. `True` and `False` must start with capital letters.

They are also not written inside quotation marks.

This is a boolean:

```python
is_ready = True
```

This is a string:

```python
is_ready = "True"
```

Those two lines may look similar, but they do not mean the same thing. `True` is a boolean value. `"True"` is text.

> Key idea: If you mean a yes-or-no value, use `True` or `False` without quotation marks.

## Boolean Variables

You can store a boolean in a variable just like you can store a number or a string.

```python
is_student = True
has_homework = False

print(is_student)
print(has_homework)
```

The output is:

```text
True
False
```

The variable does not have to begin with `is` or `has`, but those words often make boolean variables clearer.

Compare these two names:

```python
ticket = True
```

and:

```python
has_ticket = True
```

The second name is clearer. `ticket` might mean a ticket number, ticket price, or ticket name. `has_ticket` sounds like a yes-or-no fact.

> Checkpoint: A boolean variable should usually sound like a question that can be answered with yes or no.

Here is a small file you could save as `day-07/status_flags.py`.

```python
username = "maya"
is_logged_in = True
has_new_messages = False

print(username)
print(is_logged_in)
print(has_new_messages)
```

It prints:

```text
maya
True
False
```

The string stores a name. The booleans store facts about that name.

## Comparisons Give Boolean Answers

You have worked with numbers and strings already. Now you can ask Python questions about them.

```python
print(5 > 3)
print(5 < 3)
print(10 == 10)
print("cat" == "cat")
print("cat" == "dog")
```

Python prints:

```text
True
False
True
True
False
```

Each comparison asks a question.

```python
5 > 3
```

means:

```text
Is 5 greater than 3?
```

The answer is `True`.

This comparison:

```python
5 < 3
```

means:

```text
Is 5 less than 3?
```

The answer is `False`.

You will study comparisons more deeply later. For today, notice the pattern:

> Key idea: A comparison produces a boolean.

Here are comparison symbols you will see often:

```text
>   greater than
<   less than
==  equal to
!=  not equal to
>=  greater than or equal to
<=  less than or equal to
```

The `==` symbol is especially important.

This stores a value:

```python
age = 12
```

This asks a question:

```python
age == 12
```

One equals sign means:

```text
Store this value.
```

Two equals signs mean:

```text
Are these equal?
```

Here is a complete example you could save as `day-07/comparison_preview.py`.

```python
age = 12
minimum_age = 13

is_old_enough = age >= minimum_age
is_exactly_twelve = age == 12

print(is_old_enough)
print(is_exactly_twelve)
```

It prints:

```text
False
True
```

Read this line slowly:

```python
is_old_enough = age >= minimum_age
```

It means:

```text
Ask whether age is greater than or equal to minimum_age.
Store the answer in is_old_enough.
```

The stored answer is a boolean.

## Why Booleans Matter

Booleans matter because programs need to make decisions.

Imagine a weather program:

```python
is_raining = True
```

If the program knows `is_raining` is `True`, it can suggest an umbrella. If `is_raining` is `False`, it can skip that suggestion.

Here is a small preview of decision-making code:

```python
is_raining = True

if is_raining:
    print("Take an umbrella.")
else:
    print("Enjoy the walk.")
```

It prints:

```text
Take an umbrella.
```

Do not worry about the full `if` and `else` syntax yet. Just notice the idea:

```text
The boolean decides which path the program follows.
```

This is where programs begin to respond to a situation instead of only running the same lines every time.

## Example

Here is a small program about a library book. You could save it as `day-07/library_status.py`.

```python
book_title = "The Hobbit"
is_available = True
is_reserved = False

print(book_title)
print(is_available)
print(is_reserved)
```

It prints:

```text
The Hobbit
True
False
```

The string stores the book title. The booleans store yes-or-no facts about the book.

We can also use a comparison to create a boolean.

```python
copies_available = 3
has_copies = copies_available > 0

print(has_copies)
```

The output is:

```text
True
```

Read the middle line as a question:

```text
Are there more than 0 copies available?
```

The answer is `True`, so `has_copies` becomes `True`.

That is a common programming pattern:

```text
Ask a question.
Store the answer.
Use the answer later.
```

Here is the same idea preparing a program for a decision:

```python
copies_available = 0
has_copies = copies_available > 0

print("Ready to lend book?")
print(has_copies)
```

It prints:

```text
Ready to lend book?
False
```

The program is not making the lending decision yet. It is getting the yes-or-no fact ready.

## Try It Yourself

Create a file named `day-07/boolean_checks.py`.

Type this program:

```python
is_morning = True
is_weekend = False
has_breakfast = True

print(is_morning)
print(is_weekend)
print(has_breakfast)
```

Run it. Then change each boolean value and run it again:

```python
is_morning = False
is_weekend = True
has_breakfast = False

print(is_morning)
print(is_weekend)
print(has_breakfast)
```

You should see:

```text
False
True
False
```

This is not a complicated program. The point is to get comfortable seeing `True` and `False` as real values in Python.

After that, add a comparison:

```python
minutes_until_class = 15
is_late = minutes_until_class < 0

print(is_late)
```

Python prints:

```text
False
```

The comparison gives the program a boolean it could use later.

## Common Mistake

### Mistake 1: Writing `true` and `false`

Broken code:

```python
is_ready = true
```

Python does not understand `true`.

Fixed code:

```python
is_ready = True
```

Broken code:

```python
is_ready = false
```

Fixed code:

```python
is_ready = False
```

Capitalization matters.

### Mistake 2: Putting booleans in quotation marks

Broken code:

```python
is_ready = "True"
```

This runs, but it stores text instead of a boolean.

Fixed code:

```python
is_ready = True
```

Quotation marks are for strings. Booleans do not need quotation marks.

### Mistake 3: Using `=` when you mean `==`

This stores the number `10` in the variable:

```python
score = 10
```

This asks whether the score is equal to `10`:

```python
score == 10
```

One equals sign assigns. Two equals signs compare.

## Debug It

Here is a broken program.

Broken code:

```python
is_member = true
has_coupon = "False"

print(is_member)
print(has_coupon)
```

There are two problems.

First, `true` should be capitalized:

```python
True
```

Second, `"False"` is a string. If we want a real boolean, we remove the quotation marks:

```python
False
```

Fixed code:

```python
is_member = True
has_coupon = False

print(is_member)
print(has_coupon)
```

The fixed program prints:

```text
True
False
```

Here is another program with a quieter bug. It runs, but it does not store the kind of value the programmer wanted.

Broken code:

```python
age = 18
is_eighteen = age = 18

print(is_eighteen)
```

The second line uses `=` again, so Python stores `18` in both variable names. It does not ask a yes-or-no question.

Fixed code:

```python
age = 18
is_eighteen = age == 18

print(is_eighteen)
```

Now it prints:

```text
True
```

Read this line carefully:

```python
is_eighteen = age == 18
```

It means:

```text
Store whether age is equal to 18.
```

This may feel strange at first. You are learning how Python turns questions into values.

## Read the Docs

Find Python's official documentation for the boolean type:

```text
https://docs.python.org/3/library/stdtypes.html#boolean-type-bool
```

You do not need to understand the whole page.

Look for these values:

```python
True
False
```

The documentation may show advanced details. Let those wait. Today, your job is to recognize the type and use it correctly.

## Mini Challenge

Create a file named `day-07/movie_ticket.py`.

Write a small program that stores information about a movie ticket.

Use at least:

* one string
* one number
* three booleans

Start with something like this:

```python
movie_title = "Hidden Figures"
ticket_price = 12
has_ticket = True
is_vip = False
is_sold_out = False

print(movie_title)
print(ticket_price)
print(has_ticket)
print(is_vip)
print(is_sold_out)
```

It prints:

```text
Hidden Figures
12
True
False
False
```

Then add one comparison:

```python
ticket_price = 12
is_expensive = ticket_price > 10

print(is_expensive)
```

You should see:

```text
True
```

Run the program. Change the ticket price and run it again. Notice how the comparison result can change from `True` to `False`.

That change is the beginning of decision-making in code.

If you want one extra stretch, combine two boolean facts:

```python
has_ticket = True
is_sold_out = False

can_enter = has_ticket and not is_sold_out

print(can_enter)
```

It prints:

```text
True
```

You do not need to memorize `and` or `not` today. Just notice that a program can combine yes-or-no facts to prepare for a decision.

## Real-World Use

Booleans appear everywhere in real programs.

Examples:

* a website checks whether a user is logged in
* a game checks whether the player is alive
* a shopping app checks whether an item is in stock
* a banking app checks whether a transaction is approved
* a video app checks whether subtitles are turned on
* a school system checks whether an assignment is submitted

Many real programs are full of small yes-or-no facts. Each fact helps the program decide what to show, allow, block, or do next.

Here is a simple readiness check:

```python
has_username = True
has_password = True
accepted_terms = False

is_ready_to_create_account = has_username and has_password and accepted_terms

print(is_ready_to_create_account)
```

It prints:

```text
False
```

No account is created in this example. The program is only collecting the boolean answer it would need before making that decision.

Booleans are small values with a large job: they help programs choose.

## Recap

Today you learned:

* a boolean is a yes-or-no value
* Python's boolean values are `True` and `False`
* capitalization matters
* booleans are not strings
* boolean variables often start with `is`, `has`, `can`, or `should`
* comparisons produce boolean answers
* `=` assigns a value, while `==` compares values
* booleans help programs prepare for decisions

Main idea: a boolean stores the answer to a yes-or-no question.

## Lesson Checklist

Before moving on, check that you can:

* write `True` and `False` with the correct capitalization
* explain why `"True"` is a string, not a boolean
* choose boolean variable names that read like yes-or-no questions
* use comparisons such as `>`, `<`, `==`, and `!=` to produce boolean answers
* tell the difference between `=` for assignment and `==` for comparison
* fix the broken examples from the Common Mistake and Debug It sections

## Exercises

### Exercise 1

Create a file named `day-07/sunny_day.py`.

Create three boolean variables:

```python
is_sunny = True
has_homework = False
can_relax = True
```

Print each one. Then change the values and run the program again.

### Exercise 2

Fix this code.

Broken code:

```python
is_ready = true
print(is_ready)
```

### Exercise 3

Fix this code so `has_paid` stores a boolean, not a string.

Broken code:

```python
has_paid = "False"
print(has_paid)
```

### Exercise 4

Predict the output before running the code:

```python
print(8 > 3)
print(8 < 3)
print(8 == 8)
print(8 != 8)
```

Then run it and check your prediction.

### Exercise 5

Write a program that stores:

* your name as a string
* your age as a number
* whether you are learning Python as a boolean

Then print all three values.

### Exercise 6

Create this variable:

```python
temperature = 31
```

Then create a boolean named `is_hot`. Set `is_hot` by comparing whether `temperature` is greater than `30`.

Print `is_hot`.

### Exercise 7

Choose a real object near you, such as a phone, bag, book, or cup.

Write four boolean variables about it:

```python
is_charging = False
has_case = True
is_heavy = False
is_new = True
```

Use names that read like yes-or-no questions.

### Exercise 8

Create a file named `day-07/ready_check.py`.

Store three boolean facts about getting ready for class:

```python
has_notebook = True
has_pen = True
has_finished_breakfast = False

is_ready_for_class = has_notebook and has_pen and has_finished_breakfast

print(is_ready_for_class)
```

Change one value at a time and watch the final boolean change.

## Tiny Win

Before today, `True` and `False` may have looked like ordinary words.

Now you know they are real Python values. They let a program store answers, check facts, and prepare for decisions.

## Tomorrow

Tomorrow, you will use input and output so your programs can receive information from a person and respond on the screen.
