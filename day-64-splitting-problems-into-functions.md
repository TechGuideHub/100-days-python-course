# Day 64: Splitting Problems Into Functions

**Focus:** Breaking one larger program into small functions  
**You will practice:** finding repeated steps, naming each job, writing one function at a time, and keeping the main program flow readable  
**Estimated time:** 45-60 minutes

## Today's Goal

Today you will practice turning a program into a set of small functions.

You already know the pieces:

- how to define a function
- how to pass arguments into a function
- how to return a value
- how scope affects variable names
- why pure functions are easier to reason about

Today is about using those pieces together.

By the end of this lesson, you should be able to:

- look at a longer program and find the smaller jobs inside it
- turn repeated or meaningful steps into functions
- decide what information a function needs
- decide whether a function should return a value or print something
- keep the main program flow short and readable
- avoid splitting code into random pieces
- debug a refactor where a function forgot to return a value
- prepare for Day 65, where you will focus on naming functions well

The main idea:

```text
Do not split a program by line count.
Split it by job.
```

A useful function does one clear job.

## The Big Idea

A beginner program often starts as one long list of steps.

That is normal.

Before you split a program into functions, it helps to make the program work first.

Then you can look for the jobs hiding inside it.

Example:

```python
contacts = [
    {"name": "Mina", "phone": "555-0101", "city": "Pune", "favorite": True},
    {"name": "Sam", "phone": "555-0102", "city": "Chennai", "favorite": False},
    {"name": "Iris", "phone": "555-0103", "city": "Delhi", "favorite": True},
]

print("Contact Summary")
print("---------------")
print("Total contacts:", len(contacts))

favorite_count = 0
for contact in contacts:
    if contact["favorite"]:
        favorite_count += 1

print("Favorite contacts:", favorite_count)
print()

for contact in contacts:
    line = contact["name"] + " - " + contact["phone"] + " (" + contact["city"] + ")"
    print(line)
```

You should see:

```text
Contact Summary
---------------
Total contacts: 3
Favorite contacts: 2

Mina - 555-0101 (Pune)
Sam - 555-0102 (Chennai)
Iris - 555-0103 (Delhi)
```

This program works.

But it has several jobs mixed together:

- storing sample contact data
- printing the report heading
- counting favorite contacts
- formatting one contact line
- printing all contact lines

When those jobs stay tangled together, the program becomes harder to change.

For example, if you want to change how one contact is displayed, you have to find the formatting code inside the larger program.

If you want to test the favorite count, you have to run the whole report.

Functions let you give each job a place.

Code:

```python
def get_sample_contacts():
    return [
        {"name": "Mina", "phone": "555-0101", "city": "Pune", "favorite": True},
        {"name": "Sam", "phone": "555-0102", "city": "Chennai", "favorite": False},
        {"name": "Iris", "phone": "555-0103", "city": "Delhi", "favorite": True},
    ]


def count_favorites(contacts):
    favorite_count = 0

    for contact in contacts:
        if contact["favorite"]:
            favorite_count += 1

    return favorite_count


def format_contact(contact):
    return contact["name"] + " - " + contact["phone"] + " (" + contact["city"] + ")"


def print_contacts(contacts):
    for contact in contacts:
        print(format_contact(contact))


def print_contact_summary(contacts):
    print("Contact Summary")
    print("---------------")
    print("Total contacts:", len(contacts))
    print("Favorite contacts:", count_favorites(contacts))
    print()
    print_contacts(contacts)


def main():
    contacts = get_sample_contacts()
    print_contact_summary(contacts)


main()
```

You should see:

```text
Contact Summary
---------------
Total contacts: 3
Favorite contacts: 2

Mina - 555-0101 (Pune)
Sam - 555-0102 (Chennai)
Iris - 555-0103 (Delhi)
```

The output is the same.

The shape of the code is different.

Now each function has a job:

| Function | Job |
| --- | --- |
| `get_sample_contacts()` | creates the sample data |
| `count_favorites(contacts)` | counts favorite contacts |
| `format_contact(contact)` | builds one contact line |
| `print_contacts(contacts)` | prints all contact lines |
| `print_contact_summary(contacts)` | prints the full report |
| `main()` | controls the main flow |

