# Day 45: Updating Dictionaries

**Focus:** Adding, changing, and removing dictionary values  
**You will practice:** using key assignment, updating values from old values, deleting with `del`, removing with `pop()`, and avoiding common dictionary update mistakes  
**Estimated time:** 40-50 minutes

## Today's Goal

Today you will learn how to update a dictionary after it has already been created.

You have already seen that a dictionary stores values under keys:

```python
contact = {
    "name": "Mina",
    "email": "mina@example.com"
}

print(contact["email"])
```

You should see:

```text
mina@example.com
```

Today you will change dictionaries while the program is running.

By the end of this lesson, you should be able to:

- add a new key-value pair
- change the value for an existing key
- use assignment with dictionary keys
- update a value based on its old value
- remove a key-value pair with `del`
- remove a key-value pair with `pop()`
- check before deleting a key that might be missing
- recognize common dictionary update mistakes

The main idea is:

```text
dictionary[key] = value adds or changes one entry.
```

That one pattern is used in many real programs.

## The Big Idea

A dictionary can change after you create it.

Start with a contact:

```python
contact = {
    "name": "Mina",
    "email": "mina@example.com"
}

contact["phone"] = "555-0100"

print(contact)
```

You should see:

```text
{'name': 'Mina', 'email': 'mina@example.com', 'phone': '555-0100'}
```

This line added a new key-value pair:

```python
contact["phone"] = "555-0100"
```

The key `"phone"` did not exist yet, so Python created it.

The same pattern can change an existing value:

```python
contact = {
    "name": "Mina",
    "email": "old@example.com"
}

contact["email"] = "mina@example.com"

print(contact)
```

You should see:

```text
{'name': 'Mina', 'email': 'mina@example.com'}
```

This time, the key `"email"` already existed.

Python did not create a second email key. It replaced the old value with the new one.

So the same syntax can do two jobs:

```text
If the key is new, assignment adds it.
If the key already exists, assignment changes it.
```

That is useful, but it also means spelling matters.

## The Mental Model

Think of a dictionary as a group of labeled slots.

```text
name   -> Mina
email  -> mina@example.com
phone  -> 555-0100
```

The key is the label.

The value is what is stored under that label.

When you write:

```python
contact["email"] = "new@example.com"
```

Python looks for the `"email"` label.

If it finds it, Python replaces the value:

```text
email -> new@example.com
```

When you write:

```python
contact["city"] = "Pune"
```

Python looks for the `"city"` label.

If it does not find it, Python adds a new slot:

```text
city -> Pune
```

Removing an entry removes both the key and the value.

Code:

```python
contact = {
    "name": "Mina",
    "email": "mina@example.com",
    "phone": "555-0100"
}

del contact["phone"]

print(contact)
```

You should see:

```text
{'name': 'Mina', 'email': 'mina@example.com'}
```

After that, `"phone"` is no longer in the dictionary.

## Try It Yourself

Create a file named:

```text
day-45/update_dictionaries.py
```

Write each example slowly. Run the file after each step.

### Step 1: Add Contact Information

Code:

```python
contact = {
    "name": "Mina",
    "email": "mina@example.com"
}

contact["phone"] = "555-0100"

print(contact)
```

You should see:

```text
{'name': 'Mina', 'email': 'mina@example.com', 'phone': '555-0100'}
```

The key `"phone"` was new, so Python added it.

### Step 2: Change Existing Contact Information

Code:

```python
contact = {
    "name": "Mina",
    "email": "old@example.com",
    "phone": "555-0100"
}

contact["email"] = "mina@example.com"

print(contact)
```

You should see:

```text
{'name': 'Mina', 'email': 'mina@example.com', 'phone': '555-0100'}
```

The key `"email"` already existed, so Python changed its value.

### Step 3: Update A Score Based On The Old Score

You can read an old value, change it, and store the new value under the same key.

Code:

```python
game = {
    "player": "Ari",
    "score": 10
}

game["score"] = game["score"] + 5

print(game)
```

You should see:

```text
{'player': 'Ari', 'score': 15}
```

Read this line:

```python
game["score"] = game["score"] + 5
```

as:

```text
Take the old score.
Add 5.
Store the result back under "score".
```

You will see this pattern often.

