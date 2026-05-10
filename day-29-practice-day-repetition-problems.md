# Day 29: Practice Day: Repetition Problems

**Focus:** Solving small problems with loops and loop patterns  
**You will practice:** `while` loops, `for` loops, `range()`, looping through text, `break`, `continue`, counters, totals, searches, input loops, and debugging repetition mistakes  
**Estimated time:** 60-75 minutes

## Today's Goal

Today is a practice day.

You are not learning a new loop keyword. You are using the repetition tools you already know:

- `while` loops
- safe stopping conditions
- `for` loops
- `range()`
- looping through text
- `break`
- `continue`
- counters, totals, searches, and input validation

By the end of this lesson, you should be able to:

- choose between a `while` loop and a `for` loop
- use `range()` when a loop needs numbers
- loop through text one character at a time
- use `break` when a loop should stop early
- use `continue` when one loop turn should be skipped
- keep a counter, total, or flag in the right place
- test loops with more than one case
- prepare for tomorrow's number guessing game

The goal is not to write every loop perfectly the first time.

The goal is to practice reading the problem, choosing a loop pattern, and checking whether the loop stops for the right reason.

## The Big Idea

Most loop problems are built from a few familiar questions:

```text
How many times should this repeat?
Do I already have the items to loop through?
What value changes each time?
What should make the loop stop?
Should one turn be skipped?
Should the whole loop stop early?
What value needs to be remembered after the loop?
```

A practice day is a good time to slow down and answer those questions before writing code.

Example:

```text
Ask the user to guess a secret number.
Keep asking until the guess is correct.
Count how many guesses it takes.
```

That problem suggests a `while` loop because you do not know how many guesses the user will need.

The remembered value is:

```text
attempts
```

The stopping point is:

```text
the guess matches the secret number
```

Code:

```python
secret = "7"
guess = ""
attempts = 0

while guess != secret:
    guess = input("Guess: ")
    attempts = attempts + 1

print("Correct.")
print("Attempts:", attempts)
```

This is already close to tomorrow's mini project.

Today you will practice the smaller pieces so the project feels less mysterious.

## The Mental Model

Before writing a loop, identify the loop shape.

Use a `while` loop when the program should repeat until a condition changes.

```python
answer = ""

while answer != "yes":
    answer = input("Type yes: ")

print("Thanks.")
```

Use a `for` loop when the program already has a sequence to move through.

```python
for letter in "loop":
    print(letter)
```

Use `range()` when the loop needs a controlled set of numbers.

```python
for number in range(1, 4):
    print("Round", number)
```

Use a carried value when the loop needs to remember something.

```python
word = "banana"
count = 0

for letter in word:
    if letter == "a":
        count = count + 1

print("Letter a:", count)
```

The carried value might be:

- a counter, such as `count`
- a total, such as `total`
- a flag, such as `found`
- a growing string, such as `result`
- the latest input, such as `guess` or `choice`

When a loop feels confusing, do not start with syntax. Start with this:

```text
What repeats?
What changes?
What is remembered?
What stops the loop?
```

Those four questions are enough to start most beginner loop problems.

## Warm-Up

For each warm-up, predict the output before running the code.

### Warm-Up 1

Code:

```python
count = 1

while count <= 3:
    print("Count:", count)
    count = count + 1

print("Done")
```

You should see:

```text
Count: 1
Count: 2
Count: 3
Done
```

Debugging prompt:

```text
Which line moves the loop toward stopping?
```

### Warm-Up 2

Code:

```python
for number in range(2, 9, 2):
    print(number)
```

You should see:

```text
2
4
6
8
```

Debugging prompt:

```text
Where does the range start?
What value does it stop before?
What is the step?
```

### Warm-Up 3

Code:

```python
word = "Python"

for letter in word:
    print(letter.lower())
```

You should see:

```text
p
y
t
h
o
n
```

Debugging prompt:

```text
What does the loop variable hold on each turn?
```

