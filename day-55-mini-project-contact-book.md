# Day 55: Mini Project: Contact Book

**Focus:** Building a command-line contact book with lists of dictionaries, loops, menu choices, search, and simple updates  
**You will practice:** lists of dictionaries, `input()`, `while` loops, `for` loops, menu choices, adding records, viewing records, searching by name, updating one field, and quitting cleanly  
**Estimated time:** 60-75 minutes

## Today's Goal

Today you will build a small contact book.

The app will run in the command line. It will let the user add contacts, view contacts, search by name, update a phone number, and quit.

By the end of this lesson, you should be able to:

- store one contact as a dictionary
- store many contacts as a list of dictionaries
- use the same keys for every contact record
- add a new dictionary to a list
- loop through all contacts
- search contacts by name
- update one field in one contact
- build a menu that keeps running
- use `break` to quit cleanly
- test a command-line program with planned inputs
- debug common list-of-dictionaries mistakes

This mini-project combines the dictionary tools you have been practicing.

The goal is not to build a full phone app. The goal is to make one small program that can remember several records while it is running.

The contact book will not save to a file yet. When the program closes, the contacts are gone. That is normal for today.

## The Project

Create this file:

```text
day-55/contact_book.py
```

The program will:

- start with an empty contacts list
- show a simple menu
- let the user choose an option
- add one contact at a time
- store each contact as a dictionary
- show all contacts in a readable way
- search for contacts by name
- update a contact's phone number
- avoid adding contacts with blank names
- keep running until the user chooses quit
- print a closing message before stopping

Example:

```text
Contact Book
Store contacts while the program is running.

Menu:
1. View contacts
2. Add contact
3. Search by name
4. Update phone number
5. Quit
Choose an option: 2
Name: Mina
Phone: 555-0104
Email: mina@example.com
Added contact: Mina

Menu:
1. View contacts
2. Add contact
3. Search by name
4. Update phone number
5. Quit
Choose an option: 1
Contacts:
1. Mina
   Phone: 555-0104
   Email: mina@example.com
Total contacts: 1

Menu:
1. View contacts
2. Add contact
3. Search by name
4. Update phone number
5. Quit
Choose an option: 5
You saved 1 contact during this run.
Goodbye.
```

The exact contacts depend on what the user types.

This app has the same basic shape as other command-line menu programs:

```text
create starting data
while the app is running:
    show choices
    ask for a choice
    run the matching action
    quit if the user chooses quit
```

The loop keeps the app alive.

The list stores all contacts.

Each dictionary stores one contact.

## The Big Idea

A contact is one real-world record.

One contact can be a dictionary:

```python
contact = {
    "name": "Mina",
    "phone": "555-0104",
    "email": "mina@example.com"
}
```

That dictionary has three keys:

```text
name
phone
email
```

You can read one field by key:

```python
print(contact["name"])
print(contact["phone"])
print(contact["email"])
```

You should see:

```text
Mina
555-0104
mina@example.com
```

But a contact book needs more than one contact.

That means the outside container should be a list:

```python
contacts = [
    {"name": "Mina", "phone": "555-0104", "email": "mina@example.com"},
    {"name": "Sam", "phone": "555-0199", "email": "sam@example.com"}
]
```

Read the shape from the outside in:

```text
contacts is a list.
Each item in contacts is a dictionary.
Each dictionary has "name", "phone", and "email".
```

To add a contact, create a new dictionary and append it:

```python
new_contact = {
    "name": "Iris",
    "phone": "555-0130",
    "email": "iris@example.com"
}

contacts.append(new_contact)
```

To show contacts, loop through the list:

```python
for contact in contacts:
    print(contact["name"])
```

To search, loop through the list and compare names:

```python
search_name = "mina"

for contact in contacts:
    if search_name in contact["name"].lower():
        print(contact["name"])
```

That search is friendly because it does not require exact capitalization.

The user can type:

```text
mina
```

and still find:

```text
Mina
```

## The Mental Model

Think of the contact book as a small stack of cards.

One card:

```text
name: Mina
phone: 555-0104
email: mina@example.com
```

Several cards:

```text
contacts

0 -> name: Mina
     phone: 555-0104
     email: mina@example.com

1 -> name: Sam
     phone: 555-0199
     email: sam@example.com
```

The list chooses which card:

```python
contacts[0]
contacts[1]
```

The dictionary chooses which field on that card:

```python
contacts[0]["name"]
contacts[1]["phone"]
```

Inside a loop, Python gives you one card at a time:

```python
for contact in contacts:
    print(contact["name"])
```

During one loop run, `contact` is one dictionary.

That means this works:

```python
contact["name"]
```

This does not:

```python
contacts["name"]
```

`contacts` is the whole list. A list does not have a `"name"` key.

For this project, keep the shape steady:

```text
every contact has "name"
every contact has "phone"
every contact has "email"
```

Consistent keys make the menu actions much easier to write.

## Step-by-Step Build

Build the app in stages.

Do not start with the full program. A contact book has several moving parts, and each part is easier to trust when you test it by itself first.

### Step 1: Create The File

Create this file:

```text
day-55/contact_book.py
```

Code:

```python
print("Contact Book")
print("Store contacts while the program is running.")
```

Run it from your course folder:

```bash
python day-55/contact_book.py
```

If your computer uses `py`, use:

```bash
py day-55/contact_book.py
```

If your computer uses `python3`, use:

```bash
python3 day-55/contact_book.py
```

You should see:

```text
Contact Book
Store contacts while the program is running.
```

The file runs. That is the first checkpoint.

### Step 2: Store One Contact

Start with one dictionary.

Code:

```python
contact = {
    "name": "Mina",
    "phone": "555-0104",
    "email": "mina@example.com"
}

print("Name:", contact["name"])
print("Phone:", contact["phone"])
print("Email:", contact["email"])
```

You should see:

```text
Name: Mina
Phone: 555-0104
Email: mina@example.com
```

This is one contact record.

The dictionary labels each value, so the code is clear:

```text
contact["phone"] means the phone field
contact["email"] means the email field
```

### Step 3: Store Several Contacts

Now put contact dictionaries inside a list.

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
        "phone": "555-0199",
        "email": "sam@example.com"
    }
]

print("Total contacts:", len(contacts))
print("First contact:", contacts[0]["name"])
print("Second contact:", contacts[1]["name"])
```

You should see:

```text
Total contacts: 2
First contact: Mina
Second contact: Sam
```

The list has two items.

Each item is a dictionary.

This line chooses the first dictionary, then reads the `"name"` key:

```python
contacts[0]["name"]
```

Read it slowly:

```text
Go to contacts.
Get item 0.
From that dictionary, get "name".
```

### Step 4: Show All Contacts

A contact book should show every contact.

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
        "phone": "555-0199",
        "email": "sam@example.com"
    }
]

print("Contacts:")

contact_number = 1

for contact in contacts:
    print(str(contact_number) + ".", contact["name"])
    print("   Phone:", contact["phone"])
    print("   Email:", contact["email"])
    contact_number = contact_number + 1

print("Total contacts:", len(contacts))
```

You should see:

```text
Contacts:
1. Mina
   Phone: 555-0104
   Email: mina@example.com
2. Sam
   Phone: 555-0199
   Email: sam@example.com
Total contacts: 2
```

The loop visits one contact dictionary at a time.

The `contact_number` variable starts at `1` because that looks natural to the person using the app.

Python indexes still start at `0`, but display numbers can start at `1`.

### Step 5: Handle An Empty Contact Book

The app starts with no contacts.

If the list is empty, the app should say so.

Code:

```python
contacts = []

if len(contacts) == 0:
    print("No contacts yet.")
else:
    print("Contacts:")

    contact_number = 1

    for contact in contacts:
        print(str(contact_number) + ".", contact["name"])
        print("   Phone:", contact["phone"])
        print("   Email:", contact["email"])
        contact_number = contact_number + 1

    print("Total contacts:", len(contacts))
```

You should see:

