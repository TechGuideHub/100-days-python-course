# Day 21: Why Loops Matter

**Focus:** Understanding the problem loops solve  
**You will practice:** spotting repeated work, describing loop patterns in plain English, identifying progress and stopping points, and previewing `while` loops  
**Estimated time:** 40-50 minutes

## Today's Goal

Today you will learn why loops exist.

You are not trying to memorize every loop rule yet. You are learning to recognize the kind of problem that needs a loop.

By the end of this lesson, you should be able to:

- recognize repeated actions in a program
- explain why copied code becomes fragile
- describe a loop in plain English
- identify what changes during a repeated action
- explain why a loop needs a stopping point
- recognize counting, waiting, and processing many items as loop patterns
- see why loops make programs easier to change

The main idea is:

> A loop lets a program repeat useful work without copying the same instructions again and again.

That idea prepares you for `while` loops tomorrow.

## The Big Idea

Many programs do something once.

Example:

```python
print("Check backpack.")
```

But real programs often need to do the same kind of thing more than once.

Examples:

- ask another quiz question
- count down before a game starts
- keep asking for a password until it is correct
- check every item in a shopping cart
- read every line in a file
- update a game screen again and again

Without loops, repeated actions often turn into copied code.

Example:

```python
print("Check backpack.")
print("Check backpack.")
print("Check backpack.")
```

That may look harmless. The problem appears when the repeated action changes.

If the message should become clearer, every copy has to change:

```python
print("Check your backpack before leaving.")
print("Check your backpack before leaving.")
print("Check your backpack before leaving.")
```

Three copies are annoying. Thirty copies are easy to break.

A loop keeps the repeated idea in one place.

Instead of thinking:

```text
Do this.
Do this.
Do this.
Do this.
```

Think:

```text
Repeat this while it is still needed.
```

or:

```text
Do this for each thing in a group.
```

Loops are not only about saving typing. They are about making repeated behavior easier to understand, test, and change.

## The Mental Model

Think of a loop as a checkpoint a program can return to.

An `if` statement asks a question once:

```text
If the door is open:
    walk through
```

A loop asks a question, does some work, then comes back and asks again:

```text
While the room is still messy:
    put one thing away
```

The loop does not have to run forever. Each pass should move the situation closer to being done.

At first:

```text
The room is messy.
```

So the loop runs.

After one pass:

```text
One thing has been put away.
```

Then the loop checks again.

Eventually:

```text
The room is not messy anymore.
```

Now the loop stops.

A useful loop usually has these parts:

```text
Starting situation
Question to check
Repeated action
Something that changes
Stopping point
```

Example:

```text
Start with 1
While the number is 5 or less:
    say the number
    add 1 to the number
Stop when the number becomes 6
```

The changing part matters:

```text
add 1 to the number
```

Without a changing part, the loop may never stop.

Main idea:

```text
A loop repeats, but a healthy loop also makes progress.
```

## Try It Yourself

Start without Python.

Choose one repeated task from everyday life:

- washing dishes
- packing a bag
- checking messages
- watering plants
- practicing a song
- counting coins

Write it as copied instructions first.

Example:

```text
Wash plate 1
Wash plate 2
Wash plate 3
Wash plate 4
Wash plate 5
```

Now rewrite it as a loop idea:

```text
While there are dirty plates:
    wash one plate
```

Notice the difference.

The copied version depends on knowing the exact number of plates. The loop version depends on a condition:

```text
Are there dirty plates left?
```

Now try a tiny Python preview.

Create a file named:

```text
day-21/repetition_preview.py
```

Code:

```python
count = 1

while count <= 3:
    print("Practice", count)
    count = count + 1
```

You should see:

```text
Practice 1
Practice 2
Practice 3
```

Do not worry about mastering the syntax today. Read it as:

```text
Start count at 1.
While count is 3 or less:
    print a practice message
    add 1 to count
```

The loop stops because `count` changes.

## Common Mistake

### Mistake 1: Thinking loops are only for large amounts of repetition

Beginners often think:

```text
I only need a loop when something repeats 100 times.
```

Loops are useful much earlier than that.

Even three repeated blocks can be a clue.

Example:

```python
print("Send reminder to Asha")
print("Send reminder to Ben")
print("Send reminder to Cara")
```

The repeated action is:

```text
Send a reminder.
```

The part that changes is:

```text
The person's name.
```

When you see the same shape several times, pause and ask:

```text
Is this really several separate ideas, or one idea repeated with small changes?
```

That question is the beginning of loop thinking.

### Mistake 2: Forgetting that a loop needs progress

A loop should not only repeat. It should move toward stopping.

Broken code:

```python
count = 1

while count <= 3:
    print(count)
```

Do not run that version. The condition stays true because `count` never changes.

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

The line that adds `1` is what lets the loop finish.

## Debug It

Here is a loop idea with a bug:

```text
Start tasks_left at 3

While tasks_left is greater than 0:
    finish one task
```

The problem is not the goal. The goal makes sense.

The problem is that `tasks_left` never changes. The loop keeps acting as if there are still 3 tasks left.

Ask this debugging question:

```text
What changes each time through the loop?
```

If the answer is "nothing," the loop is probably broken.

Fixed idea:

