# Day 73: JSON Files

**Focus:** Saving and loading structured data with JSON  
**You will practice:** `json.dump()`, `json.load()`, `indent`, Python dictionaries and lists, profile data, settings files, and common JSON mistakes  
**Estimated time:** 45-60 minutes

## Today's Goal

Today you will learn how to save structured data in a JSON file.

In Day 72, CSV was useful because it stored rows and columns:

```text
name,score
Maya,95
Leo,88
```

That shape is perfect for simple tables.

But not every piece of data is a flat table.

Sometimes you want to save a user profile:

```text
name
level
skills
settings
```

Some of those values are single values. Some are lists. Some are smaller groups of settings.

That is where JSON is useful.

By the end of this lesson, you should be able to:

- recognize JSON as structured data
- map Python dictionaries and lists to JSON
- save data with `json.dump()`
- read data with `json.load()`
- use `indent` to make JSON easier to read
- save simple profile or settings data
- spot common JSON mistakes with quotes and trailing commas
- decide when JSON is a better fit than CSV
- prepare for Day 74, where you will handle errors with exceptions

The main idea:

```text
CSV is good for tables.
JSON is good for data with structure.
```

## The Big Idea

JSON stands for JavaScript Object Notation.

You do not need to know JavaScript to use it.

For this course, think of JSON as a plain text format for storing data that has names, values, lists, and nested groups.

It often looks a lot like a Python dictionary.

Create a folder named:

```text
day-73
```

Inside that folder, create a Python file named:

```text
day-73/save_profile.py
```

Code:

```python
import json

profile = {
    "name": "Maya",
    "level": 3,
    "is_member": True,
    "skills": ["loops", "files", "csv"],
    "settings": {
        "theme": "light",
        "notifications": False
    }
}

with open("day-73/profile.json", "w") as file:
    json.dump(profile, file, indent=4)

print("Saved profile")
```

Run it.

You should see:

```text
Saved profile
```

You should also see a new file named:

```text
day-73/profile.json
```

Open it. It should look like this:

```json
{
    "name": "Maya",
    "level": 3,
    "is_member": true,
    "skills": [
        "loops",
        "files",
        "csv"
    ],
    "settings": {
        "theme": "light",
        "notifications": false
    }
}
```

Notice two small changes:

- Python's `True` became JSON's `true`
- Python's `False` became JSON's `false`

Python handles those conversions for you.

## The Mental Model

JSON works well when your data has a shape.

Here is the usual mapping:

| Python value | JSON value |
| --- | --- |
| `dict` | object |
| `list` | array |
| `str` | string |
| `int` or `float` | number |
| `True` | `true` |
| `False` | `false` |
| `None` | `null` |

The two main tools are:

```text
json.dump() writes Python data into a JSON file.
json.load() reads JSON data back into Python.
```

You can picture it like this:

```text
Python dict or list
        |
        | json.dump()
        v
JSON file
        |
        | json.load()
        v
Python dict or list again
```

The important part is that JSON keeps the structure.

A list stays a list. A dictionary stays like a dictionary. A dictionary inside another dictionary keeps its place.

That makes JSON a good fit for settings, saved profiles, saved games, app configuration, and web data.

## Try It Yourself

Now save a small settings file.

Create a file named:

```text
day-73/save_settings.py
```

Code:

```python
import json

settings = {
    "username": "sam",
    "theme": "dark",
    "font_size": 16,
    "show_tips": True
}

with open("day-73/settings.json", "w") as file:
    json.dump(settings, file, indent=4)

print("Settings saved")
```

Run it.

You should see:

```text
Settings saved
```

Now create another file named:

```text
day-73/load_settings.py
```

Code:

```python
import json

with open("day-73/settings.json", "r") as file:
    settings = json.load(file)

print(f"User: {settings['username']}")
print(f"Theme: {settings['theme']}")
print(f"Font size: {settings['font_size']}")

settings["font_size"] = settings["font_size"] + 2

with open("day-73/settings.json", "w") as file:
    json.dump(settings, file, indent=4)

print("Font size updated")
```

Run it.

You should see:

```text
User: sam
Theme: dark
Font size: 16
Font size updated
```

Open `day-73/settings.json` again.

The `font_size` value should now be `18`.

That is a common pattern:

```text
load data
change data
save data again
```

## Common Mistake

JSON looks similar to Python, but it is stricter than Python.

This is valid as a Python dictionary:

```python
profile = {
    'name': 'Maya',
    'level': 3,
}
```

But this is not valid JSON data:

```json
{
    'name': 'Maya',
    'level': 3,
}
```

There are two problems:

- JSON strings must use double quotes
- JSON does not allow a trailing comma after the last value

This is valid JSON:

```json
{
    "name": "Maya",
    "level": 3
}
```

Another common mistake is passing a file path directly to `json.load()`.

Broken code:

```python
import json

data = json.load("day-73/profile.json")

print(data["name"])
```

This is broken because `json.load()` expects an open file object, not a file name string.

Fixed code:

```python
import json

with open("day-73/profile.json", "r") as file:
    data = json.load(file)

print(data["name"])
```

## Debug It

Here is another small mistake.

Broken code:

```python
import json

with open("day-73/profile.json", "r") as file:
    profile = json.load(file)

print(profile["favorite_color"])
```

This code is broken because the profile does not have a key named `"favorite_color"`.

Python will raise a `KeyError`.

You could fix it by using `.get()`:

Fixed code:

```python
import json

with open("day-73/profile.json", "r") as file:
    profile = json.load(file)

favorite_color = profile.get("favorite_color", "No favorite color saved yet")

print(favorite_color)
```

You should see:

```text
No favorite color saved yet
```

Do not worry if the word `KeyError` still feels a little sharp.

Tomorrow, you will learn how to handle errors more carefully with exceptions.

## Read the Docs

Python has a built-in module named `json`.

In the Python documentation for `json`, look for these names:

- `json.dump(obj, fp)`
- `json.load(fp)`
- `indent`
- `json.dumps(obj)`
- `json.loads(s)`

The names with an `s` work with strings instead of files.

Try this short example:

```python
import json

scores = [95, 88, 76]

text = json.dumps(scores)
restored_scores = json.loads(text)

print(text)
print(restored_scores[0])
```

You should see:

```text
[95, 88, 76]
95
```

For file work, you will usually use `dump()` and `load()`.

For converting data to and from a string, you can use `dumps()` and `loads()`.

## Mini Challenge

Save a list of favorite movies as JSON, then read it back.

Create a file named:

```text
day-73/movie_list.py
```

Code:

```python
import json

movies = [
    {
        "title": "Kiki's Delivery Service",
        "year": 1989,
        "rewatch": True
    },
    {
        "title": "The Iron Giant",
        "year": 1999,
        "rewatch": False
    }
]

with open("day-73/movies.json", "w") as file:
    json.dump(movies, file, indent=4)

with open("day-73/movies.json", "r") as file:
    loaded_movies = json.load(file)

for movie in loaded_movies:
    print(f"{movie['title']} ({movie['year']})")
```

You should see:

```text
Kiki's Delivery Service (1989)
The Iron Giant (1999)
```

This example is a list of dictionaries.

That is a very common JSON shape.

## Real-World Use

JSON shows up all over everyday programming.

You might use it for:

- a program's settings
- a saved user profile
- a saved game
- data sent back from a website
- configuration for a tool
- a list of records where each record has several fields

CSV is still useful.

Use CSV when your data is mostly a simple table:

```text
name,score,passed
Maya,95,true
Leo,88,true
Nina,62,false
```

Use JSON when one record needs lists, nested settings, or mixed pieces of information:

```json
{
    "name": "Maya",
    "scores": [95, 91, 98],
    "settings": {
        "theme": "light",
        "email_updates": false
    }
}
```

Here is a simple rule:

```text
If the data looks like a spreadsheet, CSV is often enough.
If the data needs containers inside containers, JSON is usually easier.
```

## Recap

Today you learned that JSON is a plain text format for structured data.

You practiced:

- importing the `json` module
- saving Python data with `json.dump()`
- reading JSON files with `json.load()`
- using `indent=4` so files are readable
- mapping Python dictionaries and lists to JSON
- avoiding invalid JSON with single quotes or trailing commas
- choosing JSON when data is more structured than a table

The core pattern is:

```python
import json

data = {
    "topic": "JSON",
    "complete": True
}

with open("day-73/data.json", "w") as file:
    json.dump(data, file, indent=4)

with open("day-73/data.json", "r") as file:
    data = json.load(file)

print(data["topic"])
```

## Lesson Checklist

Before you move on, make sure you can:

- explain why JSON is useful
- create a dictionary that can be saved as JSON
- save a JSON file with `json.dump()`
- read a JSON file with `json.load()`
- use `indent` to make the file easier to inspect
- fix JSON that uses single quotes
- remove a trailing comma from JSON data
- choose between CSV and JSON for a small problem

## Exercises

### Exercise 1

Create a file named `day-73/book_profile.py`.

Save this data to `day-73/book.json`:

- title
- author
- year
- genres, as a list
- currently_reading, as a Boolean value

Then open the JSON file and check that it is readable.

### Exercise 2

Create a file named `day-73/read_book.py`.

Load `day-73/book.json` and print one sentence like this:

```text
I am reading The Hobbit by J. R. R. Tolkien.
```

Use values from the loaded dictionary, not hard-coded text.

### Exercise 3

Create a settings file for a small quiz app.

Include:

- player name
- difficulty
- sound on or off
- best score
- categories, as a list

Save the settings to `day-73/quiz_settings.json`.

Then load the file and print the difficulty.

### Exercise 4

Decide whether CSV or JSON fits each case better:

- a list of 30 students with one score each
- a saved game with a player name, inventory list, health, and current level
- a monthly spending table with date, category, and amount
- a profile with a name, list of skills, and display settings

Write one sentence for each choice.

## Tiny Win

You can now make a program remember structured information after it closes.

That is a big step toward programs that feel less like one-time scripts and more like small real tools.

## Tomorrow

Tomorrow you will learn about exceptions.

That will help when a JSON file is missing, a key is not found, or a file has invalid JSON.

Instead of letting the program crash without guidance, you will learn how to respond to those problems on purpose.