This is the point of splitting a problem into functions.

You are not trying to make the code longer.

You are trying to make each part easier to understand.

## The Mental Model

Think of a program as a small workplace.

Each function should have a clear job.

One function counts.

One function formats.

One function prints.

One function controls the order.

That is easier to read than one person doing every job at once.

The main program should feel like a table of contents.

Example:

```text
get the contacts
print the contact summary
```

In Python, that can become:

```python
def main():
    contacts = get_sample_contacts()
    print_contact_summary(contacts)
```

That code does not show every detail.

It shows the story of the program.

The details live inside the functions.

When you split a problem, ask these questions:

```text
What data do I have?
What jobs need to happen?
Which job is repeated?
Which job has a useful name?
What information does this function need?
Should this function return a value or print something?
```

Two common function types are:

```text
Calculate something and return it.
Display something by printing it.
```

Example:

```python
def calculate_total(prices):
    total = 0

    for price in prices:
        total += price

    return total


def print_total(prices):
    total = calculate_total(prices)
    print("Total:", total)


print_total([5, 3, 2])
```

You should see:

```text
Total: 10
```

`calculate_total()` returns a value.

`print_total()` displays a value.

Keeping those jobs separate makes the program easier to change later.

For example, you could reuse `calculate_total()` in another place without printing anything.

## Try It Yourself

Create a file named:

```text
day-64/split_into_functions.py
```

You will start with one working program, then split it into functions.

### Step 1: Start With A Working Program

Code:

```python
contacts = [
    {"name": "Mina", "phone": "555-0101", "city": "Pune", "favorite": True},
    {"name": "Sam", "phone": "555-0102", "city": "Chennai", "favorite": False},
    {"name": "Iris", "phone": "555-0103", "city": "Delhi", "favorite": True},
]

print("Contact Summary")
print("---------------")
print("Total contacts:", len(contacts))

favorite_count = 0
for contact in contacts:
    if contact["favorite"]:
        favorite_count += 1

print("Favorite contacts:", favorite_count)
print()

for contact in contacts:
    line = contact["name"] + " - " + contact["phone"] + " (" + contact["city"] + ")"
    print(line)
```

You should see:

```text
Contact Summary
---------------
Total contacts: 3
Favorite contacts: 2

Mina - 555-0101 (Pune)
Sam - 555-0102 (Chennai)
Iris - 555-0103 (Delhi)
```

Do not split it yet.

First, make sure it runs.

It is easier to refactor working code than broken code.

### Step 2: Find The Jobs

Read the program again.

Write the jobs as short notes:

```text
make contact data
print heading
count favorite contacts
print favorite count
format one contact
print every contact
```

Some of these jobs are tiny.

Not every tiny job needs its own function.

Look for jobs that are:

- repeated
- useful to test by themselves
- easier to understand with a name
- likely to change later

In this program, these are good function candidates:

```text
count favorite contacts
format one contact
print every contact
print full summary
```

### Step 3: Move The Counting Into A Function

Code:

```python
def count_favorites(contacts):
    favorite_count = 0

    for contact in contacts:
        if contact["favorite"]:
            favorite_count += 1

    return favorite_count


contacts = [
    {"name": "Mina", "phone": "555-0101", "city": "Pune", "favorite": True},
    {"name": "Sam", "phone": "555-0102", "city": "Chennai", "favorite": False},
    {"name": "Iris", "phone": "555-0103", "city": "Delhi", "favorite": True},
]

print("Favorite contacts:", count_favorites(contacts))
```

You should see:

```text
Favorite contacts: 2
```

This function receives the contacts list.

It does not need to know where the contacts came from.

It only counts how many have `favorite` set to `True`.

That is one clear job.

### Step 4: Move Contact Formatting Into A Function

Code:

```python
def format_contact(contact):
    return contact["name"] + " - " + contact["phone"] + " (" + contact["city"] + ")"


contact = {"name": "Mina", "phone": "555-0101", "city": "Pune", "favorite": True}

print(format_contact(contact))
```

You should see:

```text
Mina - 555-0101 (Pune)
```

This function receives one contact.

It returns one string.

It does not print.

That means the formatted text could be used in many ways later:

- printed on the screen
- saved to a file
- added to a larger message
- compared in a small test

### Step 5: Use One Function Inside Another

Code:

```python
def format_contact(contact):
    return contact["name"] + " - " + contact["phone"] + " (" + contact["city"] + ")"


def print_contacts(contacts):
    for contact in contacts:
        print(format_contact(contact))


contacts = [
    {"name": "Mina", "phone": "555-0101", "city": "Pune", "favorite": True},
    {"name": "Sam", "phone": "555-0102", "city": "Chennai", "favorite": False},
    {"name": "Iris", "phone": "555-0103", "city": "Delhi", "favorite": True},
]

print_contacts(contacts)
```

You should see:

```text
Mina - 555-0101 (Pune)
Sam - 555-0102 (Chennai)
Iris - 555-0103 (Delhi)
```

This is a useful pattern.

One function can handle a larger job by calling a smaller function.

`print_contacts()` handles the list.

`format_contact()` handles one contact.

### Step 6: Put The Program Back Together

Code:

```python
def get_sample_contacts():
    return [
        {"name": "Mina", "phone": "555-0101", "city": "Pune", "favorite": True},
        {"name": "Sam", "phone": "555-0102", "city": "Chennai", "favorite": False},
        {"name": "Iris", "phone": "555-0103", "city": "Delhi", "favorite": True},
    ]


def count_favorites(contacts):
    favorite_count = 0

    for contact in contacts:
        if contact["favorite"]:
            favorite_count += 1

    return favorite_count


def format_contact(contact):
    return contact["name"] + " - " + contact["phone"] + " (" + contact["city"] + ")"


def print_contacts(contacts):
    for contact in contacts:
        print(format_contact(contact))


def print_contact_summary(contacts):
    print("Contact Summary")
    print("---------------")
    print("Total contacts:", len(contacts))
    print("Favorite contacts:", count_favorites(contacts))
    print()
    print_contacts(contacts)


def main():
    contacts = get_sample_contacts()
    print_contact_summary(contacts)


main()
```

You should see:

```text
Contact Summary
---------------
Total contacts: 3
Favorite contacts: 2

Mina - 555-0101 (Pune)
Sam - 555-0102 (Chennai)
Iris - 555-0103 (Delhi)
```

Try this:

```text
Add one more contact.
Run the program again.
Change how format_contact() builds the line.
Run the program again.
```

Notice what changes.

If you add a contact, the data changes.

If you change the contact line, only `format_contact()` needs to change.

That is a good sign.

## Common Mistake

A common mistake is splitting code into functions too mechanically.

Beginners sometimes create functions like this:

Code:

```python
def part_one(contacts):
    print("Contact Summary")
    print("---------------")
    print("Total contacts:", len(contacts))


def part_two(contacts):
    favorite_count = 0

    for contact in contacts:
        if contact["favorite"]:
            favorite_count += 1

    print("Favorite contacts:", favorite_count)


def part_three(contacts):
    for contact in contacts:
        print(contact["name"])
```

This code is valid Python.

But the split is weak.

The names `part_one`, `part_two`, and `part_three` do not explain the jobs.

They only explain the order.

A better split names the purpose:

Code:

```python
def print_report_heading(contacts):
    print("Contact Summary")
    print("---------------")
    print("Total contacts:", len(contacts))


def count_favorites(contacts):
    favorite_count = 0

    for contact in contacts:
        if contact["favorite"]:
            favorite_count += 1

    return favorite_count


def print_contact_names(contacts):
    for contact in contacts:
        print(contact["name"])
```

These names make the code easier to scan.

They also help you notice whether a function is doing too much.

Another common mistake is making one large function that still does everything.

Code:

```python
def handle_contacts(contacts):
    print("Contact Summary")
    print("---------------")
    print("Total contacts:", len(contacts))

    favorite_count = 0
    for contact in contacts:
        if contact["favorite"]:
            favorite_count += 1

    print("Favorite contacts:", favorite_count)
    print()

    for contact in contacts:
        print(contact["name"] + " - " + contact["phone"])
```

This puts code inside a function, but it does not really split the problem.

The function is still doing many jobs.

If a function name has to be vague, the function may be too large.

Names like these are warning signs:

```text
handle_data
do_stuff
process_everything
run_all
part_one
```

Tomorrow you will spend more time on function names.

For today, use this test:

```text
Can I say what this function does in one short sentence?
```

If not, the function may need to be split again.

## Debug It

When you split code into functions, one common bug is forgetting to return the result.

Broken code:

```python
def count_favorites(contacts):
    favorite_count = 0

    for contact in contacts:
        if contact["favorite"]:
            favorite_count += 1


def print_contact_summary(contacts):
    print("Favorite contacts:", count_favorites(contacts))


contacts = [
    {"name": "Mina", "favorite": True},
    {"name": "Sam", "favorite": False},
    {"name": "Iris", "favorite": True},
]

print_contact_summary(contacts)
```

You should see:

```text
Favorite contacts: None
```

The code is broken because `count_favorites()` calculates `favorite_count`, but never returns it.

In Python, a function that does not return anything gives back `None`.

The fix is to return the count after the loop finishes.

Fixed code:

```python
def count_favorites(contacts):
    favorite_count = 0

    for contact in contacts:
        if contact["favorite"]:
            favorite_count += 1

    return favorite_count


def print_contact_summary(contacts):
    print("Favorite contacts:", count_favorites(contacts))


contacts = [
    {"name": "Mina", "favorite": True},
    {"name": "Sam", "favorite": False},
    {"name": "Iris", "favorite": True},
]

print_contact_summary(contacts)
```

You should see:

```text
Favorite contacts: 2
```

When a refactored function gives a strange result, ask:

- Does the function receive the data it needs?
- Does the function return the value the rest of the program expects?
- Is the `return` line inside the right function?
- Is the `return` line after the loop, not too early?
- Is the main flow calling the new function?

Here is another broken refactor:

Broken code:

```python
def print_contact_names():
    for contact in contacts:
        print(contact["name"])


print_contact_names()
```

This is broken because the function uses `contacts`, but no `contacts` variable exists in this code.

It is better to pass the contacts into the function.

Fixed code:

```python
def print_contact_names(contacts):
    for contact in contacts:
        print(contact["name"])


contacts = [
    {"name": "Mina"},
    {"name": "Sam"},
    {"name": "Iris"},
]

print_contact_names(contacts)
```

You should see:

```text
Mina
Sam
Iris
```

Passing data into a function usually makes the function easier to understand.

It also makes the function easier to test with different data.

## Read the Docs

Python's official tutorial explains function definitions here:

[Python tutorial: Defining Functions](https://docs.python.org/3/tutorial/controlflow.html#defining-functions)

Today, focus only on the parts you already know:

- `def`
- parameters
- function calls
- `return`

The documentation includes advanced details too.

You do not need to understand every advanced function feature right now.

Try this:

```text
Find one example in the docs where a function returns a value.
Find one example where a function receives a parameter.
Write down which name is the function name.
```

The goal is not to memorize the docs.

The goal is to get more comfortable reading official examples.

## Mini Challenge

Build a small quiz report.

Use this starter data:

```python
answers = ["a", "c", "b", "b"]
correct_answers = ["a", "b", "b", "b"]
```

Write functions for these jobs:

```text
count correct answers
calculate percent score
choose a message
print the report
```

Your main flow can look like this:

```text
get the answers
count correct answers
calculate the percent
print the quiz report
```

You should see something like:

```text
Quiz Report
-----------
Correct answers: 3
Total questions: 4
Percent: 75.0
Nice work.
```

Hints:

- `count_correct()` should return a number.
- `calculate_percent()` should return a number.
- `get_score_message()` should return text.
- `print_quiz_report()` can print the final report.

Try to make each function small enough that you can test it with one or two lines.

## Real-World Use

Real programs are usually split into functions because real programs change.

A contact app might have functions for:

- loading contacts
- validating a phone number
- searching by name
- formatting one contact
- saving contacts
- printing a menu

A shopping app might have functions for:

- adding an item
- removing an item
- calculating a total
- applying a discount
- printing a receipt

A text utility might have functions for:

- cleaning extra spaces
- counting words
- finding a word
- replacing text
- printing a report

Notice the pattern.

Each function owns one job.

The main program decides the order.

That separation makes code easier to read, easier to debug, and easier to improve.

## Recap

Today you learned how to split a program into functions.

A useful split is based on jobs, not line count.

Good function candidates are often:

- repeated steps
- calculations you want to test
- formatting logic
- display logic
- chunks of code that are easier to understand with a name

You also practiced a simple refactoring flow:

```text
Make the program work.
Find the jobs.
Move one job into a function.
Run the program.
Move the next job into a function.
Run the program again.
Keep the main flow readable.
```

Move slowly when refactoring.

One function at a time is enough.

## Lesson Checklist

- [ ] I can find smaller jobs inside a longer program.
- [ ] I can explain why repeated code may become a function.
- [ ] I can write a function that receives data through a parameter.
- [ ] I can write a function that returns a calculated value.
- [ ] I can write a function that prints a report.
- [ ] I can use one function inside another function.
- [ ] I can keep the main program flow short and readable.
- [ ] I can avoid vague function names like `part_one`.
- [ ] I can debug a missing `return`.
- [ ] I can explain why splitting by job is better than splitting by line count.

## Exercises

### Exercise 1: Find The Jobs

Read this program description:

```text
A program stores a shopping list, prints the number of items,
prints each item, and warns the user if the list is empty.
```

Write down at least three possible function jobs.

Do not write the code yet.

Example job style:

```text
count items
print every item
show empty-list warning
```

### Exercise 2: Split A Shopping List Program

Write a program with these functions:

- `count_items(items)`
- `print_items(items)`
- `print_shopping_summary(items)`

Use this data:

```python
items = ["rice", "tea", "apples"]
```

Your program should print:

```text
Shopping Summary
----------------
Items: 3
rice
tea
apples
```

### Exercise 3: Format One Item

Write a function named `format_item(item, quantity)`.

It should return text like this:

```text
rice: 2
```

Then call it with at least three different items.

### Exercise 4: Use A Helper Function

Write a function named `print_inventory(items)`.

Each item should be a dictionary:

```python
items = [
    {"name": "rice", "quantity": 2},
    {"name": "tea", "quantity": 1},
    {"name": "apples", "quantity": 6},
]
```

Inside `print_inventory()`, call your `format_item()` function from Exercise 3.

### Exercise 5: Refactor A Text Utility

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
count words
print text report
make uppercase text
```

### Exercise 6: Fix The Missing Return

This code is supposed to print `Total: 15`.

Broken code:

```python
def calculate_total(numbers):
    total = 0

    for number in numbers:
        total += number


numbers = [4, 5, 6]
print("Total:", calculate_total(numbers))
```

Fix the function.

The problem is that it calculates `total`, but never returns it.

### Exercise 7: Pass The Data In

This code is supposed to print all task names.

Broken code:

```python
def print_tasks():
    for task in tasks:
        print(task)


print_tasks()
```

Fix it by:

- creating a `tasks` list
- adding a `tasks` parameter to the function
- passing the list into the function call

### Exercise 8: Keep Main Readable

Write a small program with a `main()` function.

The `main()` function should have only two or three lines inside it.

Example shape:

```text
def main():
    data = get_sample_data()
    print_report(data)
```

You choose the topic:

- contacts
- shopping
- quiz scores
- text report

### Exercise 9: Do Not Split Too Soon

Write a small program without functions first.

Make it work.

Then choose one job to move into a function.

Run the program again.

Then choose one more job.

Run the program again.

The exercise is to practice moving slowly.

### Exercise 10: Review An Older Program

Open an older program from this course.

Look for a section that could become a function.

Write down:

```text
Function name:
Data it needs:
What it should return or print:
Why this split helps:
```

You do not have to refactor the whole program.

Finding one good function is enough.

## Tiny Win

You can now look at a longer program and ask a better question:

```text
What jobs are hiding inside this code?
```

That question is one of the main habits of program design.

You are no longer only writing lines.

You are arranging responsibilities.

## Tomorrow

Tomorrow is:

```text
Day 65: Naming Functions Well
```

Today you practiced splitting a program into smaller jobs.

Tomorrow you will focus on the names.

A good function name helps the reader understand what the function does, what kind of result it gives back, and when it should be used.

Splitting the problem is the first step.

Naming the pieces well is the next one.
