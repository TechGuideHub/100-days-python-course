# Day 44: Reading Dictionary Values

**Focus:** Getting values out of dictionaries by key  
**You will practice:** square-bracket access, `get()`, missing keys, `KeyError`, clear key names, and using dictionary values in sentences and calculations  
**Estimated time:** 40-50 minutes

## Today's Goal

Today you will learn how to read values from a dictionary.

A dictionary stores values behind keys:

```python
student = {
    "name": "Asha",
    "age": 14,
    "city": "Chennai"
}
```

The keys are:

```text
name
age
city
```

The values are:

```text
Asha
14
Chennai
```

By the end of this lesson, you should be able to:

- read a dictionary value with square brackets
- read a dictionary value with `get()`
- explain what happens when a key is missing
- recognize a `KeyError`
- choose clear key names
- use dictionary values inside sentences
- use dictionary values in simple calculations
- avoid confusing dictionary keys with list indexes

The main idea is:

```text
Use the key to ask the dictionary for its value.
```

Today is about reading data that is already there.

Tomorrow you will learn how to change dictionary data.

## The Big Idea

A list uses positions.

```python
colors = ["red", "green", "blue"]

print(colors[0])
```

You should see:

```text
red
```

A dictionary uses keys.

```python
profile = {
    "name": "Mina",
    "city": "Pune",
    "level": "beginner"
}

print(profile["name"])
print(profile["city"])
print(profile["level"])
```

You should see:

```text
Mina
Pune
beginner
```

The square brackets are familiar, but the meaning is different.

With a list, the value inside the brackets is an index:

```text
colors[0]
```

With a dictionary, the value inside the brackets is a key:

```text
profile["name"]
```

That key must match exactly.

This works:

```python
book = {
    "title": "Python Notes",
    "pages": 120
}

print(book["title"])
```

You should see:

```text
Python Notes
```

This does not work:

Broken code:

```python
book = {
    "title": "Python Notes",
    "pages": 120
}

print(book["Title"])
```

The dictionary has a key named `"title"`, not `"Title"`.

Python treats those as different keys.

You will see an error that ends with:

```text
KeyError: 'Title'
```

That error is Python saying:

```text
I looked for this key, but it is not in the dictionary.
```

## The Mental Model

Think of a dictionary as a set of labeled boxes.

Each label is a key.

Each box holds a value.

```text
key       value
name      Asha
age       14
city      Chennai
```

When you write:

```text
student["city"]
```

read it as:

```text
Go to the student dictionary.
Find the box labeled "city".
Give me the value inside it.
```

The order is not the main point.

The label is the main point.

That is why this dictionary is easier to read than a list for profile-style data:

```python
student = {
    "name": "Asha",
    "age": 14,
    "city": "Chennai"
}
```

Compare that with:

```python
student = ["Asha", 14, "Chennai"]
```

The list version works, but you have to remember what each position means.

```text
0 means name
1 means age
2 means city
```

The dictionary version says the meaning directly:

```text
student["name"]
student["age"]
student["city"]
```

Clear keys make the code easier to read.

Prefer keys like:

```text
name
age
city
daily_goal
is_member
favorite_language
```

Avoid keys that are too vague:

```text
n
x
thing
data
value
```

Short keys are sometimes fine in small examples, but clear keys are kinder to the person reading the program.

That person might be you tomorrow.

## Try It Yourself

Create a file named:

```text
day-44/read_values.py
```

You will read values from a few small dictionaries.

### Step 1: Read Values With Square Brackets

Code:

```python
student = {
    "name": "Asha",
    "age": 14,
    "city": "Chennai"
}

print(student["name"])
print(student["age"])
print(student["city"])
```

You should see:

```text
Asha
14
Chennai
```

Each line asks for one value by key.

### Step 2: Put Values Into Variables

Code:

```python
student = {
    "name": "Asha",
    "age": 14,
    "city": "Chennai"
}

name = student["name"]
city = student["city"]

print(name)
print(city)
```

You should see:

```text
Asha
Chennai
```

This is useful when you want to reuse the value.

### Step 3: Use Values In A Sentence

Code:

```python
student = {
    "name": "Asha",
    "age": 14,
    "city": "Chennai"
}

name = student["name"]
age = student["age"]
city = student["city"]

print(f"{name} is {age} years old and lives in {city}.")
```

You should see:

```text
Asha is 14 years old and lives in Chennai.
```

The dictionary stores the facts.

The sentence uses those facts.

### Step 4: Use Values In A Calculation

Code:

```python
cart_item = {
    "name": "notebook",
    "price": 3,
    "quantity": 4
}

price = cart_item["price"]
quantity = cart_item["quantity"]
total = price * quantity

print(f"Item: {cart_item['name']}")
print(f"Total: {total}")
```

You should see:

```text
Item: notebook
Total: 12
```

Dictionary values are normal Python values.

If the value is a number, you can use it in math.

If the value is a string, you can use it in text.

### Step 5: Read A Key Stored In A Variable

Sometimes the key itself is stored in a variable.

Code:

```python
profile = {
    "name": "Mina",
    "city": "Pune",
    "level": "beginner"
}

field = "city"

print(profile[field])
```

You should see:

```text
Pune
```

Python reads `field` first.

The variable `field` contains the string `"city"`.

So this:

```text
profile[field]
```

means the same thing as:

```text
profile["city"]
```

This is useful, but it is also a common place to make mistakes.

You will practice that more below.

### Step 6: Use `get()` For A Safe Lookup

Square brackets are strict.

If the key is missing, Python raises a `KeyError`.

`get()` gives you another option.

Code:

```python
profile = {
    "name": "Mina",
    "city": "Pune"
}

print(profile.get("name"))
print(profile.get("email", "No email saved"))
```

You should see:

```text
Mina
No email saved
```

The key `"name"` exists, so `get("name")` returns `"Mina"`.

The key `"email"` does not exist, so `get("email", "No email saved")` returns the backup value.

That backup value is called a default.

Use square brackets when the key should be there.

Use `get()` when a missing key is normal and you have a backup value.

### Step 7: Notice What `get()` Does Not Do

`get()` reads from the dictionary.

It does not add the missing key.

Code:

```python
profile = {
    "name": "Mina",
    "city": "Pune"
}

email = profile.get("email", "No email saved")

print(email)
print(profile)
```

You should see:

```text
No email saved
{'name': 'Mina', 'city': 'Pune'}
```

The dictionary did not change.

Changing dictionaries is tomorrow's lesson.

## Common Mistake

### Mistake 1: Misspelling A Key

Broken code:

```python
student = {
    "name": "Asha",
    "city": "Chennai"
}

print(student["ciyt"])
```

This is broken because the dictionary has `"city"`, not `"ciyt"`.

You will see an error that ends with:

```text
KeyError: 'ciyt'
```

Fixed code:

```python
student = {
    "name": "Asha",
    "city": "Chennai"
}

print(student["city"])
```

You should see:

```text
Chennai
```

When you see `KeyError`, check the spelling of the key first.

### Mistake 2: Using A Variable When You Meant A String Key

Broken code:

```python
profile = {
    "name": "Mina",
    "city": "Pune"
}

city = "Mumbai"

print(profile[city])
```

This is broken because `city` is a variable.

Python reads the variable first.

The variable contains `"Mumbai"`, so Python tries this:

```text
profile["Mumbai"]
```

There is no `"Mumbai"` key in the dictionary.

Fixed code:

```python
profile = {
    "name": "Mina",
    "city": "Pune"
}

print(profile["city"])
```

You should see:

```text
Pune
```

If you mean the key named `"city"`, use quotes.

If you mean "use the key stored inside this variable", do not use quotes.

Example:

```python
profile = {
    "name": "Mina",
    "city": "Pune"
}

field = "city"

print(profile[field])
```

You should see:

```text
Pune
```

### Mistake 3: Confusing Index Access With Key Access

Broken code:

```python
student = {
    "name": "Asha",
    "age": 14
}

print(student[0])
```

This is broken because the dictionary does not have a key named `0`.

The first pair in the dictionary is not read with `[0]`.

Fixed code:

```python
student = {
    "name": "Asha",
    "age": 14
}

print(student["name"])
```

You should see:

```text
Asha
```

Use indexes for lists.

Use keys for dictionaries.

### Mistake 4: Using `get()` Without Thinking About The Default

Code:

```python
settings = {
    "theme": "light"
}

print(settings.get("font_size"))
```

You should see:

```text
None
```

This code runs, but the result may not be helpful yet.

`None` means "no value."

If you want a clearer backup value, give `get()` a default.

Fixed code:

```python
settings = {
    "theme": "light"
}

print(settings.get("font_size", "medium"))
```

You should see:

```text
medium
```

When a key might be missing, choose a default that makes sense for the program.

## Debug It

Read each broken program. Find the key problem, then fix the code.

### Debug 1: The Missing Email

The program should print the email if it exists. If it does not exist, it should print `"No email saved"`.

Broken code:

```python
user = {
    "name": "Asha",
    "city": "Chennai"
}

print(user["email"])
```

The problem:

```text
The key "email" is missing, but square brackets require the key to exist.
```

Fixed code:

```python
user = {
    "name": "Asha",
    "city": "Chennai"
}

print(user.get("email", "No email saved"))
```

You should see:

```text
No email saved
```

### Debug 2: The Wrong Brackets

The program should print the student's name.

Broken code:

```python
student = {
    "name": "Ben",
    "score": 8
}

print(student[0])
```

The problem:

```text
The code treats the dictionary like a list.
```

Fixed code:

```python
student = {
    "name": "Ben",
    "score": 8
}

print(student["name"])
```

You should see:

```text
Ben
```

### Debug 3: The Variable Key

The program should print `"practice"`.

Broken code:

```python
lesson = {
    "title": "Dictionaries",
    "topic": "practice"
}

topic = "title"

print(lesson[topic])
```

This code runs, but it prints the wrong value.

The problem:

```text
The variable topic contains "title", so lesson[topic] reads lesson["title"].
```

Fixed code:

```python
lesson = {
    "title": "Dictionaries",
    "topic": "practice"
}

print(lesson["topic"])
```

You should see:

```text
practice
```

### Debug 4: The Total Price

The program should print:

```text
Total: 30
```

Broken code:

```python
order = {
    "item": "pen pack",
    "price": 10,
    "quantity": 3
}

total = order["cost"] * order["quantity"]

print(f"Total: {total}")
```

The problem:

```text
The dictionary has a "price" key, not a "cost" key.
```

Fixed code:

```python
order = {
    "item": "pen pack",
    "price": 10,
    "quantity": 3
}

total = order["price"] * order["quantity"]

print(f"Total: {total}")
```

You should see:

```text
Total: 30
```

## Read the Docs

Today, look at Python's official documentation for dictionary types:

```text
https://docs.python.org/3/library/stdtypes.html#mapping-types-dict
```

You do not need to read the whole page.

Search for these pieces:

```text
d[key]
get(key[, default])
KeyError
```

The documentation often uses short names.

Read them like this:

```text
d means some dictionary.
key means the key you are looking for.
default means the backup value to return if the key is missing.
```

So this documentation idea:

```text
d[key]
```

matches code like:

```python
profile = {
    "name": "Asha",
    "city": "Chennai"
}

print(profile["name"])
```

You should see:

```text
Asha
```

And this documentation idea:

```text
get(key[, default])
```

matches code like:

```python
profile = {
    "name": "Asha",
    "city": "Chennai"
}

print(profile.get("email", "No email saved"))
```

You should see:

```text
No email saved
```

The square brackets are strict.

`get()` is more flexible.

Both are useful.

## Mini Challenge

Create a file named:

```text
day-44/profile_reader.py
```

Build a small profile reader.

Start with this dictionary:

```python
profile = {
    "name": "Ravi",
    "city": "Hyderabad",
    "daily_minutes": 25,
    "completed_lessons": 43
}
```

Your program should:

- print the learner's name
- print the learner's city
- print a sentence using `name` and `city`
- calculate the weekly practice time by multiplying `daily_minutes` by `7`
- print a sentence with the weekly practice time
- use `get()` to read `"email"` with the default `"No email saved"`
- print the email result

One possible version:

```python
profile = {
    "name": "Ravi",
    "city": "Hyderabad",
    "daily_minutes": 25,
    "completed_lessons": 43
}

name = profile["name"]
city = profile["city"]
weekly_minutes = profile["daily_minutes"] * 7
email = profile.get("email", "No email saved")

print(name)
print(city)
print(f"{name} studies from {city}.")
print(f"Weekly practice: {weekly_minutes} minutes")
print(f"Email: {email}")
```

You should see:

```text
Ravi
Hyderabad
Ravi studies from Hyderabad.
Weekly practice: 175 minutes
Email: No email saved
```

Try changing only the values in the starting dictionary.

Do not add new keys yet.

That keeps today's practice focused on reading.

## Real-World Use

Dictionaries are common when a program stores real-world records.

Example:

```python
product = {
    "name": "water bottle",
    "price": 15,
    "in_stock": True
}

print(product["name"])
print(product["price"])
print(product["in_stock"])
```

You should see:

```text
water bottle
15
True
```

A product has named facts.

Those facts are easier to read with keys than with positions.

You can also combine dictionary values into a useful message:

```python
product = {
    "name": "water bottle",
    "price": 15,
    "quantity": 2
}

total = product["price"] * product["quantity"]

print(f"{product['quantity']} x {product['name']} costs {total}.")
```

