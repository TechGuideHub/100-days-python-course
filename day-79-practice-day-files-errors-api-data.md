# Day 79: Practice Day: Files, Errors, And API Data

**Focus:** Practicing file paths, CSV, JSON, exceptions, and API-shaped data together  
**You will practice:** `pathlib.Path`, reading and writing files, CSV rows, JSON files, `try` and `except`, `FileNotFoundError`, `ValueError`, `KeyError`, nested dictionaries, API response shapes, and small debugging routines  
**Estimated time:** 65-80 minutes

## Today's Goal

Today is a practice day.

You are not learning one large new tool. You are putting several tools together:

- paths
- plain text files
- CSV files
- JSON files
- exceptions
- API-shaped dictionaries and lists
- debugging from real values

By the end of today, you should be able to:

- create paths with `Path`
- read and write small files
- read CSV rows with `csv.DictReader`
- save and load JSON with `json.dump()` and `json.load()`
- read nested data one step at a time
- handle missing files with `FileNotFoundError`
- handle bad numbers with `ValueError`
- handle missing keys with `KeyError` or `.get()`
- explain what shape an API response has before you pull values from it
- prepare for Day 80, where you will build a small lookup app

The main idea for today is:

```text
File programs are data programs.
Data programs are shape-reading programs.
Shape-reading programs need careful errors.
```

That may sound like a lot, but each piece is small.

The practice today is about keeping those pieces in order.

## The Big Idea

Real programs rarely use just one skill at a time.

A program might:

```text
find a file
read rows
convert text to numbers
skip a bad row
save a summary
print a useful answer
```

Here is a small example that does that with a CSV file.

Code:

```python
import csv
from pathlib import Path

folder = Path("day-79")
folder.mkdir(exist_ok=True)

scores_path = folder / "scores.csv"
scores_path.write_text(
    "name,score\n"
    "Mina,91\n"
    "Sam,84\n"
    "Iris,89\n"
)

total = 0
count = 0

with open(scores_path, "r", newline="") as file:
    reader = csv.DictReader(file)

    for row in reader:
        score = int(row["score"])
        total = total + score
        count = count + 1

average = total / count

print("Rows:", count)
print("Average:", average)
```

You should see:

```text
Rows: 3
Average: 88.0
```

This example uses several skills:

- `Path("day-79")` names a folder
- `folder.mkdir(exist_ok=True)` creates the folder if needed
- `folder / "scores.csv"` builds a file path
- `write_text()` creates a small CSV file
- `csv.DictReader` reads rows as dictionaries
- `int()` converts text into numbers
- the loop adds the scores

The program is not difficult because any one line is difficult.

It is difficult only if you lose track of the data as it changes form.

## The Mental Model

Use this mental model for files and API data:

```text
path -> raw text -> Python data -> selected value -> useful output
```

For a CSV file, the flow might look like this:

```text
day-79/scores.csv
    -> text rows
    -> dictionaries from csv.DictReader
    -> row["score"]
    -> average score
```

For a JSON file, the flow might look like this:

```text
day-79/weather.json
    -> JSON text
    -> Python dictionary
    -> data["current"]["temperature"]
    -> weather message
```

For API data, the flow is almost the same.

An API usually sends JSON text. Python turns that JSON into dictionaries and lists.

You then read the shape.

Code:

```python
import json

api_text = """
{
    "location": {
        "city": "Pune",
        "country": "India"
    },
    "current": {
        "temperature": 31,
        "condition": "sunny"
    },
    "forecast": [
        {"day": "Mon", "high": 33},
        {"day": "Tue", "high": 32}
    ]
}
"""

data = json.loads(api_text)

city = data["location"]["city"]
temperature = data["current"]["temperature"]
first_day = data["forecast"][0]["day"]
first_high = data["forecast"][0]["high"]

print(city)
print("Now:", temperature)
print(first_day + " high:", first_high)
```

You should see:

```text
Pune
Now: 31
Mon high: 33
```

Read that shape slowly:

```text
data is a dictionary.
data["location"] is another dictionary.
data["forecast"] is a list.
data["forecast"][0] is the first dictionary in that list.
```

When you are unsure, print the type:

```python
print(type(data))
print(type(data["forecast"]))
print(type(data["forecast"][0]))
```

