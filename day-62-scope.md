# Day 62: Scope

**Focus:** Understanding where a variable can be used  
**You will practice:** local variables, outside variables, parameters as local names, `NameError`, clearer data flow, and passing values into functions  
**Estimated time:** 45-60 minutes

## Today's Goal

Today you will learn about scope.

Scope means:

```text
where a name is available in your program
```

In Python, a variable is not automatically available everywhere.

Some names belong to the whole file.
Some names belong only inside one function.
Some names are created when a function receives arguments.

By the end of this lesson, you should be able to:

- explain scope in plain English
- identify a local variable inside a function
- explain why a local variable cannot be used outside its function
- treat parameters as local names inside a function
- recognize a `NameError` caused by scope
- explain why changing a name inside a function does not automatically change the outside name
- avoid confusing shadowed names
- pass values into functions instead of relying on outside variables
- prepare for Day 63, where you will write cleaner pure functions

The main idea:

```text
A variable can only be used where Python can see that name.
```

Scope is one of those ideas that feels small at first.

Then it starts explaining many confusing function bugs.

## The Big Idea

A variable created inside a function belongs to that function.

Code:

```python
def show_message():
    message = "Practice scope"
    print(message)


show_message()
```

You should see:

```text
Practice scope
```

The variable `message` is created inside `show_message()`.

That means `message` is a local variable.

Local means:

```text
available inside this function
```

Now look at what happens if outside code tries to use that local variable.

Broken code:

```python
def show_message():
    message = "Practice scope"
    print(message)


show_message()
print(message)
```

The first `print(message)` works because it is inside the function.

The second `print(message)` is outside the function.

Python raises a `NameError` because the outside part of the program does not have a variable named `message`.

Python may show:

```text
NameError: name 'message' is not defined
```

This does not mean the function failed.

It means `message` was only available in the function's scope.

If the outside code needs the value, the function should give the value back.

Fixed code:

```python
def build_message():
    message = "Practice scope"
    return message


result = build_message()
print(result)
```

You should see:

```text
Practice scope
```

This is a clearer flow:

```text
The function creates the message.
The function returns the message.
The outside code stores the returned value.
The outside code prints its own variable.
```

The function's local variable stays local.

The outside code gets a value it can use.

## The Mental Model

Think of a function as a small workroom.

Names created inside the workroom stay in the workroom.

Example:

```python
def make_label():
    label = "Item: notebook"
    print(label)


make_label()
```

You should see:

```text
Item: notebook
```

The name `label` is on the function's worktable.

When the function finishes, that local worktable is cleared away.

Outside code cannot reach back into the function and grab `label`.

Parameters work the same way.

Code:

```python
def greet_person(name):
    print("Hello, " + name + "!")


greet_person("Mina")
```

You should see:

```text
Hello, Mina!
```

The parameter `name` is also local to the function.

During this call:

```text
name receives "Mina"
```

Inside the function, `name` can be used like a normal variable.

Outside the function, `name` does not exist unless you created a separate outside variable with that name.

Broken code:

```python
def greet_person(name):
    print("Hello, " + name + "!")


greet_person("Mina")
print(name)
```

This is broken because `name` is a parameter.

It belongs to the function call.

The outside `print(name)` raises a `NameError`.

Fixed code:

```python
def greet_person(name):
    print("Hello, " + name + "!")


student_name = "Mina"
greet_person(student_name)
print(student_name)
```

You should see:

```text
Hello, Mina!
Mina
```

Now the outside code has its own variable:

```text
student_name
```

The function has its own local parameter:

```text
name
```

The value moves into the function through the argument.

That is the habit you want:

```text
Pass values in.
Use local names inside.
Return values out when needed.
```

## Try It Yourself

Create a file named:

```text
day-62/scope_practice.py
```

Work through these examples one at a time.

### Step 1: A Local Variable

Code:

```python
def show_status():
    status = "ready"
    print("Inside function:", status)


show_status()
```

