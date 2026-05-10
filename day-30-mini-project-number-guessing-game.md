# Day 30: Mini Project: Number Guessing Game

**Focus:** Building a complete guessing game with loops, input, random numbers, and clear exit conditions  
**You will practice:** `random`, variables, `input()`, `int()`, comparisons, `if` / `elif` / `else`, `while`, validation loops, counters, and debugging loop behavior  
**Estimated time:** 55-70 minutes

## Today's Goal

Today you will build a number guessing game.

The program will choose a secret number. The player will guess until they either find the number or run out of attempts.

By the end of this lesson, you should be able to:

* import and use Python's `random` module
* store a secret number in a variable
* ask the user for guesses with `input()`
* convert input text into a number with `int()`
* compare a guess with the secret number
* use `if`, `elif`, and `else` to give feedback
* use a `while` loop to keep the game running
* stop the loop when the player wins or attempts run out
* validate input before converting it
* test the game with planned guesses
* debug common number guessing game mistakes

This is the third mini-project in the course.

The goal is not to make a large game. The goal is to combine the loop tools from Days 21-29 into one small program that feels complete.

## The Project

Create this file:

```text
day-30/number_guessing_game.py
```

The program will:

* welcome the player
* choose a random number from `1` to `10`
* give the player `5` attempts
* ask for one guess at a time
* check that the guess is a number
* convert the guess from text to an integer
* say whether the guess is too low, too high, or correct
* stop when the player guesses correctly
* stop when the attempts run out
* print a final result

Example:

```text
Welcome to the number guessing game.
I am thinking of a number from 1 to 10.
You have 5 guesses.

Your guess: 4
Too low.
Guesses left: 4

Your guess: 8
Too high.
Guesses left: 3

Your guess: 6
Correct.
You won in 3 guesses.
Thanks for playing.
```

The exact winning number will change because the program uses randomness.

This game has a classic loop shape:

```text
choose secret number
while the game is still going:
    ask for a guess
    check the guess
    update the game state
print the result
```

The loop is the center of the project.

## The Big Idea

A number guessing game is a repeated decision program.

Each round asks:

```text
Is this guess correct?
```

If the guess is correct, the game ends.

If the guess is too low, the program gives a hint.

If the guess is too high, the program gives a different hint.

That becomes an `if` / `elif` / `else` block:

```python
if guess == secret_number:
    print("Correct.")
elif guess < secret_number:
    print("Too low.")
else:
    print("Too high.")
```

The game also needs to remember how many guesses have been used:

```python
attempts = attempts + 1
```

And it needs a clear reason to stop:

```text
The player guessed correctly.
or
The player used all attempts.
```

That is why the main loop will use this condition:

```python
while attempts < max_attempts and not game_won:
```

Read it as:

```text
Keep playing while there are attempts left and the game has not been won.
```

The game is built from tools you already know. The new work is putting them together carefully.

## The Mental Model

Think of the game as a small referee.

The referee remembers:

```text
secret_number
max_attempts
attempts
game_won
```

Each round, the referee does five jobs:

```text
1. Ask for a guess.
2. Make sure the guess can become a number.
3. Convert the guess from text to a number.
4. Compare the guess with the secret number.
5. Decide whether the game should continue.
```

The conversion step matters because `input()` always gives you text.

Code:

```python
guess_text = input("Your guess: ")
```

If the player types `7`, Python stores it as the string `"7"`, not the number `7`.

That means this is text:

```text
"7"
```

This is a number:

```text
7
```

They look similar on the screen, but Python treats them differently.

If you want to compare the guess as a number, convert it:

```python
guess = int(guess_text)
```

Then number comparisons make sense:

```python
if guess < secret_number:
    print("Too low.")
```

But `int()` needs number-like text.

This works:

```text
int("7")
```

This does not:

```text
int("seven")
```

If a player types a word, Python raises an error. You have not studied exception handling yet, so today's program will check the text before calling `int()`.

The safety pattern is:

```text
ask for text
while the text is not digits:
    explain the problem
    ask again
convert the safe text with int()
```

That lets the game stay friendly without needing advanced error handling.

## Step-by-Step Build

Build the game in stages.

Do not start with the full program. A game is easier to trust when each small part works before you add the next one.

### Step 1: Create the File

Create this file:

```text
day-30/number_guessing_game.py
```

Code:

```python
print("Welcome to the number guessing game.")
print("I am thinking of a number from 1 to 10.")
```