The shape tells you what to do next.

## Warm-Up

For each warm-up, predict the output before running the code.

These are short on purpose. The goal is to wake up the exact skills you will use in the practice problems.

### Warm-Up 1: Build A Path

Code:

```python
from pathlib import Path

folder = Path("day-79")
file_path = folder / "notes.txt"

print(folder.as_posix())
print(file_path.as_posix())
print(file_path.name)
```

You should see:

```text
day-79
day-79/notes.txt
notes.txt
```

Debugging prompt:

```text
What part is the folder?
What part is the filename?
Why is / useful when building paths?
```

### Warm-Up 2: Read CSV Rows As Dictionaries

Code:

```python
import csv
from pathlib import Path

folder = Path("day-79")
folder.mkdir(exist_ok=True)

csv_path = folder / "warmup_scores.csv"
csv_path.write_text(
    "name,score\n"
    "Mina,9\n"
    "Sam,7\n"
)

with open(csv_path, "r", newline="") as file:
    reader = csv.DictReader(file)

    for row in reader:
        print(row["name"], row["score"])
```

You should see:

```text
Mina 9
Sam 7
```

Debugging prompt:

```text
What are the dictionary keys for each row?
Why is row["score"] still text at first?
```

### Warm-Up 3: Read Nested JSON

Code:

```python
import json

text = """
{
    "user": {
        "name": "Asha",
        "level": 4
    },
    "badges": ["files", "json", "debugging"]
}
"""

profile = json.loads(text)

print(profile["user"]["name"])
print(profile["user"]["level"])
print(profile["badges"][1])
```

You should see:

```text
Asha
4
json
```

Debugging prompt:

```text
Which values are dictionaries?
Which value is a list?
Why does profile["badges"][1] print json instead of files?
```

### Warm-Up 4: Catch A Bad Number

Code:

```python
values = ["10", "8", "not ready", "7"]

total = 0

for value in values:
    try:
        number = int(value)
        total = total + number
    except ValueError:
        print("Skipped:", value)

print("Total:", total)
```

You should see:

```text
Skipped: not ready
Total: 25
```

Debugging prompt:

```text
Which value causes the ValueError?
Why does the loop continue after that value?
```

### Warm-Up 5: Read Optional API Fields

Code:

```python
result = {
    "title": "Python Basics",
    "url": "https://example.com/python-basics"
}

print(result["title"])
print(result.get("summary", "No summary yet"))
```

You should see:

```text
Python Basics
No summary yet
```

Debugging prompt:

```text
Which key is required in this example?
Which key is optional?
Why does .get() help with optional data?
```

## Try It Yourself

Create a folder named:

```text
day-79
```

Then create a file named:

```text
day-79/practice.py
```

Work through these steps in one file.

### Step 1: Write And Read A Notes File

Start with a small file program.

Code:

```python
from pathlib import Path

folder = Path("day-79")
folder.mkdir(exist_ok=True)

notes_path = folder / "notes.txt"
notes_path.write_text("review files\npractice errors\nread json\n")

text = notes_path.read_text()

print(text, end="")
```

You should see:

```text
review files
practice errors
read json
```

Now change the notes and run the program again.

Try this:

```text
Add one more line to the note text.
Print how many lines are in the file.
Print only the first line.
```

Hint:

```python
lines = text.splitlines()
print(len(lines))
print(lines[0])
```

### Step 2: Save A JSON Settings File

Replace your code with this.

Code:

```python
import json
from pathlib import Path

folder = Path("day-79")
folder.mkdir(exist_ok=True)

settings_path = folder / "settings.json"

settings = {
    "theme": "light",
    "items_per_page": 10,
    "show_tips": True
}

with open(settings_path, "w") as file:
    json.dump(settings, file, indent=4)

with open(settings_path, "r") as file:
    loaded_settings = json.load(file)

print("Theme:", loaded_settings["theme"])
print("Items per page:", loaded_settings["items_per_page"])
```

You should see:

```text
Theme: light
Items per page: 10
```

Try this:

```text
Change the theme.
Change items_per_page.
Add a new setting named notifications.
Run the program and open day-79/settings.json.
```

### Step 3: Handle A Missing File