### Step 4: Update Inventory

A dictionary can store product names and quantities.

Code:

```python
inventory = {
    "notebook": 12,
    "pen": 30,
    "eraser": 8
}

inventory["pen"] = inventory["pen"] - 2
inventory["pencil"] = 20

print(inventory)
```

You should see:

```text
{'notebook': 12, 'pen': 28, 'eraser': 8, 'pencil': 20}
```

The pen quantity changed.

The pencil entry was added.

### Step 5: Change A Product Price

Code:

```python
product = {
    "name": "Notebook",
    "price": 4.50,
    "in_stock": True
}

old_price = product["price"]
product["price"] = 5.00

print("Old price:", old_price)
print("New price:", product["price"])
```

You should see:

```text
Old price: 4.5
New price: 5.0
```

Saving the old value is useful when the program needs to compare before and after.

### Step 6: Change Settings

Settings are a natural fit for dictionaries because each setting has a name.

Code:

```python
settings = {
    "theme": "light",
    "notifications": True,
    "volume": 7
}

settings["theme"] = "dark"
settings["volume"] = settings["volume"] - 2
settings["language"] = "English"

print(settings)
```

You should see:

```text
{'theme': 'dark', 'notifications': True, 'volume': 5, 'language': 'English'}
```

This example changed two existing settings and added one new setting.

### Step 7: Delete With `del`

Use `del` when you want to remove a key-value pair and you do not need the removed value.

Code:

```python
settings = {
    "theme": "dark",
    "notifications": True,
    "volume": 5,
    "language": "English"
}

del settings["language"]

print(settings)
```

You should see:

```text
{'theme': 'dark', 'notifications': True, 'volume': 5}
```

The key `"language"` and its value were removed.

### Step 8: Remove With `pop()`

Use `pop()` when you want to remove a key and keep the value that was removed.

Code:

```python
contact = {
    "name": "Mina",
    "email": "mina@example.com",
    "phone": "555-0100"
}

removed_phone = contact.pop("phone")

print("Removed:", removed_phone)
print(contact)
```

You should see:

```text
Removed: 555-0100
{'name': 'Mina', 'email': 'mina@example.com'}
```

`pop("phone")` removes the `"phone"` entry and gives back the old phone number.

### Step 9: Check Before Deleting

Deleting a missing key causes an error.

If a key might be missing, check first.

Code:

```python
settings = {
    "theme": "dark",
    "notifications": True
}

if "volume" in settings:
    del settings["volume"]
else:
    print("No volume setting to delete.")

print(settings)
```

You should see:

```text
No volume setting to delete.
{'theme': 'dark', 'notifications': True}
```

This check keeps the program from crashing.

## Common Mistake

### Mistake 1: Misspelling A Key And Creating A New Entry

This code runs, but it does the wrong thing.

Broken code:

```python
contact = {
    "name": "Mina",
    "email": "mina@example.com"
}

contact["emial"] = "new@example.com"

print(contact)
```

You should see:

```text
{'name': 'Mina', 'email': 'mina@example.com', 'emial': 'new@example.com'}
```

The program did not update `"email"`.

It added a new key named `"emial"` because that is what the code asked for.

Fixed code:

```python
contact = {
    "name": "Mina",
    "email": "mina@example.com"
}

contact["email"] = "new@example.com"

print(contact)
```

You should see:

```text
{'name': 'Mina', 'email': 'new@example.com'}
```

Dictionary keys must match exactly.

### Mistake 2: Forgetting Quotes Around String Keys

Broken code:

```python
score = {
    "player": "Ari",
    "points": 10
}

score[points] = 15

print(score)
```

This is broken because Python reads `points` as a variable name.

No variable named `points` exists, so Python raises a `NameError`.

Fixed code:

```python
score = {
    "player": "Ari",
    "points": 10
}

score["points"] = 15

print(score)
```

You should see:

```text
{'player': 'Ari', 'points': 15}
```

String keys need quotes.

### Mistake 3: Trying To Use Dot Access

Broken code:

```python
product = {
    "name": "Notebook",
    "price": 4.50
}

product.price = 5.00

print(product)
```

This is broken because normal dictionaries do not use dot access for keys.

Use square brackets with the key.