### Warm-Up 4

Code:

```python
for number in range(1, 6):
    if number == 3:
        continue

    print(number)
```

You should see:

```text
1
2
4
5
```

Debugging prompt:

```text
Does continue stop the whole loop, or only skip one turn?
```

### Warm-Up 5

Code:

```python
for letter in "desk":
    if letter == "s":
        break

    print(letter)

print("After loop")
```

You should see:

```text
d
e
After loop
```

Debugging prompt:

```text
Which line runs immediately after break leaves the loop?
```

## Practice Problems

Use this rhythm for each problem:

```text
Read the goal.
Name the loop pattern.
Write a small version.
Predict the output.
Run the code.
Test one more case.
Fix one small thing at a time.
```

### Practice Problem 1: Count Practice Rounds

Create a file named `day-29/count_practice_rounds.py`.

Write a program that prints five practice rounds.

Rules:

```text
Print "Practice round 1" through "Practice round 5".
After the loop, print "Practice complete."
```

Hint:

```text
This is a range() problem.
```

Code:

```python
for round_number in range(1, 6):
    print("Practice round", round_number)

print("Practice complete.")
```

You should see:

```text
Practice round 1
Practice round 2
Practice round 3
Practice round 4
Practice round 5
Practice complete.
```

If round `5` does not appear, check the stop value.

Question to answer:

```text
Why is the stop value 6 instead of 5?
```

### Practice Problem 2: Add Small Scores

Create a file named `day-29/score_total.py`.

Write a program that adds a few scores.

Start with:

```python
scores = [3, 5, 2, 4]
```

Rules:

```text
Start total at 0.
Add each score to total.
Print the final total after the loop.
```

Hint:

```text
This is the accumulating pattern.
```

Code:

```python
scores = [3, 5, 2, 4]
total = 0

for score in scores:
    total = total + score

print("Total score:", total)
```

You should see:

```text
Total score: 14
```

If the total prints several times, check whether the final `print()` line is inside the loop.

If the answer is too high, check the starting value of `total`.

### Practice Problem 3: Count Vowels

Create a file named `day-29/count_vowels.py`.

Write a program that counts vowels in a word.

Start with:

```python
word = "repetition"
```

Rules:

```text
Treat a, e, i, o, and u as vowels.
Count lowercase and uppercase vowels the same way.
Print the final count.
```

Hint:

```text
Loop through the text one character at a time.
Use .lower() before checking the vowel.
```

Code:

```python
word = "repetition"
vowels = "aeiou"
vowel_count = 0

for letter in word:
    if letter.lower() in vowels:
        vowel_count = vowel_count + 1

print("Vowels:", vowel_count)
```

You should see:

```text
Vowels: 5
```

Try this:

```python
word = "Education"
```

The program should count uppercase `"E"` as a vowel too.

### Practice Problem 4: Find A Letter

Create a file named `day-29/find_letter.py`.

Write a program that searches for the first `"x"` in a word.

Start with:

```python
word = "boxcar"
```

Rules:

```text
Loop through the word.
If the letter is "x", remember that it was found.
Stop searching once it is found.
After the loop, print whether x was found.
```

Hint:

```text
This is the searching pattern.
Use a boolean flag and break.
```

Code:

```python
word = "boxcar"
found_x = False

for letter in word:
    if letter == "x":
        found_x = True
        break

if found_x:
    print("Found x.")
else:
    print("No x found.")
```

You should see:

```text
Found x.
```

Try this:

```python
word = "banana"
```

This time the program should print:

```text
No x found.
```

Debugging prompt:

```text
What value does found_x have before the loop?
What value should it have after x is found?
```

### Practice Problem 5: Skip Blank Names

Create a file named `day-29/name_list.py`.

Write a program that loops through a short list of names and skips blank entries.

Start with:

```python
names = ["Asha", "", "Ben", "Cara", ""]
```

Rules:

```text
Print a greeting for each real name.
Skip empty strings.
After the loop, print "Done."
```

