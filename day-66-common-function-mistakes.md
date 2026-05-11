# Day 66: Common Function Mistakes

**Focus:** Finding and fixing beginner function mistakes  
**You will practice:** calling functions, reading function order, checking parentheses and colons, fixing indentation, matching arguments, separating `print()` from `return`, spotting unreachable code, and thinking about scope  
**Estimated time:** 45-60 minutes

## Today's Goal

Today you will practice the function mistakes that beginners meet again and again.

You already know the main pieces:

- defining a function with `def`
- calling a function with parentheses
- passing arguments into parameters
- returning values
- keeping track of scope
- splitting programs into smaller jobs

Now the goal is to slow down and debug the small mistakes that can make function code feel mysterious.

By the end of this lesson, you should be able to:

- explain why a function does nothing until it is called
- call a function with parentheses
- place function definitions before the calls that need them
- fix missing colons and indentation errors
- match the number of arguments to the number of required parameters
- decide when to print and when to return
- notice code that cannot run after `return`
- find scope mistakes caused by using names in the wrong place
- read function error messages with less panic
- prepare for Day 67 practice

The main idea:

```text
Most function bugs come from confusing definition, call, input, output, or scope.
```

When you can name which part is wrong, the fix usually becomes smaller.

## The Big Idea

Functions add a new shape to your code.

That shape is useful, but it also creates a few new places where mistakes can hide.

Here is a simple function that works:

```python
def greet_user(name):
    return "Hello, " + name + "!"


message = greet_user("Mina")
print(message)
```

You should see:

```text
Hello, Mina!
```

This tiny program has several important parts:

```text
def greet_user(name):
```

This defines the function and says it needs one value.

```text
    return "Hello, " + name + "!"
```

This is the function body. It is indented.

```text
message = greet_user("Mina")
```

This calls the function and stores the returned value.

```text
print(message)
```

This displays the result.

If one part is missing or in the wrong place, the program can fail.

For example:

- define the function but never call it, and nothing appears
- call it without parentheses, and it does not run
- forget the colon, and Python cannot understand the definition
- indent the body incorrectly, and Python does not know what belongs to the function
- pass the wrong number of arguments, and Python refuses the call
- print when you meant to return, and the rest of the program receives `None`
- use a local variable outside the function, and Python raises a `NameError`

These mistakes are normal.

The point of today is not to avoid mistakes forever.

The point is to recognize them faster.

## The Mental Model

Think of a function as a small machine with three parts:

```text
definition
call
result
```

The definition builds the machine:

```python
def add_points(score, points):
    return score + points
```

The call runs the machine:

```python
new_score = add_points(10, 5)
```

The result is what comes back:

```python
print(new_score)
```

Full code:

```python
def add_points(score, points):
    return score + points


new_score = add_points(10, 5)
print(new_score)
```

You should see:

```text
15
```

When a function breaks, ask which part is wrong:

```text
Was the function defined?
Was it called?
Did the call use parentheses?
Did the call send the right values?
Did the function return a value?
Is the name being used in the right scope?
```

That checklist is better than staring at the whole file at once.

Start with the call.

Then check the function definition.

Then check what value comes back.

## Try It Yourself

Create a file named:

```text
day-66/function_mistakes.py
```

You will make a few small functions and practice checking each part.

### Step 1: Define And Call

Code:

```python
def show_header():
    print("Function Practice")
    print("-----------------")


show_header()
```

You should see:

```text
Function Practice
-----------------
```

The function definition stores the steps.

The function call runs the steps.

If you remove this line:

```python
show_header()
```

the program will not print the header.

That does not mean the function was written badly.

It means the function was never called.

### Step 2: Use Parentheses

Code:

```python
def show_status():
    print("Status: ready")


show_status()
```

You should see:

```text
Status: ready
```

The parentheses are what make the call happen.

This line names the function but does not run it:

```python
show_status
```

This line runs it:

```python
show_status()
```

When nothing prints, check for missing parentheses.

### Step 3: Match Arguments To Parameters

Code:

```python
def print_score(player, score):
    print(player + " scored " + str(score) + " points.")


print_score("Asha", 18)
```