Run it from your course folder:

```bash
python day-30/number_guessing_game.py
```

If your computer uses `py`, use:

```bash
py day-30/number_guessing_game.py
```

If your computer uses `python3`, use:

```bash
python3 day-30/number_guessing_game.py
```

You should see:

```text
Welcome to the number guessing game.
I am thinking of a number from 1 to 10.
```

The file runs. That is the first checkpoint.

### Step 2: Choose a Secret Number

Python has a module named `random`.

A module is code Python already has available for you to use. To use it, import it:

```python
import random
```

Now ask for a random integer from `1` to `10`:

```python
secret_number = random.randint(1, 10)
```

Code:

```python
import random

secret_number = random.randint(1, 10)

print("Welcome to the number guessing game.")
print("I am thinking of a number from 1 to 10.")
print("Secret number made.")
```

Run it a few times.

You should see:

```text
Welcome to the number guessing game.
I am thinking of a number from 1 to 10.
Secret number made.
```

The secret number is not printed. A real guessing game should keep it hidden.

While testing, though, it is sometimes useful to print the secret number temporarily:

```python
print("Debug secret:", secret_number)
```

Remove that debug line when the game works.

### Step 3: Ask for One Guess

Now ask the player for one guess.

Code:

```python
guess_text = input("Your guess: ")
print("You typed:", guess_text)
```

Try this:

```text
7
```

You should see:

```text
Your guess: 7
You typed: 7
```

At this point, the guess is still text.

That means this line stores a string:

```python
guess_text = input("Your guess: ")
```

The name `guess_text` is deliberate. It reminds you that the value came from `input()` and has not been converted yet.

### Step 4: Convert Text to a Number

To compare a guess with the secret number, convert the input text:

```python
guess = int(guess_text)
```

Code:

```python
guess_text = input("Your guess: ")
guess = int(guess_text)

print("You guessed the number", guess)
print("One more than your guess is", guess + 1)
```

Try this:

```text
7
```

You should see:

```text
Your guess: 7
You guessed the number 7
One more than your guess is 8
```

The last line proves that `guess` is a number. Python can add `1` to it.

Now try this only if you are ready to see the error:

```text
seven
```

Python will complain because `"seven"` cannot be converted with `int()`.

That is why the final game will validate the input before converting it.

### Step 5: Compare the Guess

Use a fixed secret number for this stage. That makes testing easier.

Code:

```python
secret_number = 6

guess_text = input("Your guess: ")
guess = int(guess_text)

if guess == secret_number:
    print("Correct.")
elif guess < secret_number:
    print("Too low.")
else:
    print("Too high.")
```

Try these inputs one at a time:

| Input | You should see |
| --- | --- |
| `6` | `Correct.` |
| `3` | `Too low.` |
| `9` | `Too high.` |

This is the decision part of the game.

The comparison operators do the work:

```text
==   equal to
<    less than
>    greater than
```

The `else` branch does not need to check `guess > secret_number` because only three useful cases exist:

```text
correct
too low
too high
```

If the first two cases are false, the guess must be too high.

### Step 6: Keep Guessing with a `while` Loop

Now repeat the guessing until the player gets the number.

Code:

```python
secret_number = 6
guess = 0

while guess != secret_number:
    guess_text = input("Your guess: ")
    guess = int(guess_text)

    if guess == secret_number:
        print("Correct.")
    elif guess < secret_number:
        print("Too low.")
    else:
        print("Too high.")

print("Game over.")
```

Try this:

```text
2
9
6
```

You should see:

```text
Your guess: 2
Too low.
Your guess: 9
Too high.
Your guess: 6
Correct.
Game over.
```

The loop condition is:

```python
while guess != secret_number:
```

At the start, `guess` is `0`, so the loop runs.

After each guess, the value of `guess` changes.

When `guess` becomes the secret number, the condition becomes false and the loop stops.

This is the same loop safety idea from earlier lessons:

```text
What condition keeps the loop running?
What value changes inside the loop?
What makes the condition false?
```

### Step 7: Add an Attempt Limit

A real game should not always run forever. Give the player a limited number of guesses.

Code:

```python
secret_number = 6
max_attempts = 5
attempts = 0
game_won = False

while attempts < max_attempts and not game_won:
    guess_text = input("Your guess: ")
    guess = int(guess_text)
    attempts = attempts + 1

    if guess == secret_number:
        print("Correct.")
        game_won = True
    elif guess < secret_number:
        print("Too low.")
    else:
        print("Too high.")

if game_won:
    print("You won in", attempts, "guesses.")
else:
    print("Out of guesses.")
```

