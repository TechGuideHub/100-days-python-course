# Day 25: `range()`

**Focus:** Creating number sequences for `for` loops  
**You will practice:** using `range()`, choosing start and stop values, using steps, counting down, and fixing off-by-one mistakes  
**Estimated time:** 40-50 minutes

## Today's Goal

Today you will learn how to use `range()` with a `for` loop.

Yesterday, your `for` loops moved through sequences you could see:

```python
for name in ["Asha", "Ben", "Cara"]:
    print("Hello,", name)
```

Sometimes you do not want to write every item by hand. You just want Python to count.

Example:

```python
for number in range(5):
    print(number)
```

You should see:

```text
0
1
2
3
4
```

That output may look surprising at first. The code says `range(5)`, but the loop stops at `4`.

That is not a mistake.

The most important rule for today is:

> The stop value is not included.

By the end of this lesson, you should be able to:

- use `range()` inside a `for` loop
- explain why `range(5)` starts at `0`
- explain why `range(5)` stops before `5`
- use `range(start, stop)`
- use `range(start, stop, step)`
- count upward and downward
- spot off-by-one mistakes
- debug a loop by printing the numbers it receives
- connect `range()` to positions in text

The main idea is:

> `range()` gives a `for` loop a controlled sequence of numbers.

Broken examples are labeled clearly. Study them first; run them only when you want to see the error or the wrong behavior.

## The Big Idea

`range()` makes numbers for a loop.

Code:

```python
for number in range(5):
    print(number)
```

Read it like this:

```text
For each number from 0 up to, but not including, 5:
    print the number
```

You should see:

```text
0
1
2
3
4
```

There are five numbers, but they are not `1, 2, 3, 4, 5`.

They are:

```text
0, 1, 2, 3, 4
```

Python often counts from zero because it often cares about positions.

You will see this more clearly tomorrow when you work with text:

```text
P y t h o n
0 1 2 3 4 5
```

For today, hold onto this:

```text
range(5) means five numbers, starting at 0 and stopping before 5.
```

If you want the loop to print `1` through `5`, use:

```python
for number in range(1, 6):
    print(number)
```

You should see:

```text
1
2
3
4
5
```

The stop value is `6` because `6` is the first number the range will not use.

## The Mental Model

Think of `range()` as a number maker with three possible instructions:

```text
start here
stop before here
move by this much
```

The full shape is:

```python
range(start, stop, step)
```

The pieces mean:

```text
start: where counting begins
stop: the boundary that is not included
step: how much to move each time
```

If you write only one number:

```python
range(5)
```

Python treats it like:

```python
range(0, 5, 1)
```

That means:

```text
start at 0
stop before 5
move by 1
```

So the loop receives:

```text
0, 1, 2, 3, 4
```

Here are a few common shapes:

| Code | Starts at | Stops before | Step | Numbers |
| --- | ---: | ---: | ---: | --- |
| `range(5)` | `0` | `5` | `1` | `0, 1, 2, 3, 4` |
| `range(3)` | `0` | `3` | `1` | `0, 1, 2` |
| `range(1, 5)` | `1` | `5` | `1` | `1, 2, 3, 4` |
| `range(2, 10, 2)` | `2` | `10` | `2` | `2, 4, 6, 8` |
| `range(5, 0, -1)` | `5` | `0` | `-1` | `5, 4, 3, 2, 1` |

When a range feels confusing, say the three instructions out loud.

Example:

```python
range(2, 11, 2)
```

Means:

```text
start at 2
stop before 11
move by 2
```

So the numbers are:

```text
2, 4, 6, 8, 10
```

## Try It Yourself

Create a file named:

```text
day-25/range_practice.py
```

Code:

```python
for number in range(5):
    print(number)
```

Before you run it, predict the output.

Run the file from your course folder:

```bash
python day-25/range_practice.py
```

If your computer uses `py`, use:

```bash
py day-25/range_practice.py
```

If your computer uses `python3`, use:

```bash
python3 day-25/range_practice.py
```

You should see:

```text
0
1
2
3
4
```

Now change the range:

```python
for number in range(3):
    print(number)
```

Predict first, then run it.

You should see:

```text
0
1
2
```

Now try a start and stop:

```python
for number in range(1, 4):
    print(number)
```

You should see:

```text
1
2
3
```

The stop value `4` is not printed.

Now try a step:

```python
for number in range(2, 11, 2):
    print(number)
```

You should see:

```text
2
4
6
8
10
```

Finally, try counting down:

```python
for number in range(5, 0, -1):
    print(number)

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

The step is `-1`, so Python moves downward. The stop value is still not included, so `range(5, 0, -1)` stops before `0`.

## Common Mistake

### Mistake 1: Expecting `range(5)` to mean `1` through `5`

Code:

```python
for number in range(5):
    print(number)
```

You might expect:

```text
1
2
3
4
5
```

But Python prints:

```text
0
1
2
3
4
```

`range(5)` starts at `0` and stops before `5`.

If you want `1` through `5`, write:

```python
for number in range(1, 6):
    print(number)
```

The stop value is `6` because `6` is not included.

### Mistake 2: Forgetting that the stop value is not included

This loop does not print `10`:

```python
for number in range(1, 10):
    print(number)
```

You should see:

```text
1
2
3
4
5
6
7
8
9
```

If `10` should appear, use:

```python
for number in range(1, 11):
    print(number)
```

Off-by-one bugs often happen here. The loop is close, but it stops one number earlier than you meant.

### Mistake 3: Using a step of zero

Broken code:

```python
for number in range(1, 5, 0):
    print(number)
```

Python cannot move by zero. If the step were zero, the number would never change.

Use a positive step to count up:

```python
for number in range(1, 5, 1):
    print(number)
```

Use a negative step to count down:

```python
for number in range(5, 1, -1):
    print(number)
```

### Mistake 4: Counting down with a positive step

Broken code:

```python
for number in range(5, 1):
    print(number)
```

This code runs, but it prints nothing.

The start is `5`. The stop value is `1`. The default step is `1`, so Python would move upward. Since `5` is already past the stopping boundary, there are no numbers to give the loop.

Fixed code:

```python
for number in range(5, 0, -1):
    print(number)
```

You should see:

```text
5
4
3
2
1
```

The negative step moves downward. The stop value `0` is not included.

## Debug It

Here is a program with an off-by-one bug.

It is supposed to print:

```text
Seat 1
Seat 2
Seat 3
Seat 4
Seat 5
```

Broken code:

```python
for seat in range(1, 5):
    print("Seat", seat)
```

It prints:

```text
Seat 1
Seat 2
Seat 3
Seat 4
```

The missing line is:

```text
Seat 5
```

The bug is the stop value.

This range:

```python
range(1, 5)
```

starts at `1` and stops before `5`, so it never gives the loop the number `5`.

Fixed code:

```python
for seat in range(1, 6):
    print("Seat", seat)
```

When a `range()` loop gives the wrong numbers, ask:

- What number does it start with?
- What number does it stop before?
- What is the step?

You can also make the loop show the values it receives.

Code:

```python
for seat in range(1, 6):
    print("Debug seat value:", seat)
    print("Seat", seat)
```

You should see:

```text
Debug seat value: 1
Seat 1
Debug seat value: 2
Seat 2
Debug seat value: 3
Seat 3
Debug seat value: 4
Seat 4
Debug seat value: 5
Seat 5
```

Temporary debug prints are useful because they show what Python is actually doing. You do not have to guess.

## Read the Docs

Find Python's official documentation for `range`:

```text
https://docs.python.org/3/library/stdtypes.html#ranges
```

The documentation describes `range` as an immutable sequence type. That wording is formal, but the beginner version is:

```text
range() represents a sequence of numbers that does not change.
```

Try this:

```python
print(range(5))
```

You may see:

```text
range(0, 5)
```

That does not print each number. To see the numbers one at a time, use a loop:

```python
for number in range(5):
    print(number)
```

You can also turn a range into a list when you want to inspect it:

```python
print(list(range(5)))
print(list(range(1, 6)))
print(list(range(2, 11, 2)))
```

You should see:

```text
[0, 1, 2, 3, 4]
[1, 2, 3, 4, 5]
[2, 4, 6, 8, 10]
```

You have not studied lists deeply yet. For today, `list(range(...))` is just a quick way to peek at what numbers the range would give to a loop.

## Mini Challenge

Create a file named:

```text
day-25/countdown.py
```

Build a small countdown program.

The program should:

- ask the user for a starting number
- count down from that number to `1`
- print `"Go!"` at the end

Start with a fixed number:

```python
start = 5

for number in range(start, 0, -1):
    print(number)

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

Now ask the user:

```python
start = int(input("Start countdown at: "))

for number in range(start, 0, -1):
    print(number)

print("Go!")
```

For input `3`, you should see:

```text
Start countdown at: 3
3
2
1
Go!
```

For input `1`, you should see:

```text
Start countdown at: 1
1
Go!
```

Do not worry yet about what happens if the user types a word instead of a number. You will learn stronger input protection later.