You should see:

```text
Asha scored 18 points.
```

The function has two parameters:

```text
player
score
```

The call gives two arguments:

```text
"Asha"
18
```

The count matches.

The order also matters when you use positional arguments.

### Step 4: Return When The Program Needs A Value

Code:

```python
def calculate_total(price, shipping):
    return price + shipping


total = calculate_total(20, 5)
print("Total:", total)
print("With discount:", total - 3)
```

You should see:

```text
Total: 25
With discount: 22
```

The function returns the number.

That means the rest of the program can store it, print it, or use it in another calculation.

If the function only printed the number, `total` would not receive the value.

### Step 5: Keep Scope Clear

Code:

```python
def make_label(item):
    label = "Item: " + item
    return label


item_label = make_label("notebook")
print(item_label)
```

You should see:

```text
Item: notebook
```

The variable `label` belongs inside the function.

The outside code uses its own variable:

```text
item_label
```

That keeps the data flow clear:

```text
item goes in
label is built inside
result comes back
item_label stores it outside
```

## Common Mistake

This section gathers the function mistakes worth recognizing quickly.

### Mistake 1: Defining But Not Calling

Code:

```python
def print_menu():
    print("1. Add task")
    print("2. View tasks")
    print("3. Quit")
```

This code is valid.

But as a complete program, it does not display the menu.

The function has been defined, but it has not been called.

Fixed code:

```python
def print_menu():
    print("1. Add task")
    print("2. View tasks")
    print("3. Quit")


print_menu()
```

You should see:

```text
1. Add task
2. View tasks
3. Quit
```

Remember:

```text
def stores the steps.
The call runs the steps.
```

### Mistake 2: Calling Before Defining In A Confusing Layout

Broken code:

```python
show_menu()


def show_menu():
    print("Menu")
    print("1. Start")
    print("2. Quit")
```

This is broken because Python reads the file from top to bottom.

When it reaches `show_menu()`, it has not seen the function definition yet.

Fixed code:

```python
def show_menu():
    print("Menu")
    print("1. Start")
    print("2. Quit")


show_menu()
```

You should see:

```text
Menu
1. Start
2. Quit
```

A common beginner habit is:

```text
Put your function definitions near the top.
Put the main calls near the bottom.
```

That makes the file easier to follow.

### Mistake 3: Missing Parentheses

Code:

```python
def say_done():
    print("Done")


say_done
```

This code runs, but it does not print `Done`.

The final line refers to the function object.

It does not call the function.

Fixed code:

```python
def say_done():
    print("Done")


say_done()
```

You should see:

```text
Done
```

If a function has no parameters, the call still needs empty parentheses.

### Mistake 4: Missing Colon

Broken code:

```python
def print_divider()
    print("--------------------")


print_divider()
```

The first line needs a colon.

Python may show:

```text
SyntaxError: expected ':'
```

Fixed code:

```python
def print_divider():
    print("--------------------")


print_divider()
```

You should see:

```text
--------------------
```

The colon tells Python that an indented block is about to begin.

### Mistake 5: Bad Indentation

Broken code:

```python
def greet_user():
print("Hello")
print("Welcome back")


greet_user()
```

The lines inside the function must be indented.

Python may show:

```text
IndentationError: expected an indented block
```

Fixed code:

```python
def greet_user():
    print("Hello")
    print("Welcome back")


greet_user()
```

You should see:

```text
Hello
Welcome back
```

Indentation is not decoration in Python.

It decides what belongs inside the function.

### Mistake 6: Wrong Number Of Arguments

Broken code:

```python
def print_contact(name, phone):
    print("Name:", name)
    print("Phone:", phone)


print_contact("Mina")
```

The function expects two arguments.

The call gives one.

Python may show:

```text
TypeError: print_contact() missing 1 required positional argument: 'phone'
```

Fixed code:

```python
def print_contact(name, phone):
    print("Name:", name)
    print("Phone:", phone)


print_contact("Mina", "555-0104")
```

You should see:

```text
Name: Mina
Phone: 555-0104
```

