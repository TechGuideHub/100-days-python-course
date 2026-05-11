# Day 91: Planning a Program

**Focus:** Turning an idea into a clear plan before writing code  
**You will practice:** problem statements, inputs and outputs, data models, function and class lists, small milestones, pseudocode, edge cases, test cases, and knowing when to pause before coding  
**Estimated time:** 60-75 minutes

## Today's Goal

Today you will practice planning a program before writing the first real lines of code.

That may sound less exciting than building something.

But planning is one of the habits that helps beginners become builders.

When a program is small, you can sometimes start typing and find your way. As programs get larger, that approach starts to hurt. You forget what the program is supposed to do. You store data in a shape that becomes awkward later. You write one giant function because you did not name the smaller jobs yet.

Planning does not mean writing a long document.

For a beginner project, a useful plan might fit on one page.

By the end of today, you should be able to:

- write a clear problem statement
- list the inputs a program needs
- list the outputs a program should produce
- describe the data model before coding
- name the main functions or classes
- split a project into small milestones
- write pseudocode for the main flow
- name edge cases before they surprise you
- write a few manual test cases
- avoid starting with code before the problem is clear
- prepare for Day 92, where command-line arguments will let users give input when they run a program

Today is not about making a perfect plan.

It is about making a plan good enough to keep your code from wandering.

## The Big Idea

A program plan answers a few simple questions:

```text
What problem does this program solve?
What information goes in?
What should come out?
What data shape will the program use?
What are the main jobs inside the program?
What is the smallest useful version?
What could go wrong?
How will I check that it works?
```

Those questions turn a vague idea into something buildable.

Compare these two project ideas.

Vague:

```text
Make an inventory app.
```

Clearer:

```text
Make a program that reads a small list of inventory items,
finds items whose quantity is at or below their reorder level,
and prints a short low-stock report.
```

The second version gives you handles.

You can already see:

- input: inventory items
- output: a low-stock report
- data: item name, quantity, reorder level
- rule: quantity at or below reorder level
- first milestone: make the report work with a small list in the code

That is planning.

You are not predicting every line of code.

You are making the next few lines less mysterious.

## The Mental Model

Think of a program plan like a sketch before a drawing.

The sketch is not the final work. It does not have every detail. But it helps you place the important parts before you spend time polishing.

A beginner-friendly plan usually has these parts:

```text
1. Problem statement
2. Inputs
3. Outputs
4. Data model
5. Functions or classes
6. Milestones
7. Pseudocode
8. Edge cases
9. Test cases
```

Here is what each part means.

### Problem Statement

The problem statement says what the program is for.

Keep it short.

For an inventory program:

```text
The program helps a shop owner find which items need to be reordered.
```

For a weather program:

```text
The program shows a short weather summary for one city.
```

The problem statement protects you from adding random features too early.

If the problem is:

```text
Find low-stock items.
```

Then this can wait:

```text
Add product photos.
Send email alerts.
Make charts.
Track supplier contracts.
```

Those might be useful later, but they do not belong in the first version.

### Inputs

Inputs are the information the program needs.

Inventory example:

```text
- item name
- current quantity
- reorder level
```

Weather example:

```text
- city name
- unit choice, such as celsius or fahrenheit
```

Inputs can come from different places:

- typed by the user
- stored in a file
- written directly in the code for early practice
- received from an API
- passed as command-line arguments

Day 92 will focus on that last one.

For today, just name the inputs.

### Outputs

Outputs are what the program gives back.

Inventory example:

```text
Low-stock report
- markers: 3 left, reorder at 5
- clips: 0 left, reorder at 10
```

Weather example:

```text
Weather for Tokyo
Condition: Partly cloudy
Temperature: 24 C
Rain chance: 10%
```

Output does not always mean printing.

A program might:

- print text
- save a file
- return a value from a function
- show a web page
- update a database

For this course, many beginner programs print text first.

That is a good first version.

### Data Model

The data model describes how the program stores the important information.

This is one of the most useful planning steps.

For inventory, one item might be a dictionary:

```python
item = {
    "name": "markers",
    "quantity": 3,
    "reorder_at": 5,
}
```

A full inventory could be a list of dictionaries:

```python
inventory = [
    {"name": "pencils", "quantity": 24, "reorder_at": 10},
    {"name": "markers", "quantity": 3, "reorder_at": 5},
    {"name": "paper", "quantity": 120, "reorder_at": 50},
]
```

You could also use a class:

```text
InventoryItem
- name
- quantity
- reorder_at
```

Both choices can work.

For a first version, dictionaries are often faster to write and easier to inspect. Classes become helpful when the same kind of thing has more behavior attached to it.

For weather, a summary might be a dictionary:

```python
weather_summary = {
    "city": "Tokyo",
    "condition": "Partly cloudy",
    "temperature": 24,
    "unit": "C",
}
```

Before you code, ask:

```text
What does one record look like?
What does a collection of records look like?
What names will I use for each field?
```

Good field names make the rest of the program easier to read.

### Functions And Classes

After the data model, list the jobs the program needs to do.

Do not write full code yet. Just name the pieces.

For the inventory program:

```text
needs_reorder(item)
    Decide whether one item is low.

find_low_stock_items(inventory)
    Return the items that need to be reordered.

format_low_stock_report(items)
    Turn low-stock items into readable text.

main()
    Put the steps together.
```

For the weather program:

```text
get_city_from_user()
    Ask for a city name.

fetch_weather(city)
    Get weather data for the city.

make_weather_summary(raw_data)
    Pull out only the values the user needs.

display_weather(summary)
    Print the summary.
```

A function list helps you avoid one giant block of code.

It also gives you small pieces to test.

### Milestones

Milestones are small versions of the program that work.

They keep you moving.

Inventory milestones:

```text
1. Store three inventory items directly in the code.
2. Print every item name and quantity.
3. Print only low-stock items.
4. Move the low-stock check into a function.
5. Format a neat report.
6. Later, read the inventory from a file.
7. Later, accept a file path from the command line.
```

Notice the word "later."

Good planning includes deciding what not to build yet.

### Pseudocode

Pseudocode is a rough version of the program in human-readable steps.

It is not Python, but it should be close enough that you can turn it into Python.

Inventory pseudocode:

```text
start with inventory items

create an empty list for low-stock items

for each item in inventory:
    if the quantity is less than or equal to the reorder level:
        add the item to the low-stock list

if the low-stock list is empty:
    print "All items are stocked."
else:
    print a heading
    for each low-stock item:
        print its name, quantity, and reorder level
```

Pseudocode is useful because it lets you fix the logic before you fight the syntax.

### Edge Cases

An edge case is a situation that is unusual but still possible.

Inventory edge cases:

```text
- the inventory list is empty
- no items are low
- every item is low
- an item has quantity 0
- an item is exactly at the reorder level
- an item is missing a field
- a quantity is typed as text instead of a number
```

Weather edge cases:

```text
- the city name is blank
- the city cannot be found
- the weather service is unavailable
- the response is missing temperature
- the user asks for an unsupported unit
```

You do not need to solve every edge case in version one.

But naming them helps you choose which ones matter now.

### Test Cases

A test case is one specific check.

Before you write code, write a few examples of what should happen.

Inventory test cases:

```text
Case 1:
Input: markers quantity 3, reorder at 5
Result: markers should be low stock

Case 2:
Input: paper quantity 120, reorder at 50
Result: paper should not be low stock

Case 3:
Input: clips quantity 10, reorder at 10
Result: clips should be low stock

Case 4:
Input: empty inventory list
Result: print that there are no items to check
```

These tests force you to decide important rules.

For example:

```text
Does exactly equal to the reorder level count as low stock?
```

In this lesson, yes.

That means the code should use:

```text
quantity <= reorder_at
```

not:

```text
quantity < reorder_at
```

## Example

Let's plan a small inventory report.

### Step 1: Problem Statement

```text
Create a program that finds inventory items whose quantity is at or below
their reorder level and prints a short report.
```

This is specific enough to build.

It says:

- what the program reads
- what rule it uses
- what it prints

### Step 2: Inputs And Outputs

Inputs:

```text
A list of inventory items.

Each item has:
- name
- quantity
- reorder_at
```

Output:

```text
A printed report showing only items that need to be reordered.
```

If nothing is low, the program should say:

```text
All items are stocked.
```

### Step 3: Data Model

One item:

```python
{"name": "markers", "quantity": 3, "reorder_at": 5}
```

Many items:

```python
inventory = [
    {"name": "pencils", "quantity": 24, "reorder_at": 10},
    {"name": "markers", "quantity": 3, "reorder_at": 5},
    {"name": "paper", "quantity": 120, "reorder_at": 50},
]
```

This is enough for the first version.

### Step 4: Function List

