# Day 23: Avoiding Infinite Loops

**Focus:** Designing `while` loops that have a clear way to stop  
**You will practice:** tracing loop conditions, fixing unsafe updates, adding attempt limits, and debugging loop values safely  
**Estimated time:** 45-55 minutes

## Today's Goal

Today you will learn how to keep `while` loops under control.

Yesterday, you learned that a `while` loop repeats while a condition is true. Today, you will look closely at what happens when that condition never becomes false.

By the end of this lesson, you should be able to:

* explain what an infinite loop is
* recognize why a loop is not stopping
* fix counters that are missing an update
* spot updates that move in the wrong direction
* write safer input loops
* add an attempt limit when a loop should not run forever
* use temporary print statements to inspect loop values
* stop a running program with `Ctrl+C` in many terminals
* choose a clear exit condition before writing the loop

Some examples today are intentionally unsafe. They are labeled clearly as `Broken code (do not run)`. Read those examples and trace them by hand. Run only the fixed or guarded examples.

The main idea:

> A useful loop has a planned way to stop.

Some real programs run for a long time on purpose. A game, server, or menu may keep going until a user quits. That is different from a beginner loop that runs forever because the code forgot how to leave.

## The Big Idea

An infinite loop is a loop that keeps running because its condition never becomes false.

Broken code (do not run):

```python
count = 1

while count <= 3:
    print(count)
```

At first glance, this looks close to a normal counting loop. The problem is that `count` never changes.

Trace the loop without running it:

```text
count starts as 1.
The condition count <= 3 is True.
The loop prints 1.
Python checks the condition again.
count is still 1.
The condition is still True.
```

Python is not confused. It is following the exact instructions it was given. The code says to print `count`, but it never says to change `count`.

Fixed code:

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

Now the loop has progress. After each repeat, `count` moves closer to making this condition false:

```python
count <= 3
```

When `count` becomes `4`, the condition is false and the loop ends.

That is the habit to build:

```text
Find the condition.
Find the value that can change the condition.
Check whether the change moves toward stopping.
```

## The Mental Model

Think of a `while` loop as a question at the top of a path.

Before entering the loop, Python asks:

```text
Is the condition true?
```

If the answer is yes, Python runs the indented code. Then it goes back to the top and asks the same question again.

For the loop to end, something must eventually make the answer change from yes to no.

A safe loop usually has these pieces:

```text
Starting value
Condition
Repeated action
Change
Exit
```

Example:

```python
number = 1

while number <= 5:
    print(number)
    number = number + 1

print("Done.")
```

You should see:

```text
1
2
3
4
5
Done.
```

The pieces are:

```text
Starting value: number = 1
Condition: number <= 5
Repeated action: print(number)
Change: number = number + 1
Exit: number becomes 6
```

The exit is not always written as a separate `stop` line. Often, the update creates the exit by moving a value past the loop boundary.

When a loop does not stop, ask:

```text
What condition keeps this loop running?
What line is supposed to make that condition false?
Is that line actually running?
Is it changing the right value in the right direction?
```

Those questions catch many loop bugs.

## Try It Yourself

Create a file named `day-23/loop_safety.py`.

Code:

```python
count = 1

while count <= 5:
    print("Count:", count)
    count = count + 1

print("Finished.")
```

Before you run it, answer:

```text
What is the starting value?
What is the condition?
What line changes the value?
What value makes the loop stop?
```

Run it.

You should see:

```text
Count: 1
Count: 2
Count: 3
Count: 4
Count: 5
Finished.
```

Now try these safe changes one at a time.

Change the starting value:

```python
count = 3
```

Change the stopping point:

```python
while count <= 8:
```

Change the update:

```python
count = count + 2
```

Each time, predict the output before running the program.

Do not only ask:

```text
Did it work?
```

Ask:

```text
Why did it stop exactly there?
```

That question makes loops easier to trust.

## Common Mistake

Loop bugs often come from a mismatch between the condition and the update.

### Mistake 1: Forgetting to update the counter

Broken code (do not run):

```python
number = 1

while number <= 4:
    print(number)
```

The condition checks `number`, but nothing inside the loop changes `number`.

Fixed code:

```python
number = 1

while number <= 4:
    print(number)
    number = number + 1
```

You should see:

```text
1
2
3
4
```

### Mistake 2: Updating in the wrong direction

Broken code (do not run):

```python
number = 1

while number <= 4:
    print(number)
    number = number - 1
```

The condition says to keep going while `number <= 4`. The update makes `number` smaller:

```text
1
0
-1
-2
```

Those values are still less than or equal to `4`, so the loop moves away from its exit.

Fixed code:

```python
number = 1

while number <= 4:
    print(number)
    number = number + 1
```

### Mistake 3: Checking one variable but updating another

Broken code (do not run):

```python
count = 1
total = 0

while count <= 3:
    print("Total:", total)
    total = total + 1
```

The condition checks `count`, but only `total` changes. `count` stays `1`, so `count <= 3` stays true.