Hint:

```text
Use continue when one loop turn should be ignored.
```

Code:

```python
names = ["Asha", "", "Ben", "Cara", ""]

for name in names:
    if name == "":
        continue

    print("Hello,", name)

print("Done.")
```

You should see:

```text
Hello, Asha
Hello, Ben
Hello, Cara
Done.
```

Question to answer:

```text
Why is continue better than break here?
```

### Practice Problem 6: Keep Asking Until Yes

Create a file named `day-29/yes_loop.py`.

Write a program that keeps asking until the user types `"yes"`.

Rules:

```text
Ask the user to type yes.
If the answer is not yes, ask again.
When the answer is yes, print "Accepted."
```

Hint:

```text
This is a validation loop.
Use a while loop because you do not know how many tries the user will need.
```

Code:

```python
answer = input("Type yes: ").strip().lower()

while answer != "yes":
    print("Please type yes.")
    answer = input("Type yes: ").strip().lower()

print("Accepted.")
```

Try this:

```text
no
maybe
yes
```

The program should reject the first two answers and accept the third.

Debugging prompt:

```text
Where does answer change inside the loop?
```

### Practice Problem 7: Guess With Attempts

Create a file named `day-29/guess_with_attempts.py`.

Write a small guessing loop. This is a preview of tomorrow's project.

Rules:

```text
Store a secret number as text.
Ask the user to guess.
Keep asking while the guess is wrong.
Count each guess.
When the guess is correct, print the number of attempts.
```

Code:

```python
secret = "7"
guess = ""
attempts = 0

while guess != secret:
    guess = input("Guess the number: ").strip()
    attempts = attempts + 1

    if guess != secret:
        print("Try again.")

print("Correct.")
print("Attempts:", attempts)
```

Try this:

```text
3
8
7
```

The program should say `"Try again."` twice, then print:

```text
Correct.
Attempts: 3
```

Question to answer:

```text
Why does attempts start at 0?
Why does attempts increase inside the loop?
```

## Try It Yourself

Now choose one of these problems and write it without looking back at the earlier code first.

### Option A: Countdown

Create a file named `day-29/countdown_review.py`.

Rules:

```text
Ask the user for a starting number.
Count down from that number to 1.
Print "Go!" after the loop.
```

Hint:

```text
Use int(input(...)) for the starting number.
Use range(start, 0, -1).
```

Example behavior:

```text
Start: 4
4
3
2
1
Go!
```

### Option B: Password Checker

Create a file named `day-29/password_checker.py`.

Rules:

```text
Ask for a password.
Keep asking while the password is wrong.
Stop when the user types the correct password.
Count the number of attempts.
```

Use:

```python
correct_password = "loops"
```

Hint:

```text
This is very similar to the guessing loop.
The secret is a word instead of a number.
```

Example behavior:

```text
Password: hello
Wrong password.
Password: loops
Welcome.
Attempts: 2
```

### Option C: Text Cleaner

Create a file named `day-29/text_cleaner.py`.

Rules:

```text
Ask the user for a sentence.
Build a new string that skips spaces.
Print the cleaned string.
```

Hint:

```text
Start cleaned as an empty string.
Loop through each character.
Use continue when the character is a space.
Otherwise, add the character to cleaned.
```

Example behavior:

```text
Sentence: loop practice day
looppracticeday
```

Choose the option that feels slightly uncomfortable, not impossible.

That is a good practice target.

## Common Mistake

Practice days are good days to notice habits that cause loop bugs.

### Mistake 1: Resetting the counter inside the loop

Broken code:

```python
word = "banana"

for letter in word:
    count = 0

    if letter == "a":
        count = count + 1

print("Letter a:", count)
```

This prints the wrong answer because `count` starts over on every loop turn.

Fixed code:

```python
word = "banana"
count = 0

for letter in word:
    if letter == "a":
        count = count + 1

print("Letter a:", count)
```

