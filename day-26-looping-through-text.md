# Day 26: Looping Through Text

**Focus:** Using `for` loops to inspect strings one character at a time  
**You will practice:** looping through strings, counting characters, detecting characters, using `.lower()`, and debugging text-loop counters  
**Estimated time:** 40-50 minutes

## Today's Goal

Today you will learn how to use a `for` loop with a string.

You already know that strings store text:

```python
message = "Hello"
```

A string is not just one solid block. Python can look at it one character at a time.

By the end of this lesson, you should be able to:

- describe a string as a sequence of characters
- use a `for` loop to visit each character in a string
- count letters, spaces, and other characters
- check whether a character appears in text
- use `.lower()` when uppercase and lowercase should count the same
- debug common mistakes in text loops

The main idea is:

> A string is a sequence, so a `for` loop can visit each character in order.

Broken examples are labeled clearly. Read them first, then run the fixed versions when you want to test the idea.

## The Big Idea

A `for` loop can move through a string from left to right.

Code:

```python
word = "Python"

for letter in word:
    print(letter)
```

You should see:

```text
P
y
t
h
o
n
```

Read the loop like this:

```text
For each letter in word:
    print the letter
```

The loop variable is chosen by you. Python does not require the name `letter`.

These two loops do the same thing:

```python
word = "cat"

for character in word:
    print(character)
```

```python
word = "cat"

for symbol in word:
    print(symbol)
```

For text, names like `letter`, `character`, or `symbol` are usually clearer than names like `x`.

Spaces and punctuation are characters too.

Code:

```python
message = "Hi!"

for character in message:
    print(character)
```

You should see:

```text
H
i
!
```

If the string contains a space, Python visits the space as one of the characters.

## The Mental Model

Think of a string as a row of small boxes.

The string `"cat"` holds three characters:

```text
"c" "a" "t"
```

When Python runs this loop:

```python
word = "cat"

for letter in word:
    print(letter)
```

it behaves like this:

```text
First round: letter is "c"
Second round: letter is "a"
Third round: letter is "t"
No characters left: stop the loop
```

The loop variable changes automatically. You do not write a line that says "move to the next letter." Python handles that part.

This is why `for` loops are comfortable for text. You say what you want to visit:

```python
for letter in word:
```

Python handles the walk through the string.

Here is a useful trick for seeing spaces:

```python
message = "Hi Sam"

for character in message:
    print(f"[{character}]")
```

You should see:

```text
[H]
[i]
[ ]
[S]
[a]
[m]
```

The `[ ]` line is the space. When text output looks confusing, putting markers around each character can make the hidden parts visible.

## Try It Yourself

Create a file named:

```text
day-26/text_loop_practice.py
```

Code:

```python
text = "Python 3 is fun!"

letters = 0
spaces = 0
vowels = 0
digits = 0

alphabet = "abcdefghijklmnopqrstuvwxyz"
vowel_characters = "aeiou"
digit_characters = "0123456789"

for character in text:
    lower_character = character.lower()

    if lower_character in alphabet:
        letters = letters + 1

    if character == " ":
        spaces = spaces + 1

    if lower_character in vowel_characters:
        vowels = vowels + 1

    if character in digit_characters:
        digits = digits + 1

print("Text:", text)
print("Letters:", letters)
print("Spaces:", spaces)
print("Vowels:", vowels)
print("Digits:", digits)
```

Before you run it, predict the results.

Run the file from your course folder:

```bash
python day-26/text_loop_practice.py
```

If your computer uses `py`, use:

```bash
py day-26/text_loop_practice.py
```

If your computer uses `python3`, use:

```bash
python3 day-26/text_loop_practice.py
```

You should see:

```text
Text: Python 3 is fun!
Letters: 11
Spaces: 3
Vowels: 3
Digits: 1
```

Now try these changes one at a time:

1. Change `text` to your own sentence.
2. Count only the letter `"e"`.
3. Count periods instead of digits.
4. Print each character inside square brackets so spaces are visible.

Try this:

```python
text = "Python 3 is fun!"

for character in text:
    print(f"[{character}]")
```

Make one change, run the program, and check the result. Small tests make loops easier to understand.

## Common Mistake

### Mistake 1: Looping over the variable name as text

Broken code:

```python
word = "apple"

for letter in "word":
    print(letter)
```

You should see:

```text
w
o
r
d
```

The quotes around `"word"` change the meaning. Python is looping through the literal text `"word"`, not the value stored in the variable `word`.

Fixed code:

```python
word = "apple"

for letter in word:
    print(letter)
```

You should see:

```text
a
p
p
l
e
```

Use quotes when you want exact text. Leave quotes off when you want the value stored in a variable.