Fixed code:

```python
count = 1
total = 0

while count <= 3:
    print("Total:", total)
    total = total + 1
    count = count + 1
```

You should see:

```text
Total: 0
Total: 1
Total: 2
```

The variable in the condition does not always have to be updated directly, but something in the loop must be able to make the condition false.

### Mistake 4: Writing a condition with no useful boundary

Broken code (do not run):

```python
number = 1

while number > 0:
    print(number)
    number = number + 1
```

The update makes `number` bigger. The condition only asks whether `number` is greater than `0`. Starting at `1` and counting upward will not naturally make that condition false.

A counting loop needs a boundary.

Fixed code:

```python
number = 1

while number <= 5:
    print(number)
    number = number + 1
```

### Mistake 5: Asking for input only once

Broken code (do not run):

```python
answer = input("Type yes: ")

while answer != "yes":
    print("Please type yes.")
```

If the user does not type `"yes"` the first time, the loop complains forever. It never asks for a new answer.

Fixed code:

```python
answer = input("Type yes: ")

while answer != "yes":
    print("Please type yes.")
    answer = input("Type yes: ")

print("Thanks.")
```

The input line inside the loop gives the condition a chance to change.

## Debug It

Here is a countdown program with a loop bug.

It is supposed to count down from `5` to `1`, then print `"Go!"`.

Broken code (do not run):

```python
seconds = 5

while seconds > 0:
    print(seconds)
    seconds = seconds + 1

print("Go!")
```

Trace the important pieces:

```text
Condition: seconds > 0
Update: seconds = seconds + 1
```

The update makes `seconds` bigger:

```text
5
6
7
8
```

Those values are still greater than `0`, so the loop moves away from its exit.

When a loop is unsafe, do not run it just to "see what happens." Add a temporary guard while debugging.

Code:

```python
seconds = 5
checks = 0

while seconds > 0 and checks < 3:
    print("At top of loop:", seconds)
    print(seconds)
    seconds = seconds + 1
    print("After update:", seconds)
    checks = checks + 1

print("Stopped debug trace.")
```

You should see:

```text
At top of loop: 5
5
After update: 6
At top of loop: 6
6
After update: 7
At top of loop: 7
7
After update: 8
Stopped debug trace.
```

The guard `checks < 3` lets you inspect a few repeats without letting the broken loop run forever.

Now fix the real problem. A countdown should subtract `1`.

Fixed code:

```python
seconds = 5

while seconds > 0:
    print(seconds)
    seconds = seconds - 1

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

Temporary print statements help answer:

```text
What is the value right now?
Is it changing?
Is it changing in the right direction?
```

### How to stop a running loop

If you accidentally start an infinite loop, stay calm.

In many terminals, press:

```text
Ctrl+C
```

You may see a message that includes:

```text
KeyboardInterrupt
```

That means Python stopped because the user interrupted the program.

If you are using an editor, notebook, or online tool, look for a stop button, interrupt button, or square stop icon.

After the program stops, do not run it again immediately. First ask:

```text
What condition stayed true?
What value should have changed?
Where should the update go?
Would a temporary guard make this safe to inspect?
```

## Read the Docs

Look up Python's official documentation or tutorial section for the `while` statement.

For today, focus on the basic shape:

```python
while condition:
    statement
```

Notice that Python does not add a hidden stopping limit for a `while` loop. It keeps checking the condition you wrote.

That means the responsibility is yours:

```text
Write a condition that can become false.
```

You can also look up `KeyboardInterrupt`.

For now, remember:

```text
Ctrl+C can interrupt a running Python program in many terminals.
KeyboardInterrupt is the name Python gives to that interruption.
```

You do not need to handle `KeyboardInterrupt` in your own code yet. Just recognize it if you see it.

## Mini Challenge

Build a safer guessing loop.

Create a file named `day-23/guess_limit.py`.

The program should:

```text
Store a secret number.
Let the user guess.
Stop if the user guesses correctly.
Also stop after 3 wrong guesses.
```

Code:

```python
secret = "7"
guess = ""
attempts = 0

while guess != secret and attempts < 3:
    guess = input("Guess the number: ")
    attempts = attempts + 1

    if guess == secret:
        print("Correct.")
    else:
        print("Wrong.")

if guess == secret:
    print("You won.")
else:
    print("Out of guesses.")
