# Day 60: Default Parameters

**Focus:** Giving function parameters backup values  
**You will practice:** calling functions with and without optional arguments, choosing useful defaults, placing default parameters correctly, and debugging default parameter mistakes  
**Estimated time:** 45-60 minutes

## Today's Goal

Today you will learn how to give a function parameter a default value.

You already know that parameters let a function receive information:

```python
def greet_person(name):
    print("Hello, " + name + "!")


greet_person("Mina")
```

You should see:

```text
Hello, Mina!
```

Sometimes a function has a value that is usually the same, but still needs to be changeable.

For example, most greetings might start with `"Hello"`.

But sometimes you may want `"Good morning"` or `"Welcome"`.

A default parameter lets you handle both cases.

By the end of this lesson, you should be able to:

- define a parameter with a default value
- call a function without passing the optional argument
- call the same function with a custom argument
- use defaults for greetings, messages, counts, and settings
- place default parameters after required parameters
- decide when a default makes sense
- avoid unclear defaults
- explain why a default is not the same as a return value
- prepare for keyword arguments tomorrow

The main idea:

```text
A default value is used when the caller does not provide an argument for that parameter.
```

## The Big Idea

Without a default, every parameter needs an argument.

Example:

```python
def greet_person(name, greeting):
    print(greeting + ", " + name + "!")


greet_person("Mina", "Hello")
greet_person("Sam", "Good morning")
```

You should see:

```text
Hello, Mina!
Good morning, Sam!
```

This works, but it can feel repetitive if most calls use the same greeting.

You can give `greeting` a default value:

```python
def greet_person(name, greeting="Hello"):
    print(greeting + ", " + name + "!")


greet_person("Mina")
greet_person("Sam", "Good morning")
```

You should see:

```text
Hello, Mina!
Good morning, Sam!
```

In this definition:

```python
def greet_person(name, greeting="Hello"):
```

`name` is required.

`greeting` has a default value.

Read it like this:

```text
To greet a person, I always need a name.
If no greeting is provided, use "Hello".
```

The first call:

```python
greet_person("Mina")
```

does not pass a greeting, so Python uses the default:

```text
greeting receives "Hello"
```

The second call:

```python
greet_person("Sam", "Good morning")
```

passes a custom greeting, so Python uses that instead:

```text
greeting receives "Good morning"
```

A default value is not permanent for every call.

It is only the backup value for calls that leave that argument out.

## The Mental Model

Think of a function definition as a small form.

Some blanks must be filled in every time:

```text
Name: required
```

Some blanks already have a sensible value:

```text
Greeting: Hello
```

If the caller leaves the greeting blank, the function uses `"Hello"`.

If the caller writes a different greeting, the function uses the custom value.

Code:

```python
def print_label(label, value="not set"):
    print(label + ": " + value)


print_label("Name", "Mina")
print_label("Status")
```

You should see:

```text
Name: Mina
Status: not set
```

The first call fills both blanks.

The second call fills only the required blank.

Python fills the optional blank with the default.

The order matters:

```python
def print_label(label, value="not set"):
```

Required parameters come first.

Default parameters come after them.

This is allowed:

```python
def show_task(task, status="not started"):
    print(task + " - " + status)
```

This is not allowed:

```python
def show_task(status="not started", task):
    print(task + " - " + status)
```

Python needs to know which arguments are required before it starts filling optional spaces.

Tomorrow, keyword arguments will give you another way to make function calls clearer.

For today, keep the simple rule:

```text
Required parameters first.
Default parameters after.
```

## Try It Yourself

Create a file named:

```text
day-60/default_parameters.py
```

Work through these examples one at a time.

### Step 1: A Greeting With A Default

Code:

```python
def greet_person(name, greeting="Hello"):
    print(greeting + ", " + name + "!")


greet_person("Mina")
greet_person("Sam", "Good morning")
greet_person("Iris")
```

You should see:

```text
Hello, Mina!
Good morning, Sam!
Hello, Iris!
```

The calls for Mina and Iris do not include a greeting.

Python uses `"Hello"`.

