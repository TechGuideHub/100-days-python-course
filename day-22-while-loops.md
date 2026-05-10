# Day 22: `while` Loops

**Focus:** Repeating code while a condition stays true  
**You will practice:** writing `while` loops, using counters, updating loop values, reading loop conditions, and debugging loops that do not stop  
**Estimated time:** 45-55 minutes

## Today's Goal

Today you will learn how to repeat code with a `while` loop.

So far, many of your programs have moved from top to bottom.

Example:

```python
name = input("Name: ")
print("Hello,", name)
```

They can also make decisions.

Example:

```python
if name == "":
    print("You did not enter a name.")
```

But most of those programs still do each step once.

A loop lets a program repeat a block of code.

By the end of this lesson, you should be able to:

- write a basic `while` loop
- explain when the loop condition is checked
- use a counter to control repetition
- update a value so a loop can eventually stop
- write a simple input loop
- recognize an infinite loop warning sign
- debug indentation and update mistakes in a loop

The main idea is:

> A `while` loop repeats an indented block while its condition is true.

Broken examples are labeled clearly. Study them first; run them only when you want to see the problem.

## The Big Idea

A `while` loop asks a question before it runs.

Basic shape:

```text
while condition:
    code that repeats
```

Example:

```python
count = 1

while count <= 3:
    print(count)
    count = count + 1
```

You should see:

```text
1
2
3
```

Read the loop like this:

```text
While count is less than or equal to 3,
print count,
then add 1 to count.
```

The condition is checked before each repeat.

Python keeps asking:

```text
Is count <= 3 still true?
```

When the answer becomes `False`, the loop stops. Then the program continues after the loop.

Most beginner `while` loops have three important parts:

```python
count = 1              # starting value

while count <= 3:      # condition
    print(count)
    count = count + 1  # update
```

The starting value gives the loop somewhere to begin.

The condition decides whether the loop keeps going.

The update changes a value so the condition can eventually become false.

## The Mental Model

Think of a `while` loop as a checkpoint at the top of a path.

Before Python enters the loop, it checks the condition.

```python
while count <= 3:
```

If the condition is `True`, Python runs the indented code.

Then Python goes back to the top and checks the condition again.

The loop does not stop because it has printed something. It stops only when the condition becomes `False`.

Code:

```python
seconds = 5

while seconds > 0:
    print(seconds)
    seconds = seconds - 1

print("Launch!")
```

You should see:

```text
5
4
3
2
1
Launch!
```

Here is what happens each time Python reaches the top of the loop:

| Value of `seconds` | Is `seconds > 0`? | What prints? | New value |
| ---: | --- | --- | ---: |
| 5 | `True` | `5` | 4 |
| 4 | `True` | `4` | 3 |
| 3 | `True` | `3` | 2 |
| 2 | `True` | `2` | 1 |
| 1 | `True` | `1` | 0 |
| 0 | `False` | nothing | loop ends |

This line is important:

```python
seconds = seconds - 1
```

Without it, `seconds` would stay `5`, and the condition would stay true.

Also notice that this line is not indented under the loop:

```python
print("Launch!")
```

That means it runs once, after the loop is finished.

## Try It Yourself

Create a file named:

```text
day-22/while_practice.py
```

Code:

```python
number = 1

while number <= 5:
    print("Number:", number)
    number = number + 1

print("Done counting.")
```

Before you run it, predict the output.

Run the file from your course folder:

```bash
python day-22/while_practice.py
```

If your computer uses `py`, use:

```bash
py day-22/while_practice.py
```

If your computer uses `python3`, use:

```bash
python3 day-22/while_practice.py
```

You should see:

```text
Number: 1
Number: 2
Number: 3
Number: 4
Number: 5
Done counting.
```

Now change the starting value:

```python
number = 3
```

Run the program again.

Then change the condition:

```python
while number <= 8:
```

Run it again.

After each change, ask:

```text
What value does the loop start with?
What question controls the loop?
What line changes the answer to that question?
```

Now try counting down:

```python
number = 5

while number >= 1:
    print("Number:", number)
    number = number - 1

print("Done counting down.")
```

The update changed from adding `1` to subtracting `1`.

The condition changed too:

```python
while number >= 1:
```

Those two lines need to agree with each other. If the condition counts down, the update usually needs to move down too.

## Common Mistake

Some broken loops in this section can run forever. Read them carefully before running them.

### Mistake 1: Forgetting to update the condition value

Broken code:

```python
count = 1

while count <= 3:
    print(count)
```

This loop keeps printing `1`.

The problem is that `count` never changes, so this condition stays true:

```python
count <= 3
```

Fixed code:

```python
count = 1

while count <= 3:
    print(count)
    count = count + 1
```

A `while` loop usually needs something inside it that moves the program toward stopping.

### Mistake 2: Updating in the wrong direction

Broken code:

```python
number = 1

while number <= 5:
    print(number)
    number = number - 1
```

This loop is supposed to count up to `5`, but the update makes `number` smaller.

The condition is:

```python
number <= 5
```

If `number` goes from `1` to `0` to `-1`, it is still less than or equal to `5`. The loop is moving away from stopping.

Fixed code:

```python
number = 1

while number <= 5:
    print(number)
    number = number + 1
```

The update should move the value toward making the condition false.

### Mistake 3: Indenting a line into the loop by accident

This program prints `"Finished."` once.

Code:

```python
count = 1

while count <= 3:
    print(count)
    count = count + 1

print("Finished.")
```

You should see:

```text
1
2
3
Finished.
```

This version prints `"Finished."` every time through the loop.

Code:

```python
count = 1

while count <= 3:
    print(count)
    count = count + 1
    print("Finished.")
```

You should see:

```text
1
Finished.
2
Finished.
3
Finished.
```

In the second program, `print("Finished.")` is indented under the loop.

Indentation controls what repeats. When a line should happen once after the loop, move it back to the left.

### Mistake 4: Using `if` when you need repeated checking

This checks the password once:

```python
password = input("Password: ")

if password != "python":
    print("Try again.")
```

An `if` statement makes one decision. It does not automatically ask again.

A `while` loop can keep checking:

```python
password = input("Password: ")

while password != "python":
    print("Try again.")
    password = input("Password: ")

print("Welcome.")
```

Use `if` for one decision.

Use `while` when the same decision may need to be checked repeatedly.

## Debug It

Here is a broken program.

It is supposed to print:

```text
Ticket 1
Ticket 2
Ticket 3
All tickets printed.
```

Broken code:

```python
ticket = 1

while ticket <= 3:
    print("Ticket", ticket)

ticket = ticket + 1
print("All tickets printed.")
```

The program keeps printing:

```text
Ticket 1
Ticket 1
Ticket 1
```

The update line is not indented, so it does not belong to the loop:

```python
ticket = ticket + 1
```

Python never reaches that line because the loop never ends.

Fixed code:

```python
ticket = 1

while ticket <= 3:
    print("Ticket", ticket)
    ticket = ticket + 1

print("All tickets printed.")
```

You should see:

```text
Ticket 1
Ticket 2
Ticket 3
All tickets printed.
```

When a `while` loop behaves strangely, print the value that controls the loop.

Code:

```python
ticket = 1

while ticket <= 3:
    print("Before update:", ticket)
    print("Ticket", ticket)
    ticket = ticket + 1
    print("After update:", ticket)

print("All tickets printed.")
```

You should see:

```text
Before update: 1
Ticket 1
After update: 2
Before update: 2
Ticket 2
After update: 3
Before update: 3
Ticket 3
After update: 4
All tickets printed.
```

The loop stops when `ticket` becomes `4`, because this condition is no longer true:

```python
ticket <= 3
```

When debugging a loop, ask:

1. What value starts the loop?
2. What condition keeps the loop running?
3. What value changes inside the loop?
4. Is that value moving toward making the condition false?

Those four questions catch many beginner loop bugs.

## Read the Docs

Python's official reference has a section for the `while` statement:

```text
https://docs.python.org/3/reference/compound_stmts.html#the-while-statement
```

For today, look for the basic loop shape:

```text
while condition:
    statement
```

You do not need every advanced detail yet. Focus on three details:

```text
The condition comes after the word while.
The header line ends with a colon.
The repeated code is indented underneath.
```

Official documentation sometimes uses formal words such as "statement" and "suite." For now, translate that into:

```text
A while loop controls an indented block of code.
```

## Mini Challenge

Create a file named:

```text
day-22/password_loop.py
```

Build a small password loop.

The program should:

- ask the user for a password
- keep asking while the password is wrong
- print a welcome message when the password is correct

Use this correct password:

```python
correct_password = "python"
```

One possible solution:

```python
correct_password = "python"
guess = input("Password: ")

while guess != correct_password:
    print("Wrong password.")
    guess = input("Password: ")

print("Welcome.")
```

Test it with:

```text
wrong
hello
python
```

The program should reject the first two guesses and accept the last one.

Now count the attempts:

```python
correct_password = "python"
guess = input("Password: ")
attempts = 1

while guess != correct_password:
    print("Wrong password.")
    guess = input("Password: ")
    attempts = attempts + 1

print("Welcome.")
print("Attempts:", attempts)
```