Fixed code:

```python
product = {
    "name": "Notebook",
    "price": 4.50
}

product["price"] = 5.00

print(product)
```

You should see:

```text
{'name': 'Notebook', 'price': 5.0}
```

Dictionary keys are accessed with square brackets:

```python
product["price"]
```

not:

```python
product.price
```

### Mistake 4: Deleting A Missing Key

Broken code:

```python
settings = {
    "theme": "dark",
    "notifications": True
}

del settings["volume"]

print(settings)
```

This is broken because `"volume"` is not in the dictionary.

Python raises a `KeyError`.

Fixed code:

```python
settings = {
    "theme": "dark",
    "notifications": True
}

if "volume" in settings:
    del settings["volume"]
else:
    print("Volume was already missing.")

print(settings)
```

You should see:

```text
Volume was already missing.
{'theme': 'dark', 'notifications': True}
```

Check with `in` before deleting a key that might not exist.

You can also use `pop()` with a default value:

```python
settings = {
    "theme": "dark",
    "notifications": True
}

removed_volume = settings.pop("volume", None)

print("Removed:", removed_volume)
print(settings)
```

You should see:

```text
Removed: None
{'theme': 'dark', 'notifications': True}
```

The `None` value means there was no old value to remove.

## Debug It

Read each broken program. Find the dictionary update problem, then compare it with the fixed version.

### Debug 1: Contact Email

Goal:

```text
{'name': 'Mina', 'email': 'new@example.com'}
```

Broken code:

```python
contact = {
    "name": "Mina",
    "email": "old@example.com"
}

contact["email_address"] = "new@example.com"

print(contact)
```

The problem:

```text
The code adds "email_address" instead of updating "email".
```

Fixed code:

```python
contact = {
    "name": "Mina",
    "email": "old@example.com"
}

contact["email"] = "new@example.com"

print(contact)
```

You should see:

```text
{'name': 'Mina', 'email': 'new@example.com'}
```

### Debug 2: Product Price

Goal:

```text
Old price: 4.5
New price: 4.0
```

Broken code:

```python
product = {
    "name": "Notebook",
    "price": 4.50
}

old_price = product[price]
product.price = 4.00

print("Old price:", old_price)
print("New price:", product["price"])
```

There are two problems.

First, `"price"` is a string key, so it needs quotes.

Second, dictionaries do not update keys with dot access.

Fixed code:

```python
product = {
    "name": "Notebook",
    "price": 4.50
}

old_price = product["price"]
product["price"] = 4.00

print("Old price:", old_price)
print("New price:", product["price"])
```

You should see:

```text
Old price: 4.5
New price: 4.0
```

### Debug 3: Inventory Sale

Goal:

```text
{'notebook': 12, 'pen': 27, 'eraser': 8}
```

Broken code:

```python
inventory = {
    "notebook": 12,
    "pen": 30,
    "eraser": 8
}

inventory["pens"] = inventory["pen"] - 3

print(inventory)
```

This code runs, but it creates a new key named `"pens"`.

The goal is to update the existing `"pen"` quantity.

Fixed code:

```python
inventory = {
    "notebook": 12,
    "pen": 30,
    "eraser": 8
}

inventory["pen"] = inventory["pen"] - 3

print(inventory)
```

You should see:

```text
{'notebook': 12, 'pen': 27, 'eraser': 8}
```

### Debug 4: Removing A Setting

Goal:

```text
No setting removed.
{'theme': 'dark', 'notifications': True}
```

Broken code:

```python
settings = {
    "theme": "dark",
    "notifications": True
}

removed = settings.pop("volume")

print("Removed:", removed)
print(settings)
```

This is broken because `"volume"` is missing.

`pop("volume")` raises a `KeyError` when the key does not exist.

Fixed code:

```python
settings = {
    "theme": "dark",
    "notifications": True
}

removed = settings.pop("volume", None)

if removed is None:
    print("No setting removed.")
else:
    print("Removed:", removed)

print(settings)
```

You should see:

```text
No setting removed.
{'theme': 'dark', 'notifications': True}
```

When dictionary updates surprise you, ask:

- Did I spell the key exactly right?
- Did I put string keys in quotes?
- Am I using square brackets instead of dot access?
- Could this key be missing?
- Am I adding a new key or changing an existing key?

