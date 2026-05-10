# Day 56: Why Functions Exist

**Focus:** Understanding the problem functions solve  
**You will practice:** spotting repeated jobs, naming small actions, reading tiny function previews, and deciding when a chunk of code deserves a name  
**Estimated time:** 40-50 minutes

## Today's Goal

Today you will learn why functions exist.

You are not trying to memorize all function syntax yet. That starts tomorrow.

Today is about the idea:

> A function is a named action that a program can reuse.

You have already used functions many times:

```python
print("Hello")
len(["milk", "rice"])
sorted(["zebra", "apple", "book"])
```

`print()`, `len()`, and `sorted()` are functions Python already gives you.

Soon, you will write your own.

By the end of this lesson, you should be able to:

- explain a function as a named reusable action
- spot repeated code that could become a function
- describe why functions make programs easier to read
- explain how functions isolate one small job
- see how functions make projects easier to change
- read a tiny function preview without needing every syntax detail yet
- prepare for Day 57, where you will write simple functions yourself

The main idea:

```text
When a program has a small job it needs to do more than once, give that job a name.
```

That name becomes a tool your program can use.

## The Big Idea

A program is often a set of steps.

At first, writing every step directly is fine.

Example:

```python
print("Hello, Maya.")
print("Welcome back.")

print("Hello, Iris.")
print("Welcome back.")

print("Hello, Sam.")
print("Welcome back.")
```

You should see:

```text
Hello, Maya.
Welcome back.
Hello, Iris.
Welcome back.
Hello, Sam.
Welcome back.
```

This works.

But notice the repeated job:

```text
greet a person
```

That job has two steps:

```text
print hello with the person's name
print welcome back
```

When code repeats the same job, a function lets you name that job once and reuse it.

Code:

```python
def greet(name):
    print("Hello, " + name + ".")
    print("Welcome back.")

greet("Maya")
greet("Iris")
greet("Sam")
```

You should see:

```text
Hello, Maya.
Welcome back.
Hello, Iris.
Welcome back.
Hello, Sam.
Welcome back.
```

Do not worry about every symbol yet.

For now, read it like this:

```text
Define a reusable action named greet.
It needs a name to greet.
When the action runs, it prints two lines.

Run greet for Maya.
Run greet for Iris.
Run greet for Sam.
```

The function does not make the program magical.

It gives one repeated job a clear name.

That helps in four important ways:

```text
less repeated code
clearer reading
smaller jobs
easier changes
```

Functions are not only about saving typing.

They are about giving shape to a program.

## The Mental Model

Think of a function as a recipe card.

The card has a name:

```text
make tea
```

The card has steps:

```text
boil water
add tea
wait
pour
```

Once the recipe exists, you do not rewrite every step each time.

You can simply say:

```text
make tea
```

In Python, a function works in a similar way.

It gives a name to steps that belong together.

Example:

```python
def show_menu():
    print("Menu:")
    print("1. Show contacts")
    print("2. Add contact")
    print("3. Quit")

show_menu()
show_menu()
```

You should see:

```text
Menu:
1. Show contacts
2. Add contact
3. Quit
Menu:
1. Show contacts
2. Add contact
3. Quit
```

The function name `show_menu` tells you what the block does.

That matters because code is read more often than it is written.

Compare this:

```python
print("Menu:")
print("1. Show contacts")
print("2. Add contact")
print("3. Quit")
```

with this:

```text
show_menu()
```

The first version shows every detail.

The second version tells the story:

```text
show the menu
```

Both are useful at different times.

When you are building a tiny program, direct steps are fine.

When a program grows, named actions help you see the larger shape:

```text
show_menu()
get_choice()
add_contact()
print_contacts()
```

You have not learned how to write all of those yet.

Today, just notice how the names make the program easier to scan.

## Try It Yourself

You do not need to write a large program today.

Create this file:

```text
day-56/function_preview.py
```

Try this:

```python
def print_contact(contact):
    print(contact["name"])
    print(contact["phone"])
    print(contact["email"])

contact_one = {
    "name": "Mina",
    "phone": "555-0104",
    "email": "mina@example.com"
}

contact_two = {
    "name": "Sam",
    "phone": "555-0199",
    "email": "sam@example.com"
}

print_contact(contact_one)
print("")
print_contact(contact_two)
```

You should see:

```text
Mina
555-0104
mina@example.com

Sam
555-0199
sam@example.com
```

The function is named `print_contact`.

That name is useful because the code inside the function has one job:

```text
print one contact
```

Without the function, you might write this:

```text
print(contact_one["name"])
print(contact_one["phone"])
print(contact_one["email"])

print("")

print(contact_two["name"])
print(contact_two["phone"])
print(contact_two["email"])
```

That also works.

But if you later want every contact to print with labels, you have to change every copied print block.

With a function, the change happens in one place.

Code:

```python
def print_contact(contact):
    print("Name:", contact["name"])
    print("Phone:", contact["phone"])
    print("Email:", contact["email"])

contact = {
    "name": "Iris",
    "phone": "555-0130",
    "email": "iris@example.com"
}

print_contact(contact)
```

You should see:

```text
Name: Iris
Phone: 555-0130
Email: iris@example.com
```

The main habit today is not typing `def` perfectly.

The habit is asking:

```text
What small job is this code doing?
Would a name make that job easier to understand?
Will I need this job again?
```

## Common Mistake

A common beginner mistake is thinking functions are only for code that repeats.

Repetition is one good reason to create a function.

But it is not the only reason.

Sometimes a function is useful because it gives a complicated job a clear name.

Example:

```python
score = 3
total_questions = 5

percentage = int(score * 100 / total_questions)

if percentage == 100:
    print("Perfect score.")
elif percentage >= 60:
    print("Good work.")
else:
    print("Keep practicing.")
```

You should see:

```text
Good work.
```

This code does not repeat.

Still, there are two separate jobs:

```text
calculate a percentage
choose a message
```

Later, those jobs might become functions:

```python
def show_score_message(score, total_questions):
    percentage = int(score * 100 / total_questions)

    if percentage == 100:
        print("Perfect score.")
    elif percentage >= 60:
        print("Good work.")
    else:
        print("Keep practicing.")

show_score_message(3, 5)
```

You should see:

```text
Good work.
```

Again, do not focus on writing this from memory yet.

Notice the name:

```text
show_score_message
```

That name hides the details until you need them.

A good function name lets the reader understand the program before reading every line inside.

## Debug It

Functions have a new rule that can surprise beginners:

```text
A function does not run just because it exists.
```

Defining a function means:

```text
Here are the steps for later.
```

Calling a function means:

```text
Run those steps now.
```

Broken code:

```python
def show_menu():
    print("Menu:")
    print("1. Add contact")
    print("2. Show contacts")
    print("3. Quit")
```

This code is broken as a complete program because it defines the action but never calls it.

If you run it, nothing prints.

The function is waiting to be used.

Fixed code:

```python
def show_menu():
    print("Menu:")
    print("1. Add contact")
    print("2. Show contacts")
    print("3. Quit")

show_menu()
```

You should see:

```text
Menu:
1. Add contact
2. Show contacts
3. Quit
```

Another common bug is using a value the function does not have.

Broken code:

```python
def greet():
    print("Hello, " + name + ".")

greet()
```

This is broken because the function uses `name`, but no `name` exists inside the function or before the function call.

One fixed version gives the function the value it needs:

```python
def greet(name):
    print("Hello, " + name + ".")

greet("Maya")
```

You should see:

```text
Hello, Maya.
```

You will practice this more tomorrow.

For today, remember:

```text
Define the function.
Call the function.
Give it the values it needs.
```

## Read the Docs

You have already used built-in functions from Python.

A built-in function is a function that is ready to use without you writing it.

Examples:

```python
names = ["Mina", "Sam", "Iris"]

print(len(names))
print(sorted(names))
```

You should see:

```text
3
['Iris', 'Mina', 'Sam']
```

Look up Python's documentation for built-in functions and find `len()`.

Do not try to read the whole page.

Just answer these questions:

```text
What does len() return?
What kind of values have you used len() with already?
What does the function name make you think it does?
```

The important connection is this:

```text
Python gives you useful named actions.
You can write your own useful named actions too.
```

## Mini Challenge

Look at this repeated code from a small quiz:

```python
score = 0
total_questions = 3

score = score + 1
print("Score:", score, "out of", total_questions)

score = score + 1
print("Score:", score, "out of", total_questions)

score = score + 1
print("Score:", score, "out of", total_questions)
```

You should see:

```text
Score: 1 out of 3
Score: 2 out of 3
Score: 3 out of 3
```

The repeated job is:

```text
show the current score
```

A function preview might look like this:

```python
def show_score(score, total_questions):
    print("Score:", score, "out of", total_questions)

score = 0
total_questions = 3

score = score + 1
show_score(score, total_questions)

score = score + 1
show_score(score, total_questions)

score = score + 1
show_score(score, total_questions)
```

You should see:

```text
Score: 1 out of 3
Score: 2 out of 3
Score: 3 out of 3
```

Your challenge:

Write down names for functions that could help these old projects.

Do not write the full functions yet.

For a greeting program:

```text
greet_user
ask_profile_questions
print_profile
```

For a quiz game:

```text
ask_question
show_score
show_final_result
```

For a shopping list or contact book menu:

```text
show_menu
get_choice
print_items
print_contacts
```

A good function name usually starts with an action word:

```text
show
get
ask
print
add
remove
update
calculate
```

You are practicing the design skill before the syntax skill.

## Real-World Use

Functions appear anywhere a program has named work to do.

A contact book might have functions like:

```text
show_menu
add_contact
find_contact
print_contact
print_all_contacts
```

Each name points to one job.

That makes the project easier to change.

