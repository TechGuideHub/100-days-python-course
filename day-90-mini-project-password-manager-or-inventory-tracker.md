# Day 90: Mini Project: Inventory Tracker

**Focus:** Building a small command-line inventory tracker with classes and JSON saving  
**You will practice:** classes, methods, object attributes, lists of objects, JSON persistence, menu choices, adding records, listing records, updating records, saving, loading, and error handling  
**Estimated time:** 80-100 minutes

## Today's Goal

Today you will build an inventory tracker.

The app will run in the command line. It will let the user add items, list items, update quantities and prices, save the inventory to a JSON file, and load it again later.

You have already practiced dictionaries, lists, files, JSON, functions, exceptions, and classes.

Today those pieces come together.

By the end of this lesson, you should be able to:

- create a class for one inventory item
- create a class that manages many inventory items
- write methods that read and update object data
- store many objects in a list
- convert objects into dictionaries before saving them as JSON
- convert dictionaries back into objects after loading JSON
- build a menu that keeps running until the user quits
- handle missing files, invalid numbers, and broken JSON data
- test a command-line project with planned inputs
- prepare for Day 91, where you will plan a larger project before building it

This is a project day.

The point is not to memorize the whole program line by line.

The point is to see how small parts work together in a program that feels useful.

## The Big Idea

An inventory tracker keeps records.

One record might look like this:

```text
name: notebook
quantity: 12
price: 2.5
```

Earlier in the course, you might have stored that record as a dictionary:

```python
item = {
    "name": "notebook",
    "quantity": 12,
    "price": 2.5
}
```

That still works.

Today you will use a class instead:

```python
class InventoryItem:
    def __init__(self, name, quantity, price):
        self.name = name
        self.quantity = quantity
        self.price = price
```

Then one item can be created like this:

```python
item = InventoryItem("notebook", 12, 2.5)

print(item.name)
print(item.quantity)
print(item.price)
```

You should see:

```text
notebook
12
2.5
```

The class gives your program a clear word for one thing:

```text
InventoryItem
```

That makes the rest of the code easier to read.

Instead of passing around loose dictionaries, the program can pass around item objects.

## The Mental Model

Think of the app as two layers.

The first layer is one item:

```text
InventoryItem
- name
- quantity
- price
```

The second layer is the whole inventory:

```text
Inventory
- save path
- list of InventoryItem objects
```

The `InventoryItem` class knows how to describe one item.

The `Inventory` class knows how to manage many items.

That split keeps the project organized:

```text
InventoryItem
    stores data for one item
    turns one item into a dictionary
    creates a readable display line

Inventory
    stores the list of items
    adds items
    finds items
    saves all items
    loads all items
```

There is one extra idea today: JSON cannot directly save your custom objects.

Python can save dictionaries and lists to JSON.

Python cannot automatically save this object:

```python
InventoryItem("notebook", 12, 2.5)
```

So before saving, you convert the object into a dictionary:

```python
{
    "name": "notebook",
    "quantity": 12,
    "price": 2.5
}
```

After loading, you convert the dictionary back into an object.

That back-and-forth is a common pattern:

```text
object -> dictionary -> JSON file
JSON file -> dictionary -> object
```

## The Project

Create a folder named:

```text
day-90
```

Inside that folder, create this file:

```text
day-90/inventory_tracker.py
```

Your finished app will:

1. Start with an empty inventory.
2. Try to load saved items from:

```text
day-90/inventory.json
```

3. Show a menu.
4. Let the user list all items.
5. Let the user add a new item.
6. Let the user update an existing item's quantity or price.
7. Let the user save the inventory.
8. Let the user load the inventory again.
9. Handle common input and file problems with friendly messages.
10. Keep running until the user chooses quit.

Example session:

```text
Inventory Tracker
No saved inventory found yet.

Menu:
1. List items
2. Add item
3. Update item
4. Save inventory
5. Load inventory
6. Quit
Choose an option: 2
Item name: notebook
Quantity: 12
Price: 2.50
Added notebook.

Menu:
1. List items
2. Add item
3. Update item
4. Save inventory
5. Load inventory
6. Quit
Choose an option: 1

Inventory:
1. notebook - 12 in stock - $2.50 each

Menu:
1. List items
2. Add item
3. Update item
4. Save inventory
5. Load inventory
6. Quit
Choose an option: 4
Saved 1 item to day-90/inventory.json.

Menu:
1. List items
2. Add item
3. Update item
4. Save inventory
5. Load inventory
6. Quit
Choose an option: 6
Goodbye.
```