You should see:

```text
2 x water bottle costs 30.
```

This pattern appears in many programs:

```text
Read a value.
Use the value in text.
Use the value in a calculation.
Choose a default if a value might be missing.
```

You might see dictionaries used for:

- a user profile
- a shopping cart item
- a quiz question
- a weather report
- a settings screen
- a contact card

The exact data changes, but the reading pattern stays the same.

## Recap

A dictionary stores values behind keys.

You can read a value with square brackets:

```python
student = {
    "name": "Asha",
    "score": 9
}

print(student["score"])
```

You should see:

```text
9
```

Use square brackets when the key should exist.

If the key is missing, Python raises a `KeyError`.

You can read a value with `get()`:

```python
student = {
    "name": "Asha",
    "score": 9
}

print(student.get("grade", "Not graded yet"))
```

You should see:

```text
Not graded yet
```

Use `get()` when the key might be missing and you want a backup value.

The key must match exactly:

```text
city is not the same as City
score is not the same as scores
email is not the same as e-mail
```

Lists use indexes.

Dictionaries use keys.

## Lesson Checklist

Before moving on, check that you can:

- read a dictionary value with `dictionary["key"]`
- explain why missing keys cause `KeyError`
- use `get()` with a default value
- choose between square brackets and `get()`
- use dictionary values inside an f-string
- use numeric dictionary values in a calculation
- explain why `profile[0]` is usually wrong
- tell the difference between `profile["city"]` and `profile[city]`
- choose clear key names for simple data
- keep today's work focused on reading, not updating

## Exercises

### Exercise 1

Create this dictionary:

```python
movie = {
    "title": "Hidden Figures",
    "year": 2016,
    "rating": "PG"
}
```

Print each value using square brackets.

### Exercise 2

Use the same `movie` dictionary.

Print this sentence:

```text
Hidden Figures came out in 2016.
```

### Exercise 3

Create this dictionary:

```python
snack = {
    "name": "apple",
    "calories": 95,
    "count": 2
}
```

Calculate the total calories and print:

```text
Total calories: 190
```

### Exercise 4

Create this dictionary:

```python
contact = {
    "name": "Mina",
    "phone": "555-0101"
}
```

Use `get()` to read `"email"` with the default `"No email saved"`.

Print the result.

### Exercise 5

Predict the output, then run the code.

```python
settings = {
    "theme": "dark",
    "font_size": "large"
}

print(settings["theme"])
print(settings.get("language", "English"))
```

### Exercise 6

Fix the broken code.

Broken code:

```python
book = {
    "title": "Python Basics",
    "pages": 180
}

print(book["page"])
```

The goal is to print `180`.

### Exercise 7

Fix the broken code.

Broken code:

```python
profile = {
    "name": "Asha",
    "city": "Chennai"
}

print(profile[0])
```

The goal is to print the name.

### Exercise 8

Fix the broken code.

Broken code:

```python
profile = {
    "name": "Asha",
    "city": "Chennai"
}

city = "Delhi"

print(profile[city])
```

The goal is to print the saved city from the dictionary.

### Exercise 9

Create a dictionary named `lesson` with these keys:

```text
title
day
topic
minutes
```

Choose your own values.

Print a sentence that uses all four values.

### Exercise 10

Write a program that starts with this dictionary:

```python
order = {
    "item": "pencil",
    "price": 2,
    "quantity": 5
}
```

Print:

```text
5 pencils cost 10.
```

### Exercise 11

For each line, say whether it uses a string key or a variable key.

```text
profile["name"]
profile[field]
settings["theme"]
settings[selected_key]
```

Then write one sentence explaining the difference.

### Exercise 12

Choose clear keys for a dictionary that stores a person's:

```text
first name
last name
age
favorite color
daily step goal
```

Write the dictionary.

Then print two sentences using values from it.

## Tiny Win

You can now ask a dictionary for the exact value you need.

That is a small skill, but it unlocks a lot of real programs.

Once data has names, your code can read more like a sentence:

```text
print(profile["name"])
print(order["total"])
print(settings.get("language", "English"))
```

The key points are:

```text
Use the right key.
Spell it exactly.
Choose square brackets or get().
Use the value like any other Python value.
```

## Tomorrow

Tomorrow is:

```text
Day 45: Updating Dictionaries
```

Today you read values from dictionaries.

Tomorrow you will change dictionaries by adding new key-value pairs and replacing existing values.

That is why today's examples did not change the dictionaries themselves.

First read the data clearly.

Then learn how to update it safely.
