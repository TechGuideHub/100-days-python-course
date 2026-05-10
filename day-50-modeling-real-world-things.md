# Day 50: Modeling Real-World Things

**Focus:** Turning real-world things into clear Python data  
**You will practice:** choosing dictionaries, lists, tuples, and sets for attributes, repeated items, fixed values, unique values, and relationships  
**Estimated time:** 45-60 minutes

## Today's Goal

Today you will practice modeling real-world things with the Python data types you already know.

A contact, book, task, product, order, student, playlist, or game character can all be described with data.

The question is:

```text
What shape should that data have?
```

By the end of this lesson, you should be able to:

- identify the one thing your program is describing
- choose dictionary keys for the thing's attributes
- use a list when a thing has repeated items
- use a tuple when a small group of values has a fixed shape
- use a set when unique values matter
- represent simple relationships between things
- move from a plain description to Python data step by step
- avoid vague keys, inconsistent keys, and list shapes that hide meaning

You are not learning classes yet.

For now, real-world modeling means using the tools you already have:

```text
dictionary
list
tuple
set
```

The goal is not to model every detail.

The goal is to choose enough clear data for the program you are writing.

## The Big Idea

A real-world thing becomes Python data when you choose what the program needs to remember.

Start with a contact.

Description:

```text
Sam is a contact.
Sam has a phone number and an email address.
Sam has the tags friend, school, and friend.
```

The one main thing is:

```text
contact
```

The named facts about the contact are:

```text
name
phone
email
tags
```

A dictionary fits because the contact has labeled information.

Code:

```python
contact = {
    "name": "Sam",
    "phone": "555-0104",
    "email": "sam@example.com",
    "tags": {"friend", "school", "friend"}
}

print(contact["name"])
print(contact["phone"])
print(sorted(contact["tags"]))
```

You should see:

```text
Sam
555-0104
['friend', 'school']
```

The set removes the repeated `"friend"` tag because tags should usually be unique.

Now look at a book.

Description:

```text
Python Notes is a book.
It has one title, one author, 120 pages, and several topics.
```

Code:

```python
book = {
    "title": "Python Notes",
    "author": "Mina Patel",
    "pages": 120,
    "topics": ["variables", "loops", "dictionaries"]
}

print(book["title"])
print("Topic count:", len(book["topics"]))
print("First topic:", book["topics"][0])
```

You should see:

```text
Python Notes
Topic count: 3
First topic: variables
```

The book is one thing, so it is a dictionary.

The topics are many values of the same kind, so they are a list.

Now look at a product.

Description:

```text
A notebook product has a name, price, stock count, fixed dimensions, and unique labels.
```

Code:

```python
product = {
    "name": "Notebook",
    "price": 3.5,
    "stock": 12,
    "dimensions_cm": (21, 14),
    "labels": {"school", "paper", "school"}
}

height = product["dimensions_cm"][0]
width = product["dimensions_cm"][1]

print(product["name"])
print("Height:", height)
print("Width:", width)
print("Labels:", sorted(product["labels"]))
```

You should see:

```text
Notebook
Height: 21
Width: 14
Labels: ['paper', 'school']
```

The product is a dictionary.

The dimensions are a tuple because there are exactly two values and their positions mean something:

```text
position 0 -> height
position 1 -> width
```

The labels are a set because duplicates are not useful.

## The Mental Model

When you model something, ask six questions.

Question 1:

```text
What is the main thing?
```

If the program is about one task, make one task dictionary.

Code:

```python
task = {
    "title": "Review dictionary notes",
    "done": False,
    "priority": "medium"
}

print(task["title"])
print(task["done"])
```

You should see:

```text
Review dictionary notes
False
```

Question 2:

```text
What are its attributes?
```

Attributes are named facts about the thing.

For a task, attributes might be:

```text
title
done
priority
due_date
```

For a student, attributes might be:

```text
name
level
scores
completed_topics
```

Question 3:

```text
Does one attribute contain repeated items?
```

