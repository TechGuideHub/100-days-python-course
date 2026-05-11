# Day 87: Dictionary Comprehensions

**Focus:** Creating dictionaries from loops in one clear expression  
**You will practice:** `{key: value for item in items}`, building lookup tables, transforming values, filtering key/value pairs, using `.items()`, and avoiding common syntax mistakes with colons, commas, braces, and brackets  
**Estimated time:** 50-65 minutes

## Today's Goal

Today you will learn how to build dictionaries with a compact pattern called a dictionary comprehension.

You already know that dictionaries connect keys to values:

```python
scores = {
    "Mina": 91,
    "Bo": 78,
    "Ava": 88,
}

print(scores["Mina"])
```

You should see:

```text
91
```

A dictionary comprehension lets you create a dictionary from another collection.

By the end of today, you should be able to:

- write a dictionary comprehension with `{key: value for item in items}`
- turn a list into a lookup table
- transform dictionary values while keeping the same keys
- filter which key/value pairs are kept
- use `.items()` when you need both keys and values
- spot common mistakes with `:`, `,`, `{}`, and `[]`
- prepare for Day 88, where you will start using classes to give related data a reusable shape

This is not about making code shorter at any cost.

It is about recognizing a common pattern:

```text
Start with many items.
Choose a key for each item.
Choose a value for each item.
Build a dictionary.
```

## The Big Idea

Here is a normal loop that builds a dictionary.

```python
names = ["Mina", "Bo", "Ava"]

lengths = {}

for name in names:
    lengths[name] = len(name)

print(lengths)
```

You should see:

```text
{'Mina': 4, 'Bo': 2, 'Ava': 3}
```

The loop says:

```text
For each name, use the name as the key and its length as the value.
```

A dictionary comprehension says the same thing in one expression:

```python
names = ["Mina", "Bo", "Ava"]

lengths = {name: len(name) for name in names}

print(lengths)
```

You should see:

```text
{'Mina': 4, 'Bo': 2, 'Ava': 3}
```

The pattern is:

```text
{key: value for item in items}
```

The colon matters.

In a dictionary, the colon separates the key from the value:

```text
key: value
```

That is why dictionary comprehensions use a colon too.

## The Mental Model

A dictionary comprehension has three main parts.

```text
{key_expression: value_expression for item in collection}
```

Read it like this:

```text
For each item in the collection,
make one dictionary entry,
using this key expression and this value expression.
```

For example:

```python
words = ["apple", "bee", "cat", "door"]

length_by_word = {word: len(word) for word in words}

print(length_by_word)
```

You should see:

```text
{'apple': 5, 'bee': 3, 'cat': 3, 'door': 4}
```

The key expression is:

```text
word
```

The value expression is:

```text
len(word)
```

The loop part is:

```text
for word in words
```

Dictionary comprehensions look similar to list comprehensions from Day 86, but the shape is different.

List comprehension:

```text
[value for item in items]
```

Dictionary comprehension:

```text
{key: value for item in items}
```

A list gives you values in order.

A dictionary gives you keys that can look up values.

### Building Lookup Tables

One of the best uses for dictionary comprehensions is building lookup tables.

A lookup table is a dictionary that lets you quickly find one piece of information from another piece of information.

Here is a list of student records:

```python
students = [
    {"id": "s100", "name": "Mina Patel", "score": 91},
    {"id": "s101", "name": "Bo Chen", "score": 78},
    {"id": "s102", "name": "Ava Singh", "score": 88},
]

names_by_id = {student["id"]: student["name"] for student in students}

print(names_by_id)
print(names_by_id["s102"])
```

You should see:

```text
{'s100': 'Mina Patel', 's101': 'Bo Chen', 's102': 'Ava Singh'}
Ava Singh
```

The key is each student's id.

The value is each student's name.

That makes this lookup fast and readable:

```text
names_by_id["s102"]
```

You can build a different lookup from the same data:

```python
students = [
    {"id": "s100", "name": "Mina Patel", "score": 91},
    {"id": "s101", "name": "Bo Chen", "score": 78},
    {"id": "s102", "name": "Ava Singh", "score": 88},
]

scores_by_id = {student["id"]: student["score"] for student in students}

print(scores_by_id)
```

You should see:

```text
{'s100': 91, 's101': 78, 's102': 88}
```

Same source list.

Different key/value choice.

