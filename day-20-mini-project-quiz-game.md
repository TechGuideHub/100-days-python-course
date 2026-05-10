# Day 20: Mini Project: Quiz Game

**Focus:** Building a complete quiz game with decisions and scoring  
**You will practice:** `input()`, string cleanup, comparisons, `if` / `elif` / `else`, boolean logic, score tracking, testing, and debugging  
**Estimated time:** 50-65 minutes

## Today's Goal

Today you will build a small quiz game.

The game will ask questions, check the player's answers, keep score, and print a final result.

It will not use loops yet. That means some of the code will repeat. That is fine for today. The repetition helps you see the pattern clearly before Python starts repeating it for you tomorrow.

By the end of this lesson, you should be able to:

* plan a small program with several stages
* use `input()` to collect answers
* compare strings with `==`
* use `if`, `elif`, and `else` to respond to answers
* use `and`, `or`, and `not` in a real program
* track a score with a number variable
* print a final result based on the score
* test a program with different answer combinations
* debug common quiz-game mistakes

This is the second mini-project in the course.

The goal is not to make a large game. The goal is to combine the decision-making tools you have learned into one complete program.

## The Project

Create this file:

```text
day-20/quiz_game.py
```

The program will:

* welcome the player
* ask for the player's name
* start the score at `0`
* ask five quiz questions
* check each answer
* add `1` point for each correct answer
* show the score after each question
* print a final score and message

Example:

```text
Welcome to the quiz game.
Answer five questions. Type your answer and press Enter.

Player name: Maya

Question 1
Which Python function asks the user for text? INPUT
Correct.
Score: 1 out of 5

Question 2
Which keyword is the final backup path after if and elif? elif
Close. elif checks another condition. else is the final backup.
Score: 1 out of 5

Question 3
What is 6 + 2? 8
Correct.
Score: 2 out of 5

Question 4
A player has a ticket and is not banned.
Can the player enter? yes/no yes
Correct.
Score: 3 out of 5

Question 5
Which value means a condition worked: True or False? true
Correct.
Score: 4 out of 5

Final score for Maya: 4 out of 5.
Percentage: 80%
Good work. A few details can still be reviewed.
```

This project has the shape of many simple games:

```text
ask -> check -> update score -> show result
```

That pattern is worth learning slowly.

## The Big Idea

A quiz game is a decision program.

Every question creates a small decision:

```text
Was the answer correct?
```

In Python, that question becomes a comparison:

```python
answer == "input"
```

The comparison produces a boolean value:

```text
True or False
```

Then an `if` statement chooses what happens next:

```python
if answer == "input":
    print("Correct.")
else:
    print("Not quite.")
```

To keep score, the program uses a number variable:

```python
score = 0
```

When the player gets an answer right, the program adds one point:

```python
score = score + 1
```

That line means:

```text
Take the old score.
Add 1.
Store the new score back in score.
```

The quiz is built from small pieces you already know. The new skill is putting them in a useful order.

## The Mental Model

Think of the quiz game as a careful scorekeeper.

For each question, the scorekeeper does four jobs:

```text
1. Ask the question.
2. Clean up the answer a little.
3. Decide whether the answer is correct.
4. Update the score if needed.
```

In code, that often looks like this:

```python
answer = input("Which Python function asks the user for text? ")
answer = answer.strip().lower()

if answer == "input" or answer == "input()":
    print("Correct.")
    score = score + 1
else:
    print("Not quite. The answer is input().")
```

The cleanup line does two small jobs:

```python
answer = answer.strip().lower()
```

* `strip()` removes extra spaces from the start and end
* `lower()` makes uppercase and lowercase answers easier to compare

So these answers can all be treated the same:

```text
input
INPUT
 Input 
input()
```

The program is not becoming intelligent. It is just becoming less fragile. That is a good habit.

## Step-by-Step Build

Build the project in stages.

Do not start with the full quiz. A project is easier to trust when each small part works before you add the next one.

### Step 1: Create the File

Create this file:

```text
day-20/quiz_game.py
```

Code:

```python
print("Welcome to the quiz game.")
print("Answer five questions. Type your answer and press Enter.")
```

Run it from your course folder:

```bash
python day-20/quiz_game.py
```

If your computer uses `py`, use:

```bash
py day-20/quiz_game.py
```

If your computer uses `python3`, use:

```bash
python3 day-20/quiz_game.py
```

You should see:

```text
Welcome to the quiz game.
Answer five questions. Type your answer and press Enter.
```

This does not feel like a game yet. That is fine. First, make sure the file runs.

### Step 2: Ask for the Player's Name

Add a blank line and ask for the player's name:

```python
print("Welcome to the quiz game.")
print("Answer five questions. Type your answer and press Enter.")

print("")
player = input("Player name: ")
```

Run it and type a name.

Example:

```text
Welcome to the quiz game.
Answer five questions. Type your answer and press Enter.

Player name: Maya
```

The name will be used at the end. That gives the program a small thread of memory:

```text
ask now -> use later
```

### Step 3: Create the Score

After the player name, create two number variables:

```python
score = 0
total_questions = 5
```

Now the program has a place to store progress.

At the beginning, the score is zero because the player has not answered anything yet.

The `total_questions` variable keeps the number of questions in one clear place. This line:

```python
print("Score: " + str(score) + " out of " + str(total_questions))
```

is clearer than hiding the number `5` in several different score messages.

### Step 4: Ask the First Question

Add the first question:

```python
print("")
print("Question 1")
answer_one = input("Which Python function asks the user for text? ")
answer_one = answer_one.strip().lower()

if answer_one == "input" or answer_one == "input()":
    print("Correct.")
    score = score + 1
else:
    print("Not quite. The answer is input().")

print("Score: " + str(score) + " out of " + str(total_questions))
```

There are several useful ideas in this block.

This line collects the answer:

```python
answer_one = input("Which Python function asks the user for text? ")
```

This line cleans it up:

```python
answer_one = answer_one.strip().lower()
```

This line accepts two correct versions:

```python
if answer_one == "input" or answer_one == "input()":
```

The answer can be:

```text
input
```

or:

```text
input()
```

Both should count as correct.

The `or` means:

```text
If either comparison is true, treat the answer as correct.
```

Try this:

| Input | You should see |
| --- | --- |
| `input` | `Correct.` |
| `INPUT` | `Correct.` |
| ` input ` | `Correct.` |
| `print` | `Not quite.` |

These are manual test cases. You are not writing a testing tool yet. You are running the program with chosen inputs and checking the result.

That counts.

### Step 5: Add a Question with `elif`

Now add a second question.

This one uses `elif` to give a helpful response for a close answer:

```python
print("")
print("Question 2")
answer_two = input("Which keyword is the final backup path after if and elif? ")
answer_two = answer_two.strip().lower()

if answer_two == "else":
    print("Correct.")
    score = score + 1
elif answer_two == "elif":
    print("Close. elif checks another condition. else is the final backup.")
else:
    print("Not quite. The answer is else.")

print("Score: " + str(score) + " out of " + str(total_questions))
```

The structure is:

```text
if correct answer:
    give the point
elif common near answer:
    explain the difference
else:
    show the answer
```

Notice that the `elif` does not add a point. The answer is close, but it is not the correct answer for this question.

That is one useful job for `elif`: different wrong answers can get different responses.

### Step 6: Add a Number Question

The third question is a math question.

To keep the program beginner-safe, compare the typed answer as text. That means the program will not crash if someone types:

```text
eight
```

Add this:

```python
print("")
print("Question 3")
answer_three = input("What is 6 + 2? ")
answer_three = answer_three.strip()

if answer_three == "8":
    print("Correct.")
    score = score + 1
elif answer_three == "7" or answer_three == "9":
    print("Close. The answer is 8.")
else:
    print("Not quite. The answer is 8.")

print("Score: " + str(score) + " out of " + str(total_questions))
```

This question still practices numbers because the quiz is tracking a numeric score. The answer itself stays as text.

That is a deliberate choice. You already know how to use `int()`, but without loops or error handling, a quiz can be friendlier if it checks simple typed answers as strings.