The exact items depend on what the user types.

## Step-by-Step Build

Build this project in small pieces.

A project with classes, a menu, and a save file has several moving parts. Make one part work, run the file, then add the next part.

### Step 1: Import The Tools

Start with the modules you need.

```python
import json
from pathlib import Path
```

`json` lets you read and write JSON data.

`Path` gives you a clean way to work with the save file path.

### Step 2: Add The Save Path

Add a constant for the file where the inventory will be saved.

```python
SAVE_PATH = Path("day-90/inventory.json")
```

The file does not need to exist yet.

Your program will create it when the user saves.

### Step 3: Create The Item Class

Create a class for one inventory item.

```python
class InventoryItem:
    def __init__(self, name, quantity, price):
        self.name = name
        self.quantity = quantity
        self.price = price
```

This class stores three attributes:

```text
name
quantity
price
```

Try it with a small test:

```python
item = InventoryItem("notebook", 12, 2.5)

print(item.name)
print(item.quantity)
print(item.price)
```

You should see:

```text
notebook
12
2.5
```

### Step 4: Add A Display Method

The menu needs to show one item in a readable way.

Add this method inside `InventoryItem`:

```python
def display_line(self, number):
    return f"{number}. {self.name} - {self.quantity} in stock - ${self.price:.2f} each"
```

The `:.2f` part formats the price with two decimal places.

For example:

```python
item = InventoryItem("notebook", 12, 2.5)
print(item.display_line(1))
```

You should see:

```text
1. notebook - 12 in stock - $2.50 each
```

This is a good use for a method because the method belongs to one item.

### Step 5: Convert One Item To A Dictionary

JSON can save dictionaries.

It cannot directly save an `InventoryItem` object.

Add this method inside `InventoryItem`:

```python
def to_dict(self):
    return {
        "name": self.name,
        "quantity": self.quantity,
        "price": self.price
    }
```

Now this object:

```python
InventoryItem("notebook", 12, 2.5)
```

can become this dictionary:

```text
{"name": "notebook", "quantity": 12, "price": 2.5}
```

That dictionary is safe to write into a JSON file.

### Step 6: Create The Inventory Class

Now create a class for the whole inventory.

```python
class Inventory:
    def __init__(self, save_path):
        self.save_path = Path(save_path)
        self.items = []
```

This object stores:

- where the JSON file should live
- the list of current items

Create one inventory like this:

```python
inventory = Inventory(SAVE_PATH)
```

At first, `inventory.items` is an empty list.

### Step 7: Add An Item

Add this method inside `Inventory`:

```python
def add_item(self, name, quantity, price):
    item = InventoryItem(name, quantity, price)
    self.items.append(item)
```

The inventory manages the list.

The item manages the data for one record.

That means the menu will not need to know exactly how items are stored.

It can ask the inventory to add one.

### Step 8: Find An Item By Name

The update feature needs to find one item.

Add this method inside `Inventory`:

```python
def find_item(self, name):
    search_name = name.lower()

    for item in self.items:
        if item.name.lower() == search_name:
            return item

    return None
```

This method returns an `InventoryItem` object if it finds one.

If it does not find one, it returns `None`.

The search ignores capitalization, so these can match:

```text
Notebook
notebook
NOTEBOOK
```

### Step 9: Save The Inventory

Saving means:

```text
turn every item object into a dictionary
write the list of dictionaries to a JSON file
```

Add this method inside `Inventory`:

```python
def save(self):
    self.save_path.parent.mkdir(parents=True, exist_ok=True)

    data = []

    for item in self.items:
        data.append(item.to_dict())

    with self.save_path.open("w", encoding="utf-8") as file:
        json.dump(data, file, indent=4)
```

The save file will contain a JSON list.

It will look similar to this:

```json
[
    {
        "name": "notebook",
        "quantity": 12,
        "price": 2.5
    }
]
```

The app uses `indent=4` so the file is easier for a learner to inspect.

### Step 10: Load The Inventory