Imagine the contact book prints contacts like this:

```text
Mina - 555-0104 - mina@example.com
```

Later, you want labels:

```text
Name: Mina
Phone: 555-0104
Email: mina@example.com
```

If contact printing is copied in five places, you have to update five places.

If contact printing lives in one function named `print_contact`, you update one place.

Functions also help you avoid mixing jobs together.

This is harder to read:

```text
show menu
ask for choice
print contact details
update score
ask another question
remove item
print menu again
```

This is easier to scan:

```text
show_menu()
handle_choice()
print_contact(contact)
show_score(score, total_questions)
```

The second version still needs real code behind the names.

But the names help the reader understand the program's plan.

Good functions make code feel less like one long paragraph and more like clear sections.

## Recap

A function is a named reusable action.

You have already used built-in functions like:

```text
print
len
sorted
input
```

Writing your own function lets you take steps that belong together and give them a name.

Functions help because they:

- reduce repeated code
- make programs easier to read
- isolate one small job
- make projects easier to change
- let the main program show the big picture

The tiny preview shape is:

```python
def function_name():
    print("Do a small job.")

function_name()
```

You do not need to master that shape today.

You only need to understand why it is useful.

The question to ask is:

```text
What job deserves a name?
```

## Lesson Checklist

Before moving on, check that you can:

- explain a function as a named action
- identify repeated code that could become a function
- name a small job from an old program
- explain why copied code can be hard to change
- explain why a function does not run until it is called
- read a tiny `def` preview without needing every detail yet
- describe how functions will help with menus, score messages, greetings, and contact printing

## Exercises

### Exercise 1

Look at this code:

```python
print("Hello, Mina.")
print("Welcome back.")

print("Hello, Sam.")
print("Welcome back.")
```

What repeated job could become a function?

Write only the function name you would choose.

### Exercise 2

Choose the best function name for each job.

```text
Print the menu for a contact book.
Print one contact's name, phone, and email.
Add one point to a quiz score.
Show the final score.
Ask the user for their name.
```

Use action words like `show`, `print`, `add`, `ask`, or `get`.

### Exercise 3

Read this preview:

```python
def show_menu():
    print("Menu:")
    print("1. Add")
    print("2. Quit")

show_menu()
```

Answer these questions:

```text
What is the function name?
How many print lines are inside the function?
Which line runs the function?
```

### Exercise 4

This code defines a function but does not call it.

Broken code:

```python
def greet_user():
    print("Hello.")
    print("Ready to practice Python?")
```

Add the missing function call.

### Exercise 5

Look at this contact code:

```python
contact = {
    "name": "Asha",
    "phone": "555-0188",
    "email": "asha@example.com"
}

print(contact["name"])
print(contact["phone"])
print(contact["email"])
```

What function name would describe the three print lines?

### Exercise 6

Look at this score code:

```python
score = 2
total_questions = 5

print("Score:", score, "out of", total_questions)
```

What small job is the final line doing?

Write a function name for that job.

### Exercise 7

Choose one old project:

```text
conversation program
quiz game
number guessing game
shopping list app
contact book
```

List three small jobs in that project.

Example:

```text
show menu
ask for choice
print contacts
```

### Exercise 8

Read these possible function names:

```text
thing
do_stuff
show_menu
print_contact
handle_it
calculate_total
```

Which names are clear?

Which names are too vague?

Write one sentence explaining your choices.

### Exercise 9

This code repeats a message:

```python
print("Item added.")
print("Remember to save your list.")

print("Item removed.")
print("Remember to save your list.")
```

What repeated line could become a function?

What would you name it?

### Exercise 10

Preview only.

Fill in the missing function call:

```python
def say_goodbye():
    print("Goodbye.")

# Write the call below this line.
```

### Exercise 11

Write a short paragraph answering this question:

```text
Why can functions make a project easier to change?
```

Use one example from a greeting, score update, menu display, or contact printing program.

### Exercise 12

Look at an old file you wrote earlier in the course.

Find one place where:

```text
several lines work together
the job has a clear purpose
the code might be useful again
```

Write the job in plain English.

Then write a possible function name.

Do not refactor the old file yet.

Tomorrow you will start writing functions directly.

## Tiny Win

You learned the reason functions exist before getting deep into syntax.

That matters.

When you see this tomorrow:

```python
def greet():
    print("Hello.")
```

it should not feel like a random new shape.

It means:

```text
Give these steps a name so the program can use them later.
```

That is the tiny win:

```text
You can now look at code and ask what job deserves a name.
```

## Tomorrow

Tomorrow is:

```text
Day 57: Writing Functions
```

Today you focused on why functions exist.

Tomorrow you will practice the basic syntax:

```text
def
function names
indentation
calling a function
writing more than one function
```

You will keep the programs small.

The goal will be to turn today's idea into working code:

```text
name a job
write the steps
call the job when needed
```

Functions are one of the main tools that help small programs grow without turning into one long, tangled file.
