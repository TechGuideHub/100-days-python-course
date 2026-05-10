# Day 59: Return Values

**Focus:** Sending results back from functions with `return`  
**You will practice:** returning values, storing returned values, using returned strings, numbers, booleans, and lists, and fixing common return mistakes  
**Estimated time:** 45-60 minutes

## Today's Goal

Today you will learn how a function can send a result back to the rest of your program.

Yesterday, you learned how parameters send values into a function.

Today, you will learn how `return` sends a value out of a function.

By the end of this lesson, you should be able to:

- explain what `return` does
- tell the difference between printing a value and returning a value
- store a returned value in a variable
- use a returned value in another calculation
- use a returned value in a message
- return strings, numbers, booleans, and lists
- explain why code after `return` does not run
- fix common mistakes with missing return values
- prepare for Day 60, where parameters can have default values

The main idea is:

```text
print shows a value to the user.
return gives a value back to the program.
```

Both are useful.

They solve different problems.

## The Big Idea

A function can do work in two common ways.

It can print something:

```python
def show_total(price, tax):
    total = price + tax
    print("Total:", total)


show_total(20, 3)
```

You should see:

```text
Total: 23
```

This is useful when the function's job is to display something.

But what if the program needs to use the total again?

For example:

```text
calculate the total
add shipping
show a final message
save the total for later
```

Printing alone is not enough for that.

The function needs to hand the result back.

That is what `return` does.

Code:

```python
def calculate_total(price, tax):
    total = price + tax
    return total


bill_total = calculate_total(20, 3)

print("Total:", bill_total)
print("With shipping:", bill_total + 5)
```

You should see:

```text
Total: 23
With shipping: 28
```

In this line:

```python
bill_total = calculate_total(20, 3)
```

the function call gives back `23`.

Python stores that returned value in `bill_total`.

Then the rest of the program can use it.

That is the difference:

```text
print: display the answer
return: give the answer back
```

When a function returns a value, the function call can be used anywhere that value would make sense.

Example:

```python
def add_tax(price):
    return price + 2


print("Notebook total:", add_tax(8))
```

You should see:

```text
Notebook total: 10
```

The function call `add_tax(8)` is replaced by the value it returns.

## The Mental Model

Think of a function call as asking a small worker to do one job.

Parameters are the values you give the function.

`return` is the value the function gives back.

Example:

```python
def add_points(score, points):
    new_score = score + points
    return new_score


current_score = add_points(10, 5)
print(current_score)
```

You should see:

```text
15
```

Read it like this:

```text
Call add_points.
Send in 10 and 5.
Inside the function, calculate 15.
Return 15.
Store 15 in current_score.
Print current_score.
```

The returned value comes back to the exact place where the function was called.

This means you can use a returned value directly in another expression:

```python
def double(number):
    return number * 2


answer = double(6) + 3
print(answer)
```

You should see:

```text
15
```

Python runs `double(6)` first.

That returns `12`.

Then Python finishes the calculation:

```text
12 + 3
```

One more rule matters:

```text
When a function reaches return, the function stops.
```

Code:

```python
def choose_status(score):
    if score >= 60:
        return "passing"

    return "practicing"


status = choose_status(75)
print(status)
```

You should see:

```text
passing
```

Because `score` is at least `60`, Python returns `"passing"` and leaves the function.

It does not continue looking for another result.

## Try It Yourself

Create a file named:

```text
day-59/return_values.py
```

Work through these examples one at a time.

### Step 1: Return A Number

Code:

```python
def add_numbers(first, second):
    return first + second


sum_result = add_numbers(8, 4)
print(sum_result)
```

You should see:

```text
12
```

The function does not print the sum.

It returns the sum.

The variable `sum_result` stores the returned number.

### Step 2: Use A Returned Number In Another Calculation

Code:

```python
def calculate_subtotal(price, quantity):
    return price * quantity


subtotal = calculate_subtotal(5, 3)
shipping = 2

print("Subtotal:", subtotal)
print("Final total:", subtotal + shipping)
```