Now practice a normal file problem: the file might not exist yet.

Code:

```python
import json
from pathlib import Path

folder = Path("day-79")
folder.mkdir(exist_ok=True)

settings_path = folder / "app_settings.json"

default_settings = {
    "theme": "light",
    "items_per_page": 10
}

try:
    with open(settings_path, "r") as file:
        settings = json.load(file)
except FileNotFoundError:
    settings = default_settings

    with open(settings_path, "w") as file:
        json.dump(settings, file, indent=4)

print("Theme:", settings["theme"])
print("Items per page:", settings["items_per_page"])
```

You should see:

```text
Theme: light
Items per page: 10
```

Run it twice.

The first run creates the file.

The second run loads the file.

That is a common app pattern:

```text
Try to load saved data.
If it is not there, create a starter version.
```

## Practice Problems

Use this rhythm for each problem:

```text
Read the data shape.
Name the risky line.
Write the smallest useful version.
Run it.
Handle one likely error.
Run it again.
```

Do not try to make every problem perfect on the first pass.

The goal is to practice seeing the path from file to data to answer.

### Practice Problem 1: Count Clean Lines

Create a file named:

```text
day-79/count_lines.py
```

Goal:

```text
Create day-79/tasks.txt.
Write several task lines into it.
Some lines should be blank.
Read the file.
Print only the non-empty lines.
Print the count of non-empty lines.
```

Starter data:

```text
write notes

practice csv
read json

debug carefully
```

Target result:

```text
write notes
practice csv
read json
debug carefully
Task count: 4
```

Hints:

```text
Use Path("day-79").
Use write_text() to create the file.
Use read_text().splitlines().
Use line.strip() to test whether a line is empty.
```

Debugging prompt:

```text
If your count is too high, are you counting blank lines?
```

### Practice Problem 2: CSV Score Summary

Create a file named:

```text
day-79/score_summary.py
```

Goal:

```text
Create day-79/scores_mixed.csv.
Read name and score columns.
Convert score to an integer.
Skip rows where score is not a number.
Print each valid score.
Print the average of valid scores.
```

Starter CSV:

```text
name,score
Mina,91
Sam,not ready
Iris,89
Dev,80
```

Target result:

```text
Mina: 91
Skipped Sam
Iris: 89
Dev: 80
Average: 86.66666666666667
```

Hints:

```text
Use csv.DictReader.
Put int(row["score"]) inside try.
Catch ValueError.
Keep total and count only for valid rows.
```

Debugging prompt:

```text
If the average crashes, what is count?
What should your program do if every row is invalid?
```

### Practice Problem 3: JSON Profile Update

Create a file named:

```text
day-79/profile_update.py
```

Goal:

```text
Create day-79/profile.json.
Store a profile with name, level, and skills.
Load the file.
Increase level by 1.
Add one new skill.
Save the updated profile.
Print the new level and skills.
```

Starter profile shape:

```json
{
    "name": "Mina",
    "level": 3,
    "skills": ["files", "csv"]
}
```

Target result:

```text
Mina is now level 4
Skills: files, csv, json
```

Hints:

```text
Use json.dump(..., indent=4).
Use json.load() before changing the data.
Use append() on the skills list.
Use ", ".join(profile["skills"]) for the display line.
```

Debugging prompt:

```text
What type is profile["skills"]?
Which list method adds one skill?
```

### Practice Problem 4: Read A Weather API Shape

Create a file named:

```text
day-79/weather_shape.py
```

Goal:

```text
Start with the dictionary below.
Print the city.
Print the current condition.
Print each forecast day and high temperature.
```

Data:

```python
weather = {
    "location": {
        "city": "Kochi",
        "country": "India"
    },
    "current": {
        "condition": "rain",
        "temperature": 28
    },
    "forecast": [
        {"day": "Mon", "high": 29, "low": 24},
        {"day": "Tue", "high": 30, "low": 25},
        {"day": "Wed", "high": 31, "low": 25}
    ]
}
```

Target result:

```text
City: Kochi
Now: rain, 28
Mon high: 29
Tue high: 30
Wed high: 31
```

Hints:

```text
weather["location"] is a dictionary.
weather["forecast"] is a list.
Each forecast item is a dictionary.
```

Debugging prompt:

```text
Before writing the loop, print type(weather["forecast"]).
Inside the loop, print one forecast item.
```

### Practice Problem 5: Search Results With Optional Fields

Create a file named:

```text
day-79/search_results.py
```

Goal:

```text
Start with the dictionary below.
Print each result title.
Print the summary if it exists.
Print "No summary" if it does not exist.
```

Data:

```python
response = {
    "query": "python files",
    "results": [
        {
            "title": "Reading Files",
            "summary": "Use open or Path.read_text."
        },
        {
            "title": "CSV Files"
        },
        {
            "title": "JSON Files",
            "summary": "Use the json module."
        }
    ]
}
```

Target result:

```text
Reading Files: Use open or Path.read_text.
CSV Files: No summary
JSON Files: Use the json module.
```

Hints:

```text
Loop through response["results"].
Use result["title"] for required data.
Use result.get("summary", "No summary") for optional data.
```

Debugging prompt:

```text
What happens if you use result["summary"] on every result?
What exception name do you see?
```

### Practice Problem 6: Safe JSON Loader

Create a file named:

```text
day-79/safe_settings.py
```

Goal:

```text
Write a function named load_settings(path).
If the JSON file exists, return the loaded settings.
If the JSON file is missing, return default settings.
Print the returned settings.
```

Default settings:

```python
{
    "theme": "light",
    "items_per_page": 10,
    "show_tips": True
}
```

Hints:

```text
The function should receive a path.
The try block should open and load the file.
The except FileNotFoundError block should return the default dictionary.
Call the function with Path("day-79/settings_missing.json").
```

Debugging prompt:

```text
Should the default dictionary be returned inside the except block or after it?
How can you test both the missing-file path and the existing-file path?
```

### Practice Problem 7: Build A Small Lookup Function

Create a file named:

```text
day-79/product_lookup_prep.py
```

Goal:

```text
Create a list of product dictionaries.
Write a function named find_product(products, product_id).
Return the matching product dictionary.
Return None if no product matches.
Print a friendly message for both cases.
```

Starter data:

```python
products = [
    {"id": "P100", "name": "notebook", "price": 5},
    {"id": "P101", "name": "pen", "price": 2},
    {"id": "P102", "name": "bag", "price": 25}
]
```

Target result for `P101`:

```text
P101: pen costs 2
```

Target result for `P999`:

```text
No product found for P999
```

Hints:

```text
Loop through products.
Compare product["id"] with product_id.
Use return product when you find a match.
Use return None after the loop.
```

Debugging prompt:

```text
Why should return None happen after the loop, not inside the first failed comparison?
```

### Practice Problem 8: Combine File, JSON, And Lookup

Create a file named:

```text
day-79/product_file_lookup.py
```

Goal:

```text
Save the product list from Practice Problem 7 into day-79/products.json.
Load the products back from the file.
Reuse find_product(products, product_id).
Look up two product ids.
```

Target result:

```text
P100: notebook costs 5
No product found for P999
```

Hints:

```text
Use json.dump(products, file, indent=4).
Use json.load(file) to load the list back.
After loading, products is a list.
Each product is a dictionary.
```

Debugging prompt:

```text
After json.load(), print type(products).
Then print type(products[0]).
The types tell you how to loop and index.
```

This problem is a direct warm-up for Day 80.

Tomorrow's lookup app will use the same basic idea, but with user input and cleaner functions.

## Common Mistake

A common mistake is reading the wrong level of nested data.

Suppose you have this API-shaped data:

```python
response = {
    "results": [
        {"title": "Files", "views": 120},
        {"title": "Errors", "views": 95}
    ]
}
```

This line does not work:

```python
print(response["results"]["title"])
```

Why?

Because `response["results"]` is a list, not a dictionary.

You need one result from the list first.

Code:

```python
response = {
    "results": [
        {"title": "Files", "views": 120},
        {"title": "Errors", "views": 95}
    ]
}

first_result = response["results"][0]

print(first_result["title"])
print(first_result["views"])
```

You should see:

```text
Files
120
```

Or loop through every result:

```python
response = {
    "results": [
        {"title": "Files", "views": 120},
        {"title": "Errors", "views": 95}
    ]
}

for result in response["results"]:
    print(result["title"], result["views"])
```

