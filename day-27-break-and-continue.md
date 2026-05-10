# Day 27: `break` and `continue`

**Focus:** Leaving a loop early and skipping one loop turn  
**You will practice:** using `break` in quit and search loops, using `continue` to ignore unwanted input, tracing loop flow, and debugging skipped updates  
**Estimated time:** 40-50 minutes

## Today's Goal

Today you will learn two small statements that change the path through a loop:

```python
break
continue
```

By the end of this lesson, you should be able to:

- use `break` to leave a loop early
- use `continue` to skip the rest of the current loop turn
- explain the difference between stopping a loop and skipping one repeat
- write a simple input loop that stops when the user types a quit word
- ignore blank input without ending the whole program
- stop a search as soon as the answer is found
- debug loops that stop too soon, keep going too long, or skip important code

The main idea is:

> `break` leaves the loop. `continue` moves to the next turn of the same loop.

Broken examples are labeled clearly. Read them first; run them only when you want to study the wrong behavior or the error.

## The Big Idea

A loop normally follows its usual path.

A `while` loop checks its condition again and again:

```python
count = 1

while count <= 3:
    print(count)
    count = count + 1
```

A `for` loop moves through each item in a sequence:

```python
for letter in "cat":
    print(letter)
```

Most of the time, that normal path is exactly what you want. Sometimes, though, a loop needs a clearer instruction from inside the loop body.

Use `break` when the loop is finished early.

Code:

```python
for letter in "python":
    if letter == "h":
        break

    print(letter)

print("Done")
```

You should see:

```text
p
y
t
Done
```

The loop stopped when it reached `"h"`. It did not print `"h"`, and it did not continue to `"o"` or `"n"`.

Use `continue` when only the current loop turn should be skipped.

Code:

```python
for letter in "python":
    if letter == "h":
        continue

    print(letter)

print("Done")
```

You should see:

```text
p
y
t
o
n
Done
```

This time the loop did not stop. It skipped the print line only for `"h"`, then kept going.

Keep the difference short:

```text
break      stop the whole loop
continue   skip this one turn
```

## The Mental Model

Think of each loop turn as one trip through the loop body.

Normally, Python starts at the top of the loop body and runs each indented line in order.

With `break`, Python leaves the loop immediately:

```text
Start this loop turn.
Reach break.
Leave the loop completely.
Continue after the loop.
```

With `continue`, Python skips the rest of the current turn:

```text
Start this loop turn.
Reach continue.
Skip the remaining loop body.
Move to the next loop turn.
```

In a `for` loop, `continue` moves to the next item.

In a `while` loop, `continue` moves back to the condition check. That detail matters because a `while` loop often depends on an update line.

Code:

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

The loop did reach `3`, but `continue` skipped the print line for that one turn.

The update came before `continue`:

```python
number = number + 1
```

That is important. If a `while` loop uses `continue` before changing the value that controls the loop, the loop can get stuck.

## Try It Yourself

Create a file named:

```text
day-27/break_continue_practice.py
```

Code:

```python
while True:
    word = input("Type a word, or quit: ")

    if word == "quit":
        break

    print("Word:", word)

print("Goodbye.")
```

Run the file from your course folder:

```bash
python day-27/break_continue_practice.py
```

If your computer uses `py`, use:

```bash
py day-27/break_continue_practice.py
```

If your computer uses `python3`, use:

```bash
python3 day-27/break_continue_practice.py
```

Try this input:

```text
apple
python
quit
```

You should see:

```text
Word: apple
Word: python
Goodbye.
```

Now ignore blank input:

```python
while True:
    word = input("Type a word, or quit: ")

    if word == "quit":
        break

    if word == "":
        continue

    print("Word:", word)

print("Goodbye.")
```

Run it again. Press Enter without typing a word. The blank input should be ignored, and the loop should ask again.

Now add one more rule before the `print()` line:

```python
if word == "skip":
    continue
```

Test with:

```text
hello
skip
world
quit
```

The program should print `hello` and `world`, but not `skip`.

Ask yourself:

```text
Which input stops the whole loop?
Which input skips only one loop turn?
Which input reaches the print line?
```

Those questions are the heart of today's lesson.

## Common Mistake

### Mistake 1: Thinking `break` skips only one line

This program does not just skip the print for `"k"`. It leaves the loop.

Code:

```python
for letter in "desktop":
    if letter == "k":
        break

    print(letter)

print("After loop")
```

You should see:

```text
d
e
s
After loop
```

When Python reaches `break`, the loop is done. It does not come back for `"t"`, `"o"`, or `"p"`.

Remember:

```text
break means leave the loop, not skip one print.
```

### Mistake 2: Using `continue` when the search should stop

This program keeps going after it finds `"x"`:

```python
for letter in "boxcar":
    if letter == "x":
        continue

    print(letter)
```

You should see:

```text
b
o
c
a
r
```