```text
No contacts yet.
```

Now change the first line:

```python
contacts = [
    {"name": "Mina", "phone": "555-0104", "email": "mina@example.com"}
]
```

You should see:

```text
Contacts:
1. Mina
   Phone: 555-0104
   Email: mina@example.com
Total contacts: 1
```

This gives the app two display paths:

```text
empty contact book
contact book with records
```

### Step 6: Add One Contact From Input

Now ask the user for contact details.

Code:

```python
contacts = []

name = input("Name: ").strip()
phone = input("Phone: ").strip()
email = input("Email: ").strip()

new_contact = {
    "name": name,
    "phone": phone,
    "email": email
}

contacts.append(new_contact)

print("Contacts:", contacts)
```

Try this:

```text
Mina
555-0104
mina@example.com
```

You should see:

```text
Name: Mina
Phone: 555-0104
Email: mina@example.com
Contacts: [{'name': 'Mina', 'phone': '555-0104', 'email': 'mina@example.com'}]
```

The output is not pretty yet, but the data is correct.

The important pattern is:

```python
new_contact = {
    "name": name,
    "phone": phone,
    "email": email
}

contacts.append(new_contact)
```

The dictionary collects the fields.

The list stores the dictionary.

### Step 7: Reject A Blank Name

A contact without a name is hard to search for later.

Keep phone and email simple today. They can be blank if the user does not know them yet.

But the name should not be blank.

Code:

```python
contacts = []

name = input("Name: ").strip()

if name == "":
    print("No contact added. Name is required.")
else:
    phone = input("Phone: ").strip()
    email = input("Email: ").strip()

    new_contact = {
        "name": name,
        "phone": phone,
        "email": email
    }

    contacts.append(new_contact)
    print("Added contact:", name)

print("Contacts:", contacts)
```

Try this:

```text

```

You should see:

```text
Name:
No contact added. Name is required.
Contacts: []
```

Now run it again and type:

```text
Mina
555-0104
mina@example.com
```

You should see:

```text
Name: Mina
Phone: 555-0104
Email: mina@example.com
Added contact: Mina
Contacts: [{'name': 'Mina', 'phone': '555-0104', 'email': 'mina@example.com'}]
```

The `.strip()` call helps here.

If the user types spaces and presses Enter, the cleaned name becomes an empty string:

```python
name = input("Name: ").strip()
```

### Step 8: Build A Small Menu Loop

Now make the app repeat.

Start with only three choices:

```text
1. View contacts
2. Add contact
3. Quit
```

Code:

```python
contacts = []

print("Contact Book")

while True:
    print("")
    print("Menu:")
    print("1. View contacts")
    print("2. Add contact")
    print("3. Quit")

    choice = input("Choose an option: ").strip()

    if choice == "1":
        if len(contacts) == 0:
            print("No contacts yet.")
        else:
            print("Contacts:")

            contact_number = 1

            for contact in contacts:
                print(str(contact_number) + ".", contact["name"])
                print("   Phone:", contact["phone"])
                print("   Email:", contact["email"])
                contact_number = contact_number + 1

            print("Total contacts:", len(contacts))

    elif choice == "2":
        name = input("Name: ").strip()

        if name == "":
            print("No contact added. Name is required.")
        else:
            phone = input("Phone: ").strip()
            email = input("Email: ").strip()

            new_contact = {
                "name": name,
                "phone": phone,
                "email": email
            }

            contacts.append(new_contact)
            print("Added contact:", name)

    elif choice == "3":
        print("Goodbye.")
        break

    else:
        print("Please choose 1, 2, or 3.")
```

Try a normal run:

```text
2
Mina
555-0104
mina@example.com
1
3
```

The menu should come back after adding the contact.

Choice `3` should stop the loop.

### Step 9: Search By Name

Searching means:

```text
ask for search text
loop through contacts
print matching contacts
remember whether anything matched
```

Code:

```python
contacts = [
    {"name": "Mina", "phone": "555-0104", "email": "mina@example.com"},
    {"name": "Sam", "phone": "555-0199", "email": "sam@example.com"},
    {"name": "Amina", "phone": "555-0188", "email": "amina@example.com"}
]

search_name = input("Search name: ").strip().lower()

found_match = False

for contact in contacts:
    if search_name in contact["name"].lower():
        print("Name:", contact["name"])
        print("Phone:", contact["phone"])
        print("Email:", contact["email"])
        found_match = True

if found_match == False:
    print("No matching contacts.")
```

Try this:

```text
mina
```

You should see:

```text
Search name: mina
Name: Mina
Phone: 555-0104
Email: mina@example.com
Name: Amina
Phone: 555-0188
Email: amina@example.com
```

The search checks whether the search text appears anywhere inside the contact name.

That means `mina` matches both `Mina` and `Amina`.

Try this:

```text
z
```

You should see:

```text
Search name: z
No matching contacts.
```

The `found_match` variable starts as `False`.

When the loop finds a match, it changes to `True`.

After the loop, the program can tell whether nothing matched.

### Step 10: Update A Phone Number

Updating means:

```text
ask which contact to update
find that contact
ask for the new value
replace one dictionary value
```

Code:

```python
contacts = [
    {"name": "Mina", "phone": "555-0104", "email": "mina@example.com"},
    {"name": "Sam", "phone": "555-0199", "email": "sam@example.com"}
]

name_to_update = input("Name to update: ").strip().lower()

found_contact = False

for contact in contacts:
    if contact["name"].lower() == name_to_update:
        print("Current phone:", contact["phone"])
        new_phone = input("New phone: ").strip()
        contact["phone"] = new_phone
        print("Updated phone for", contact["name"])
        found_contact = True

if found_contact == False:
    print("No contact found with that exact name.")

print(contacts)
```

Try this:

```text
mina
555-0000
```

You should see:

```text
Name to update: mina
Current phone: 555-0104
New phone: 555-0000
Updated phone for Mina
[{'name': 'Mina', 'phone': '555-0000', 'email': 'mina@example.com'}, {'name': 'Sam', 'phone': '555-0199', 'email': 'sam@example.com'}]
```

The update line is:

```python
contact["phone"] = new_phone
```

That changes the dictionary already stored inside the list.

For today, updating uses an exact name match.

That keeps the app simple when two contacts have similar names.

### Step 11: Final Working Code

Now combine the pieces.

Code:

```python
contacts = []

print("Contact Book")
print("Store contacts while the program is running.")

while True:
    print("")
    print("Menu:")
    print("1. View contacts")
    print("2. Add contact")
    print("3. Search by name")
    print("4. Update phone number")
    print("5. Quit")

    choice = input("Choose an option: ").strip()

    if choice == "1":
        if len(contacts) == 0:
            print("No contacts yet.")
        else:
            print("Contacts:")

            contact_number = 1

            for contact in contacts:
                print(str(contact_number) + ".", contact["name"])
                print("   Phone:", contact["phone"])
                print("   Email:", contact["email"])
                contact_number = contact_number + 1

            print("Total contacts:", len(contacts))

    elif choice == "2":
        name = input("Name: ").strip()

        if name == "":
            print("No contact added. Name is required.")
        else:
            phone = input("Phone: ").strip()
            email = input("Email: ").strip()

            new_contact = {
                "name": name,
                "phone": phone,
                "email": email
            }

            contacts.append(new_contact)
            print("Added contact:", name)

    elif choice == "3":
        if len(contacts) == 0:
            print("No contacts to search.")
        else:
            search_name = input("Search name: ").strip().lower()

            if search_name == "":
                print("Please type a name to search for.")
            else:
                found_match = False

                for contact in contacts:
                    if search_name in contact["name"].lower():
                        print("Name:", contact["name"])
                        print("Phone:", contact["phone"])
                        print("Email:", contact["email"])
                        found_match = True

                if found_match == False:
                    print("No matching contacts.")

    elif choice == "4":
        if len(contacts) == 0:
            print("No contacts to update.")
        else:
            name_to_update = input("Name to update: ").strip().lower()

            if name_to_update == "":
                print("Please type a name to update.")
            else:
                found_contact = False

                for contact in contacts:
                    if contact["name"].lower() == name_to_update:
                        print("Current phone:", contact["phone"])
                        new_phone = input("New phone: ").strip()
                        contact["phone"] = new_phone
                        print("Updated phone for", contact["name"])
                        found_contact = True

                if found_contact == False:
                    print("No contact found with that exact name.")

    elif choice == "5":
        if len(contacts) == 1:
            print("You saved 1 contact during this run.")
        else:
            print("You saved", len(contacts), "contacts during this run.")

        print("Goodbye.")
        break

    else:
        print("Please choose 1, 2, 3, 4, or 5.")
```