```text
needs_reorder(item)
    Return True if item quantity is at or below reorder_at.

find_low_stock_items(inventory)
    Return a list of items that need reorder.

format_report(low_stock_items)
    Return a readable report as text.
```

This list is small, but it already gives the program structure.

### Step 5: Milestones

```text
1. Make `needs_reorder()` work for one item.
2. Make `find_low_stock_items()` work for a list.
3. Make `format_report()` print useful text.
4. Put the functions together with sample data.
5. Later, let the user choose an inventory file.
```

Milestone 5 is a bridge to Day 92.

After tomorrow's lesson, the program might eventually run like this:

```text
python inventory_report.py --file inventory.csv
```

You do not need to build that today.

Today you are making the plan ready for it.

### Step 6: A Small Python Version

Here is a small version that follows the plan.

```python
def needs_reorder(item):
    return item["quantity"] <= item["reorder_at"]


def find_low_stock_items(inventory):
    low_stock_items = []

    for item in inventory:
        if needs_reorder(item):
            low_stock_items.append(item)

    return low_stock_items


def format_report(low_stock_items):
    if not low_stock_items:
        return "All items are stocked."

    lines = ["Low-stock items:"]

    for item in low_stock_items:
        line = f"- {item['name']}: {item['quantity']} left, reorder at {item['reorder_at']}"
        lines.append(line)

    return "\n".join(lines)


inventory = [
    {"name": "pencils", "quantity": 24, "reorder_at": 10},
    {"name": "markers", "quantity": 3, "reorder_at": 5},
    {"name": "paper", "quantity": 120, "reorder_at": 50},
    {"name": "clips", "quantity": 10, "reorder_at": 10},
]

low_stock_items = find_low_stock_items(inventory)
report = format_report(low_stock_items)

print(report)
```

You should see:

```text
Low-stock items:
- markers: 3 left, reorder at 5
- clips: 10 left, reorder at 10
```

The code is not long because the plan did some of the thinking first.

### Step 7: Check The Smallest Rule

Before trusting the full report, check the smallest rule.

```python
def needs_reorder(item):
    return item["quantity"] <= item["reorder_at"]


print(needs_reorder({"name": "markers", "quantity": 3, "reorder_at": 5}))
print(needs_reorder({"name": "paper", "quantity": 120, "reorder_at": 50}))
print(needs_reorder({"name": "clips", "quantity": 10, "reorder_at": 10}))
```

You should see:

```text
True
False
True
```

That last `True` matters.

It confirms the rule:

```text
At the reorder level counts as low stock.
```

## Try It Yourself

Create a folder named:

```text
day-91
```

Inside it, create this file:

```text
day-91/plan.txt
```

You are going to write a plan before writing a full program.

Choose one project:

```text
Option A: Inventory low-stock report
Option B: Weather summary program
```

Use this template.

```text
Project name:

Problem statement:

Inputs:

Outputs:

Data model:

Functions or classes:

Milestones:

Pseudocode:

Edge cases:

Test cases:

Future command-line arguments:
```

Here is a filled-in start for the inventory option.

```text
Project name:
Inventory low-stock report

Problem statement:
Find items whose quantity is at or below their reorder level and print a report.

Inputs:
- item name
- quantity
- reorder_at

Outputs:
- a printed low-stock report
- a message if all items are stocked

Data model:
Each item is a dictionary with name, quantity, and reorder_at.
The inventory is a list of item dictionaries.

Functions or classes:
- needs_reorder(item)
- find_low_stock_items(inventory)
- format_report(low_stock_items)
- main()
```

Now finish the rest of the template in your own words.

If you choose the weather option, keep the first version small.

For example:

```text
Project name:
Weather summary program

Problem statement:
Show a short weather summary for one city.

Inputs:
- city name
- temperature unit

Outputs:
- city name
- condition
- temperature
- rain chance

Data model:
Use a summary dictionary with city, condition, temperature, unit, and rain_chance.
```

Do not write the whole weather app today.

Your goal is to make the plan clear enough that the first coding step is obvious.

## Common Mistake

The common mistake is starting with code because planning feels like delay.

You might think:

```text
I will understand the program once I start writing it.
```

Sometimes that works for a tiny exercise.

For a larger program, it often creates a messy first hour:

- you change variable names over and over
- you mix input, logic, and printing in one place
- you forget the rule you meant to use
- you build features that do not belong in version one
- you cannot tell whether the program is correct

Planning is not a separate fancy step.