You should see:

```text
Subtotal: 15
Final total: 17
```

The returned value is not stuck inside the function.

Once it is stored in `subtotal`, the program can use it again.

### Step 3: Return A String

Code:

```python
def make_greeting(name):
    return "Hello, " + name + "!"


message = make_greeting("Mina")

print(message)
print(message.upper())
```

You should see:

```text
Hello, Mina!
HELLO, MINA!
```

The function returns a string.

After the string is stored in `message`, you can print it, change it, combine it, or pass it into another function.

### Step 4: Return A Boolean

Code:

```python
def is_passing(score):
    return score >= 60


passed = is_passing(72)
print(passed)

if is_passing(45):
    print("Passed")
else:
    print("Keep practicing")
```

You should see:

```text
True
Keep practicing
```

The expression `score >= 60` already creates a boolean value.

The function returns that boolean value.

This is useful when a function's job is to answer a yes-or-no question.

Function names that return booleans often start with words like:

```text
is
has
can
should
```

Examples:

```text
is_passing
has_items
can_vote
should_continue
```

### Step 5: Return A List

Code:

```python
def get_open_tasks(tasks):
    open_tasks = []

    for task in tasks:
        if not task["done"]:
            open_tasks.append(task["title"])

    return open_tasks


tasks = [
    {"title": "Read lesson", "done": False},
    {"title": "Drink water", "done": True},
    {"title": "Practice return", "done": False},
]

unfinished = get_open_tasks(tasks)

print(unfinished)
print("Open tasks:", len(unfinished))
```

You should see:

```text
['Read lesson', 'Practice return']
Open tasks: 2
```

A function can return a list just like it can return a number or a string.

The type of value depends on the job the function is doing.

## Common Mistake

Most return mistakes come from mixing up two ideas:

```text
showing a value
giving a value back
```

### Mistake 1: Forgetting `return`

Broken code:

```python
def calculate_total(price, tax):
    total = price + tax


bill_total = calculate_total(20, 3)
print(bill_total)
```

You should see:

```text
None
```

This code is broken for the goal because the function calculates `total`, but it never returns it.

When a function does not return a value, Python gives back `None`.

Fixed code:

```python
def calculate_total(price, tax):
    total = price + tax
    return total


bill_total = calculate_total(20, 3)
print(bill_total)
```

You should see:

```text
23
```

### Mistake 2: Printing Instead Of Returning

Broken code:

```python
def calculate_total(price, tax):
    total = price + tax
    print(total)


bill_total = calculate_total(20, 3)
print("With shipping:", bill_total + 5)
```

This is broken because `calculate_total()` prints `23`, but it does not return `23`.

So `bill_total` receives `None`.

Then Python cannot add `None + 5`.

Fixed code:

```python
def calculate_total(price, tax):
    total = price + tax
    return total


bill_total = calculate_total(20, 3)
print("With shipping:", bill_total + 5)
```

You should see:

```text
With shipping: 28
```

Use `print()` when the job is to display something.

Use `return` when the rest of the program needs the value.

### Mistake 3: Expecting Code After `return` To Run

Code:

```python
def check_age(age):
    if age >= 18:
        return "adult"
        print("This line will not run.")

    return "minor"


status = check_age(20)
print(status)
```

You should see:

```text
adult
```

The `print()` line after `return "adult"` never runs.

As soon as Python reaches `return`, it leaves the function.

If you want something to happen before the function returns, put it before `return`.

### Mistake 4: Calling A Function But Ignoring The Result

Broken code:

```python
def make_greeting(name):
    return "Hello, " + name + "!"


make_greeting("Mina")
print("Greeting created.")
```

You should see:

```text
Greeting created.
```

This code calls the function, but it does not store or print the returned value.

The greeting is created and then ignored.

Fixed code:

```python
def make_greeting(name):
    return "Hello, " + name + "!"


message = make_greeting("Mina")
print(message)
```

