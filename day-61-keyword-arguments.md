# Day 61: Keyword Arguments

**Focus:** Calling functions by naming the parameters you are filling  
**You will practice:** positional arguments, keyword arguments, clearer calls, order flexibility, defaults, and common call mistakes  
**Estimated time:** 45-60 minutes

## Today's Goal

Today you will learn how to call functions with keyword arguments.

You already know that functions can receive values through parameters:

```python
def display_profile(name, city, role):
    print("Name:", name)
    print("City:", city)
    print("Role:", role)


display_profile("Mina", "Pune", "student")
```

You should see:

```text
Name: Mina
City: Pune
Role: student
```

That call uses positional arguments.

The first argument goes into the first parameter, the second argument goes into the second parameter, and so on.

Today you will add another way to call a function:

```text
display_profile(name="Mina", city="Pune", role="student")
```

That call uses keyword arguments.

By the end of this lesson, you should be able to:

- explain what a keyword argument is
- call a function with `parameter=value`
- tell positional arguments and keyword arguments apart
- use keyword arguments to make a function call clearer
- change the order of keyword arguments safely
- combine positional arguments, keyword arguments, and default values carefully
- fix misspelled keyword names
- avoid putting a positional argument after a keyword argument
- avoid using keyword syntax where normal assignment is needed
- choose when keyword arguments help and when they add noise

The main idea is:

```text
A keyword argument names the parameter it is sending a value to.
```

## The Big Idea

Python can match arguments to parameters in two common ways.

It can match by position:

```python
def show_product_price(name, price, currency):
    print("Product:", name)
    print("Price:", currency, price)


show_product_price("notebook", 5, "USD")
```

You should see:

```text
Product: notebook
Price: USD 5
```

In that call:

```text
name receives "notebook"
price receives 5
currency receives "USD"
```

That works because the arguments are in the same order as the parameters.

Python can also match by keyword:

```python
def show_product_price(name, price, currency):
    print("Product:", name)
    print("Price:", currency, price)


show_product_price(name="notebook", price=5, currency="USD")
```

You should see:

```text
Product: notebook
Price: USD 5
```

This time, the call names each parameter directly:

```text
name="notebook"
price=5
currency="USD"
```

The left side is the parameter name.

The right side is the value being passed in.

Read this:

```text
show_product_price(name="notebook", price=5, currency="USD")
```

as:

```text
Call show_product_price.
Send "notebook" to the name parameter.
Send 5 to the price parameter.
Send "USD" to the currency parameter.
```

Keyword arguments are especially useful when a function has several values that could be confusing by position.

Compare this:

```python
def build_message(sender, recipient, message):
    print("From " + sender + " to " + recipient + ": " + message)


build_message("Mina", "Sam", "Please review the notes.")
```

You should see:

```text
From Mina to Sam: Please review the notes.
```

with this:

```python
def build_message(sender, recipient, message):
    print("From " + sender + " to " + recipient + ": " + message)


build_message(
    sender="Mina",
    recipient="Sam",
    message="Please review the notes."
)
```

You should see:

```text
From Mina to Sam: Please review the notes.
```

Both calls work.

The keyword version is longer, but it is easier to read because each value is labeled.

That is the main benefit of keyword arguments:

```text
They can make a function call explain itself.
```

## The Mental Model

Think of a function's parameters as labeled slots.

Example:

```text
def print_contact(name, phone, email):
```

This function has three slots:

```text
name
phone
email
```

With positional arguments, Python fills the slots from left to right:

```python
def print_contact(name, phone, email):
    print("Name:", name)
    print("Phone:", phone)
    print("Email:", email)


print_contact("Mina", "555-0104", "mina@example.com")
```

You should see:

```text
Name: Mina
Phone: 555-0104
Email: mina@example.com
```

With keyword arguments, you point to the slot by name:

```python
def print_contact(name, phone, email):
    print("Name:", name)
    print("Phone:", phone)
    print("Email:", email)


print_contact(email="mina@example.com", name="Mina", phone="555-0104")
```

You should see:

```text
Name: Mina
Phone: 555-0104
Email: mina@example.com
```

