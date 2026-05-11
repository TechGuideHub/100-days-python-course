# Day 68: Mini Project: Text Utility Toolkit

**Focus:** Building a command-line text utility toolkit with functions, strings, loops, and menu choices  
**You will practice:** writing helper functions, passing text into parameters, returning cleaned or counted values, using string methods, looping through words, and keeping a menu program readable  
**Estimated time:** 60-75 minutes

## Today's Goal

Today you will build a small text utility toolkit.

The program will run in the command line. It will let the user enter a piece of text, clean it, count characters, count words, change the letter case, search for a word, and show a small summary.

By the end of this lesson, you should be able to:

- split a command-line program into small functions
- use parameters to send text into a function
- use `return` to send a result back
- use string methods like `strip()`, `split()`, `lower()`, `upper()`, and `title()`
- count characters with a loop
- count words with `split()`
- build a menu that keeps running until the user quits
- test a program by typing planned inputs
- debug common function and string mistakes
- prepare for saving text to files on Day 69

This mini project combines the function tools you have been practicing.

The goal is not to build a full writing app. The goal is to build a small set of useful text tools and keep each tool in its own function.

## The Project

Create this file:

```text
day-68/text_utility_toolkit.py
```

The program will:

- start with no saved text
- show a simple menu
- let the user enter or replace the current text
- show the current text
- clean extra spacing
- count characters
- count words
- convert the text to lowercase, uppercase, or title case
- check whether a word appears in the text
- show a short summary
- keep running until the user chooses quit

Example:

```text
Text Utility Toolkit
Work with one piece of text at a time.

Menu:
1. Enter or replace text
2. Show current text
3. Clean text
4. Count characters
5. Count words
6. Convert case
7. Check if a word appears
8. Show summary
9. Quit
Choose an option: 1
Enter text:   python makes small tools useful  
Text saved.

Menu:
1. Enter or replace text
2. Show current text
3. Clean text
4. Count characters
5. Count words
6. Convert case
7. Check if a word appears
8. Show summary
9. Quit
Choose an option: 3
Cleaned text: python makes small tools useful

Menu:
1. Enter or replace text
2. Show current text
3. Clean text
4. Count characters
5. Count words
6. Convert case
7. Check if a word appears
8. Show summary
9. Quit
Choose an option: 5
Words: 5

Menu:
1. Enter or replace text
2. Show current text
3. Clean text
4. Count characters
5. Count words
6. Convert case
7. Check if a word appears
8. Show summary
9. Quit
Choose an option: 9
Goodbye.
```

The exact output depends on what the user types.

This project has the same basic command-line shape you have used before:

```text
create starting data
while the app is running:
    show choices
    ask for a choice
    run the matching action
    quit if the user chooses quit
```

Today the data is one string.

The tools are functions.

## The Big Idea

A text utility toolkit is a group of small jobs.

Each job receives text and gives back an answer.

Examples:

```python
def clean_text(text):
    words = text.split()
    return " ".join(words)
```

This function receives text.

It returns cleaner text.

It does not ask for input.

It does not print.

That makes it easy to test:

```python
result = clean_text("  hello   there  ")
print(result)
```

You should see:

```text
hello there
```

Another function can count words:

```python
def count_words(text):
    words = clean_text(text).split()
    return len(words)
```

This function receives text and returns a number.

The menu can print that number later:

```python
word_total = count_words(current_text)
print("Words:", word_total)
```

This is a good habit:

```text
Helper functions do the small jobs.
The menu decides when to call them.
```

## The Mental Model

Think of the toolkit as a desk with several small tools on it.

One tool cleans text.

One tool counts characters.

One tool counts words.

One tool changes case.

One tool searches for a word.

The menu is not one giant tool. It is the person choosing which small tool to use next.

That means the code should not hide everything inside one long `while` loop.

Instead, the loop can call functions:

```python
if choice == "3":
    current_text = clean_text(current_text)
```

The function handles the cleaning.