Later, you will learn stronger ways to handle number input.

### Step 7: Add a Boolean Logic Question

The fourth question uses a tiny rule:

```text
A player can enter if they have a ticket and they are not banned.
```

Add this:

```python
print("")
print("Question 4")
print("A player has a ticket and is not banned.")
answer_four = input("Can the player enter? yes/no ")
answer_four = answer_four.strip().lower()

has_ticket = True
is_banned = False
can_enter = has_ticket and not is_banned

answered_yes = answer_four == "yes" or answer_four == "y"
answered_no = answer_four == "no" or answer_four == "n"

if answered_yes and can_enter:
    print("Correct.")
    score = score + 1
elif answered_no and not can_enter:
    print("Correct.")
    score = score + 1
elif answered_yes or answered_no:
    print("Not quite. The player can enter.")
else:
    print("Please answer yes or no next time. The player can enter.")

print("Score: " + str(score) + " out of " + str(total_questions))
```

This block is longer than the earlier questions, so read it slowly.

First, the program stores the rule:

```python
has_ticket = True
is_banned = False
can_enter = has_ticket and not is_banned
```

Since `has_ticket` is `True` and `is_banned` is `False`, the rule becomes:

```text
can_enter = True and not False
can_enter = True and True
can_enter = True
```

Then the program checks what the player typed:

```python
answered_yes = answer_four == "yes" or answer_four == "y"
answered_no = answer_four == "no" or answer_four == "n"
```

Finally, it compares the player's answer with the rule.

This is the most logic-heavy part of the project. The helpful habit is naming the smaller questions:

```python
can_enter
answered_yes
answered_no
```

Clear names make the final `if` statements easier to follow.

### Step 8: Add One More Review Question

The fifth question checks the idea of booleans directly:

```python
print("")
print("Question 5")
answer_five = input("Which value means a condition worked: True or False? ")
answer_five = answer_five.strip().lower()

if answer_five == "true":
    print("Correct.")
    score = score + 1
elif answer_five == "false":
    print("False means the condition did not work.")
else:
    print("Not quite. The answer is True.")

print("Score: " + str(score) + " out of " + str(total_questions))
```

Now the quiz has five questions.

The code is a little repetitive. That is expected. Tomorrow, this repetition will make loops feel useful instead of mysterious.

### Step 9: Print the Final Result

At the end of the file, calculate the percentage:

```python
percentage = int(score * 100 / total_questions)
```

Then print the final result:

```python
print("")
print("Final score for " + player + ": " + str(score) + " out of " + str(total_questions) + ".")
print("Percentage: " + str(percentage) + "%")
```

Now add score bands:

```python
if score == total_questions:
    print("Perfect score. You remembered every answer.")
elif score >= 3:
    print("Good work. A few details can still be reviewed.")
else:
    print("Keep practicing. Rerun the quiz and read each explanation.")
```

This final decision uses number comparisons:

```python
score == total_questions
score >= 3
```

The exact messages are not important. What matters is that the program responds differently based on the final score.

### Step 10: Put It Together

Here is the complete program:

```python
print("Welcome to the quiz game.")
print("Answer five questions. Type your answer and press Enter.")

print("")
player = input("Player name: ")

score = 0
total_questions = 5

print("")
print("Question 1")
answer_one = input("Which Python function asks the user for text? ")
answer_one = answer_one.strip().lower()

if answer_one == "input" or answer_one == "input()":
    print("Correct.")
    score = score + 1
else:
    print("Not quite. The answer is input().")

print("Score: " + str(score) + " out of " + str(total_questions))

print("")
print("Question 2")
answer_two = input("Which keyword is the final backup path after if and elif? ")
answer_two = answer_two.strip().lower()

if answer_two == "else":
    print("Correct.")
    score = score + 1
elif answer_two == "elif":
    print("Close. elif checks another condition. else is the final backup.")
else:
    print("Not quite. The answer is else.")

print("Score: " + str(score) + " out of " + str(total_questions))

print("")
print("Question 3")
answer_three = input("What is 6 + 2? ")
answer_three = answer_three.strip()

if answer_three == "8":
    print("Correct.")
    score = score + 1
elif answer_three == "7" or answer_three == "9":
    print("Close. The answer is 8.")
else:
    print("Not quite. The answer is 8.")

print("Score: " + str(score) + " out of " + str(total_questions))

print("")
print("Question 4")
print("A player has a ticket and is not banned.")
answer_four = input("Can the player enter? yes/no ")
answer_four = answer_four.strip().lower()

has_ticket = True
is_banned = False
can_enter = has_ticket and not is_banned

answered_yes = answer_four == "yes" or answer_four == "y"
answered_no = answer_four == "no" or answer_four == "n"

if answered_yes and can_enter:
    print("Correct.")
    score = score + 1
elif answered_no and not can_enter:
    print("Correct.")
    score = score + 1
elif answered_yes or answered_no:
    print("Not quite. The player can enter.")
else:
    print("Please answer yes or no next time. The player can enter.")

print("Score: " + str(score) + " out of " + str(total_questions))

print("")
print("Question 5")
answer_five = input("Which value means a condition worked: True or False? ")
answer_five = answer_five.strip().lower()

if answer_five == "true":
    print("Correct.")
    score = score + 1
elif answer_five == "false":
    print("False means the condition did not work.")
else:
    print("Not quite. The answer is True.")

print("Score: " + str(score) + " out of " + str(total_questions))

percentage = int(score * 100 / total_questions)

print("")
print("Final score for " + player + ": " + str(score) + " out of " + str(total_questions) + ".")
print("Percentage: " + str(percentage) + "%")

if score == total_questions:
    print("Perfect score. You remembered every answer.")
elif score >= 3:
    print("Good work. A few details can still be reviewed.")
else:
    print("Keep practicing. Rerun the quiz and read each explanation.")
```

Run the program at least three times. Use different answers each time.

Try these complete quiz runs:

| Q1 | Q2 | Q3 | Q4 | Q5 | Score should be |
| --- | --- | --- | --- | --- | ---: |
| `input` | `else` | `8` | `yes` | `true` | 5 |
| `INPUT()` | `elif` | `8` | `y` | `false` | 3 |
| `print` | `else` | `7` | `no` | `true` | 2 |
| ` input ` | `ELSE` | `eight` | `maybe` | `TRUE` | 3 |

When you test, do not only look for errors.

Also check the small details:

* Did the score increase only when it should?
* Did uppercase answers still work?
* Did extra spaces get ignored?
* Did the final message match the score?
* Did any explanation feel unclear?

Testing is not just checking whether the program crashes. Testing is checking whether the program behaves the way you intended.

## Example

Here is one full run:

```text
Welcome to the quiz game.
Answer five questions. Type your answer and press Enter.

Player name: Noor

Question 1
Which Python function asks the user for text? input()
Correct.
Score: 1 out of 5

Question 2
Which keyword is the final backup path after if and elif? else
Correct.
Score: 2 out of 5

Question 3
What is 6 + 2? 9
Close. The answer is 8.
Score: 2 out of 5

Question 4
A player has a ticket and is not banned.
Can the player enter? yes/no y
Correct.
Score: 3 out of 5

Question 5
Which value means a condition worked: True or False? true
Correct.
Score: 4 out of 5

Final score for Noor: 4 out of 5.
Percentage: 80%
Good work. A few details can still be reviewed.
```

The score changed four times because four answers were correct.

Question 3 did not add a point because `9` is close, but not correct.

The final message came from this condition:

```python
elif score >= 3:
    print("Good work. A few details can still be reviewed.")
```

Since `score` was `4`, the condition was true.

## Try It Yourself

Change the quiz so it feels like your own.

Choose one theme:

* Python basics
* school subjects
* sports
* movies
* geography
* food
* music
* family trivia
* a book you like

Start by changing only the question text and correct answers.

Keep the same structure:

```python
answer = input("Your question here: ")
answer = answer.strip().lower()

if answer == "correct answer":
    print("Correct.")
    score = score + 1
else:
    print("Not quite.")
```

