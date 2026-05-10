# Day 06: Strings

**Focus:** Working with text in Python  
**You will practice:** Quotes, concatenation, f-strings, string methods, and `len()`  
**Estimated time:** 40-55 minutes

## Today's Goal

Today you will learn how Python works with text.

In Python, text is called a string.

By the end of this lesson, you should be able to:

* recognize strings in Python code
* use single quotes and double quotes
* join strings together
* put variables inside strings with f-strings
* use a few simple string methods
* use `len()` to count characters
* spot common string mistakes

Strings appear in almost every program you will write. Names, messages, usernames, file names, menu options, search terms, addresses, labels, errors, and greetings are usually stored as strings.

Broken examples are labeled clearly. Study them first; run them only when you want to see the error.

---

## The Big Idea

A string is text that Python treats as text.

These are strings:

```python
"Hello"
```

```python
"Python is useful."
```

```python
"123"
```

That last one is important. Even though `"123"` looks like a number, the quotation marks tell Python:

```text
Treat this as text.
```

Compare these two values:

```python
age = 12
age_text = "12"
```

The first value is a number. The second value is a string.

They look similar to a person, but Python sees them differently. Python can do math with numbers, but it handles strings as text.

---

## The Mental Model

Think of a string as a row of characters.

Each character might be:

* a letter
* a number symbol
* a space
* punctuation
* another symbol

> Key idea: A string is a piece of text kept inside matching quotation marks.

Python uses quotation marks as boundaries. They tell Python where the text starts and where the text ends.

```python
message = "Good morning"
```

Python sees:

```text
The text starts after the first quote.
The text ends before the second quote.
```

Without quotes, Python thinks you are talking about a variable name or a Python command.

Broken code:

```python
message = Good morning
```

Python does not know that `Good morning` is supposed to be text.

---

## Quotes

Python lets you create strings with double quotes:

```python
name = "Maya"
```

Python also lets you create strings with single quotes:

```python
name = 'Maya'
```

Both are fine.

This course will mostly use double quotes because they are easy to see and match many beginner examples.

Single quotes are useful when the text itself contains a double quote. Double quotes are useful when the text itself contains an apostrophe.

```python
quote = 'She said, "Python is working."'
message = "It's time to practice."

print(quote)
print(message)
```

It prints:

```text
She said, "Python is working."
It's time to practice.
```

The quote that starts the string must also end the string.

This works:

```python
word = "hello"
```

This works too:

```python
word = 'hello'
```

Broken code:

```python
word = "hello'
```

The string starts with a double quote, so Python expects a double quote at the end.

---

## First String Variables

Create a file named:

```text
day-06/strings_practice.py
```

```python
first_name = "Asha"
favorite_food = "dosa"
city = "Hyderabad"

print(first_name)
print(favorite_food)
print(city)
```

You should see:

```text
Asha
dosa
Hyderabad
```

Each variable stores a string.

The variable name is not the text itself. The variable is a label that points to the text.

```python
first_name = "Asha"
```

This means:

```text
Remember the string "Asha" under the name first_name.
```

---

## Joining Strings

You can join strings with `+`.

This is concatenation: putting strings next to each other.

```python
first_name = "Asha"
greeting = "Hello, " + first_name

print(greeting)
```

It prints:

```text
Hello, Asha
```

Notice the space after the comma:

```python
"Hello, "
```

That space matters.

Broken code:

```python
first_name = "Asha"
greeting = "Hello," + first_name

print(greeting)
```

That prints:

```text
Hello,Asha
```

Python joined the strings exactly as written. It did not add a space for you.

> Checkpoint: If output looks squeezed together, look for missing spaces inside your strings.

---

## Concatenating Several Strings

You can join more than two strings.

```python
first_name = "Asha"
city = "Hyderabad"

sentence = "My name is " + first_name + " and I live in " + city + "."

print(sentence)
```

It prints:

```text
My name is Asha and I live in Hyderabad.
```

This works, but it can become crowded. There are many `+` signs, many quote marks, and several places where a missing space can hide.

Python gives us a cleaner tool for this.

---

## F-Strings

An f-string lets you place variables inside a string.

The `f` goes before the opening quote. Variables go inside curly braces.

```python
first_name = "Asha"
city = "Hyderabad"

sentence = f"My name is {first_name} and I live in {city}."

print(sentence)
```

It prints:

```text
My name is Asha and I live in Hyderabad.
```

This is usually easier to read than concatenation.

Compare the two versions:

```python
sentence = "My name is " + first_name + " and I live in " + city + "."
```

```python
sentence = f"My name is {first_name} and I live in {city}."
```

Both can work when the variables already exist.

The f-string version keeps the sentence looking like a sentence. That makes it easier to notice missing spaces, punctuation, and variable names.

---

## F-Strings With Numbers

F-strings are also helpful when your sentence includes numbers.

```python
name = "Maya"
age = 14

print(f"{name} is {age} years old.")
```

It prints:

```text
Maya is 14 years old.
```

This is cleaner than trying to join a string and a number with `+`.

Broken code:

```python
age = 14
print("Age: " + age)
```