## Read the Docs

Today, look at Python's official documentation for dictionary types:

```text
https://docs.python.org/3/library/stdtypes.html#mapping-types-dict
```

You do not need to read the whole page.

Look for these ideas:

```text
d[key]
d[key] = value
del d[key]
key in d
d.pop(key)
d.pop(key, default)
```

The documentation often uses short names.

Read them like this:

```text
d means some dictionary.
key means the key you want.
value means the value you want to store.
```

So this documentation pattern:

```python
d[key] = value
```

matches code like:

```python
settings["theme"] = "dark"
```

And this pattern:

```python
d.pop(key, default)
```

matches code like:

```python
removed = settings.pop("volume", None)
```

Documentation can look compact. Your job is to connect the short version to code you already understand.

## Mini Challenge

Create a file named:

```text
day-45/product_update.py
```

Build a small product updater.

Start with this dictionary:

```python
product = {
    "name": "Water Bottle",
    "price": 12.00,
    "stock": 15,
    "featured": False
}
```

Your program should:

- print the original product
- change the price to `10.00`
- reduce the stock by `3`
- change `featured` to `True`
- add a new key named `"category"` with the value `"outdoor"`
- remove `"featured"` with `pop()` and save the removed value
- print the removed value
- print the final product

One possible solution:

```python
product = {
    "name": "Water Bottle",
    "price": 12.00,
    "stock": 15,
    "featured": False
}

print("Original:", product)

product["price"] = 10.00
product["stock"] = product["stock"] - 3
product["featured"] = True
product["category"] = "outdoor"

removed_featured = product.pop("featured")

print("Removed featured value:", removed_featured)
print("Final:", product)
```

You should see:

```text
Original: {'name': 'Water Bottle', 'price': 12.0, 'stock': 15, 'featured': False}
Removed featured value: True
Final: {'name': 'Water Bottle', 'price': 10.0, 'stock': 12, 'category': 'outdoor'}
```

After it works, change the starting stock and run the program again.

The final stock should still be 3 lower than the starting stock.

## Real-World Use

Dictionaries are used whenever a program keeps named pieces of information.

A contact book can update a phone number:

```python
contact = {
    "name": "Mina",
    "phone": "555-0100"
}

contact["phone"] = "555-0199"

print(contact)
```

You should see:

```text
{'name': 'Mina', 'phone': '555-0199'}
```

A game can update a score:

```python
game = {
    "player": "Ari",
    "score": 20
}

game["score"] = game["score"] + 10

print(game)
```

You should see:

```text
{'player': 'Ari', 'score': 30}
```

A store can update inventory:

```python
inventory = {
    "notebook": 12,
    "pen": 30
}

inventory["pen"] = inventory["pen"] - 1
inventory["marker"] = 6

print(inventory)
```

You should see:

```text
{'notebook': 12, 'pen': 29, 'marker': 6}
```

A product page can update a price:

```python
product = {
    "name": "Notebook",
    "price": 4.50
}

product["price"] = 4.00

print(product)
```

You should see:

```text
{'name': 'Notebook', 'price': 4.0}
```

A settings screen can change user choices:

```python
settings = {
    "theme": "light",
    "notifications": True
}

settings["theme"] = "dark"
settings["notifications"] = False

print(settings)
```

You should see:

```text
{'theme': 'dark', 'notifications': False}
```

In all of these examples, the dictionary keeps the same general shape while some values change.

That is what makes dictionaries useful for real data.

## Recap

Today you learned how to update dictionaries.

You practiced:

- adding a new key-value pair
- changing the value for an existing key
- using `dictionary[key] = value`
- updating a value based on the old value
- saving an old value before changing it
- deleting with `del`
- removing and saving a value with `pop()`
- checking whether a key exists before deleting it
- using `pop(key, default)` when a missing key is allowed
- avoiding misspelled keys, missing quotes, dot access, and missing-key deletion errors

The key pattern is:

```python
dictionary[key] = value
```

Read it as:

```text
Store this value under this key.
```

If the key exists, the value changes.

If the key does not exist, the key-value pair is added.

## Lesson Checklist

Before moving on, check that you can:

- add a new key-value pair to a dictionary
- change an existing value in a dictionary
- explain why the same assignment syntax can add or update
- update a number based on its old value
- save an old value before replacing it
- delete a key-value pair with `del`
- remove a key-value pair with `pop()`
- explain the difference between `del` and `pop()`
- check whether a key exists with `in`
- use `pop(key, default)` for a key that might be missing
- explain why misspelled keys can create unwanted entries
- explain why string keys need quotes
- explain why normal dictionaries do not use dot access

## Exercises

### Exercise 1

Predict the output.

```python
profile = {
    "name": "Sam",
    "city": "Delhi"
}

profile["city"] = "Mumbai"

print(profile)
```

Then run it.

### Exercise 2

Add a new key named `"phone"` to this dictionary:

```python
contact = {
    "name": "Iris",
    "email": "iris@example.com"
}
```

Use any phone number string you like.

Print the dictionary.

### Exercise 3

Change the score from `40` to `50`.

Start with:

```python
game = {
    "player": "Dev",
    "score": 40
}
```

Print the updated dictionary.

### Exercise 4

Increase the score by `10` using the old value.

Start with:

```python
game = {
    "player": "Dev",
    "score": 40
}
```

The code should still work if the starting score changes later.

### Exercise 5

Reduce the `"notebook"` inventory by `2`.

Start with:

```python
inventory = {
    "notebook": 12,
    "pen": 30
}
```

Print the final inventory.

### Exercise 6

Change the product price to `7.50`.

Start with:

```python
product = {
    "name": "Pen Set",
    "price": 8.00
}
```

Print only the new price.

### Exercise 7

Update these settings:

```python
settings = {
    "theme": "light",
    "notifications": True,
    "volume": 8
}
```

Your program should:

- change `"theme"` to `"dark"`
- change `"notifications"` to `False`
- lower `"volume"` by `3`
- print the final dictionary

### Exercise 8

Remove `"temporary"` from this dictionary with `del`:

```python
data = {
    "name": "Report",
    "temporary": True
}
```

Print the dictionary after deleting.

### Exercise 9

Use `pop()` to remove `"phone"` and save the removed value.

Start with:

```python
contact = {
    "name": "Iris",
    "phone": "555-0123"
}
```

Print:

```text
Removed phone: 555-0123
```

Then print the dictionary.

### Exercise 10

Fix the broken code.

Broken code:

```python
profile = {
    "name": "Sam",
    "email": "sam@example.com"
}

profile["emial"] = "new@example.com"

print(profile)
```

The goal is to change the existing email address.

### Exercise 11

Fix the broken code.

Broken code:

```python
settings = {
    "theme": "dark"
}

del settings["volume"]

print(settings)
```

The goal is to delete `"volume"` only if it exists.

### Exercise 12

Fix the broken code.

Broken code:

```python
product = {
    "name": "Notebook",
    "price": 4.50
}

product.price = 5.00

print(product)
```

The goal is to update the `"price"` key.

### Exercise 13

Write a small dictionary update program from scratch.

Create a dictionary named `account` with these keys:

```text
username
level
points
active
```

Then:

- increase `"level"` by `1`
- increase `"points"` by `25`
- change `"active"` to `False`
- add `"last_login"` with any date string
- print the final dictionary

### Exercise 14

Choose `del`, `pop()`, or assignment for each situation.

Situation:

```text
Change a user's email address.
```

Situation:

```text
Add a missing phone number.
```

Situation:

```text
Remove a temporary setting and ignore its old value.
```

Situation:

```text
Remove a coupon code and save the removed code.
```

Situation:

```text
Increase a product stock count by 10.
```

Write the Python operation you would use for each one.

## Tiny Win

You can now maintain named data.

A dictionary is no longer just something you read from. You can add information, correct old information, remove information, and update numbers as things happen.

That is a big part of writing programs that feel connected to real life.

## Tomorrow

Tomorrow is:

```text
Day 46: Looping Through Dictionaries
```

Today you updated one key at a time:

```python
inventory["pen"] = inventory["pen"] - 2
settings["theme"] = "dark"
```

Tomorrow you will visit many keys and values with a loop.

That will let you print, inspect, and process a whole dictionary without writing one line for every key.