This loop has two exit paths:

```text
attempts reaches max_attempts
game_won becomes True
```

The condition says both things must be true for another round to happen:

```python
while attempts < max_attempts and not game_won:
```

Read it carefully:

```text
Keep going while attempts are still available
and
the game has not been won.
```

This is one of the most important lines in the project.

### Step 8: Show Guesses Left

After each wrong guess, show how many guesses remain.

Code:

```python
secret_number = 6
max_attempts = 5
attempts = 0
game_won = False

while attempts < max_attempts and not game_won:
    guess_text = input("Your guess: ")
    guess = int(guess_text)
    attempts = attempts + 1

    if guess == secret_number:
        print("Correct.")
        game_won = True
    elif guess < secret_number:
        print("Too low.")
    else:
        print("Too high.")

    guesses_left = max_attempts - attempts

    if not game_won and guesses_left > 0:
        print("Guesses left:", guesses_left)

if game_won:
    print("You won in", attempts, "guesses.")
else:
    print("Out of guesses.")
```

The game calculates guesses left after counting the current attempt:

```python
guesses_left = max_attempts - attempts
```

If the player wins, the program does not need to print guesses left.

If no guesses are left, the program does not need to print:

```text
Guesses left: 0
```

That is why the condition checks both:

```python
if not game_won and guesses_left > 0:
```

### Step 9: Validate Before `int()`

Now make the game safer.

The problem is this line:

```python
guess = int(guess_text)
```

It works only when `guess_text` contains digits.

Use `.isdigit()` to check before converting:

```python
guess_text = input("Your guess: ").strip()

while not guess_text.isdigit():
    print("Please type a whole number, like 4.")
    guess_text = input("Your guess: ").strip()

guess = int(guess_text)
```

Code:

```python
guess_text = input("Your guess: ").strip()

while not guess_text.isdigit():
    print("Please type a whole number, like 4.")
    guess_text = input("Your guess: ").strip()

guess = int(guess_text)
print("Number guess:", guess)
```

Try this:

```text
apple
7
```

You should see:

```text
Your guess: apple
Please type a whole number, like 4.
Your guess: 7
Number guess: 7
```

The word `apple` does not become an attempt in the final game. It is rejected before conversion.

This is beginner-safe input handling:

```text
Do not call int() until the text looks like a number.
```

### Step 10: Put It Together

Here is the complete program:

```python
import random

secret_number = random.randint(1, 10)
max_attempts = 5
attempts = 0
game_won = False

print("Welcome to the number guessing game.")
print("I am thinking of a number from 1 to 10.")
print("You have", max_attempts, "guesses.")

print("")

while attempts < max_attempts and not game_won:
    valid_guess = False
    guess = 0

    while not valid_guess:
        guess_text = input("Your guess: ").strip()

        if not guess_text.isdigit():
            print("Please type a whole number, like 4.")
        else:
            guess = int(guess_text)

            if guess < 1 or guess > 10:
                print("Please choose a number from 1 to 10.")
            else:
                valid_guess = True

    attempts = attempts + 1

    if guess == secret_number:
        print("Correct.")
        game_won = True
    elif guess < secret_number:
        print("Too low.")
    else:
        print("Too high.")

    guesses_left = max_attempts - attempts

    if not game_won and guesses_left > 0:
        print("Guesses left:", guesses_left)

    print("")

if game_won:
    print("You won in", attempts, "guesses.")
else:
    print("Out of guesses. The number was", secret_number)

print("Thanks for playing.")
```

Run the program several times.

Try a normal game:

```text
5
8
6
```

Try invalid input:

```text
hello
3
```

Try an out-of-range number:

```text
15
4
```

Try losing on purpose:

```text
1
1
1
1
1
```

When you test, check more than whether the program crashes.

Also ask:

* Does a word get rejected before `int()`?
* Does an out-of-range number get rejected?
* Does a valid guess count as one attempt?
* Does an invalid guess avoid using an attempt?
* Does the game stop after a correct guess?
* Does the game stop after `5` valid guesses?
* Does the final message match the result?

That is how you test a small game with confidence.

## Try It Yourself

Make the game your own.

Start with small changes:

* change the range from `1` through `10` to `1` through `20`
* change `max_attempts` from `5` to `6`
* change the welcome message
* print a different message when the player wins
* print a different message when the player loses