Loading means:

```text
read the JSON file
check that the data has the expected shape
turn each dictionary back into an InventoryItem object
```

Add this method inside `Inventory`:

```python
def load(self):
    if not self.save_path.exists():
        self.items = []
        return False

    try:
        with self.save_path.open("r", encoding="utf-8") as file:
            data = json.load(file)
    except json.JSONDecodeError as error:
        raise ValueError("The save file is not valid JSON.") from error

    if not isinstance(data, list):
        raise ValueError("The save file should contain a list of items.")

    loaded_items = []

    for record in data:
        if not isinstance(record, dict):
            raise ValueError("Each saved item should be a dictionary.")

        try:
            name = str(record["name"]).strip()
            quantity = int(record["quantity"])
            price = float(record["price"])
        except (KeyError, TypeError, ValueError) as error:
            raise ValueError("One saved item has missing or invalid fields.") from error

        if name == "":
            raise ValueError("One saved item has a blank name.")

        if quantity < 0:
            raise ValueError("One saved item has a negative quantity.")

        if price < 0:
            raise ValueError("One saved item has a negative price.")

        loaded_items.append(InventoryItem(name, quantity, price))

    self.items = loaded_items
    return True
```

This method returns `False` when no save file exists yet.

It returns `True` when a file was found and loaded.

If the file exists but the data is broken, it raises `ValueError` with a message the menu can show.

### Step 11: Add Number Helpers

The user will type quantity and price as text.

The program needs to turn that text into numbers.

Add these helper functions:

```python
def ask_for_quantity(prompt):
    raw_value = input(prompt).strip()

    try:
        quantity = int(raw_value)
    except ValueError:
        print("Please enter a whole number for the quantity.")
        return None

    if quantity < 0:
        print("Quantity cannot be negative.")
        return None

    return quantity
```

And:

```python
def ask_for_price(prompt):
    raw_value = input(prompt).strip()

    try:
        price = float(raw_value)
    except ValueError:
        print("Please enter a number for the price.")
        return None

    if price < 0:
        print("Price cannot be negative.")
        return None

    return price
```

These functions return `None` when the input is not usable.

That lets the menu stop the current action without crashing the whole app.

### Step 12: Show The Menu

Add a function for the menu text.

```python
def show_menu():
    print()
    print("Menu:")
    print("1. List items")
    print("2. Add item")
    print("3. Update item")
    print("4. Save inventory")
    print("5. Load inventory")
    print("6. Quit")
```

The menu does not make decisions.

It only prints the choices.

### Step 13: List Items

Add this function:

```python
def list_items(inventory):
    if not inventory.items:
        print("No inventory items yet.")
        return

    print()
    print("Inventory:")

    for index, item in enumerate(inventory.items, start=1):
        print(item.display_line(index))
```

Notice that `list_items()` receives the inventory object.

It asks the object for its items, then asks each item for its display line.

### Step 14: Add Items From The Menu

Add this function:

```python
def add_item_from_menu(inventory):
    name = input("Item name: ").strip()

    if name == "":
        print("Item name cannot be blank.")
        return

    if inventory.find_item(name) is not None:
        print("That item already exists. Use update instead.")
        return

    quantity = ask_for_quantity("Quantity: ")

    if quantity is None:
        return

    price = ask_for_price("Price: ")

    if price is None:
        return

    inventory.add_item(name, quantity, price)
    print(f"Added {name}.")
```

This function protects the inventory from common bad inputs:

- blank item names
- duplicate item names
- invalid quantity values
- invalid price values

### Step 15: Update Items From The Menu

Add this function:

```python
def update_item_from_menu(inventory):
    name = input("Item to update: ").strip()

    if name == "":
        print("Item name cannot be blank.")
        return

    item = inventory.find_item(name)

    if item is None:
        print("No item found with that name.")
        return

    print("Current item:")
    print(item.display_line(1))

    raw_quantity = input("New quantity (leave blank to keep current): ").strip()

    if raw_quantity != "":
        try:
            quantity = int(raw_quantity)
        except ValueError:
            print("Please enter a whole number for the quantity.")
            return

        if quantity < 0:
            print("Quantity cannot be negative.")
            return

        item.quantity = quantity

    raw_price = input("New price (leave blank to keep current): ").strip()

    if raw_price != "":
        try:
            price = float(raw_price)
        except ValueError:
            print("Please enter a number for the price.")
            return

        if price < 0:
            print("Price cannot be negative.")
            return

        item.price = price

    print(f"Updated {item.name}.")
```