Run the program several times.

Try a normal run:

```text
2
Mina
555-0104
mina@example.com
2
Sam
555-0199
sam@example.com
1
5
```

Try searching:

```text
2
Mina
555-0104
mina@example.com
2
Amina
555-0188
amina@example.com
3
mina
5
```

Try updating:

```text
2
Mina
555-0104
mina@example.com
4
mina
555-0000
1
5
```

Try blank input:

```text
2

5
```

Try a wrong menu choice:

```text
9
5
```

When you test, check more than whether the program crashes.

Also ask:

- Does the menu come back after each normal action?
- Does choice `5` stop the loop?
- Does a blank name stay out of the contact book?
- Does viewing contacts handle an empty list?
- Does searching handle an empty list?
- Does searching find names with different capitalization?
- Does updating change only the phone number?
- Does the closing message match the number of contacts added?

That is how you test a command-line project with confidence.

## Try It Yourself

Make the app your own.

Start with small changes:

- change the welcome message
- change the menu wording
- add a contact field named `"city"`
- add a contact field named `"notes"`
- add a menu choice that shows only names
- add a menu choice that shows the total number of contacts
- make search check phone numbers too
- make update change email instead of phone

If you add a new field, update three places:

```text
where the app asks for input
where the new contact dictionary is created
where contacts are printed
```

Example:

```python
city = input("City: ").strip()
```

Then add the field to the dictionary:

```python
new_contact = {
    "name": name,
    "phone": phone,
    "email": email,
    "city": city
}
```

Then print it:

```python
print("   City:", contact["city"])
```

Those three pieces belong together.

Try this: add two contacts with similar names.

Example:

```text
Mina
Amina
```

Search for:

```text
mina
```

Both names should appear because the search uses:

```python
if search_name in contact["name"].lower():
```

Now update `Mina`.

The update uses an exact match:

```python
if contact["name"].lower() == name_to_update:
```

That means searching can be broad, but updating stays more careful.

## Common Mistake

### Mistake 1: Treating The Contacts List Like One Dictionary

Broken code:

```python
contacts = [
    {"name": "Mina", "phone": "555-0104", "email": "mina@example.com"}
]

print(contacts["name"])
```

This is broken because `contacts` is a list.

Lists use indexes or loops. They do not use dictionary keys directly.

Fixed code:

```python
contacts = [
    {"name": "Mina", "phone": "555-0104", "email": "mina@example.com"}
]

print(contacts[0]["name"])
```

You should see:

```text
Mina
```

When you have many contacts, a loop is usually better:

```python
for contact in contacts:
    print(contact["name"])
```

### Mistake 2: Using Different Keys In Different Contacts

Broken code:

```python
contacts = [
    {"name": "Mina", "phone": "555-0104"},
    {"contact_name": "Sam", "phone": "555-0199"}
]

for contact in contacts:
    print(contact["name"])
```

This code prints the first name, then breaks on the second dictionary.

The first dictionary has `"name"`.

The second dictionary has `"contact_name"`.

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

When a list stores similar records, keep the keys consistent.

### Mistake 3: Comparing A Menu Choice To A Number

Broken code:

```python
choice = input("Choose an option: ")

if choice == 1:
    print("View contacts.")
else:
    print("Unknown choice.")
```

If the user types `1`, the program prints:

```text
Unknown choice.
```