That is the main decision in a dictionary comprehension:

```text
What should become the key?
What should become the value?
```

### Transforming Values

Sometimes you already have a dictionary, but you want a new dictionary with changed values.

Use `.items()` when you need both the key and the value.

```python
prices = {
    "notebook": 3.50,
    "pen": 1.25,
    "mug": 8.00,
}

sale_prices = {
    item: round(price * 0.90, 2)
    for item, price in prices.items()
}

print(sale_prices)
```

You should see:

```text
{'notebook': 3.15, 'pen': 1.12, 'mug': 7.2}
```

The keys stay the same:

```text
notebook
pen
mug
```

The values change:

```text
price * 0.90
```

Here is another transformation.

```python
scores = {
    "Mina": 91,
    "Bo": 78,
    "Ava": 88,
}

curved_scores = {
    name: min(score + 5, 100)
    for name, score in scores.items()
}

print(curved_scores)
```

You should see:

```text
{'Mina': 96, 'Bo': 83, 'Ava': 93}
```

The expression `min(score + 5, 100)` keeps the score from going above 100.

That is normal Python inside the value expression.

### Filtering Key/Value Pairs

You can add an `if` condition at the end.

```text
{key: value for item in items if condition}
```

The `if` decides whether that entry is included.

```python
inventory = {
    "pencils": 24,
    "markers": 0,
    "paper": 12,
    "clips": 0,
}

in_stock = {
    item: count
    for item, count in inventory.items()
    if count > 0
}

print(in_stock)
```

You should see:

```text
{'pencils': 24, 'paper': 12}
```

Only the pairs with a count greater than zero were kept.

You can also filter while building a lookup table from a list.

```python
students = [
    {"id": "s100", "name": "Mina Patel", "score": 91},
    {"id": "s101", "name": "Bo Chen", "score": 78},
    {"id": "s102", "name": "Ava Singh", "score": 88},
]

passing_scores = {
    student["id"]: student["score"]
    for student in students
    if student["score"] >= 80
}

print(passing_scores)
```

You should see:

```text
{'s100': 91, 's102': 88}
```

The `if` goes after the `for` part.

That is one of the small grammar details that becomes natural with practice.

### Iterating With `.items()`

When you loop over a dictionary directly, Python gives you the keys.

```python
prices = {
    "notebook": 3.50,
    "pen": 1.25,
    "mug": 8.00,
}

for item in prices:
    print(item)
```

You should see:

```text
notebook
pen
mug
```

That is useful when you only need keys.

But a dictionary comprehension often needs both keys and values.

Use `.items()` for that:

```python
prices = {
    "notebook": 3.50,
    "pen": 1.25,
    "mug": 8.00,
}

for item, price in prices.items():
    print(item, price)
```

You should see:

```text
notebook 3.5
pen 1.25
mug 8.0
```

Now turn that loop into a dictionary comprehension:

```python
prices = {
    "notebook": 3.50,
    "pen": 1.25,
    "mug": 8.00,
}

price_labels = {
    item: f"${price:.2f}"
    for item, price in prices.items()
}

print(price_labels)
```

You should see:

```text
{'notebook': '$3.50', 'pen': '$1.25', 'mug': '$8.00'}
```

That is a common real program task:

```text
Keep the same keys.
Format or clean the values.
Return a new dictionary.
```

## Try It Yourself

Create a folder named:

```text
day-87
```

Inside it, create this file:

```text
day-87/dictionary_comprehensions.py
```

### Step 1: Start With Product Records

Add this data:

```python
products = [
    {"sku": "A100", "name": "notebook", "price": 3.50},
    {"sku": "B200", "name": "pen", "price": 1.25},
    {"sku": "C300", "name": "mug", "price": 8.00},
]

print(products)
```

You should see the list of dictionaries printed.

Each product is one dictionary.

The whole collection is a list.

### Step 2: Build A Price Lookup

Replace the `print(products)` line with this:

```python
products = [
    {"sku": "A100", "name": "notebook", "price": 3.50},
    {"sku": "B200", "name": "pen", "price": 1.25},
    {"sku": "C300", "name": "mug", "price": 8.00},
]

prices_by_sku = {
    product["sku"]: product["price"]
    for product in products
}

print(prices_by_sku)
print(prices_by_sku["B200"])
```

You should see:

```text
{'A100': 3.5, 'B200': 1.25, 'C300': 8.0}
1.25
```