You should see:

```text
Letter a: 3
```

Rule to remember:

```text
Create the carried value before the loop.
Update it inside the loop.
Use it after the loop.
```

### Mistake 2: Forgetting to ask again

Broken code:

```python
answer = input("Type yes: ")

while answer != "yes":
    print("Please type yes.")
```

If the first answer is not `"yes"`, this loop cannot recover. The value of `answer` never changes.

Fixed code:

```python
answer = input("Type yes: ")

while answer != "yes":
    print("Please type yes.")
    answer = input("Type yes: ")
```

Rule to remember:

```text
An input loop must give the user another chance inside the loop.
```

### Mistake 3: Printing the final result too early

This code prints the running total:

```python
total = 0

for number in range(1, 4):
    total = total + number
    print("Total:", total)
```

You should see:

```text
Total: 1
Total: 3
Total: 6
```

That can help while debugging, but it is not one final report.

Fixed code:

```python
total = 0

for number in range(1, 4):
    total = total + number

print("Total:", total)
```

You should see:

```text
Total: 6
```

Question to ask:

```text
Should this line run every time, or once after the loop?
```

### Mistake 4: Using `break` when you meant `continue`

Broken code:

```python
names = ["Asha", "", "Ben"]

for name in names:
    if name == "":
        break

    print(name)
```

This stops at the blank name and never reaches `"Ben"`.

Fixed code:

```python
names = ["Asha", "", "Ben"]

for name in names:
    if name == "":
        continue

    print(name)
```

You should see:

```text
Asha
Ben
```

Use `continue` when one item should be ignored.

Use `break` when the whole loop should end.

## Debug It

These programs are intentionally broken. Read the goal first, predict what the broken code does, then study the fix.

### Debug It 1: Attempt Counter

Goal:

```text
Ask for the secret word.
Keep asking until the user types "python".
Count every attempt.
```

Broken code:

```python
guess = ""

while guess != "python":
    attempts = 0
    guess = input("Secret word: ")
    attempts = attempts + 1

print("Attempts:", attempts)
```

The problem is that `attempts` resets to `0` on every loop turn.

Fixed code:

```python
guess = ""
attempts = 0

while guess != "python":
    guess = input("Secret word: ")
    attempts = attempts + 1

print("Attempts:", attempts)
```

Try this input:

```text
java
python
```

The program should print:

```text
Attempts: 2
```

Debugging prompt:

```text
Which value needs to remember earlier loop turns?
Where should that value be created?
```

### Debug It 2: Countdown Direction

Goal:

```text
Print 5, 4, 3, 2, 1, then "Go!"
```

Broken code:

```python
number = 5

while number > 0:
    print(number)
    number = number + 1

print("Go!")
```

The update moves away from the stopping point.

Fixed code:

```python
number = 5

while number > 0:
    print(number)
    number = number - 1

print("Go!")
```

You should see:

```text
5
4
3
2
1
Go!
```

Debugging prompt:

```text
Is the update moving the value toward making the condition false?
```

### Debug It 3: Continue Skips The Update

Goal:

```text
Print 1, 2, 4, 5.
Skip 3.
Stop after 5.
```

Broken code:

```python
number = 1

while number <= 5:
    if number == 3:
        continue

    print(number)
    number = number + 1
```

Do not run that version. When `number` becomes `3`, `continue` skips the update, so `number` stays `3`.

Fixed code:

```python
number = 0

while number < 5:
    number = number + 1

    if number == 3:
        continue

    print(number)
```

You should see:

```text
1
2
4
5
```

Debugging prompt:

```text
In a while loop, can continue skip the line that makes the loop stop?
```

## Read the Docs

Today, revisit Python's official tutorial section about control flow:

```text
https://docs.python.org/3/tutorial/controlflow.html
```

Look for these topics:

- `for` statements
- the `range()` function
- `break` and `continue`

Read lightly. You are not trying to memorize the page.

Use the documentation to confirm three ideas:

```text
A for loop moves through a sequence.
range() creates number sequences.
break and continue change the path inside a loop.
```

Also look up the official documentation for `input()`:

```text
https://docs.python.org/3/library/functions.html#input
```

For tomorrow's project, remember this practical detail:

```text
input() gives you text.
```

If you want to compare a guess as text, store the secret as text:

```python
secret = "7"
```

If you want to compare a guess as a number, convert the input:

```python
guess = int(input("Guess: "))
```

Both choices can work. For early practice, text comparison is often easier because it avoids conversion errors while you are learning the loop.

## Mini Challenge

Create a file named `day-29/number_guessing_preview.py`.

Build a small preview of tomorrow's number guessing game.

Rules:

```text
Store the secret number as 6.
Give the user at most 3 attempts.
After each wrong guess, print "Too low." or "Too high."
If the user guesses correctly, print "Correct." and stop early.
If all attempts are used, print "Out of guesses."
```

Use text input, then convert only after you know the input is not empty.

Code:

```python
secret = 6
attempts = 0
max_attempts = 3
won = False

while attempts < max_attempts:
    guess_text = input("Guess the number: ").strip()

    if guess_text == "":
        print("Please type a number.")
        continue

    guess = int(guess_text)
    attempts = attempts + 1

    if guess == secret:
        print("Correct.")
        won = True
        break

    if guess < secret:
        print("Too low.")
    else:
        print("Too high.")

if not won:
    print("Out of guesses.")
```

Try this winning path:

```text
3
8
6
```

The program should say `"Too low."`, then `"Too high."`, then `"Correct."`.

Try this losing path:

```text
1
2
3
```

The program should use all three attempts and then print `"Out of guesses."`

Try one blank input:

```text

6
```

The blank input should not count as an attempt.

This preview has several pieces you already know:

- a `while` loop
- an attempt counter
- `continue` for blank input
- `break` after a correct guess
- a `won` flag
- final logic after the loop

Tomorrow you will turn this idea into a cleaner mini project.

## Real-World Use

Loop practice is not only for classroom examples.

Programs use repetition when they need to:

- ask again after invalid input
- count attempts, points, messages, or errors
- add prices, scores, minutes, or totals
- search for a matching item
- scan text for letters, digits, or spaces
- skip blank or unwanted values
- stop early after finding an answer
- run a menu until the user chooses to quit

The number guessing game uses several real loop habits:

```text
keep asking
count attempts
compare input with a target
stop early after success
handle the losing case after the loop
```

Those same habits appear later in quizzes, shopping lists, contact books, file tools, and command-line programs.

## Recap

Today you practiced:

- using `while` loops when the number of repeats is not known ahead of time
- using `for` loops when you already have a sequence
- using `range()` for numbered repetition
- looping through text one character at a time
- counting with a counter
- adding with a total
- searching with a boolean flag
- using `break` to stop early
- using `continue` to skip one loop turn
- debugging loop updates, indentation, and carried values

The main practice questions were:

```text
What repeats?
What changes?
What is remembered?
What stops the loop?
```

Keep those questions close. They make repetition problems much easier to start.

## Lesson Checklist

Before moving on, check that you can:

- choose `while` for a loop that stops when a condition changes
- choose `for` for a loop that moves through a sequence
- use `range()` to repeat a known number of times
- explain why `range(1, 6)` includes `5`
- loop through a string and inspect each character
- start counters and totals before the loop
- print final results after the loop
- use `break` when the whole loop should stop
- use `continue` when one loop turn should be skipped
- write a validation loop that asks again
- count attempts in a guessing loop
- test a loop with more than one input path

## Exercises

### Exercise 1

Predict the output before running the code.

```python
for number in range(1, 5):
    print(number)
```

Then answer:

```text
Why does 5 not print?
```

### Exercise 2

Write a loop that prints:

```text
Attempt 1
Attempt 2
Attempt 3
```

Use `range()`.