The problem is that `input()` returns text.

This comparison is really:

```text
"1" == 1
```

Those are different values.

Fixed code:

```python
choice = input("Choose an option: ")

if choice == "1":
    print("View contacts.")
else:
    print("Unknown choice.")
```

Compare menu choices with strings unless you have converted the input.

### Mistake 4: Updating A Copy Of The Value Instead Of The Dictionary

Broken code:

```python
contact = {
    "name": "Mina",
    "phone": "555-0104"
}

phone = contact["phone"]
phone = "555-0000"

print(contact["phone"])
```

You should see:

```text
555-0104
```

The contact did not change.

The variable `phone` received a copy of the old phone value. Changing `phone` does not change the dictionary.

Fixed code:

```python
contact = {
    "name": "Mina",
    "phone": "555-0104"
}

contact["phone"] = "555-0000"

print(contact["phone"])
```

You should see:

```text
555-0000
```

To update a dictionary field, assign back into the dictionary key.

## Debug It

Debugging this app usually means checking the data shape and the menu choice.

The examples in this section have bugs. Read the code, find the problem, then compare it with the fix.

### Bug 1: The Search Never Matches

Goal:

```text
Found: Mina
```

Broken code:

```python
contacts = [
    {"name": "Mina", "phone": "555-0104"}
]

search_name = "mina"

for contact in contacts:
    if search_name in contact["name"]:
        print("Found:", contact["name"])
```

Nothing prints.

The problem is capitalization.

The search text is lowercase:

```text
mina
```

The stored name starts with a capital letter:

```text
Mina
```

Fixed code:

```python
contacts = [
    {"name": "Mina", "phone": "555-0104"}
]

search_name = "mina"

for contact in contacts:
    if search_name in contact["name"].lower():
        print("Found:", contact["name"])
```

You should see:

```text
Found: Mina
```

When a search should ignore capitalization, compare lowercase text with lowercase text.

### Bug 2: The Program Says No Match Too Early

Goal:

```text
Found: Sam
```

Broken code:

```python
contacts = [
    {"name": "Mina", "phone": "555-0104"},
    {"name": "Sam", "phone": "555-0199"}
]

search_name = "sam"

for contact in contacts:
    if search_name in contact["name"].lower():
        print("Found:", contact["name"])
    else:
        print("No matching contacts.")
```

You should see:

```text
No matching contacts.
Found: Sam
```

That is confusing. The program says there is no match before it has checked every contact.

Fixed code:

```python
contacts = [
    {"name": "Mina", "phone": "555-0104"},
    {"name": "Sam", "phone": "555-0199"}
]

search_name = "sam"
found_match = False

for contact in contacts:
    if search_name in contact["name"].lower():
        print("Found:", contact["name"])
        found_match = True

if found_match == False:
    print("No matching contacts.")
```

You should see:

```text
Found: Sam
```

Print the no-match message after the loop, when all contacts have been checked.

### Bug 3: The Update Changes Every Matching Name

Broken code:

```python
contacts = [
    {"name": "Mina", "phone": "555-0104"},
    {"name": "mina", "phone": "555-0188"}
]

name_to_update = "mina"

for contact in contacts:
    if contact["name"].lower() == name_to_update:
        contact["phone"] = "555-0000"

print(contacts)
```

You should see:

```text
[{'name': 'Mina', 'phone': '555-0000'}, {'name': 'mina', 'phone': '555-0000'}]
```

Both contacts changed because both names match after `.lower()`.

That may be fine in a tiny practice program, but it can surprise you.

One beginner-safe fix is to stop after the first update.

Fixed code:

```python
contacts = [
    {"name": "Mina", "phone": "555-0104"},
    {"name": "mina", "phone": "555-0188"}
]

name_to_update = "mina"

for contact in contacts:
    if contact["name"].lower() == name_to_update:
        contact["phone"] = "555-0000"
        break

print(contacts)
```

You should see:

```text
[{'name': 'Mina', 'phone': '555-0000'}, {'name': 'mina', 'phone': '555-0188'}]
```

