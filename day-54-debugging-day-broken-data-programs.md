# Day 54: Debugging Day: Broken Data Programs

**Focus:** Debugging data programs that use lists, dictionaries, nested data, and loops  
**You will practice:** reading errors, inspecting data shape, fixing missing keys, repairing loop targets, using the right index or key, handling inconsistent records, avoiding accidental new keys, removing data safely, and reading nested data one layer at a time  
**Estimated time:** 60-75 minutes

## Today's Goal

Today is a debugging day.

You are not learning a large new syntax idea. You are practicing how to stay calm when a data program breaks.

The programs today use:

- lists
- dictionaries
- lists of dictionaries
- dictionaries with lists inside
- nested dictionaries
- loops

These are the same tools you will use tomorrow in the Contact Book mini project.

By the end of this lesson, you should be able to:

- read a `KeyError`, `TypeError`, or surprising output without panicking
- inspect the shape of a list or dictionary
- print one small piece of data instead of guessing
- fix one layer of nested data at a time
- notice when a loop is visiting the wrong thing
- avoid adding a new dictionary key by accident
- remove list items safely
- delete dictionary keys safely
- repair small programs that store contact-style records

The main idea is:

```text
Most broken data programs are shape mismatches.
```

The code expects one shape.

The data has a different shape.

Debugging means finding the mismatch.

## The Big Idea

A data program works when the code and the data agree.

Example:

```python
contacts = [
    {"name": "Mina", "phone": "555-0104"},
    {"name": "Sam", "phone": "555-0199"}
]

for contact in contacts:
    print(contact["name"] + ": " + contact["phone"])
```

You should see:

```text
Mina: 555-0104
Sam: 555-0199
```

This works because the shape is clear:

```text
contacts is a list.
Each item in contacts is a dictionary.
Each dictionary has "name" and "phone" keys.
```

Now imagine one record changes.

Broken code:

```python
contacts = [
    {"name": "Mina", "phone": "555-0104"},
    {"name": "Sam", "phone_number": "555-0199"}
]

for contact in contacts:
    print(contact["name"] + ": " + contact["phone"])
```

The second dictionary has `"phone_number"`, but the loop expects `"phone"`.

That is not a mysterious Python problem.

It is a shape problem.

When a data program breaks, use this routine:

```text
1. Read the error.
2. Find the line Python complained about.
3. Inspect the data shape near that line.
4. Print one small piece.
5. Fix one layer.
6. Rerun the program.
```

Do not fix five things at once.

Fix one thing, rerun, then continue.

## The Mental Model

Think of debugging as asking one question again and again:

```text
What am I holding right now?
```

You might be holding:

```text
a list
a dictionary
a string
a number
a Boolean
None
```

Each one uses a different kind of access.

```text
List       -> use an index or a loop
Dictionary -> use a key
String     -> use string tools
Number     -> use arithmetic
Boolean    -> use it in a condition
None       -> handle the missing value
```

Example:

```python
contact = {
    "name": "Mina",
    "phone": "555-0104",
    "address": {
        "city": "Pune",
        "country": "India"
    },
    "tags": ["friend", "python"]
}

print(type(contact))
print(list(contact.keys()))

address = contact["address"]
print(type(address))
print(list(address.keys()))

tags = contact["tags"]
print(type(tags))
print(len(tags))
print(tags[0])
```

You should see:

```text
<class 'dict'>
['name', 'phone', 'address', 'tags']
<class 'dict'>
['city', 'country']
<class 'list'>
2
friend
```

This is the work of debugging:

```text
Print the kind of thing you have.
Print its keys if it is a dictionary.
Print its length and one item if it is a list.
```

Once you know the shape, the next step is usually smaller than it felt.

## Try It Yourself

Create a file named:

```text
day-54/debug_data_programs.py
```

Use it as a small debugging lab.

Start with a working contact report.

Code:

```python
contacts = [
    {
        "name": "Mina",
        "phone": "555-0104",
        "email": "mina@example.com"
    },
    {
        "name": "Sam",
        "phone": "555-0199"
    }
]

for contact in contacts:
    name = contact["name"]
    phone = contact["phone"]
    email = contact.get("email", "No email saved")

    print(name + ": " + phone + " | " + email)
```

You should see:

```text
Mina: 555-0104 | mina@example.com
Sam: 555-0199 | No email saved
```

The second contact does not have an email address.

That is not always an error. In a contact book, email may be optional.