### Exercise 3

Write a `while` loop that counts from `1` to `4`.

After the loop, print:

```text
Done
```

### Exercise 4

Fix the loop.

Broken code:

```python
count = 1

while count <= 4:
    print(count)
```

Explain why the broken version does not stop.

### Exercise 5

Fix the range.

This program should print:

```text
Seat 1
Seat 2
Seat 3
Seat 4
```

Broken code:

```python
for seat in range(1, 4):
    print("Seat", seat)
```

### Exercise 6

Write a program that counts how many times `"a"` appears in:

```python
word = "avalanche"
```

The answer should be:

```text
3
```

### Exercise 7

Write a program that counts digits in:

```python
code = "A1B22C333"
```

Hint:

```python
digits = "0123456789"
```

The answer should be:

```text
6
```

### Exercise 8

Write a program that searches for `"!"` in a message.

Start with:

```python
message = "Careful!"
found = False
```

Use `break` after the program finds `"!"`.

After the loop, print:

```text
Exclamation found.
```

or:

```text
No exclamation found.
```

### Exercise 9

Write a loop that prints the numbers from `1` to `7`, but skips `4`.

Use `continue`.

You should see:

```text
1
2
3
5
6
7
```

### Exercise 10

Write a validation loop.

Rules:

```text
Ask the user to type "start".
Keep asking until they type start.
When they do, print "Starting now."
```

Make the input friendly by using:

```python
.strip().lower()
```

### Exercise 11

Write a simple menu loop.

The menu should repeat until the user chooses `"3"`.

```text
1. Say hello
2. Show score
3. Quit
```

Rules:

```text
Blank input should be ignored.
Choice 1 prints "Hello."
Choice 2 prints "Score: 0"
Choice 3 stops the loop.
Anything else prints "Unknown choice."
After the loop, print "Goodbye."
```

Use both `break` and `continue`.

### Exercise 12

Build a word hider.

Ask the user for a word.

Build a new string where every vowel becomes `"*"`.

Example behavior:

```text
Word: banana
b*n*n*
```

Hint:

```text
Start hidden as an empty string.
For each letter:
    If it is a vowel, add "*".
    Otherwise, add the original letter.
```

### Exercise 13

Build a tiny number guessing practice loop.

Rules:

```text
The secret number is "5".
The user keeps guessing until they type 5.
Every wrong guess prints "Try again."
The correct guess prints "Correct."
The program prints the number of attempts.
```

Keep the secret as text for this version:

```python
secret = "5"
```

### Exercise 14

Add an attempt limit to Exercise 13.

Rules:

```text
The user gets 3 attempts.
If they guess correctly, print "Correct." and stop.
If they use all attempts, print "Out of guesses."
```

Hint:

```text
The loop condition needs to check both the guess and the attempt count.
```

You may use:

```python
while guess != secret and attempts < 3:
```

### Exercise 15

Choose one loop from today's lesson and add temporary debug prints.

Show:

```text
the value at the top of the loop
the value after it changes
the final value after the loop
```

Then remove the debug prints when the loop makes sense.

Debugging is not a sign that you failed. It is how you see what the program is doing.

## Tiny Win

Today you practiced loops as problem-solving tools, not just syntax.

You can now look at a repetition problem and ask:

```text
Is this counting, adding, searching, validating, skipping, stopping, or building?
```

That question is a strong starting point.

## Tomorrow

Tomorrow you will build a mini project:

```text
Number Guessing Game
```

You already have most of the pieces:

- a secret number
- user input
- a `while` loop
- attempt counting
- comparisons
- `break` after success
- a message after the game ends

Before tomorrow, make sure you can explain this loop in your own words:

```python
secret = "7"
guess = ""
attempts = 0

while guess != secret:
    guess = input("Guess: ")
    attempts = attempts + 1

print("Correct.")
print("Attempts:", attempts)
```

If that loop makes sense, tomorrow's project is already halfway familiar.