```text
Start tasks_left at 3

While tasks_left is greater than 0:
    finish one task
    subtract 1 from tasks_left
```

Code:

```python
tasks_left = 3

while tasks_left > 0:
    print("Finish one task")
    tasks_left = tasks_left - 1

print("Done")
```

You should see:

```text
Finish one task
Finish one task
Finish one task
Done
```

Debugging a loop often starts with two questions:

```text
What condition keeps this going?
What action moves it toward stopping?
```

## Read the Docs

Find Python's official tutorial section about control flow:

```text
https://docs.python.org/3/tutorial/controlflow.html
```

You may see `if`, `for`, and `while` near each other.

For today, keep the reading light. Look for the idea that these tools control the path a program takes.

Use this beginner translation:

```text
if      choose whether to do something
while   repeat while a condition is true
for     repeat over a group of things
```

You already know the first one. Tomorrow you begin the second.

## Mini Challenge

Design a small menu that keeps running until the user chooses to quit.

Use plain English or pseudo-code. The menu has three choices:

```text
1. Say hello
2. Show a fun fact
3. Quit
```

Start with this:

```text
Set choice to empty

While choice is not "3":
    show the menu
    ask for a choice
```

Then add what should happen for each choice.

Example:

```text
If choice is "1":
    say hello
```

The goal is not perfect Python yet. The goal is to describe this pattern:

```text
Keep going until the user chooses to stop.
```

That is a classic `while` loop situation.

## Real-World Use

Loops appear whenever a program needs repeated behavior.

Examples:

- a login screen asks again when the password is wrong
- a timer counts down until it reaches zero
- a game updates positions many times per second
- a music app moves to the next song
- a bank program checks many transactions
- a calendar app sends reminders to several people
- a store adds each item price to an order total
- a file tool reads one line after another

The repeated action may be small. The number of repetitions may be known or unknown.

The loop idea stays the same:

```text
Do the same kind of work again under clear conditions.
```

## Recap

Today you learned that:

- loops are for repeated actions
- copied repeated code is fragile
- a loop keeps repeated behavior in one place
- some loops count
- some loops wait until something changes
- some loops process many items
- a useful loop needs progress
- a useful loop needs a stopping point

Main idea:

```text
A loop is controlled repetition.
```

## Lesson Checklist

Before moving on, check that you can:

- explain why copying repeated code can cause mistakes
- describe a loop without using Python syntax
- identify the repeated action in a small example
- identify what changes each time through a loop
- explain why a loop needs a stopping point
- recognize a counting loop idea
- recognize a "keep asking until" loop idea
- recognize a "for each item" loop idea
- explain why loops make code easier to change

## Exercises

### Exercise 1

Write three repeated actions from your day.

Examples:

```text
Check each message.
Wash each cup.
Practice each spelling word.
```

For each one, write the repeated action in this format:

```text
While or For each:
    action
```

### Exercise 2

Rewrite this copied code as a loop idea:

```python
print("Drink water.")
print("Drink water.")
print("Drink water.")
print("Drink water.")
```

Use this format:

```text
Repeat 4 times:
    Drink water.
```

### Exercise 3

This copied code prints a countdown:

```python
print(5)
print(4)
print(3)
print(2)
print(1)
print("Go")
```

Write a loop idea for it.

Start like this:

```text
Start at 5
While the number is greater than 0:
```

Then finish the repeated action and the change.

### Exercise 4

Predict the output:

```python
number = 1

while number <= 4:
    print(number)
    number = number + 1
```

Do not run it first. Follow the value of `number` with your eyes.

### Exercise 5

Debug this loop idea:

```text
Start attempts at 1

While attempts is less than or equal to 3:
    ask for password
```

What is missing?

Write a fixed version in plain English.

### Exercise 6

Write a loop idea for this situation:

```text
Keep asking the user to type "yes" until they actually type "yes".
```

Start with:

```text
Set answer to empty

While ...
    ...
```

### Exercise 7

A quiz program asks five questions.

For each question, it should:

```text
ask the question
check the answer
add 1 to the score if correct
```

Write this as one repeated block. Do not write five separate question blocks.

### Exercise 8

Look at this repeated code:

```python
print("Email sent to Asha")
print("Email sent to Ben")
print("Email sent to Cara")
print("Email sent to Dev")
```

Answer in plain English:

```text
What is the repeated action?
What changes each time?
```

### Exercise 9

Imagine a shopping cart with many prices.

Write a loop idea for adding all prices to a total.

Start like this:

```text
Set total to 0

For each price in the cart:
```

Then finish the idea.

### Exercise 10

Read this preview:

```python
number = 1

while number <= 3:
    print("Practice")
    number = number + 1
```

Now imagine changing `3` to `5`.

Answer:

```text
What changes in the output?
What stays the same in the code?
```

That is one reason loops are useful.

## Tiny Win

Before today, repeated code may have looked normal.

Now you can see the pattern underneath it:

```text
One action, repeated under a condition.
```

That is loop thinking.

## Tomorrow

Tomorrow you will learn `while` loops.

A `while` loop repeats as long as its condition is true:

```text
while condition:
    repeated action
```

The important question will be:

```text
What will eventually make the condition false?
```

That question is how you keep repetition under control.