The `break` stops the loop after the first matching contact.

The final project does not use this version because seeing every matching exact name can also be useful while learning.

The important lesson is to ask:

```text
Should this update one record or every matching record?
```

### Bug 4: Quit Prints Goodbye But Keeps Running

Broken code:

```python
while True:
    choice = input("Choose: ").strip()

    if choice == "5":
        print("Goodbye.")
    else:
        print("Still working.")
```

The problem is that the `"5"` branch does not stop the loop.

Fixed code:

```python
while True:
    choice = input("Choose: ").strip()

    if choice == "5":
        print("Goodbye.")
        break
    else:
        print("Still working.")
```

Use `break` when a menu choice should end a `while True` loop.

## Read the Docs

Today, look up Python's official tutorial section about data structures:

```text
https://docs.python.org/3/tutorial/datastructures.html
```

Look for these list ideas:

```python
list.append(x)
len(list)
```

The word `list` in the documentation means "some list."

In your own code, you use your variable name:

```python
contacts.append(new_contact)
len(contacts)
```

Also look up Python's official documentation for dictionaries:

```text
https://docs.python.org/3/library/stdtypes.html#mapping-types-dict
```

Look for the key access shape:

```python
d[key]
```

In your own code, that becomes:

```python
contact["name"]
contact["phone"]
contact["email"]
```

For today, remember:

- `append(x)` adds `x` to the end of a list
- `len(contacts)` counts how many contacts are in the list
- `contact["name"]` reads one value from one contact dictionary
- `contact["phone"] = new_phone` updates one value
- `input()` gives text, so menu choices like `"1"` are strings
- `break` exits the nearest loop

Documentation often shows more than you need right away.

Read it with one practical question:

```text
Which container am I working with right now?
```

## Mini Challenge

Create this file:

```text
day-55/bonus_contact_book.py
```

Build a second version of the app with one extra field:

```text
favorite
```

Keep it simple.

When adding a contact, ask:

```text
Favorite contact? yes/no:
```

Store the answer as text:

```python
"favorite": favorite
```

Then add a menu choice:

```text
Show favorite contacts
```

The new choice should:

- loop through all contacts
- print contacts where `"favorite"` is `"yes"`
- print a helpful message if no favorite contacts exist

Example contact:

```python
new_contact = {
    "name": name,
    "phone": phone,
    "email": email,
    "favorite": favorite
}
```

Example check:

```python
if contact["favorite"] == "yes":
    print(contact["name"])
```

After that works, make the favorite check more forgiving:

```python
favorite = input("Favorite contact? yes/no: ").strip().lower()
```

Now the user can type:

```text
YES
```

and the app stores:

```text
yes
```

## Real-World Use

Contact books are a good practice project because they match real app patterns.

Many programs store records that have the same fields:

```text
contacts
students
products
tasks
books
customers
appointments
```

Each record often becomes a dictionary:

```python
contact = {
    "name": "Mina",
    "phone": "555-0104",
    "email": "mina@example.com"
}
```

Many records often become a list of dictionaries:

```python
contacts = [
    {"name": "Mina", "phone": "555-0104", "email": "mina@example.com"},
    {"name": "Sam", "phone": "555-0199", "email": "sam@example.com"}
]
```

The menu actions are also common:

```text
create a record
show records
search records
update a record
quit
```

Later, these actions can become functions.

Later still, the records can be saved to a file.

Today, keeping everything in memory lets you focus on the data shape and the loop.

## Recap

Today you built a command-line contact book.

You used:

- a list to store many contacts
- dictionaries to store named fields for each contact
- `input()` to collect user choices and contact details
- `.strip()` to clean user input
- `.lower()` to make searching friendlier
- a `while True` loop to keep the app running
- `if`, `elif`, and `else` to handle menu choices
- `append()` to add a contact dictionary to the list
- a `for` loop to view and search contacts
- dictionary assignment to update a phone number
- `break` to quit cleanly

The most important shape was:

```python
contacts = [
    {"name": "Mina", "phone": "555-0104", "email": "mina@example.com"},
    {"name": "Sam", "phone": "555-0199", "email": "sam@example.com"}
]
```

Read it as:

```text
one list
many dictionaries
one dictionary per contact
same keys on each contact
```

That shape is useful far beyond contact books.

## Lesson Checklist

Before moving on, make sure you can:

- create a contact dictionary with `"name"`, `"phone"`, and `"email"`
- create a list of contact dictionaries
- add a new contact dictionary with `append()`
- loop through contacts and print each field
- handle an empty contacts list
- compare menu choices as strings
- search names using `.lower()`
- update a phone number with `contact["phone"] = new_phone`
- use a flag variable like `found_match`
- place the no-match message after the search loop
- use `break` to quit a menu loop
- explain why the app forgets contacts after it closes

## Exercises

### Exercise 1: Add A Starting Contact

Start the final program with one contact already in the list.

Use this:

```python
contacts = [
    {
        "name": "Mina",
        "phone": "555-0104",
        "email": "mina@example.com"
    }
]
```

Run the program and choose:

```text
1
5
```

The contact should appear before you add anything.

### Exercise 2: Add A City Field

Add a `"city"` field to each new contact.

Update the add-contact section:

```python
city = input("City: ").strip()
```

Then store it:

```python
new_contact = {
    "name": name,
    "phone": phone,
    "email": email,
    "city": city
}
```

Then update the view and search output:

```python
print("   City:", contact["city"])
```

Test by adding one contact and viewing the contact list.

### Exercise 3: Search By Email

Add a menu choice named:

```text
Search by email
```

The search should ask for part of an email address:

```python
search_email = input("Search email: ").strip().lower()
```

Then check:

```python
if search_email in contact["email"].lower():
```

Test with:

```text
example
```

and:

```text
mina
```

Both should work if the email contains that text.

### Exercise 4: Update Email Instead Of Phone

Create a menu choice that updates a contact's email address.

Use the phone update section as a guide.

The update line should become:

```python
contact["email"] = new_email
```

Test it by:

- adding one contact
- updating the email
- viewing the contact list
- checking that the phone number did not change

### Exercise 5: Show Only Names

Add a menu choice named:

```text
Show names only
```

It should print:

```text
Mina
Sam
Amina
```

Use this loop shape:

```python
for contact in contacts:
    print(contact["name"])
```

If there are no contacts, print:

```text
No contacts yet.
```

### Exercise 6: Count Matching Search Results

Change the search section so it counts matches.

Start with:

```python
match_count = 0
```

Inside the matching branch, add:

```python
match_count = match_count + 1
```

After the loop, print:

```python
print("Matches found:", match_count)
```

Test with two contacts whose names both contain the same search text.

### Exercise 7: Reject Blank Phone Updates

Change the update section so a blank phone number does not replace the old phone number.

Use this shape:

```python
new_phone = input("New phone: ").strip()

if new_phone == "":
    print("Phone number was not changed.")
else:
    contact["phone"] = new_phone
    print("Updated phone for", contact["name"])
```

Test by pressing Enter at the new phone prompt.

The old phone number should still appear when you view contacts.

### Exercise 8: Explain The Data Shape

Write a short explanation in your own words.

Answer these questions:

```text
What is contacts?
What is one contact?
Why does the program use contact["name"]?
Why does the program loop through contacts before searching?
Why does the app forget contacts after it quits?
```

You do not need perfect wording.

The goal is to check whether the structure makes sense to you.

## Tiny Win

You built a small app that can create, display, search, and update records.

That is a real step up from printing one value or looping through a fixed list.

You now have a program where the user's choices change the data while the program runs.

## Tomorrow

Tomorrow you will start using functions to clean up programs like this.

The final contact book works, but the code has repeated blocks:

```text
showing contacts
adding contacts
searching contacts
updating contacts
printing the menu
```

Functions will let you give those blocks names.

Instead of keeping everything inside one long `while` loop, you will learn how to move related steps into reusable pieces.

That will make projects like the contact book easier to read, test, and extend.