```

Read the condition carefully:

```python
guess != secret and attempts < 3
```

The loop keeps going while both parts are true:

```text
The guess is still wrong.
There are attempts left.
```

This loop has two exit paths:

```text
The user guesses correctly.
The attempts reach 3.
```

Test it with a winning path and a losing path.

Try this:

```text
7
```

Then try this:

```text
1
2
3
```

The important safety idea is the attempt limit. Even if the user keeps guessing wrong, the loop still has a planned stop.

## Real-World Use

Infinite loops are not always mistakes. Some programs are designed to keep running until something tells them to stop.

Examples:

* a game keeps updating until the player quits
* a server keeps listening for requests until it is shut down
* a menu keeps showing until the user chooses quit
* a timer keeps running until it reaches zero
* a download keeps reading data until there is no more data left

The difference between a useful long-running loop and a broken infinite loop is the exit condition.

A game loop may run for a long time, but it still watches for events like:

```text
the player clicked quit
the window closed
the game ended
```

A menu loop may run for a long time, but it still checks:

```python
choice != "q"
```

Beginner programs usually need one of these clear stopping plans:

* stop after a counter reaches a limit
* stop when the user types a quit word
* stop when a correct answer is entered
* stop when attempts run out
* stop when there is no more data to process

Before you write a loop, choose the stopping plan.

## Recap

Today you learned that:

* an infinite loop keeps running because its condition never becomes false
* a `while` loop needs a clear exit path
* counters must be updated inside the loop
* the update must move toward the stopping condition
* input loops must give the user another chance to enter input
* a condition can be unsafe if it has no useful boundary
* temporary print statements can show how loop values change
* a temporary guard can make a broken loop safer to inspect
* `Ctrl+C` can interrupt many running Python programs in a terminal
* some long-running loops are useful when they have a planned exit

Main debugging question:

```text
What will make this condition false?
```

If you cannot answer that question, the loop is not ready yet.

## Lesson Checklist

Before moving on, check that you can:

* explain why a `while` loop might become infinite
* identify the condition that controls a loop
* identify the value that should change inside a loop
* fix a missing counter update
* fix an update that moves away from the exit
* fix an input loop that asks only once
* add an attempt limit to a loop
* use a temporary guard while debugging unsafe loop behavior
* explain what `Ctrl+C` and `KeyboardInterrupt` mean
* decide whether a loop has a clear stopping plan

## Exercises

### Exercise 1

Read this broken loop. Do not run it.

Broken code:

```python
count = 1

while count <= 3:
    print(count)
```

Why does it not stop?

Write a fixed version.

### Exercise 2

Fix the update direction.

This program should count from `1` to `5`. Do not run the broken version.

Broken code:

```python
number = 1

while number <= 5:
    print(number)
    number = number - 1
```

Write the fixed version.

### Exercise 3

Fix the countdown.

The program should print:

```text
5
4
3
2
1
Done
```

Do not run the broken version.

Broken code:

```python
number = 5

while number > 0:
    print(number)
    number = number + 1

print("Done")
```

### Exercise 4

Find the variable mismatch. Do not run the broken version.

Broken code:

```python
count = 1
score = 0

while count <= 4:
    print("Score:", score)
    score = score + 10
```

Which variable is checked by the condition?

Which variable is updated?

Write a fixed version that runs exactly four times.

### Exercise 5

Fix the input loop.

Do not run the broken version. If you ever start a loop like this by accident, interrupt it before fixing the code.

Broken code:

```python
word = input("Type stop: ")

while word != "stop":
    print("That was not stop.")

print("Stopped.")
```

The fixed program should keep asking until the user types `"stop"`.

### Exercise 6

Write a loop that keeps asking for a name until the user enters a non-empty string.

Start with:

```python
name = ""
```

Use this condition:

```python
while name == "":
```

When the loop ends, print:

```text
Hello, NAME
```

### Exercise 7

Add debug print statements to this safe loop.

```python
coins = 4

while coins > 0:
    print("Spend one coin.")
    coins = coins - 1

print("No coins left.")
```

Show the value of `coins` before and after the update.

### Exercise 8

Design the exit condition before writing code.

For each situation, write the condition that should keep the loop running.

Situation A:

```text
Keep asking while the password is wrong.
```

Situation B:

```text
Keep counting while count is less than or equal to 10.
```

Situation C:

```text
Keep showing a menu while choice is not "q".
```

### Exercise 9

Write a loop with an attempt limit.

The program should ask for the word `"python"`.

It should stop when:

```text
The user types python.
or
The user has tried 3 times.
```

You may use this condition:

```python
while guess != "python" and attempts < 3:
```

### Exercise 10

Look at this safe loop:

```python
number = 1

while number <= 5:
    print(number)
    number = number + 1
```

Answer these questions:

```text
What is the starting value?
What condition keeps the loop running?
What line changes the value?
What value finally stops the loop?
```

Now write one sentence explaining why this loop is not infinite.

## Tiny Win

You can now read a `while` loop with a sharper eye.

You are not only asking:

```text
What repeats?
```

You are asking:

```text
What makes it stop?
```

That question is one of the most useful habits in programming.

## Tomorrow

Tomorrow, you will learn `for` loops.

A `while` loop is useful when repetition depends on a condition:

```python
correct_password = "python"
password = ""
attempts = 0

while password != correct_password and attempts < 3:
    password = input("Password: ")
    attempts = attempts + 1
```

A `for` loop is often better when you already know the group of things or the number of steps:

```python
for number in range(1, 6):
    print(number)
```

With a `for` loop, Python handles the next value for you. That makes many counting loops easier to write and harder to make infinite by accident.
