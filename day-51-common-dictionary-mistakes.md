# Day 51: Common Dictionary Mistakes

**Focus:** Finding and fixing common dictionary and data modeling mistakes  
**You will practice:** reading error messages, checking keys, using `get()`, inspecting nested data, and repairing broken dictionary programs  
**Estimated time:** 45-60 minutes

## Today's Goal

Today you will practice debugging dictionary mistakes.

You have already learned how to create dictionaries, read values, update values, loop through dictionaries, and work with larger data shapes.

Now the goal is to slow down and notice what usually goes wrong.

By the end of this lesson, you should be able to:

- recognize a `KeyError`
- spot misspelled keys
- remember quotes around string keys
- avoid dot access with normal dictionaries
- tell when you need an index and when you need a key
- notice inconsistent keys across records
- update the correct nested value
- avoid assuming a key exists
- debug dictionary data one layer at a time

The main idea is:

```text
Most dictionary bugs are shape bugs.
```

When a dictionary program breaks, ask:

```text
What kind of data am I holding right now?
What keys does it have?
Am I reading the correct layer?
```

Tomorrow is a practice day for data modeling. Today gives you the debugging habits that make that practice calmer.

## The Big Idea

A dictionary is easy to use when the key exists and the shape is simple.

Code:

```python
student = {
    "name": "Maya",
    "city": "Pune",
    "level": "beginner"
}

print(student["name"])
print(student["city"])
```

You should see:

```text
Maya
Pune
```

This works because the keys match exactly:

```text
name
city
level
```

But dictionary programs often fail when one of these things is wrong:

- the key is misspelled
- the key is missing
- the string key was written without quotes
- the code uses dot access instead of square brackets
- the code treats a list like a dictionary
- the code treats a dictionary like a list
- different records use different key names
- the code updates the wrong layer of nested data

Here is a small data shape:

Code:

```python
student = {
    "name": "Maya",
    "scores": [88, 92, 95],
    "profile": {
        "city": "Pune",
        "active": True
    }
}

print(type(student))
print(list(student.keys()))
print(type(student["scores"]))
print(type(student["profile"]))
print(list(student["profile"].keys()))
```

You should see:

```text
<class 'dict'>
['name', 'scores', 'profile']
<class 'list'>
<class 'dict'>
['city', 'active']
```

That is one of the best debugging moves:

```text
Print the shape before guessing.
```

The shape tells you what kind of access makes sense.

If the current value is a dictionary, use a key:

```python
student["profile"]["city"]
```

If the current value is a list, use an index or a loop:

```python
student["scores"][0]
```

## The Mental Model

Think of dictionary debugging as standing at one layer of data.

At each layer, ask:

```text
Am I holding a dictionary, a list, or a single value?
```

Example:

```python
club = {
    "name": "Python Club",
    "members": [
        {
            "name": "Asha",
            "points": 12
        },
        {
            "name": "Ben",
            "points": 9
        }
    ]
}
```

Read this one layer at a time:

```text
club is a dictionary.
club["members"] is a list.
club["members"][0] is a dictionary.
club["members"][0]["name"] is a string.
```

Code:

```python
club = {
    "name": "Python Club",
    "members": [
        {
            "name": "Asha",
            "points": 12
        },
        {
            "name": "Ben",
            "points": 9
        }
    ]
}

members = club["members"]
first_member = members[0]

print(club["name"])
print(first_member["name"])
print(first_member["points"])
```

You should see:

```text
Python Club
Asha
12
```

The code is a little longer than this:

```python
print(club["members"][0]["points"])
```

But the longer version is easier to debug because it names each layer:

```python
members = club["members"]
first_member = members[0]
print(first_member["points"])
```

When nested data feels confusing, split the line apart.

That is not a step backward. That is debugging.

## Try It Yourself

Create a file named:

```text
day-51/dictionary_mistakes.py
```

Use this lesson to practice inspecting data before fixing it.

### Step 1: Check The Keys

Code:

```python
profile = {
    "name": "Iris",
    "city": "Kochi",
    "badges": ["loops", "dictionaries"]
}

print(list(profile.keys()))
print(profile["name"])
print(profile["city"])
```