This update style lets the user change one field or both fields.

If the user presses Enter at a prompt, the old value stays.

### Step 16: Build The Main Loop

Now connect everything with `main()`.

```python
def main():
    inventory = Inventory(SAVE_PATH)

    print("Inventory Tracker")

    try:
        loaded = inventory.load()
    except ValueError as error:
        print(f"Could not load saved inventory: {error}")
    except OSError as error:
        print(f"Could not read the inventory file: {error}")
    else:
        if loaded:
            print(f"Loaded {len(inventory.items)} item(s).")
        else:
            print("No saved inventory found yet.")

    while True:
        show_menu()
        choice = input("Choose an option: ").strip()

        if choice == "1":
            list_items(inventory)
        elif choice == "2":
            add_item_from_menu(inventory)
        elif choice == "3":
            update_item_from_menu(inventory)
        elif choice == "4":
            try:
                inventory.save()
            except OSError as error:
                print(f"Could not save inventory: {error}")
            else:
                print(f"Saved {len(inventory.items)} item(s) to {inventory.save_path}.")
        elif choice == "5":
            try:
                loaded = inventory.load()
            except ValueError as error:
                print(f"Could not load inventory: {error}")
            except OSError as error:
                print(f"Could not read the inventory file: {error}")
            else:
                if loaded:
                    print(f"Loaded {len(inventory.items)} item(s).")
                else:
                    print("No saved inventory found yet.")
        elif choice == "6":
            print("Goodbye.")
            break
        else:
            print("Choose a number from 1 to 6.")
```

Then add the usual script guard:

```python
if __name__ == "__main__":
    main()
```

That line makes the app run when the file is started directly.

### Step 17: Put The Full Program Together

Here is the full project code.

