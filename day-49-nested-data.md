# Day 49: Nested Data

**Focus:** Reading data that contains other data  
**You will practice:** dictionaries inside dictionaries, lists inside dictionaries, dictionaries inside lists, nested access, simple nested loops, and debugging layer mistakes  
**Estimated time:** 45-55 minutes

## Today's Goal

Today you will learn how to read nested data.

Nested data means data inside data.

You have already seen lists:

```python
skills = ["Python", "HTML", "CSS"]
```

You have already seen dictionaries:

```python
profile = {
    "name": "Maya",
    "city": "Pune"
}
```

Nested data combines those ideas:

```python
profile = {
    "name": "Maya",
    "address": {
        "city": "Pune",
        "country": "India"
    }
}
```

The value for `"address"` is another dictionary.

That is nested data.

By the end of this lesson, you should be able to:

- recognize data inside data
- read a dictionary that contains another dictionary
- read a dictionary that contains a list
- read a list that contains dictionaries
- access nested values one layer at a time
- loop through simple nested data
- debug mistakes caused by skipping a layer
- explain why clear structure matters

The main idea is:

```text
Nested data is not a new collection.
It is lists and dictionaries placed inside each other.
```

Tomorrow you will use this idea to model real-world things more carefully.

## The Big Idea

A dictionary value can be another dictionary.

Example:

```python
profile = {
    "username": "maya_dev",
    "address": {
        "city": "Pune",
        "country": "India"
    }
}

print(profile["username"])
print(profile["address"]["city"])
```

You should see:

```text
maya_dev
Pune
```

Read this line slowly:

```text
profile["address"]["city"]
```

It means:

```text
Start with profile.
Use the key "address" to get the inner dictionary.
Inside that inner dictionary, use the key "city".
```

The first key gets you one layer deeper.

The second key gets the value you wanted.

A dictionary can also contain a list.

Example:

```python
player = {
    "name": "Nia",
    "inventory": ["map", "torch", "coin"]
}

print(player["name"])
print(player["inventory"][0])
print(player["inventory"][2])
```

You should see:

```text
Nia
map
coin
```

Read this line slowly:

```text
player["inventory"][0]
```

It means:

```text
Start with player.
Use the key "inventory" to get the list.
Inside that list, use index 0.
```

A list can also contain dictionaries.

Example:

```python
students = [
    {"name": "Asha", "score": 9},
    {"name": "Ben", "score": 7},
    {"name": "Cara", "score": 10}
]

print(students[0]["name"])
print(students[2]["score"])
```

You should see:

```text
Asha
10
```

Read this line slowly:

```text
students[2]["score"]
```

It means:

```text
Start with students.
Use index 2 to get the third dictionary.
Inside that dictionary, use the key "score".
```

The bracket style depends on the layer you are reading:

```text
Dictionary layer -> use a key.
List layer       -> use an index.
```

## The Mental Model

Think of nested data as rooms inside rooms.

You do not jump straight to the final value.

You enter one room, then the next room, then the next.

Use this question at every layer:

```text
What type of thing do I have right now?
```

If you have a dictionary, use a key.

If you have a list, use an index or a loop.

If you have a string, number, or Boolean, you have reached a normal value.

Example:

```python
order = {
    "order_id": 1042,
    "customer": {
        "name": "Asha",
        "email": "asha@example.com"
    },
    "items": [
        {"name": "notebook", "price": 3, "quantity": 2},
        {"name": "pen", "price": 1, "quantity": 5}
    ]
}

print(order["customer"]["name"])
print(order["items"][0]["name"])
print(order["items"][1]["quantity"])
```

You should see:

```text
Asha
notebook
5
```

Read the first line:

```text
order["customer"]["name"]
```

Layer by layer:

```text
order                 -> dictionary
order["customer"]     -> inner dictionary
order["customer"]["name"] -> string
```

Read the second line:

```text
order["items"][0]["name"]
```

Layer by layer:

```text
order                  -> dictionary
order["items"]         -> list
order["items"][0]      -> first dictionary in the list
order["items"][0]["name"] -> string
```

The chain is not magic.

Each bracket handles exactly one layer.

When you get confused, split the chain into named steps:

```python
order = {
    "order_id": 1042,
    "customer": {
        "name": "Asha",
        "email": "asha@example.com"
    },
    "items": [
        {"name": "notebook", "price": 3, "quantity": 2},
        {"name": "pen", "price": 1, "quantity": 5}
    ]
}

items = order["items"]
first_item = items[0]
name = first_item["name"]

print(name)
```

