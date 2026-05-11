# Day 67: Practice Day: Function Problems

**Focus:** Practicing function problems from the full function unit  
**You will practice:** why functions exist, writing functions, parameters, return values, default parameters, keyword arguments, scope, pure functions, splitting programs, naming functions, and common mistakes  
**Estimated time:** 60-75 minutes

## Today's Goal

Today is a practice day.

You are not learning one large new idea. You are putting the function lessons together.

You will practice:

- spotting jobs that deserve a function
- writing functions with `def`
- calling functions
- passing values into parameters
- returning values
- using default parameters
- using keyword arguments when they make calls clearer
- keeping scope easy to follow
- writing pure helper functions
- splitting one program into smaller jobs
- choosing names that explain the job
- debugging common function mistakes

By the end of this lesson, you should be able to look at a small program and ask:

```text
What job is repeated?
What job would be clearer with a name?
What information does this function need?
Should this function print or return?
Where does each variable live?
Can this helper be pure?
Is the main program easy to read?
```

Those questions prepare you for Day 68.

Tomorrow you will build a Text Utility Toolkit. It will use functions for jobs like cleaning text, counting words, changing case, finding words, and printing reports.

Today gives you the function practice you need before that project.

## The Big Idea

A function is a named job.

That job may display something:

```python
def print_title():
    print("Text Tools")


print_title()
```

You should see:

```text
Text Tools
```

That job may receive information:

```python
def greet_person(name):
    print("Hello, " + name + "!")


greet_person("Mina")
greet_person("Sam")
```

You should see:

```text
Hello, Mina!
Hello, Sam!
```

That job may return an answer:

```python
def count_words(text):
    words = text.split()
    return len(words)


word_count = count_words("Python functions help")
print("Words:", word_count)
```

You should see:

```text
Words: 3
```

The most useful function questions are simple:

```text
What should this function be named?
What data should go in?
What should come back?
Should this function print, or should it return a value?
```

When you answer those questions clearly, functions stop feeling like extra syntax.

They become a way to organize thought.

## The Mental Model

Think of a function as a small tool with a label.

Some tools only do an action:

```text
print_header()
show_menu()
print_goodbye()
```

Some tools need values before they can work:

```text
format_name(first_name, last_name)
calculate_total(price, tax)
contains_word(text, word)
```

Some tools give a value back:

```python
def make_label(label, value):
    return label + ": " + str(value)


line = make_label("Score", 18)
print(line)
```

You should see:

```text
Score: 18
```

Read a function call like a request:

```text
make_label("Score", 18)
```

means:

```text
Use the make_label tool.
Send in "Score" and 18.
Get back one string.
```

Good functions make the data flow visible:

```text
arguments go in
local work happens inside
return value comes out
```

That flow is easier to debug than a function that quietly depends on outside variables.

## Warm-Up

For each warm-up, predict the output before running the code.

### Warm-Up 1: Define And Call

Code:

```python
def print_header():
    print("Function Practice")
    print("-----------------")


print_header()
print("Ready")
```

You should see:

```text
Function Practice
-----------------
Ready
```

Debugging prompt:

```text
Which lines define the function?
Which line calls the function?
Would anything print if the final two lines were removed?
```

### Warm-Up 2: Parameters

Code:

```python
def print_contact(name, phone):
    print("Name:", name)
    print("Phone:", phone)


print_contact("Mina", "555-0104")
print_contact("Sam", "555-0199")
```

You should see:

```text
Name: Mina
Phone: 555-0104
Name: Sam
Phone: 555-0199
```

Debugging prompt:

```text
What does name receive in the first call?
What does phone receive in the second call?
```

### Warm-Up 3: Return Values

Code:

```python
def calculate_total(price, tax):
    return price + tax


total = calculate_total(20, 3)
print("Total:", total)
print("With shipping:", total + 5)
```

You should see:

```text
Total: 23
With shipping: 28
```

Debugging prompt:

```text
Why does calculate_total use return instead of print?
Where is the returned value stored?
```

