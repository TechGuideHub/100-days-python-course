# Day 47: Lists of Dictionaries

**Focus:** Storing many similar records with a list of dictionaries  
**You will practice:** creating a list of dictionaries, reading one record, looping through records, printing selected fields, adding a new dictionary, and spotting common nested-data mistakes  
**Estimated time:** 45-55 minutes

## Today's Goal

Today you will put two familiar ideas together:

```text
lists
dictionaries
```

A dictionary is useful for describing one thing:

```python
student = {
    "name": "Maya",
    "score": 88,
    "passed": True
}
```

A list is useful for storing many things:

```python
students = ["Maya", "Noah", "Iris"]
```

A list of dictionaries lets you store many complete records:

```python
students = [
    {"name": "Maya", "score": 88, "passed": True},
    {"name": "Noah", "score": 95, "passed": True},
    {"name": "Iris", "score": 71, "passed": True}
]
```

By the end of this lesson, you should be able to:

- create a list that contains dictionaries
- explain why each dictionary is one record
- read one dictionary from the list
- read one value from one dictionary
- loop through all records
- print selected fields from each record
- add a new dictionary to the list with `append()`
- avoid common mistakes with commas, keys, indexes, and brackets

The main idea is:

```text
A list of dictionaries stores many similar records.
```

Tomorrow you will see the related pattern:

```text
dictionaries of lists
```

Today, each item in the list is a dictionary.

## The Big Idea

Start with one contact:

```python
contact = {
    "name": "Sam",
    "phone": "555-0104",
    "email": "sam@example.com"
}

print(contact["name"])
```

You should see:

```text
Sam
```

That works for one contact.

But a contact book needs several contacts.

Code:

```python
contacts = [
    {
        "name": "Sam",
        "phone": "555-0104",
        "email": "sam@example.com"
    },
    {
        "name": "Mina",
        "phone": "555-0188",
        "email": "mina@example.com"
    },
    {
        "name": "Dev",
        "phone": "555-0120",
        "email": "dev@example.com"
    }
]

print(contacts)
```

You should see:

```text
[{'name': 'Sam', 'phone': '555-0104', 'email': 'sam@example.com'}, {'name': 'Mina', 'phone': '555-0188', 'email': 'mina@example.com'}, {'name': 'Dev', 'phone': '555-0120', 'email': 'dev@example.com'}]
```

The output is long, but the shape is simple:

```text
contacts is a list.
Each item inside contacts is a dictionary.
Each dictionary describes one contact.
```

You can write the same structure more compactly:

```python
contacts = [
    {"name": "Sam", "phone": "555-0104", "email": "sam@example.com"},
    {"name": "Mina", "phone": "555-0188", "email": "mina@example.com"},
    {"name": "Dev", "phone": "555-0120", "email": "dev@example.com"}
]
```

Both versions work.

The taller version is often easier while you are learning because every dictionary is easier to see.

## The Mental Model

Think of a list of dictionaries as a stack of record cards.

One card:

```text
name: Sam
phone: 555-0104
email: sam@example.com
```

Several cards together:

```text
contacts

0 -> name: Sam
     phone: 555-0104
     email: sam@example.com

1 -> name: Mina
     phone: 555-0188
     email: mina@example.com

2 -> name: Dev
     phone: 555-0120
     email: dev@example.com
```

The list uses indexes:

```python
contacts[0]
contacts[1]
contacts[2]
```

Each dictionary uses keys:

```python
contacts[0]["name"]
contacts[1]["phone"]
contacts[2]["email"]
```

Read this line slowly:

```python
contacts[0]["name"]
```

It means:

```text
Go to the contacts list.
Get item 0.
That item is a dictionary.
From that dictionary, get the value for "name".
```

The list answers:

```text
Which record?
```

The dictionary answers:

```text
Which field inside that record?
```

## Try It Yourself

Create a file named:

```text
day-47/lists_of_dictionaries.py
```

Write each step slowly. Run the file after each step.

### Step 1: Create A List Of Students

Code:

```python
students = [
    {
        "name": "Maya",
        "score": 88,
        "passed": True
    },
    {
        "name": "Noah",
        "score": 95,
        "passed": True
    },
    {
        "name": "Iris",
        "score": 71,
        "passed": True
    }
]

print(students)
```

You should see:

```text
[{'name': 'Maya', 'score': 88, 'passed': True}, {'name': 'Noah', 'score': 95, 'passed': True}, {'name': 'Iris', 'score': 71, 'passed': True}]
```