### Mistake 2: Resetting the counter inside the loop

Broken code:

```python
word = "banana"

for letter in word:
    count = 0
    if letter == "a":
        count = count + 1

print(count)
```

The counter goes back to `0` on every round. It never gets to remember earlier letters.

Fixed code:

```python
word = "banana"
count = 0

for letter in word:
    if letter == "a":
        count = count + 1

print(count)
```

You should see:

```text
3
```

Start the counter before the loop. Update it inside the loop. Print it after the loop.

### Mistake 3: Forgetting that uppercase and lowercase are different

This code counts lowercase `"a"`:

```python
word = "Ananya"
count = 0

for letter in word:
    if letter == "a":
        count = count + 1

print(count)
```

You should see:

```text
2
```

The first character is uppercase `"A"`, and Python treats `"A"` and `"a"` as different characters.

Fixed code:

```python
word = "Ananya"
count = 0

for letter in word:
    if letter.lower() == "a":
        count = count + 1

print(count)
```

You should see:

```text
3
```

When letter case should not matter, compare lowercase versions.

### Mistake 4: Printing the final answer inside the loop

This program runs, but it prints the count while it is still changing:

```python
word = "banana"
count = 0

for letter in word:
    if letter == "a":
        count = count + 1
    print("Count:", count)
```

You should see:

```text
Count: 0
Count: 1
Count: 1
Count: 2
Count: 2
Count: 3
```

If you only want the final answer, move the print line back to the left:

```python
word = "banana"
count = 0

for letter in word:
    if letter == "a":
        count = count + 1

print("Count:", count)
```

You should see:

```text
Count: 3
```

Indentation decides whether a line runs every round or once after the loop finishes.

## Debug It

Here is a broken program.

It is supposed to count how many times the letter `"o"` appears in `"coconut"`.

Broken code:

```python
word = "coconut"

for letter in word:
    count = 0
    if letter == "o":
        count = count + 1

print("Number of o letters:", count)
```

It should print:

```text
Number of o letters: 2
```

But it prints:

```text
Number of o letters: 0
```

The problem is this line:

```python
count = 0
```

It is inside the loop, so the counter resets for every character. The last character in `"coconut"` is `"t"`, so the final count ends at `0`.

Fixed code:

```python
word = "coconut"
count = 0

for letter in word:
    if letter == "o":
        count = count + 1

print("Number of o letters:", count)
```

You should see:

```text
Number of o letters: 2
```

If you are not sure what a loop is doing, print the loop variable and the counter.

Code:

```python
word = "coconut"
count = 0

for letter in word:
    print("Checking:", letter)

    if letter == "o":
        count = count + 1

    print("Count is now:", count)

print("Final count:", count)
```

You should see:

```text
Checking: c
Count is now: 0
Checking: o
Count is now: 1
Checking: c
Count is now: 1
Checking: o
Count is now: 2
Checking: n
Count is now: 2
Checking: u
Count is now: 2
Checking: t
Count is now: 2
Final count: 2
```

Temporary print lines are meant to answer a question. Once you understand the loop, remove them.

When debugging a text loop, ask:

- What exact string am I looping through?
- What is the loop variable on each round?
- Did I create the counter before the loop?
- Did I update the counter inside the loop?
- Is the final answer printed after the loop?
- Should uppercase and lowercase be treated the same?

## Read the Docs

Find Python's official documentation for string methods:

```text
https://docs.python.org/3/library/stdtypes.html#string-methods
```

You do not need to read the whole page. Look for these methods:

- `lower`
- `isalpha`
- `isdigit`
- `isspace`

These methods help you ask small questions about text.

Code:

```python
print("A".isalpha())
print("7".isdigit())
print(" ".isspace())
```

You should see:

```text
True
True
True
```

For today, keep the practical meaning:

```text
isalpha asks whether text is alphabetic.
isdigit asks whether text is a digit.
isspace asks whether text is whitespace.
```

Documentation is not a book you must read from start to finish. It is a place to look up the next tool when your program needs it.

## Mini Challenge

Build a small text inspector.

Create a file named:

```text
day-26/text_inspector.py
```

The program should ask the user for a sentence and count:

- total characters
- letters
- spaces
- vowels
- digits

Code:

```python
text = input("Type a sentence: ")

letters = 0
spaces = 0
vowels = 0
digits = 0

alphabet = "abcdefghijklmnopqrstuvwxyz"
vowel_characters = "aeiou"
digit_characters = "0123456789"

for character in text:
    lower_character = character.lower()

    if lower_character in alphabet:
        letters = letters + 1

    if character == " ":
        spaces = spaces + 1

    if lower_character in vowel_characters:
        vowels = vowels + 1

    if character in digit_characters:
        digits = digits + 1

print("Characters:", len(text))
print("Letters:", letters)
print("Spaces:", spaces)
print("Vowels:", vowels)
print("Digits:", digits)
```

