# Day 43: Dictionaries

**Focus:** Storing related information with keys and values  
**You will practice:** creating dictionaries, recognizing keys and values, printing dictionaries, reading their shape, and choosing dictionaries for real-world data  
**Estimated time:** 40-50 minutes

## Today's Goal

Today you will learn about dictionaries.

A dictionary stores related information in key-value pairs.

You have already used collections that store values by position:

```python
profile = ["Mina", 12, "Pune"]
```

That list works, but you have to remember what each position means:

```text
index 0 -> name
index 1 -> age
index 2 -> city
```

A dictionary lets you write those labels directly:

```python
profile = {
    "name": "Mina",
    "age": 12,
    "city": "Pune"
}
```

Now the shape of the data is easier to read.

By the end of this lesson, you should be able to:

- create a dictionary with curly braces
- explain what keys and values are
- recognize the `key: value` pattern
- print a dictionary
- print its keys and values
- use dictionaries for profiles, products, contacts, game characters, and weather summaries
- explain why dictionaries are useful for real-world data

The main idea is:

```text
A dictionary stores values with labels.
```

Tomorrow you will practice reading dictionary values in more detail. Today is about understanding the shape.

## The Big Idea

A dictionary is made of pairs.

Each pair has a key and a value.

Code:

```python
profile = {
    "name": "Mina",
    "age": 12,
    "city": "Pune"
}

print(profile)
```

You should see:

```text
{'name': 'Mina', 'age': 12, 'city': 'Pune'}
```

Python may print strings with single quotes even if you typed double quotes. That is normal.

Read this dictionary one pair at a time:

```python
profile = {
    "name": "Mina",
    "age": 12,
    "city": "Pune"
}
```

Like this:

```text
The key "name" has the value "Mina".
The key "age" has the value 12.
The key "city" has the value "Pune".
```

The colon connects each key to its value:

```text
"name": "Mina"
```

The comma separates one pair from the next:

```text
"name": "Mina",
"age": 12,
```

The curly braces hold the whole dictionary:

```text
{
    key: value,
    key: value,
    key: value
}
```

The keys are usually strings:

```python
product = {
    "name": "Notebook",
    "price": 3.5,
    "in_stock": True
}
```

The values can be different types:

```text
"Notebook" is a string.
3.5 is a number.
True is a Boolean.
```

That is one reason dictionaries are so useful. A real thing often has several different kinds of information attached to it.

## The Mental Model

Think of a dictionary as a labeled record.

A list says:

```text
Here are some values in order.
```

A dictionary says:

```text
Here is a thing, and each piece of information has a label.
```

Compare these two versions.

Code:

```python
contact_list = ["Sam", "555-0104", "sam@example.com"]

print(contact_list)
```

You should see:

```text
['Sam', '555-0104', 'sam@example.com']
```

This is a list. It stores the values, but the labels live only in your memory.

Now use a dictionary.

Code:

```python
contact = {
    "name": "Sam",
    "phone": "555-0104",
    "email": "sam@example.com"
}

print(contact)
```

You should see:

```text
{'name': 'Sam', 'phone': '555-0104', 'email': 'sam@example.com'}
```

This version carries its own labels.

That helps you read the code later:

```text
"name" tells you what "Sam" means.
"phone" tells you what "555-0104" means.
"email" tells you what "sam@example.com" means.
```

You can also ask a dictionary for its keys and values.

Code:

```python
product = {
    "name": "Water bottle",
    "price": 12.99,
    "in_stock": True
}

print("Keys:", list(product.keys()))
print("Values:", list(product.values()))
```

You should see:

```text
Keys: ['name', 'price', 'in_stock']
Values: ['Water bottle', 12.99, True]
```

The keys are the labels.

The values are the information stored under those labels.

For today, that is enough. Tomorrow you will spend more time using a key to read one specific value.

## Try It Yourself

Create a file named:

```text
day-43/dictionaries_practice.py
```

You will create a few small dictionaries and print them.

### Step 1: Create A Profile

Code:

```python
profile = {
    "name": "Mina",
    "age": 12,
    "city": "Pune"
}

print(profile)
print("Keys:", list(profile.keys()))
print("Values:", list(profile.values()))
```

You should see:

```text
{'name': 'Mina', 'age': 12, 'city': 'Pune'}
Keys: ['name', 'age', 'city']
Values: ['Mina', 12, 'Pune']
```

This dictionary describes one person.

The keys are:

```text
name
age
city
```

The values are:

```text
Mina
12
Pune
```

### Step 2: Create A Product

Code:

```python
product = {
    "name": "Notebook",
    "price": 3.5,
    "in_stock": True
}

print(product)
print("Product keys:", list(product.keys()))
```

