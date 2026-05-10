# Day 63: Pure Functions

**Focus:** Writing functions that return predictable values without changing outside data  
**You will practice:** pure functions, return values, visible inputs, avoiding hidden changes, and separating calculations from display  
**Estimated time:** 45-60 minutes

## Today's Goal

Today you will learn about pure functions.

The name sounds more advanced than the idea.

A pure function follows three simple habits:

```text
The same input gives the same output.
The function returns a value.
The function does not change data outside itself.
```

You have already learned how to write functions, pass arguments, return values, and think about scope. Today puts those ideas together.

By the end of this lesson, you should be able to:

- explain what a pure function is
- write small functions that return values
- keep printing separate from calculating
- avoid changing global lists inside a function
- spot hidden inputs that make a function harder to trust
- explain why pure functions are easier to test
- use pure functions for small jobs like totals, names, labels, and scores
- prepare for splitting larger problems into smaller functions tomorrow

The main idea is:

```text
A pure function is a small, predictable helper.
```

It takes the information it needs through parameters.

It gives the answer back with `return`.

It does not quietly change something somewhere else.

## The Big Idea

Here is a pure function:

```python
def calculate_total(price, tax):
    return price + tax


total = calculate_total(20, 3)
print(total)
print(calculate_total(20, 3))
```

You should see:

```text
23
23
```

This function is pure because:

```text
The inputs are price and tax.
The output is the returned total.
Calling it with 20 and 3 always returns 23.
It does not print, ask for input, or change outside data.
```

Now compare it with this function:

```python
def print_total(price, tax):
    print(price + tax)


result = print_total(20, 3)
print(result)
```

You should see:

```text
23
None
```

This function is not useless. It does display the total.

But it does not give the total back to the program. The printed `23` appears on the screen, then the function returns `None`.

That matters if another part of the program needs to use the answer:

```python
def calculate_total(price, tax):
    return price + tax


total = calculate_total(20, 3)
message = "Your total is " + str(total)
print(message)
```

You should see:

```text
Your total is 23
```

Returning a value gives the program something it can keep using.

Printing shows something to the person running the program.

Both are useful. They are just different jobs.

## The Mental Model

Think of a pure function like a small calculator.

You give it visible inputs:

```text
20
3
```

It gives back a visible answer:

```text
23
```

It does not secretly check another variable.

It does not change your list of tasks.

It does not print the answer instead of returning it.

It simply receives values, does one small job, and returns a value.

Example:

```python
def format_name(first_name, last_name):
    clean_first = first_name.strip().title()
    clean_last = last_name.strip().title()
    return clean_first + " " + clean_last


full_name = format_name("  mina", "patel ")
print(full_name)
```

You should see:

```text
Mina Patel
```

The function does not need to know where the name came from.

It does not print the name itself.

It receives two strings and returns one cleaner string.

That makes the function easy to reuse:

```python
def format_name(first_name, last_name):
    clean_first = first_name.strip().title()
    clean_last = last_name.strip().title()
    return clean_first + " " + clean_last


print(format_name("asha", "rao"))
print(format_name("SAM", "khan"))
print(format_name("  leena", "das  "))
```

You should see:

```text
Asha Rao
Sam Khan
Leena Das
```

Same function.

Different inputs.

Predictable outputs.

## Try It Yourself

Create a file named:

```text
day-63/pure_functions.py
```

Work through these examples one at a time.

### Step 1: Calculate A Total

Code:

```python
def calculate_total(price, tax):
    return price + tax


first_total = calculate_total(50, 5)
second_total = calculate_total(100, 12)

print(first_total)
print(second_total)
```

You should see:

```text
55
112
```

Try this:

```text
Add a third call with different numbers.
Store the result in a variable.
Print the variable after the function call.
```

The function does not need to change.

Only the arguments change.

### Step 2: Format A Name

Code:

```python
def format_name(first_name, last_name):
    clean_first = first_name.strip().title()
    clean_last = last_name.strip().title()
    return clean_first + " " + clean_last


student_name = format_name("  ravi", "mehta ")
print(student_name)
```

You should see:

```text
Ravi Mehta
```

This function receives messy text and returns cleaner text.

It does not ask for the name with `input()`.

It does not print the name inside the function.

That keeps the job focused.

### Step 3: Check Adult Status

Code:

```python
def is_adult(age):
    return age >= 18


print(is_adult(21))
print(is_adult(16))
```

You should see:

```text
True
False
```

The function receives an age and returns a Boolean.

That returned value could be used in an `if` statement later:

```python
def is_adult(age):
    return age >= 18


age = 20

if is_adult(age):
    print("Adult account")
else:
    print("Child account")
```

