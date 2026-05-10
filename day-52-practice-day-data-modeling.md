# Day 52: Practice Day: Data Modeling

**Focus:** Practicing dictionary-based data models for real-world records  
**You will practice:** dictionaries, reading and updating values, looping through dictionaries, lists of dictionaries, dictionaries of lists, nested data, modeling real-world things, and common dictionary mistakes  
**Estimated time:** 60-75 minutes

## Today's Goal

Today is a practice day.

You are not learning one big new syntax idea. You are using the dictionary tools from the last several lessons to model real data.

You will practice with:

- one dictionary
- reading values by key
- updating values
- looping through keys, values, and items
- a list of dictionaries
- a dictionary of lists
- nested dictionaries and lists
- choosing a useful shape for real-world data
- debugging common dictionary mistakes

By the end of this lesson, you should be able to look at a small problem and ask:

```text
What is one record?
What keys should that record have?
Do I need one record or many records?
Do I need a list, a dictionary, or both?
How will I read, update, and loop through the data?
```

That thinking prepares you for tomorrow.

Day 53 is a refactor day. You will clean up old code. Data modeling practice helps because messy data shapes often lead to messy code.

Today is about getting more comfortable before that cleanup work.

## The Big Idea

Data modeling means choosing a shape for your data.

A contact can be one dictionary:

```python
contact = {
    "name": "Mina",
    "phone": "555-0104",
    "email": "mina@example.com"
}

print(contact["name"])
print(contact["phone"])
```

You should see:

```text
Mina
555-0104
```

Several contacts can be a list of dictionaries:

```python
contacts = [
    {"name": "Mina", "phone": "555-0104"},
    {"name": "Sam", "phone": "555-0199"},
    {"name": "Iris", "phone": "555-0130"}
]

for contact in contacts:
    print(contact["name"] + ":", contact["phone"])
```

You should see:

```text
Mina: 555-0104
Sam: 555-0199
Iris: 555-0130
```

A task board can be a dictionary of lists:

```python
tasks = {
    "todo": ["write notes", "practice dictionaries"],
    "done": ["read lesson"]
}

tasks["todo"].append("review mistakes")

for status, task_list in tasks.items():
    print(status + ":", len(task_list))
```

You should see:

```text
todo: 3
done: 1
```

An order can be nested data:

```python
order = {
    "order_id": "A100",
    "customer": "Mina",
    "items": [
        {"name": "notebook", "price": 5, "quantity": 2},
        {"name": "pen", "price": 2, "quantity": 3}
    ]
}

total = 0

for item in order["items"]:
    total = total + item["price"] * item["quantity"]

print("Order:", order["order_id"])
print("Customer:", order["customer"])
print("Total:", total)
```

You should see:

```text
Order: A100
Customer: Mina
Total: 16
```

All of these examples use familiar tools.

The important skill is choosing the right shape:

```text
one thing with named details        dictionary
many similar things                 list of dictionaries
named groups of many values          dictionary of lists
details inside details               nested data
```

## The Mental Model

Think of data modeling as drawing a small map before writing code.

For one student, use one dictionary:

```python
student = {
    "name": "Asha",
    "score": 88,
    "passed": True
}

print(student["name"])
print(student["score"])
```

You should see:

```text
Asha
88
```

For several students, put those dictionaries in a list:

```python
students = [
    {"name": "Asha", "score": 88, "passed": True},
    {"name": "Ben", "score": 52, "passed": False},
    {"name": "Cara", "score": 91, "passed": True}
]

for student in students:
    print(student["name"], student["score"])
```

You should see:

```text
Asha 88
Ben 52
Cara 91
```

Read the shape from the outside in:

```text
students is a list.
Each item in the list is one student dictionary.
Each student dictionary has keys like "name", "score", and "passed".
```

For a dictionary of lists, read the keys first:

```python
playlist = {
    "morning": ["Open Sky", "Fresh Start"],
    "focus": ["Deep Work", "Quiet Keys"],
    "evening": ["Slow Walk"]
}

for mood, songs in playlist.items():
    print(mood + ":", len(songs), "songs")
```

You should see:

```text
morning: 2 songs
focus: 2 songs
evening: 1 songs
```

Read that shape like this:

```text
playlist is a dictionary.
Each key is a mood.
Each value is a list of song titles.
```

For nested data, pause before indexing.

Ask:

```text
Am I holding a dictionary right now?
Am I holding a list right now?
What key or index gets me one step closer?
```