The call for Sam includes a greeting, so Python uses `"Good morning"`.

Try this:

```text
Change the default greeting to "Welcome".
Run the program again.
Add one call that uses "Good evening".
```

### Step 2: A Default Message

Defaults are useful when a message is usually the same.

Code:

```python
def send_update(name, message="Your account is ready."):
    print("To:", name)
    print("Message:", message)


send_update("Mina")
send_update("Sam", "Your password was changed.")
```

You should see:

```text
To: Mina
Message: Your account is ready.
To: Sam
Message: Your password was changed.
```

The default message handles the common case.

The custom message handles the special case.

### Step 3: A Default Count

A default can also be a number.

Code:

```python
def repeat_message(message, times=1):
    for count in range(times):
        print(message)


repeat_message("Practice functions")
repeat_message("Review defaults", 3)
```

You should see:

```text
Practice functions
Review defaults
Review defaults
Review defaults
```

The first call does not pass `times`, so the message prints once.

The second call passes `3`, so the message prints three times.

### Step 4: A Default Setting

Defaults often describe settings.

Code:

```python
def show_settings(theme="light", notifications=True):
    print("Theme:", theme)
    print("Notifications:", notifications)


show_settings()
show_settings("dark", False)
```

You should see:

```text
Theme: light
Notifications: True
Theme: dark
Notifications: False
```

This function has no required parameters.

Both settings have defaults.

That means this call is allowed:

```python
show_settings()
```

It uses both default values.

### Step 5: Required First, Defaults After

When a function has required values and default values, put the required values first.

Code:

```python
def display_score(player, score, label="points"):
    print(player + " scored " + str(score) + " " + label + ".")


display_score("Asha", 18)
display_score("Ben", 4, "stars")
```

You should see:

```text
Asha scored 18 points.
Ben scored 4 stars.
```

`player` and `score` are required.

`label` has a default.

The default makes sense because `"points"` is the common word.

### Step 6: Defaults And Return Values

Defaults work with functions that return values too.

Code:

```python
def add_tax(price, tax_rate=0.05):
    return price + price * tax_rate


standard_total = add_tax(100)
custom_total = add_tax(100, 0.08)

print(standard_total)
print(custom_total)
```

You should see:

```text
105.0
108.0
```

The default value helps the function receive a missing argument.

The `return` statement sends the result back.

Those are two different jobs.

## Common Mistake

Default parameters are small, but they introduce a few rules worth practicing.

### Mistake 1: Putting A Required Parameter After A Default

Broken code:

```python
def greet_person(greeting="Hello", name):
    print(greeting + ", " + name + "!")
```

This is broken because `greeting` has a default, but `name` is still required after it.

Python does not allow required parameters after default parameters.

Fixed code:

```python
def greet_person(name, greeting="Hello"):
    print(greeting + ", " + name + "!")


greet_person("Mina")
```

You should see:

```text
Hello, Mina!
```

Use this order:

```text
required parameters first
default parameters after
```

### Mistake 2: Using An Unclear Default

This code runs, but the default is hard to understand.

Broken code:

```python
def create_user(name, role="x"):
    print(name + " is a " + role + ".")


create_user("Mina")
```

You should see:

```text
Mina is a x.
```

The function works, but `"x"` does not tell the reader what the default means.

Fixed code:

```python
def create_user(name, role="member"):
    print(name + " is a " + role + ".")


create_user("Mina")
```

You should see:

```text
Mina is a member.
```

A good default should be clear, ordinary, and safe for the common case.

### Mistake 3: Expecting The Default To Change Automatically

This code runs, but the result may surprise you.

Broken code:

```python
default_greeting = "Hello"


def greet_person(name, greeting=default_greeting):
    print(greeting + ", " + name + "!")


default_greeting = "Welcome"

greet_person("Mina")
```

You should see:

```text
Hello, Mina!
```

The default was set when Python read the function definition.

Changing `default_greeting` later does not rewrite the function's default.

Fixed code:

```python
def greet_person(name, greeting="Hello"):
    print(greeting + ", " + name + "!")


greet_person("Mina")
greet_person("Sam", "Welcome")
```