You should see:

```text
notebook
```

This is often the best beginner habit.

Long bracket chains are legal, but named steps are easier to debug.

## Try It Yourself

Create a file named:

```text
day-49/nested_data.py
```

You will practice reading nested structures one layer at a time.

### Step 1: A User Profile With An Address

Code:

```python
profile = {
    "username": "maya_dev",
    "address": {
        "city": "Pune",
        "country": "India"
    },
    "skills": ["Python", "HTML", "CSS"]
}

print(profile["username"])
print(profile["address"]["city"])
print(profile["skills"][0])
```

You should see:

```text
maya_dev
Pune
Python
```

The profile has three top-level keys:

```text
username
address
skills
```

The value for `"address"` is a dictionary.

The value for `"skills"` is a list.

### Step 2: An Order With Items

Code:

```python
order = {
    "order_id": 1042,
    "customer": "Asha",
    "items": [
        {"name": "notebook", "price": 3, "quantity": 2},
        {"name": "pen", "price": 1, "quantity": 5}
    ]
}

first_item = order["items"][0]
first_total = first_item["price"] * first_item["quantity"]

print("Order:", order["order_id"])
print("First item:", first_item["name"])
print("First item total:", first_total)
print("Second item:", order["items"][1]["name"])
```

You should see:

```text
Order: 1042
First item: notebook
First item total: 6
Second item: pen
```

The order is a dictionary.

The `"items"` value is a list.

Each item in that list is a dictionary.

### Step 3: A Class Roster

Code:

```python
roster = [
    {"name": "Asha", "score": 9},
    {"name": "Ben", "score": 7},
    {"name": "Cara", "score": 10}
]

for student in roster:
    print(f"{student['name']} scored {student['score']}.")
```

You should see:

```text
Asha scored 9.
Ben scored 7.
Cara scored 10.
```

In this loop, `student` is one dictionary at a time.

That means this works inside the loop:

```text
student["name"]
```

The loop handles the list layer.

The key handles the dictionary layer.

### Step 4: A Game Inventory

Code:

```python
player = {
    "name": "Nia",
    "stats": {
        "level": 4,
        "health": 80
    },
    "inventory": ["map", "torch", "coin"]
}

print("Player:", player["name"])
print("Level:", player["stats"]["level"])
print("Health:", player["stats"]["health"])

for item in player["inventory"]:
    print("Item:", item)
```

You should see:

```text
Player: Nia
Level: 4
Health: 80
Item: map
Item: torch
Item: coin
```

The stats are stored in an inner dictionary.

The inventory is stored in a list.

### Step 5: A Weather Report

Code:

```python
weather = {
    "city": "Kochi",
    "current": {
        "temperature_c": 29,
        "condition": "rainy"
    },
    "forecast": [
        {"day": "Monday", "high_c": 30, "condition": "rain"},
        {"day": "Tuesday", "high_c": 31, "condition": "cloudy"}
    ]
}

print("City:", weather["city"])
print("Now:", weather["current"]["temperature_c"])

for day in weather["forecast"]:
    print(f"{day['day']}: {day['condition']}, high {day['high_c']}C")
```

You should see:

```text
City: Kochi
Now: 29
Monday: rain, high 30C
Tuesday: cloudy, high 31C
```

This shape is common in real programs.

There is one weather report.

Inside it, there is current weather and a list of forecast days.

## Common Mistake

### Mistake 1: Skipping A Layer

Broken code:

```python
profile = {
    "name": "Maya",
    "address": {
        "city": "Pune",
        "country": "India"
    }
}

print(profile["city"])
```

This is broken because `"city"` is not a top-level key in `profile`.

The top-level keys are:

```text
name
address
```

The `"city"` key is inside the `"address"` dictionary.

Fixed code:

```python
profile = {
    "name": "Maya",
    "address": {
        "city": "Pune",
        "country": "India"
    }
}

print(profile["address"]["city"])
```

You should see:

```text
Pune
```

Read it as:

```text
profile -> address -> city
```

### Mistake 2: Using The Wrong Key

Broken code:

```python
weather = {
    "current": {
        "temperature_c": 29,
        "condition": "rainy"
    }
}

print(weather["current"]["temperature"])
```

This is broken because the inner dictionary has `"temperature_c"`, not `"temperature"`.

Fixed code:

```python
weather = {
    "current": {
        "temperature_c": 29,
        "condition": "rainy"
    }
}

print(weather["current"]["temperature_c"])
```

You should see:

```text
29
```

When you see `KeyError`, check the exact key at the exact layer.

### Mistake 3: Treating A List Like A Dictionary

Broken code:

```python
order = {
    "items": [
        {"name": "notebook", "price": 3},
        {"name": "pen", "price": 1}
    ]
}

print(order["items"]["name"])
```

This is broken because `order["items"]` is a list.

A list needs an index or a loop before you can read one item's dictionary keys.

Fixed code:

```python
order = {
    "items": [
        {"name": "notebook", "price": 3},
        {"name": "pen", "price": 1}
    ]
}

print(order["items"][0]["name"])
```

You should see:

```text
notebook
```

Read it as:

```text
order -> items -> first item -> name
```

### Mistake 4: Treating A List Of Dictionaries Like One Dictionary

Broken code:

```python
students = [
    {"name": "Asha", "score": 9},
    {"name": "Ben", "score": 7}
]

print(students["name"])
```

This is broken because `students` is a list.

The `"name"` key belongs to each dictionary inside the list.

Fixed code:

```python
students = [
    {"name": "Asha", "score": 9},
    {"name": "Ben", "score": 7}
]

print(students[0]["name"])
```

You should see:

```text
Asha
```

Or loop through every student:

```python
students = [
    {"name": "Asha", "score": 9},
    {"name": "Ben", "score": 7}
]

for student in students:
    print(student["name"])
```

You should see:

```text
Asha
Ben
```

## Debug It

Read each broken program. Find the layer problem, then fix it.

### Debug 1: The City

Goal:

```text
City: Pune
```

Broken code:

```python
profile = {
    "name": "Maya",
    "address": {
        "city": "Pune",
        "country": "India"
    }
}

print("City:", profile["city"])
```

The problem:

```text
"city" is inside profile["address"], not directly inside profile.
```

Fixed code:

```python
profile = {
    "name": "Maya",
    "address": {
        "city": "Pune",
        "country": "India"
    }
}

print("City:", profile["address"]["city"])
```

You should see:

```text
City: Pune
```

### Debug 2: The Order Total

Goal:

```text
Total: 6
```

Broken code:

```python
order = {
    "items": [
        {"name": "notebook", "price": 3, "quantity": 2}
    ]
}

total = order["items"]["price"] * order["items"]["quantity"]

print("Total:", total)
```

The problem:

```text
order["items"] is a list, so the code must choose an item before using "price" and "quantity".
```

Fixed code:

```python
order = {
    "items": [
        {"name": "notebook", "price": 3, "quantity": 2}
    ]
}

item = order["items"][0]
total = item["price"] * item["quantity"]

print("Total:", total)
```

You should see:

```text
Total: 6
```

### Debug 3: The Roster Loop

Goal:

```text
Asha
Ben
Cara
```

Broken code:

```python
roster = [
    {"name": "Asha", "score": 9},
    {"name": "Ben", "score": 7},
    {"name": "Cara", "score": 10}
]

for student in roster:
    print(roster["name"])
```

The problem:

```text
roster is the whole list.
student is one dictionary from the list.
```

Fixed code:

```python
roster = [
    {"name": "Asha", "score": 9},
    {"name": "Ben", "score": 7},
    {"name": "Cara", "score": 10}
]

for student in roster:
    print(student["name"])
```

You should see:

```text
Asha
Ben
Cara
```

### Debug 4: The Forecast High

Goal:

```text
Tuesday high: 31
```

Broken code:

```python
weather = {
    "forecast": [
        {"day": "Monday", "high_c": 30},
        {"day": "Tuesday", "high_c": 31}
    ]
}

print("Tuesday high:", weather["forecast"][1]["high"])
```

The problem:

```text
The key is "high_c", not "high".
```

Fixed code:

```python
weather = {
    "forecast": [
        {"day": "Monday", "high_c": 30},
        {"day": "Tuesday", "high_c": 31}
    ]
}

print("Tuesday high:", weather["forecast"][1]["high_c"])
```

You should see:

```text
Tuesday high: 31
```

## Read the Docs

Nested data still uses the same list and dictionary tools you already know.

Find Python's official documentation for lists:

```text
https://docs.python.org/3/tutorial/introduction.html#lists
```

Find Python's official documentation for dictionaries:

```text
https://docs.python.org/3/library/stdtypes.html#mapping-types-dict
```