Python does not automatically join a string and a number with `+`.

Fixed code:

```python
age = 14
print(f"Age: {age}")
```

For beginner programs, f-strings are often the simplest way to create readable output.

---

## String Methods

Strings come with useful actions attached to them.

These actions are called methods.

A method is written after the value, with a dot:

```python
word.upper()
```

For today, think of a method as something a value knows how to do.

You do not need to memorize all string methods today. The goal is to understand the pattern:

```python
value.method()
```

Once you know that pattern, you can learn new methods when you need them.

```python
name = "maya"
shout = "HELLO"
book = "the secret garden"
username = "   kavya   "
message = "I like Java."
word = "banana"

print(name.upper())
print(shout.lower())
print(book.title())
print(username.strip())
print(message.replace("Java", "Python"))
print(word.count("a"))
```

It prints:

```text
MAYA
hello
The Secret Garden
kavya
I like Python.
3
```

Here is what each method did:

* `.upper()` turned letters into uppercase
* `.lower()` turned letters into lowercase
* `.title()` capitalized the first letter of each word
* `.strip()` removed extra spaces from the beginning and end
* `.replace()` replaced one piece of text with another
* `.count()` counted how many times a piece of text appeared

Real user input often contains accidental spaces, unusual capitalization, or small text differences. String methods help you clean and shape that text.

---

## Methods Do Not Change the Original String

This part matters: string methods usually create a new string. They do not change the original string in place.

```python
name = "maya"
name.upper()

print(name)
```

It still prints:

```text
maya
```

The uppercase version was created, but it was not saved anywhere.

If you want to keep the new version, store it:

```python
name = "maya"
name = name.upper()

print(name)
```

Now it prints:

```text
MAYA
```

Or store it in a new variable:

```python
name = "maya"
big_name = name.upper()

print(name)
print(big_name)
```

That gives you both values:

```text
maya
MAYA
```

> Key idea: If a method creates a new value, print it or save it.

---

## The Length of a String

Python has a built-in function named `len()`.

It tells you how many characters are in a string.

```python
word = "Python"
message = "Hi Sam"

print(len(word))
print(len(message))
```

Both lengths are 6:

```text
6
6
```

Spaces count too.

The characters in `"Hi Sam"` are:

```text
H
i
space
S
a
m
```

`len()` is not a string method. It does not use a dot.

Write this:

```python
len(word)
```

Broken code:

```python
word.len()
```

Strings do not have a `.len()` method.

---

## Try It Yourself

Create a file named:

```text
day-06/string_tools.py
```

```python
name = "  kavya  "
city = "chennai"
favorite_language = "python"

clean_name = name.strip().title()
clean_city = city.title()
language = favorite_language.upper()

print(f"Name: {clean_name}")
print(f"City: {clean_city}")
print(f"Favorite language: {language}")
```

It prints:

```text
Name: Kavya
City: Chennai
Favorite language: PYTHON
```

Notice this line:

```python
clean_name = name.strip().title()
```

Python reads it from left to right:

1. Start with `name`.
2. Remove extra spaces with `.strip()`.
3. Convert it to title case with `.title()`.
4. Store the result in `clean_name`.

This is called chaining methods.

You do not need to chain methods all the time. It is just useful to know that it is possible.

If it feels too crowded, split it into steps:

```python
name = "  kavya  "

clean_name = name.strip()
clean_name = clean_name.title()

print(clean_name)
```

It prints:

```text
Kavya
```

Clear code is better than clever code.

---

## Common Mistake

### Mistake 1: Forgetting a closing quote

Broken code:

```python
message = "Hello
```

Python keeps looking for the end of the string and cannot find it.

Fixed code:

```python
message = "Hello"
```

### Mistake 2: Mixing quote types

Broken code:

```python
name = "Maya'
```

Fixed code:

```python
name = "Maya"
```

This also works:

```python
name = 'Maya'
```

### Mistake 3: Forgetting spaces during concatenation

Broken code:

```python
first = "Good"
second = "morning"

print(first + second)
```

That prints:

```text
Goodmorning
```

Fixed code:

```python
first = "Good"
second = "morning"

print(first + " " + second)
```

It prints:

```text
Good morning
```

### Mistake 4: Joining strings and numbers with `+`

Broken code:

```python
score = 10
print("Score: " + score)
```

Fixed code:

```python
score = 10
print(f"Score: {score}")
```

It prints:

```text
Score: 10
```

### Mistake 5: Forgetting method parentheses

Broken code:

```python
name = "maya"
print(name.upper)
```

This prints the method object instead of calling the method.

Fixed code:

```python
name = "maya"
print(name.upper())
```

The fixed program prints:

```text
MAYA
```

The parentheses mean:

```text
Run this method now.
```

---

## Debug It

Here is a broken program.

Broken code:

```python
first_name = "Ravi"
city = "Pune"

print("My name is " + first_name + "and I live in " + city + ".")
```

That prints:

```text
My name is Raviand I live in Pune.
```

What is wrong?

A space is missing before `and`.

Fixed code:

```python
first_name = "Ravi"
city = "Pune"

print("My name is " + first_name + " and I live in " + city + ".")
```

The fixed program prints:

```text
My name is Ravi and I live in Pune.
```

Fixed code:

```python
first_name = "Ravi"
city = "Pune"

print(f"My name is {first_name} and I live in {city}.")
```

The f-string version prints the same sentence:

```text
My name is Ravi and I live in Pune.
```

Here is another broken program.

Broken code:

```python
name = "leela"
name.title()

print(name)
```

The programmer expected:

```text
Leela
```

But the program prints:

```text
leela
```

What is wrong?

`.title()` creates a new string, but the new string was not saved.

Fixed code:

```python
name = "leela"
name = name.title()

print(name)
```

It prints:

```text
Leela
```

When debugging strings, ask:

* Are the quotes matched?
* Are the spaces included?
* Am I joining text and numbers safely?
* Did I call the method with parentheses?
* Did I save the new string if I need it later?

---

## Read the Docs

Find Python's official documentation for string methods:

```text
https://docs.python.org/3/library/stdtypes.html#string-methods
```

You do not need to read the whole page.

Look for these method names:

* `upper`
* `lower`
* `strip`
* `replace`
* `count`

Your goal is to notice that Python strings have many built-in tools. You do not need to memorize every method.

---

## Mini Challenge

Create a file named:

```text
day-06/profile_card.py
```

Make a small profile card using string variables and f-strings.

Start with these variables:

```python
name = "  anika  "
city = "mumbai"
favorite_color = "blue"
favorite_food = "pav bhaji"
```

Clean up the values before printing:

* remove extra spaces from `name`
* make `name` title case
* make `city` title case
* make `favorite_color` uppercase

Your output should look like this:

```text
--- Profile Card ---
Name: Anika
City: Mumbai
Favorite Color: BLUE
Favorite Food: pav bhaji
Name Length: 5
```

Use `len()` to show the length of the cleaned name.

Small hint:

```python
clean_name = name.strip().title()
```

Build it slowly:

1. Create the variables.
2. Clean one value.
3. Print one line.
4. Add the next line.
5. Run the program again.

That edit-run-check loop is the main practice.

---

## Real-World Use

Strings are everywhere in real programs.

A shopping app might store:

* product names
* delivery addresses
* coupon codes
* customer messages

A game might store:

* player names
* level titles
* dialogue
* score messages

A school system might store:

* student names
* class names
* feedback comments
* report labels

Even programs that do a lot of math usually need strings to explain the results to people.

The number may be the answer, but the string makes the answer readable.

```python
total = 250
print(f"Your total is {total} rupees.")
```

You should see:

```text
Your total is 250 rupees.
```

Strings let programs show readable messages.

---

## Recap

Today you learned:

* strings are text values
* strings are written inside quotes
* single quotes and double quotes both work
* the starting and ending quote must match
* `+` can join strings together
* f-strings are a clean way to put variables inside text
* string methods use dot syntax, like `.upper()`
* methods need parentheses to run
* many string methods create a new string instead of changing the old one
* `len()` tells you how many characters are in a string

Main idea:

```text
Strings are how Python stores and shapes text.
```

---

## Exercises

### Exercise 1

Create three string variables:

```python
first_name = "..."
last_name = "..."
city = "..."
```

Use an f-string to print one sentence that includes all three values.

For example:

```text
My name is Neha Sharma and I live in Delhi.
```

### Exercise 2

Fix the spacing in this program:

```python
word_one = "Good"
word_two = "night"

print(word_one + word_two)
```

The output should be:

```text
Good night
```

### Exercise 3

Use string methods to clean this name:

```python
name = "   arjun   "
```

Print:

```text
Arjun
```

### Exercise 4

Fix this broken f-string:

```python
name = "Sara"
print("Hello, {name}")
```

The output should be:

```text
Hello, Sara
```

### Exercise 5

Fix this program:

```python
score = 20
print("Final score: " + score)
```

Use an f-string.

### Exercise 6

Write a program that stores a sentence in a variable.

Then print:

* the sentence in uppercase
* the sentence in lowercase
* the number of characters in the sentence

### Exercise 7

Use `.replace()` to change this sentence:

```python
message = "I am learning Java."
```

into:

```text
I am learning Python.
```

### Exercise 8

Find and fix all the problems:

```python
name = "diya"
age = 13

name.title()

print("Student: " + name)
print("Age: " + age)
print("Welcome, {name}!")
```

The output should be:

```text
Student: Diya
Age: 13
Welcome, Diya!
```

---

## Lesson Checklist

Before moving on, check that you can:

* create a string with single quotes or double quotes
* explain why `"12"` is different from `12`
* join strings with `+` and include spaces where needed
* use an f-string to include variables in a message
* call string methods with parentheses
* save a method result when you need it later
* use `len()` to count characters
* identify at least two common string mistakes

---

## Tiny Win

You can now make a Python program print readable messages instead of bare values.

You can also clean, reshape, combine, and count text.

---

## Tomorrow

Tomorrow, you will learn about booleans: values that can be either `True` or `False`.