When you see this kind of error, compare the definition and the call:

```text
How many required parameters are in the definition?
How many arguments are in the call?
```

### Mistake 7: Mixing `print()` And `return`

Broken code:

```python
def calculate_total(price, shipping):
    total = price + shipping
    print(total)


order_total = calculate_total(20, 5)
print("With discount:", order_total - 3)
```

This is broken because `calculate_total()` prints `25`, but it does not return `25`.

So `order_total` receives `None`.

Then Python cannot subtract `3` from `None`.

Fixed code:

```python
def calculate_total(price, shipping):
    total = price + shipping
    return total


order_total = calculate_total(20, 5)
print("With discount:", order_total - 3)
```

You should see:

```text
With discount: 22
```

Use `print()` when the job is to show something on the screen.

Use `return` when the rest of the program needs the value.

### Mistake 8: Code After `return`

Code:

```python
def choose_message(score):
    if score >= 80:
        return "Strong result"
        print("This line will not run")

    return "Keep practicing"


message = choose_message(90)
print(message)
```

You should see:

```text
Strong result
```

The `print()` line after `return "Strong result"` never runs.

As soon as Python reaches `return`, it leaves the function.

Fixed code:

```python
def choose_message(score):
    if score >= 80:
        print("Checking high score")
        return "Strong result"

    return "Keep practicing"


message = choose_message(90)
print(message)
```

You should see:

```text
Checking high score
Strong result
```

If a line needs to run, put it before `return`.

### Mistake 9: Scope Confusion

Broken code:

```python
def build_greeting(name):
    greeting = "Hello, " + name + "!"


build_greeting("Mina")
print(greeting)
```

This is broken because `greeting` is created inside the function.

The outside code cannot use that local variable.

Fixed code:

```python
def build_greeting(name):
    greeting = "Hello, " + name + "!"
    return greeting


message = build_greeting("Mina")
print(message)
```

You should see:

```text
Hello, Mina!
```

If outside code needs a value from inside a function, return the value.

### Mistake 10: Mutable Default Values

You do not need to master this yet.

Just be careful with defaults that are lists or dictionaries.

This code can surprise beginners:

```python
def add_item(item, items=[]):
    items.append(item)
    return items


print(add_item("rice"))
print(add_item("tea"))
```

You should see:

```text
['rice']
['rice', 'tea']
```

The list is reused between calls.

For now, a safer beginner pattern is:

```python
def add_item(item, items=None):
    if items is None:
        items = []

    items.append(item)
    return items


print(add_item("rice"))
print(add_item("tea"))
```

You should see:

```text
['rice']
['tea']
```

You will see this topic again later.

For now, remember:

```text
Use simple default values first.
Be careful with lists and dictionaries as defaults.
```

## Debug It

Read each broken example.

Find the mistake before looking at the fix.

### Debug 1

Goal:

```text
Task List
```

Broken code:

```python
def show_title():
    print("Task List")
```

The problem:

```text
The function is defined, but it is never called.
```

Fixed code:

```python
def show_title():
    print("Task List")


show_title()
```

You should see:

```text
Task List
```

### Debug 2

Goal:

```text
Saved
```

Broken code:

```python
def show_saved():
    print("Saved")


show_saved
```

The problem:

```text
The function call is missing parentheses.
```

Fixed code:

```python
def show_saved():
    print("Saved")


show_saved()
```

You should see:

```text
Saved
```

### Debug 3

Goal:

```text
Mina: 12
```

Broken code:

```python
def show_score(player, score):
    print(player + ": " + str(score))


show_score("Mina")
```

The problem:

```text
The function needs two arguments.
The call gives one.
```

Fixed code:

```python
def show_score(player, score):
    print(player + ": " + str(score))


show_score("Mina", 12)
```

You should see:

```text
Mina: 12
```

### Debug 4

Goal:

```text
Final total: 28
```

Broken code:

```python
def add_tax(total):
    print(total + 3)


final_total = add_tax(25)
print("Final total:", final_total)
```

The problem:

```text
add_tax prints the answer, but it does not return it.
final_total receives None.
```

Fixed code:

```python
def add_tax(total):
    return total + 3


final_total = add_tax(25)
print("Final total:", final_total)
```

You should see:

```text
Final total: 28
```

### Debug 5

Goal:

```text
Hello, Sam!
```

Broken code:

```python
def make_greeting(name):
    message = "Hello, " + name + "!"


make_greeting("Sam")
print(message)
```

The problem:

```text
message is local to the function.
The outside code cannot use it.
```

Fixed code:

```python
def make_greeting(name):
    message = "Hello, " + name + "!"
    return message


message = make_greeting("Sam")
print(message)
```

You should see:

```text
Hello, Sam!
```

When debugging functions, use this order:

```text
Check the function definition.
Check the function call.
Check the arguments.
Check whether the function prints or returns.
Check where each variable was created.
```

## Read the Docs

Python's official tutorial has a section about defining functions:

```text
https://docs.python.org/3/tutorial/controlflow.html#defining-functions
```

You do not need to read the whole page today.

Look for these pieces:

```text
def
function name
parameters
function body
return
```

When the documentation feels dense, use today's debugging questions:

```text
Where is the function defined?
Where is it called?
What values are passed in?
What value is returned?
Which names are local to the function?
```

Also look at Python's built-in function documentation:

```text
https://docs.python.org/3/library/functions.html
```

Pick one function you already know, such as `len()` or `print()`.

Notice the parentheses.

Functions are called with parentheses whether Python wrote them or you wrote them.

## Mini Challenge

Create a file named:

```text
day-66/fix_function_bugs.py
```

Start with this broken program:

```python
def calculate_score(correct, total):
    percent = int(correct * 100 / total)


def choose_message(percent):
    if percent >= 80:
        return "Strong result"
        print("Great work")

    return "Keep practicing"


score = calculate_score(4, 5)
message = choose_message(score)
print("Score:", score)
print(message)
```

The program is supposed to print:

```text
Score: 80
Strong result
```

Fix it by answering these questions:

```text
Which function forgot to return a value?
Which line after return can never run?
Does the main code store and use the returned values?
```

One fixed version:

```python
def calculate_score(correct, total):
    percent = int(correct * 100 / total)
    return percent


def choose_message(percent):
    if percent >= 80:
        return "Strong result"

    return "Keep practicing"


score = calculate_score(4, 5)
message = choose_message(score)
print("Score:", score)
print(message)
```

You should see:

```text
Score: 80
Strong result
```

After it works, change the score:

```python
score = calculate_score(2, 5)
```

You should see:

```text
Score: 40
Keep practicing
```

## Real-World Use

Function mistakes show up in real projects because functions are the places where data moves around.

A contact book might have:

```python
def format_contact(contact):
    return contact["name"] + " - " + contact["phone"]


contact = {"name": "Mina", "phone": "555-0104"}
line = format_contact(contact)
print(line)
```

You should see:

```text
Mina - 555-0104
```

This works because:

```text
the function receives the contact
the function returns the formatted line
the outside code stores the result
the outside code prints it
```

If the function printed the line but did not return it, another part of the program could not reuse the line.

A quiz program might have:

```python
def is_passing(score):
    return score >= 60


quiz_score = 75

if is_passing(quiz_score):
    print("Passed")
else:
    print("Try again")
```

You should see:

```text
Passed
```

This works because the function returns a Boolean value.

The `if` statement uses that returned value.

The more your programs grow, the more important these questions become:

```text
What does this function need?
What does it give back?
Who uses the result?
Where does each name live?
```

Those questions prevent many function bugs before they happen.

## Recap

Today you practiced common function mistakes.

The main ones were:

- defining a function but not calling it
- calling a function before Python has seen the definition
- forgetting parentheses in a function call
- forgetting the colon after the `def` line
- indenting the function body incorrectly
- passing the wrong number of arguments
- printing when the program needs a returned value
- expecting code after `return` to run
- using a local variable outside its function
- using a list or dictionary as a default value without understanding the effect

The basic debugging questions are:

```text
Was the function defined before it was called?
Was the function actually called?
Did the call use parentheses?
Did the call send the right number of arguments?
Did the function return a value if the rest of the program needs one?
Is each variable being used in the scope where it exists?
```