You should see:

```text
Hello, Mina!
Welcome, Sam!
```

If you want a different greeting for one call, pass it as an argument.

### Mistake 4: Confusing A Default With A Return Value

A default value does not make a function send anything back.

Broken code:

```python
def add_tax(price, tax_rate=0.05):
    total = price + price * tax_rate


add_tax(100)
print(total)
```

This is broken because `total` was created inside the function.

The default `tax_rate` gives the function a backup input.

It does not return `total`.

Fixed code:

```python
def add_tax(price, tax_rate=0.05):
    return price + price * tax_rate


total = add_tax(100)
print(total)
```

You should see:

```text
105.0
```

Use a default when an input can be optional.

Use `return` when a function needs to give a result back.

### Mistake 5: Thinking A Default Is Used When Any Falsey Value Is Passed

Defaults are used when the argument is missing.

They are not used just because the argument is empty or false.

Code:

```python
def show_message(message="No message"):
    print("Message:", message)


show_message()
show_message("")
show_message("Ready")
```

You should see:

```text
Message: No message
Message: 
Message: Ready
```

The empty string was still an argument.

Python used it.

The default was only used for:

```python
show_message()
```

## Debug It

Read each goal first.

Then study the broken code and find the problem before looking at the fix.

### Debug 1: Missing Required Argument

Goal:

```text
Hello, Mina!
Hello, Sam!
```

Broken code:

```python
def greet_person(name, greeting="Hello"):
    print(greeting + ", " + name + "!")


greet_person("Mina")
greet_person()
```

The problem:

```text
name is required.
Only greeting has a default.
The second call does not pass a name.
```

Fixed code:

```python
def greet_person(name, greeting="Hello"):
    print(greeting + ", " + name + "!")


greet_person("Mina")
greet_person("Sam")
```

You should see:

```text
Hello, Mina!
Hello, Sam!
```

### Debug 2: Wrong Parameter Order

Goal:

```text
Task: Read docs
Status: not started
```

Broken code:

```python
def show_task(status="not started", task):
    print("Task:", task)
    print("Status:", status)


show_task("Read docs")
```

The problem:

```text
task is required.
It appears after a default parameter.
Required parameters must come first.
```

Fixed code:

```python
def show_task(task, status="not started"):
    print("Task:", task)
    print("Status:", status)


show_task("Read docs")
```

You should see:

```text
Task: Read docs
Status: not started
```

### Debug 3: Default Not Used

Goal:

```text
Message: No message
```

Broken code:

```python
def show_message(message="No message"):
    print("Message:", message)


show_message("")
```

The problem:

```text
The call passes an empty string.
That means the argument is present.
Python does not use the default.
```

Fixed code:

```python
def show_message(message="No message"):
    print("Message:", message)


show_message()
```

You should see:

```text
Message: No message
```

Leave the argument out when you want the default.

### Debug 4: Missing Return

Goal:

```text
105.0
```

Broken code:

```python
def add_tax(price, tax_rate=0.05):
    total = price + price * tax_rate


final_price = add_tax(100)
print(final_price)
```

The problem:

```text
The default tax_rate works.
The function still does not return total.
```

Without `return`, Python gives back `None`.

Fixed code:

```python
def add_tax(price, tax_rate=0.05):
    total = price + price * tax_rate
    return total


final_price = add_tax(100)
print(final_price)
```

You should see:

```text
105.0
```

### Debug 5: Unclear Default

Goal:

```text
Mina joined as member.
```

Broken code:

```python
def show_join_message(name, role=""):
    print(name + " joined as " + role + ".")


show_join_message("Mina")
```

The problem:

```text
The default is an empty string.
The output is not useful for the common case.
```

Fixed code:

```python
def show_join_message(name, role="member"):
    print(name + " joined as " + role + ".")


show_join_message("Mina")
```

You should see:

```text
Mina joined as member.
```

Choose a default that creates useful output when the caller leaves the argument out.

## Read the Docs

Python's official tutorial has a section called default argument values:

```text
https://docs.python.org/3/tutorial/controlflow.html#default-argument-values
```