You should see:

```text
['name', 'city', 'badges']
Iris
Kochi
```

The `keys()` check shows the labels that are actually available.

### Step 2: Use `get()` For An Optional Key

Code:

```python
profile = {
    "name": "Iris",
    "city": "Kochi",
    "badges": ["loops", "dictionaries"]
}

nickname = profile.get("nickname", "No nickname saved")

print(nickname)
```

You should see:

```text
No nickname saved
```

Use `get()` when a missing key is normal.

Use square brackets when a missing key should stop the program because the data is not shaped correctly.

### Step 3: Read A List Inside A Dictionary

Code:

```python
profile = {
    "name": "Iris",
    "city": "Kochi",
    "badges": ["loops", "dictionaries"]
}

badges = profile["badges"]

print(badges[0])
print(badges[1])
```

You should see:

```text
loops
dictionaries
```

The key `"badges"` gives you a list.

After that, list indexes make sense.

### Step 4: Read A Dictionary Inside A List

Code:

```python
lessons = [
    {
        "day": 50,
        "topic": "Modeling Real-World Things"
    },
    {
        "day": 51,
        "topic": "Common Dictionary Mistakes"
    }
]

today = lessons[1]

print(today["day"])
print(today["topic"])
```

You should see:

```text
51
Common Dictionary Mistakes
```

The list gives you one dictionary.

Then the dictionary gives you values by key.

## Common Mistake

These are the dictionary mistakes you will see often.

Read each broken example carefully. The point is not to memorize every error. The point is to learn what question to ask next.

### Mistake 1: Misspelling A Key

Broken code:

```python
profile = {
    "name": "Maya",
    "city": "Pune"
}

print(profile["ciyt"])
```

This is broken because the dictionary has `"city"`, not `"ciyt"`.

Python raises:

```text
KeyError: 'ciyt'
```

A `KeyError` means:

```text
Python looked for that key and did not find it.
```

Fixed code:

```python
profile = {
    "name": "Maya",
    "city": "Pune"
}

print(profile["city"])
```

You should see:

```text
Pune
```

When you see `KeyError`, check the spelling and capitalization first.

### Mistake 2: Forgetting Quotes Around String Keys

Broken code:

```python
student = {
    "name": "Asha",
    "score": 91
}

print(student[name])
```

This is broken because Python reads `name` as a variable.

There is no variable named `name`, so Python raises a `NameError`.

Fixed code:

```python
student = {
    "name": "Asha",
    "score": 91
}

print(student["name"])
```

You should see:

```text
Asha
```

String keys need quotes.

### Mistake 3: Trying To Use Dot Access

Broken code:

```python
product = {
    "name": "Notebook",
    "price": 4.5
}

print(product.price)
```

This is broken because normal dictionaries do not use dot access for keys.

Python raises an `AttributeError` because the dictionary does not have a `.price` attribute.

Fixed code:

```python
product = {
    "name": "Notebook",
    "price": 4.5
}

print(product["price"])
```

You should see:

```text
4.5
```

Use square brackets with dictionary keys:

```python
product["price"]
```

not:

```python
product.price
```

### Mistake 4: Mixing Indexes And Keys

Broken code:

```python
students = [
    {
        "name": "Maya",
        "score": 88
    },
    {
        "name": "Leo",
        "score": 72
    }
]

print(students["name"])
```

This is broken because `students` is a list.

Lists use indexes:

```text
0
1
2
```

The dictionaries inside the list use keys:

```text
name
score
```

Fixed code:

```python
students = [
    {
        "name": "Maya",
        "score": 88
    },
    {
        "name": "Leo",
        "score": 72
    }
]

first_student = students[0]

print(first_student["name"])
```

You should see:

```text
Maya
```

First use a list index.

Then use a dictionary key.

### Mistake 5: Using Inconsistent Keys Across Records

Broken code:

```python
contacts = [
    {
        "name": "Mina",
        "email": "mina@example.com"
    },
    {
        "name": "Dev",
        "email_address": "dev@example.com"
    }
]

for contact in contacts:
    print(contact["name"] + ": " + contact["email"])
```