You do not need to read the whole pages today.

Look for these ideas:

```text
list[index]
d[key]
d.items()
```

Then connect them to nested data:

```python
data = {
    "letters": ["a", "b", "c"]
}

print(data["letters"])
print(data["letters"][1])
```

You should see:

```text
['a', 'b', 'c']
b
```

The documentation may not call this "nested data" every time.

That is fine.

You are combining two ideas:

```text
Use a key when the current layer is a dictionary.
Use an index when the current layer is a list.
```

Later in the course, you will see nested data in JSON files and data from websites.

For now, keep the focus on reading the Python structure in front of you.

## Mini Challenge

Create a file named:

```text
day-49/order_summary.py
```

Build an order summary from nested data.

Start with this data:

```python
order = {
    "order_id": 2041,
    "customer": {
        "name": "Ravi",
        "city": "Hyderabad"
    },
    "items": [
        {"name": "notebook", "price": 3, "quantity": 2},
        {"name": "pencil", "price": 1, "quantity": 4},
        {"name": "folder", "price": 2, "quantity": 1}
    ]
}
```

Your program should:

- print the order id
- print the customer's name and city
- loop through the items
- print each item name, quantity, and item total
- print the full order total

One possible solution:

```python
order = {
    "order_id": 2041,
    "customer": {
        "name": "Ravi",
        "city": "Hyderabad"
    },
    "items": [
        {"name": "notebook", "price": 3, "quantity": 2},
        {"name": "pencil", "price": 1, "quantity": 4},
        {"name": "folder", "price": 2, "quantity": 1}
    ]
}

print("Order:", order["order_id"])
print(f"Customer: {order['customer']['name']} from {order['customer']['city']}")

total = 0

for item in order["items"]:
    item_total = item["price"] * item["quantity"]
    total = total + item_total
    print(f"{item['quantity']} x {item['name']} = {item_total}")

print("Total:", total)
```

You should see:

```text
Order: 2041
Customer: Ravi from Hyderabad
2 x notebook = 6
4 x pencil = 4
1 x folder = 2
Total: 12
```

After it works, add one more item to the `"items"` list.

Run the program again.

The loop should include the new item without adding a new print line for it.

## Real-World Use

Nested data is common because real-world things often have smaller parts.

A user profile may have an address:

```python
profile = {
    "username": "maya_dev",
    "address": {
        "city": "Pune",
        "country": "India"
    }
}

print(profile["address"]["city"])
```

You should see:

```text
Pune
```

An order may have many items:

```python
order = {
    "items": [
        {"name": "notebook", "quantity": 2},
        {"name": "pen", "quantity": 5}
    ]
}

for item in order["items"]:
    print(item["name"], item["quantity"])
```

You should see:

```text
notebook 2
pen 5
```

A class roster may be a list of student dictionaries:

```python
roster = [
    {"name": "Asha", "present": True},
    {"name": "Ben", "present": False}
]

for student in roster:
    print(student["name"], student["present"])
```

You should see:

```text
Asha True
Ben False
```

A game inventory may store a list of item names and a dictionary of stats:

```python
player = {
    "inventory": ["map", "torch"],
    "stats": {
        "health": 80,
        "level": 4
    }
}

print(player["inventory"][1])
print(player["stats"]["health"])
```

You should see:

```text
torch
80
```

A weather report may have current conditions and a forecast list:

```python
weather = {
    "current": {
        "condition": "cloudy"
    },
    "forecast": [
        {"day": "Monday", "condition": "rain"},
        {"day": "Tuesday", "condition": "sunny"}
    ]
}

print(weather["current"]["condition"])
print(weather["forecast"][1]["condition"])
```

You should see:

```text
cloudy
sunny
```

The exact topic changes.

The reading habit stays the same:

```text
Name the outer structure.
Read one layer.
Check what type you have.
Read the next layer.
Stop when you reach the value.
```

## Recap

Today you learned that:

- nested data means data inside data
- a dictionary can contain another dictionary
- a dictionary can contain a list
- a list can contain dictionaries
- each bracket handles one layer
- dictionary layers use keys
- list layers use indexes or loops
- long bracket chains can be split into smaller named steps
- `KeyError` often means the key is wrong or at the wrong layer
- `TypeError` can happen when you treat a list like a dictionary
- clear structure makes real data easier to read

The most useful question is:

```text
What type of thing do I have right now?
```

If you can answer that, the next bracket usually becomes clearer.