You now have a dictionary that can answer:

```text
What is the price for this SKU?
```

### Step 3: Build A Name Lookup

Now build a different lookup from the same product list.

```python
products = [
    {"sku": "A100", "name": "notebook", "price": 3.50},
    {"sku": "B200", "name": "pen", "price": 1.25},
    {"sku": "C300", "name": "mug", "price": 8.00},
]

names_by_sku = {
    product["sku"]: product["name"].title()
    for product in products
}

print(names_by_sku)
```

You should see:

```text
{'A100': 'Notebook', 'B200': 'Pen', 'C300': 'Mug'}
```

The key is still the SKU.

The value is now the product name, cleaned up with `.title()`.

### Step 4: Filter While Building

Build a dictionary of only the lower-priced products.

```python
products = [
    {"sku": "A100", "name": "notebook", "price": 3.50},
    {"sku": "B200", "name": "pen", "price": 1.25},
    {"sku": "C300", "name": "mug", "price": 8.00},
]

budget_products = {
    product["sku"]: product["name"]
    for product in products
    if product["price"] < 5
}

print(budget_products)
```

You should see:

```text
{'A100': 'notebook', 'B200': 'pen'}
```

The mug is not included because its price is 8.00.

### Step 5: Transform An Existing Dictionary

Add this separate example:

```python
stock = {
    "notebook": 12,
    "pen": 48,
    "mug": 6,
}

stock_labels = {
    item: f"{count} in stock"
    for item, count in stock.items()
}

print(stock_labels)
```

You should see:

```text
{'notebook': '12 in stock', 'pen': '48 in stock', 'mug': '6 in stock'}
```

This time the source collection was already a dictionary.

That is why `.items()` was the right tool.

## Common Mistake

The most common mistake is using a comma where a colon belongs.

This is not a dictionary comprehension:

```text
lengths = {name, len(name) for name in names}
```

Use a colon between the key and the value:

```python
names = ["Mina", "Bo", "Ava"]

lengths = {name: len(name) for name in names}

print(lengths)
```

You should see:

```text
{'Mina': 4, 'Bo': 2, 'Ava': 3}
```

Another mistake is using square brackets with a key/value pair.

This is not valid dictionary-comprehension syntax:

```text
lengths = [name: len(name) for name in names]
```

Square brackets make a list comprehension.

Curly braces plus a colon make a dictionary comprehension:

```text
{key: value for item in items}
```

A third mistake is adding a comma before `for`.

This is not the shape Python expects:

```text
lengths = {name: len(name), for name in names}
```

The correct shape is:

```python
names = ["Mina", "Bo", "Ava"]

lengths = {name: len(name) for name in names}

print(lengths)
```

You should see:

```text
{'Mina': 4, 'Bo': 2, 'Ava': 3}
```

One more detail: curly braces without a colon can create a set comprehension.

```python
names = ["Mina", "Bo", "Ava"]

unique_names = {name for name in names}

print(sorted(unique_names))
```

You should see the names from the set, sorted into a list:

```text
['Ava', 'Bo', 'Mina']
```

A set is useful, but it is not a dictionary.

If you want key/value pairs, look for the colon.

## Debug It

You are given this code:

```text
prices = {
    "notebook": 3.50,
    "pen": 1.25,
    "mug": 8.00,
}

sale_prices = {
    item: round(price * 0.90, 2)
    for item in prices
}

print(sale_prices)
```

The program fails because `price` does not exist.

When you loop over a dictionary directly, you get keys only.

This part:

```text
for item in prices
```

gives you:

```text
notebook
pen
mug
```

It does not give you the prices.

Use `.items()` to get both pieces:

```python
prices = {
    "notebook": 3.50,
    "pen": 1.25,
    "mug": 8.00,
}

sale_prices = {
    item: round(price * 0.90, 2)
    for item, price in prices.items()
}

print(sale_prices)
```

You should see:

```text
{'notebook': 3.15, 'pen': 1.12, 'mug': 7.2}
```

When a dictionary comprehension fails, ask:

- Did I use `{}` instead of `[]`?
- Did I put a colon between the key and value?
- Am I looping over the right collection?
- Do I need `.items()`?
- Is the variable name on the left also available on the right?

Most dictionary-comprehension bugs come from one of those five questions.

## Read the Docs

Today the most useful dictionary tool is `.items()`.