The list has three items.

Each item is a dictionary.

Each dictionary has the same keys:

```text
name
score
passed
```

That repeated shape is what makes the data easy to loop through.

### Step 2: Read One Dictionary

Code:

```python
students = [
    {
        "name": "Maya",
        "score": 88,
        "passed": True
    },
    {
        "name": "Noah",
        "score": 95,
        "passed": True
    },
    {
        "name": "Iris",
        "score": 71,
        "passed": True
    }
]

first_student = students[0]

print(first_student)
```

You should see:

```text
{'name': 'Maya', 'score': 88, 'passed': True}
```

`students[0]` gives you the first dictionary in the list.

After that, `first_student` behaves like any other dictionary.

### Step 3: Read One Field From One Dictionary

Code:

```python
students = [
    {
        "name": "Maya",
        "score": 88,
        "passed": True
    },
    {
        "name": "Noah",
        "score": 95,
        "passed": True
    },
    {
        "name": "Iris",
        "score": 71,
        "passed": True
    }
]

first_student = students[0]

print(first_student["name"])
print(first_student["score"])
```

You should see:

```text
Maya
88
```

You can also do it in one line:

```python
students = [
    {"name": "Maya", "score": 88, "passed": True},
    {"name": "Noah", "score": 95, "passed": True},
    {"name": "Iris", "score": 71, "passed": True}
]

print(students[0]["name"])
```

You should see:

```text
Maya
```

That line uses a list index first and a dictionary key second.

### Step 4: Loop Through All Records

Code:

```python
students = [
    {"name": "Maya", "score": 88, "passed": True},
    {"name": "Noah", "score": 95, "passed": True},
    {"name": "Iris", "score": 71, "passed": True}
]

for student in students:
    print(student)
```

You should see:

```text
{'name': 'Maya', 'score': 88, 'passed': True}
{'name': 'Noah', 'score': 95, 'passed': True}
{'name': 'Iris', 'score': 71, 'passed': True}
```

The loop visits one dictionary at a time.

On each loop:

```text
student is one dictionary.
```

### Step 5: Print Selected Fields

Usually you do not want to print the whole dictionary.

You want a few useful fields.

Code:

```python
students = [
    {"name": "Maya", "score": 88, "passed": True},
    {"name": "Noah", "score": 95, "passed": True},
    {"name": "Iris", "score": 71, "passed": True}
]

for student in students:
    print(student["name"], "-", student["score"])
```

You should see:

```text
Maya - 88
Noah - 95
Iris - 71
```

This is one of the most useful patterns in beginner Python:

```python
for record in records:
    print(record["some_key"])
```

The list gives you each record.

The dictionary keys give you the fields inside each record.

### Step 6: Add A New Dictionary To The List

Use `append()` to add another record.

Code:

```python
students = [
    {"name": "Maya", "score": 88, "passed": True},
    {"name": "Noah", "score": 95, "passed": True},
    {"name": "Iris", "score": 71, "passed": True}
]

new_student = {
    "name": "Leo",
    "score": 82,
    "passed": True
}

students.append(new_student)

for student in students:
    print(student["name"], "-", student["score"])
```

You should see:

```text
Maya - 88
Noah - 95
Iris - 71
Leo - 82
```

`append()` adds the new dictionary as one item at the end of the list.

The loop does not need another `print()` line.

It already knows how to visit every record in the list.

### Step 7: Use The Same Pattern With Products

Lists of dictionaries are not only for students.

Code:

```python
products = [
    {"name": "Notebook", "price": 3.5, "stock": 12},
    {"name": "Pen", "price": 1.25, "stock": 30},
    {"name": "Water Bottle", "price": 12.0, "stock": 5}
]

for product in products:
    print(product["name"], "costs", product["price"])
```

You should see:

```text
Notebook costs 3.5
Pen costs 1.25
Water Bottle costs 12.0
```

The pattern is the same:

```text
one list
many dictionaries
one dictionary per record
same keys on each record
```

## Common Mistake

### Mistake 1: Missing Commas Between Dictionaries

Broken code:

```python
students = [
    {"name": "Maya", "score": 88}
    {"name": "Noah", "score": 95}
]

print(students)
```

This is broken because list items need commas between them.

The dictionaries are the list items here, so each dictionary needs a comma after it except the last one.

Fixed code:

```python
students = [
    {"name": "Maya", "score": 88},
    {"name": "Noah", "score": 95}
]

print(students)
```

You should see:

```text
[{'name': 'Maya', 'score': 88}, {'name': 'Noah', 'score': 95}]
```

### Mistake 2: Using Inconsistent Keys

Broken code:

```python
students = [
    {"name": "Maya", "score": 88},
    {"student_name": "Noah", "score": 95}
]

for student in students:
    print(student["name"])
```

This code prints the first name, then breaks on the second dictionary.

The first dictionary has `"name"`.

The second dictionary has `"student_name"` instead.

Fixed code:

```python
students = [
    {"name": "Maya", "score": 88},
    {"name": "Noah", "score": 95}
]

for student in students:
    print(student["name"])
```

You should see:

```text
Maya
Noah
```

When a list stores similar records, try to use the same keys in each dictionary.

### Mistake 3: Treating A List Like A Dictionary

Broken code:

```python
students = [
    {"name": "Maya", "score": 88},
    {"name": "Noah", "score": 95}
]

print(students["name"])
```

This is broken because `students` is a list.

Lists use indexes, not keys.

Fixed code:

```python
students = [
    {"name": "Maya", "score": 88},
    {"name": "Noah", "score": 95}
]

print(students[0]["name"])
```

You should see:

```text
Maya
```

Use the list index to choose a record.

Then use the dictionary key to choose a field.

### Mistake 4: Treating A Dictionary Like A List

Broken code:

```python
student = {
    "name": "Maya",
    "score": 88
}

print(student[0])
```

This is broken because `student` is a dictionary.

Dictionaries use keys, not list-style indexes.

Fixed code:

```python
student = {
    "name": "Maya",
    "score": 88
}

print(student["name"])
```

You should see:

```text
Maya
```

Ask yourself:

```text
Am I holding the list?
Use an index or a loop.

Am I holding one dictionary?
Use a key.
```

## Debug It

Read each broken program. Find the list-of-dictionaries mistake, then compare it with the fixed version.

### Debug 1: Missing Comma

Goal:

```text
Maya
Noah
```

Broken code:

```python
students = [
    {"name": "Maya", "score": 88}
    {"name": "Noah", "score": 95}
]

for student in students:
    print(student["name"])
```

The problem:

```text
There is no comma between the two dictionaries.
```

Fixed code:

```python
students = [
    {"name": "Maya", "score": 88},
    {"name": "Noah", "score": 95}
]

for student in students:
    print(student["name"])
```

You should see:

```text
Maya
Noah
```

### Debug 2: Wrong Level

Goal:

```text
First student: Maya
```

Broken code:

```python
students = [
    {"name": "Maya", "score": 88},
    {"name": "Noah", "score": 95}
]

print("First student:", students["name"])
```

The problem:

```text
students is the list, so it cannot use the key "name" directly.
```

Fixed code:

```python
students = [
    {"name": "Maya", "score": 88},
    {"name": "Noah", "score": 95}
]

print("First student:", students[0]["name"])
```

You should see:

```text
First student: Maya
```

### Debug 3: Inconsistent Key

Goal:

```text
Task: practice dictionaries
Task: read documentation
```

Broken code:

```python
tasks = [
    {"title": "practice dictionaries", "done": False},
    {"name": "read documentation", "done": False}
]

for task in tasks:
    print("Task:", task["title"])
```

The problem:

```text
The second dictionary uses "name", but the loop expects "title".
```

Fixed code:

```python
tasks = [
    {"title": "practice dictionaries", "done": False},
    {"title": "read documentation", "done": False}
]

for task in tasks:
    print("Task:", task["title"])
```

You should see:

```text
Task: practice dictionaries
Task: read documentation
```

### Debug 4: Dictionary Treated Like A List

Goal:

```text
Notebook
Pen
```

Broken code:

```python
products = [
    {"name": "Notebook", "price": 3.5},
    {"name": "Pen", "price": 1.25}
]

for product in products:
    print(product[0])
```

The problem:

```text
Inside the loop, product is one dictionary. It needs a key, not index 0.
```

Fixed code:

```python
products = [
    {"name": "Notebook", "price": 3.5},
    {"name": "Pen", "price": 1.25}
]

for product in products:
    print(product["name"])
```

You should see:

```text
Notebook
Pen
```

When nested data is confusing, name what each variable holds:

```text
products is the list.
product is one dictionary from the list.
product["name"] is one value from that dictionary.
```