### Warm-Up 4: Defaults And Keyword Arguments

Code:

```python
def build_message(name, message="keep practicing", punctuation="."):
    return name + ", " + message + punctuation


print(build_message("Mina"))
print(build_message("Sam", punctuation="!"))
print(build_message(name="Iris", message="review functions"))
```

You should see:

```text
Mina, keep practicing.
Sam, keep practicing!
Iris, review functions.
```

Debugging prompt:

```text
Which calls use the default message?
Which call changes only the punctuation?
Why does the keyword version make the third call easy to read?
```

### Warm-Up 5: Scope And Pure Helpers

Code:

```python
def clean_word(word):
    return word.strip().lower()


raw_word = "  Python "
cleaned = clean_word(raw_word)

print(raw_word)
print(cleaned)
```

You should see:

```text
  Python 
python
```

Debugging prompt:

```text
Why did raw_word stay unchanged?
What value did the function return?
Is clean_word a pure function?
```

## Practice Problems

Use this rhythm for each problem:

```text
Read the goal.
Write the smallest useful function.
Call the function once.
Check the result.
Call it with different values.
Change one thing at a time.
```

### Practice Problem 1: Name The Job

Create a file named `day-67/function_practice.py`.

Goal:

```text
Write one function that prints a simple app title.
Call it at the start of the program.
```

Hint:

```text
This function does not need parameters because the title is the same each time.
```

Code:

```python
def print_app_title():
    print("Text Helper")
    print("===========")


print_app_title()
print("Choose a tool soon.")
```

You should see:

```text
Text Helper
===========
Choose a tool soon.
```

Try this:

```text
Change only the text inside print_app_title.
Run the program again.
The function call should stay the same.
```

Debugging prompt:

```text
If nothing prints, did you define the function but forget to call it?
```

### Practice Problem 2: Use Parameters For Changing Values

Create a file named `day-67/contact_function.py`.

Goal:

```text
Write one function that prints one contact.
Call it for three contacts.
```

Hint:

```text
The printing pattern is the same.
The name and phone number change.
Those changing pieces should be parameters.
```

Code:

```python
def print_contact(name, phone):
    print(name + ": " + phone)


print_contact("Mina", "555-0104")
print_contact("Sam", "555-0199")
print_contact("Iris", "555-0130")
```

You should see:

```text
Mina: 555-0104
Sam: 555-0199
Iris: 555-0130
```

Try this:

```text
Add an email parameter.
Print the email on a second line.
Update every function call.
```

Debugging prompt:

```text
If Python says a required argument is missing, compare the number of parameters with the number of arguments.
```

### Practice Problem 3: Return A Value

Create a file named `day-67/score_function.py`.

Goal:

```text
Write a function that calculates a quiz percentage.
Store the returned value.
Print a short score report.
```

Hint:

```text
Calculating the percentage is different from printing the report.
The calculation should return a number.
```

Code:

```python
def calculate_percentage(correct, total):
    return correct * 100 / total


percentage = calculate_percentage(4, 5)

print("Percentage:", percentage)

if percentage >= 60:
    print("Passed")
else:
    print("Try again")
```

You should see:

```text
Percentage: 80.0
Passed
```

Try this:

```text
Call calculate_percentage with 2 and 5.
The if statement should choose a different message.
```

Debugging prompt:

```text
If percentage is None, did the function forget to return the calculated value?
```

### Practice Problem 4: Defaults For The Common Case

Create a file named `day-67/message_defaults.py`.

Goal:

```text
Write a function that builds a reminder message.
Use default values for the common message and punctuation.
```

Hint:

```text
The name is required.
The reminder and punctuation can have defaults.
```

Code:

```python
def build_reminder(name, reminder="review one example", punctuation="."):
    return name + ", " + reminder + punctuation


print(build_reminder("Mina"))
print(build_reminder("Sam", "save your file"))
print(build_reminder("Iris", punctuation="!"))
```

You should see:

```text
Mina, review one example.
Sam, save your file.
Iris, review one example!
```

Try this:

```text
Change the default reminder.
Run the program again.
Notice which calls changed and which did not.
```

Debugging prompt:

```text
Are required parameters before default parameters in the function definition?
```

### Practice Problem 5: Keyword Arguments For Clarity

Create a file named `day-67/keyword_practice.py`.

Goal:

```text
Write a function that builds a text report line.
Use keyword arguments for calls that would be easy to misread.
```

Hint:

```text
When two arguments are both strings, keywords can prevent mix-ups.
```

Code:

```python
def build_report_line(label, value, uppercase=False):
    line = label + ": " + str(value)

    if uppercase:
        return line.upper()

    return line


print(build_report_line("Words", 5))
print(build_report_line(label="Characters", value=32))
print(build_report_line(label="Status", value="ready", uppercase=True))
```

You should see:

```text
Words: 5
Characters: 32
STATUS: READY
```

Try this:

```text
Add another call that uses uppercase=False as a keyword.
Decide whether that keyword helps or adds noise.
```

Debugging prompt:

```text
If Python says an unexpected keyword was used, check that the keyword matches the parameter name exactly.
```

### Practice Problem 6: Keep Scope Clear

Create a file named `day-67/scope_review.py`.

Goal:

```text
Write a function that adds one completed task.
Do not change an outside variable from inside the function.
Return the new value.
```

Hint:

```text
Pass the current count in.
Return the updated count.
Assign the returned value outside the function.
```

Code:

```python
def add_completed_task(completed):
    return completed + 1


completed_tasks = 2
completed_tasks = add_completed_task(completed_tasks)
completed_tasks = add_completed_task(completed_tasks)

print("Completed:", completed_tasks)
```

You should see:

```text
Completed: 4
```

Try this:

```text
Create a second function named get_remaining_tasks.
It should receive completed and total.
It should return total - completed.
```

Debugging prompt:

```text
Where does completed live?
Where does completed_tasks live?
Why are those two names allowed to be different?
```

### Practice Problem 7: Split A Text Report

Create a file named `day-67/text_report_functions.py`.

Goal:

```text
Start preparing for tomorrow's Text Utility Toolkit.
Split a small text report into functions.
```

Hint:

```text
Use pure helpers for counting and formatting.
Use one display function for printing the final report.
```

Code:

```python
def count_words(text):
    words = text.split()
    return len(words)


def count_characters(text):
    return len(text)


def make_uppercase(text):
    return text.upper()


def print_text_report(text):
    print("Text Report")
    print("-----------")
    print("Characters:", count_characters(text))
    print("Words:", count_words(text))
    print("Uppercase:", make_uppercase(text))


message = "Functions make text tools easier"
print_text_report(message)
```

You should see:

```text
Text Report
-----------
Characters: 32
Words: 5
Uppercase: FUNCTIONS MAKE TEXT TOOLS EASIER
```

Try this:

```text
Add a function named make_lowercase.
Call it from print_text_report.
```

Debugging prompt:

```text
Which functions return values?
Which function prints the report?
Why is that split useful?
```

## Try It Yourself

Choose one option and write it without looking back at the full solutions first.

### Option A: Text Cleaner

Create a file named `day-67/text_cleaner.py`.

Start with:

```python
text = "  Python Functions Are Useful  "
```

Rules:

```text
Write a function named clean_text.
It should receive text.
It should return the text stripped and lowercased.
Print the original text.
Print the cleaned text.
Do not print inside clean_text.
```

Hint:

```text
Use strip() first, then lower().
Store the returned value outside the function.
```

### Option B: Receipt Helpers

Create a file named `day-67/receipt_helpers.py`.

Start with:

```python
items = [5, 3, 2]
```

Rules:

```text
Write calculate_subtotal.
Write add_tax with a default tax rate of 0.05.
Write build_total_line.
Each function should return a value.
Print the final lines outside the functions.
```

Hint:

```text
One function can use the return value from another function.
```

### Option C: Quiz Report Tools

Create a file named `day-67/quiz_report_tools.py`.

Start with:

```python
answers = ["a", "c", "b", "b"]
correct_answers = ["a", "b", "b", "b"]
```

Rules:

```text
Write count_correct.
Write calculate_percentage.
Write get_score_message.
Write print_quiz_report.
Use return values for the first three functions.
Use print inside print_quiz_report.
```

Hint:

```text
Use indexes or zip() to compare each answer with the matching correct answer.
```

Choose the option that feels useful for tomorrow.

The text cleaner is the closest bridge into Day 68.

## Common Mistake

Practice days are good days to notice small habits that create function bugs.

### Mistake 1: Defining A Function But Never Calling It

Broken code:

```python
def show_menu():
    print("1. Clean text")
    print("2. Count words")
    print("3. Quit")
```

This code defines the function, but it never runs the function.

Fixed code:

```python
def show_menu():
    print("1. Clean text")
    print("2. Count words")
    print("3. Quit")


show_menu()
```

You should see:

```text
1. Clean text
2. Count words
3. Quit
```

Remember:

```text
def stores the job.
The function call runs the job.
```

### Mistake 2: Printing When The Rest Of The Program Needs A Return Value

Broken code:

```python
def count_words(text):
    words = text.split()
    print(len(words))


word_count = count_words("Python makes tools")
print("Saved count:", word_count)
```

You should see:

```text
3
Saved count: None
```

The function printed the count, but it did not return the count.

Fixed code:

```python
def count_words(text):
    words = text.split()
    return len(words)


word_count = count_words("Python makes tools")
print("Saved count:", word_count)
```

You should see:

```text
Saved count: 3
```

Use `return` when another part of the program needs the answer.

### Mistake 3: Relying On A Hidden Outside Variable

This code runs:

```python
suffix = "!"


def add_suffix(text):
    return text + suffix


print(add_suffix("Ready"))
```

You should see:

```text
Ready!
```

The hidden problem is that `add_suffix()` depends on `suffix` from outside the function.

A clearer version passes the suffix in:

```python
def add_suffix(text, suffix):
    return text + suffix


print(add_suffix("Ready", "!"))
```

You should see:

```text
Ready!
```

Now the call shows both pieces of information.

### Mistake 4: Putting A Required Parameter After A Default

Broken code:

```python
def build_label(value="not set", label):
    return label + ": " + value
```

This is broken because `label` is required, but it appears after a default parameter.

Fixed code:

```python
def build_label(label, value="not set"):
    return label + ": " + value


print(build_label("Status"))
```

You should see:

```text
Status: not set
```

Use this order:

```text
required parameters first
default parameters after
```

### Mistake 5: Choosing Names That Hide The Job

This code runs:

```python
def do_it(text):
    return text.strip().lower()


print(do_it("  HELLO  "))
```

You should see:

```text
hello
```

The name `do_it` does not explain the job.

This name is clearer:

```python
def clean_text(text):
    return text.strip().lower()


print(clean_text("  HELLO  "))
```

You should see:

```text
hello
```

A good function name usually starts with an action word:

```text
print
show
get
count
calculate
build
format
clean
find
replace
```

If the function returns `True` or `False`, names like these often work well:

```text
is_empty
has_word
can_continue
should_stop
```

## Debug It

Read the goal first.

Then study the broken code and find the problem before looking at the fixed version.

### Debug 1: Missing Function Call

Goal:

```text
Text Tools
Ready
```

Broken code:

```python
def print_title():
    print("Text Tools")


print("Ready")
```

The problem:

```text
The function is defined but never called.
```

Fixed code:

```python
def print_title():
    print("Text Tools")


print_title()
print("Ready")
```

You should see:

```text
Text Tools
Ready
```

### Debug 2: Missing Return

Goal:

```text
Characters: 12
```

Broken code:

```python
def count_characters(text):
    len(text)


characters = count_characters("hello python")
print("Characters:", characters)
```

The problem:

```text
The function calculates len(text), but it does not return the result.
```

Fixed code:

```python
def count_characters(text):
    return len(text)


characters = count_characters("hello python")
print("Characters:", characters)
```