Try this small check:

```python
profile = {
    "name": "Mina",
    "city": "Pune",
    "role": "analyst",
}

print(list(profile.keys()))
print(list(profile.values()))
print(list(profile.items()))
```

You should see:

```text
['name', 'city', 'role']
['Mina', 'Pune', 'analyst']
[('name', 'Mina'), ('city', 'Pune'), ('role', 'analyst')]
```

Notice that `.items()` gives pairs.

Each pair has:

```text
key, value
```

That is why this loop works:

```python
profile = {
    "name": "Mina",
    "city": "Pune",
    "role": "analyst",
}

for key, value in profile.items():
    print(key, "->", value)
```

You should see:

```text
name -> Mina
city -> Pune
role -> analyst
```

In the Python documentation or the interactive help system, look up:

```text
dict.items
dict.keys
dict.values
```

Do not try to memorize every dictionary method.

Focus on the shape of the data each method gives back.

## Mini Challenge

Build a contact lookup.

Start with this data:

```python
contacts = [
    {"name": "Mina Patel", "email": "mina@example.com", "active": True},
    {"name": "Bo Chen", "email": "bo@example.com", "active": False},
    {"name": "Ava Singh", "email": "ava@example.com", "active": True},
]

active_emails = {
    contact["name"]: contact["email"]
    for contact in contacts
    if contact["active"]
}

print(active_emails)
```

You should see:

```text
{'Mina Patel': 'mina@example.com', 'Ava Singh': 'ava@example.com'}
```

Then change the comprehension so the keys are lowercase names:

```python
contacts = [
    {"name": "Mina Patel", "email": "mina@example.com", "active": True},
    {"name": "Bo Chen", "email": "bo@example.com", "active": False},
    {"name": "Ava Singh", "email": "ava@example.com", "active": True},
]

active_emails = {
    contact["name"].lower(): contact["email"]
    for contact in contacts
    if contact["active"]
}

print(active_emails)
```

You should see:

```text
{'mina patel': 'mina@example.com', 'ava singh': 'ava@example.com'}
```

That version is useful when you want a simple lookup key that is easy to type.

## Real-World Use

Dictionary comprehensions show up whenever a program needs to reshape data.

You might use them to:

- build a product lookup from a list of product records
- turn usernames into user profiles
- format raw numbers for display
- keep only active accounts
- reverse a small dictionary when the values are unique
- prepare data before saving it as JSON

For example, many programs receive data as a list of records.

That is good for showing all records in order.

But when you need to find one record by an id, a dictionary is often easier.

```python
tasks = [
    {"id": 1, "title": "Write outline", "done": True},
    {"id": 2, "title": "Draft lesson", "done": False},
    {"id": 3, "title": "Review examples", "done": False},
]

tasks_by_id = {task["id"]: task for task in tasks}

print(tasks_by_id[2])
```

You should see:

```text
{'id': 2, 'title': 'Draft lesson', 'done': False}
```

This example points toward Day 88.

Right now, each task is a dictionary.

Tomorrow, you will learn how a class can describe one kind of thing, such as a task, contact, product, or bank account.

## Recap

Today you learned that:

- a dictionary comprehension creates a dictionary from another collection
- the basic shape is `{key: value for item in items}`
- the colon separates the key expression from the value expression
- `.items()` gives you key/value pairs from an existing dictionary
- an `if` at the end filters which entries are included
- dictionary comprehensions are useful for lookup tables and data cleanup
- duplicate keys do not create multiple entries

That last point is worth seeing once.

```python
pairs = [
    ("pen", 1.25),
    ("notebook", 3.50),
    ("pen", 1.50),
]

prices = {name: price for name, price in pairs}

print(prices)
```

You should see:

```text
{'pen': 1.5, 'notebook': 3.5}
```

The second `"pen"` value replaced the first one.

Dictionary keys must be unique.

## Lesson Checklist

Before moving on, make sure you can:

- write `{key: value for item in items}`
- choose a useful key expression
- choose a useful value expression
- build a lookup table from a list of dictionaries
- transform values from an existing dictionary
- filter entries with `if`
- use `.items()` when you need both key and value
- explain why `{item for item in items}` is a set comprehension
- fix mistakes with colons, commas, braces, and brackets
- explain why duplicate keys overwrite earlier entries
- describe how dictionaries of related data lead into classes

