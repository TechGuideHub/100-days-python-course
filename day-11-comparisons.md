# Day 11: Comparisons

**Focus:** Comparing values and reading boolean results  
**You will practice:** Equality, inequality, number comparisons, string comparisons, boolean variables, and comparison debugging  
**Estimated time:** 40-50 minutes

## Today's Goal

Today you will learn how Python compares values.

By the end of this lesson, you should be able to:

* use `==` to check whether two values are equal
* use `!=` to check whether two values are different
* use `>`, `<`, `>=`, and `<=` with numbers
* understand that comparisons produce `True` or `False`
* compare simple strings
* avoid confusing assignment with comparison
* use small print statements to debug comparison problems

You already met booleans on Day 7. Today you will see one of the most common ways Python creates them.

A comparison asks a yes-or-no question.

```python
print(10 > 5)
print("cat" == "cat")
print(7 != 7)
```

You should see:

```text
True
True
False
```

That idea will prepare you for `if` statements tomorrow.

## The Big Idea

Programs often need to check facts.

```text
Is the score high enough?
Are the two passwords the same?
Is the temperature below zero?
Is the username different from the saved username?
Is the player out of lives?
```

These questions do not need long answers. They need yes or no.

In Python, a comparison turns a question about values into a boolean answer.

```python
score = 76
passing_score = 50

print(score >= passing_score)
```

This asks:

```text
Is score greater than or equal to passing_score?
```

Python answers:

```text
True
```

That answer is a boolean, just like the values you studied earlier.

## The Mental Model

Think of a comparison as a small test.

The test checks one rule and gives one answer.

```python
speed = 72
speed_limit = 60

is_speeding = speed > speed_limit

print(is_speeding)
```

You should see:

```text
True
```

Read this line slowly:

```python
is_speeding = speed > speed_limit
```

It means:

```text
Ask whether speed is greater than speed_limit.
Store the answer in is_speeding.
```

The value stored in `is_speeding` is not the speed. It is the answer to the comparison.

This pattern is common:

```python
is_passing = score >= 50
is_empty = item_count == 0
is_different = first_name != second_name
```

Boolean variable names often start with words like `is`, `has`, or `can` because those names read like yes-or-no questions.

## Comparison Operators

Python gives you several comparison operators.

```text
==   equal to
!=   not equal to
>    greater than
<    less than
>=   greater than or equal to
<=   less than or equal to
```

Here they are with numbers:

```python
print(5 == 5)
print(5 != 5)
print(8 > 3)
print(8 < 3)
print(10 >= 10)
print(4 <= 9)
```

You should see:

```text
True
False
True
False
True
True
```

The boundary operators are especially useful.

```python
minimum_age = 18
user_age = 18

can_enter = user_age >= minimum_age

print(can_enter)
```

You should see:

```text
True
```

The user is not older than 18. The user is exactly 18, and `>=` includes equality.

The same idea works with `<=`.

```python
max_attempts = 3
attempts_used = 3

still_allowed = attempts_used <= max_attempts

print(still_allowed)
```

You should see:

```text
True
```

## Comparing Numbers

Number comparisons usually feel familiar because they use symbols you may already know from math.

```python
age = 18

print(age == 18)
print(age > 18)
print(age >= 18)
print(age < 18)
print(age <= 18)
print(age != 18)
```

You should see:

```text
True
False
True
False
True
False
```

Read each comparison as a question:

```text
age == 18     Is age equal to 18?
age > 18      Is age greater than 18?
age >= 18     Is age greater than or equal to 18?
age != 18     Is age different from 18?
```

Many real rules include a boundary:

```text
18 or older
50 or more
100 or less
at least 1 item
no more than 3 attempts
```

Those are good moments for `>=` and `<=`.

## Comparing Strings

You can compare strings too.

The most common beginner string comparisons are equality and inequality.

```python
print("apple" == "apple")
print("apple" == "banana")
print("apple" != "banana")
```

You should see:

```text
True
False
True
```

String comparisons are exact. Capital letters matter.

```python
print("Python" == "Python")
print("Python" == "python")
```

You should see:

```text
True
False
```

Spaces matter too.

```python
print("cat" == "cat")
print("cat" == "cat ")
```

You should see:

```text
True
False
```

The second string has a space at the end. Python treats that space as part of the text.

Here is a simple password check:

```python
saved_password = "sunrise"
typed_password = "sunrise"

password_matches = typed_password == saved_password

print(password_matches)
```

You should see:

```text
True
```

If you change the typed password:

```python
typed_password = "Sunrise"
```

then the comparison becomes `False` because uppercase `S` and lowercase `s` are different characters.

Python can also compare strings with `<` and `>`, using alphabetical ordering:

```python
print("apple" < "banana")
print("zebra" > "ant")
```

You should see:

```text
True
True
```

For now, focus mostly on `==` and `!=` with strings. Exact matches are the comparison you will use most often at this stage.

## Example

Create a file named:

```text
day-11/score_check.py
```

Code:

```python
score = 76
passing_score = 50
perfect_score = 100

is_passing = score >= passing_score
is_perfect = score == perfect_score
needs_practice = score < passing_score

print("Score:", score)
print("Passing score:", passing_score)
print("Is passing?", is_passing)
print("Is perfect?", is_perfect)
print("Needs practice?", needs_practice)
```

You should see:

```text
Score: 76
Passing score: 50
Is passing? True
Is perfect? False
Needs practice? False
```

This program does not make decisions yet. It only checks facts.

These are the most important lines:

```python
is_passing = score >= passing_score
is_perfect = score == perfect_score
needs_practice = score < passing_score
```

Each line asks a question and stores the answer.

Now change the score:

```python
score = 42
```

The comparison answers change:

```text
Is passing? False
Is perfect? False
Needs practice? True
```

The code stayed the same. The data changed, so the answers changed.

## Try It Yourself

Create a file named:

```text
day-11/comparison_practice.py
```

Type this program:

```python
temperature = 28
freezing_point = 0
hot_day = 30

is_freezing = temperature <= freezing_point
is_hot = temperature >= hot_day
is_not_freezing_point = temperature != freezing_point

print("Temperature:", temperature)
print("Is freezing?", is_freezing)
print("Is hot?", is_hot)
print("Is not exactly freezing?", is_not_freezing_point)
```

Run it. Then change `temperature` to each value below and run it again.

```python
0
12
30
35
```

Before each run, predict the answers.

Use this practice loop:

1. Change one value.
2. Predict the booleans.
3. Run the program.
4. Compare your prediction with the output.

You are learning to read the code before the computer runs it.

## Common Mistake

### Mistake 1: Using `=` when you mean `==`

One equals sign assigns a value.

```python
score = 100
```

This means:

```text
Store 100 in score.
```

Two equals signs compare values.

```python
score == 100
```

This means:

```text
Is score equal to 100?
```

Broken code:

```python
score = 100
is_perfect = score = 100

print(is_perfect)
```

This code runs, but it is broken for what we wanted.

It prints `100`, not `True`.

The line with two single equals signs assigns `100` to both names. It does not ask a question.

Fixed code:

```python
score = 100
is_perfect = score == 100

print(is_perfect)
```

You should see:

```text
True
```

Remember:

```text
=   assigns
==  compares
```

### Mistake 2: Reversing `>=` or `<=`

This is correct:

```python
age >= 18
```

Broken code:

```python
age => 18
```

The equals sign comes second.

Use:

```text
>=
<=
```

not:

```text
=>
=<
```

### Mistake 3: Expecting strings to ignore case

This comparison is false:

```python
print("yes" == "Yes")
```

You should see:

```text
False
```

Python compares the strings exactly. Later, you will learn ways to clean user input before comparing it.

## Debug It

Here is a broken program.

Broken code:

```python
score = 82
is_passing = score => 50

print(is_passing)
```

What is wrong?

The comparison operator is reversed. Python understands `>=`, not `=>`.

Fixed code:

```python
score = 82
is_passing = score >= 50

print(is_passing)
```

You should see:

```text
True
```

Here is another broken program.

Broken code:

```python
level = 3
is_level_three = level = 3

print(is_level_three)
```

The variable name `is_level_three` sounds like it should store a boolean, but the line uses assignment where it needs comparison.

Fixed code:

```python
level = 3
is_level_three = level == 3

print(is_level_three)
```

You should see:

```text
True
```

When debugging comparisons, print the pieces.

```python
level = 3

print("level:", level)
print("comparison result:", level == 3)
```

You should see:

```text
level: 3
comparison result: True
```

Small print statements can help you see what Python is actually comparing.

## Read the Docs

Look up Python's official documentation for comparisons:

```text
https://docs.python.org/3/reference/expressions.html#comparisons
```

Do not try to understand every detail. Official documentation often includes advanced cases.

Today, look only for these operators:

```text
<
<=
>
>=
==
!=
```

Your goal is to recognize the symbols you practiced today.

Documentation becomes less intimidating when you visit it in small, calm steps.

## Mini Challenge

Create a file named:

```text
day-11/ticket_checker.py
```

Write a small program that checks facts about a movie ticket.

Start with these variables:

```python
movie_title = "Hidden Figures"
ticket_price = 12
money_available = 15
minimum_age = 10
user_age = 11
requested_movie = "Hidden Figures"
```

Then create comparison results:

```python
can_afford_ticket = money_available >= ticket_price
is_old_enough = user_age >= minimum_age
movie_matches = requested_movie == movie_title
has_extra_money = money_available > ticket_price
```