This is broken because the first contact uses `"email"` and the second contact uses `"email_address"`.

The loop expects every contact to have the same shape.

Fixed code:

```python
contacts = [
    {
        "name": "Mina",
        "email": "mina@example.com"
    },
    {
        "name": "Dev",
        "email": "dev@example.com"
    }
]

for contact in contacts:
    print(contact["name"] + ": " + contact["email"])
```

You should see:

```text
Mina: mina@example.com
Dev: dev@example.com
```

When you have a list of records, try to keep the keys consistent.

Consistent records are easier to loop through.

### Mistake 6: Updating The Wrong Nested Layer

Broken code:

```python
student = {
    "name": "Nia",
    "progress": {
        "lessons_done": 12,
        "streak": 4
    }
}

student["lessons_done"] = 13

print(student)
```

This code runs, but it updates the wrong layer.

It adds `"lessons_done"` to the outside dictionary.

The original value inside `"progress"` is still `12`.

Fixed code:

```python
student = {
    "name": "Nia",
    "progress": {
        "lessons_done": 12,
        "streak": 4
    }
}

student["progress"]["lessons_done"] = 13

print(student)
```

You should see:

```text
{'name': 'Nia', 'progress': {'lessons_done': 13, 'streak': 4}}
```

When nested updates surprise you, print the data before and after the change.

### Mistake 7: Assuming A Key Exists

Broken code:

```python
user = {
    "name": "Sam"
}

print(user["email"].lower())
```

This is broken because `"email"` is not in the dictionary.

The code assumes every user has an email address.

Fixed code:

```python
user = {
    "name": "Sam"
}

email = user.get("email")

if email is None:
    print("No email saved.")
else:
    print(email.lower())
```

You should see:

```text
No email saved.
```

Use `get()` when the key is optional.

Use an `if` statement when the program needs to choose what to do next.

## Debug It

When dictionary code breaks, use a calm debugging path.

Try this:

```text
1. Print the data.
2. Print the type of the current value.
3. If it is a dictionary, print its keys.
4. If it is a list, print its length and one item.
5. Read one layer at a time.
6. Decide whether a missing key is a bug or a normal case.
```

Here is a broken program.

Goal:

```text
Mina: Pune
Ravi: Unknown city
```

Broken code:

```python
orders = [
    {
        "id": 101,
        "customer": {
            "name": "Mina",
            "city": "Pune"
        }
    },
    {
        "id": 102,
        "customer": {
            "name": "Ravi"
        }
    }
]

for order in orders:
    print(order["customer"]["name"] + ": " + order["customer"]["city"])
```

This is broken because the second customer's dictionary does not have a `"city"` key.

Before fixing it, inspect the shape.

Code:

```python
orders = [
    {
        "id": 101,
        "customer": {
            "name": "Mina",
            "city": "Pune"
        }
    },
    {
        "id": 102,
        "customer": {
            "name": "Ravi"
        }
    }
]

print(type(orders))
print(len(orders))

first_order = orders[0]
print(type(first_order))
print(list(first_order.keys()))

first_customer = first_order["customer"]
print(type(first_customer))
print(list(first_customer.keys()))

second_customer = orders[1]["customer"]
print(list(second_customer.keys()))
```

You should see:

```text
<class 'list'>
2
<class 'dict'>
['id', 'customer']
<class 'dict'>
['name', 'city']
['name']
```

Now the problem is visible:

```text
The first customer has "city".
The second customer does not.
```

Fixed code:

```python
orders = [
    {
        "id": 101,
        "customer": {
            "name": "Mina",
            "city": "Pune"
        }
    },
    {
        "id": 102,
        "customer": {
            "name": "Ravi"
        }
    }
]

for order in orders:
    customer = order["customer"]
    name = customer["name"]
    city = customer.get("city", "Unknown city")

    print(name + ": " + city)
```

You should see:

```text
Mina: Pune
Ravi: Unknown city
```

Here is another broken program.

Goal:

```text
Asha has 12 points.
Ben has 9 points.
```

Broken code:

```python
club = {
    "name": "Python Club",
    "members": [
        {
            "name": "Asha",
            "points": 12
        },
        {
            "name": "Ben",
            "points": 9
        }
    ]
}

for member in club["members"]:
    print(club["name"] + " has " + str(member["points"]) + " points.")
```

This code runs, but it prints the club name instead of each member name.

The loop variable is `member`, so the member name should come from `member["name"]`.

Fixed code:

```python
club = {
    "name": "Python Club",
    "members": [
        {
            "name": "Asha",
            "points": 12
        },
        {
            "name": "Ben",
            "points": 9
        }
    ]
}

for member in club["members"]:
    print(member["name"] + " has " + str(member["points"]) + " points.")
```

You should see:

```text
Asha has 12 points.
Ben has 9 points.
```

When a program runs but prints the wrong thing, check which variable you are using.

In nested data, the outer dictionary and the inner dictionary may both have useful names. Use the one that matches the sentence you are building.

## Read the Docs

Python's official documentation describes dictionaries under mapping types:

```text
https://docs.python.org/3/library/stdtypes.html#mapping-types-dict
```

You do not need to read the whole page today.

Look for these dictionary ideas:

```text
d[key]
key in d
d.get(key)
d.get(key, default)
d.keys()
d.items()
```

Read the documentation names like this:

```text
d means some dictionary.
key means the key you want.
default means the value to use if the key is missing.
```

Try this:

```python
settings = {
    "theme": "dark",
    "autosave": True
}

print("theme" in settings)
print("volume" in settings)
print(settings.get("volume", "not set"))
print(list(settings.keys()))
```

You should see:

```text
True
False
not set
['theme', 'autosave']
```

The `in` check answers:

```text
Does this key exist?
```

The `get()` method answers:

```text
Give me the value if it exists. Otherwise, give me a backup value.
```

## Mini Challenge

Create a file named:

```text
day-51/fix_contact_report.py
```

This starter code has mistakes for you to fix.

Broken code:

```python
contacts = [
    {
        "name": "Mina",
        "phone": "555-0101",
        "favorite": True
    },
    {
        "name": "Dev",
        "phone_number": "555-0102",
        "favorite": False
    },
    {
        "name": "Iris",
        "favorite": True
    }
]

for contact in contacts:
    print(contact.name + ": " + contact["phone"])
```

Goal:

```text
Mina: 555-0101
Dev: 555-0102
Iris: No phone saved
```

Fix the program.

Use these hints:

- normal dictionaries use square brackets, not dot access
- the phone key should be consistent when possible
- one contact is missing a phone number
- `get()` can help with the missing phone number

One possible fixed shape is:

Code:

```python
contacts = [
    {
        "name": "Mina",
        "phone": "555-0101",
        "favorite": True
    },
    {
        "name": "Dev",
        "phone": "555-0102",
        "favorite": False
    },
    {
        "name": "Iris",
        "favorite": True
    }
]

for contact in contacts:
    name = contact["name"]
    phone = contact.get("phone", "No phone saved")

    print(name + ": " + phone)
```

You should see:

```text
Mina: 555-0101
Dev: 555-0102
Iris: No phone saved
```

After it works, add one more contact.

Then run the program again.

## Real-World Use

Dictionary mistakes are common in real programs because real data is rarely perfect.

You might get data from:

- a form
- a contact list
- a shopping cart
- a quiz result
- a saved settings file
- a web API later in the course

Sometimes one record has all the keys.

Sometimes another record is missing one.

Sometimes two records use different names for the same idea:

```text
phone
phone_number
mobile
```

That is a data modeling problem.

Before writing a lot of code, decide what shape your data should have.

For a contact, you might choose:

```python
contact = {
    "name": "Mina",
    "phone": "555-0101",
    "email": "mina@example.com",
    "favorite": True
}
```

If a value is optional, choose how you want to represent that.

You could leave the key out:

```python
contact = {
    "name": "Iris",
    "favorite": True
}
```

Then use `get()` when reading it.

