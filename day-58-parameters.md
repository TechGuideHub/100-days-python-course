# Day 58: Parameters

**Focus:** Giving functions values to work with  
**You will practice:** one parameter, multiple parameters, arguments, calling the same function with different values, and using parameters inside function bodies  
**Estimated time:** 45-60 minutes

## Today's Goal

Today you will make functions more flexible.

Yesterday, you learned how to write a function and call it. A function without parameters does the same job every time you call it.

Today, you will learn how to send information into a function.

By the end of this lesson, you should be able to:

- define a function with one parameter
- define a function with multiple parameters
- call a function with arguments
- explain the difference between a parameter and an argument
- use parameter names inside the function body
- call the same function with different values
- debug wrong argument counts
- avoid quoting variable names accidentally

The main idea is:

```text
A parameter is a name that receives a value when the function is called.
```

Today, your functions will still mostly print results.

Tomorrow, you will learn how functions can send values back with `return`.

## The Big Idea

A function can have a blank space for information it needs.

That blank space is called a parameter.

Example:

```python
def greet_person(name):
    print("Hello, " + name + "!")


greet_person("Mina")
greet_person("Sam")
greet_person("Iris")
```

You should see:

```text
Hello, Mina!
Hello, Sam!
Hello, Iris!
```

In this function:

```python
def greet_person(name):
    print("Hello, " + name + "!")
```

`name` is the parameter.

It is a name the function can use inside its body.

In this call:

```python
greet_person("Mina")
```

`"Mina"` is the argument.

It is the actual value being sent into the function.

Read it like this:

```text
Call greet_person.
Give it the value "Mina".
Inside the function, the parameter name receives "Mina".
```

That is why one function can greet many different people.

The code inside the function stays the same. The value passed in can change.

## The Mental Model

Think of a parameter as a temporary label inside a function.

When you write:

```python
def display_score(player, score):
    print(player + " scored " + str(score) + " points.")


display_score("Asha", 18)
display_score("Ben", 12)
```

You should see:

```text
Asha scored 18 points.
Ben scored 12 points.
```

The first call works like this:

```text
player receives "Asha"
score receives 18
```

The second call works like this:

```text
player receives "Ben"
score receives 12
```

The parameter names only exist for the function while it is running.

Inside the function body, you can use them like normal variables:

```python
def show_product(name, price, stock):
    print("Product:", name)
    print("Price:", price)
    print("In stock:", stock)


show_product("notebook", 5, 12)
```

You should see:

```text
Product: notebook
Price: 5
In stock: 12
```

For now, order matters.

This call:

```python
show_product("notebook", 5, 12)
```

matches this definition:

```text
def show_product(name, price, stock):
```

So Python connects the values like this:

```text
name receives "notebook"
price receives 5
stock receives 12
```

If you pass the values in the wrong order, Python may still run, but the output may not make sense.

## Try It Yourself

Create a file named:

```text
day-58/parameters_practice.py
```

Work through these examples one at a time.

### Step 1: One Parameter

Code:

```python
def greet_person(name):
    print("Hello, " + name + "!")


greet_person("Mina")
greet_person("Ravi")
greet_person("Asha")
```

You should see:

```text
Hello, Mina!
Hello, Ravi!
Hello, Asha!
```

Try this:

```text
Change the names.
Add two more function calls.
Run the program again.
```

The function does not need to be rewritten for each person.

Only the argument changes.

### Step 2: Use A Variable As The Argument

An argument can be a literal value:

```python
def greet_person(name):
    print("Hello, " + name + "!")


greet_person("Mina")
```

It can also be a variable:

```python
def greet_person(name):
    print("Hello, " + name + "!")


student_name = "Dev"
greet_person(student_name)
```

You should see:

```text
Hello, Dev!
```

In the call:

```python
greet_person(student_name)
```

Python first reads the value stored in `student_name`.

Then that value is passed into the function.

### Step 3: Multiple Parameters

A function can receive more than one value.

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

The function has two parameters:

```text
name
phone
```

Each call needs two arguments.

### Step 4: Use Parameters Inside The Body

Parameters are useful because the function body can build work around them.

Code:

```python
def display_score(player, score):
    if score >= 10:
        print(player + " had a strong round.")
    else:
        print(player + " is still warming up.")

    print("Score:", score)


display_score("Asha", 12)
display_score("Ben", 7)
```

You should see:

```text
Asha had a strong round.
Score: 12
Ben is still warming up.
Score: 7
```

The function uses `score` in an `if` statement.

It uses `player` when it prints the message.

Parameters are not only for printing directly. They can guide decisions inside the function.

### Step 5: Show A Product