Use a list for repeated items when order or duplicates may matter.

Code:

```python
student = {
    "name": "Maya",
    "level": 3,
    "scores": [8, 10, 9]
}

print(student["name"])
print("Latest score:", student["scores"][-1])
```

You should see:

```text
Maya
Latest score: 9
```

The scores are a list because there can be many scores.

The order matters because the latest score is at the end.

Question 4:

```text
Does a small group of values have a fixed shape?
```

Use a tuple when the number of values is fixed and the positions have meaning.

Code:

```python
game_character = {
    "name": "Nia",
    "position": (4, 9)
}

x = game_character["position"][0]
y = game_character["position"][1]

print("x:", x)
print("y:", y)
```

You should see:

```text
x: 4
y: 9
```

The position is a tuple because it is always two values:

```text
x position
y position
```

Question 5:

```text
Should duplicates disappear?
```

Use a set when each value should appear once.

Code:

```python
playlist = {
    "name": "Focus Mix",
    "artists": {"Asha Rao", "Ben Lee", "Asha Rao"}
}

print(playlist["name"])
print(sorted(playlist["artists"]))
```

You should see:

```text
Focus Mix
['Asha Rao', 'Ben Lee']
```

The set keeps each artist name once.

Question 6:

```text
Does one thing contain or point to other things?
```

That is a relationship.

An order has many order items.

Code:

```python
order = {
    "order_id": "A100",
    "items": [
        {"name": "Notebook", "quantity": 2},
        {"name": "Pen", "quantity": 3}
    ]
}

print("Order:", order["order_id"])
print("Item count:", len(order["items"]))
print("First item:", order["items"][0]["name"])
```

You should see:

```text
Order: A100
Item count: 2
First item: Notebook
```

The order is one dictionary.

The `"items"` value is a list because there can be many items.

Each item inside the list is another dictionary because each item has its own named facts.

This is the main modeling pattern:

```text
dictionary for one described thing
list for many things
tuple for a fixed small group
set for unique values
```

## Try It Yourself

Create a file named:

```text
day-50/modeling_data.py
```

You will build several small data models.

### Step 1: Start With A Student

Description:

```text
Maya is a student.
Maya is on level 3.
Maya has scores 8, 10, and 9.
Maya has completed lists, dictionaries, and lists.
```

Code:

```python
student = {
    "name": "Maya",
    "level": 3,
    "scores": [8, 10, 9],
    "completed_topics": {"lists", "dictionaries", "lists"}
}

print(student["name"])
print("Level:", student["level"])
print("Latest score:", student["scores"][-1])
print("Completed topics:", sorted(student["completed_topics"]))
```

You should see:

```text
Maya
Level: 3
Latest score: 9
Completed topics: ['dictionaries', 'lists']
```

The student is one thing, so use a dictionary.

The scores are repeated values, so use a list.

The completed topics should be unique, so use a set.

### Step 2: Model A Product

Description:

```text
A notebook product has a name, price, stock count, fixed dimensions, and labels.
```

Code:

```python
product = {
    "name": "Notebook",
    "price": 3.5,
    "stock": 12,
    "dimensions_cm": (21, 14),
    "labels": {"school", "paper", "school"}
}

height = product["dimensions_cm"][0]
width = product["dimensions_cm"][1]

print(product["name"])
print("Price:", product["price"])
print("Stock:", product["stock"])
print("Height:", height)
print("Width:", width)
print("Labels:", sorted(product["labels"]))
```

You should see:

```text
Notebook
Price: 3.5
Stock: 12
Height: 21
Width: 14
Labels: ['paper', 'school']
```

The dimensions are a tuple because there are exactly two values in a fixed order.

### Step 3: Model An Order

Description:

```text
Order A100 belongs to Maya.
It has two items.
Each item has a name, quantity, and price.
The order status is paid.
```

Code:

```python
order = {
    "order_id": "A100",
    "customer": "Maya",
    "items": [
        {"name": "Notebook", "quantity": 2, "price": 3.5},
        {"name": "Pen", "quantity": 3, "price": 1.25}
    ],
    "status": "paid"
}

total = 0

for item in order["items"]:
    total = total + item["quantity"] * item["price"]

print("Order:", order["order_id"])
print("Customer:", order["customer"])
print("Items:", len(order["items"]))
print("Total:", total)
```

You should see:

```text
Order: A100
Customer: Maya
Items: 2
Total: 10.75
```

The order is one thing.

The items are many things inside the order.

That is why `"items"` is a list of dictionaries.

### Step 4: Model A Playlist

Description:

```text
A playlist has a name, a list of songs, unique favorite song IDs, and a fixed current position.
```

Code:

```python
playlist = {
    "name": "Focus Mix",
    "songs": ["First Light", "Clean Lines", "Small Steps"],
    "favorite_song_ids": {101, 103, 101},
    "current_position": (0, 42)
}

print(playlist["name"])
print("First song:", playlist["songs"][0])
print("Song count:", len(playlist["songs"]))
print("Favorites:", sorted(playlist["favorite_song_ids"]))
print("Position:", playlist["current_position"])
```

You should see:

```text
Focus Mix
First song: First Light
Song count: 3
Favorites: [101, 103]
Position: (0, 42)
```

The songs are a list because order matters.

The favorite song IDs are a set because the same song should not be saved twice as a favorite.

The current position is a tuple because it has a fixed shape:

```text
song index
seconds into the song
```

### Step 5: Model A Game Character

Description:

```text
Nia is a game character.
Nia has a level, health, position, inventory, and skills.
```

Code:

```python
character = {
    "name": "Nia",
    "level": 5,
    "health": 80,
    "position": (4, 9),
    "inventory": ["map", "key"],
    "skills": {"jump", "dash", "jump"}
}

print(character["name"])
print("Health:", character["health"])
print("Position:", character["position"])
print("Inventory:", character["inventory"])
print("Skills:", sorted(character["skills"]))
```

You should see:

```text
Nia
Health: 80
Position: (4, 9)
Inventory: ['map', 'key']
Skills: ['dash', 'jump']
```

The character is a dictionary.

The inventory is a list because the character can carry several things.

The skills are a set because learning `"jump"` twice should still count as one skill.

## Common Mistake

### Mistake 1: Modeling Too Much At Once

This code may run, but it is trying to hold more than the current program needs.

Broken code:

```python
student = {
    "name": "Maya",
    "level": 3,
    "scores": [8, 10, 9],
    "home_address": {
        "street": "18 Lake Road",
        "city": "Pune",
        "postal_code": "411001"
    },
    "family_contacts": [
        {"name": "Anil", "phone": "555-0111"},
        {"name": "Rita", "phone": "555-0112"}
    ],
    "medical_notes": ["allergy note", "doctor note"]
}

print(student["name"])
```

The problem is not syntax.

The problem is that a simple score program probably does not need addresses, family contacts, and medical notes.

Start smaller.

Fixed code:

```python
student = {
    "name": "Maya",
    "level": 3,
    "scores": [8, 10, 9]
}

print(student["name"])
print("Scores:", student["scores"])
```

You should see:

```text
Maya
Scores: [8, 10, 9]
```

Add more details only when the program has a real reason to use them.

### Mistake 2: Using Vague Key Names

Broken code:

```python
product = {
    "n": "Notebook",
    "p": 3.5,
    "s": 12
}

print(product["price"])
```

This is broken because the dictionary does not have a `"price"` key.

It has a vague key named `"p"`.

Fixed code:

```python
product = {
    "name": "Notebook",
    "price": 3.5,
    "stock": 12
}

print(product["price"])
```

You should see:

```text
3.5
```

Clear keys make the data easier to read and harder to misuse.

### Mistake 3: Using Inconsistent Keys

Broken code:

```python
students = [
    {"name": "Maya", "score": 88},
    {"student_name": "Noah", "score": 95}
]

for student in students:
    print(student["name"], student["score"])
```