## Lesson Checklist

Before moving on, check that you can:

- explain nested data in your own words
- identify the outer collection in a nested structure
- identify an inner dictionary
- identify an inner list
- read `profile["address"]["city"]` in layers
- read `order["items"][0]["name"]` in layers
- use a loop to visit dictionaries inside a list
- use a loop to visit items inside a dictionary value
- split a long nested access into smaller variables
- fix code that skips a layer
- fix code that uses the wrong key
- fix code that uses a key when an index is needed
- explain why clear nested data prepares you for modeling real things

## Exercises

### Exercise 1

Predict the output.

```python
profile = {
    "name": "Maya",
    "address": {
        "city": "Pune",
        "country": "India"
    }
}

print(profile["address"])
print(profile["address"]["country"])
```

Then run it.

### Exercise 2

Create a profile dictionary with these keys:

```text
name
address
skills
```

The `"address"` value should be a dictionary with `"city"` and `"country"`.

The `"skills"` value should be a list with three skills.

Print the name, city, and first skill.

### Exercise 3

Start with this data:

```python
player = {
    "name": "Kai",
    "inventory": ["key", "rope", "apple"]
}
```

Print the player's name.

Then print each inventory item with a loop.

### Exercise 4

Start with this roster:

```python
roster = [
    {"name": "Asha", "score": 9},
    {"name": "Ben", "score": 7},
    {"name": "Cara", "score": 10}
]
```

Use a loop to print:

```text
Asha: 9
Ben: 7
Cara: 10
```

### Exercise 5

Start with this order:

```python
order = {
    "items": [
        {"name": "notebook", "price": 3, "quantity": 2},
        {"name": "pencil", "price": 1, "quantity": 4}
    ]
}
```

Print the name of the first item.

Then calculate and print the total for the second item.

### Exercise 6

Start with this weather report:

```python
weather = {
    "city": "Kochi",
    "current": {
        "temperature_c": 29,
        "condition": "rainy"
    },
    "forecast": [
        {"day": "Monday", "condition": "rain"},
        {"day": "Tuesday", "condition": "cloudy"}
    ]
}
```

Print the city.

Print the current condition.

Loop through the forecast and print each day with its condition.

### Exercise 7

Fix the broken code.

Broken code:

```python
profile = {
    "name": "Maya",
    "address": {
        "city": "Pune"
    }
}

print(profile["city"])
```

The goal is to print:

```text
Pune
```

### Exercise 8

Fix the broken code.

Broken code:

```python
order = {
    "items": [
        {"name": "notebook"},
        {"name": "pen"}
    ]
}

print(order["items"]["name"])
```

The goal is to print:

```text
notebook
```

### Exercise 9

Fix the broken code.

Broken code:

```python
roster = [
    {"name": "Asha"},
    {"name": "Ben"}
]

for student in roster:
    print(roster["name"])
```

The goal is to print both names.

### Exercise 10

Write the type after each step.

Use this data:

```python
order = {
    "items": [
        {"name": "folder", "price": 2}
    ]
}
```

Complete these notes:

```text
order is a ...
order["items"] is a ...
order["items"][0] is a ...
order["items"][0]["name"] is a ...
```

### Exercise 11

Split this long access into smaller variables:

```text
print(weather["forecast"][1]["condition"])
```

Use variable names like:

```text
forecast
second_day
condition
```

Then print `condition`.

### Exercise 12

Design your own nested data for one real-world thing.

Choose one:

```text
a library book record
a movie listing
a restaurant menu
a sports team
a travel plan
```

Use at least one dictionary inside another dictionary, or one list of dictionaries.

Print three values from your structure.

Then write one sentence explaining the shape you chose.

## Tiny Win

You can now read data with shape.

That is a real beginner milestone.

Many programs do not store one flat list or one small dictionary.

They store things like:

```text
one order with many items
one user with an address
one class with many students
one weather report with many forecast days
```

Nested data lets one variable hold that structure.

The win is not speed.

The win is reading slowly and choosing the right layer.

## Tomorrow

Tomorrow is:

```text
Day 50: Modeling Real-World Things
```

Today you practiced reading nested data that already exists.

Tomorrow you will make design choices:

```text
Should this be a dictionary?
Should this be a list?
Should this be a list of dictionaries?
Should this be a dictionary with smaller dictionaries inside it?
```

Nested data is the tool.

Modeling is deciding the right shape for the thing your program needs to remember.