Then try one of these extension ideas:

* accept two correct spellings with `or`
* add a close answer with `elif`
* change the final score messages
* add one more question and update `total_questions`
* ask for the player's favorite topic at the beginning
* print a short review message for each wrong answer
* make one question use `yes` or `no`
* make one question use a small boolean rule

For today, do not add a loop.

If you want ten questions, you may write ten question blocks. It will feel repetitive, and that feeling is useful.

Tomorrow, you will learn the tool that removes that kind of repetition.

## Common Mistake

### Mistake 1: Forgetting to Update the Score

Broken code:

```python
score = 0
answer = input("What is 2 + 2? ")

if answer == "4":
    print("Correct.")
else:
    print("Not quite.")

print(score)
```

If the answer is correct, you should see:

```text
Correct.
0
```

The program says the answer is correct, but the score stays `0`.

Fixed code:

```python
score = 0
answer = input("What is 2 + 2? ")

if answer == "4":
    print("Correct.")
    score = score + 1
else:
    print("Not quite.")

print(score)
```

The score must change inside the correct-answer branch.

### Mistake 2: Comparing Against the Wrong Capitalization

Broken code:

```python
answer = input("Type True or False: ")

if answer == "true":
    print("Correct.")
else:
    print("Not quite.")
```

If the user types:

```text
True
```

the program prints:

```text
Not quite.
```

That happens because `"True"` and `"true"` are different strings.

Fixed code:

```python
answer = input("Type True or False: ")
answer = answer.lower()

if answer == "true":
    print("Correct.")
else:
    print("Not quite.")
```

For quiz answers, cleaning the answer before comparing it usually makes the game nicer to use.

### Mistake 3: Writing an `or` Condition Incorrectly

Broken code:

```python
answer = input("Which function asks for text? ")
answer = answer.lower()

if answer == "input" or "input()":
    print("Correct.")
else:
    print("Not quite.")
```

This looks reasonable at first, but it is wrong.

Python does not read it as:

```text
answer equals "input" or answer equals "input()"
```

Write the full comparison twice:

```python
if answer == "input" or answer == "input()":
    print("Correct.")
else:
    print("Not quite.")
```

Each side of `or` should be a real yes-or-no expression.

### Mistake 4: Changing the Total Questions but Not the Program

Broken code:

```python
score = 0
total_questions = 10
```

If the program only asks five questions, the final score will look strange:

```text
Final score: 4 out of 10
```

The number is not a calculation mistake. The program was told there are ten questions.

Keep `total_questions` matched to the number of question blocks you actually wrote.

## Debug It

Debugging a quiz game usually means checking one small question at a time.

The examples in this section are supposed to have bugs. Read the code before looking at the fix.

### Bug 1: The Score Goes Up for a Wrong Answer

Broken code:

```python
score = 0
answer = input("What is 6 + 2? ")

if answer == "8":
    print("Correct.")
else:
    print("Not quite.")
    score = score + 1

print(score)
```

If the user types:

```text
7
```

the score becomes `1`.

The problem is indentation. The score update is inside the `else` branch.

Fixed code:

```python
score = 0
answer = input("What is 6 + 2? ")

if answer == "8":
    print("Correct.")
    score = score + 1
else:
    print("Not quite.")

print(score)
```

Indentation decides which branch owns a line.

### Bug 2: The Program Rejects a Correct Answer with Spaces

Broken code:

```python
answer = input("Which function asks the user for text? ")
answer = answer.lower()

if answer == "input":
    print("Correct.")
else:
    print("Not quite.")
```

If the user types:

```text
 input
```

the answer contains a leading space. That string is not equal to `"input"`.

Fixed code:

```python
answer = input("Which function asks the user for text? ")
answer = answer.strip().lower()

if answer == "input":
    print("Correct.")
else:
    print("Not quite.")
```

Use `strip()` when extra spaces should not matter.

### Bug 3: The Final Message Is Too Easy to Reach

Broken code:

```python
score = 2
total_questions = 5

if score == total_questions:
    print("Perfect score.")
elif score >= 2:
    print("Good work.")
else:
    print("Keep practicing.")
```

This code says `2` out of `5` is "Good work."

Maybe that is kinder than you intended. The code is not broken in Python's eyes. The bug is in the rule.

Fixed code:

```python
score = 2
total_questions = 5

if score == total_questions:
    print("Perfect score.")
elif score >= 3:
    print("Good work.")
else:
    print("Keep practicing.")
```

When a program gives the wrong message, check the comparison. The operator may be valid, but the rule may be wrong.

### Bug 4: A Boolean Rule Is Hard to See

Broken code:

```python
has_ticket = True
is_banned = False
answer = input("Can the player enter? yes/no ")
answer = answer.lower()

if answer == "yes" and has_ticket or not is_banned:
    print("Correct.")
else:
    print("Not quite.")
```

This condition is confusing. It mixes the user's answer with the entry rule all at once.

Debug it by naming the smaller questions:

```python
has_ticket = True
is_banned = False
answer = input("Can the player enter? yes/no ")
answer = answer.strip().lower()

can_enter = has_ticket and not is_banned
answered_yes = answer == "yes" or answer == "y"
answered_no = answer == "no" or answer == "n"

print("can_enter:", can_enter)
print("answered_yes:", answered_yes)
print("answered_no:", answered_no)

if answered_yes and can_enter:
    print("Correct.")
elif answered_no and not can_enter:
    print("Correct.")
else:
    print("Not quite.")
```

The temporary `print()` lines let you see the smaller boolean values.

Once the program works, you can remove those debug prints.

## Read the Docs

Python's string documentation includes the methods you used today.

Look up these two methods if you can:

```text
https://docs.python.org/3/library/stdtypes.html#str.lower
https://docs.python.org/3/library/stdtypes.html#str.strip
```

You do not need to memorize every string method.

For today, focus on these facts:

* `lower()` returns a lowercase version of a string
* `strip()` returns a copy with spaces removed from the start and end

Try this:

```python
word = "  INPUT  "

print(word)
print(word.strip())
print(word.lower())
print(word.strip().lower())
```

You should see:

```text
  INPUT  
INPUT
  input  
input
```

The order matters a little.

This:

```python
word.strip().lower()
```

means:

```text
First remove outside spaces.
Then make the result lowercase.
```

In this quiz game, that makes answer checking more forgiving.

## Mini Challenge

Create a second file:

```text
day-20/mini_quiz_custom.py
```

Build a three-question quiz about any topic you know well.

Requirements:

* ask for the player's name
* create `score = 0`
* create `total_questions = 3`
* ask three questions
* use `if`, `elif`, and `else` at least once
* use `or` to accept two versions of one answer
* use `and` or `not` in one boolean rule
* print the final score
* print a different final message for a high, medium, or low score

Example theme:

```text
Topic: Food

Question 1: Which fruit is usually yellow, banana or grape?
Question 2: Is soup usually eaten with a spoon? yes/no
Question 3: What is 3 + 2?
```

Possible code shape for a yes/no question:

```python
answer = input("Is soup usually eaten with a spoon? yes/no ")
answer = answer.strip().lower()

answered_yes = answer == "yes" or answer == "y"
answered_no = answer == "no" or answer == "n"

if answered_yes:
    print("Correct.")
    score = score + 1
elif answered_no:
    print("Not quite. Soup is usually eaten with a spoon.")
else:
    print("Please answer yes or no next time.")
```

Do not worry about making the quiz long. A clear three-question quiz is better practice than a messy twenty-question quiz.

## Real-World Use

Quiz-game logic appears in more places than school quizzes.

Examples:

* a language-learning app checks whether your translation matches
* a training site scores a safety quiz
* a game checks whether a puzzle answer is correct
* a form checks whether required answers are present
* a study app gives feedback after each question
* a customer-support tool routes a person based on answers

The interface may look different, but the logic is familiar:

```text
collect an answer
compare it with a rule
give feedback
update a result
```

That is the same shape you used today.

## Recap

Today you built a complete quiz game.

You practiced:

* collecting answers with `input()`
* storing answers in variables
* cleaning strings with `strip()` and `lower()`
* comparing strings with `==`
* using `if`, `elif`, and `else`
* using `or` to accept more than one answer
* using `and` and `not` in a boolean rule
* tracking a numeric score
* calculating a simple percentage
* choosing a final message with comparisons
* testing a program with planned inputs
* debugging score and logic mistakes

The main idea:

> A quiz game is a chain of small decisions with a score that remembers the result.

## Lesson Checklist

Before moving on, check that you can:

* create and run `day-20/quiz_game.py`
* build the project one small stage at a time
* clean an answer with `strip()` and `lower()`
* accept two correct answers with `or`
* use `elif` for a close answer
* update a score only when an answer is correct
* use named booleans to make a yes/no rule clearer
* calculate and print a final percentage
* test the quiz with correct, incorrect, uppercase, and spaced answers
* explain why the repeated question blocks are useful practice before loops

## Exercises

### Exercise 1

Create this file:

```text
day-20/two_question_quiz.py
```

Ask two questions. Track the score. Print the final score.

Keep the questions simple.

### Exercise 2

Fix this program:

```python
score = 0
answer = input("Which keyword starts a condition? ")

if answer == "if":
    print("Correct.")
else:
    print("Not quite.")

print("Score:", score)
```

The score should become `1` when the answer is correct.

### Exercise 3

Fix this answer check so it accepts both `input` and `input()`:

```python
answer = input("Which function asks for text? ")
answer = answer.strip().lower()

if answer == "input" or "input()":
    print("Correct.")
else:
    print("Not quite.")
```

Remember:

```text
Each side of or needs its own comparison.
```

### Exercise 4

Write a question that uses `elif` for a close answer.

Example:

```text
Question: Which keyword means final backup, else or elif?
Correct answer: else
Close answer: elif
```

Your program should print:

* `Correct.` for the correct answer
* a helpful explanation for the close answer
* `Not quite.` for any other answer

### Exercise 5

Create a yes/no question.

Accept both short and long answers:

```text
yes
y
no
n
```

Use boolean variables like:

```python
answered_yes
answered_no
```

### Exercise 6

Change the final score messages.

Use these rules:

```text
5 points: Excellent review.
3 or 4 points: Solid start.
0, 1, or 2 points: Review and try again.
```

Write the `if`, `elif`, and `else` block for those rules.

### Exercise 7

Add one question to the final quiz.

Then update:

```python
total_questions = 6
```

Run the quiz and make sure the final score says:

```text
out of 6
```

### Exercise 8

Debug this score bug:

```python
score = 0
answer = input("What is 3 + 3? ")

if answer == "6":
    print("Correct.")
else:
    print("Not quite.")
score = score + 1

print(score)
```

What happens if the user types `5`?

Move the score update so wrong answers do not get a point.

### Exercise 9

Write a quiz question based on this rule:

```text
A user can reset a password if the email is verified and the account is not locked.
```

Start with:

```python
email_verified = True
account_locked = False
```

Create a boolean named:

```python
can_reset_password
```

Ask:

```text
Can the user reset the password? yes/no
```

Then check whether the player's answer matches the rule.

### Exercise 10

Run your quiz three times.

Write down:

* one input that should earn a point
* one input that should not earn a point
* one input with uppercase letters or extra spaces
* the score you expected
* the score the program printed

If the expected score and printed score do not match, debug one question block at a time.

## Tiny Win

You built a program that asks questions, checks answers, tracks a score, and gives a final result.

That is a real game shape. It has rules, feedback, state, and an ending.

The code repeats today, but the pattern is clear. That clarity is exactly what makes the next lesson easier.

## Tomorrow

Tomorrow you will start Phase 3: loops and repetition.

The first lesson is:

```text
Day 21: Why Loops Matter
```

Today, each quiz question needed its own block of code.

That worked, but it was repetitive:

```text
ask a question
check the answer
update the score
show the score
```

Loops let a program repeat a pattern without you writing the same shape again and again.

You have now felt the problem loops solve.