You should see:

```text
Hello, Mina!
```

You do not always need to store a returned value.

But you do need to use it somehow.

These both use the returned value:

```python
def make_greeting(name):
    return "Hello, " + name + "!"


message = make_greeting("Sam")
print(message)

print(make_greeting("Iris"))
```

You should see:

```text
Hello, Sam!
Hello, Iris!
```

### Mistake 5: Forgetting To Call The Function

Broken code:

```python
def make_greeting(name):
    return "Hello, " + name + "!"


message = make_greeting
print(message)
```

This is broken for the goal because `make_greeting` without parentheses is the function itself.

It does not call the function.

It also does not send in the required `name`.

Fixed code:

```python
def make_greeting(name):
    return "Hello, " + name + "!"


message = make_greeting("Mina")
print(message)
```

You should see:

```text
Hello, Mina!
```

The parentheses matter:

```text
make_greeting      the function object
make_greeting()    a function call
```

When a function has a parameter, the call also needs the argument:

```python
make_greeting("Mina")
```

## Debug It

Read each goal first.

Then study the broken code and find the problem before looking at the fix.

### Debug 1: Discounted Price

Goal:

```text
Discounted price: 80
```

Broken code:

```python
def apply_discount(price, discount):
    price - discount


new_price = apply_discount(100, 20)
print("Discounted price:", new_price)
```

The problem:

```text
The function subtracts the numbers, but it does not return the answer.
```

Fixed code:

```python
def apply_discount(price, discount):
    return price - discount


new_price = apply_discount(100, 20)
print("Discounted price:", new_price)
```

You should see:

```text
Discounted price: 80
```

### Debug 2: Bonus Points

Goal:

```text
Final score: 15
```

Broken code:

```python
def add_bonus(score):
    return score + 5


final_score = add_bonus
print("Final score:", final_score)
```

The problem:

```text
The function was stored instead of called.
The call needs parentheses and an argument.
```

Fixed code:

```python
def add_bonus(score):
    return score + 5


final_score = add_bonus(10)
print("Final score:", final_score)
```

You should see:

```text
Final score: 15
```

### Debug 3: Build A Full Message

Goal:

```text
Mina, welcome back.
```

Broken code:

```python
def build_message(name):
    return name + ", "
    return "welcome back."


message = build_message("Mina")
print(message)
```

The problem:

```text
The first return ends the function.
The second return is never reached.
```

Fixed code:

```python
def build_message(name):
    return name + ", welcome back."


message = build_message("Mina")
print(message)
```

You should see:

```text
Mina, welcome back.
```

### Debug 4: Return A Finished List

Goal:

```text
[3, 5]
```

Broken code:

```python
def get_positive_numbers(numbers):
    positives = []

    for number in numbers:
        if number > 0:
            positives.append(number)

        return positives


result = get_positive_numbers([-2, 3, 5, -1])
print(result)
```

The problem:

```text
The return line is inside the loop.
The function returns after the first number instead of checking the whole list.
```

Fixed code:

```python
def get_positive_numbers(numbers):
    positives = []

    for number in numbers:
        if number > 0:
            positives.append(number)

    return positives


result = get_positive_numbers([-2, 3, 5, -1])
print(result)
```

You should see:

```text
[3, 5]
```

When debugging return values, ask:

- Does the function have a `return` line?
- Is the returned value the value I actually need?
- Did I store or use the returned value?
- Did I call the function with parentheses?
- Is `return` indented in the right place?
- Is there code after `return` that I expected to run?

## Read the Docs

Python's official tutorial explains function definitions here:

```text
https://docs.python.org/3/tutorial/controlflow.html#defining-functions
```

Look for examples that use `return`.

Do not try to understand the whole page today.

Focus on these questions:

```text
Where is the function defined?
Where is return used?
What value comes back from the function?
Where does the returned value get used?
```

You may also see the word `None`.

For now, remember this:

```text
If a function finishes without returning a value, Python gives back None.
```

Code:

```python
def show_message():
    print("Practice return values.")


result = show_message()
print(result)
```

You should see:

```text
Practice return values.
None
```

The function printed a message, but it did not return a value.

That is why `result` is `None`.

## Mini Challenge

Create a file named:

```text
day-59/score_tools.py
```

Build a small score report using return values.

Your program should define these functions:

- `calculate_percentage(score, total_questions)`
- `build_result_message(name, percentage)`
- `passed_quiz(percentage)`

Rules:

```text
Each function should return a value.
Store at least one returned value in a variable.
Use at least one returned value in an if statement.
Print the final results outside the functions.
```

One possible solution:

```python
def calculate_percentage(score, total_questions):
    return int(score * 100 / total_questions)


def build_result_message(name, percentage):
    if percentage >= 80:
        return name + " had a strong result."

    return name + " is still practicing."


def passed_quiz(percentage):
    return percentage >= 60


student_name = "Asha"
score = 4
total_questions = 5

percentage = calculate_percentage(score, total_questions)
message = build_result_message(student_name, percentage)

print("Percentage:", percentage)
print(message)

if passed_quiz(percentage):
    print("Passed")
else:
    print("Try again")
```

You should see:

```text
Percentage: 80
Asha had a strong result.
Passed
```

After it works, change only these values:

```python
student_name = "Ben"
score = 2
total_questions = 5
```

Run the program again.

You should see a different percentage and a different message.

That is the point of combining parameters and return values:

```text
Parameters send changing values into the function.
Return sends the result back out.
```

## Real-World Use

Return values are useful when a function prepares a result that other code needs.

A contact book might have a function that builds one contact line:

```python
def format_contact(contact):
    return contact["name"] + " - " + contact["phone"]


contact = {
    "name": "Mina",
    "phone": "555-0104",
}

contact_line = format_contact(contact)

print(contact_line)
print("Characters:", len(contact_line))
```

You should see:

```text
Mina - 555-0104
Characters: 15
```

The function does not print the contact directly.

It returns a formatted string.

That gives the rest of the program more choices.

The program can:

```text
print the string
count its characters
store it in a list
save it to a file later
combine it with another message
```

Here is another example from a shopping list:

```python
def count_items(items):
    return len(items)


shopping_list = ["rice", "beans", "apples"]
item_count = count_items(shopping_list)

print("You have", item_count, "items.")
```

You should see:

```text
You have 3 items.
```

The function returns a number.

The print line decides how to display that number.

That separation is useful:

```text
One function calculates.
Another part of the program decides what to say.
```

## Recap

`return` sends a value back from a function.

Parameters send values into a function:

```python
def add_numbers(first, second):
    return first + second
```

The returned value comes back to the function call:

```python
total = add_numbers(3, 4)
```

Then the rest of the program can use it:

```python
print(total)
print(total + 10)
```

You can return different kinds of values:

```text
number
string
boolean
list
dictionary
```

Today you practiced numbers, strings, booleans, and lists.

The key difference is:

```text
print displays a value.
return gives a value back.
```

Also remember:

```text
A function stops when it reaches return.
A function without a return value gives back None.
A returned value needs to be stored or used.
```

## Lesson Checklist

Before moving on, check that you can:

- explain what `return` does
- explain the difference between `print()` and `return`
- write a function that returns a number
- write a function that returns a string
- write a function that returns a boolean
- write a function that returns a list
- store a returned value in a variable
- use a returned value in another calculation
- use a returned value inside an `if` statement
- explain why code after `return` does not run
- explain why a function without `return` gives back `None`
- fix code that prints when it should return
- fix code that calls a function but ignores the result
- call a returning function with parentheses and arguments

## Exercises

### Exercise 1

Write a function named `add_numbers`.

It should have two parameters:

```text
first
second
```

It should return the sum.

Call it with `6` and `9`, store the result, and print it.

### Exercise 2

Write a function named `calculate_total`.

It should have two parameters:

```text
price
tax
```