It is part of programming.

Another common mistake is planning too much.

This is too large for today:

```text
Build a full inventory system with users, suppliers, categories, charts,
email alerts, barcode scanning, and a web dashboard.
```

A better first version is:

```text
Given a few inventory items, print the ones that need reorder.
```

You can always grow a working small program.

It is much harder to rescue a huge unfinished one.

## Debug It

Planning can have bugs too.

Here is a weak plan:

```text
Make an inventory program.
Use a list.
Print the result.
```

The plan is not wrong, but it does not answer enough questions.

Debug it by asking:

```text
What kind of inventory program?
What is inside the list?
What counts as low stock?
What should the printed result look like?
What should happen if nothing is low?
```

A stronger version:

```text
Problem:
Find inventory items that need reorder.

Input:
A list of dictionaries. Each dictionary has name, quantity, and reorder_at.

Rule:
An item needs reorder when quantity is less than or equal to reorder_at.

Output:
Print one line for each low-stock item.
If no items are low, print "All items are stocked."
```

Now you can test the rule directly:

```python
def needs_reorder(item):
    return item["quantity"] <= item["reorder_at"]


test_items = [
    {"name": "markers", "quantity": 3, "reorder_at": 5},
    {"name": "paper", "quantity": 120, "reorder_at": 50},
    {"name": "clips", "quantity": 10, "reorder_at": 10},
]

for item in test_items:
    print(item["name"], needs_reorder(item))
```

You should see:

```text
markers True
paper False
clips True
```

If you expected `clips` to be `False`, the code is not the only thing to inspect.

You need to inspect the rule.

Good debugging often means asking:

```text
Is the code wrong, or is my plan unclear?
```

## Read the Docs

Planning also changes how you read documentation.

Instead of opening a documentation page and hoping something makes sense, arrive with a question from your plan.

For example, if your future weather program needs a command-line city, your question might be:

```text
How does Python read a value like --city Tokyo?
```

That points you toward `argparse`, which you will use on Day 92.

For today, skim the names only:

```text
argparse
ArgumentParser
add_argument
parse_args
```

Do not try to memorize them yet.

Just notice that command-line input has its own vocabulary:

```text
argument
option
flag
positional argument
```

Your plan helps you decide which of those you need.

For the inventory program, future command-line arguments might be:

```text
--file inventory.csv
--show low-stock
```

For the weather program:

```text
--city Tokyo
--unit celsius
```

Tomorrow those ideas become real Python.

## Mini Challenge

Write a plan for this small program:

```text
Packing helper
```

The program should help someone decide what to pack based on the weather.

Keep the first version simple:

```text
Inputs:
- condition, such as rain, sun, cold, or hot
- number of days

Outputs:
- a short packing list
```

Use this data model:

```python
packing_rules = {
    "rain": ["umbrella", "waterproof shoes"],
    "sun": ["sunglasses", "hat"],
    "cold": ["jacket", "warm socks"],
    "hot": ["water bottle", "light shirts"],
}
```

Write:

- a problem statement
- three milestones
- pseudocode
- three edge cases
- three test cases

Then write only this one function:

```python
def get_packing_items(condition, rules):
    return rules.get(condition, [])
```

Try it:

```python
packing_rules = {
    "rain": ["umbrella", "waterproof shoes"],
    "sun": ["sunglasses", "hat"],
    "cold": ["jacket", "warm socks"],
    "hot": ["water bottle", "light shirts"],
}

print(get_packing_items("rain", packing_rules))
print(get_packing_items("wind", packing_rules))
```

You should see:

```text
['umbrella', 'waterproof shoes']
[]
```

The empty list is a design choice.

Your plan should say what an unknown condition means.

## Real-World Use

Professional programmers plan constantly, even when the plan is small.

They may call it:

- a ticket
- a design note
- a checklist
- a project brief
- a README
- an issue description
- acceptance criteria

The names change, but the habit is the same.

Before building, they ask:

```text
What are we trying to make true?
How will someone use it?
What data does it need?
What are the first few pieces?
How will we know it works?
```

For an inventory tool, planning prevents unclear rules like:

```text
Is 10 items low if the reorder level is 10?
```

For a weather tool, planning prevents mixed-up input like:

```text
Is "Paris" a city typed during the program,
or should it be passed when the program starts?
```

That second question matters for Day 92.

Command-line arguments are easier when you already know the program's inputs.

## Recap

Today you learned that a program plan should name:

- the problem the program solves
- the inputs it needs
- the outputs it should produce
- the data model it will use
- the functions or classes that divide the work
- the milestones that create a small working version
- the pseudocode for the main flow
- the edge cases that might cause trouble
- the test cases that show whether the program works

You also saw that planning is not about writing a perfect document.

It is about making clear decisions before code hides them.

The most useful beginner planning question is:

```text
What is the smallest version that proves the idea works?
```

Answer that, build it, then improve from there.

## Lesson Checklist

Before moving on, make sure you can:

- write a one-sentence problem statement
- separate inputs from outputs
- describe one record in a data model
- describe a collection of records
- list functions before writing them
- decide whether a class might help
- split a project into milestones
- write pseudocode for the main flow
- name at least three edge cases
- write at least three test cases
- explain why starting with code too soon can make a program harder
- describe one possible command-line argument for a future version

## Exercises

### Exercise 1: Write The Problem Statement

Create this file:

```text
day-91/inventory_plan.txt
```

Write a one-sentence problem statement for an inventory report.

It should mention:

- inventory items
- low stock
- printed report

Keep it specific.

### Exercise 2: List Inputs And Outputs

In the same file, add:

```text
Inputs:

Outputs:
```

For inputs, include at least three fields one inventory item needs.

For outputs, describe what the user should see.

### Exercise 3: Choose A Data Model

Write the shape of one inventory item.

Use this as a starting point:

```python
{
    "name": "markers",
    "quantity": 3,
    "reorder_at": 5,
}
```

Then write one sentence explaining why a list of dictionaries can represent the full inventory.

### Exercise 4: Name The Functions

Add a function list.

Use short names and one job per function.

Starter list:

```text
needs_reorder(item)
find_low_stock_items(inventory)
format_report(low_stock_items)
main()
```

Under each function, write one sentence saying what it should do.

### Exercise 5: Write Pseudocode

Write pseudocode for the inventory report.

Use plain steps.

Include:

- starting with an inventory list
- checking each item
- collecting low-stock items
- printing a message if none are low
- printing each low-stock item if some are low

### Exercise 6: Find Edge Cases

Write at least five edge cases.

Include these two:

```text
The inventory list is empty.
An item quantity is exactly equal to reorder_at.
```

Then add three of your own.

### Exercise 7: Write Test Cases

Write at least four test cases.

Use this format:

```text
Case:
Input:
Result:
```

Make sure one test checks an item exactly at the reorder level.

### Exercise 8: Plan A Weather Version

Create this file:

```text
day-91/weather_plan.txt
```

Write a short plan for a weather summary program.

Include:

- problem statement
- inputs
- outputs
- data model
- function list
- edge cases
- test cases

Keep it smaller than the Day 80 project.

This is a planning exercise, not a full rebuild.

### Exercise 9: Prepare For Command-Line Arguments

At the bottom of either plan file, add a section named:

```text
Future command-line arguments:
```

For inventory, you might write:

```text
--file inventory.csv
--show low-stock
```

For weather, you might write:

```text
--city Tokyo
--unit celsius
```

Write one sentence explaining what each argument would control.

### Exercise 10: Build One Tiny Function

Create this file:

```text
day-91/reorder_rule.py
```

Write only the reorder rule function and a few checks.

Starter code:

```python
def needs_reorder(item):
    return item["quantity"] <= item["reorder_at"]


print(needs_reorder({"name": "markers", "quantity": 3, "reorder_at": 5}))
print(needs_reorder({"name": "paper", "quantity": 120, "reorder_at": 50}))
print(needs_reorder({"name": "clips", "quantity": 10, "reorder_at": 10}))
```

You should see:

```text
True
False
True
```

This is the bridge from planning to coding.

The plan names the rule.

The function proves the rule.

## Tiny Win

You practiced a skill that makes every later project easier.

You can now slow down for a few minutes, name the shape of a program, and then code with more direction.

That is not busywork.

That is how bigger programs become less intimidating.

## Tomorrow

Tomorrow you will learn command-line arguments.

Today you wrote future inputs like:

```text
--city Tokyo
--unit celsius
--file inventory.csv
```

On Day 92, you will learn how Python can read values like those when the program starts.

That means your programs will become easier to reuse:

```text
python weather_summary.py --city Tokyo --unit celsius
python inventory_report.py --file inventory.csv
```

The planning work from today will help because command-line arguments are just another way to answer a planning question:

```text
What information does this program need before it can do its job?
```