That question prevents many beginner mistakes.

## Warm-Up

For each warm-up, predict the output before running the code.

### Warm-Up 1: Read And Update One Contact

Code:

```python
contact = {
    "name": "Mina",
    "phone": "555-0104",
    "favorite": False
}

contact["favorite"] = True

print(contact["name"])
print(contact["phone"])
print("Favorite:", contact["favorite"])
```

You should see:

```text
Mina
555-0104
Favorite: True
```

Debugging prompt:

```text
Which line changes an existing value?
Which lines read values?
```

### Warm-Up 2: Loop Through A Product

Code:

```python
product = {
    "name": "water bottle",
    "price": 12,
    "stock": 4
}

for field, value in product.items():
    print(field + ":", value)
```

You should see:

```text
name: water bottle
price: 12
stock: 4
```

Debugging prompt:

```text
Why does this loop use .items() instead of .values()?
```

### Warm-Up 3: Loop Through A List Of Students

Code:

```python
students = [
    {"name": "Asha", "score": 88},
    {"name": "Ben", "score": 52},
    {"name": "Cara", "score": 91}
]

for student in students:
    if student["score"] >= 60:
        print(student["name"], "passed")
    else:
        print(student["name"], "needs practice")
```

You should see:

```text
Asha passed
Ben needs practice
Cara passed
```

Debugging prompt:

```text
What does student hold on each loop turn?
```

### Warm-Up 4: Use A Dictionary Of Lists

Code:

```python
tasks = {
    "todo": ["write notes", "practice loops"],
    "done": ["read lesson"]
}

tasks["done"].append("practice loops")
tasks["todo"].remove("practice loops")

print("Todo:", tasks["todo"])
print("Done:", tasks["done"])
```

You should see:

```text
Todo: ['write notes']
Done: ['read lesson', 'practice loops']
```

Debugging prompt:

```text
Which value is a list?
Which methods are list methods?
```

### Warm-Up 5: Read Nested Order Data

Code:

```python
order = {
    "customer": "Sam",
    "items": [
        {"name": "pencil", "price": 2, "quantity": 5},
        {"name": "notebook", "price": 4, "quantity": 2}
    ]
}

total = 0

for item in order["items"]:
    item_total = item["price"] * item["quantity"]
    total = total + item_total
    print(item["name"] + ":", item_total)

print("Total:", total)
```

You should see:

```text
pencil: 10
notebook: 8
Total: 18
```

Debugging prompt:

```text
What is order["items"]?
What is item inside the loop?
```

## Practice Problems

Use this rhythm for each problem:

```text
Read the goal.
Name the data shape.
Write the smallest useful version.
Predict the result.
Run the code.
Change one value and run it again.
Debug one thing at a time.
```

### Practice Problem 1: Contact Book

Create a file named `day-52/contact_book_practice.py`.

Goal:

```text
Store several contacts.
Print each contact's name and phone number.
Mark one contact as a favorite.
Print only favorite contacts.
```

Hint:

```text
This is a list of dictionaries because there are several similar contact records.
```

Code:

```python
contacts = [
    {"name": "Mina", "phone": "555-0104", "favorite": False},
    {"name": "Sam", "phone": "555-0199", "favorite": False},
    {"name": "Iris", "phone": "555-0130", "favorite": True}
]

for contact in contacts:
    if contact["name"] == "Sam":
        contact["favorite"] = True

print("All contacts")

for contact in contacts:
    print(contact["name"] + ":", contact["phone"])

print("Favorites")

for contact in contacts:
    if contact["favorite"]:
        print(contact["name"])
```

You should see:

```text
All contacts
Mina: 555-0104
Sam: 555-0199
Iris: 555-0130
Favorites
Sam
Iris
```

Try this:

```text
Add an "email" key to every contact.
Print each contact's email in the first loop.
```

Debugging prompt:

```text
If one contact is missing "email", which lookup style could keep the program from crashing?
```

### Practice Problem 2: Student Report

Create a file named `day-52/student_report.py`.

Goal:

```text
Store students as dictionaries.
Add a "passed" key to each student.
Count how many students passed.
Print a short report.
```

Hint:

```text
Add the "passed" key inside the loop because it depends on each student's score.
```

Code:

```python
students = [
    {"name": "Asha", "score": 88},
    {"name": "Ben", "score": 52},
    {"name": "Cara", "score": 91},
    {"name": "Dev", "score": 60}
]

passed_count = 0

for student in students:
    student["passed"] = student["score"] >= 60

    if student["passed"]:
        passed_count = passed_count + 1

for student in students:
    print(student["name"] + ":", student["score"], "passed:", student["passed"])

print("Passed:", passed_count)
print("Total students:", len(students))
```

You should see:

```text
Asha: 88 passed: True
Ben: 52 passed: False
Cara: 91 passed: True
Dev: 60 passed: True
Passed: 3
Total students: 4
```

Try this:

```text
Change Dev's score to 59.
Run the program again.
Only the data should change, not the logic.
```

Debugging prompt:

```text
Why is passed_count created before the loop?
```

### Practice Problem 3: Product Stock

Create a file named `day-52/product_stock.py`.

Goal:

```text
Store products.
Print each product.
Reduce the stock for one product.
Print which products are low stock.
```

Hint:

```text
Each product is one dictionary.
The catalog is a list because there are many products.
```

Code:

```python
products = [
    {"name": "notebook", "price": 5, "stock": 12},
    {"name": "pen", "price": 2, "stock": 3},
    {"name": "backpack", "price": 30, "stock": 2}
]

for product in products:
    if product["name"] == "pen":
        product["stock"] = product["stock"] - 1

print("Products")

for product in products:
    print(product["name"] + ":", product["stock"], "in stock")

print("Low stock")

for product in products:
    if product["stock"] <= 2:
        print(product["name"])
```

You should see:

```text
Products
notebook: 12 in stock
pen: 2 in stock
backpack: 2 in stock
Low stock
pen
backpack
```

Try this:

```text
Add a product with stock 0.
Run the program again.
It should appear in the low stock section.
```

Debugging prompt:

```text
Which key stores the number that changes?
```

### Practice Problem 4: Order Total

Create a file named `day-52/order_total.py`.

Goal:

```text
Store one order.
The order should contain a list of item dictionaries.
Calculate the total.
Print one line per item and one final total.
```

Hint:

```text
order is one dictionary.
order["items"] is a list.
Each item in that list is a dictionary.
```

Code:

```python
order = {
    "order_id": "A100",
    "customer": "Mina",
    "items": [
        {"name": "notebook", "price": 5, "quantity": 2},
        {"name": "pen", "price": 2, "quantity": 3},
        {"name": "folder", "price": 4, "quantity": 1}
    ]
}

total = 0

print("Order:", order["order_id"])
print("Customer:", order["customer"])

for item in order["items"]:
    item_total = item["price"] * item["quantity"]
    total = total + item_total
    print(item["quantity"], "x", item["name"], "=", item_total)

print("Total:", total)
```

You should see:

```text
Order: A100
Customer: Mina
2 x notebook = 10
3 x pen = 6
1 x folder = 4
Total: 20
```

Try this:

```text
Add another item dictionary to order["items"].
The loop should include it without another print line.
```

Debugging prompt:

```text
Why does the program need a loop before it can calculate the order total?
```

### Practice Problem 5: Playlist Data

Create a file named `day-52/playlist_practice.py`.

Goal:

```text
Store one playlist.
The playlist has a name and a list of song dictionaries.
Print every song.
Calculate the total duration.
```

Hint:

```text
Use nested data because the playlist has its own details and also contains many songs.
```

Code:

```python
playlist = {
    "name": "Focus Mix",
    "songs": [
        {"title": "Open Sky", "artist": "Nia", "minutes": 3},
        {"title": "Quiet Keys", "artist": "Ravi", "minutes": 4},
        {"title": "Deep Work", "artist": "Mina", "minutes": 5}
    ]
}

total_minutes = 0

print("Playlist:", playlist["name"])

for song in playlist["songs"]:
    total_minutes = total_minutes + song["minutes"]
    print(song["title"], "by", song["artist"])

print("Total minutes:", total_minutes)
```

You should see:

```text
Playlist: Focus Mix
Open Sky by Nia
Quiet Keys by Ravi
Deep Work by Mina
Total minutes: 12
```

Try this:

```text
Add a "liked" key to each song.
Print only liked songs in a second loop.
```

Debugging prompt:

```text
What is the difference between playlist["name"] and playlist["songs"]?
```

### Practice Problem 6: Task Board

Create a file named `day-52/task_board.py`.

Goal:

```text
Store tasks by status.
Move one task from todo to doing.
Move one task from doing to done.
Print a board summary.
```

Hint:

```text
This is a dictionary of lists because each status name points to a list of task titles.
```

Code:

```python
task_board = {
    "todo": ["write notes", "practice data modeling"],
    "doing": ["read lesson"],
    "done": []
}

task_board["todo"].remove("practice data modeling")
task_board["doing"].append("practice data modeling")

task_board["doing"].remove("read lesson")
task_board["done"].append("read lesson")

for status, tasks in task_board.items():
    print(status + ":", len(tasks))

    for task in tasks:
        print("-", task)
```

You should see:

```text
todo: 1
- write notes
doing: 1
- practice data modeling
done: 1
- read lesson
```

Try this:

```text
Before removing a task, check whether it is in the source list.
That makes the move safer.
```

Debugging prompt:

```text
Which part is the dictionary?
Which parts are lists?
```

### Practice Problem 7: Game Inventory

Create a file named `day-52/game_inventory.py`.

Goal:

```text
Store a player with health, coins, and inventory.
Use a potion if one is available.
Add coins.
Print a player summary.
```

Hint:

```text
The player is one dictionary.
The inventory can be another dictionary inside it.
```

Code:

```python
player = {
    "name": "Kai",
    "health": 70,
    "coins": 12,
    "inventory": {
        "potion": 2,
        "key": 1,
        "gem": 0
    }
}

if player["inventory"]["potion"] > 0:
    player["inventory"]["potion"] = player["inventory"]["potion"] - 1
    player["health"] = player["health"] + 20

player["coins"] = player["coins"] + 5

print("Player:", player["name"])
print("Health:", player["health"])
print("Coins:", player["coins"])
print("Inventory")

for item, quantity in player["inventory"].items():
    print(item + ":", quantity)
```

You should see:

```text
Player: Kai
Health: 90
Coins: 17
Inventory
potion: 1
key: 1
gem: 0
```

Try this:

```text
Set potion to 0.
Run the program again.
Health should stay at 70.
```

Debugging prompt:

```text
Why does reading the potion count need two keys?
```

## Try It Yourself

Choose one option and write it without looking back at the full solutions first.

### Option A: Contact Search

Create a file named `day-52/contact_search.py`.

Start with:

```python
contacts = [
    {"name": "Mina", "phone": "555-0104", "email": "mina@example.com"},
    {"name": "Sam", "phone": "555-0199", "email": "sam@example.com"},
    {"name": "Iris", "phone": "555-0130", "email": "iris@example.com"}
]

search_name = "Sam"
```

Rules:

```text
Loop through contacts.
If a contact's name matches search_name, print the phone and email.
Use a variable named found.
If no contact matches, print "Contact not found."
```

Hint:

```text
found should start as False before the loop.
Change it to True when you find the contact.
```

### Option B: Product Order

Create a file named `day-52/product_order.py`.

Start with:

```python
products = [
    {"name": "notebook", "price": 5},
    {"name": "pen", "price": 2},
    {"name": "folder", "price": 4}
]

cart = [
    {"name": "notebook", "quantity": 2},
    {"name": "pen", "quantity": 3}
]
```

Rules:

```text
Print each cart item.
Find the matching product price.
Calculate each item total.
Calculate the full cart total.
```

Hint:

```text
This uses two lists of dictionaries.
Start by looping through cart.
Inside that loop, search products for the matching name.
```

### Option C: Task Groups

Create a file named `day-52/task_groups.py`.

Start with:

```python
task_groups = {
    "school": ["read chapter", "solve worksheet"],
    "home": ["clean desk"],
    "practice": ["write Python code", "debug one program"]
}
```

Rules:

```text
Print each group name.
Print each task in that group.
Print the total number of tasks across all groups.
```

Hint:

```text
Loop through task_groups.items().
Each value is a list, so use a second loop for the tasks.
```

Choose the option that feels a little uncomfortable.

That is the best practice target.

## Common Mistake

Practice days are good days to notice habits that cause dictionary bugs.

### Mistake 1: Treating A Dictionary Like A List

Broken code:

```python
contact = {
    "name": "Mina",
    "phone": "555-0104"
}

print(contact[0])
```

This is broken because the dictionary does not have a key named `0`.

The data is labeled with `"name"` and `"phone"`.

Fixed code:

```python
contact = {
    "name": "Mina",
    "phone": "555-0104"
}

print(contact["name"])
```

You should see:

```text
Mina
```

Use indexes for lists.

Use keys for dictionaries.

### Mistake 2: Forgetting `.items()` When You Need Keys And Values

Broken code:

```python
inventory = {
    "notebook": 12,
    "pen": 3
}

for item, quantity in inventory:
    print(item + ":", quantity)
```

This is broken because looping through a dictionary directly gives one key at a time.

The loop is asking for two values, but Python is only giving one key.

Fixed code:

```python
inventory = {
    "notebook": 12,
    "pen": 3
}

for item, quantity in inventory.items():
    print(item + ":", quantity)
```

You should see:

```text
notebook: 12
pen: 3
```

Use `.items()` when you need both the key and the value.

### Mistake 3: Treating A List Of Dictionaries Like One Dictionary

Broken code:

```python
students = [
    {"name": "Asha", "score": 88},
    {"name": "Ben", "score": 52}
]

print(students["name"])
```

This is broken because `students` is a list.

The dictionaries are inside the list.

Fixed code:

```python
students = [
    {"name": "Asha", "score": 88},
    {"name": "Ben", "score": 52}
]

for student in students:
    print(student["name"])
```

You should see:

```text
Asha
Ben
```

Read from the outside in:

```text
students is a list.
student is one dictionary inside the list.
student["name"] reads one key from that dictionary.
```

### Mistake 4: Skipping A Level In Nested Data

Broken code:

```python
order = {
    "customer": "Mina",
    "items": [
        {"name": "notebook", "price": 5},
        {"name": "pen", "price": 2}
    ]
}

print(order["items"]["price"])
```

This is broken because `order["items"]` is a list.

A list needs an index or a loop before you can read a key from one item dictionary.

Fixed code:

```python
order = {
    "customer": "Mina",
    "items": [
        {"name": "notebook", "price": 5},
        {"name": "pen", "price": 2}
    ]
}

for item in order["items"]:
    print(item["name"] + ":", item["price"])
```

You should see:

```text
notebook: 5
pen: 2
```

When nested data feels confusing, pause and ask what each step returns.

### Mistake 5: Accidentally Appending A Whole List

Broken code:

```python
tasks = {
    "todo": ["write notes", "practice"],
    "done": []
}

tasks["done"].append(tasks["todo"])

print(tasks)
```

This code runs, but it does the wrong thing.

It appends the whole todo list inside the done list.

Fixed code:

```python
tasks = {
    "todo": ["write notes", "practice"],
    "done": []
}

finished_task = tasks["todo"].pop()
tasks["done"].append(finished_task)

print(tasks)
```

You should see:

```text
{'todo': ['write notes'], 'done': ['practice']}
```

If you want to move one value, save one value first.

## Debug It

These programs are intentionally broken or do not meet their stated goal. Read the goal first, find the problem, then compare with the fixed version.

### Debug 1: Contact Phone Update

Goal:

```text
Mina: 555-0104
Sam: 555-0200
```

Broken code:

```python
contacts = [
    {"name": "Mina", "phone": "555-0104"},
    {"name": "Sam", "phone": "555-0199"}
]

for contact in contacts:
    if contact["name"] == "Sam":
        contact["phones"] = "555-0200"

for contact in contacts:
    print(contact["name"] + ":", contact["phone"])
```

The problem:

```text
The update creates a new key named "phones" instead of changing "phone".
```

Fixed code:

```python
contacts = [
    {"name": "Mina", "phone": "555-0104"},
    {"name": "Sam", "phone": "555-0199"}
]

for contact in contacts:
    if contact["name"] == "Sam":
        contact["phone"] = "555-0200"

for contact in contacts:
    print(contact["name"] + ":", contact["phone"])
```

You should see:

```text
Mina: 555-0104
Sam: 555-0200
```

### Debug 2: Student Average

Goal:

```text
Average: 80.0
```

Broken code:

```python
students = [
    {"name": "Asha", "score": 90},
    {"name": "Ben", "score": 70}
]

total = 0

for student in students:
    total = total + student["score"]

average = total / len("students")

print("Average:", average)
```

The problem:

```text
len("students") counts the letters in the word "students".
The program needs len(students), the number of student dictionaries.
```

Fixed code:

```python
students = [
    {"name": "Asha", "score": 90},
    {"name": "Ben", "score": 70}
]

total = 0

for student in students:
    total = total + student["score"]

average = total / len(students)

print("Average:", average)
```

You should see:

```text
Average: 80.0
```

### Debug 3: Order Total

Goal:

```text
Total: 16
```

Broken code:

```python
order = {
    "items": [
        {"name": "notebook", "price": 5, "quantity": 2},
        {"name": "pen", "price": 2, "quantity": 3}
    ]
}

total = 0

for item in order:
    total = total + item["price"] * item["quantity"]

print("Total:", total)
```

The problem:

```text
Looping through order gives the dictionary keys.
The item dictionaries are inside order["items"].
```

Fixed code:

```python
order = {
    "items": [
        {"name": "notebook", "price": 5, "quantity": 2},
        {"name": "pen", "price": 2, "quantity": 3}
    ]
}

total = 0

for item in order["items"]:
    total = total + item["price"] * item["quantity"]

print("Total:", total)
```

You should see:

```text
Total: 16
```

### Debug 4: Playlist Duration

Goal:

```text
Total minutes: 7
```

Broken code:

```python
playlist = {
    "songs": [
        {"title": "Open Sky", "minutes": 3},
        {"title": "Quiet Keys", "minutes": 4}
    ]
}

total_minutes = 0

for song in playlist["songs"]:
    total_minutes = total_minutes + song["duration"]

print("Total minutes:", total_minutes)
```

The problem:

```text
The song dictionaries use the key "minutes", not "duration".
```

Fixed code:

```python
playlist = {
    "songs": [
        {"title": "Open Sky", "minutes": 3},
        {"title": "Quiet Keys", "minutes": 4}
    ]
}

total_minutes = 0

for song in playlist["songs"]:
    total_minutes = total_minutes + song["minutes"]

print("Total minutes:", total_minutes)
```

You should see:

```text
Total minutes: 7
```

### Debug 5: Game Inventory

Goal:

```text
Potions: 1
Health: 90
```

Broken code:

```python
player = {
    "health": 70,
    "inventory": {
        "potion": 2
    }
}

if player["inventory"]["potions"] > 0:
    player["inventory"]["potion"] = player["inventory"]["potion"] - 1
    player["health"] = player["health"] + 20

print("Potions:", player["inventory"]["potion"])
print("Health:", player["health"])
```

The problem:

```text
The inventory key is "potion", not "potions".
```

Fixed code:

```python
player = {
    "health": 70,
    "inventory": {
        "potion": 2
    }
}

if player["inventory"]["potion"] > 0:
    player["inventory"]["potion"] = player["inventory"]["potion"] - 1
    player["health"] = player["health"] + 20

print("Potions:", player["inventory"]["potion"])
print("Health:", player["health"])
```

You should see:

```text
Potions: 1
Health: 90
```

When debugging dictionary data, ask:

- What is the outer collection?
- What does one loop step give me?
- Is this value a dictionary, a list, or a simple value?
- Did I spell the key exactly?
- Am I using `.items()` when I need both parts?
- Am I changing the correct key?

## Read the Docs

Today, revisit Python's official dictionary documentation:

```text
https://docs.python.org/3/library/stdtypes.html#mapping-types-dict
```

You do not need to read the whole page.

Look for these ideas:

```text
d[key]
d[key] = value
key in d
d.get(key, default)
d.keys()
d.values()
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

Those list methods matter because many dictionary values can be lists.

Try this small documentation-style practice:

```python
task_board = {
    "todo": ["write notes"],
    "done": []
}

if "todo" in task_board:
    task = task_board["todo"].pop()
    task_board["done"].append(task)

print(list(task_board.keys()))
print(list(task_board.values()))
print(list(task_board.items()))
```

You should see:

```text
['todo', 'done']
[[], ['write notes']]
[('todo', []), ('done', ['write notes'])]
```

Read documentation with one question in mind:

```text
What does this operation need, and what does it give back?
```

That question works for dictionaries, lists, and nested data.

## Mini Challenge

Create a file named:

```text
day-52/data_modeling_practice.py
```

Build a small personal dashboard from several data shapes.

Your program should include:

- a contact book as a list of dictionaries
- a task board as a dictionary of lists
- a playlist as a dictionary with a list of song dictionaries
- a game player as a dictionary with a nested inventory dictionary

Rules:

```text
Print all contact names.
Move one task from todo to done.
Print the number of tasks in each task group.
Print each song title and the total playlist minutes.
Use one potion if the player has one.
Print the player's health and remaining potions.
```

One possible solution:

```python
contacts = [
    {"name": "Mina", "phone": "555-0104"},
    {"name": "Sam", "phone": "555-0199"}
]

task_board = {
    "todo": ["practice dictionaries", "review mistakes"],
    "done": ["read lesson"]
}