Functions are powerful because they create clear boundaries.

Most function bugs happen when those boundaries are fuzzy.

## Lesson Checklist

Before moving on, check that you can:

- explain the difference between defining and calling a function
- fix a function that is defined but never called
- add missing parentheses to a function call
- place a function definition before the call that uses it
- add the missing colon after a `def` line
- indent a function body correctly
- match arguments to required parameters
- explain why `print()` is not the same as `return`
- fix a function that returns `None` by accident
- explain why code after `return` does not run
- return a local value so outside code can use it
- avoid relying on hidden outside variables when a parameter would be clearer
- be cautious with mutable default values

## Exercises

### Exercise 1

This code defines a function but does not call it.

Fix it.

```python
def say_hello():
    print("Hello")
```

### Exercise 2

This code does not print `Ready`.

Fix it.

```python
def show_ready():
    print("Ready")


show_ready
```

### Exercise 3

Fix the missing colon.

```python
def print_line()
    print("==========")


print_line()
```

### Exercise 4

Fix the indentation.

```python
def show_title():
print("Daily Notes")


show_title()
```

### Exercise 5

Fix the function call.

```python
def print_contact(name, phone):
    print("Name:", name)
    print("Phone:", phone)


print_contact("Asha")
```

The goal is:

```text
Name: Asha
Phone: 555-0188
```

### Exercise 6

Fix the function so `total` receives a number.

```python
def calculate_total(price, tax):
    print(price + tax)


total = calculate_total(20, 3)
print("Total:", total)
```

### Exercise 7

Move the useful line so it runs before `return`.

```python
def get_status(done):
    if done:
        return "done"
        print("Task is complete")

    return "open"
```

### Exercise 8

Fix the scope mistake.

```python
def make_label(item):
    label = "Item: " + item


make_label("rice")
print(label)
```

The goal is:

```text
Item: rice
```

### Exercise 9

Read this code:

```python
def add_point(score):
    score = score + 1
    return score


score = 0
add_point(score)
print(score)
```

It prints:

```text
0
```

Fix the outside code so it stores the returned value.

### Exercise 10

This code calls a function before defining it.

Rewrite the code in a clearer order.

```python
print_header()


def print_header():
    print("Report")
```

### Exercise 11

Choose `print()` or `return` for each job.

```text
Show a menu on the screen.
Calculate a final total for later use.
Build a greeting message that another line will print.
Display a goodbye message.
Check whether a score is passing.
```

Write one sentence for each choice.

### Exercise 12

Write a small program with three functions:

```text
calculate_percentage
choose_message
print_report
```

Rules:

```text
calculate_percentage should return a number.
choose_message should return text.
print_report should print the final report.
Call all three functions.
```

### Exercise 13

Find and fix both mistakes.

```python
def build_message(name)
    return "Hello, " + name + "!"


message = build_message
print(message)
```

### Exercise 14

Write your own broken function example.

Choose one mistake:

```text
missing call
missing parentheses
wrong number of arguments
missing return
scope confusion
```

Then write the fixed version below it.

### Exercise 15

Open one older function file from this course.

For three function calls, answer:

```text
What function is being called?
How many arguments are passed?
Does the function print, return, or both?
Where is the returned value used?
```

If one of those answers is unclear, rewrite the function or call to make it easier to read.

## Tiny Win

You can now debug function mistakes by category.

Instead of thinking:

```text
The whole function is broken.
```

you can ask:

```text
Is this a call problem?
Is this an argument problem?
Is this a return problem?
Is this a scope problem?
```

That makes debugging less vague.

A smaller question usually leads to a smaller fix.

## Tomorrow

Tomorrow is:

```text
Day 67: Practice Day: Function Debugging
```

Today you reviewed the mistakes.

Tomorrow you will practice them in longer exercises.

Expect to fix programs that combine:

```text
missing calls
wrong arguments
missing returns
unreachable code
scope mistakes
```

The goal will be to read a broken function program calmly, find one problem at a time, and keep the final code clear.