```python
import json
from pathlib import Path


SAVE_PATH = Path("day-90/inventory.json")


class InventoryItem:
    def __init__(self, name, quantity, price):
        self.name = name
        self.quantity = quantity
        self.price = price

    def display_line(self, number):
        return f"{number}. {self.name} - {self.quantity} in stock - ${self.price:.2f} each"

    def to_dict(self):
        return {
            "name": self.name,
            "quantity": self.quantity,
            "price": self.price
        }


class Inventory:
    def __init__(self, save_path):
        self.save_path = Path(save_path)
        self.items = []

    def add_item(self, name, quantity, price):
        item = InventoryItem(name, quantity, price)
        self.items.append(item)

    def find_item(self, name):
        search_name = name.lower()

        for item in self.items:
            if item.name.lower() == search_name:
                return item

        return None

    def save(self):
        self.save_path.parent.mkdir(parents=True, exist_ok=True)

        data = []

        for item in self.items:
            data.append(item.to_dict())

        with self.save_path.open("w", encoding="utf-8") as file:
            json.dump(data, file, indent=4)

    def load(self):
        if not self.save_path.exists():
            self.items = []
            return False

        try:
            with self.save_path.open("r", encoding="utf-8") as file:
                data = json.load(file)
        except json.JSONDecodeError as error:
            raise ValueError("The save file is not valid JSON.") from error

        if not isinstance(data, list):
            raise ValueError("The save file should contain a list of items.")

        loaded_items = []

        for record in data:
            if not isinstance(record, dict):
                raise ValueError("Each saved item should be a dictionary.")

            try:
                name = str(record["name"]).strip()
                quantity = int(record["quantity"])
                price = float(record["price"])
            except (KeyError, TypeError, ValueError) as error:
                raise ValueError("One saved item has missing or invalid fields.") from error

            if name == "":
                raise ValueError("One saved item has a blank name.")

            if quantity < 0:
                raise ValueError("One saved item has a negative quantity.")

            if price < 0:
                raise ValueError("One saved item has a negative price.")

            loaded_items.append(InventoryItem(name, quantity, price))

        self.items = loaded_items
        return True


def ask_for_quantity(prompt):
    raw_value = input(prompt).strip()

    try:
        quantity = int(raw_value)
    except ValueError:
        print("Please enter a whole number for the quantity.")
        return None

    if quantity < 0:
        print("Quantity cannot be negative.")
        return None

    return quantity


def ask_for_price(prompt):
    raw_value = input(prompt).strip()

    try:
        price = float(raw_value)
    except ValueError:
        print("Please enter a number for the price.")
        return None

    if price < 0:
        print("Price cannot be negative.")
        return None

    return price


def show_menu():
    print()
    print("Menu:")
    print("1. List items")
    print("2. Add item")
    print("3. Update item")
    print("4. Save inventory")
    print("5. Load inventory")
    print("6. Quit")


def list_items(inventory):
    if not inventory.items:
        print("No inventory items yet.")
        return

    print()
    print("Inventory:")

    for index, item in enumerate(inventory.items, start=1):
        print(item.display_line(index))


def add_item_from_menu(inventory):
    name = input("Item name: ").strip()

    if name == "":
        print("Item name cannot be blank.")
        return

    if inventory.find_item(name) is not None:
        print("That item already exists. Use update instead.")
        return

    quantity = ask_for_quantity("Quantity: ")

    if quantity is None:
        return

    price = ask_for_price("Price: ")

    if price is None:
        return

    inventory.add_item(name, quantity, price)
    print(f"Added {name}.")


def update_item_from_menu(inventory):
    name = input("Item to update: ").strip()

    if name == "":
        print("Item name cannot be blank.")
        return

    item = inventory.find_item(name)

    if item is None:
        print("No item found with that name.")
        return

    print("Current item:")
    print(item.display_line(1))

    raw_quantity = input("New quantity (leave blank to keep current): ").strip()

    if raw_quantity != "":
        try:
            quantity = int(raw_quantity)
        except ValueError:
            print("Please enter a whole number for the quantity.")
            return

        if quantity < 0:
            print("Quantity cannot be negative.")
            return

        item.quantity = quantity

    raw_price = input("New price (leave blank to keep current): ").strip()

    if raw_price != "":
        try:
            price = float(raw_price)
        except ValueError:
            print("Please enter a number for the price.")
            return

        if price < 0:
            print("Price cannot be negative.")
            return

        item.price = price

    print(f"Updated {item.name}.")


def main():
    inventory = Inventory(SAVE_PATH)

    print("Inventory Tracker")

    try:
        loaded = inventory.load()
    except ValueError as error:
        print(f"Could not load saved inventory: {error}")
    except OSError as error:
        print(f"Could not read the inventory file: {error}")
    else:
        if loaded:
            print(f"Loaded {len(inventory.items)} item(s).")
        else:
            print("No saved inventory found yet.")

    while True:
        show_menu()
        choice = input("Choose an option: ").strip()

        if choice == "1":
            list_items(inventory)
        elif choice == "2":
            add_item_from_menu(inventory)
        elif choice == "3":
            update_item_from_menu(inventory)
        elif choice == "4":
            try:
                inventory.save()
            except OSError as error:
                print(f"Could not save inventory: {error}")
            else:
                print(f"Saved {len(inventory.items)} item(s) to {inventory.save_path}.")
        elif choice == "5":
            try:
                loaded = inventory.load()
            except ValueError as error:
                print(f"Could not load inventory: {error}")
            except OSError as error:
                print(f"Could not read the inventory file: {error}")
            else:
                if loaded:
                    print(f"Loaded {len(inventory.items)} item(s).")
                else:
                    print("No saved inventory found yet.")
        elif choice == "6":
            print("Goodbye.")
            break
        else:
            print("Choose a number from 1 to 6.")


if __name__ == "__main__":
    main()
```

## Try It Yourself

Run the app from your course folder:

```bash
python day-90/inventory_tracker.py
```

If your computer uses `py`, use:

```bash
py day-90/inventory_tracker.py
```

If your computer uses `python3`, use:

```bash
python3 day-90/inventory_tracker.py
```

Try this test path through the menu:

```text
2
notebook
12
2.50
1
3
notebook
15

1
4
6
```

That means:

```text
add an item
list the inventory
update the item quantity
keep the old price
list the inventory again
save
quit
```

After saving, open:

```text
day-90/inventory.json
```

You should see a JSON list with your saved item.

Then run the program again.

It should load the saved inventory at startup.