When you change the range, update every place that mentions it.

For example, if the secret number is from `1` to `20`, this line should change:

```python
secret_number = random.randint(1, 20)
```

This message should change too:

```python
print("I am thinking of a number from 1 to 20.")
```

And this validation check should change:

```python
if guess < 1 or guess > 20:
```

Those three pieces are connected.

Try this: add a debug mode while testing.

Code:

```python
debug_mode = True

if debug_mode:
    print("Debug secret:", secret_number)
```

When `debug_mode` is `True`, you can see the answer and test winning paths quickly.

When the game is ready, change it to:

```python
debug_mode = False
```

Do not leave the secret number visible in the finished game.

## Common Mistake

### Mistake 1: Comparing Text to a Number

Broken code:

```python
secret_number = 6
guess = input("Your guess: ")

if guess == secret_number:
    print("Correct.")
else:
    print("Not correct.")
```

If the player types `6`, the program still prints:

```text
Not correct.
```

The problem is that `guess` is text and `secret_number` is a number.

This comparison is really:

```text
"6" == 6
```

Those are not the same value.

Fixed code:

```python
secret_number = 6
guess_text = input("Your guess: ")
guess = int(guess_text)

if guess == secret_number:
    print("Correct.")
else:
    print("Not correct.")
```

Convert the input before using number comparisons.

### Mistake 2: Calling `int()` Too Soon

Broken code:

```python
guess_text = input("Your guess: ")
guess = int(guess_text)

if guess < 1 or guess > 10:
    print("Please choose a number from 1 to 10.")
```

If the player types:

```text
apple
```

the program crashes before it reaches the range check.

The problem is that `"apple"` cannot become an integer.

Fixed code:

```python
guess_text = input("Your guess: ").strip()

while not guess_text.isdigit():
    print("Please type a whole number, like 4.")
    guess_text = input("Your guess: ").strip()

guess = int(guess_text)

if guess < 1 or guess > 10:
    print("Please choose a number from 1 to 10.")
```

Check whether the text is digits before calling `int()`.

### Mistake 3: Forgetting to Count Attempts

Broken code:

```python
secret_number = 6
max_attempts = 5
attempts = 0
game_won = False

while attempts < max_attempts and not game_won:
    guess = int(input("Your guess: "))

    if guess == secret_number:
        game_won = True
        print("Correct.")
    else:
        print("Try again.")
```

If the guesses are wrong, this loop does not stop after `5` attempts.

The condition checks `attempts`, but `attempts` never changes.

Fixed code:

```python
secret_number = 6
max_attempts = 5
attempts = 0
game_won = False

while attempts < max_attempts and not game_won:
    guess = int(input("Your guess: "))
    attempts = attempts + 1

    if guess == secret_number:
        game_won = True
        print("Correct.")
    else:
        print("Try again.")
```

The attempt counter must change inside the loop.

### Mistake 4: Using `or` Incorrectly in a Range Check

Broken code:

```python
guess = 4

if guess < 1 and guess > 10:
    print("Out of range.")
```

This condition can never be true.

A number cannot be less than `1` and greater than `10` at the same time.

Fixed code:

```python
guess = 4

if guess < 1 or guess > 10:
    print("Out of range.")
```

Use `or` because either problem should count:

```text
too small
or
too large
```

## Debug It

Debugging this game usually means watching the values that control the loop.

The examples in this section are supposed to have bugs. Read them before looking at the fixes.

### Bug 1: The Game Stops After One Wrong Guess

Broken code:

```python
secret_number = 6
game_won = False

while not game_won:
    guess = int(input("Your guess: "))

    if guess == secret_number:
        print("Correct.")
    else:
        print("Wrong.")

    game_won = True
```

The problem is this line:

```python
game_won = True
```

It runs after every guess, even wrong guesses.

Fixed code:

```python
secret_number = 6
game_won = False

while not game_won:
    guess = int(input("Your guess: "))

    if guess == secret_number:
        print("Correct.")
        game_won = True
    else:
        print("Wrong.")
```

Only set `game_won` to `True` inside the correct-answer branch.

### Bug 2: Invalid Guesses Use Up Attempts

Broken code:

```python
attempts = 0
max_attempts = 5

guess_text = input("Your guess: ").strip()
attempts = attempts + 1

while not guess_text.isdigit():
    print("Please type a whole number.")
    guess_text = input("Your guess: ").strip()
    attempts = attempts + 1

print("Attempts:", attempts)
```