This is broken because the second dictionary uses `"student_name"` instead of `"name"`.

The loop expects every student dictionary to have the same basic shape.

Fixed code:

```python
students = [
    {"name": "Maya", "score": 88},
    {"name": "Noah", "score": 95}
]

for student in students:
    print(student["name"], student["score"])
```

You should see:

```text
Maya 88
Noah 95
```

When a list holds several dictionaries of the same kind, keep their keys consistent.

### Mistake 4: Using A List When A Dictionary Is Clearer

This code runs, but the meaning is hidden in positions.

Broken code:

```python
contact = ["Sam", "555-0104", "sam@example.com"]

print(contact[2])
```

You should see:

```text
sam@example.com
```

The program works, but you have to remember that position `2` means email.

That is fragile.

Fixed code:

```python
contact = {
    "name": "Sam",
    "phone": "555-0104",
    "email": "sam@example.com"
}

print(contact["email"])
```

You should see:

```text
sam@example.com
```

Use a dictionary when each value needs a label.

## Debug It

Read each broken program. Decide whether the problem is syntax, shape, or key choice. Then compare it with the fixed version.

### Debug 1: Product Price

The program should print the product price.

Broken code:

```python
product = ["Notebook", 3.5, True]

print(product["price"])
```

The problem:

```text
The product is stored as a list, but the code tries to read it like a dictionary.
```

Fixed code:

```python
product = {
    "name": "Notebook",
    "price": 3.5,
    "in_stock": True
}

print(product["price"])
```

You should see:

```text
3.5
```

### Debug 2: Task Tags

The program should show each tag only once.

Broken code:

```python
task = {
    "title": "Review notes",
    "tags": ["python", "review", "python"]
}

print(task["tags"])
```

The problem:

```text
The code uses a list, so duplicate tags stay in the data.
```

Fixed code:

```python
task = {
    "title": "Review notes",
    "tags": {"python", "review", "python"}
}

print(sorted(task["tags"]))
```

You should see:

```text
['python', 'review']
```

Use a set when duplicates should disappear.

### Debug 3: Student Report

The program should print every student's name and score.

Broken code:

```python
students = [
    {"name": "Maya", "score": 88},
    {"student": "Noah", "score": 95},
    {"name": "Iris", "score": 91}
]

for student in students:
    print(student["name"] + ":", student["score"])
```

The problem:

```text
One dictionary uses "student" while the others use "name".
```

Fixed code:

```python
students = [
    {"name": "Maya", "score": 88},
    {"name": "Noah", "score": 95},
    {"name": "Iris", "score": 91}
]

for student in students:
    print(student["name"] + ":", student["score"])
```

You should see:

```text
Maya: 88
Noah: 95
Iris: 91
```

Consistent keys make loops much easier.

### Debug 4: Order Items

The program should count two order items.

Broken code:

```python
order = {
    "order_id": "A100",
    "items": "Notebook, Pen"
}

print("Items:", len(order["items"]))
```

The problem:

```text
The items are stored as one string, so len() counts characters, not order items.
```

Fixed code:

```python
order = {
    "order_id": "A100",
    "items": [
        {"name": "Notebook", "quantity": 2},
        {"name": "Pen", "quantity": 3}
    ]
}

print("Items:", len(order["items"]))
```

You should see:

```text
Items: 2
```

Use a list when a thing contains several smaller things.

## Read the Docs

Today, look at Python's official documentation for built-in types:

```text
https://docs.python.org/3/library/stdtypes.html
```

You do not need to read the whole page.

Search for these sections:

```text
Sequence Types
Mapping Types
Set Types
```

Connect the documentation names to the shapes from today:

```text
list  -> a mutable sequence
tuple -> an immutable sequence
dict  -> a mapping type
set   -> an unordered collection of distinct values
```

The documentation uses formal words.

Translate them into working questions:

```text
Sequence: Do I have several values in order?
Mapping: Do I have labels pointing to values?
Distinct: Do I want each value only once?
```

That is enough for today.

Documentation becomes easier when you connect the official wording to examples you already understand.

## Mini Challenge

Create a file named:

```text
day-50/reading_order_model.py
```

Build a small model for a book order.

Start with this description:

```text
A customer orders two books.
Each book has a title, author, price, and topics.
The order has an ID, customer name, shipping city, and status.
The order also keeps a set of unique labels.
```

Your program should create one dictionary named `book_order`.

It should include:

- `"order_id"` as a string
- `"customer"` as a string
- `"shipping_city"` as a string
- `"status"` as a string
- `"labels"` as a set
- `"books"` as a list of book dictionaries

One possible version:

```python
book_order = {
    "order_id": "B200",
    "customer": "Ravi",
    "shipping_city": "Hyderabad",
    "status": "packed",
    "labels": {"books", "gift", "books"},
    "books": [
        {
            "title": "Python Notes",
            "author": "Mina Patel",
            "price": 12,
            "topics": ["variables", "loops"]
        },
        {
            "title": "Data Practice",
            "author": "Sam Lee",
            "price": 15,
            "topics": ["lists", "dictionaries"]
        }
    ]
}

total = 0

for book in book_order["books"]:
    total = total + book["price"]

print("Order:", book_order["order_id"])
print("Customer:", book_order["customer"])
print("Books:", len(book_order["books"]))
print("Labels:", sorted(book_order["labels"]))
print("Total:", total)
```

You should see:

```text
Order: B200
Customer: Ravi
Books: 2
Labels: ['books', 'gift']
Total: 27
```

After it works, add one more book dictionary to the `"books"` list.

Run the program again.

The book count and total should change without rewriting the loop.

## Real-World Use

Real programs spend a lot of time choosing data shapes.

A contact book might use a list of contact dictionaries:

```python
contacts = [
    {"name": "Sam", "phone": "555-0104", "email": "sam@example.com"},
    {"name": "Maya", "phone": "555-0188", "email": "maya@example.com"}
]

print(contacts[0]["email"])
```

You should see:

```text
sam@example.com
```

A task app might use a list of task dictionaries:

```python
tasks = [
    {"title": "Read lesson", "done": True, "labels": {"python", "study"}},
    {"title": "Solve exercises", "done": False, "labels": {"practice"}}
]

for task in tasks:
    print(task["title"], task["done"])
```

You should see:

```text
Read lesson True
Solve exercises False
```

A store might use products and orders:

```python
product = {
    "name": "Water Bottle",
    "price": 12,
    "stock": 15,
    "categories": {"outdoor", "school"}
}

order = {
    "order_id": "A101",
    "items": [
        {"name": "Water Bottle", "quantity": 1, "price": 12}
    ]
}

print(product["name"])
print(order["items"][0]["quantity"])
```

You should see:

```text
Water Bottle
1
```

A game might store a character:

```python
character = {
    "name": "Kai",
    "health": 70,
    "position": (2, 5),
    "inventory": ["coin", "torch"],
    "skills": {"jump", "climb"}
}

print(character["position"])
print(sorted(character["skills"]))
```

You should see:

```text
(2, 5)
['climb', 'jump']
```

In all of these examples, the code is easier to read because the data shape matches the thing being described.

## Recap

Today you practiced modeling real-world things with Python data.

Use a dictionary when:

- you have one thing
- the thing has named attributes
- you want labels like `"name"`, `"price"`, `"email"`, or `"status"`

Use a list when:

- you have many values of the same kind
- order matters
- duplicates might be meaningful

Use a tuple when:

- you have a small fixed group of values
- the positions have a clear meaning
- the shape should not grow or shrink

Use a set when:

- each value should appear once
- order does not matter
- membership checks are important

Ask these modeling questions:

```text
What is the main thing?
What does the program need to know about it?
Which facts need labels?
Which facts can repeat?
Which facts have a fixed position?
Which facts should be unique?
Does this thing contain other things?
```