## Read the Docs

Today's structure uses list operations and dictionary access together.

Look at these official documentation pages:

```text
https://docs.python.org/3/tutorial/datastructures.html
https://docs.python.org/3/library/stdtypes.html#mapping-types-dict
```

You do not need to read both pages fully.

Look for these ideas:

```text
list.append(x)
d[key]
key in d
```

Connect the documentation names to today's code:

```python
students = [
    {"name": "Maya", "score": 88}
]

new_student = {"name": "Noah", "score": 95}

students.append(new_student)

print(students[1]["name"])
```

You should see:

```text
Noah
```

In the documentation, `x` can mean any value.

Here, the value you append is a dictionary.

That is the key idea:

```text
A list can hold dictionaries just like it can hold strings or numbers.
```

## Mini Challenge

Create a file named:

```text
day-47/contact_list.py
```

Build a small contact list.

Start with this list:

```python
contacts = [
    {
        "name": "Sam",
        "phone": "555-0104",
        "email": "sam@example.com"
    },
    {
        "name": "Mina",
        "phone": "555-0188",
        "email": "mina@example.com"
    }
]
```

Your program should:

- print the first contact's name
- loop through all contacts
- print each contact's name and phone number
- create a new contact dictionary
- append the new contact to the list
- print the contact list again using a loop

One possible solution:

```python
contacts = [
    {
        "name": "Sam",
        "phone": "555-0104",
        "email": "sam@example.com"
    },
    {
        "name": "Mina",
        "phone": "555-0188",
        "email": "mina@example.com"
    }
]

print("First contact:", contacts[0]["name"])

print("Contact List")

for contact in contacts:
    print(contact["name"], "-", contact["phone"])

new_contact = {
    "name": "Dev",
    "phone": "555-0120",
    "email": "dev@example.com"
}

contacts.append(new_contact)

print("Updated Contact List")

for contact in contacts:
    print(contact["name"], "-", contact["phone"])
```

You should see:

```text
First contact: Sam
Contact List
Sam - 555-0104
Mina - 555-0188
Updated Contact List
Sam - 555-0104
Mina - 555-0188
Dev - 555-0120
```

After it works, add a `"city"` key to every contact.

Then update the loop so it prints:

```text
Sam - 555-0104 - Pune
```

Use any cities you like.

## Real-World Use

Lists of dictionaries are common because many programs store many similar records.

A contact book can store many contacts:

```python
contacts = [
    {"name": "Sam", "phone": "555-0104"},
    {"name": "Mina", "phone": "555-0188"}
]

for contact in contacts:
    print(contact["name"], contact["phone"])
```

You should see:

```text
Sam 555-0104
Mina 555-0188
```

A store can store many products:

```python
products = [
    {"name": "Notebook", "price": 3.5, "stock": 12},
    {"name": "Pen", "price": 1.25, "stock": 30}
]

for product in products:
    print(product["name"], "-", product["stock"], "in stock")
```

You should see:

```text
Notebook - 12 in stock
Pen - 30 in stock
```

A task app can store many tasks:

```python
tasks = [
    {"title": "practice loops", "done": True},
    {"title": "read docs", "done": False}
]

for task in tasks:
    print(task["title"], "-", task["done"])
```

You should see:

```text
practice loops - True
read docs - False
```

A reading tracker can store many books:

```python
books = [
    {"title": "Python Notes", "pages": 120},
    {"title": "Small Programs", "pages": 95}
]

for book in books:
    print(book["title"], "-", book["pages"], "pages")
```

You should see:

```text
Python Notes - 120 pages
Small Programs - 95 pages
```

A score table can store many score records:

```python
scores = [
    {"student": "Asha", "score": 9},
    {"student": "Ben", "score": 7},
    {"student": "Cara", "score": 10}
]

for record in scores:
    print(record["student"], "scored", record["score"])
```

You should see:

```text
Asha scored 9
Ben scored 7
Cara scored 10
```

The subjects change, but the shape stays the same:

```text
contacts -> many contact dictionaries
products -> many product dictionaries
tasks -> many task dictionaries
books -> many book dictionaries
scores -> many score dictionaries
```

When you have many similar things, a list of dictionaries is often a good first shape.

## Recap

Today you learned that a list can contain dictionaries.

You practiced:

- creating a list of dictionaries
- thinking of each dictionary as one record
- reading one dictionary with a list index
- reading one field with a dictionary key
- combining an index and a key, like `students[0]["name"]`
- looping through every dictionary in the list
- printing selected fields from each dictionary
- adding a new dictionary with `append()`
- using the same keys for similar records
- fixing missing commas between dictionaries
- avoiding list/dictionary mix-ups

The most important pattern is:

```python
for record in records:
    print(record["field"])
```

Read it as:

```text
For each dictionary in this list, print one value from that dictionary.
```

## Lesson Checklist

Before moving on, check that you can:

- create a list with at least two dictionaries inside it
- explain why each dictionary is one record
- explain why the list stores many records
- read the first dictionary with `records[0]`
- read one field with `records[0]["key"]`
- loop through all dictionaries in a list
- print selected fields inside a loop
- add a new dictionary to the list with `append()`
- use the same keys across similar dictionaries
- fix a missing comma between dictionaries
- explain why `records["name"]` is wrong when `records` is a list
- explain why `record[0]` is wrong when `record` is a dictionary

## Exercises

### Exercise 1

Create a list named `students`.

It should contain three dictionaries.

Each dictionary should have:

```text
name
score
passed
```

Print the whole list.

### Exercise 2

Use your `students` list.

Print the first dictionary.

Then print only the first student's name.

### Exercise 3

Loop through your `students` list.

Print each student's name.

### Exercise 4

Loop through your `students` list.

Print each student's name and score like this:

```text
Maya - 88
```

### Exercise 5

Create a new dictionary for one more student.

Append it to the `students` list.

Loop through the list again and print every name.

### Exercise 6

Create a list named `products`.

It should contain three product dictionaries.

Each dictionary should have:

```text
name
price
stock
```

Loop through the list and print each product's name and price.

### Exercise 7

Create a list named `tasks`.

Each task dictionary should have:

```text
title
done
```

Loop through the list and print each task title.

### Exercise 8

Fix the broken code.

Broken code:

```python
books = [
    {"title": "Python Notes", "pages": 120}
    {"title": "Small Programs", "pages": 95}
]

for book in books:
    print(book["title"])
```

The goal is to print both book titles.

### Exercise 9

Fix the broken code.

Broken code:

```python
contacts = [
    {"name": "Sam", "phone": "555-0104"},
    {"contact_name": "Mina", "phone": "555-0188"}
]

for contact in contacts:
    print(contact["name"])
```

The goal is to use the same key for both contact names.

### Exercise 10

Fix the broken code.

Broken code:

```python
products = [
    {"name": "Notebook", "price": 3.5},
    {"name": "Pen", "price": 1.25}
]

print(products["name"])
```

The goal is to print the first product's name.

### Exercise 11

Fix the broken code.

Broken code:

```python
task = {
    "title": "practice dictionaries",
    "done": False
}

print(task[0])
```

The goal is to print the task title.

### Exercise 12

Create a list named `books`.

Each book dictionary should have:

```text
title
author
pages
finished
```

Add at least three books.

Loop through the list and print:

```text
Title by Author
```

### Exercise 13

Create a list named `scores`.

Use this shape:

```python
scores = [
    {"student": "Asha", "score": 9},
    {"student": "Ben", "score": 7},
    {"student": "Cara", "score": 10}
]
```

Loop through the list.

Count how many scores are at least `8`.

Print the count.

### Exercise 14

Write a small program from scratch.

Choose one topic:

```text
contacts
products
students
tasks
books
scores
```

Your program should:

- create a list of at least three dictionaries
- print one full dictionary
- print one selected field from one dictionary
- loop through all dictionaries
- print two selected fields from each dictionary
- append one new dictionary
- loop again to show the new record

## Tiny Win

You can now store more than one real-world record at a time.

That is a major step beyond one dictionary.

Your programs can now say:

```text
Here are many contacts.
Here are many products.
Here are many students.
Here are many tasks.
```

And for each one:

```text
Here are the named fields inside it.
```

That pattern appears again and again in useful Python programs.

## Tomorrow

Tomorrow is:

```text
Day 48: Dictionaries of Lists
```

Today you used this shape:

```python
students = [
    {"name": "Maya", "score": 88},
    {"name": "Noah", "score": 95}
]
```

The outside container is a list.

Each inside item is a dictionary.

Tomorrow you will flip the shape:

```python
scores = {
    "names": ["Maya", "Noah"],
    "values": [88, 95]
}
```

The outside container will be a dictionary.

Some values inside it will be lists.

That will help you compare two common ways to organize related data.