You should see:

```text
Characters: 12
```

### Debug 3: Wrong Argument Order

Goal:

```text
Mina scored 18 points.
```

Broken code:

```python
def format_score(name, score):
    return name + " scored " + str(score) + " points."


message = format_score(18, "Mina")
print(message)
```

The problem:

```text
The arguments are in the wrong order.
name receives 18.
score receives "Mina".
```

Fixed code:

```python
def format_score(name, score):
    return name + " scored " + str(score) + " points."


message = format_score("Mina", 18)
print(message)
```

You should see:

```text
Mina scored 18 points.
```

Another clear version uses keyword arguments:

```python
def format_score(name, score):
    return name + " scored " + str(score) + " points."


message = format_score(name="Mina", score=18)
print(message)
```

You should see:

```text
Mina scored 18 points.
```

### Debug 4: Local Variable Used Outside

Goal:

```text
Cleaned: python
```

Broken code:

```python
def clean_text(text):
    cleaned = text.strip().lower()


clean_text("  PYTHON  ")
print("Cleaned:", cleaned)
```

The problem:

```text
cleaned is local to the function.
The outside code cannot use that local name.
```

Fixed code:

```python
def clean_text(text):
    cleaned = text.strip().lower()
    return cleaned


result = clean_text("  PYTHON  ")
print("Cleaned:", result)
```

You should see:

```text
Cleaned: python
```

### Debug 5: Return Too Early

Goal:

```text
['read', 'practice']
```

Broken code:

```python
def get_short_words(words):
    short_words = []

    for word in words:
        if len(word) <= 8:
            short_words.append(word)

        return short_words


result = get_short_words(["read", "practice", "documentation"])
print(result)
```

The problem:

```text
The return line is inside the loop.
The function returns after checking only the first word.
```

Fixed code:

```python
def get_short_words(words):
    short_words = []

    for word in words:
        if len(word) <= 8:
            short_words.append(word)

    return short_words


result = get_short_words(["read", "practice", "documentation"])
print(result)
```

You should see:

```text
['read', 'practice']
```

When debugging functions, ask:

- Was the function called?
- Did the call pass the right number of arguments?
- Are the arguments in the right order?
- Would keyword arguments make the call clearer?
- Does the function return a value when the caller needs one?
- Is the `return` line indented correctly?
- Is outside code trying to use a local variable?
- Does the function depend on hidden outside data?

## Read the Docs

Today, revisit Python's official function documentation:

```text
https://docs.python.org/3/tutorial/controlflow.html#defining-functions
```

You do not need to read the whole page.

Look for these ideas:

```text
def
parameters
return
default argument values
keyword arguments
```

For tomorrow, also look at string methods:

```text
https://docs.python.org/3/library/stdtypes.html#string-methods
```

Look for:

```text
strip
lower
upper
title
split
replace
count
startswith
endswith
```

Try this small documentation-style practice:

```python
def clean_and_count(text):
    cleaned = text.strip()
    words = cleaned.split()
    return len(words)


print(clean_and_count("  Python functions help  "))
```

You should see:

```text
3
```

When reading documentation, ask:

```text
Does this method return a new value?
Does it change the existing value?
What arguments does it need?
What kind of value comes back?
```

That habit matters for tomorrow's text toolkit.

## Mini Challenge

Create a file named:

```text
day-67/text_function_review.py
```

Build a small text report using functions.

Your program should define these functions:

- `clean_text(text)`
- `count_words(text)`
- `make_preview(text, length=20)`
- `contains_word(text, word)`
- `print_text_report(text, search_word)`

Rules:

```text
clean_text should return stripped text.
count_words should return a number.
make_preview should return the first length characters.
contains_word should return True or False.
print_text_report should print the final report.
Use at least one keyword argument.
Keep the helper functions small.
```

One possible solution:

```python
def clean_text(text):
    return text.strip()


def count_words(text):
    words = clean_text(text).split()
    return len(words)


def make_preview(text, length=20):
    cleaned = clean_text(text)
    return cleaned[:length]


def contains_word(text, word):
    cleaned_text = clean_text(text).lower()
    clean_search = word.lower()
    return clean_search in cleaned_text


def print_text_report(text, search_word):
    print("Text Report")
    print("-----------")
    print("Cleaned:", clean_text(text))
    print("Words:", count_words(text))
    print("Preview:", make_preview(text, length=18))
    print("Contains search word:", contains_word(text, search_word))


sample_text = "  Python functions make text tools easier  "
print_text_report(sample_text, "tools")
```

You should see:

```text
Text Report
-----------
Cleaned: Python functions make text tools easier
Words: 6
Preview: Python functions m
Contains search word: True
```

After it works, change only the values near the bottom:

```text
Use a different sample_text.
Search for a different word.
Change the preview length.
```

The helper functions should still make sense.

## Real-World Use

Functions are useful anywhere a program has named work to do.

A text utility might have functions like:

```text
clean_text
count_words
count_characters
make_title_case
find_word
replace_word
print_report
show_menu
```

A contact book might have functions like:

```text
print_contact
find_contact
format_contact
add_contact
print_all_contacts
```

A quiz program might have functions like:

```text
ask_question
count_correct
calculate_percentage
get_score_message
print_report
```

The topic changes, but the function thinking stays similar:

```text
Name the job.
Pass in the data.
Return the answer when another part of the program needs it.
Print only when the job is display.
Keep the main flow readable.
```

This is why tomorrow's project will be built from functions.

A Text Utility Toolkit has many small jobs.

Without functions, those jobs become one long block of string code.

With functions, the main program can read more like:

```text
show menu
get text
clean text
count words
replace text
print report
```

That is easier to build, test, and change.

## Recap

Today you practiced the full function unit.

You reviewed:

- why functions exist
- defining and calling functions
- parameters and arguments
- return values
- defaults for common values
- keyword arguments for clearer calls
- scope and local variables
- pure helper functions
- splitting programs by job
- choosing useful names
- debugging common mistakes

The main function habit is:

```text
Use parameters for input.
Use local variables for inside work.
Use return for useful results.
Use print for display.
```

The main design habit is:

```text
Split by job, not by line count.
```

The main debugging habit is:

```text
Follow the data.
Where does it enter?
Where is it stored?
Where does it return?
Where is it printed?
```

Those questions will help in tomorrow's toolkit.

## Lesson Checklist

Before moving on, check that you can:

- explain why functions help reduce repeated code
- write a function with `def`
- call a function after defining it
- pass one or more arguments into parameters
- explain the difference between a parameter and an argument
- return a number, string, Boolean, or list
- store a returned value in a variable
- decide when to use `print()` and when to use `return`
- write a function with a default parameter
- place required parameters before default parameters
- call a function with keyword arguments
- mix positional and keyword arguments in the correct order
- explain why local variables are not available outside a function
- pass values into a function instead of relying on hidden outside variables
- write a small pure helper function
- split a short program into functions by job
- choose names that say what the function does
- debug a missing call, missing return, wrong argument order, scope bug, or early return

## Exercises

### Exercise 1

Write a function named `print_divider`.

It should print:

```text
--------------------
```

Call it three times.

### Exercise 2

Write a function named `greet_person`.

It should receive one parameter named `name`.

This call:

```python
greet_person("Mina")
```

should print:

```text
Hello, Mina!
```

### Exercise 3

Write a function named `format_name`.

It should receive:

```text
first_name
last_name
```

It should return one full name.

Store the returned value in a variable and print it.

### Exercise 4

Write a function named `calculate_total`.

It should receive:

```text
price
tax
```

It should return the total.

Call it with `20` and `3`.

### Exercise 5

Fix the broken code.

Broken code:

```python
def make_greeting(name):
    "Hello, " + name + "!"


message = make_greeting("Sam")
print(message)
```

The goal is:

```text
Hello, Sam!
```

### Exercise 6

Write a function named `repeat_word`.

It should receive:

```text
word
times with a default value of 2
```

Use a loop to print the word.

Call it once with the default.