playlist = {
    "name": "Practice Mix",
    "songs": [
        {"title": "Open Sky", "minutes": 3},
        {"title": "Quiet Keys", "minutes": 4}
    ]
}

player = {
    "name": "Kai",
    "health": 70,
    "inventory": {
        "potion": 1,
        "key": 1
    }
}

print("Contacts")

for contact in contacts:
    print("-", contact["name"])

completed_task = task_board["todo"].pop(0)
task_board["done"].append(completed_task)

print("Tasks")

for status, tasks in task_board.items():
    print(status + ":", len(tasks))

total_minutes = 0

print("Playlist:", playlist["name"])

for song in playlist["songs"]:
    total_minutes = total_minutes + song["minutes"]
    print("-", song["title"])

print("Total minutes:", total_minutes)

if player["inventory"]["potion"] > 0:
    player["inventory"]["potion"] = player["inventory"]["potion"] - 1
    player["health"] = player["health"] + 20

print("Player:", player["name"])
print("Health:", player["health"])
print("Potions:", player["inventory"]["potion"])
```

You should see:

```text
Contacts
- Mina
- Sam
Tasks
todo: 1
done: 2
Playlist: Practice Mix
- Open Sky
- Quiet Keys
Total minutes: 7
Player: Kai
Health: 90
Potions: 0
```

After it works, change the data without changing the loops:

```text
Add another contact.
Add another todo task.
Add another song.
Set potion to 0 and run again.
```

The program should still make sense.

That is a sign that the data model is doing its job.

## Real-World Use

Real programs spend a lot of time shaping data.

A contact book may use:

```text
a list of contact dictionaries
```

A school report may use:

```text
a list of student dictionaries
```

A store may use:

```text
a list of product dictionaries
an order dictionary
a list of item dictionaries inside the order
```

A task app may use:

```text
a dictionary where each status points to a list of tasks
```

A game may use:

```text
a player dictionary
a nested inventory dictionary
```

The code becomes easier to read when the shape matches the real thing.

For example, this is harder to understand:

```python
student = ["Asha", 88, True]

print(student[0])
print(student[1])
```

You should see:

```text
Asha
88
```

This is easier to understand:

```python
student = {
    "name": "Asha",
    "score": 88,
    "passed": True
}

print(student["name"])
print(student["score"])
```

You should see:

```text
Asha
88
```

The dictionary version carries the meaning with the data.

That matters when programs grow.

Tomorrow, when you refactor old code, look for data that would be clearer with names:

```text
old code has many separate variables
old code repeats the same print pattern
old code uses indexes that are hard to remember
old code has several similar records
```

Those are signs that a better data shape may make the code easier to clean up.

## Recap

Today you practiced data modeling with dictionaries.

You reviewed:

- creating dictionaries
- reading values with keys
- updating values
- looping with `.keys()`, `.values()`, and `.items()`
- storing several records as a list of dictionaries
- grouping lists inside a dictionary
- reading nested data one step at a time
- modeling contacts, students, products, orders, playlists, tasks, and game inventory
- debugging misspelled keys
- debugging loops that use the wrong shape
- choosing data structures before writing the full program

The main choices were:

```text
One thing with named details:
dictionary

Many similar things:
list of dictionaries

Named groups of many values:
dictionary of lists