You do not need to read the whole page today.

Look for examples shaped like this:

```python
def function_name(required, optional="default"):
    print(required)
    print(optional)
```

When you read a function definition, ask:

```text
Which parameters are required?
Which parameters have default values?
What value is used if the caller leaves an argument out?
Does the default make sense for the common case?
```

You may also see the phrase "argument" in the docs.

That is the value passed in the function call.

This call:

```python
greet_person("Mina")
```

passes one argument.

If the function has another parameter with a default, Python can still run the call.

Tomorrow, you will read calls where arguments are named directly in the call.

Those are keyword arguments.

## Mini Challenge

Create a file named:

```text
day-60/default_report.py
```

Build a small report program using default parameters.

Your program should define these functions:

- `print_greeting(name, greeting="Hello")`
- `print_message(message="Keep practicing.")`
- `repeat_line(line="-", times=3)`
- `format_score(name, score, label="points")`
- `show_settings(theme="light", notifications=True)`

Rules:

```text
Call every function at least once with its default.
Call at least three functions with a custom value.
Use one function that returns a value.
Print the returned value.
```

One possible solution:

```python
def print_greeting(name, greeting="Hello"):
    print(greeting + ", " + name + "!")


def print_message(message="Keep practicing."):
    print(message)


def repeat_line(line="-", times=3):
    for count in range(times):
        print(line)


def format_score(name, score, label="points"):
    return name + " scored " + str(score) + " " + label + "."


def show_settings(theme="light", notifications=True):
    print("Theme:", theme)
    print("Notifications:", notifications)


print_greeting("Mina")
print_greeting("Sam", "Welcome")

print_message()
print_message("Review one example before moving on.")

repeat_line()
repeat_line("=", 2)

score_line = format_score("Asha", 18)
print(score_line)
print(format_score("Ben", 4, "stars"))

show_settings()
show_settings("dark", False)
```

You should see:

```text
Hello, Mina!
Welcome, Sam!
Keep practicing.
Review one example before moving on.
-
-
-
=
=
Asha scored 18 points.
Ben scored 4 stars.
Theme: light
Notifications: True
Theme: dark
Notifications: False
```

After it works, change one default value in a function definition.

Run the program again.

Notice which calls changed and which calls stayed the same.

## Real-World Use

Default parameters show up when a function has a common case.

Examples:

```text
send a normal welcome message
repeat something once unless told otherwise
show a setting with a standard value
create a user with the role member
calculate tax with the usual rate
print a report with details turned off
```

Defaults help keep simple calls simple.

Without defaults, every call may need extra information even when the information is ordinary:

```python
def print_receipt(customer, currency):
    print("Customer:", customer)
    print("Currency:", currency)


print_receipt("Mina", "USD")
print_receipt("Sam", "USD")
print_receipt("Iris", "USD")
```

You should see:

```text
Customer: Mina
Currency: USD
Customer: Sam
Currency: USD
Customer: Iris
Currency: USD
```

With a default:

```python
def print_receipt(customer, currency="USD"):
    print("Customer:", customer)
    print("Currency:", currency)


print_receipt("Mina")
print_receipt("Sam")
print_receipt("Iris", "EUR")
```

You should see:

```text
Customer: Mina
Currency: USD
Customer: Sam
Currency: USD
Customer: Iris
Currency: EUR
```

The function is still flexible.

The common case just takes less typing.

Good defaults should be:

- clear
- ordinary
- safe
- easy to explain
- useful when the caller leaves the argument out

If you cannot explain the default, the function may not need one yet.

## Recap

Today you learned how default parameters make some arguments optional.

You practiced:

- defining a parameter with `=`
- calling a function without the optional argument
- overriding the default with a custom argument
- using defaults for greetings
- using defaults for messages
- using defaults for counts and settings
- keeping required parameters before default parameters
- choosing clear defaults
- seeing that defaults are set when the function is defined
- keeping default inputs separate from return values

The key pattern:

```python
def function_name(required, optional="default"):
    print(required)
    print(optional)
```

The key habit:

```text
Use a default only when there is a clear common value.
```