Good data modeling is mostly careful naming and choosing the simplest useful shape.

## Lesson Checklist

Before moving on, check that you can:

- turn a short description into a dictionary
- choose clear dictionary keys
- use a list for repeated items
- use a tuple for a fixed pair like a position or dimensions
- use a set for unique tags, labels, topics, or skills
- model a contact, book, task, product, order, student, playlist, and game character
- explain why a list of dictionaries is useful for several records
- explain why consistent keys matter inside a list of dictionaries
- spot when a list hides meaning that a dictionary should label
- keep a model small until the program needs more detail

## Exercises

### Exercise 1

Model this contact as a dictionary:

```text
name: Dev
phone: 555-0120
email: dev@example.com
tags: friend, school, friend
```

Use a set for the tags.

Print the email and the sorted tags.

### Exercise 2

Model this book:

```text
title: Clean Python
author: Asha Rao
pages: 180
topics: strings, lists, dictionaries
```

Use a list for the topics.

Print the title and the number of topics.

### Exercise 3

Model a task with these attributes:

```text
title
done
priority
labels
```

Use a Boolean for `done`.

Use a set for `labels`.

### Exercise 4

Model a product with:

```text
name
price
stock
dimensions_cm
labels
```

Use a tuple for `dimensions_cm`.

Use a set for `labels`.

### Exercise 5

Model an order with:

```text
order_id
customer
items
status
```

Make `items` a list of dictionaries.

Each item dictionary should have:

```text
name
quantity
price
```

Print the order ID and item count.

### Exercise 6

Model a student with:

```text
name
level
scores
completed_topics
```

Use a list for scores.

Use a set for completed topics.

Print the latest score.

### Exercise 7

Model a playlist with:

```text
name
songs
favorite_song_ids
current_position
```

Use a list for songs.

Use a set for favorite song IDs.

Use a tuple for current position.

### Exercise 8

Model a game character with:

```text
name
level
health
position
inventory
skills
```

Use a tuple for position.

Use a list for inventory.

Use a set for skills.

### Exercise 9

Choose `dict`, `list`, `tuple`, or `set` for each situation.

```text
A product with a name, price, and stock count.
A playlist where song order matters.
A position with x and y values.
A group of unique tags.
A list of student records.
A contact with phone and email.
```

Write one sentence explaining each choice.

### Exercise 10

Fix the vague keys.

Broken code:

```python
book = {
    "t": "Python Notes",
    "p": 120
}

print(book["pages"])
```

Rewrite the dictionary with clearer keys.

### Exercise 11

Fix the inconsistent keys.

Broken code:

```python
tasks = [
    {"title": "Read lesson", "done": True},
    {"task_title": "Practice", "done": False}
]

for task in tasks:
    print(task["title"])
```

Make both task dictionaries use the same keys.

### Exercise 12

Turn this description into Python data:

```text
Kai is a student.
Kai is on level 4.
Kai has scores 7, 9, and 10.
Kai has completed loops, lists, and loops.
Kai has a favorite study location stored as city and country.
```

Use:

- a dictionary for the student
- a list for scores
- a set for completed topics
- a tuple for the study location

Print the student's name, latest score, sorted completed topics, and study location.

## Tiny Win

You can now look at a real-world thing and choose a useful Python shape for it.

That is a practical skill.

Programs become easier to write when the data already makes sense:

```text
contact["email"]
student["scores"]
product["dimensions_cm"]
order["items"]
character["skills"]
```

Clear data shapes lead to clearer code.

## Tomorrow

Tomorrow is:

```text
Day 51: Common Dictionary Mistakes
```

Today you focused on choosing the shape of the data.

Tomorrow you will slow down on dictionary mistakes that happen once the shape exists:

```text
misspelled keys
missing keys
wrong key names
mixing up keys and indexes
changing one dictionary shape but not another
```

That practice will make today's models easier to read, debug, and trust.