Details inside details:
nested dictionaries and lists
```

When you feel stuck, ask:

```text
What am I holding right now?
What key or index gets me one step closer?
What should one record look like?
```

Those questions are often enough to get moving again.

## Lesson Checklist

Before moving on, check that you can:

- create a dictionary for one real-world thing
- choose clear string keys
- read a value with `dictionary["key"]`
- use `get()` when a key might be missing
- update an existing value
- add a new key-value pair
- loop through a dictionary with `.items()`
- explain why a list of dictionaries stores many similar records
- loop through a list of dictionaries
- explain why a dictionary of lists groups values by name
- update a list stored inside a dictionary
- read nested data one level at a time
- calculate a total from nested item dictionaries
- debug a misspelled key
- debug code that treats a list like a dictionary
- debug code that treats a dictionary like a list
- explain why useful data shapes make refactoring easier

## Exercises

### Exercise 1

Create a dictionary named `contact`.

It should store:

```text
name: Dev
phone: 555-0120
email: dev@example.com
favorite: False
```

Print the contact's name and email.

### Exercise 2

Update the `favorite` value from Exercise 1 to `True`.

Print the whole dictionary.

### Exercise 3

Create a dictionary named `product`.

It should store:

```text
name: pencil
price: 1
stock: 20
```

Reduce the stock by `3`.

Print:

```text
pencil stock: 17
```

### Exercise 4

Loop through this dictionary with `.items()`:

```python
settings = {
    "theme": "dark",
    "autosave": True,
    "font_size": "medium"
}
```

Print each setting and value.

### Exercise 5

Create a list named `students`.

It should contain three student dictionaries.

Each dictionary should have:

```text
name
score
```

Loop through the list and print each student's name.

### Exercise 6

Use the `students` list from Exercise 5.

Print only students with a score of at least `80`.

### Exercise 7

Add a `passed` key to each student.

The value should be `True` when the score is at least `60`.

Print the final list.

### Exercise 8

Create this dictionary of lists:

```python
tasks = {
    "todo": ["read", "practice"],
    "done": []
}
```

Move `"read"` from `todo` to `done`.

Print the final dictionary.

### Exercise 9

Create a playlist dictionary with:

```text
name
songs
```

The `songs` value should be a list of at least three song dictionaries.

Each song should have:

```text
title
artist
minutes
```

Print each song title.

### Exercise 10

Use the playlist from Exercise 9.

Calculate and print the total minutes.

### Exercise 11

Create this order:

```python
order = {
    "customer": "Iris",
    "items": [
        {"name": "marker", "price": 3, "quantity": 2},
        {"name": "folder", "price": 4, "quantity": 1}
    ]
}
```

Calculate the total.

You should get:

```text
Total: 10
```

### Exercise 12

Fix the broken code.

Broken code:

```python
profile = {
    "name": "Mina",
    "city": "Pune"
}

print(profile[0])
```

The goal is to print the name.

### Exercise 13

Fix the broken code.

Broken code:

```python
scores = {
    "Asha": 9,
    "Ben": 7
}

for student, score in scores:
    print(student + ":", score)
```

The goal is to print each student and score.

### Exercise 14

Fix the broken code.

Broken code:

```python
students = [
    {"name": "Asha", "score": 88},
    {"name": "Ben", "score": 52}
]

print(students["score"])
```

The goal is to print each score.

### Exercise 15

Fix the broken code.

Broken code:

```python
player = {
    "inventory": {
        "potion": 2
    }
}

player["inventory"]["potions"] = player["inventory"]["potions"] - 1

print(player)
```

The goal is to reduce the `"potion"` count by `1`.

### Exercise 16

Choose the best data shape for each situation.

Write one sentence explaining your choice.

```text
One contact with name, phone, and email.
Many contacts.
Tasks grouped by todo, doing, and done.
One order with many item records.
A game player with health and inventory.
A playlist with a name and many songs.
```

Use these choices:

```text
dictionary
list of dictionaries
dictionary of lists
nested dictionaries and lists
```

### Exercise 17

Build a small game inventory.

Start with:

```python
player = {
    "name": "Nia",
    "health": 50,
    "inventory": {
        "potion": 1,
        "coin": 10
    }
}
```

Rules:

```text
If potion is greater than 0, use one potion.
Using a potion adds 25 health.
Add 5 coins.
Print the final player dictionary.
```

### Exercise 18

Write a small data model from scratch for a library checkout.

It should include:

```text
a member name
a list of borrowed books
each borrowed book should have title, due_day, and renewed
```

Then print each borrowed book title.

### Exercise 19

Choose one old program from earlier in the course.

Without changing it yet, write answers to these questions:

```text
What data does the program store?
Is any data repeated?
Would a dictionary make any value clearer?
Would a list of dictionaries remove repeated variables?
Which part would be easiest to clean up tomorrow?
```

This prepares you for the refactor day.

## Tiny Win

You practiced thinking about the shape of data before rushing into code.

That is a real programming skill.

When the data shape is clear, the code usually becomes easier to write:

```text
one record
many records
named groups
nested details
```

You do not need to get the perfect model on the first try.

You only need to get better at asking what the data really is.

## Tomorrow

Tomorrow is:

```text
Day 53: Refactor Day: Clean Up Old Code
```

Today you practiced choosing data shapes.

Tomorrow you will use that skill to improve old programs.

You will look for code that can be clearer, smaller, or easier to change.

Useful questions for tomorrow:

```text
Can repeated variables become a list?
Can mystery indexes become dictionary keys?
Can repeated print lines become a loop?
Can a messy section be cleaned one small step at a time?
```

Refactoring is not starting over.

It is taking working code and making it easier to understand.