Try this:

```text
apple
banana
4
```

The program counts `3` attempts, even though only one usable number was entered.

If invalid input should not cost an attempt, count the attempt after validation.

Fixed code:

```python
attempts = 0
max_attempts = 5

guess_text = input("Your guess: ").strip()

while not guess_text.isdigit():
    print("Please type a whole number.")
    guess_text = input("Your guess: ").strip()

guess = int(guess_text)
attempts = attempts + 1

print("Guess:", guess)
print("Attempts:", attempts)
```

Ask this debugging question:

```text
Which inputs should count as real attempts?
```

Then place the counter update after the answer is accepted.

### Bug 3: The Loop Condition Is Hard to Trust

Broken code:

```python
attempts = 0
max_attempts = 5
game_won = False

while attempts < max_attempts or not game_won:
    guess = int(input("Your guess: "))
    attempts = attempts + 1

    if guess == 6:
        game_won = True
```

The condition uses `or`:

```python
while attempts < max_attempts or not game_won:
```

That means the loop keeps running if either side is true.

After `5` wrong attempts, this part is false:

```text
attempts < max_attempts
```

But this part is still true:

```text
not game_won
```

So the loop keeps going.

Fixed code:

```python
attempts = 0
max_attempts = 5
game_won = False

while attempts < max_attempts and not game_won:
    guess = int(input("Your guess: "))
    attempts = attempts + 1

    if guess == 6:
        game_won = True
```

Use `and` because both requirements must be true:

```text
There are attempts left.
The game has not been won.
```

### Bug 4: The Secret Number Keeps Changing

Broken code:

```python
import random

game_won = False

while not game_won:
    secret_number = random.randint(1, 10)
    guess = int(input("Your guess: "))

    if guess == secret_number:
        print("Correct.")
        game_won = True
    else:
        print("Wrong. The number was", secret_number)
```

The secret number changes on every loop round.

That makes the game feel unfair because the player is not trying to find one stable answer.

Fixed code:

```python
import random

secret_number = random.randint(1, 10)
game_won = False

while not game_won:
    guess = int(input("Your guess: "))

    if guess == secret_number:
        print("Correct.")
        game_won = True
    else:
        print("Wrong.")
```

Choose the secret number before the loop so it stays the same for the whole game.

Debug tip:

```python
print("Debug secret:", secret_number)
```

Use that line temporarily if you need to check whether the secret is changing.

Remove it when you are done debugging.

## Read the Docs

Today, look up the documentation for `random.randint()`:

```text
https://docs.python.org/3/library/random.html#random.randint
```

The important part is that both ends are included.

This code:

```python
random.randint(1, 10)
```

can return:

```text
1, 2, 3, 4, 5, 6, 7, 8, 9, or 10
```

That is different from `range(1, 10)`, which stops before `10`.

You can also look up:

```text
https://docs.python.org/3/library/functions.html#int
https://docs.python.org/3/library/stdtypes.html#str.isdigit
```

For today, remember:

* `int()` converts number-like text into an integer
* `.isdigit()` asks whether a string contains only digit characters
* `random.randint(a, b)` returns a random integer from `a` through `b`

Try this small file:

```python
import random

print(random.randint(1, 3))
print(random.randint(1, 3))
print(random.randint(1, 3))
```

Run it several times.

You should see numbers from `1` through `3`. The exact order can change each time.

## Mini Challenge

Create this file:

```text
day-30/bonus_guessing_game.py
```

Build a second version of the game with one extra feature.

Choose one:

* Easy mode: numbers from `1` to `10`, `5` guesses
* Medium mode: numbers from `1` to `20`, `6` guesses
* Hard mode: numbers from `1` to `50`, `7` guesses

Start with one mode written directly in code:

```python
largest_number = 20
max_attempts = 6
secret_number = random.randint(1, largest_number)
```

Then use `largest_number` in your messages and validation:

```python
print("I am thinking of a number from 1 to", largest_number)
```

```python
if guess < 1 or guess > largest_number:
    print("Please choose a number from 1 to", largest_number)
```

This is a useful improvement because the number range lives in one variable.

If you change:

```python
largest_number = 50
```

the rest of the program can use that value.

That habit prepares you for larger programs where repeated facts should not be scattered everywhere.

## Real-World Use

Number guessing games are small, but the logic appears in many real programs.

Examples:

* a login screen counts attempts
* a quiz app checks whether an answer is correct
* a game gives hints based on player input
* a form rejects invalid input before saving it
* a setup wizard keeps asking until the choice is allowed
* a command-line tool keeps running until the task is complete

The project uses several common patterns:

```text
generate a value
ask for input
validate the input
convert the input
compare values
repeat until done
show a final result
```

Those patterns are not only for games. They are part of many small useful programs.

## Recap

Today you built a complete number guessing game.

You practiced:

* importing `random`
* using `random.randint()`
* storing game state in variables
* collecting input with `input()`
* remembering that input starts as text
* validating text before converting it
* converting with `int()`
* comparing numbers with `==`, `<`, and `>`
* using `if`, `elif`, and `else` for feedback
* using a `while` loop for repeated guesses
* counting attempts
* using a boolean flag named `game_won`
* writing a loop condition with two exit paths
* testing valid, invalid, winning, and losing runs
* using temporary debug prints

The main idea:

> A game loop keeps running while the game is not finished, and each round must move the game closer to an ending.

## Lesson Checklist

Before moving on, check that you can:

* create and run `day-30/number_guessing_game.py`
* explain why `input()` gives text
* explain why `int()` is needed before number comparisons
* explain why `"7"` and `7` are different values
* use `.isdigit()` to reject non-number text before conversion
* create a random secret number with `random.randint()`
* compare a guess with the secret number
* give different feedback for low, high, and correct guesses
* count valid attempts
* write a loop that stops after a win
* write a loop that stops when attempts run out
* use temporary debug prints without leaving them in the final game

## Exercises

### Exercise 1

Create this file:

```text
day-30/one_guess.py
```

Write a one-guess version of the game.

Requirements:

* set `secret_number = 6`
* ask for one guess
* convert the guess with `int()`
* print `Correct.`, `Too low.`, or `Too high.`

### Exercise 2

Fix this program.

Broken code:

```python
secret_number = 5
guess = input("Your guess: ")

if guess == secret_number:
    print("Correct.")
```

The program should treat the user's guess as a number.

### Exercise 3

Write a validation loop.

Ask for a guess until the user types digits.

Start with:

```python
guess_text = input("Your guess: ").strip()
```

Use:

```python
while not guess_text.isdigit():
```

When the input is valid, convert it and print the number.

### Exercise 4

Fix the attempt counter.

Broken code:

```python
attempts = 0
max_attempts = 3

while attempts < max_attempts:
    guess = int(input("Guess: "))
    print("You guessed", guess)
```

The loop should stop after `3` guesses.

### Exercise 5

Write a loop condition for this rule:

```text
Keep playing while attempts are less than max_attempts and the game has not been won.
```

Use these variables:

```python
attempts = 0
max_attempts = 5
game_won = False
```

### Exercise 6

Add a debug print to your game:

```python
print("Debug secret:", secret_number)
```

Use it to test one winning game quickly.

Then remove the debug print or guard it with:

```python
debug_mode = False
```

### Exercise 7

Change the game so the secret number is from `1` to `20`.

Update:

* the `random.randint()` line
* the welcome message
* the out-of-range validation

Run the game and test:

```text
0
21
10
```

The first two should be rejected as out of range.

### Exercise 8

Make invalid input not count as an attempt.

Test with:

```text
apple
banana
4
```

Only `4` should count as a real guess.

### Exercise 9

Add a message for the final guess.

If the player is wrong and has no guesses left, print:

```text
No guesses left.
```

Do not print:

```text
Guesses left: 0
```

### Exercise 10

Write down three test runs before running the game.

Include:

* a winning run
* a losing run
* a run with invalid input

For each one, write:

```text
Inputs:
What should happen:
What actually happened:
```

If the result is different from what you expected, debug one value at a time.

## Tiny Win

You built a complete loop-based game.

It chooses a secret value, accepts user input, protects the conversion step, gives hints, tracks attempts, and ends cleanly.

That is a solid project shape. You can reuse the same structure in menus, quizzes, password checks, setup prompts, and small command-line tools.

## Tomorrow

Tomorrow you begin lists.

The next lesson is:

```text
Day 31: Lists
```

So far, when a program needed several values, you often wrote separate variables:

```python
guess_one = 4
guess_two = 8
guess_three = 6
```

A list lets one variable hold many related values:

```python
guesses = [4, 8, 6]
```

That will make programs like this guessing game easier to improve.

For example, a future version could remember every guess the player made and print them at the end.

That is exactly the kind of problem lists are built to solve.