Call it once with a custom number.

### Exercise 7

Write a function named `build_label`.

It should receive:

```text
label
value with a default value of "not set"
```

This call:

```python
print(build_label("Status"))
```

should print:

```text
Status: not set
```

### Exercise 8

Read this function:

```python
def show_product(name, price, currency="USD"):
    print(name, price, currency)
```

Write three calls:

```text
one positional call
one keyword call
one mixed call
```

Make one call use `"INR"` as the currency.

### Exercise 9

Fix the broken code.

Broken code:

```python
def show_score(player, score):
    print(player + ": " + str(score))


show_score(player="Asha", 15)
```

The goal is:

```text
Asha: 15
```

### Exercise 10

Write a pure function named `is_long_word`.

It should receive:

```text
word
minimum_length with a default value of 8
```

It should return `True` when the word length is at least the minimum length.

It should not print.

### Exercise 11

Write a function named `clean_text`.

It should receive text and return the stripped, lowercased version.

Try it with:

```python
text = "  HELLO PYTHON  "
```

Print the returned value outside the function.

### Exercise 12

Fix the scope bug.

Broken code:

```python
def make_title(text):
    title = text.title()


make_title("python functions")
print(title)
```

The goal is:

```text
Python Functions
```

Use a return value.

### Exercise 13

Write a function named `count_vowels`.

It should receive text.

It should return the number of vowels in the text.

Hint:

```python
if letter in "aeiou":
```

Make the function work for uppercase letters too.

### Exercise 14

Write a function named `contains_word`.

It should receive:

```text
text
word
```

It should return whether the word appears in the text.

Use `.lower()` so the search is not case-sensitive.

### Exercise 15

Start with this working code:

```python
message = "Python makes practice easier"

words = message.split()

print("Text Report")
print("-----------")
print("Characters:", len(message))
print("Words:", len(words))
print("Uppercase:", message.upper())
```

Split it into at least three functions.

Possible jobs:

```text
count characters
count words
make uppercase text
print text report
```

### Exercise 16

Choose the better function name for each job.

```text
Clean extra spaces from text.
Count the number of words.
Build one report line.
Check whether text contains a word.
Print the menu.
```

Avoid names like:

```text
do_it
handle_stuff
process
thing
```

### Exercise 17

Fix the early return.

Broken code:

```python
def get_even_numbers(numbers):
    evens = []

    for number in numbers:
        if number % 2 == 0:
            evens.append(number)

        return evens


print(get_even_numbers([1, 2, 3, 4, 5, 6]))
```

The goal is:

```text
[2, 4, 6]
```

### Exercise 18

Build a small toolkit preview.

Write these functions:

```text
clean_text
count_words
count_characters
make_title_case
print_report
```

Use this text:

```python
sample = "  learning functions makes projects easier  "
```

The helper functions should return values.

`print_report` can print the final result.

### Exercise 19

Look at one old program from earlier in the course.

Write answers to these questions:

```text
What repeated job could become a function?
What data would the function need?
Should the function print or return?
What would you name it?
Would a default value help?
Would keyword arguments make any call clearer?
```

Do not refactor the whole program yet.

Finding one good function is enough.

## Tiny Win

You practiced functions as a full set of tools instead of separate lessons.

That matters.

A useful function has a clear job, clear inputs, and a clear result.

When that is true, the rest of the program becomes easier to read:

```text
clean the text
count the words
build the report
print the result
```

You do not need perfect functions on the first try.

You need the habit of asking what each function is responsible for.

## Tomorrow

Tomorrow is:

```text
Day 68: Text Utility Toolkit
```

Today you practiced the function skills that project will need.

Tomorrow you will use functions to build a small toolkit for working with text.

You will likely write helpers for jobs such as:

```text
clean text
count words
count characters
change case
search for a word
replace text
print a report
show a menu
```

The main lesson from today carries forward:

```text
Give each job a name.
Pass in the data it needs.
Return useful results.
Keep display code separate when you can.
```

That is how the toolkit will stay understandable as it grows.