Code:

```python
def show_product(name, price, stock):
    print("Product:", name)
    print("Price:", price)

    if stock == 0:
        print("Status: out of stock")
    else:
        print("Status:", stock, "available")


show_product("notebook", 5, 12)
show_product("pen", 2, 0)
```

You should see:

```text
Product: notebook
Price: 5
Status: 12 available
Product: pen
Price: 2
Status: out of stock
```

The same function can show different products because each call sends different arguments.

### Step 6: Print A Repeated Line

Code:

```python
def print_repeated_line(line, times):
    for count in range(times):
        print(line)


print_repeated_line("Practice parameters", 3)
print_repeated_line("-", 5)
```

You should see:

```text
Practice parameters
Practice parameters
Practice parameters
-
-
-
-
-
```

The parameter `line` controls what gets printed.

The parameter `times` controls how many times the loop runs.

## Common Mistake

Parameters are simple, but a few mistakes show up often.

### Mistake 1: Using The Wrong Name Inside The Function

Broken code:

```python
def greet_person(person_name):
    print("Hello, " + name + "!")


greet_person("Mina")
```

This is broken because the parameter is named `person_name`, but the function body tries to use `name`.

Python raises a `NameError` because `name` does not exist.

Fixed code:

```python
def greet_person(person_name):
    print("Hello, " + person_name + "!")


greet_person("Mina")
```

You should see:

```text
Hello, Mina!
```

Use the same parameter name inside the function body.

### Mistake 2: Passing The Wrong Number Of Arguments

Broken code:

```python
def print_contact(name, phone):
    print("Name:", name)
    print("Phone:", phone)


print_contact("Mina")
```

This is broken because the function expects two arguments:

```text
name
phone
```

The call only gives one.

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

When a function has two parameters, each normal call needs two arguments.

### Mistake 3: Quoting A Variable Name By Accident

This code runs, but it does the wrong thing.

Broken code:

```python
def greet_person(name):
    print("Hello, " + name + "!")


student_name = "Mina"
greet_person("student_name")
```

You should see:

```text
Hello, student_name!
```

The problem is the quotes.

`"student_name"` is the text `student_name`.

`student_name` without quotes means the value stored in the variable.

Fixed code:

```python
def greet_person(name):
    print("Hello, " + name + "!")


student_name = "Mina"
greet_person(student_name)
```

You should see:

```text
Hello, Mina!
```

Use quotes when you want exact text.

Leave quotes off when you want Python to read a variable.

### Mistake 4: Confusing Parameter And Argument

Broken code:

```python
def greet_person("Mina"):
    print("Hello!")
```

This is broken because the function definition needs a parameter name, not the actual value.

`"Mina"` belongs in the function call.

Fixed code:

```python
def greet_person(name):
    print("Hello, " + name + "!")


greet_person("Mina")
```

You should see:

```text
Hello, Mina!
```

Remember:

```text
Parameter: the name in the function definition.
Argument: the value in the function call.
```

### Mistake 5: Passing Values In The Wrong Order

This code runs, but the result is confusing.

Broken code:

```python
def display_score(player, score):
    print(player + " scored " + str(score) + " points.")


display_score(18, "Asha")
```

You should see:

```text
18 scored Asha points.
```

The values are in the wrong order.

Fixed code:

```python
def display_score(player, score):
    print(player + " scored " + str(score) + " points.")


display_score("Asha", 18)
```

You should see:

```text
Asha scored 18 points.
```

For now, match the call order to the definition order.

## Debug It

Read each goal first.

Then study the broken code and find the problem before looking at the fix.

### Debug 1: Greeting

Goal:

```text
Hello, Mina!
```

Broken code:

```python
def greet_person(name):
    print("Hello, " + person + "!")


greet_person("Mina")
```

The problem:

```text
The parameter is named name.
The function body uses person.
Those names do not match.
```

Fixed code:

```python
def greet_person(name):
    print("Hello, " + name + "!")


greet_person("Mina")
```

You should see:

```text
Hello, Mina!
```

### Debug 2: Contact Card

Goal:

```text
Name: Sam
Phone: 555-0199
Email: sam@example.com
```

Broken code:

```python
def print_contact(name, phone, email):
    print("Name:", name)
    print("Phone:", phone)
    print("Email:", email)


print_contact("Sam", "555-0199")
```

The problem:

```text
The function has three parameters, so the call needs three arguments.
```

Fixed code:

```python
def print_contact(name, phone, email):
    print("Name:", name)
    print("Phone:", phone)
    print("Email:", email)


print_contact("Sam", "555-0199", "sam@example.com")
```

You should see:

```text
Name: Sam
Phone: 555-0199
Email: sam@example.com
```

### Debug 3: Score Message

Goal:

```text
Asha scored 15 points.
```

Broken code:

```python
def display_score(player, score):
    print(player + " scored " + str(score) + " points.")


player_name = "Asha"
player_score = 15

display_score("player_name", "player_score")
```

The problem:

```text
The call passes text, not the values stored in the variables.
```

Fixed code:

```python
def display_score(player, score):
    print(player + " scored " + str(score) + " points.")


player_name = "Asha"
player_score = 15

display_score(player_name, player_score)
```

You should see:

```text
Asha scored 15 points.
```

### Debug 4: Repeated Line

Goal:

```text
Focus
Focus
Focus
```

Broken code:

```python
def print_repeated_line(line, times):
    for count in range(line):
        print(times)


print_repeated_line("Focus", 3)
```

The problem:

```text
The loop should use times.
The print should use line.
The code swapped the two parameter names inside the function body.
```

Fixed code:

```python
def print_repeated_line(line, times):
    for count in range(times):
        print(line)


print_repeated_line("Focus", 3)
```

You should see:

```text
Focus
Focus
Focus
```

When debugging parameters, ask:

- What parameters does the function define?
- How many arguments does the call pass?
- Do the names inside the function match the parameter names?
- Did I pass a variable or the text of a variable name?
- Are the arguments in the right order?

## Read the Docs

Python's official tutorial explains function definitions here:

```text
https://docs.python.org/3/tutorial/controlflow.html#defining-functions
```

You do not need to read the whole page today.

Look for the shape:

```python
def function_name(parameter):
    print(parameter)


function_name("argument")
```

In documentation, you may see examples with different parameter names.

That is normal. Parameter names are chosen by the person writing the function.

Try this documentation-reading habit:

```text
Find the function definition.
Circle the parameter names.
Find the function calls.
Notice the argument values.
Ask what each parameter receives.
```

Here is a small practice example:

```python
def repeat_word(word, count):
    for number in range(count):
        print(word)


repeat_word("Python", 2)
```

You should see:

```text
Python
Python
```

Read it as:

```text
word receives "Python"
count receives 2
```

That habit will help when you read other people's code.

## Mini Challenge

Create a file named:

```text
day-58/contact_and_score_report.py
```

Build a small report program using functions with parameters.

Your program should define these functions:

- `greet_person(name)`
- `print_contact(name, phone, email)`
- `display_score(player, score)`
- `show_product(name, price, stock)`
- `print_repeated_line(line, times)`

Rules:

```text
Call every function at least twice.
Use different argument values each time.
Use at least one variable as an argument.
Use at least one literal value as an argument.
```

One possible solution:

```python
def greet_person(name):
    print("Hello, " + name + "!")


def print_contact(name, phone, email):
    print("Name:", name)
    print("Phone:", phone)
    print("Email:", email)


def display_score(player, score):
    print(player + " scored " + str(score) + " points.")


def show_product(name, price, stock):
    print("Product:", name)
    print("Price:", price)
    print("Stock:", stock)


def print_repeated_line(line, times):
    for count in range(times):
        print(line)


student_name = "Mina"
student_score = 18

greet_person(student_name)
greet_person("Sam")

print_repeated_line("-", 3)

print_contact("Mina", "555-0104", "mina@example.com")

print_repeated_line("-", 3)

print_contact("Sam", "555-0199", "sam@example.com")

print_repeated_line("-", 3)

display_score(student_name, student_score)
display_score("Sam", 12)

print_repeated_line("-", 3)

show_product("notebook", 5, 12)
show_product("pen", 2, 0)
```

You should see:

```text
Hello, Mina!
Hello, Sam!
-
-
-
Name: Mina
Phone: 555-0104
Email: mina@example.com
-
-
-
Name: Sam
Phone: 555-0199
Email: sam@example.com
-
-
-
Mina scored 18 points.
Sam scored 12 points.
-
-
-
Product: notebook
Price: 5
Stock: 12
Product: pen
Price: 2
Stock: 0
```

After it works, change only the function calls.

Do not change the function definitions.

That is the point of parameters: the function can stay the same while the input values change.

## Real-World Use

Parameters make functions reusable.

Without parameters, you may end up with separate functions for every small variation:

```python
def greet_mina():
    print("Hello, Mina!")


def greet_sam():
    print("Hello, Sam!")


greet_mina()
greet_sam()
```

You should see:

```text
Hello, Mina!
Hello, Sam!
```

That works, but it does not scale well.

This is more useful:

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

The function describes the general action.

The argument supplies the specific value.

This pattern appears everywhere:

```text
send an email to this address
show this product
save this contact
display this score
repeat this message
search for this word
format this report
```

The action is reusable. The data changes.

Parameters are one of the main ways programs avoid repeated code.

## Recap

Today you learned how parameters let functions receive values.

You practiced:

- defining one parameter
- defining multiple parameters
- calling a function with arguments
- using parameters inside the function body
- passing literal values as arguments
- passing variables as arguments
- calling the same function with different values
- printing contacts, scores, products, greetings, and repeated lines
- debugging mismatched names
- debugging wrong argument counts
- avoiding accidental quotes around variable names
- telling parameters and arguments apart

The key vocabulary:

```text
Parameter: a name in the function definition.
Argument: a value passed into the function call.
```

The key habit:

```text
When a function call runs, each parameter receives the matching argument.
```

## Lesson Checklist

Before moving on, check that you can:

- explain what a parameter is
- explain what an argument is
- write a function with one parameter
- call that function with different argument values
- write a function with two or three parameters
- match arguments to parameters by order
- use a parameter inside a `print()` call
- use a parameter inside an `if` statement
- use a parameter inside a loop
- pass a variable as an argument
- avoid putting quotes around a variable argument
- fix a function that uses the wrong parameter name
- fix a call with too few arguments
- explain why parameters reduce repeated code

## Exercises

### Exercise 1

Write a function named `greet_person`.

It should have one parameter named `name`.

It should print:

```text
Hello, Mina!
```

when called like this:

```python
greet_person("Mina")
```

### Exercise 2

Call your `greet_person` function three times with three different names.

### Exercise 3

Create a variable:

```python
student_name = "Asha"
```

Pass that variable into `greet_person`.

Make sure you do not put quotes around `student_name` in the function call.

### Exercise 4

Write a function named `print_contact`.

It should have two parameters:

```text
name
phone
```

Call it with:

```python
print_contact("Mina", "555-0104")
```

### Exercise 5

Update `print_contact` so it has three parameters:

```text
name
phone
email
```

Call it with three arguments.

### Exercise 6

Write a function named `display_score`.

It should have two parameters:

```text
player
score
```

It should print:

```text
Asha scored 15 points.
```

when called with `"Asha"` and `15`.

### Exercise 7

Update `display_score`.

If `score` is at least `10`, print:

```text
Strong round
```

Otherwise, print:

```text
Keep practicing
```

### Exercise 8

Write a function named `show_product`.

It should have three parameters:

```text
name
price
stock
```

It should print all three values in a short product card.

### Exercise 9

Write a function named `print_repeated_line`.

It should have two parameters:

```text
line
times
```

Use a `for` loop and `range(times)` to print the line more than once.

### Exercise 10

Fix the broken code.

Broken code:

```python
def greet_person(person_name):
    print("Hello, " + name + "!")


greet_person("Mina")
```

The goal is:

```text
Hello, Mina!
```

### Exercise 11

Fix the broken code.

Broken code:

```python
def display_score(player, score):
    print(player + " scored " + str(score) + " points.")


display_score("Asha")
```

The goal is:

```text
Asha scored 15 points.
```

### Exercise 12

Fix the broken code.

Broken code:

```python
def greet_person(name):
    print("Hello, " + name + "!")


student_name = "Mina"
greet_person("student_name")
```

The goal is:

```text
Hello, Mina!
```

### Exercise 13

Fix the broken code.

Broken code:

```python
def show_product(name, price, stock):
    print("Product:", name)
    print("Price:", price)
    print("Stock:", stock)


show_product(5, "notebook", 12)
```

The goal is for the product name to be `notebook` and the price to be `5`.

### Exercise 14

Write a function named `print_label`.

It should have two parameters:

```text
label
value
```

This call:

```python
print_label("City", "Pune")
```

should print:

```text
City: Pune
```

Call it at least three times with different labels and values.

### Exercise 15

Choose one short program from an earlier day that repeats similar print lines.

Write one function with parameters that could replace the repeated lines.

You do not need to rewrite the whole old program yet.

Just write the function and two example calls.

## Tiny Win

You can now write one function and reuse it with different values.

That is a major step in writing cleaner programs.

Instead of copying the same print pattern again and again, you can give the pattern a name and pass in the parts that change.

## Tomorrow

Tomorrow is:

```text
Day 59: Return Values
```

Today, your functions mostly printed results.

That is useful, but sometimes a function should calculate or prepare a value and hand it back to the rest of the program.

Tomorrow you will learn how `return` works.

The new question will be:

```text
Should this function print the answer, or should it give the answer back?
```

Parameters help a function receive values.

Return values help a function send values back.