## Lesson Checklist

Before moving on, check that you can:

- explain what a default parameter is
- write a function with one required parameter and one default parameter
- call that function with only the required argument
- call that function with a custom value for the default parameter
- use a default string
- use a default number
- use a default Boolean value
- place default parameters after required parameters
- explain why `def example(a=1, b):` is invalid
- choose a clear default for a common case
- avoid using a confusing placeholder as a default
- explain why changing a variable later does not automatically change a default
- explain why a default is not the same as `return`
- fix a call that accidentally skips a required argument
- recognize how tomorrow's keyword arguments will make some calls clearer

## Exercises

### Exercise 1

Write a function named `greet_person`.

It should have:

```text
name
greeting with a default value of "Hello"
```

This call:

```python
greet_person("Mina")
```

should print:

```text
Hello, Mina!
```

### Exercise 2

Call `greet_person` again with a custom greeting.

This call:

```python
greet_person("Sam", "Good morning")
```

should print:

```text
Good morning, Sam!
```

### Exercise 3

Write a function named `print_message`.

It should have one parameter named `message` with a default value of:

```text
No updates today.
```

Call it once without an argument.

Call it once with a custom message.

### Exercise 4

Write a function named `repeat_word`.

It should have:

```text
word
times with a default value of 2
```

Use a `for` loop and `range(times)` to print the word.

### Exercise 5

Write a function named `show_settings`.

It should have:

```text
theme with a default value of "light"
notifications with a default value of True
```

Call it once with no arguments.

Call it once with custom values.

### Exercise 6

Write a function named `display_score`.

It should have:

```text
player
score
label with a default value of "points"
```

Call it with:

```python
display_score("Asha", 18)
```

Then call it with:

```python
display_score("Ben", 4, "stars")
```

### Exercise 7

Fix the broken function definition.

Broken code:

```python
def print_order(status="pending", order_id):
    print(order_id + " is " + status)
```

The required parameter should come first.

### Exercise 8

Fix the unclear default.

Broken code:

```python
def create_user(name, role=""):
    print(name + " is a " + role + ".")
```

Choose a default role that makes sense when the caller leaves it out.

### Exercise 9

Predict the output before running this code:

```python
def show_message(message="No message"):
    print("Message:", message)


show_message()
show_message("")
show_message("Ready")
```

Then run it and check your prediction.

### Exercise 10

Write a function named `calculate_total`.

It should have:

```text
price
tax_rate with a default value of 0.05
```

Return the total price.

Call it once with the default tax rate and once with a custom tax rate.

### Exercise 11

Fix the broken code.

Broken code:

```python
def calculate_total(price, tax_rate=0.05):
    total = price + price * tax_rate


print(calculate_total(100))
```

The goal is:

```text
105.0
```

### Exercise 12

Write a function named `print_receipt`.

It should have:

```text
customer
currency with a default value of "USD"
```

Call it for two customers who use the default currency.

Call it for one customer who uses `"EUR"`.

### Exercise 13

Write a function named `show_task`.

It should have:

```text
task
status with a default value of "not started"
```

Call it once with only the task.

Call it once with the task and a custom status.

### Exercise 14

Choose one function from yesterday's return value practice.

Add a default parameter if there is a clear common value.

If there is no clear common value, write one sentence explaining why a default would make the function less clear.

### Exercise 15

Write three short function definitions.

Each one should use a different kind of default:

```text
a string default
a number default
a Boolean default
```

Call each function at least twice:

```text
once using the default
once overriding the default
```

## Tiny Win

You can now make a function flexible without forcing every call to repeat ordinary values.

That is the point of defaults:

```text
Keep the common case simple.
Keep the special case possible.
```

## Tomorrow

Tomorrow is:

```text
Day 61: Keyword Arguments
```

Today, you called functions mostly by position:

```python
display_score("Asha", 18, "points")
```

That works, but longer calls can become hard to read.

Tomorrow you will learn how to name arguments in the call:

```python
display_score(player="Asha", score=18, label="points")
```

Default parameters make some arguments optional.

Keyword arguments make many function calls clearer.