Or you could include the key with a value like `None`:

```python
contact = {
    "name": "Iris",
    "phone": None,
    "favorite": True
}
```

Both choices can work.

What matters is that your program knows which choice you made.

## Recap

Today you practiced common dictionary mistakes:

- misspelled keys cause `KeyError`
- string keys need quotes
- normal dictionaries use square brackets, not dot access
- lists use indexes, dictionaries use keys
- records in a list are easier to process when their keys are consistent
- nested updates must target the correct layer
- `get()` is useful when a key might be missing

You also practiced a debugging path:

```text
Print the shape.
Check the keys.
Read one layer at a time.
Use get() when a missing key is normal.
```

## Lesson Checklist

Before moving on, make sure you can:

- explain what a `KeyError` means
- fix a misspelled dictionary key
- add quotes around string keys
- replace dot access with square bracket access
- choose between a list index and a dictionary key
- print `list(dictionary.keys())` to inspect available keys
- use `get()` with a default value
- read nested data one layer at a time
- update a nested dictionary value without adding the key in the wrong place

## Exercises

### Exercise 1: Fix The Misspelled Key

Goal:

```text
Theme: dark
```

Broken code:

```python
settings = {
    "theme": "dark",
    "font_size": "medium"
}

print("Theme:", settings["theem"])
```

Fix the key and run the program.

### Exercise 2: Add The Missing Quotes

Goal:

```text
Score: 84
```

Broken code:

```python
result = {
    "student": "Noah",
    "score": 84
}

print("Score:", result[score])
```

Fix the key access.

### Exercise 3: Replace Dot Access

Goal:

```text
Notebook costs 4.5
```

Broken code:

```python
product = {
    "name": "Notebook",
    "price": 4.5
}

print(product.name + " costs " + str(product.price))
```

Fix both dictionary reads.

### Exercise 4: Use The Right Layer

Goal:

```text
Leo
```

Broken code:

```python
students = [
    {
        "name": "Maya",
        "score": 88
    },
    {
        "name": "Leo",
        "score": 72
    }
]

print(students["name"])
```

Fix the code by choosing the correct list index first.

### Exercise 5: Make The Records Consistent

Goal:

```text
Mina: mina@example.com
Dev: dev@example.com
```

Broken code:

```python
contacts = [
    {
        "name": "Mina",
        "email": "mina@example.com"
    },
    {
        "name": "Dev",
        "email_address": "dev@example.com"
    }
]

for contact in contacts:
    print(contact["name"] + ": " + contact["email"])
```

Fix the data shape so both contacts use the same key.

### Exercise 6: Update The Nested Value

Goal:

```text
{'name': 'Nia', 'progress': {'lessons_done': 13, 'streak': 4}}
```

Broken code:

```python
student = {
    "name": "Nia",
    "progress": {
        "lessons_done": 12,
        "streak": 4
    }
}

student["lessons_done"] = 13

print(student)
```

Fix the update so it changes the value inside `"progress"`.

### Exercise 7: Handle A Missing Key

Goal:

```text
Iris: No phone saved
```

Broken code:

```python
contact = {
    "name": "Iris"
}

print(contact["name"] + ": " + contact["phone"])
```

Fix the program with `get()`.

### Exercise 8: Debug A Small Report

This program has more than one mistake.

Goal:

```text
Reading: done
Practice: not done
```

Broken code:

```python
tasks = [
    {
        "title": "Reading",
        "done": True
    },
    {
        "name": "Practice",
        "done": False
    }
]

for task in tasks:
    if task.done:
        status = "done"
    else:
        status = "not done"

    print(task["title"] + ": " + status)
```

Fix the inconsistent key and the dot access.

## Tiny Win

You can now treat dictionary bugs as questions about data shape.

That is a useful habit.

Instead of guessing, you can print the current value, check its keys, and move through the data one layer at a time.

## Tomorrow

Day 52 is a practice day:

```text
Practice Day: Data Modeling
```

You will design and repair small data shapes using lists, dictionaries, and nested structures.

Today's debugging habits will help you decide what each record should look like before you write the rest of the program.