You should see:

```text
Files 120
Errors 95
```

When nested data feels confusing, say the shape out loud:

```text
response is a dictionary.
response["results"] is a list.
Each item in the list is a dictionary.
Each dictionary has title and views keys.
```

That one habit prevents many `TypeError` and `KeyError` surprises.

## Debug It

Here is a small program with several realistic mistakes.

Read it first. Do not fix everything at once.

Code:

```python
import csv
import json
from pathlib import Path

folder = Path("day-79")
orders_path = folder / "orders.csv"
settings_path = folder / "order_settings.json"

orders_path.write_text(
    "id,total\n"
    "A100,12\n"
    "A101,not ready\n"
    "A102,9\n"
)

with open(orders_path, "r", newline="") as file:
    reader = csv.DictReader(file)

    for row in reader:
        total = int(row["amount"])
        print(row["id"], total)

with open(settings_path, "r") as file:
    settings = json.load(file)

print("Currency:", settings["currency"])
```

Find and fix these problems:

```text
The day-79 folder may not exist yet.
The CSV column is named total, not amount.
One total is not a number.
The settings file may not exist yet.
```

One possible fix:

```python
import csv
import json
from pathlib import Path

folder = Path("day-79")
folder.mkdir(exist_ok=True)

orders_path = folder / "orders.csv"
settings_path = folder / "order_settings.json"

orders_path.write_text(
    "id,total\n"
    "A100,12\n"
    "A101,not ready\n"
    "A102,9\n"
)

default_settings = {
    "currency": "INR"
}

try:
    with open(settings_path, "r") as file:
        settings = json.load(file)
except FileNotFoundError:
    settings = default_settings

    with open(settings_path, "w") as file:
        json.dump(settings, file, indent=4)

with open(orders_path, "r", newline="") as file:
    reader = csv.DictReader(file)

    for row in reader:
        try:
            total = int(row["total"])
            print(row["id"], total)
        except ValueError:
            print("Skipped", row["id"])

print("Currency:", settings["currency"])
```

You should see:

```text
A100 12
Skipped A101
A102 9
Currency: INR
```

Debugging prompt:

```text
Which fix prevents FileNotFoundError?
Which fix prevents KeyError?
Which fix prevents ValueError?
Why is each except block catching a specific exception?
```

## Read the Docs

Today, read documentation with one question in mind:

```text
What type does this tool give me back?
```

Look up these Python tools:

- `pathlib.Path`
- `Path.exists()`
- `Path.read_text()`
- `Path.write_text()`
- `csv.DictReader`
- `json.load()`
- `json.loads()`
- `json.dump()`
- `FileNotFoundError`
- `ValueError`
- `KeyError`

Do not try to memorize every option.

For each tool, write one short note:

```text
What does it need?
What does it return?
What error might happen if the data is missing or wrong?
```

Examples:

```text
Path.exists() needs a path and returns True or False.
json.load(file) needs an open file and returns Python data.
csv.DictReader(file) needs a CSV file and gives rows that behave like dictionaries.
int(text) needs number-looking text and may raise ValueError.
```

The docs are easier to read when you bring a small question with you.

## Mini Challenge

Build a tiny saved-data lookup.

Create a file named:

```text
day-79/city_lookup.py
```

Goal:

```text
Save city data into day-79/cities.json.
Load it back.
Write a function named find_city(cities, city_name).
Print the city's country and population if found.
Print a friendly message if not found.
```

Starter data:

```python
cities = [
    {"name": "Pune", "country": "India", "population": 7400000},
    {"name": "Kochi", "country": "India", "population": 2100000},
    {"name": "Nairobi", "country": "Kenya", "population": 5300000}
]
```

Target result:

```text
Pune is in India and has population 7400000
No city found for Tokyo
```

Suggested function shape:

```python
def find_city(cities, city_name):
    for city in cities:
        if city["name"] == city_name:
            return city

    return None
```

After that function works, try one improvement:

```text
Make the lookup case-insensitive.
```

That means:

```text
pune
Pune
PUNE
```

should all find the same city.

Hint:

```python
if city["name"].lower() == city_name.lower():
```

## Real-World Use

These skills show up together often.

A small app might use a JSON file for settings:

```text
theme
font size
recent files
saved username
```

A spreadsheet export might arrive as CSV:

```text
orders
student scores
inventory
expenses
```

An API response might arrive as JSON:

```text
weather data
search results
product details
currency rates
map locations
```

Your program usually has the same job:

```text
load the data
check the shape
convert the values you need
handle normal problems
show a useful answer
```

The normal problems matter:

- a file is missing
- a number is stored as text
- a row has bad data
- a key is missing
- an API result has an optional field
- a search finds nothing

Good beginner programs do not need to handle every possible disaster.

They should handle the problems you can name.

## Recap

Today you practiced combining file and data skills.

You used paths to point at files.

You used CSV for table-shaped data.

You used JSON for structured data.

You read API-shaped dictionaries and lists from the outside in.

You used exceptions for normal problems like missing files and bad numbers.

You prepared for lookup programs by writing functions that search through lists of dictionaries.

The pattern to remember is:

```text
Find the data.
Load the data.
Check the shape.
Pick the value.
Handle the likely problem.
Print the answer.
```

## Lesson Checklist

Before you move on, make sure you can:

- build a file path with `Path`
- create a folder with `mkdir(exist_ok=True)`
- read text with `read_text()`
- write text with `write_text()`
- read CSV rows with `csv.DictReader`
- convert CSV text values with `int()` or `float()`
- catch `ValueError` when conversion fails
- save JSON with `json.dump()`
- load JSON with `json.load()`
- load JSON text with `json.loads()`
- catch `FileNotFoundError` for missing files
- use `.get()` for optional dictionary fields
- explain whether a nested value is a list or dictionary
- loop through a list of dictionaries
- return `None` when a lookup finds no match

## Exercises

Choose at least three.

### Exercise 1: Bad Row Report

Create a CSV file with these columns:

```text
name,hours
```

Read it and print:

```text
Mina worked 5 hours
```

If a row has a bad hour value, print:

```text
Skipped Mina because hours was not a number
```

### Exercise 2: Missing Settings File

Write a program that tries to load:

```text
day-79/display_settings.json
```

If it is missing, create it with:

```json
{
    "font_size": 14,
    "theme": "light"
}
```

Then print both settings.

### Exercise 3: Optional API Field

Start with this data:

```python
books = {
    "results": [
        {"title": "Small Python", "rating": 5},
        {"title": "Debugging Notes"},
        {"title": "File Practice", "rating": 4}
    ]
}
```

Print each title and rating.

If a book has no rating, print:

```text
not rated
```

### Exercise 4: Save A Filtered List

Create a list of task dictionaries:

```python
tasks = [
    {"title": "read docs", "done": True},
    {"title": "practice csv", "done": False},
    {"title": "fix bug", "done": True}
]
```

Save only the completed tasks into:

```text
day-79/completed_tasks.json
```

Then load the file and print the completed task titles.

### Exercise 5: Lookup With A Missing Key

Start with this data:

```python
contacts = [
    {"name": "Mina", "phone": "555-0104"},
    {"name": "Sam"},
    {"name": "Iris", "phone": "555-0130"}
]
```

Print each contact.

If a contact has no phone number, print:

```text
No phone saved
```

Use `.get()`.

### Exercise 6: Explain The Shape

Before writing code, explain this data in four lines:

```python
data = {
    "status": "ok",
    "items": [
        {"id": 1, "name": "notebook"},
        {"id": 2, "name": "pen"}
    ]
}
```

Use this style:

```text
data is a ...
data["items"] is a ...
data["items"][0] is a ...
data["items"][0]["name"] is a ...
```

Then write code that prints:

```text
1 notebook
2 pen
```

## Tiny Win

Pick one program from today and add this line before the main loop:

```python
print("Data loaded successfully")
```

Then run the program.

That tiny message is not fancy, but it proves something useful:

```text
The file step worked before the processing step began.
```

When a program has several moving parts, small confirmation messages can make debugging calmer.

## Tomorrow

Tomorrow you will build a lookup app.

It will use the same pieces you practiced today:

- saved JSON data
- a list of dictionaries
- a lookup function
- user input
- missing-result handling
- clear output

Day 79 is the rehearsal.

Day 80 turns the rehearsal into a small app.