You should see:

```text
Inside function: ready
```

The variable `status` is local because it is created inside the function.

### Step 2: A Local Variable Outside The Function

Broken code:

```python
def show_status():
    status = "ready"
    print("Inside function:", status)


show_status()
print("Outside function:", status)
```

This is broken because the outside code tries to use `status`.

The name `status` only exists inside `show_status()`.

One fix is to return the value.

Fixed code:

```python
def get_status():
    status = "ready"
    return status


current_status = get_status()
print("Outside function:", current_status)
```

You should see:

```text
Outside function: ready
```

Now the outside code uses `current_status`, a variable it owns.

### Step 3: Parameters Are Local Names

Code:

```python
def print_score(player, score):
    print(player + " scored " + str(score) + " points.")


print_score("Asha", 15)
```

You should see:

```text
Asha scored 15 points.
```

Inside the function:

```text
player receives "Asha"
score receives 15
```

The names `player` and `score` are local to the function.

Broken code:

```python
def print_score(player, score):
    print(player + " scored " + str(score) + " points.")


print_score("Asha", 15)
print(player)
```

The final line is broken because `player` is a parameter.

It is not available outside the function.

### Step 4: Outside Variables Can Be Read, But Be Careful

Python can sometimes read a variable from outside a function.

Code:

```python
app_name = "Notes App"


def show_title():
    print(app_name)


show_title()
```

You should see:

```text
Notes App
```

This works because `app_name` exists outside the function before the function is called.

For a simple constant-like value, this may be fine.

But relying on outside variables too often can make code harder to understand.

This function looks like it needs no information:

```python
def show_title():
    print(app_name)
```

But it secretly depends on `app_name` existing somewhere else.

A clearer version passes the value in.

Code:

```python
def show_title(app_name):
    print(app_name)


show_title("Notes App")
```

You should see:

```text
Notes App
```

Now the data flow is visible:

```text
show_title receives the app name
show_title prints the app name
```

### Step 5: Changing A Local Name Does Not Change The Outside Name

This mistake is common.

Code:

```python
status = "open"


def close_task():
    status = "closed"
    print("Inside function:", status)


close_task()
print("Outside function:", status)
```

You should see:

```text
Inside function: closed
Outside function: open
```

The function created its own local variable named `status`.

It did not change the outside `status`.

Those are two separate names in two separate scopes.

If you want the outside value to change, return the new value and assign it outside.

Fixed code:

```python
def close_task(current_status):
    if current_status == "open":
        return "closed"

    return current_status


task_status = "open"
task_status = close_task(task_status)
print(task_status)
```

You should see:

```text
closed
```

This makes the change easy to follow:

```text
task_status starts as "open"
task_status is passed into close_task
close_task returns "closed"
task_status receives the returned value
```

### Step 6: Avoid Shadowing When It Confuses The Reader

Shadowing means using the same name in an inner scope and an outer scope.

Code:

```python
student = "Mina"


def show_student(student):
    print("Inside function:", student)


show_student("Sam")
print("Outside function:", student)
```

You should see:

```text
Inside function: Sam
Outside function: Mina
```

This code works, but it can be confusing.

There are two different names both called `student`:

```text
outside student = "Mina"
local parameter student = "Sam"
```

A clearer version uses names that show the flow.

Code:

```python
current_student = "Mina"


def show_student(student_name):
    print("Inside function:", student_name)


show_student("Sam")
print("Outside function:", current_student)
```

You should see:

```text
Inside function: Sam
Outside function: Mina
```

The output is the same, but the names are easier to track.

Clear names reduce scope mistakes.

## Common Mistake

Scope bugs usually come from one of four habits.

### Mistake 1: Using A Function Variable Outside

Broken code:

```python
def build_greeting(name):
    greeting = "Hello, " + name + "!"


build_greeting("Mina")
print(greeting)
```

This is broken because `greeting` is local to `build_greeting()`.