Notice the order of the call:

```text
email first
name second
phone third
```

The output still comes out correctly.

That is because Python is no longer guessing by position. It is using the parameter names.

This is allowed:

```text
print_contact(email="mina@example.com", name="Mina", phone="555-0104")
```

This is usually easier to scan:

```text
print_contact(name="Mina", phone="555-0104", email="mina@example.com")
```

Both work.

When you choose the normal parameter order, the call is easier for other people to compare with the function definition.

Keyword arguments also work well with default values.

Example:

```python
def show_product_price(name, price, currency="USD", discount=0):
    print("Product:", name)
    print("Price:", currency, price)
    print("Discount:", str(discount) + "%")


show_product_price("notebook", 5)
print("")
show_product_price("pen", price=2, currency="INR")
print("")
show_product_price(name="bag", price=20, discount=10)
```

You should see:

```text
Product: notebook
Price: USD 5
Discount: 0%

Product: pen
Price: INR 2
Discount: 0%

Product: bag
Price: USD 20
Discount: 10%
```

The first call uses default values for `currency` and `discount`.

The second call gives `name` by position, then gives `price` and `currency` by keyword.

The third call uses keywords and changes only the discount. Since `currency` is not given, it stays `"USD"`.

The careful rule is:

```text
Positional arguments can come before keyword arguments.
Positional arguments cannot come after keyword arguments.
```

This works:

```text
show_product_price("pen", price=2, currency="INR")
```

This does not:

```text
show_product_price(name="pen", 2, currency="INR")
```

Once you start using keyword arguments in a call, keep the rest of that call keyword-based too.

## Try It Yourself

Create a file named:

```text
day-61/keyword_arguments.py
```

Work through these examples one at a time.

### Step 1: Display A Profile

Code:

```python
def display_profile(name, city, hobby):
    print("Name:", name)
    print("City:", city)
    print("Hobby:", hobby)


display_profile("Asha", "Hyderabad", "drawing")
print("")
display_profile(hobby="cycling", name="Dev", city="Kochi")
```

You should see:

```text
Name: Asha
City: Hyderabad
Hobby: drawing

Name: Dev
City: Kochi
Hobby: cycling
```

The first call uses positional arguments.

The second call uses keyword arguments.

The keyword call does not follow the parameter order, but it still works because each value is labeled.

Try this:

```text
Change the city in the keyword call.
Move the keyword arguments into the normal parameter order.
Run the program again.
```

### Step 2: Show A Product Price

Code:

```python
def show_price(product, price, tax_included=False):
    print("Product:", product)
    print("Price:", price)

    if tax_included:
        print("Tax: included")
    else:
        print("Tax: added at checkout")


show_price("notebook", 5)
print("")
show_price(product="water bottle", price=12, tax_included=True)
```

You should see:

```text
Product: notebook
Price: 5
Tax: added at checkout

Product: water bottle
Price: 12
Tax: included
```

The first call uses the default value for `tax_included`.

The second call uses a keyword argument to change that default.

This is one of the most useful places for keyword arguments:

```text
Use a keyword to make an optional setting clear.
```

### Step 3: Print A Contact

Code:

```python
def print_contact(name, phone, email, city="Unknown"):
    print("Name:", name)
    print("Phone:", phone)
    print("Email:", email)
    print("City:", city)


print_contact("Mina", "555-0104", email="mina@example.com")
print("")
print_contact(name="Sam", email="sam@example.com", phone="555-0199", city="Chennai")
```

You should see:

```text
Name: Mina
Phone: 555-0104
Email: mina@example.com
City: Unknown

Name: Sam
Phone: 555-0199
Email: sam@example.com
City: Chennai
```

The first call mixes positional and keyword arguments:

```text
"Mina" fills name
"555-0104" fills phone
email="mina@example.com" fills email
city uses its default value
```

The second call uses keyword arguments for everything.

Both are fine.

Use the version that makes the call easiest to read.

### Step 4: Build A Message

Code:

```python
def build_message(sender, recipient, message, urgent=False):
    line = "From " + sender + " to " + recipient + ": " + message

    if urgent:
        line = "URGENT: " + line

    return line


first_message = build_message("Mina", "Sam", "Please review the notes.")
second_message = build_message(
    recipient="Asha",
    sender="Dev",
    message="The report is ready.",
    urgent=True
)

print(first_message)
print(second_message)
```

You should see:

```text
From Mina to Sam: Please review the notes.
URGENT: From Dev to Asha: The report is ready.
```

The keyword version is useful here because `sender` and `recipient` can be easy to swap by accident.

The call is longer, but it is clearer:

```text
recipient="Asha"
sender="Dev"
urgent=True
```

Long function calls often become easier to read when each argument has a label.

## Common Mistake

Keyword arguments are friendly once you learn the rules, but Python is strict about names and order.

### Mistake 1: Misspelling The Parameter Name

Broken code:

```python
def display_profile(name, city):
    print("Name:", name)
    print("City:", city)


display_profile(nam="Mina", city="Pune")
```

This is broken because the function has a parameter named `name`, not `nam`.

Python may show an error like:

```text
TypeError: display_profile() got an unexpected keyword argument 'nam'
```

Fixed code:

```python
def display_profile(name, city):
    print("Name:", name)
    print("City:", city)


display_profile(name="Mina", city="Pune")
```

You should see:

```text
Name: Mina
City: Pune
```

The keyword name must match the parameter name exactly.

### Mistake 2: Putting A Positional Argument After A Keyword Argument

Broken code:

```python
def show_price(product, price):
    print("Product:", product)
    print("Price:", price)


show_price(product="notebook", 5)
```

This is broken because `5` is positional, but it comes after a keyword argument.

Python may show:

```text
SyntaxError: positional argument follows keyword argument
```

Fixed code:

```python
def show_price(product, price):
    print("Product:", product)
    print("Price:", price)


show_price(product="notebook", price=5)
```

You should see:

```text
Product: notebook
Price: 5
```

Another fixed version is:

```python
def show_price(product, price):
    print("Product:", product)
    print("Price:", price)


show_price("notebook", 5)
```

You should see:

```text
Product: notebook
Price: 5
```

Choose one style for the call and keep it readable.

### Mistake 3: Using Keyword Syntax Where Normal Assignment Is Needed

Keyword syntax belongs inside a function call.

Broken code:

```python
def print_contact(name, phone):
    print("Name:", name)
    print("Phone:", phone)


name="Mina", phone="555-0104"
print_contact()
```

This is broken because `name="Mina", phone="555-0104"` is not how you create two normal variables.

It is trying to use keyword-argument style outside a function call.

Fixed code:

```python
def print_contact(name, phone):
    print("Name:", name)
    print("Phone:", phone)


name = "Mina"
phone = "555-0104"

print_contact(name=name, phone=phone)
```

You should see:

```text
Name: Mina
Phone: 555-0104
```

This line can look strange at first:

```text
print_contact(name=name, phone=phone)
```

Read it as:

```text
Send the value from the variable name into the parameter named name.
Send the value from the variable phone into the parameter named phone.
```

The left side is the parameter name.

The right side is the value or variable you are passing in.

### Mistake 4: Overusing Keywords For Simple Calls

This code works:

```python
def greet(name):
    print("Hello, " + name + "!")


greet(name="Mina")
```

You should see:

```text
Hello, Mina!
```

But this is often simpler:

```python
def greet(name):
    print("Hello, " + name + "!")


greet("Mina")
```

You should see:

```text
Hello, Mina!
```

Keyword arguments are useful when they make meaning clearer.

They are less useful when the call is already obvious.

Good times to use keyword arguments:

- the function has several arguments
- two arguments have the same type, such as two strings or two numbers
- you are changing an optional default
- the call would be hard to understand later

Less useful times:

- the function has one simple argument
- the meaning is already obvious
- the keywords make the line much longer without adding clarity

Good code is not about using every feature every time.

It is about making the next reading easier.

## Debug It

Read each goal first.

Then study the broken code and find the problem before looking at the fix.

### Debug 1: Product Price

Goal:

```text
Product: notebook
Price: 5
```

Broken code:

```python
def print_product(product, price):
    print("Product:", product)
    print("Price:", price)


print_product(proudct="notebook", price=5)
```

The problem:

```text
The keyword proudct is misspelled.
The parameter is named product.
```

Fixed code:

```python
def print_product(product, price):
    print("Product:", product)
    print("Price:", price)


print_product(product="notebook", price=5)
```

You should see:

```text
Product: notebook
Price: 5
```

### Debug 2: Message Builder

Goal:

```text
Hi Mina, remember to save.
```

Broken code:

```python
def build_message(name, reminder):
    return "Hi " + name + ", remember to " + reminder + "."


message = build_message(name="Mina", "save")
print(message)
```

The problem:

```text
"save" is a positional argument.
It comes after the keyword argument name="Mina".
```

Fixed code:

```python
def build_message(name, reminder):
    return "Hi " + name + ", remember to " + reminder + "."


message = build_message(name="Mina", reminder="save")
print(message)
```

You should see:

```text
Hi Mina, remember to save.
```

### Debug 3: Contact Printer

Goal:

```text
Name: Asha
Phone: 555-0188
```

Broken code:

```python
def print_contact(name, phone):
    print("Name:", name)
    print("Phone:", phone)


contact_name = "Asha"
contact_phone = "555-0188"

print_contact(contact_name=name, contact_phone=phone)
```

The problem:

```text
The function does not have parameters named contact_name or contact_phone.
Also, name and phone are not the variables created above.
```

Fixed code:

```python
def print_contact(name, phone):
    print("Name:", name)
    print("Phone:", phone)


contact_name = "Asha"
contact_phone = "555-0188"

print_contact(name=contact_name, phone=contact_phone)
```

You should see:

```text
Name: Asha
Phone: 555-0188
```

The parameter names are on the left.

The variables you want to pass are on the right.

### Debug 4: Default Value

Goal:

```text
Mina: Great work!
```

Broken code:

```python
def build_message(name, message, punctuation="."):
    return name + ": " + message + punctuation


text = build_message("Mina", punctuation="!", "Great work")
print(text)
```

The problem:

```text
"Great work" is positional.
It appears after punctuation="!".
```

Fixed code:

```python
def build_message(name, message, punctuation="."):
    return name + ": " + message + punctuation


text = build_message("Mina", "Great work", punctuation="!")
print(text)
```

You should see:

```text
Mina: Great work!
```

This fixed call uses positional arguments first, then a keyword argument for the optional punctuation.

## Read the Docs

Python's official tutorial has a section on keyword arguments:

```text
https://docs.python.org/3/tutorial/controlflow.html#keyword-arguments
```

You do not need to read every detail today.

Look for examples where a function is called like this:

```text
function_name(parameter=value)
```

When reading documentation, ask:

```text
What are the parameter names?
Which arguments are positional?
Which arguments are keyword arguments?
Are any default values being changed?
```

You will often see keyword arguments in documentation because they make examples easier to understand.

For example, a function call like this:

```text
create_user(username="mina", active=True)
```

is easier to read than:

```text
create_user("mina", True)
```

The second call may work, but the first call explains what `True` means.

That is the reading habit to build.

Do not only ask:

```text
Does this code run?
```

Also ask:

```text
Will this call still make sense when I read it next week?
```

## Mini Challenge

Create a file named:

```text
day-61/profile_product_messages.py
```

Build a small program that uses keyword arguments in useful places.

Your program should define these functions:

- `display_profile(name, city, interest)`
- `show_product_price(product, price, currency="USD", sale=False)`
- `print_contact(name, phone, email, city="Unknown")`
- `build_message(sender, recipient, text, urgent=False)`

Rules:

```text
Call at least one function with positional arguments.
Call at least one function with keyword arguments.
Call at least one function with a mix of positional and keyword arguments.
Use a keyword argument to change a default value.
Use a keyword argument order that is different from the function definition at least once.
```

One possible solution:

```python
def display_profile(name, city, interest):
    print("Name:", name)
    print("City:", city)
    print("Interest:", interest)


def show_product_price(product, price, currency="USD", sale=False):
    print("Product:", product)
    print("Price:", currency, price)

    if sale:
        print("Sale item: yes")
    else:
        print("Sale item: no")


def print_contact(name, phone, email, city="Unknown"):
    print("Name:", name)
    print("Phone:", phone)
    print("Email:", email)
    print("City:", city)


def build_message(sender, recipient, text, urgent=False):
    message = "From " + sender + " to " + recipient + ": " + text

    if urgent:
        message = "URGENT: " + message

    return message


display_profile(name="Mina", interest="reading", city="Pune")
print("")

show_product_price("notebook", price=5)
print("")

print_contact("Sam", "555-0199", email="sam@example.com")
print("")

message = build_message(
    recipient="Asha",
    sender="Dev",
    text="Can you check the contact list?",
    urgent=True
)

print(message)
```

You should see:

```text
Name: Mina
City: Pune
Interest: reading

Product: notebook
Price: USD 5
Sale item: no

Name: Sam
Phone: 555-0199
Email: sam@example.com
City: Unknown

URGENT: From Dev to Asha: Can you check the contact list?
```

After it works, change only the function calls.

Try these changes:

```text
Change the product currency.
Mark the product as a sale item.
Give the contact a city.
Make the message not urgent.
Put the keyword arguments back into the normal parameter order.
```

The function definitions can stay the same.

You are practicing how different calls can use the same function in clear ways.

## Real-World Use

Keyword arguments show up often in real programs because real functions can have several settings.

You might see calls shaped like this:

```text
send_message(to="sam@example.com", subject="Reminder", urgent=True)
create_user(username="mina", email="mina@example.com", active=True)
calculate_total(price=20, tax_rate=0.08, discount=5)
save_contact(name="Asha", phone="555-0188", favorite=False)
```

The keyword names help you read the call without looking up the function immediately.

They are especially useful for boolean values.

This is not very clear:

```text
show_product_price("notebook", 5, "USD", True)
```

What does `True` mean?

This is clearer:

```text
show_product_price("notebook", 5, currency="USD", sale=True)
```

Now the meaning is visible in the call.

Keyword arguments are also helpful when a function has default values.

If a function has several optional settings, keywords let you change one setting without filling in every setting before it.

Example:

```python
def build_message(sender, recipient, text, urgent=False, punctuation="."):
    message = "From " + sender + " to " + recipient + ": " + text + punctuation

    if urgent:
        message = "URGENT: " + message

    return message


message = build_message(
    "Mina",
    "Sam",
    "Please review the notes",
    punctuation="!"
)

print(message)
```

You should see:

```text
From Mina to Sam: Please review the notes!
```

The call changes `punctuation` while leaving `urgent` at its default value of `False`.

That is hard to do clearly with only positional arguments.

## Recap

A positional argument is matched by order:

```text
show_price("notebook", 5)
```

A keyword argument is matched by parameter name:

```text
show_price(product="notebook", price=5)
```

Keyword arguments use this shape:

```text
parameter=value
```

The parameter name must match the function definition.

Keyword arguments can make calls clearer, especially when:

- a function has several arguments
- the argument order is easy to mix up
- a value like `True` or `False` needs a label
- you are changing a default value
- the call would otherwise be hard to read

The key rule for mixing styles is:

```text
Put positional arguments first.
Put keyword arguments after them.
```

This works:

```text
print_contact("Mina", phone="555-0104", email="mina@example.com")
```

This does not:

```text
print_contact(name="Mina", "555-0104", email="mina@example.com")
```

Keyword arguments do not replace positional arguments.

They give you another tool for writing clearer function calls.

## Lesson Checklist

Before moving on, check that you can:

- explain what a keyword argument is
- write a function call using `parameter=value`
- explain the difference between positional and keyword arguments
- call a function with all positional arguments
- call a function with all keyword arguments
- mix positional and keyword arguments in the correct order
- explain why keyword arguments can be easier to read
- use keyword arguments with default values
- identify the parameter name on the left side of `=`
- identify the value or variable on the right side of `=`
- fix a misspelled keyword argument
- fix a call where a positional argument appears after a keyword argument
- avoid using keyword syntax outside a function call
- decide when keywords are helpful and when they are unnecessary