You should see:

```text
{'name': 'Notebook', 'price': 3.5, 'in_stock': True}
Product keys: ['name', 'price', 'in_stock']
```

This is the kind of shape a shop program might use.

It keeps related product information together:

```text
name
price
whether it is in stock
```

### Step 3: Create A Contact

Code:

```python
contact = {
    "name": "Sam",
    "phone": "555-0104",
    "email": "sam@example.com"
}

print(contact)
print("Contact values:", list(contact.values()))
```

You should see:

```text
{'name': 'Sam', 'phone': '555-0104', 'email': 'sam@example.com'}
Contact values: ['Sam', '555-0104', 'sam@example.com']
```

This is a small record for one contact.

Later in the course, dictionaries like this will help you build a contact book.

### Step 4: Create A Game Character

Code:

```python
character = {
    "name": "Nia",
    "level": 4,
    "health": 80,
    "has_key": False
}

print(character)
print("Character keys:", list(character.keys()))
```

You should see:

```text
{'name': 'Nia', 'level': 4, 'health': 80, 'has_key': False}
Character keys: ['name', 'level', 'health', 'has_key']
```

This dictionary describes one game character.

It can store text, numbers, and Boolean values together.

### Step 5: Create A Weather Summary

Code:

```python
weather = {
    "city": "Pune",
    "temperature_c": 31,
    "condition": "sunny",
    "rain_expected": False
}

print(weather)
print("Weather keys:", list(weather.keys()))
print("Weather values:", list(weather.values()))
```

You should see:

```text
{'city': 'Pune', 'temperature_c': 31, 'condition': 'sunny', 'rain_expected': False}
Weather keys: ['city', 'temperature_c', 'condition', 'rain_expected']
Weather values: ['Pune', 31, 'sunny', False]
```

This is close to how real programs think about data:

```text
one city
one temperature
one condition
one rain flag
```

Each value has a name.

That is the power of a dictionary.

## Common Mistake

### Mistake 1: Using `=` Instead Of `:`

Broken code:

```python
profile = {
    "name" = "Mina",
    "age" = 12
}
```

This is broken because dictionary pairs use colons, not equal signs.

Fixed code:

```python
profile = {
    "name": "Mina",
    "age": 12
}

print(profile)
```

You should see:

```text
{'name': 'Mina', 'age': 12}
```

Use this shape:

```text
key: value
```

### Mistake 2: Forgetting Quotes Around String Keys

Broken code:

```python
profile = {
    name: "Mina",
    age: 12
}

print(profile)
```

This is broken because `name` and `age` are being treated as variable names.

The program needs string keys.

Fixed code:

```python
profile = {
    "name": "Mina",
    "age": 12
}

print(profile)
```

You should see:

```text
{'name': 'Mina', 'age': 12}
```

Most beginner dictionaries use string keys because the keys are labels.

### Mistake 3: Forgetting Quotes Around String Values

Broken code:

```python
weather = {
    "city": Pune,
    "condition": sunny
}

print(weather)
```

This is broken because `Pune` and `sunny` are being treated as variable names.

The program needs string values.

Fixed code:

```python
weather = {
    "city": "Pune",
    "condition": "sunny"
}

print(weather)
```

You should see:

```text
{'city': 'Pune', 'condition': 'sunny'}
```

Use quotes for text.

Do not use quotes for numbers or Booleans:

```python
weather = {
    "temperature_c": 31,
    "rain_expected": False
}

print(weather)
```

You should see:

```text
{'temperature_c': 31, 'rain_expected': False}
```

### Mistake 4: Reusing The Same Key By Accident

Code:

```python
contact = {
    "name": "Sam",
    "phone": "555-0104",
    "phone": "555-0199"
}

print(contact)
```

You should see:

```text
{'name': 'Sam', 'phone': '555-0199'}
```

This code runs, but it loses the first phone number.

A dictionary key should usually appear once.

If you need two different phone numbers, use two different keys:

```python
contact = {
    "name": "Sam",
    "home_phone": "555-0104",
    "work_phone": "555-0199"
}

print(contact)
```

You should see:

```text
{'name': 'Sam', 'home_phone': '555-0104', 'work_phone': '555-0199'}
```

The labels should make the difference clear.

## Debug It

Read each broken program. Find the dictionary mistake, then fix it.

### Debug 1: Profile Shape

The program should create and print a profile dictionary.

Broken code:

```python
profile = {
    "name" = "Mina",
    "age" = 12,
    "city" = "Pune"
}

print(profile)
```

The problem:

```text
The code uses equal signs inside the dictionary.
```

Fixed code:

```python
profile = {
    "name": "Mina",
    "age": 12,
    "city": "Pune"
}

print(profile)
```