## Exercises

### Exercise 1: Name Length Lookup

Create this file:

```text
day-87/name_lengths.py
```

Write a program that:

- stores four names in a list
- builds a dictionary where each key is a name
- stores the length of each name as the value
- prints the dictionary

Starter code:

```python
names = ["Mina", "Bo", "Ava", "Ravi"]

lengths = {name: len(name) for name in names}

print(lengths)
```

### Exercise 2: Score Labels

Create this file:

```text
day-87/score_labels.py
```

Start with this dictionary:

```python
scores = {
    "Mina": 91,
    "Bo": 78,
    "Ava": 88,
}

labels = {
    name: f"{score} points"
    for name, score in scores.items()
}

print(labels)
```

Then change the value expression so scores of 80 or higher say `"pass"` and lower scores say `"review"`.

Hint:

```text
"pass" if score >= 80 else "review"
```

### Exercise 3: Filter Inventory

Create this file:

```text
day-87/filter_inventory.py
```

Write a program that keeps only items with a count greater than zero.

Starter code:

```python
inventory = {
    "pencils": 24,
    "markers": 0,
    "paper": 12,
    "clips": 0,
}

available = {
    item: count
    for item, count in inventory.items()
    if count > 0
}

print(available)
```

### Exercise 4: Reverse A Small Dictionary

Create this file:

```text
day-87/reverse_states.py
```

Start with this dictionary:

```python
states = {
    "NY": "New York",
    "CA": "California",
    "TX": "Texas",
}

codes_by_state = {
    state: code
    for code, state in states.items()
}

print(codes_by_state)
```

This works well because each state name is unique.

Add one more state code and run the program again.

### Exercise 5: Build An Email Lookup

Create this file:

```text
day-87/email_lookup.py
```

Use this data:

```python
users = [
    {"username": "mina", "email": "mina@example.com"},
    {"username": "bo", "email": "bo@example.com"},
    {"username": "ava", "email": "ava@example.com"},
]

emails_by_username = {
    user["username"]: user["email"]
    for user in users
}

print(emails_by_username)
print(emails_by_username["ava"])
```

Then add one more user.

### Exercise 6: Fix The Shape

These snippets are trying to build a dictionary.

Rewrite each one correctly.

```text
lengths = [name: len(name) for name in names]
```

```text
lengths = {name, len(name) for name in names}
```

```text
lengths = {name: len(name), for name in names}
```

The corrected version should have this shape:

```text
{key: value for item in items}
```

### Exercise 7: Watch Duplicate Keys

Create this file:

```text
day-87/duplicate_keys.py
```

Run this program:

```python
pairs = [
    ("pen", 1.25),
    ("notebook", 3.50),
    ("pen", 1.50),
]

prices = {name: price for name, price in pairs}

print(prices)
```

Answer this question in a comment:

```text
Why is there only one pen key?
```

### Exercise 8: Prepare For Classes

Create this file:

```text
day-87/class_preview.py
```

Start with this list:

```python
contacts = [
    {"name": "Mina Patel", "email": "mina@example.com", "city": "Pune"},
    {"name": "Bo Chen", "email": "bo@example.com", "city": "Toronto"},
    {"name": "Ava Singh", "email": "ava@example.com", "city": "Delhi"},
]

contacts_by_email = {
    contact["email"]: contact
    for contact in contacts
}

print(contacts_by_email["bo@example.com"])
```

Then write three comments at the bottom of the file:

```text
# One contact has a name.
# One contact has an email.
# One contact has a city.
```

Those comments describe the shape of one contact.

That idea is exactly where classes begin.

## Tiny Win

You can now build dictionaries from lists and reshape existing dictionaries without writing a full loop every time.

That is a practical skill.

When you see data shaped like a list of records, you can decide whether a lookup table would make the next step easier.

You are not just storing data now.

You are choosing a shape for it.

## Tomorrow

Tomorrow you will start Day 88: Introduction to Classes.

Classes help you describe one kind of thing in your program.

Today you used dictionaries like this:

```python
contact = {
    "name": "Mina Patel",
    "email": "mina@example.com",
    "city": "Pune",
}

print(contact["name"])
```

You should see:

```text
Mina Patel
```

Tomorrow you will learn another way to model that same idea:

```text
A contact has a name.
A contact has an email.
A contact has a city.
```

That is the bridge from dictionaries to classes.