`get()` lets the program use a backup value.

Now inspect the data before printing it.

Code:

```python
contacts = [
    {
        "name": "Mina",
        "phone": "555-0104",
        "email": "mina@example.com"
    },
    {
        "name": "Sam",
        "phone": "555-0199"
    }
]

print(type(contacts))
print(len(contacts))

first_contact = contacts[0]
print(type(first_contact))
print(list(first_contact.keys()))

second_contact = contacts[1]
print(list(second_contact.keys()))
```

You should see:

```text
<class 'list'>
2
<class 'dict'>
['name', 'phone', 'email']
['name', 'phone']
```

That output explains why direct access to `contact["email"]` would fail for Sam.

Try this:

```python
contact = {
    "name": "Iris",
    "phone": "555-0130",
    "notes": ["met at class", "prefers text"]
}

notes = contact["notes"]

print(type(notes))
print(len(notes))
print(notes[0])
```

You should see:

```text
<class 'list'>
2
met at class
```

When a dictionary value is a list, you still use list tools after you reach that value.

## Common Mistake

Data bugs often come from small mismatches.

The good news is that the same debugging routine works for most of them.

### Mistake 1: Missing Keys

Broken code:

```python
contact = {
    "name": "Sam",
    "phone": "555-0199"
}

print(contact["email"])
```

This raises a `KeyError` because `"email"` is not in the dictionary.

Read the error like this:

```text
Python tried to read the key "email".
The current dictionary does not have that key.
```

Fixed code:

```python
contact = {
    "name": "Sam",
    "phone": "555-0199"
}

email = contact.get("email", "No email saved")

print(email)
```

You should see:

```text
No email saved
```

Use `get()` when a missing key is allowed.

Use direct access when the key should always exist.

### Mistake 2: Wrong Loop Target

Broken code:

```python
contacts = [
    {"name": "Mina", "phone": "555-0104"},
    {"name": "Sam", "phone": "555-0199"}
]

for contact in contacts[0]:
    print(contact["name"])
```

This loops through the first dictionary's keys.

On the first loop, `contact` is the string `"name"`, not a contact dictionary.

Fixed code:

```python
contacts = [
    {"name": "Mina", "phone": "555-0104"},
    {"name": "Sam", "phone": "555-0199"}
]

for contact in contacts:
    print(contact["name"])
```

You should see:

```text
Mina
Sam
```

When a loop feels strange, print the loop variable:

```python
contacts = [
    {"name": "Mina", "phone": "555-0104"},
    {"name": "Sam", "phone": "555-0199"}
]

for contact in contacts:
    print(contact)
```

You should see:

```text
{'name': 'Mina', 'phone': '555-0104'}
{'name': 'Sam', 'phone': '555-0199'}
```

That shows the loop gives you one dictionary at a time.

### Mistake 3: Wrong Index Or Key

Broken code:

```python
contacts = [
    {"name": "Mina", "phone": "555-0104"},
    {"name": "Sam", "phone": "555-0199"}
]

print(contacts["name"])
```

`contacts` is a list.

A list needs an index or a loop before you can use a dictionary key.

Fixed code:

```python
contacts = [
    {"name": "Mina", "phone": "555-0104"},
    {"name": "Sam", "phone": "555-0199"}
]

first_contact = contacts[0]

print(first_contact["name"])
```

You should see:

```text
Mina
```

Read the access one step at a time:

```text
contacts[0] gets the first dictionary.
first_contact["name"] gets the name inside that dictionary.
```

### Mistake 4: Inconsistent Records

Broken code:

```python
contacts = [
    {"name": "Mina", "phone": "555-0104"},
    {"name": "Sam", "phone_number": "555-0199"},
    {"name": "Iris", "phone": "555-0130"}
]

for contact in contacts:
    print(contact["name"] + ": " + contact["phone"])
```

The second record uses `"phone_number"` instead of `"phone"`.

The loop expects every contact to have the same basic shape.

Fixed code:

```python
contacts = [
    {"name": "Mina", "phone": "555-0104"},
    {"name": "Sam", "phone": "555-0199"},
    {"name": "Iris", "phone": "555-0130"}
]

for contact in contacts:
    print(contact["name"] + ": " + contact["phone"])
```

You should see:

```text
Mina: 555-0104
Sam: 555-0199
Iris: 555-0130
```

Consistent records make loops simple.

If a value is optional, keep the key optional on purpose and use `get()`.

If a value is required, use the same key in every record.