With the same test input, the important lines are:

```text
Wrong password.
Wrong password.
Welcome.
Attempts: 3
```

Do not limit the number of attempts yet. For today, focus on the loop condition and the update.

## Real-World Use

`while` loops are useful when a program does not know ahead of time how many repeats it needs.

Examples:

- keep asking for a password until it is correct
- keep showing a menu until the user chooses quit
- keep reading messages while there are messages left
- keep moving a game character while a key is pressed
- keep downloading pieces of a file until the file is complete
- keep checking whether a background task is finished

The pattern is:

```text
Repeat while some condition is still true.
```

Sometimes you know the exact number of repeats. Python has `for` loops for that, and you will learn them soon.

`while` loops are especially useful when the stopping point depends on something that changes while the program is running.

User input is a good early example. You cannot always know how many tries a person will need, so the program keeps asking while the answer is not acceptable.

## Recap

Today you learned:

- a `while` loop repeats code while a condition is true
- Python checks the condition before each loop run
- the indented lines under `while` are the loop body
- a counter is a variable used to track repetition
- many loops need a starting value, a condition, and an update
- the update should move the loop toward stopping
- forgetting the update can create an infinite loop
- indentation decides what repeats and what runs after the loop
- `while` is useful when you do not know the number of repeats ahead of time

Main idea:

```text
In every while loop, find the value that changes.
```

If nothing changes, the loop probably cannot end.

## Lesson Checklist

Before moving on, check that you can:

- write a `while` loop with a condition and an indented body
- explain that the condition is checked before each repeat
- use a counter to count up
- use a counter to count down
- update the loop value inside the loop
- identify the line that makes a loop stop eventually
- move a line out of the loop when it should run once
- explain why a missing update can create an infinite loop
- write a loop that keeps asking for input until the answer is accepted
- debug a loop by printing the value before and after the update

## Exercises

### Exercise 1

Predict the output before running the code.

```python
count = 1

while count <= 4:
    print(count)
    count = count + 1

print("Done")
```

### Exercise 2

Change this loop so it prints the numbers from `10` down to `1`.

```python
number = 1

while number <= 10:
    print(number)
    number = number + 1
```

### Exercise 3

Write a loop that prints:

```text
2
4
6
8
10
```

Start with:

```python
number = 2
```

Then use a `while` loop.

### Exercise 4

Fix the infinite loop.

Broken code:

```python
count = 1

while count <= 5:
    print("Counting:", count)
```

### Exercise 5

Fix the update direction.

This program should count down from `5` to `1`.

Broken code:

```python
number = 5

while number >= 1:
    print(number)
    number = number + 1
```

### Exercise 6

Fix the indentation.

The program should print `"Finished"` only once.

Broken code:

```python
count = 1

while count <= 3:
    print(count)
    count = count + 1
    print("Finished")
```

### Exercise 7

Write a loop that asks for a name until the user enters something other than an empty string.

Start with:

```python
name = input("Name: ")
```

Then keep asking while `name == ""`.

When the loop ends, print:

```text
Hello, NAME
```

### Exercise 8

Write a loop that keeps asking the user to type `"yes"` until they do.

When they finally type `"yes"`, print:

```text
Thanks.
```

### Exercise 9

Debug this program by adding print statements before and after the update.

```python
coins = 3

while coins > 0:
    print("You have", coins, "coins.")
    coins = coins - 1

print("No coins left.")
```

Your debug output should help you see how `coins` changes each time.

### Exercise 10

Write a small menu loop.

The program should show this menu:

```text
1. Say hello
2. Say goodbye
3. Quit
```

Ask the user for a choice.

Keep showing the menu while the choice is not `"3"`.

If the user chooses `"1"`, print:

```text
Hello.
```

If the user chooses `"2"`, print:

```text
Goodbye.
```

When the user chooses `"3"`, print:

```text
Menu closed.
```

Build it slowly:

1. Store the first choice.
2. Write the `while choice != "3":` loop.
3. Put the menu actions inside the loop.
4. Ask for a new choice at the end of the loop body.

## Tiny Win

You can now make a program repeat a task on purpose.

That means your programs are no longer limited to one pass from top to bottom.

## Tomorrow

Tomorrow you will learn how to avoid infinite loops.

Today you saw the basic warning sign:

```python
while condition:
    code
```

If nothing inside the loop changes the condition, the loop may never stop.

Tomorrow you will learn safer ways to design loops, test loops, and recover when a loop runs longer than expected.