You should see:

```text
{'name': 'Mina', 'age': 12, 'city': 'Pune'}
```

### Debug 2: Weather Text

The program should create a weather summary.

Broken code:

```python
weather = {
    "city": "Pune",
    "temperature_c": 31,
    "condition": sunny
}

print(weather)
```

The problem:

```text
sunny is text, so it needs quotes.
```

Fixed code:

```python
weather = {
    "city": "Pune",
    "temperature_c": 31,
    "condition": "sunny"
}

print(weather)
```

You should see:

```text
{'city': 'Pune', 'temperature_c': 31, 'condition': 'sunny'}
```

### Debug 3: Two Phone Numbers

The program should keep both phone numbers.

Broken code:

```python
contact = {
    "name": "Sam",
    "phone": "555-0104",
    "phone": "555-0199"
}

print(contact)
```

The problem:

```text
The same key appears twice, so the first phone number is replaced.
```

Fixed code:

```python
contact = {
    "name": "Sam",
    "home_phone": "555-0104",
    "work_phone": "555-0199"
}

print(contact)
```

You should see:

```text
{'name': 'Sam', 'home_phone': '555-0104', 'work_phone': '555-0199'}
```

When two values mean different things, give them different keys.

## Read the Docs

Find Python's official documentation for dictionaries:

```text
https://docs.python.org/3/library/stdtypes.html#mapping-types-dict
```

You do not need to read the whole page today.

Look for these ideas:

```text
dict
key: value
len(d)
key in d
d.keys()
d.values()
```

Documentation often uses short names.

Read them like this:

```text
d means some dictionary.
key means one key in that dictionary.
d.keys() means get the dictionary's keys.
d.values() means get the dictionary's values.
```

You may also see this pattern:

```python
profile = {"name": "Mina", "age": 12}

print(len(profile))
print("name" in profile)
print(list(profile.keys()))
print(list(profile.values()))
```

You should see:

```text
2
True
['name', 'age']
['Mina', 12]
```

The line `"name" in profile` checks whether `"name"` is a key.

That is a useful detail:

```text
For dictionaries, `in` checks keys.
```

Tomorrow you will use keys to read values more directly.

## Mini Challenge

Create a file named:

```text
day-43/weather_summary.py
```

Build a small weather summary dictionary.

Start with this information:

```text
city: Pune
temperature_c: 31
condition: sunny
rain_expected: False
```

Your program should:

- create a dictionary named `weather`
- print the whole dictionary
- print the keys as a list
- print the values as a list
- print the number of key-value pairs
- check whether `"temperature_c"` is one of the keys

One possible version:

```python
weather = {
    "city": "Pune",
    "temperature_c": 31,
    "condition": "sunny",
    "rain_expected": False
}

print("Weather:", weather)
print("Keys:", list(weather.keys()))
print("Values:", list(weather.values()))
print("Pair count:", len(weather))
print("Has temperature:", "temperature_c" in weather)
```

You should see:

```text
Weather: {'city': 'Pune', 'temperature_c': 31, 'condition': 'sunny', 'rain_expected': False}
Keys: ['city', 'temperature_c', 'condition', 'rain_expected']
Values: ['Pune', 31, 'sunny', False]
Pair count: 4
Has temperature: True
```

After it works, make a second dictionary named `evening_weather` with different values.

Print both dictionaries.

Do not worry about reading individual values yet. That is tomorrow's focus.

## Real-World Use

Dictionaries are everywhere in real programs because real data usually has labels.

A user profile might look like this:

```python
profile = {
    "username": "mina12",
    "display_name": "Mina",
    "is_active": True
}

print(profile)
```

You should see:

```text
{'username': 'mina12', 'display_name': 'Mina', 'is_active': True}
```

A product record might look like this:

```python
product = {
    "name": "Notebook",
    "price": 3.5,
    "category": "school"
}

print(product)
```

You should see:

```text
{'name': 'Notebook', 'price': 3.5, 'category': 'school'}
```

A contact might look like this:

```python
contact = {
    "name": "Sam",
    "email": "sam@example.com",
    "phone": "555-0104"
}

print(contact)
```

You should see:

```text
{'name': 'Sam', 'email': 'sam@example.com', 'phone': '555-0104'}
```

A game character might look like this:

```python
character = {
    "name": "Nia",
    "level": 4,
    "health": 80,
    "has_key": False
}

print(character)
```

You should see:

```text
{'name': 'Nia', 'level': 4, 'health': 80, 'has_key': False}
```

A weather summary might look like this:

```python
weather = {
    "city": "Pune",
    "temperature_c": 31,
    "condition": "sunny"
}

print(weather)
```

You should see:

```text
{'city': 'Pune', 'temperature_c': 31, 'condition': 'sunny'}
```

In each case, a dictionary is useful because the data is not just a pile of values.

It is a small description of something:

```text
one user
one product
one contact
one game character
one weather report
```

Each piece has a name, so a dictionary fits.

## Recap

Today you learned that:

- a dictionary stores key-value pairs
- dictionaries use curly braces
- each pair uses a colon between the key and the value
- commas separate the pairs
- keys are usually strings
- values can be strings, numbers, Booleans, and other data
- printing a dictionary shows the whole record
- `dict_name.keys()` gives you the keys
- `dict_name.values()` gives you the values
- `list(dict_name.keys())` and `list(dict_name.values())` make those results easier to print
- `len(dict_name)` counts key-value pairs
- `key in dict_name` checks whether a key exists
- a dictionary is a good choice when values need labels

The basic shape is:

```text
thing = {
    "label": value,
    "another_label": another_value
}
```

Read it as:

```text
This is one thing described by named pieces of information.
```

## Lesson Checklist

Before moving on, check that you can:

- create a dictionary with at least three key-value pairs
- explain what a key is
- explain what a value is
- point to the colon between a key and a value
- point to the commas between pairs
- print a whole dictionary
- print dictionary keys with `list(dict_name.keys())`
- print dictionary values with `list(dict_name.values())`
- use `len()` to count key-value pairs
- explain why `"name" in profile` checks for a key
- choose a dictionary for a profile, product, contact, character, or weather summary
- fix a dictionary that uses `=` instead of `:`
- fix string keys or string values that are missing quotes

## Exercises

### Exercise 1

Create a dictionary named `profile`.

It should store:

```text
name: Asha
age: 13
city: Kochi
```

Print the whole dictionary.

### Exercise 2

Create a dictionary named `product`.

It should store:

```text
name: Pencil
price: 0.5
in_stock: True
```

Print the whole dictionary.

Then print its keys as a list.

### Exercise 3

Create a dictionary named `contact`.

It should store:

```text
name: Dev
phone: 555-0120
email: dev@example.com
```

Print its values as a list.

### Exercise 4

Create a dictionary named `character`.

It should store:

```text
name: Kai
level: 2
health: 95
has_key: False
```

Print the whole dictionary.

Then print the number of key-value pairs.

### Exercise 5

Create a dictionary named `weather`.

It should store:

```text
city: Kochi
temperature_c: 29
condition: rainy
rain_expected: True
```

Print the dictionary, its keys, and its values.

### Exercise 6

Predict the output.

```python
profile = {
    "name": "Mina",
    "age": 12
}

print(len(profile))
print("name" in profile)
print("city" in profile)
```

Then run it.

### Exercise 7

Fix the broken code.

Broken code:

```python
product = {
    "name" = "Notebook",
    "price" = 3.5
}

print(product)
```

The goal is to create a product dictionary.

### Exercise 8

Fix the broken code.

Broken code:

```python
contact = {
    name: "Sam",
    phone: "555-0104"
}

print(contact)
```

The goal is to use string keys.

### Exercise 9

Fix the broken code.

Broken code:

```python
weather = {
    "city": "Pune",
    "condition": sunny
}

print(weather)
```

The goal is to store `"sunny"` as text.

### Exercise 10

This code runs, but it loses information.

```python
contact = {
    "name": "Sam",
    "phone": "555-0104",
    "phone": "555-0199"
}

print(contact)
```

Rewrite it so the two phone numbers have different keys.

### Exercise 11

For each situation, write `list`, `tuple`, `set`, or `dictionary`.

```text
A changing shopping cart.
A fixed screen size like width and height.
A group of unique tags.
A product with a name, price, and category.
A weather report with city, temperature, and condition.
A game character with health, level, and inventory status.
```

Then write one sentence explaining each choice.

### Exercise 12

Create three dictionaries:

- `profile`
- `product`
- `weather`

Each dictionary should have at least three key-value pairs.

For each dictionary, print:

- the whole dictionary
- the keys as a list
- the values as a list
- the number of key-value pairs

## Tiny Win

You can now store related information with names attached.

That is an important step toward real data.

A dictionary lets your code say:

```text
This value is a name.
This value is a price.
This value is a city.
This value is a condition.
```

That is easier to understand than remembering positions in a list.

## Tomorrow

Tomorrow is:

```text
Day 44: Reading Dictionary Values
```

Today you learned the dictionary shape:

```python
profile = {
    "name": "Mina",
    "age": 12
}
```

Tomorrow you will practice using keys to read specific values:

```python
profile = {
    "name": "Mina",
    "age": 12
}

print(profile["name"])
```

The goal will be to get comfortable asking a dictionary for exactly the information you need.