You should see:

```text
Adult account
```

### Step 4: Build A Label

Code:

```python
def build_label(label, value):
    return label + ": " + str(value)


print(build_label("Name", "Mina"))
print(build_label("Score", 42))
print(build_label("Active", True))
```

You should see:

```text
Name: Mina
Score: 42
Active: True
```

The function does not care what kind of value it receives.

It converts the value to text and returns one label string.

### Step 5: Compute A Score

Code:

```python
def compute_score(correct_answers, bonus_points):
    return correct_answers * 10 + bonus_points


score = compute_score(7, 5)
print(score)
```

You should see:

```text
75
```

This function is easy to check because all the needed information is visible in the call:

```text
correct_answers receives 7
bonus_points receives 5
```

So the calculation is:

```text
7 * 10 + 5
```

That gives `75`.

## Common Mistake

Pure functions are mostly about habits.

These mistakes are common when your functions start doing more work.

### Mistake 1: Mixing `print` And `return`

Broken code:

```python
def calculate_total(price, tax):
    print(price + tax)


total = calculate_total(20, 3)
print("Saved total:", total)
```

You should see:

```text
23
Saved total: None
```

This is broken because the function prints the answer but does not return it.

If the rest of the program needs the total, use `return`.

Fixed code:

```python
def calculate_total(price, tax):
    return price + tax


total = calculate_total(20, 3)
print("Saved total:", total)
```

You should see:

```text
Saved total: 23
```

Printing is fine when the job is to display something.

Returning is better when the job is to calculate or prepare a value.

### Mistake 2: Changing A Global List

Broken code:

```python
tasks = ["study"]


def add_task(task):
    tasks.append(task)
    return tasks


new_tasks = add_task("practice")

print(tasks)
print(new_tasks)
```

You should see:

```text
['study', 'practice']
['study', 'practice']
```

This function changes `tasks`, even though `tasks` was created outside the function.

That can be surprising in a larger program.

A purer version receives the old list and returns a new list:

Fixed code:

```python
def add_task(tasks, task):
    return tasks + [task]


original_tasks = ["study"]
new_tasks = add_task(original_tasks, "practice")

print(original_tasks)
print(new_tasks)
```

You should see:

```text
['study']
['study', 'practice']
```

The original list stays unchanged.

The new list contains the added task.

### Mistake 3: Using Hidden Inputs

Broken code:

```python
tax_percent = 8


def calculate_tax(price):
    return price * tax_percent / 100


print(calculate_tax(100))
```

You should see:

```text
8.0
```

This code runs, but the function has a hidden input.

The call only shows `100`, but the answer also depends on `tax_percent`.

That means this function is harder to test by just reading the call.

Fixed code:

```python
def calculate_tax(price, tax_percent):
    return price * tax_percent / 100


print(calculate_tax(100, 8))
```

You should see:

```text
8.0
```

Now both inputs are visible:

```text
price receives 100
tax_percent receives 8
```

### Mistake 4: Doing Too Many Jobs

Broken code:

```python
discount = 5


def checkout(price):
    final_total = price - discount
    print("Final total:", final_total)
    return final_total


checkout(50)
```

You should see:

```text
Final total: 45
```

This function calculates, uses a hidden discount, prints, and returns.

It works, but it is carrying several jobs at once.

Fixed code:

```python
def calculate_discounted_total(price, discount):
    return price - discount


def format_total_message(total):
    return "Final total: " + str(total)


total = calculate_discounted_total(50, 5)
message = format_total_message(total)
print(message)
```

You should see:

```text
Final total: 45
```

Now each function has a smaller job.

One calculates.

One formats a message.

The `print()` call happens outside both helper functions.

## Debug It

Read the goal first.

Then study the broken code and find what makes the function less predictable.

### Debug 1: Same Input, Different Output

Goal:

```text
Calling compute_score(3, 10) should always return 30.
```

Broken code:

```python
points_per_correct = 10


def compute_score(correct_answers):
    return correct_answers * points_per_correct


print(compute_score(3))

points_per_correct = 20
print(compute_score(3))
```

You should see:

```text
30
60
```

The same visible input, `3`, gives two different outputs because the function uses `points_per_correct` from outside.

Fixed code:

```python
def compute_score(correct_answers, points_per_correct):
    return correct_answers * points_per_correct


print(compute_score(3, 10))
print(compute_score(3, 10))
```

You should see:

```text
30
30
```

Now the points value is a visible argument.

### Debug 2: A Function Changes The List

Goal:

```text
Return formatted names without changing the original list.
```

Broken code:

```python
names = ["mina", "sam"]


def format_names():
    for index in range(len(names)):
        names[index] = names[index].title()
    return names


print(format_names())
print(names)
```

You should see:

```text
['Mina', 'Sam']
['Mina', 'Sam']
```

This changes the outside list.

That may not be what the rest of the program expected.

Fixed code:

```python
def format_names(names):
    formatted_names = []

    for name in names:
        formatted_names.append(name.title())

    return formatted_names


student_names = ["mina", "sam"]

print(format_names(student_names))
print(student_names)
```

You should see:

```text
['Mina', 'Sam']
['mina', 'sam']
```

The function returns a new list.

The original list stays the same.

### Debug 3: A Function Prints Too Early

Goal:

```text
Build a label, save it, then print it later.
```

Broken code:

```python
def build_label(label, value):
    print(label + ": " + str(value))


score_label = build_label("Score", 88)
print("Saved:", score_label)
```

You should see:

```text
Score: 88
Saved: None
```

The function displays the label, but it does not return the label.

Fixed code:

```python
def build_label(label, value):
    return label + ": " + str(value)


score_label = build_label("Score", 88)
print("Saved:", score_label)
```

You should see:

```text
Saved: Score: 88
```

If a function builds a value, return the value.

Let the caller decide when to print it.

## Read the Docs

Python's official documentation is useful for noticing whether a tool returns a new value or changes an existing value.

Look up these two entries:

```text
https://docs.python.org/3/library/functions.html#sorted
https://docs.python.org/3/tutorial/datastructures.html#more-on-lists
```

`sorted()` returns a new sorted list.

Code:

```python
scores = [30, 10, 20]

sorted_scores = sorted(scores)

print(scores)
print(sorted_scores)
```

You should see:

```text
[30, 10, 20]
[10, 20, 30]
```

The original list did not change.

Now compare that with the list method `.sort()`.

Code:

```python
scores = [30, 10, 20]

scores.sort()

print(scores)
```

You should see:

```text
[10, 20, 30]
```

`.sort()` changes the list itself.

Neither tool is automatically better.

Choose based on the job:

```text
Need a new sorted value? Use sorted().
Need to sort the list in place? Use .sort().
```

When reading documentation, ask:

```text
Does this return a new value?
Does this change the existing object?
Does this print something?
Does this need hidden information?
```

Those questions help you understand how a function behaves.

## Mini Challenge

Create a file named:

```text
day-63/score_report.py
```

Build a small score report using pure helper functions.

Your program should define these functions:

- `calculate_total(price, tax)`
- `format_name(first_name, last_name)`
- `is_adult(age)`
- `build_label(label, value)`
- `compute_score(correct_answers, bonus_points)`

Rules:

```text
Each function should return a value.
Do not use print() inside these functions.
Do not use input() inside these functions.
Do not change a global list inside these functions.
Print the final report after the function calls.
```

One possible solution:

```python
def calculate_total(price, tax):
    return price + tax


def format_name(first_name, last_name):
    clean_first = first_name.strip().title()
    clean_last = last_name.strip().title()
    return clean_first + " " + clean_last


def is_adult(age):
    return age >= 18


def build_label(label, value):
    return label + ": " + str(value)


def compute_score(correct_answers, bonus_points):
    return correct_answers * 10 + bonus_points


student_name = format_name("  mina", "patel ")
student_age = 19
total_cost = calculate_total(40, 5)
student_score = compute_score(8, 3)

print(build_label("Name", student_name))
print(build_label("Adult", is_adult(student_age)))
print(build_label("Total cost", total_cost))
print(build_label("Score", student_score))
```

You should see:

```text
Name: Mina Patel
Adult: True
Total cost: 45
Score: 83
```

After it works, change only the values near the bottom.

Do not change the function definitions.

That is one sign that your helper functions are reusable.

## Real-World Use

Pure functions are useful because they are easy to test.

Example:

```python
def calculate_total(price, tax):
    return price + tax


print(calculate_total(20, 3) == 23)
print(calculate_total(0, 5) == 5)
print(calculate_total(10, 0) == 10)
```

You should see:

```text
True
True
True
```

Each line is a tiny check.

You do not need to type input.

You do not need to read a printed sentence.

You do not need to wonder whether another variable changed the answer.

Pure functions are also easier to debug.

If this call is wrong:

```text
compute_score(7, 5)
```

you know where to look:

```text
the function body
the arguments 7 and 5
```

There are fewer hiding places.

Pure functions are also easier to reuse.

A function like this:

```python
def build_label(label, value):
    return label + ": " + str(value)
```

can be used in many places:

```text
printed on the screen
saved to a file
shown in a menu
used in a report
checked in a test
```

The function only builds the label.

The caller decides what to do with it.

Not every function in a real program will be pure.

Some functions should print.

Some functions should ask for input.

Some functions should save data.

Some functions should update a list on purpose.

Pure functions are especially helpful for the inside work of a program:

```text
calculating
formatting
checking
converting
building small values
```

Keep the messy outside actions near the edges of the program.

Keep the small thinking work in pure helpers when you can.

## Recap

Today you learned that a pure function is predictable.

You practiced:

- writing functions that return values
- using parameters as visible inputs
- keeping `print()` outside calculation helpers
- formatting names
- checking adult status
- building labels
- calculating totals
- computing scores
- avoiding hidden global inputs
- avoiding changes to outside lists
- comparing returned values with printed output
- noticing whether a function returns a new value or changes an existing value

The key idea:

```text
Same input, same output, no hidden changes.
```

The key habit:

```text
Put information into a function with parameters.
Get information out with return.
Print outside when you only need to display the final result.
```

## Lesson Checklist

Before moving on, check that you can:

- explain what a pure function is
- explain why printing is different from returning
- write a function that calculates and returns a total
- write a function that formats and returns a name
- write a function that returns `True` or `False`
- write a function that builds and returns a label
- write a function that computes and returns a score
- spot a function that changes a global list
- rewrite a function so it receives the list as a parameter
- avoid using hidden global values as inputs
- keep a helper function focused on one job
- explain why pure functions are easier to test
- explain why pure functions are easier to reuse

## Exercises

### Exercise 1

Write a function named `calculate_total`.

It should have two parameters:

```text
price
tax
```

It should return the price plus the tax.

Call it with `25` and `4`, store the result, and print the result.

### Exercise 2

Write a function named `format_name`.

It should receive:

```text
first_name
last_name
```

It should return one full name.

Try it with extra spaces and lowercase letters.

### Exercise 3

Write a function named `is_adult`.

It should return `True` when the age is at least `18`.

It should return `False` otherwise.

### Exercise 4

Write a function named `build_label`.

This call:

```text
build_label("City", "Pune")
```

should return:

```text
City: Pune
```

Print the returned value outside the function.

### Exercise 5

Write a function named `compute_score`.

It should receive:

```text
correct_answers
bonus_points
```

Each correct answer is worth `10` points.

Return the final score.

### Exercise 6

Fix the broken code.

Broken code:

```python
def calculate_total(price, tax):
    print(price + tax)


total = calculate_total(30, 4)
print("Total:", total)
```

The goal is:

```text
Total: 34
```

### Exercise 7

Fix the broken code.

Broken code:

```python
discount = 5


def calculate_total(price):
    return price - discount


print(calculate_total(40))
```

The function should receive the discount as a parameter.

### Exercise 8

Fix the broken code.

Broken code:

```python
items = ["pen"]


def add_item(item):
    items.append(item)
    return items


print(add_item("notebook"))
print(items)
```

Rewrite it so the function receives the list and returns a new list.

The original list should stay unchanged.

### Exercise 9

Decide whether this function is pure.

```python
def format_city(city):
    return city.strip().title()
```

Explain your answer in one or two sentences.

### Exercise 10

Decide whether this function is pure.

```python
def ask_for_city():
    city = input("City: ")
    return city.strip().title()
```

Explain your answer in one or two sentences.

### Exercise 11

Write a pure function named `make_username`.

It should receive:

```text
first_name
birth_year
```

It should return a username like:

```text
mina2004
```

Do not print inside the function.

### Exercise 12

Write a pure function named `apply_discount`.

It should receive:

```text
price
discount
```

It should return the discounted price.

Then print the returned value outside the function.

### Exercise 13

Write a pure function named `get_status_message`.

It should receive a score.

If the score is at least `50`, return:

```text
Pass
```

Otherwise, return:

```text
Try again
```

### Exercise 14

Choose one short program from an earlier day.

Find one part that calculates, formats, checks, or builds a value.

Move that part into a pure function.

Keep the `print()` calls outside the pure function.

## Tiny Win

You can now write functions that behave like reliable little tools.

When the inputs are clear and the return value is clear, the function becomes easier to test, debug, and reuse.

That makes bigger programs feel less tangled.

## Tomorrow

Tomorrow is:

```text
Day 64: Splitting Problems Into Functions
```

Today you practiced making one small function predictable.

Tomorrow you will take a larger problem and split it into several functions that work together.

Pure functions will help because each helper can have:

```text
clear inputs
one focused job
one returned result
```

That is how a bigger program starts to feel manageable.