### Mistake 5: Accidental New Dictionary Key

Broken code:

```python
contact = {
    "name": "Mina",
    "email": "old@example.com"
}

contact["emial"] = "mina@example.com"

print(contact["email"])
print(contact)
```

This code does not update `"email"`.

It adds a new key named `"emial"`.

Python does not know that `"emial"` is a typo.

Fixed code:

```python
contact = {
    "name": "Mina",
    "email": "old@example.com"
}

contact["email"] = "mina@example.com"

print(contact["email"])
print(contact)
```

You should see:

```text
mina@example.com
{'name': 'Mina', 'email': 'mina@example.com'}
```

When an update seems ignored, print the whole dictionary.

Look for a new key that should not be there.

### Mistake 6: Unsafe Remove Or Delete

Broken code:

```python
names = ["Mina", "Sam", "Mina", "Iris"]

for name in names:
    if name == "Mina":
        names.remove(name)

print(names)
```

This changes the list while the loop is using it.

That can skip items and make the result hard to trust.

Fixed code:

```python
names = ["Mina", "Sam", "Mina", "Iris"]

kept_names = []

for name in names:
    if name != "Mina":
        kept_names.append(name)

names = kept_names

print(names)
```

You should see:

```text
['Sam', 'Iris']
```

Build a new list when you want to remove several items.

For dictionaries, check before deleting.

Broken code:

```python
contact = {
    "name": "Sam",
    "phone": "555-0199"
}

del contact["email"]

print(contact)
```

This raises a `KeyError` because `"email"` is already missing.

Fixed code:

```python
contact = {
    "name": "Sam",
    "phone": "555-0199"
}

if "email" in contact:
    del contact["email"]

print(contact)
```

You should see:

```text
{'name': 'Sam', 'phone': '555-0199'}
```

The `in` check asks whether the key exists before deleting it.

### Mistake 7: Nested Access Errors

Broken code:

```python
contact = {
    "name": "Mina",
    "address": {
        "city": "Pune",
        "country": "India"
    }
}

print(contact["city"])
```

`"city"` is not directly inside `contact`.

It is inside `contact["address"]`.

Fixed code:

```python
contact = {
    "name": "Mina",
    "address": {
        "city": "Pune",
        "country": "India"
    }
}

address = contact["address"]

print(address["city"])
```

You should see:

```text
Pune
```

Splitting the line helps:

```text
contact is a dictionary.
contact["address"] is another dictionary.
address["city"] is the city string.
```

## Debug It

Read each broken program slowly.

Use the routine:

```text
Read the error.
Inspect the data shape.
Print small pieces.
Fix one layer at a time.
Rerun.
```

### Debug 1: Missing Email

Goal:

```text
Mina: mina@example.com
Sam: No email saved
```

Broken code:

```python
contacts = [
    {"name": "Mina", "email": "mina@example.com"},
    {"name": "Sam"}
]

for contact in contacts:
    print(contact["name"] + ": " + contact["email"])
```

The problem:

```text
The second contact does not have an "email" key.
```

Inspect first:

```python
contacts = [
    {"name": "Mina", "email": "mina@example.com"},
    {"name": "Sam"}
]

for contact in contacts:
    print(contact["name"], list(contact.keys()))
```

You should see:

```text
Mina ['name', 'email']
Sam ['name']
```

Fixed code:

```python
contacts = [
    {"name": "Mina", "email": "mina@example.com"},
    {"name": "Sam"}
]

for contact in contacts:
    email = contact.get("email", "No email saved")
    print(contact["name"] + ": " + email)
```

You should see:

```text
Mina: mina@example.com
Sam: No email saved
```

### Debug 2: Wrong Loop Target

Goal:

```text
Mina
Sam
Iris
```

Broken code:

```python
contact_book = {
    "contacts": [
        {"name": "Mina", "phone": "555-0104"},
        {"name": "Sam", "phone": "555-0199"},
        {"name": "Iris", "phone": "555-0130"}
    ]
}

for contact in contact_book:
    print(contact["name"])
```

The problem:

```text
Looping through contact_book gives dictionary keys.
The contact dictionaries are inside contact_book["contacts"].
```

Fixed code:

```python
contact_book = {
    "contacts": [
        {"name": "Mina", "phone": "555-0104"},
        {"name": "Sam", "phone": "555-0199"},
        {"name": "Iris", "phone": "555-0130"}
    ]
}

for contact in contact_book["contacts"]:
    print(contact["name"])
```