It should return `price + tax`.

Store the returned value in a variable named `total`.

Then print:

```text
Total: 23
```

when the price is `20` and the tax is `3`.

### Exercise 3

Write a function named `make_greeting`.

It should have one parameter named `name`.

It should return a greeting string.

This code:

```python
message = make_greeting("Mina")
print(message)
```

should print:

```text
Hello, Mina!
```

### Exercise 4

Fix the broken code.

Broken code:

```python
def triple(number):
    number * 3


answer = triple(4)
print(answer)
```

The goal is:

```text
12
```

### Exercise 5

Fix the broken code.

Broken code:

```python
def double(number):
    print(number * 2)


answer = double(5)
print(answer + 1)
```

The goal is:

```text
11
```

### Exercise 6

Write a function named `is_even`.

It should return `True` if a number is even and `False` otherwise.

Hint:

```python
number % 2 == 0
```

Call it with at least two numbers.

Use one returned value in an `if` statement.

### Exercise 7

Write a function named `is_passing`.

It should return whether a score is at least `60`.

Use it like this:

```python
if is_passing(72):
    print("Passed")
else:
    print("Keep practicing")
```

### Exercise 8

Write a function named `get_first_two_items`.

It should have one parameter named `items`.

It should return the first two items from the list.

Try it with:

```python
tasks = ["read", "practice", "review"]
```

### Exercise 9

Fix the broken code.

Broken code:

```python
def build_message(name):
    return "Hello, "
    return name


message = build_message("Sam")
print(message)
```

The goal is:

```text
Hello, Sam
```

### Exercise 10

Fix the broken code.

Broken code:

```python
def add_shipping(total):
    return total + 5


final_total = add_shipping
print(final_total)
```

The goal is to call the function with `20` and print:

```text
25
```

### Exercise 11

Write a function named `format_contact`.

It should receive a contact dictionary like this:

```python
contact = {
    "name": "Asha",
    "phone": "555-0188",
}
```

It should return:

```text
Asha - 555-0188
```

Store the returned value in a variable and print it.

### Exercise 12

Write a function named `get_completed_tasks`.

It should receive a list of task dictionaries.

Each task should have:

```text
title
done
```

The function should return a list of titles where `done` is `True`.

### Exercise 13

Choose the better tool for each job: `print()` or `return`.

```text
Show a menu on the screen.
Calculate a quiz percentage.
Build a greeting message to use later.
Display a goodbye message.
Check whether a score is passing.
Create a list of unfinished tasks.
```

Write one sentence for each choice.

### Exercise 14

Look at one old program from this course.

Find one place where the code calculates or builds a value.

Write a function that returns that value instead of printing it immediately.

You do not need to refactor the whole old file.

Just write the new function and one example call.

### Exercise 15

Write a small program with three functions:

```text
calculate_subtotal
calculate_tax
calculate_final_total
```

Each function should return a number.

Use the returned values to print a small receipt:

```text
Subtotal: 30
Tax: 3
Final total: 33
```

## Tiny Win

You can now write a function that gives an answer back.

That makes functions much more useful.

Before today, your functions mostly displayed things.

Now your functions can calculate, decide, build, filter, and hand the result to the next part of the program.

The tiny win is:

```text
You can decide whether a function should show the answer or return the answer.
```

That decision is a big part of writing clear programs.

## Tomorrow

Tomorrow is:

```text
Day 60: Default Parameters
```

So far, when a function has a parameter, each normal call needs an argument.

Example:

```python
def make_greeting(name):
    return "Hello, " + name + "!"


print(make_greeting("Mina"))
```

You should see:

```text
Hello, Mina!
```

Tomorrow, you will learn how to give a parameter a fallback value.

That will let a function work even when the caller does not provide every argument.

The new idea will look like this:

```python
def make_greeting(name, greeting="Hello"):
    return greeting + ", " + name + "!"
```

For now, keep today's idea clear:

```text
Parameters bring values in.
Return values send results out.
```