It skipped `"x"`, but it did not stop the loop.

If the goal is to stop searching as soon as `"x"` is found, use `break`.

Code:

```python
for letter in "boxcar":
    if letter == "x":
        break

    print(letter)
```

You should see:

```text
b
o
```

Use `continue` when the loop should keep going. Use `break` when the loop should be finished.

### Mistake 3: Putting important code after `continue`

This program runs, but one line never runs:

```python
for number in range(1, 6):
    if number == 3:
        continue
        print("Skipping 3")

    print(number)
```

The unreachable line is:

```python
print("Skipping 3")
```

Once Python reaches `continue`, it jumps to the next loop turn. It does not run later lines in the same indented block.

Fixed code:

```python
for number in range(1, 6):
    if number == 3:
        print("Skipping 3")
        continue

    print(number)
```

Put any message or update that must happen before the `continue`.

### Mistake 4: Using `continue` too early in a `while` loop

Broken code (do not run):

```python
number = 1

while number <= 5:
    if number == 3:
        continue

    print(number)
    number = number + 1
```

This loop gets stuck at `3`.

When `number == 3`, Python reaches `continue` before this update:

```python
number = number + 1
```

The update never runs, so `number` stays `3` forever.

Fixed code:

```python
number = 1

while number <= 5:
    if number == 3:
        number = number + 1
        continue

    print(number)
    number = number + 1
```

You should see:

```text
1
2
4
5
```

Another clean version updates near the top:

```python
number = 0

while number < 5:
    number = number + 1

    if number == 3:
        continue

    print(number)
```

In a `while` loop, check whether `continue` skips the update your loop needs in order to stop.

## Debug It

Here is a broken program.

It is supposed to:

```text
ignore blank names
stop when the user types done
greet every other name
```

Broken code:

```python
while True:
    name = input("Name: ")

    if name == "":
        break

    if name == "done":
        continue

    print("Hello,", name)

print("Finished.")
```

Try this input in your head:

```text
Asha

Ben
done
```

The blank line is supposed to be ignored, but the program stops there.

This part is wrong:

```python
if name == "":
    break
```

Blank input should skip only the current loop turn.

This part is wrong too:

```python
if name == "done":
    continue
```

Typing `"done"` should stop the whole loop.

Fixed code:

```python
while True:
    name = input("Name: ")

    if name == "done":
        break

    if name == "":
        continue

    print("Hello,", name)

print("Finished.")
```

Now the behavior matches the goal:

```text
Asha      greet
blank     ignore
Ben       greet
done      stop
```

When debugging `break` and `continue`, ask:

- Which input should end the whole loop?
- Which input should skip only this one turn?
- Which lines are skipped when `continue` runs?
- Which line runs immediately after `break` leaves the loop?

Small temporary print statements can also help.

Code:

```python
while True:
    name = input("Name: ")

    print("Debug: name is", name)

    if name == "done":
        print("Debug: breaking")
        break

    if name == "":
        print("Debug: continuing")
        continue

    print("Hello,", name)

print("Finished.")
```

Debug messages are temporary. Once the loop behaves correctly, remove them.

## Read the Docs

Find Python's official tutorial section for `break` and `continue`:

```text
https://docs.python.org/3/tutorial/controlflow.html#break-and-continue-statements-and-else-clauses-on-loops
```

The documentation uses formal wording. For today, translate it this way:

```text
break      leave the nearest loop around it
continue   go to the next cycle of the nearest loop around it
```

The phrase "nearest loop" matters. `break` and `continue` affect the loop they are inside.

Right now, most of your examples have one loop at a time. Later, when you see loops inside loops, this detail will matter more.

For now, keep this practical version:

```text
break and continue control the loop around them.
```

## Mini Challenge

Create a file named:

```text
day-27/find_letter.py
```

Build a small text scanner.

The program should:

- ask the user for a word
- ask the user for a letter to find
- look through the word one character at a time
- stop as soon as it finds the letter
- print whether the letter was found

Start with this:

```python
word = input("Word: ")
target = input("Letter to find: ")

found = False

for letter in word:
    if letter == target:
        found = True
        break

if found:
    print("Found it.")
else:
    print("Not found.")
```

Try:

```text
Word: notebook
Letter to find: b
```

You should see:

```text
Found it.
```

Try:

```text
Word: notebook
Letter to find: z
```

You should see:

```text
Not found.
```

The useful part is:

```python
if letter == target:
    found = True
    break
```

Once the program finds the target letter, it does not need to keep searching.

Now add one more detail. Skip spaces while searching:

```python
text = input("Text: ")
target = input("Letter to find: ")

found = False

for letter in text:
    if letter == " ":
        continue

    if letter == target:
        found = True
        break

if found:
    print("Found it.")
else:
    print("Not found.")
```

This version uses both tools:

```text
continue   ignore spaces and keep searching
break      stop when the target is found
```

Test with:

```text
Text: red kite
Letter to find: k
```

Then test with:

```text
Text: red kite
Letter to find: z
```

Predict each result before you run it.

## Real-World Use

`break` is useful when a loop has already done enough.

Examples:

- stop asking for commands when the user types `"quit"`
- stop checking letters when a matching letter is found
- stop a game loop when the player chooses to exit
- stop checking attempts after the correct password is entered
- stop reading input when a blank line means the user is finished

`continue` is useful when one loop turn should be ignored.

Examples:

- skip blank input
- skip spaces in a piece of text
- skip numbers that do not match a rule
- skip a menu choice that is empty
- skip one special value while still printing the rest

The difference is small but practical:

```text
break      I am done with this loop.
continue   I am done with this one turn.
```

A menu may stop on `"quit"`, skip blank input, and handle normal commands. A search may skip characters that do not matter, but stop once the target is found.

## Recap

Today you learned that:

- `break` leaves a loop immediately
- `continue` skips the rest of the current loop turn
- after `break`, Python runs the first line after the loop
- after `continue`, Python moves to the next loop turn
- `break` is useful for quit commands and search loops
- `continue` is useful for ignoring blank or unwanted values
- `while True` can be reasonable when the loop has a clear `break`
- in a `while` loop, `continue` can accidentally skip the update
- code after `break` or `continue` in the same block may not run

The shortest version:

```text
break      leave the loop
continue   skip to the next turn
```

When you are unsure which one to use, ask:

```text
Should the whole loop stop?
Or should only this one repeat be skipped?
```

## Lesson Checklist

Before moving on, check that you can:

- explain what `break` does
- explain what `continue` does
- choose `break` for a quit command
- choose `break` for a search that can stop early
- choose `continue` for blank input
- choose `continue` for a value that should be ignored
- tell which line runs after a loop ends
- tell which lines are skipped after `continue`
- spot a `while` loop update that `continue` might skip
- fix a loop that uses `break` and `continue` in the wrong places

## Exercises

### Exercise 1

Predict the output before running the code.

```python
for letter in "garden":
    if letter == "d":
        break

    print(letter)

print("Done")
```

### Exercise 2

Predict the output.

```python
for letter in "garden":
    if letter == "d":
        continue

    print(letter)

print("Done")
```

Which letter is skipped? Does the loop stop?

### Exercise 3

Change this program so it stops when it reaches `4`.

```python
for number in range(1, 8):
    print(number)
```

It should print:

```text
1
2
3
```

### Exercise 4

Change this program so it skips `4` but keeps going.

```python
for number in range(1, 8):
    print(number)
```

It should print:

```text
1
2
3
5
6
7
```

### Exercise 5

Write a loop that asks the user for words.

The loop should stop when the user types:

```text
done
```

For every other word, print:

```text
You typed: WORD
```

Use `break`.

### Exercise 6

Improve Exercise 5.

If the user presses Enter without typing anything, ignore that turn and ask again.

Use `continue`.

### Exercise 7

Debug this program. Do not run the broken version.

It should skip `3` and then print `4` and `5`.

Broken code:

```python
number = 1

while number <= 5:
    if number == 3:
        continue

    print(number)
    number = number + 1
```

What makes it get stuck?

Write a fixed version.

### Exercise 8

Write a program that searches for the letter `"e"` in a word.

Start with:

```python
word = input("Word: ")
found = False
```

Loop through the letters in the word. If you find `"e"`, set `found` to `True` and use `break`.

After the loop, print either:

```text
The word contains e.
```

or:

```text
The word does not contain e.
```

### Exercise 9

Read this program and explain what happens when the user types a blank line.

```python
while True:
    message = input("Message: ")

    if message == "":
        continue

    if message == "quit":
        break

    print("Saved:", message)

print("Closed.")
```

Then explain what happens when the user types:

```text
quit
```

### Exercise 10

Build a small menu loop.

The menu should repeat until the user chooses `"3"`.

```text
1. Say hello
2. Say thanks
3. Quit
```

Rules:

```text
If the choice is blank, ignore it and show the menu again.
If the choice is "1", print "Hello."
If the choice is "2", print "Thanks."
If the choice is "3", stop the loop.
For any other choice, print "Unknown choice."
```

Use both `break` and `continue`.

Build it slowly:

1. Make the loop stop.
2. Add the blank-input skip.
3. Add the menu actions.

## Tiny Win

You can now control a loop from inside the loop body.

That gives you two useful moves:

```text
stop early
skip this turn
```

Small tools, but they make many loops feel more natural.

## Tomorrow

Tomorrow you will study common loop patterns.

You have already seen several pieces:

```text
counting
repeating until input is valid
searching
skipping unwanted values
stopping early
```

Tomorrow is about recognizing those shapes so you can choose the right loop more confidently.