The menu handles the choice.

The variable `current_text` stores the piece of text the user is working on.

```text
current_text starts empty.
The user enters text.
The menu keeps using and changing that same text.
```

## Step-by-Step Build

Build the project slowly.

Do not start by typing the final version from top to bottom. A menu program is easier to trust when each tool works before you combine everything.

### Step 1: Start with a menu

Create:

```text
day-68/text_utility_toolkit.py
```

Start with this small version:

```python
def show_menu():
    print()
    print("Menu:")
    print("1. Enter or replace text")
    print("2. Show current text")
    print("3. Clean text")
    print("4. Count characters")
    print("5. Count words")
    print("6. Convert case")
    print("7. Check if a word appears")
    print("8. Show summary")
    print("9. Quit")


def main():
    print("Text Utility Toolkit")
    print("Work with one piece of text at a time.")

    while True:
        show_menu()
        choice = input("Choose an option: ").strip()

        if choice == "9":
            print("Goodbye.")
            break
        else:
            print("That choice is not ready yet.")


main()
```

Run it.

Try:

```text
1
4
9
```

For now, every choice except `9` prints the same message. That is fine. You are proving that the menu repeats and quits.

### Step 2: Store the current text

Inside `main()`, create an empty string:

```python
current_text = ""
```

Then add choices `1` and `2`:

```python
if choice == "1":
    current_text = input("Enter text: ")
    print("Text saved.")
elif choice == "2":
    if current_text == "":
        print("No text yet.")
    else:
        print("Current text:", current_text)
elif choice == "9":
    print("Goodbye.")
    break
else:
    print("Choose a number from 1 to 9.")
```

Now the program can remember one piece of text while it is running.

It will not save the text after the program closes. That is normal for today.

### Step 3: Write a cleaner function

Messy text often has extra spaces at the beginning, at the end, or between words.

This function removes that extra spacing:

```python
def clean_text(text):
    words = text.split()
    return " ".join(words)
```

The line:

```python
words = text.split()
```

turns this:

```text
  hello   there  
```

into a list like this:

```python
["hello", "there"]
```

The line:

```python
return " ".join(words)
```

joins those words back together with one space between each word.

Add this menu action:

```python
elif choice == "3":
    if current_text == "":
        print("No text yet.")
    else:
        current_text = clean_text(current_text)
        print("Cleaned text:", current_text)
```

Notice this line:

```python
current_text = clean_text(current_text)
```

The function returns the cleaned version.

The program stores that returned value back into `current_text`.

### Step 4: Count characters

Python already has `len()`, but writing a counting function helps you practice loops.

```python
def count_characters(text, include_spaces=True):
    if include_spaces:
        return len(text)

    character_count = 0

    for character in text:
        if character != " ":
            character_count += 1

    return character_count
```

This function has a default parameter:

```python
include_spaces=True
```

If you call the function with one argument, it includes spaces:

```python
count_characters("hi there")
```

If you call it with `False`, it skips spaces:

```python
count_characters("hi there", False)
```

Add this menu action:

```python
elif choice == "4":
    if current_text == "":
        print("No text yet.")
    else:
        print("Characters including spaces:", count_characters(current_text))
        print("Characters excluding spaces:", count_characters(current_text, False))
```

### Step 5: Count words

A word count can start with `split()`:

```python
def count_words(text):
    words = clean_text(text).split()
    return len(words)
```

This function cleans the text first, then splits it into words.

Add this menu action:

```python
elif choice == "5":
    if current_text == "":
        print("No text yet.")
    else:
        print("Words:", count_words(current_text))
```

### Step 6: Convert case

A case converter should receive the text and the mode.

```python
def convert_case(text, mode):
    if mode == "lower":
        return text.lower()
    elif mode == "upper":
        return text.upper()
    elif mode == "title":
        return text.title()
    else:
        return text
```

The `mode` parameter tells the function what kind of change to make.

Add this menu action:

```python
elif choice == "6":
    if current_text == "":
        print("No text yet.")
    else:
        print("Case options:")
        print("1. lowercase")
        print("2. uppercase")
        print("3. title case")

        case_choice = input("Choose a case option: ").strip()

        if case_choice == "1":
            current_text = convert_case(current_text, "lower")
            print("Updated text:", current_text)
        elif case_choice == "2":
            current_text = convert_case(current_text, "upper")
            print("Updated text:", current_text)
        elif case_choice == "3":
            current_text = convert_case(current_text, "title")
            print("Updated text:", current_text)
        else:
            print("That case option does not exist.")
```

This changes `current_text`.

If the user converts to uppercase, later tools use the uppercase version.

### Step 7: Check whether a word appears

A simple search should avoid one common problem.

This check:

```python
"cat" in "catalog"
```

is `True`, but `cat` and `catalog` are not the same word.

For this project, loop through the words and compare one cleaned word at a time:

```python
def word_appears(text, target_word):
    target_word = target_word.strip().lower()
    punctuation = ".,!?;:\"'()[]{}"

    for word in text.lower().split():
        clean_word = word.strip(punctuation)

        if clean_word == target_word:
            return True

    return False
```

This is still a simple search. It will not handle every language or every punctuation rule. It is enough for a beginner command-line tool.

Add this menu action:

```python
elif choice == "7":
    if current_text == "":
        print("No text yet.")
    else:
        word = input("Word to find: ")

        if word.strip() == "":
            print("Please enter a word.")
        elif word_appears(current_text, word):
            print("Yes, that word appears.")
        else:
            print("No, that word was not found.")
```

### Step 8: Build a simple summary

The summary can reuse functions you already wrote.

```python
def build_summary(text):
    cleaned_text = clean_text(text)
    words = cleaned_text.split()

    summary = "Summary\n"
    summary += "Characters including spaces: " + str(count_characters(cleaned_text)) + "\n"
    summary += "Characters excluding spaces: " + str(count_characters(cleaned_text, False)) + "\n"
    summary += "Words: " + str(len(words)) + "\n"

    if len(words) == 0:
        summary += "First word: none\n"
        summary += "Last word: none"
    else:
        summary += "First word: " + words[0] + "\n"
        summary += "Last word: " + words[-1]

    return summary
```

The summary is not a paragraph summary. It is a short report about the text.

Add this menu action:

```python
elif choice == "8":
    if current_text == "":
        print("No text yet.")
    else:
        print(build_summary(current_text))
```

### Final working code

Here is the full program:

```python
def clean_text(text):
    words = text.split()
    return " ".join(words)


def count_characters(text, include_spaces=True):
    if include_spaces:
        return len(text)

    character_count = 0

    for character in text:
        if character != " ":
            character_count += 1

    return character_count


def count_words(text):
    words = clean_text(text).split()
    return len(words)


def convert_case(text, mode):
    if mode == "lower":
        return text.lower()
    elif mode == "upper":
        return text.upper()
    elif mode == "title":
        return text.title()
    else:
        return text


def word_appears(text, target_word):
    target_word = target_word.strip().lower()
    punctuation = ".,!?;:\"'()[]{}"

    for word in text.lower().split():
        clean_word = word.strip(punctuation)

        if clean_word == target_word:
            return True

    return False


def build_summary(text):
    cleaned_text = clean_text(text)
    words = cleaned_text.split()

    summary = "Summary\n"
    summary += "Characters including spaces: " + str(count_characters(cleaned_text)) + "\n"
    summary += "Characters excluding spaces: " + str(count_characters(cleaned_text, False)) + "\n"
    summary += "Words: " + str(len(words)) + "\n"

    if len(words) == 0:
        summary += "First word: none\n"
        summary += "Last word: none"
    else:
        summary += "First word: " + words[0] + "\n"
        summary += "Last word: " + words[-1]

    return summary


def show_current_text(text):
    if text == "":
        print("No text yet.")
    else:
        print("Current text:", text)


def show_menu():
    print()
    print("Menu:")
    print("1. Enter or replace text")
    print("2. Show current text")
    print("3. Clean text")
    print("4. Count characters")
    print("5. Count words")
    print("6. Convert case")
    print("7. Check if a word appears")
    print("8. Show summary")
    print("9. Quit")


def main():
    current_text = ""

    print("Text Utility Toolkit")
    print("Work with one piece of text at a time.")

    while True:
        show_menu()
        choice = input("Choose an option: ").strip()

        if choice == "1":
            current_text = input("Enter text: ")
            print("Text saved.")

        elif choice == "2":
            show_current_text(current_text)

        elif choice == "3":
            if current_text == "":
                print("No text yet.")
            else:
                current_text = clean_text(current_text)
                print("Cleaned text:", current_text)

        elif choice == "4":
            if current_text == "":
                print("No text yet.")
            else:
                print("Characters including spaces:", count_characters(current_text))
                print("Characters excluding spaces:", count_characters(current_text, False))

        elif choice == "5":
            if current_text == "":
                print("No text yet.")
            else:
                print("Words:", count_words(current_text))

        elif choice == "6":
            if current_text == "":
                print("No text yet.")
            else:
                print("Case options:")
                print("1. lowercase")
                print("2. uppercase")
                print("3. title case")

                case_choice = input("Choose a case option: ").strip()

                if case_choice == "1":
                    current_text = convert_case(current_text, "lower")
                    print("Updated text:", current_text)
                elif case_choice == "2":
                    current_text = convert_case(current_text, "upper")
                    print("Updated text:", current_text)
                elif case_choice == "3":
                    current_text = convert_case(current_text, "title")
                    print("Updated text:", current_text)
                else:
                    print("That case option does not exist.")

        elif choice == "7":
            if current_text == "":
                print("No text yet.")
            else:
                word = input("Word to find: ")

                if word.strip() == "":
                    print("Please enter a word.")
                elif word_appears(current_text, word):
                    print("Yes, that word appears.")
                else:
                    print("No, that word was not found.")

        elif choice == "8":
            if current_text == "":
                print("No text yet.")
            else:
                print(build_summary(current_text))

        elif choice == "9":
            print("Goodbye.")
            break

        else:
            print("Choose a number from 1 to 9.")


if __name__ == "__main__":
    main()
```

## Try It Yourself

Run the program and test it with planned inputs.

First test:

```text
1
  Python   is   useful  
3
2
9
```

You should see the text cleaned to:

```text
Python is useful
```

Second test:

```text
1
Python, tools, and tiny scripts
7
tools
7
tool
9
```

The word `tools` should be found.

The word `tool` should not be found, because it is not the same full word.

Third test:

```text
1
small tools matter
4
5
6
2
8
9
```

This checks the character count, word count, uppercase conversion, and summary.

When a menu program has many choices, do not test everything randomly. Pick one small path through the menu and check the output.

## Common Mistake

A common mistake is calling a function but not saving the returned value.

Broken:

```python
clean_text(current_text)
print(current_text)
```

This calls `clean_text()`, but the returned text is ignored.

The old `current_text` is still unchanged.

Fix:

```python
current_text = clean_text(current_text)
print(current_text)
```

When a function returns a new value, store that value if you want to keep it.

The same idea applies to `lower()`, `upper()`, and `title()`.

Broken:

```python
current_text.upper()
```

Fixed:

```python
current_text = current_text.upper()
```

String methods usually return a new string. They do not change the old string in place.

## Debug It

Here is a broken version of the word count:

```python
def count_words(text):
    words = clean_text(text).split()


total = count_words("one two three")
print("Words:", total)
```

You will see:

```text
Words: None
```

The function creates the list of words, but it never returns the count.

Fix it:

```python
def count_words(text):
    words = clean_text(text).split()
    return len(words)


total = count_words("one two three")
print("Words:", total)
```

You should see:

```text
Words: 3
```

If the full toolkit is not working, check these questions:

- Does the function return the value the menu needs?
- Did you store the returned value when the text should change?
- Are menu choices compared with strings like `"1"` and `"9"`?
- Is the `break` only used when the user chooses quit?
- Is `current_text` created before the loop starts?
- Did you type `elif` instead of starting every check with `if`?

Debug one menu choice at a time.

If choice `5` is broken, test only choice `5` until it works. Then move on.

## Read the Docs

Python's string methods are the main tools in this project:

[Python documentation: string methods](https://docs.python.org/3/library/stdtypes.html#string-methods)

Look for:

- `str.strip()`
- `str.split()`
- `str.lower()`
- `str.upper()`
- `str.title()`
- `str.join()`

Also look up:

[Python documentation: `len()`](https://docs.python.org/3/library/functions.html#len)

Ask these questions while reading:

- Does this method return a new string?
- Does it change the original string?
- What does it return when the string is empty?
- Does it need an argument?

For today, you do not need to memorize every string method.

You only need to recognize that Python already has many small tools for working with text.

## Mini Challenge

Add a vowel counter.

Write this function:

```python
def count_vowels(text):
    vowels = "aeiou"
    total = 0

    for character in text.lower():
        if character in vowels:
            total += 1

    return total
```

Then add a new menu choice:

```text
10. Count vowels
```

The menu action should print:

```text
Vowels: 7
```

The exact number depends on the current text.

Small warning: if you add a tenth option, update the invalid-choice message too.

## Real-World Use

Text tools appear in many real programs.

A website form might clean extra spaces from a name before saving it.

A search box might convert text to lowercase so `Python` and `python` match.

A writing app might count words.

A support tool might search a message for a keyword.

A report tool might create a small summary before showing more details.

The program you built today is small, but the pattern is real:

```text
receive text
clean it
analyze it
show a useful result
```

The functions are the reusable part.

The menu is only one way to use them.

Later, the same functions could be used with files, web forms, or larger programs.

## Recap

Today you built a command-line text utility toolkit.

You used one variable, `current_text`, to store the text while the program runs.

You wrote helper functions for cleaning, counting, converting, searching, and summarizing.

You used a `while True` loop to keep the menu alive.

You used `return` when a function created a value the rest of the program needed.

The main idea:

```text
Keep each text job small.
Pass text in.
Return the result.
Let the menu decide when to use it.
```

## Lesson Checklist

- [ ] I can build a menu that repeats until the user quits.
- [ ] I can store one piece of text in a variable.
- [ ] I can write a function that receives text as a parameter.
- [ ] I can return cleaned text from a function.
- [ ] I can count characters with and without spaces.
- [ ] I can count words with `split()`.
- [ ] I can convert text to lowercase, uppercase, and title case.
- [ ] I can search for a word in a beginner-safe way.
- [ ] I can reuse helper functions inside another function.
- [ ] I can test a command-line program with planned inputs.

## Exercises

1. Add a menu choice that prints the first character and last character of the current text.

2. Add a function named `count_spaces(text)` that returns how many spaces are in the text.

3. Add a function named `starts_with_word(text, word)` that returns `True` if the cleaned text starts with that word.

4. Change `build_summary()` so it also shows the average word length.

5. Add a menu choice that replaces one word with another word.

6. Make the program print the current text after every change.

7. Add a choice named `Reset text` that sets `current_text` back to an empty string.

8. Write three test runs on paper before running the program. Include the menu choices and the output you expect.

## Tiny Win

You built a program that feels like a small toolbox instead of one long script.

That matters.

You can now take a larger idea, find the small jobs inside it, and give each job a function.

That is one of the most useful habits in beginner Python.

## Tomorrow

Tomorrow you will move from text that only lives while the program is running to text that can be saved and loaded.

Day 69 will introduce files.

Today, the toolkit forgets everything when it closes.

Tomorrow, you will start teaching programs how to remember.