Try it with:

```text
Python 3 is fun
```

You should see:

```text
Characters: 15
Letters: 11
Spaces: 3
Vowels: 3
Digits: 1
```

Then test your program with:

- a sentence with no digits
- a sentence with uppercase vowels
- a sentence with several spaces

Beginner programs become stronger when you test them with different inputs.

## Real-World Use

Looping through text is useful whenever a program needs to inspect text carefully.

Examples:

- a sign-up form checks whether a password contains a number
- a writing app counts letters, spaces, or punctuation
- a search feature checks whether a keyword appears
- a file-renaming tool looks for spaces in file names
- a quiz program checks whether an answer contains a required word

Today's examples are small, but the pattern is real:

```text
For each character in the text:
    ask a small question
    remember the answer
```

Many larger text tools begin with that kind of careful loop.

## Recap

Today you learned that:

- a string is a sequence of characters
- a `for` loop can visit each character in a string
- the loop variable holds one character at a time
- spaces and punctuation are characters too
- counters usually start before the loop
- counters are updated inside the loop
- final results usually print after the loop
- `in` can check whether a character appears in a group of characters
- `.lower()` helps when uppercase and lowercase should be treated the same
- simple text analysis can be built from small character checks

The key idea:

```text
Looping through text lets Python inspect one character at a time.
```

That is enough to count, detect, and begin analyzing text.

## Lesson Checklist

Before moving on, check that you can:

- explain why a string can be looped through
- write a `for` loop that visits each character in a string
- choose a clear loop variable name
- count how many times a character appears
- count spaces in a sentence
- use `in` to check a character against a group of characters
- use `.lower()` when case should not matter
- place a counter before the loop
- place the final print after the loop
- debug a loop by printing the current character and counter

## Exercises

### Exercise 1

Predict the output before running the code.

```python
word = "code"

for letter in word:
    print(letter)
```

### Exercise 2

Write a program that loops through this word:

```python
word = "tiger"
```

Print each letter inside square brackets.

You should see:

```text
[t]
[i]
[g]
[e]
[r]
```

### Exercise 3

Count how many times `"s"` appears in:

```python
word = "mississippi"
```

The answer should be:

```text
4
```

### Exercise 4

Count how many spaces are in this sentence:

```python
sentence = "loops make repetition clearer"
```

The answer should be:

```text
3
```

### Exercise 5

Fix this program.

It should loop through the value stored in `word`, not the letters `w`, `o`, `r`, and `d`.

Broken code:

```python
word = "mango"

for letter in "word":
    print(letter)
```

### Exercise 6

Fix the counter.

This program should count the letter `"a"` in `"papaya"`.

Broken code:

```python
word = "papaya"

for letter in word:
    count = 0
    if letter == "a":
        count = count + 1

print(count)
```

The answer should be:

```text
3
```

### Exercise 7

Write a program that counts vowels in:

```python
sentence = "The rain stopped."
```

Treat uppercase and lowercase vowels the same.

The answer should be:

```text
5
```

### Exercise 8

Write a program that checks whether a password contains an exclamation mark.

Start with:

```python
password = "sunrise!"
has_exclamation = False
```

Loop through the password. If a character is `"!"`, set `has_exclamation` to `True`.

You should see:

```text
Contains !: True
```

### Exercise 9

Write a program that counts digits in:

```python
code = "A7B2C9"
```

Use this string:

```python
digits = "0123456789"
```

The answer should be:

```text
3
```

### Exercise 10

Debug this program by adding print statements inside the loop.

```python
word = "tomato"
count = 0

for letter in word:
    if letter == "t":
        count = count + 1

print(count)
```

Print the current `letter` and the current `count` on each round. Then remove the debug prints when you understand the loop.

### Exercise 11

Write a small program that asks the user for a sentence.

Then count:

- spaces
- commas
- periods

Test it with:

```text
Hello, friend. Welcome, again.
```

### Exercise 12

Write your own text question.

Examples:

```text
How many times does "e" appear?
Does the text contain a question mark?
How many uppercase "A" characters are there?
```

Then write a loop that answers the question. Keep the question simple enough that one loop can solve it.

## Tiny Win

Today you made Python slow down and inspect text piece by piece.

Text is no longer only something your program can print. It is something your program can examine.

## Tomorrow

Tomorrow you will learn `break` and `continue`.

They give you more control inside loops. You will learn how to stop a loop early and how to skip one round when a certain condition appears.