## Common Mistake

A common mistake is trying to save objects directly with `json.dump()`.

This will not work:

```python
item = InventoryItem("notebook", 12, 2.5)

with open("day-90/inventory.json", "w", encoding="utf-8") as file:
    json.dump(item, file)
```

Python does not know how to turn your custom object into JSON by itself.

Save a dictionary instead:

```python
item = InventoryItem("notebook", 12, 2.5)

with open("day-90/inventory.json", "w", encoding="utf-8") as file:
    json.dump(item.to_dict(), file)
```

In the full project, you save a list of dictionaries because the inventory has many items.

Another common mistake is forgetting that `input()` always gives you a string.

This looks numeric to a person:

```text
12
```

But from `input()`, it starts as text:

```python
raw_quantity = input("Quantity: ")
```

Convert it before doing number work:

```python
quantity = int(raw_quantity)
```

Then handle the case where the user types something that is not a number.

## Debug It

Use these small checks when the full project is not behaving.

### Bug 1: The Saved File Is Empty

If `day-90/inventory.json` is created but has no useful data, check whether the inventory list had items before saving.

Add this temporary line before `inventory.save()`:

```python
print(len(inventory.items))
```

If it prints `0`, the save method is working with an empty list.

The problem is earlier in the menu path.

Check that `add_item_from_menu()` reaches this line:

```python
inventory.add_item(name, quantity, price)
```

### Bug 2: The Program Cannot Find An Item To Update

If you add `Notebook` and search for `notebook`, the update should still find it.

That is why `find_item()` lowercases both names:

```python
if item.name.lower() == search_name:
```

If updates are not finding items, check that the method still compares lowercase text with lowercase text.

### Bug 3: Loading Replaces Current Unsaved Items

The load feature reads the save file and replaces `self.items` with the loaded list.

This line does the replacement:

```python
self.items = loaded_items
```

That is intentional for today's simple app.

If you add an item and choose load before saving, your unsaved item can disappear.

For now, treat load as:

```text
make the app match the save file
```

In a larger app, you might ask the user before replacing unsaved changes.

### Bug 4: The Menu Keeps Going After Bad Input

Most menu actions use `return` when something goes wrong.

For example:

```python
if quantity is None:
    return
```

That stops the current menu action.

It does not stop the whole program.

The outer `while True` loop still shows the menu again.

That is the behavior you want for a command-line app.

## Read the Docs

Today, look at these official Python documentation pages:

[Python documentation: `json`](https://docs.python.org/3/library/json.html)

Look for:

- `json.dump()`
- `json.load()`
- `json.JSONDecodeError`

[Python documentation: `pathlib`](https://docs.python.org/3/library/pathlib.html)

Look for:

- `Path`
- `.exists()`
- `.open()`
- `.parent`
- `.mkdir()`

[Python documentation: classes](https://docs.python.org/3/tutorial/classes.html)

Look for:

- class definitions
- instance objects
- method objects
- instance variables

You do not need to understand the whole classes page today.

Use it to notice that your `InventoryItem` and `Inventory` objects are normal Python objects with attributes and methods.

## Mini Challenge

Add a total value feature.

One item's total value is:

```text
quantity * price
```

Add this method inside `InventoryItem`:

```python
def total_value(self):
    return self.quantity * self.price
```

Then update `display_line()` so it includes the total:

```python
def display_line(self, number):
    return (
        f"{number}. {self.name} - {self.quantity} in stock - "
        f"${self.price:.2f} each - total ${self.total_value():.2f}"
    )
```

Test it by adding:

```text
notebook
12
2.50
```

The total should be:

```text
$30.00
```

## Real-World Use

Inventory systems appear in many places.

A small shop tracks products and stock levels.

A classroom tracks supplies.

A repair desk tracks spare parts.

A home project might track tools, paint, cables, or books.

The real systems are larger, but the beginner shape is the same:

```text
one record
many records
add records
update records
save records
load records
handle bad input
```

Classes help by giving the important ideas names.

`InventoryItem` is one record.

`Inventory` is the collection of records.

The menu is only one way to use those classes.

Later, the same classes could be used from tests, a web app, or a graphical app.

## Recap

Today you built a command-line inventory tracker.

You used one class for a single item and another class for the full inventory.

You added methods that display items, convert items to dictionaries, add items, find items, save items, and load items.

You used JSON so the program can remember data after it closes.

You also handled common problems:

- missing save files
- broken JSON
- blank names
- duplicate names
- invalid quantities
- invalid prices
- file read and write errors

The main idea:

```text
Use classes to keep related data and behavior together.
Use dictionaries as the bridge between objects and JSON.
```

## Lesson Checklist

Before moving on, make sure you can:

- explain what one `InventoryItem` object stores
- explain what the `Inventory` object manages
- write an `__init__` method with `self`
- call a method on an object
- use a list to store many objects
- find one object in a list by checking an attribute
- convert an object into a dictionary
- save a list of dictionaries with `json.dump()`
- load JSON with `json.load()`
- convert loaded dictionaries back into objects
- handle `ValueError` from bad numeric input
- handle `json.JSONDecodeError` from broken JSON
- explain why loading replaces the current inventory list

## Exercises

### Exercise 1: Add A Category

Add a `category` attribute to each inventory item.

Update:

- `InventoryItem.__init__()`
- `InventoryItem.to_dict()`
- `Inventory.load()`
- `add_item_from_menu()`
- `display_line()`

Example categories:

```text
school
kitchen
tools
books
```

Save the inventory and check that the category appears in `day-90/inventory.json`.

### Exercise 2: Add A Delete Option

Add a menu choice named:

```text
Delete item
```

Begin with a method on `Inventory`:

```python
def delete_item(self, name):
    item = self.find_item(name)

    if item is None:
        return False

    self.items.remove(item)
    return True
```

Then add a menu function that asks for the item name and prints whether the item was deleted.

### Exercise 3: Show Low Stock Items

Add a menu choice that asks for a maximum quantity.

If the user enters:

```text
5
```

show every item with quantity less than or equal to `5`.

Use this shape:

```python
for item in inventory.items:
    if item.quantity <= maximum:
        print(item.display_line(index))
```

You will need to decide how to count the displayed matches.

### Exercise 4: Add Automatic Save On Quit

Change the quit option so it saves before saying goodbye.

Use the same `try` and `except OSError` shape from the save menu option.

Test this path:

```text
2
pencil
20
0.25
6
```

Then run the app again and check whether `pencil` loads.

### Exercise 5: Reject Duplicate Names During Load

Right now, a manually edited JSON file could contain duplicate item names.

Change `load()` so it rejects duplicates.

Hint:

```python
seen_names = set()
```

Store lowercase names in the set.

If a lowercase name is already in the set, raise `ValueError`.

### Exercise 6: Sort Items Before Listing

Change `list_items()` so it displays items alphabetically by name.

Hint:

```python
sorted_items = sorted(inventory.items, key=lambda item: item.name.lower())
```

Then loop through `sorted_items` instead of `inventory.items`.

### Exercise 7: Save A Backup File

Add a second save path:

```python
BACKUP_PATH = Path("day-90/inventory_backup.json")
```

Add a menu option that saves the same inventory data to the backup path.

You can create a second `Inventory` object with a different path, or you can write a method that accepts a path.

Choose the version that is easier for you to explain.

### Exercise 8: Plan Three Test Runs

Write three planned test runs before using the app.

Include:

- the menu choices you will type
- the item names you will use
- the quantities and prices you will use
- the result you expect

At least one test should use invalid input, such as:

```text
quantity: twelve
price: -3
```

Good testing is planned before the bug appears.

## Tiny Win

You built a project that remembers.

That is a big step for a beginner program.

The data is no longer trapped inside one run of the script.

You also used classes for a practical reason, not just as a syntax exercise.

`InventoryItem` and `Inventory` give the project a clear shape.

That shape is what lets the menu stay readable while the project grows.

## Tomorrow

Tomorrow is a planning day for the next larger build.

Day 91 will slow down before writing code.

You will take a project idea and turn it into a small plan:

- what the user can do
- what data the program needs
- which classes or functions might belong together
- what files the project should use
- what test runs should prove the project works

That planning habit matters more as your programs get larger.

Today's inventory tracker gives you the raw material for that planning work:

```text
features
data
classes
files
errors
tests
```

Tomorrow you will learn how to sketch those pieces before the code gets long.