The outside code cannot use it.

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

If outside code needs a value from a function, return it.

### Mistake 2: Changing A Name Inside And Expecting Outside To Change

Code:

```python
score = 0


def add_point():
    score = 1
    print("Inside function:", score)


add_point()
print("Outside function:", score)
```

You should see:

```text
Inside function: 1
Outside function: 0
```

This code runs, but it probably does not do what the beginner expected.

The assignment inside the function creates a local `score`.

It does not update the outside `score`.

Fixed code:

```python
def add_point(current_score):
    return current_score + 1


score = 0
score = add_point(score)
print(score)
```

You should see:

```text
1
```

The function receives a value and returns a new value.

That is easier to understand than trying to reach into the outside scope.

### Mistake 3: Shadowing A Name Without Meaning To

Code:

```python
name = "Mina"


def greet(name):
    print("Hello, " + name + "!")


greet("Sam")
print(name)
```

You should see:

```text
Hello, Sam!
Mina
```

This is not an error.

But it can surprise you if you expected the outside `name` to become `"Sam"`.

The parameter `name` is local to the function.

The outside `name` is separate.

Clearer code:

```python
saved_name = "Mina"


def greet(person_name):
    print("Hello, " + person_name + "!")


greet("Sam")
print(saved_name)
```

You should see:

```text
Hello, Sam!
Mina
```

Different names can make different scopes easier to see.

### Mistake 4: Hiding Data Flow

Code:

```python
tax_rate = 0.08


def show_total(price):
    total = price + (price * tax_rate)
    print("Total:", total)


show_total(20)
```

You should see:

```text
Total: 21.6
```

This code runs.

The hidden problem is that `show_total()` depends on `tax_rate` from outside the function.

That dependency is easy to miss.

Clearer code:

```python
def show_total(price, tax_rate):
    total = price + (price * tax_rate)
    print("Total:", total)


show_total(20, 0.08)
```

You should see:

```text
Total: 21.6
```

Now the function call shows both pieces of information:

```text
price
tax rate
```

Python has advanced tools for changing outside variables from inside functions.

For now, avoid that shortcut.

Pass values in and return values out.

That habit will make tomorrow's lesson much easier.

## Debug It

When a function has a scope bug, ask:

```text
Where was this name created?
Am I using it inside or outside that scope?
Is this name a parameter?
Did I mean to return a value?
Did I accidentally use the same name in two places?
```

### Debug 1: Local Variable Outside

Goal:

```text
Print the label outside the function.
```

Broken code:

```python
def make_label(item):
    label = "Item: " + item


make_label("notebook")
print(label)
```

The problem:

```text
label is local to make_label.
The outside print cannot see it.
```

Fixed code:

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

### Debug 2: Parameter Outside

Goal:

```text
Print the score message, then print the original player name.
```

Broken code:

```python
def show_score(player, score):
    print(player + ": " + str(score))


show_score("Asha", 15)
print(player)
```

The problem:

```text
player is a parameter.
It only exists inside show_score.
```

Fixed code:

```python
def show_score(player, score):
    print(player + ": " + str(score))


player_name = "Asha"
show_score(player_name, 15)
print(player_name)
```

You should see:

```text
Asha: 15
Asha
```

### Debug 3: The Outside Value Does Not Change

Goal:

```text
Change the task status from open to closed.
```

Broken code:

```python
task_status = "open"


def close_task():
    task_status = "closed"


close_task()
print(task_status)
```

You should see:

```text
open
```

The code runs, but the result is wrong for the goal.

The problem:

```text
task_status inside the function is local.
It does not update the outside task_status.
```

Fixed code:

```python
def close_task(status):
    return "closed"


task_status = "open"
task_status = close_task(task_status)
print(task_status)
```

You should see:

```text
closed
```

### Debug 4: Hidden Outside Dependency

Goal:

```text
Calculate a discounted price from the values given to the function.
```

Code:

```python
discount = 5


def show_discounted_price(price):
    print("Discounted price:", price - discount)


show_discounted_price(20)
```

You should see:

```text
Discounted price: 15
```

This code runs, but the function depends on `discount` from outside.

That makes the function less clear.

Better code:

```python
def show_discounted_price(price, discount):
    print("Discounted price:", price - discount)


show_discounted_price(20, 5)
```

You should see:

```text
Discounted price: 15
```

The function now receives everything it needs.

## Read the Docs

Python's official tutorial explains function definitions here:

```text
https://docs.python.org/3/tutorial/controlflow.html#defining-functions
```

You do not need to understand every sentence today.

Look for the part that talks about local variables or a local symbol table.

That wording is more formal than this lesson, but the idea is the same:

```text
Functions have their own local names.
```

When you read a function in the docs or in someone else's code, ask:

```text
What are the parameters?
What local variables are created inside?
What values are passed in?
What values are returned?
Does the function rely on names from outside?
```

That is enough for now.

You are learning how to read function boundaries.

## Mini Challenge

Create a file named:

```text
day-62/scope_challenge.py
```

Build a small task progress program.

Rules:

```text
Start with completed_tasks = 2.
Start with total_tasks = 5.
Write a function named add_completed_task.
Write a function named show_progress.
Do not use completed_tasks directly inside either function.
Pass values into the functions.
Return the updated completed count from add_completed_task.
```

One possible solution:

```python
def add_completed_task(completed):
    return completed + 1


def show_progress(completed, total):
    remaining = total - completed
    print("Completed:", completed)
    print("Remaining:", remaining)


completed_tasks = 2
total_tasks = 5

completed_tasks = add_completed_task(completed_tasks)
show_progress(completed_tasks, total_tasks)
```

You should see:

```text
Completed: 3
Remaining: 2
```

Notice the scope of each name:

```text
completed_tasks belongs to the outside program.
total_tasks belongs to the outside program.
completed is local to each function that uses it.
total is local to show_progress.
remaining is local to show_progress.
```

The function `show_progress()` can do its job because it receives the values it needs.

It does not have to search the rest of the file for outside variables.

## Real-World Use

Scope matters in real programs because functions often live far away from the code that calls them.

In a small contact book, you might have:

```python
def print_contact(contact):
    print("Name:", contact["name"])
    print("Phone:", contact["phone"])


selected_contact = {
    "name": "Mina",
    "phone": "555-0104"
}

print_contact(selected_contact)
```

You should see:

```text
Name: Mina
Phone: 555-0104
```

This is clear because `print_contact()` receives the contact it needs.

A less clear version would make the function rely on an outside variable:

```python
contact = {
    "name": "Mina",
    "phone": "555-0104"
}


def print_contact():
    print("Name:", contact["name"])
    print("Phone:", contact["phone"])


print_contact()
```

You should see:

```text
Name: Mina
Phone: 555-0104
```

This runs, but the function secretly depends on a variable named `contact`.

If the program grows, that can become hard to track.

Passing the contact in is better:

```text
print_contact(selected_contact)
```

The call shows the data flow.

This matters in quiz programs, shopping lists, contact books, report builders, and games.

Functions are easier to reuse when they do not depend on random names outside themselves.

That idea leads directly into tomorrow:

```text
A pure function uses its inputs to produce an output, without relying on hidden outside state.
```

You do not need to master that sentence today.

Just keep the habit:

```text
Give the function what it needs.
Let the function return what the rest of the program needs.
```

## Recap

Scope means where a name is available.

A variable created inside a function is local to that function.

A parameter is also local to the function.

Outside code cannot use a local variable from inside a function.

If outside code tries, Python raises a `NameError`.

An outside variable can sometimes be read inside a function, but relying on that too much makes data flow harder to see.

Changing a name inside a function does not automatically change the outside name.

Using the same name inside and outside a function is called shadowing. It is allowed, but it can confuse beginners.

The safest beginner habit is:

```text
Pass values into functions.
Use local names inside functions.
Return values that outside code needs.
Assign returned values outside the function.
```

This habit keeps functions easier to read, test, reuse, and debug.

## Lesson Checklist

Before moving on, check that you can:

- explain scope as where a name can be used
- identify a local variable inside a function
- explain why a function variable cannot be used outside the function
- explain why parameters are local names
- recognize a `NameError` caused by scope
- explain why changing a local name does not change an outside name
- spot shadowing when the same name appears inside and outside a function
- pass an outside value into a function as an argument
- return a value from a function when outside code needs it
- describe why hidden outside variables can make functions harder to understand

## Exercises

### Exercise 1

In your own words, answer:

```text
What does scope mean?
```

Use one sentence.

### Exercise 2

Read this code:

```python
def print_city():
    city = "Pune"
    print(city)


print_city()
```

Which name is local to the function?

### Exercise 3

What happens if you add this line to the end of Exercise 2?

```python
print(city)
```

Explain why.

### Exercise 4

Fix the code by returning the local value.

Broken code:

```python
def build_title():
    title = "Daily Report"


build_title()
print(title)
```

### Exercise 5

Read this code:

```python
def greet(name):
    print("Hello, " + name + "!")


greet("Mina")
```

Is `name` available outside the function?

Why or why not?

### Exercise 6

Write a function named `make_label`.

It should receive one parameter named `item`.

It should return text like:

```text
Item: notebook
```

Store the returned value in a variable outside the function and print it.

### Exercise 7

Fix the data flow.

Code:

```python
tax_rate = 0.08


def calculate_total(price):
    return price + (price * tax_rate)


print(calculate_total(20))
```

Rewrite the function so `tax_rate` is passed in as a parameter.

### Exercise 8

Read this code:

```python
score = 10


def show_score(score):
    print("Inside:", score)


show_score(25)
print("Outside:", score)
```

What prints?

Why are the two `score` names different?

### Exercise 9

Rewrite Exercise 8 with clearer names.

Use:

```text
saved_score
current_score
```

### Exercise 10

Fix the logic bug.

Code:

```python
task_status = "open"


def close_task():
    task_status = "closed"


close_task()
print(task_status)
```

The goal is to print:

```text
closed
```

Use a return value.

### Exercise 11

Write a function named `add_point`.

It should receive the current score and return the score plus one.

Use it like this:

```text
score starts at 0
call add_point
store the returned value back in score
print score
```

### Exercise 12

Choose one old function you wrote earlier in the course.

For each name in the function, label it:

```text
parameter
local variable
outside variable
```

If the function relies on an outside variable, rewrite it so the value is passed in.

### Exercise 13

Write a function named `show_contact`.

It should receive a contact dictionary and print the contact's name and phone number.

Create the contact outside the function.

Pass it into the function.

### Exercise 14

Read this code:

```python
discount = 5


def get_discounted_price(price):
    return price - discount
```

Why might this be harder to reuse than a function that receives both `price` and `discount`?

Rewrite the function with two parameters.

### Exercise 15

Write a short answer:

```text
Why is passing values into functions usually clearer than making functions rely on outside variables?
```

Use an example from a score program, contact book, shopping list, or task tracker.

## Tiny Win

You can now look at a variable and ask:

```text
Where does this name live?
```

That question explains many function bugs.

It also helps you write cleaner code.

When a function receives the values it needs and returns the value it creates, the program becomes easier to follow.

## Tomorrow

Tomorrow is:

```text
Day 63: Pure Functions
```

Today you learned that hidden outside variables can make functions harder to understand.

Tomorrow you will turn that idea into a stronger habit.

A pure function is easier to reason about because it works from its inputs and returns an output.

You have already practiced the main shape:

```python
def add_point(current_score):
    return current_score + 1


score = 0
score = add_point(score)
```

That is a good bridge from scope to pure functions:

```text
clear input
local work
clear output
```