You should see:

```text
Mina
Sam
Iris
```

### Debug 3: Wrong Key In A Nested List

Goal:

```text
First note: call after 5
```

Broken code:

```python
contact = {
    "name": "Mina",
    "notes": [
        {"text": "call after 5", "important": True},
        {"text": "send address", "important": False}
    ]
}

first_note = contact["notes"][0]

print("First note:", first_note["message"])
```

The problem:

```text
Each note dictionary uses the key "text", not "message".
```

Fixed code:

```python
contact = {
    "name": "Mina",
    "notes": [
        {"text": "call after 5", "important": True},
        {"text": "send address", "important": False}
    ]
}

first_note = contact["notes"][0]

print("First note:", first_note["text"])
```

You should see:

```text
First note: call after 5
```

### Debug 4: Inconsistent Contact Records

Goal:

```text
Mina: 555-0104
Sam: 555-0199
Iris: 555-0130
```

Broken code:

```python
contacts = [
    {"name": "Mina", "phone": "555-0104"},
    {"full_name": "Sam", "phone": "555-0199"},
    {"name": "Iris", "phone": "555-0130"}
]

for contact in contacts:
    print(contact["name"] + ": " + contact["phone"])
```

The problem:

```text
The second record uses "full_name" while the loop expects "name".
```

Fixed code:

```python
contacts = [
    {"name": "Mina", "phone": "555-0104"},
    {"name": "Sam", "phone": "555-0199"},
    {"name": "Iris", "phone": "555-0130"}
]

for contact in contacts:
    print(contact["name"] + ": " + contact["phone"])
```

You should see:

```text
Mina: 555-0104
Sam: 555-0199
Iris: 555-0130
```

### Debug 5: Accidental New Key

Goal:

```text
Mina: 555-0200
```

Broken code:

```python
contact = {
    "name": "Mina",
    "phone": "555-0104"
}

contact["phone_number"] = "555-0200"

print(contact["name"] + ": " + contact["phone"])
```

The problem:

```text
The program adds "phone_number" instead of updating "phone".
```

Fixed code:

```python
contact = {
    "name": "Mina",
    "phone": "555-0104"
}

contact["phone"] = "555-0200"

print(contact["name"] + ": " + contact["phone"])
```

You should see:

```text
Mina: 555-0200
```

### Debug 6: Unsafe Remove

Goal:

```text
['Sam', 'Iris']
```

Broken code:

```python
contacts = [
    {"name": "Mina", "active": False},
    {"name": "Sam", "active": True},
    {"name": "Mina", "active": False},
    {"name": "Iris", "active": True}
]

for contact in contacts:
    if contact["active"] == False:
        contacts.remove(contact)

names = []

for contact in contacts:
    names.append(contact["name"])

print(names)
```

The problem:

```text
The program removes items from contacts while looping through contacts.
```

Fixed code:

```python
contacts = [
    {"name": "Mina", "active": False},
    {"name": "Sam", "active": True},
    {"name": "Mina", "active": False},
    {"name": "Iris", "active": True}
]

active_contacts = []

for contact in contacts:
    if contact["active"] == True:
        active_contacts.append(contact)

names = []

for contact in active_contacts:
    names.append(contact["name"])

print(names)
```

You should see:

```text
['Sam', 'Iris']
```

### Debug 7: Nested Access Error

Goal:

```text
City: Pune
```

Broken code:

```python
contact = {
    "name": "Mina",
    "details": {
        "address": {
            "city": "Pune",
            "country": "India"
        }
    }
}

print("City:", contact["address"]["city"])
```

The problem:

```text
"address" is inside contact["details"], not directly inside contact.
```

Fixed code:

```python
contact = {
    "name": "Mina",
    "details": {
        "address": {
            "city": "Pune",
            "country": "India"
        }
    }
}

details = contact["details"]
address = details["address"]

print("City:", address["city"])
```

You should see:

```text
City: Pune
```

## Read the Docs

Today, revisit the Python documentation for dictionaries:

```text
https://docs.python.org/3/library/stdtypes.html#mapping-types-dict
```

Look for these tools:

```text
d[key]
d[key] = value
key in d
d.get(key, default)
d.keys()
d.items()
```

Also revisit list methods:

```text
https://docs.python.org/3/tutorial/datastructures.html#more-on-lists
```

Look for:

```text
append
remove
pop
```

When reading docs, connect the names to your own data:

```text
d means some dictionary.
key means the key you want.
default means a backup value.
```

Try this:

```python
contact = {
    "name": "Mina",
    "phone": "555-0104",
    "tags": ["friend"]
}

print("email" in contact)
print(contact.get("email", "No email saved"))
print(list(contact.keys()))

contact["tags"].append("python")

print(contact["tags"])
```

You should see:

```text
False
No email saved
['name', 'phone', 'tags']
['friend', 'python']
```

The dictionary gives you the list at `contact["tags"]`.

Then `.append()` changes that list.

## Mini Challenge

Create a file named:

```text
day-54/contact_debug_lab.py
```

Start with this broken program.

Broken code:

```python
contacts = [
    {
        "name": "Mina",
        "phone": "555-0104",
        "email": "mina@example.com",
        "tags": ["friend", "python"]
    },
    {
        "name": "Sam",
        "phone_number": "555-0199",
        "tags": []
    },
    {
        "full_name": "Iris",
        "phone": "555-0130",
        "email": "iris@example.com",
        "tags": ["school"]
    }
]

for contact in contacts:
    print(contact["name"] + ": " + contact["phone"])
    print("Email:", contact["email"])
    print("First tag:", contact["tags"][0])
```

Your job:

```text
1. Run the program and read the first error.
2. Print each contact's keys.
3. Make the required keys consistent.
4. Use get() for optional email.
5. Do not assume every contact has a first tag.
6. Print a clean contact report.
```

One possible final report is:

```text
Mina: 555-0104
Email: mina@example.com
First tag: friend

Sam: 555-0199
Email: No email saved
First tag: No tags

Iris: 555-0130
Email: iris@example.com
First tag: school
```

After the report works, add this search:

```text
Find the contact named Sam and print the phone number.
```

Then add this safe remove:

```text
Build a new list that keeps every contact except Mina.
Print the remaining contact names.
```

This challenge prepares you for tomorrow because a contact book is mostly careful data shape work.

## Real-World Use

Data programs break in ordinary ways.

A contact book may have:

- a missing email address
- a phone number stored under the wrong key
- contacts with inconsistent keys
- a search loop that looks at the wrong collection
- a remove feature that skips contacts
- nested notes or addresses that need one-layer-at-a-time access

The same thing happens in larger programs.

An app might receive user data from a form.

A website might receive data from another service.

A file might contain old records from an earlier version of a program.

The programmer's job is not to memorize every possible mistake.

The job is to inspect the data calmly:

```text
What shape did I expect?
What shape did I receive?
Where are they different?
```

That is the habit you practiced today.

## Recap

Today you debugged broken data programs.

You practiced:

- reading error messages before changing code
- finding the line that failed
- checking whether the current value is a list or dictionary
- printing dictionary keys
- printing list lengths and one item
- fixing missing keys
- choosing the correct loop target
- using the correct index or key
- making records consistent
- avoiding accidental new dictionary keys
- removing list items safely
- deleting dictionary keys safely
- reading nested data one layer at a time

Use this small routine when a data program breaks:

```text
Read the error.
Inspect the data shape.
Print small pieces.
Fix one layer.
Rerun.
```

If the program runs but prints the wrong thing, the same routine still works.

Print the loop variable.

Print the whole dictionary.

Check whether the value you changed is the value you later read.

## Lesson Checklist

Before moving on, check that you can:

- explain what a `KeyError` usually means
- print `list(dictionary.keys())`
- print `type(value)` while debugging
- use `get()` for an optional key
- tell when a loop is visiting keys instead of records
- use an index before reading a dictionary inside a list
- fix a list of dictionaries with inconsistent keys
- spot an accidental new key after a typo
- build a new list instead of removing from the list you are looping through
- check whether a key exists before deleting it
- split nested access into smaller variables
- rerun after each small fix

## Exercises

### Exercise 1

Fix the missing key.

Broken code:

```python
contact = {
    "name": "Dev",
    "phone": "555-0120"
}

print(contact["email"])
```

The goal is:

```text
No email saved
```

### Exercise 2

Fix the wrong loop target.

Broken code:

```python
contact_book = {
    "contacts": [
        {"name": "Mina"},
        {"name": "Sam"}
    ]
}

for contact in contact_book:
    print(contact["name"])
```

The goal is:

```text
Mina
Sam
```

### Exercise 3

Fix the wrong index or key.

Broken code:

```python
contacts = [
    {"name": "Mina", "phone": "555-0104"},
    {"name": "Sam", "phone": "555-0199"}
]

print(contacts["phone"])
```

The goal is to print Sam's phone number.

### Exercise 4

Make the records consistent.

Broken code:

```python
contacts = [
    {"name": "Mina", "phone": "555-0104"},
    {"name": "Sam", "number": "555-0199"}
]

for contact in contacts:
    print(contact["name"] + ": " + contact["phone"])
```

The goal is:

```text
Mina: 555-0104
Sam: 555-0199
```

### Exercise 5

Fix the accidental new key.

Broken code:

```python
contact = {
    "name": "Iris",
    "phone": "555-0130"
}

contact["phones"] = "555-0140"

print(contact["phone"])
```

The goal is:

```text
555-0140
```

### Exercise 6

Remove inactive contacts safely.

Start with:

```python
contacts = [
    {"name": "Mina", "active": False},
    {"name": "Sam", "active": True},
    {"name": "Iris", "active": True}
]
```

Build a new list named `active_contacts`.

Print:

```text
Sam
Iris
```

### Exercise 7

Delete an optional key safely.

Start with:

```python
contact = {
    "name": "Mina",
    "phone": "555-0104",
    "email": "mina@example.com"
}
```

If `"email"` exists, delete it.

Print the final dictionary.

### Exercise 8

Fix the nested access.

Broken code:

```python
contact = {
    "name": "Mina",
    "address": {
        "city": "Pune",
        "country": "India"
    }
}

print(contact["city"])
```

The goal is:

```text
Pune
```

### Exercise 9

Debug the notes list.

Broken code:

```python
contact = {
    "name": "Sam",
    "notes": [
        {"text": "prefers morning calls"},
        {"text": "send reminder"}
    ]
}

for note in contact:
    print(note["text"])
```

The goal is:

```text
prefers morning calls
send reminder
```

### Exercise 10

Add debug prints before fixing the code.

Broken code:

```python
order = {
    "customer": {
        "name": "Mina"
    },
    "items": [
        {"name": "notebook", "price": 5}
    ]
}

print(order["name"])
```

Before fixing it, print:

```text
type(order)
list(order.keys())
type(order["customer"])
list(order["customer"].keys())
```

Then fix the program so it prints:

```text
Mina
```

### Exercise 11

Find the bug that does not crash.

Broken code:

```python
contact = {
    "name": "Mina",
    "favorite": False
}

contact["favorites"] = True

if contact["favorite"]:
    print("Favorite contact")
else:
    print("Regular contact")
```

The goal is:

```text
Favorite contact
```

### Exercise 12

Write a short debugging checklist in your own words.

Include these ideas:

```text
read the error
print the type
print keys or length
fix one layer
rerun
```

### Exercise 13

Repair this contact search.

Broken code:

```python
contacts = [
    {"name": "Mina", "phone": "555-0104"},
    {"name": "Sam", "phone": "555-0199"},
    {"name": "Iris", "phone": "555-0130"}
]

search_name = "Sam"

for contact in contacts[0]:
    if contact["name"] == search_name:
        print(contact["phone"])
```

The goal is:

```text
555-0199
```

### Exercise 14

Repair this tag counter.

Broken code:

```python
contact = {
    "name": "Mina",
    "tags": ["friend", "python", "school"]
}

print(len(contact["tag"]))
```

The goal is:

```text
3
```

### Exercise 15

Build a tiny contact report from scratch.

Use a list of three contact dictionaries.

Each contact should have:

```text
name
phone
```

At least one contact should also have:

```text
email
```

Print each contact like this:

```text
Name: phone | email or No email saved
```

Use `get()` for the email.

## Tiny Win

You practiced treating bugs as information.

An error message is not a verdict.

It is a clue about one line, one value, or one missing key.

When you can slow down and inspect the data shape, broken programs become much less mysterious.

That is a real step toward building programs you can trust.

## Tomorrow

Tomorrow is:

```text
Day 55: Mini Project: Contact Book
```

You will use lists of dictionaries to store contacts.

You will search, add, update, display, and maybe remove contacts.

Today's debugging practice matters because contact books are full of data-shape decisions:

```text
What keys does every contact need?
Which keys are optional?
What does one loop step give me?
How do I update an existing contact without creating the wrong key?
How do I remove a contact safely?
```

Bring today's routine with you:

```text
Read the error.
Inspect the data shape.
Print small pieces.
Fix one layer at a time.
Rerun.
```