## Exercises

### Exercise 1

Write a function named `display_profile`.

It should have three parameters:

```text
name
city
hobby
```

Call it once with positional arguments.

Call it once with keyword arguments.

### Exercise 2

Read this function:

```python
def print_contact(name, phone, email):
    print("Name:", name)
    print("Phone:", phone)
    print("Email:", email)
```

Write a call that uses keyword arguments in the normal order.

Then write a call that uses keyword arguments in a different order.

### Exercise 3

Fix the broken code.

Broken code:

```python
def show_price(product, price):
    print(product, price)


show_price(prduct="notebook", price=5)
```

The goal is to print:

```text
notebook 5
```

### Exercise 4

Fix the broken code.

Broken code:

```python
def show_price(product, price):
    print(product, price)


show_price(product="notebook", 5)
```

The goal is to use keyword arguments correctly.

### Exercise 5

Write a function named `show_product`.

It should have these parameters:

```text
name
price
currency
```

Call it like this:

```text
show_product(name="pen", price=2, currency="INR")
```

### Exercise 6

Update `show_product` so `currency` has a default value of `"USD"`.

Call it once without giving `currency`.

Call it once with `currency="INR"`.

### Exercise 7

Write a function named `build_message`.

It should have these parameters:

```text
sender
recipient
message
```

Use keyword arguments so the call clearly shows who sends the message and who receives it.

### Exercise 8

Read this call:

```text
build_message(recipient="Sam", message="See you at 4.", sender="Mina")
```

Answer these questions:

```text
Which value goes into recipient?
Which value goes into message?
Which value goes into sender?
Does the order of the keywords matter here?
```

### Exercise 9

Fix the broken code.

Broken code:

```python
def print_contact(name, phone):
    print("Name:", name)
    print("Phone:", phone)


contact_name = "Dev"
contact_phone = "555-0160"

print_contact(contact_name=name, contact_phone=phone)
```

The goal is:

```text
Name: Dev
Phone: 555-0160
```

### Exercise 10

Write a function named `show_task`.

It should have these parameters:

```text
title
done=False
```

Call it once with the default value.

Call it once with `done=True`.

Use a keyword argument for `done`.

### Exercise 11

This call works:

```text
greet(name="Mina")
```

Write one sentence explaining why this might still be less readable than:

```text
greet("Mina")
```

### Exercise 12

Write two versions of a call to this function:

```python
def show_score(player, score, total):
    print(player, score, total)
```

One version should use only positional arguments.

One version should use only keyword arguments.

### Exercise 13

Write a function named `print_label`.

It should have two parameters:

```text
label
value
```

Call it like this:

```text
print_label(label="City", value="Pune")
```

Then call it like this:

```text
print_label(value="Pune", label="City")
```

Both calls should print the same result.

### Exercise 14

Fix the broken code.

Broken code:

```python
def build_message(name, message, punctuation="."):
    print(name + ": " + message + punctuation)


build_message(name="Asha", punctuation="!", "Good morning")
```

The goal is:

```text
Asha: Good morning!
```

### Exercise 15

Choose one function from today's lesson:

```text
display_profile
show_product_price
print_contact
build_message
```

Write three calls to that function:

```text
one positional call
one keyword call
one mixed call
```

Then decide which call is easiest to read and explain why.

## Tiny Win

You can now choose how a function call sends values into parameters.

For short obvious calls, positional arguments may be enough.

For longer calls, optional settings, and easy-to-swap values, keyword arguments can make the code much easier to read.

The tiny win is this:

```text
You can label values at the call site instead of relying only on order.
```

That small habit makes many function calls less mysterious.

## Tomorrow

Tomorrow is:

```text
Day 62: Scope
```

Today you saw names in a few different places:

```text
parameter names
variable names
keyword names in function calls
```

Tomorrow you will learn where names exist and where Python can use them.

That topic is called scope.

The next question will be:

```text
Where is this name available?
```

Keyword arguments help you pay attention to parameter names.

Scope will help you pay attention to where names live.