For today, focus on the range:

```python
range(start, 0, -1)
```

It starts at the user's number, stops before `0`, and moves by `-1`.

## Real-World Use

`range()` is useful when a program needs numbered repetition.

Examples:

- print ticket numbers
- repeat a practice question five times
- count down a timer
- number the rounds in a game
- print every even number in a small range
- check a fixed number of attempts
- create simple rows or columns
- work with positions in text or lists

That last idea matters for tomorrow.

Text has characters:

```text
code
```

Those characters have positions:

```text
c o d e
0 1 2 3
```

`range()` can help you think about those positions.

Code:

```python
word = "code"

for position in range(4):
    print(position)
```

You should see:

```text
0
1
2
3
```

Those numbers match the positions of the letters in `"code"`.

You do not need to use the positions with the word yet. Just notice the connection:

```text
range(4) gives 0, 1, 2, 3
"code" has four letters at positions 0, 1, 2, 3
```

That is why counting from zero becomes useful.

## Recap

Today you learned that:

- `range()` gives a `for` loop a sequence of numbers
- `range(5)` gives `0, 1, 2, 3, 4`
- Python often counts from zero
- the stop value is not included
- `range(start, stop)` lets you choose where counting begins
- `range(start, stop, step)` lets you choose how counting moves
- a positive step counts upward
- a negative step counts downward
- a step of zero is not allowed
- off-by-one bugs often come from forgetting the stop value rule
- debug prints can show the numbers a loop actually receives

Main idea:

```text
start here
stop before here
move by this much
```

That sentence solves many `range()` mistakes.

## Lesson Checklist

Before moving on, check that you can:

- write a `for` loop with `range()`
- predict the output of `range(5)`
- explain why the stop value is not included
- use `range(start, stop)` to print a chosen set of numbers
- use `range(start, stop, step)` to skip numbers
- count down with a negative step
- fix an off-by-one range mistake
- explain why `range(1, 5, 0)` is not allowed
- use `list(range(...))` to inspect a range
- add a temporary debug print inside a loop

## Exercises

### Exercise 1

Predict the output before running the code.

```python
for number in range(4):
    print(number)
```

Write the output first. Then run it.

### Exercise 2

Write a loop that prints:

```text
1
2
3
4
5
```

Use `range()`. Remember that the stop value is not included.

### Exercise 3

Write a loop that prints:

```text
10
11
12
13
14
15
```

What should the stop value be?

### Exercise 4

Write a loop that prints the even numbers:

```text
2
4
6
8
10
```

Use a step of `2`.

### Exercise 5

Write a countdown loop that prints:

```text
3
2
1
Done
```

Use a negative step.

### Exercise 6

Fix this loop so it prints `1` through `10`.

```python
for number in range(1, 10):
    print(number)
```

### Exercise 7

Fix this loop so it counts down from `5` to `1`.

```python
for number in range(5, 1):
    print(number)
```

### Exercise 8

Predict the output.

```python
for number in range(3, 12, 3):
    print(number)
```

Then run it. Explain why `12` does or does not appear.

### Exercise 9

Write a loop that prints:

```text
Attempt 1
Attempt 2
Attempt 3
```

Use:

```python
range(1, 4)
```

Then change it to print five attempts.

### Exercise 10

Use `list(range(...))` to inspect these ranges:

```python
print(list(range(6)))
print(list(range(1, 6)))
print(list(range(0, 10, 2)))
print(list(range(10, 0, -2)))
```

For each one, write:

```text
start:
stop before:
step:
numbers:
```

### Exercise 11

Write a loop that prints the positions of a four-letter word:

```text
0
1
2
3
```

Use:

```python
range(4)
```

This prepares you for tomorrow's lesson about looping through text.

### Exercise 12

Debug this program.

It is supposed to print:

```text
Box 1
Box 2
Box 3
Box 4
```

Broken code:

```python
for box in range(1, 4):
    print("Box", box)
```

Fix the range. Then add a temporary debug print:

```python
print("Debug box:", box)
```

Run it again and watch the values.

## Tiny Win

You can now ask Python for exactly the numbers a loop needs.

That gives you a clean way to control repetition:

```python
for number in range(1, 6):
    print(number)
```

Start. Stop before. Step.

That is the whole shape.

## Tomorrow

Tomorrow you will loop through text.

Text is made of characters:

```text
Python
```

A loop can visit those characters one at a time.

You will also see why today's zero-based counting matters:

```text
P y t h o n
0 1 2 3 4 5
```

`range()` taught you how Python counts positions. Tomorrow, those positions will belong to letters.