Print a clear summary:

```python
print("Movie:", movie_title)
print("Ticket price:", ticket_price)
print("Money available:", money_available)
print("Can afford ticket?", can_afford_ticket)
print("Old enough?", is_old_enough)
print("Requested movie matches?", movie_matches)
print("Has extra money?", has_extra_money)
```

You should see:

```text
Movie: Hidden Figures
Ticket price: 12
Money available: 15
Can afford ticket? True
Old enough? True
Requested movie matches? True
Has extra money? True
```

Then change the data and run it again.

```python
money_available = 8
user_age = 9
requested_movie = "hidden figures"
```

Watch which comparison results change.

Pay special attention to this comparison:

```python
requested_movie == movie_title
```

The lowercase `h` changes the result because string comparison is exact.

## Real-World Use

Comparisons appear in almost every real program.

Examples:

* a login page checks whether the typed password matches the saved password
* a game checks whether the player's health is greater than `0`
* a shop checks whether the cart total is high enough for free delivery
* a form checks whether two email fields match
* a bank app checks whether the account balance is greater than the payment amount
* a school app checks whether a score is greater than or equal to the passing score

Today your programs are not choosing different paths yet. They are collecting the yes-or-no answers that decisions will need.

Tomorrow, you will use those answers with `if`.

## Recap

Today you learned:

* comparisons ask questions about values
* comparisons produce booleans: `True` or `False`
* `==` checks whether two values are equal
* `!=` checks whether two values are different
* `>` checks whether the left value is greater
* `<` checks whether the left value is less
* `>=` means greater than or equal to
* `<=` means less than or equal to
* string comparisons are exact
* `=` assigns a value, while `==` compares values
* printing comparison results can help you debug

Main idea:

```text
A comparison is a yes-or-no question written in code.
```

## Lesson Checklist

Before moving on, check that you can:

* explain what a comparison does
* predict whether a simple comparison will be `True` or `False`
* use `==` and `!=` correctly
* use `>`, `<`, `>=`, and `<=` with numbers
* explain why `"Python"` and `"python"` are different strings
* store a comparison result in a boolean variable
* spot when `=` was used instead of `==`
* fix a reversed comparison operator like `=>`

## Exercises

### Exercise 1

Predict the output before running this code:

```python
print(6 == 6)
print(6 != 6)
print(6 > 2)
print(6 < 2)
print(6 >= 6)
print(6 <= 5)
```

Then run it and check your prediction.

### Exercise 2

Create a file named:

```text
day-11/age_checks.py
```

Write this code:

```python
age = 16

is_child = age < 13
is_teenager = age >= 13
is_adult = age >= 18

print(is_child)
print(is_teenager)
print(is_adult)
```

Run it with different ages.

Try:

```python
8
13
18
21
```

### Exercise 3

Fix this code:

```python
temperature = 35
is_hot = temperature => 30

print(is_hot)
```

The program should print:

```text
True
```

### Exercise 4

Fix this code so `is_winner` stores a boolean:

```python
score = 10
is_winner = score = 10

print(is_winner)
```

The output should be:

```text
True
```

### Exercise 5

Write a program that compares two usernames.

Use:

```python
saved_username = "maya"
typed_username = "maya"
```

Create a variable named `username_matches`. It should store the result of comparing the two usernames.

Print the result.

Then change `typed_username` to:

```python
"Maya"
```

Run the program again and notice what changes.

### Exercise 6

Create a file named:

```text
day-11/price_checks.py
```

Use these variables:

```python
item_price = 45
money = 50
discount_price = 40
```

Create and print these comparison results:

* whether `money` is greater than or equal to `item_price`
* whether `item_price` is greater than `discount_price`
* whether `item_price` is equal to `discount_price`
* whether `money` is not equal to `0`

Use clear boolean variable names.

### Exercise 7

Write a small program about a game character.

Use at least these variables:

```python
health = 10
lives = 3
level = 2
```

Create comparison variables such as:

```python
is_alive = health > 0
has_lives_left = lives > 0
is_beginner_level = level <= 2
```

Print each result with a label. Then change the values and run the program again.

### Exercise 8

Predict the output:

```python
word_one = "tree"
word_two = "Tree"

print(word_one == word_two)
print(word_one != word_two)
```

Then run it.

Add a comment explaining why the first comparison is `False`.

```python
# This is False because uppercase and lowercase letters are different.
```

## Tiny Win

Before today, `True` and `False` may have looked like values you typed directly.

Now you know Python can create them by checking facts.

```python
score >= 50
password == saved_password
temperature < 0
```

You can now ask small questions in code and read Python's boolean answers.

## Tomorrow

Tomorrow, you will use comparisons with `if` statements.

That is where your programs begin choosing different paths based on whether a comparison is `True` or `False`.
