# Day 89: Methods, Attributes, and Objects

**Focus:** Using object attributes and methods to model changing state  
**You will practice:** reading attributes, writing methods, using `self`, creating multiple objects, updating attributes safely, and adding a simple `__str__` method  
**Estimated time:** 60-75 minutes

## Today's Goal

Yesterday you learned that a class is a blueprint and an object is one thing made from that blueprint.

Today you will make objects do more.

An object can hold data:

```text
item.name
item.quantity
item.price
```

An object can also have actions:

```text
item.sell(3)
item.restock(10)
item.summary()
```

The data pieces are called attributes.

The actions are called methods.

By the end of today, you should be able to:

- explain the difference between an attribute and a method
- write methods that read object attributes
- write methods that update object attributes
- use `self` to mean "this object"
- create several objects from the same class
- keep each object's data separate
- avoid unsafe attribute updates when a method would be clearer
- use `__str__` to control how an object prints
- prepare for Day 90, where you will use objects in a small inventory or password-style project

Today's lesson is still beginner Python.

The goal is not to memorize object-oriented programming words.

The goal is to make the dot feel useful:

```text
object.attribute
object.method()
```

## The Big Idea

An attribute is object data.

A method is an object action.

Here is a small object that has both:

```python
class GameCharacter:
    def __init__(self, name, health):
        self.name = name
        self.health = health

    def status(self):
        return f"{self.name}: {self.health} HP"

    def take_damage(self, amount):
        self.health -= amount


hero = GameCharacter("Mina", 100)

print(hero.status())
hero.take_damage(25)
print(hero.status())
```

You should see:

```text
Mina: 100 HP
Mina: 75 HP
```

This object has two attributes:

```text
name
health
```

This object has two methods:

```text
status()
take_damage()
```

The method `status()` reads the object's data.

The method `take_damage()` changes the object's data.

Both methods use `self`:

```text
self.name
self.health
```

Inside a method, `self` means the object that is currently using the method.

When you call:

```text
hero.status()
```

Python runs `status()` with `hero` as `self`.

When you call:

```text
hero.take_damage(25)
```

Python runs `take_damage()` with:

```text
self   -> hero
amount -> 25
```

You do not pass `self` yourself.

The object before the dot supplies it.

## The Mental Model

Think of an object as a small labeled box.

Inside the box are values:

```text
name: "Mina"
health: 100
```

Those values are attributes.

On the outside of the box are buttons:

```text
status()
take_damage(amount)
```

Those buttons are methods.

When you press a method button, the method can look inside its own box.

That is what `self` gives it access to.

Here is the same idea with two objects:

```python
class Pet:
    def __init__(self, name, animal, energy):
        self.name = name
        self.animal = animal
        self.energy = energy

    def play(self):
        self.energy -= 10
        return f"{self.name} played and now has {self.energy} energy."

    def nap(self):
        self.energy += 15
        return f"{self.name} napped and now has {self.energy} energy."


cat = Pet("Noodle", "cat", 50)
dog = Pet("Scout", "dog", 80)

print(cat.play())
print(dog.nap())
print(cat.energy)
print(dog.energy)
```

You should see:

```text
Noodle played and now has 40 energy.
Scout napped and now has 95 energy.
40
95
```

Both objects came from the same `Pet` class.

But `cat.energy` and `dog.energy` are separate.

Changing one object does not change the other object.

That is one of the main reasons classes are useful.

### Attribute Names Are Nouns

Attributes usually describe what an object knows or stores.

Good attribute names often sound like nouns:

```text
name
quantity
price
username
password
is_active
```

Examples:

```text
item.quantity
account.username
task.is_done
```

### Method Names Are Verbs

Methods usually describe what an object can do.

Good method names often sound like verbs or action phrases:

```text
sell()
restock()
change_password()
mark_done()
summary()
```

Examples:

```text
item.sell(2)
account.change_password("new-pass")
task.mark_done()
```

This is not a strict Python rule.

It is a naming habit that makes code easier to read.

### Methods Can Return Values

A method can answer a question without changing the object.

```python
class InventoryItem:
    def __init__(self, name, quantity):
        self.name = name
        self.quantity = quantity

    def is_low_stock(self):
        return self.quantity < 5


item = InventoryItem("notebook", 3)

print(item.name)
print(item.quantity)
print(item.is_low_stock())
```

You should see:

```text
notebook
3
True
```

The method `is_low_stock()` reads `self.quantity`.

It does not change `self.quantity`.

Methods like this often return `True`, `False`, a number, or a string.

### Methods Can Change Attributes

A method can also update the object's data.

```python
class InventoryItem:
    def __init__(self, name, quantity):
        self.name = name
        self.quantity = quantity

    def restock(self, amount):
        self.quantity += amount


item = InventoryItem("notebook", 3)

print(item.quantity)
item.restock(7)
print(item.quantity)
```

You should see:

```text
3
10
```

This line changes the object:

```text
self.quantity += amount
```

Because `self` is the current object, the update belongs to that one object only.

### Updating Attributes Safely

Python lets you change an attribute directly:

```python
class InventoryItem:
    def __init__(self, name, quantity):
        self.name = name
        self.quantity = quantity


item = InventoryItem("notebook", 3)

item.quantity = -100

print(item.quantity)
```

You should see:

```text
-100
```

That code runs, but the result does not make sense for inventory.

A store cannot have negative notebooks in stock.

For beginner projects, you can protect important updates by using methods.

```python
class InventoryItem:
    def __init__(self, name, quantity):
        self.name = name
        self.quantity = quantity

    def restock(self, amount):
        if amount <= 0:
            return "Restock amount must be positive."

        self.quantity += amount
        return f"Added {amount} {self.name}."

    def sell(self, amount):
        if amount <= 0:
            return "Sale amount must be positive."

        if amount > self.quantity:
            return f"Not enough {self.name} in stock."

        self.quantity -= amount
        return f"Sold {amount} {self.name}."


item = InventoryItem("notebook", 3)

print(item.sell(2))
print(item.quantity)
print(item.sell(5))
print(item.quantity)
print(item.restock(4))
print(item.quantity)
```

You should see:

```text
Sold 2 notebook.
1
Not enough notebook in stock.
1
Added 4 notebook.
5
```

The methods control how `quantity` changes.

That makes the object harder to put into a bad state.

For now, this is enough:

```text
If changing an attribute needs a rule, write a method for that change.
```

## Try It Yourself

Create a folder named:

```text
day-89
```

Inside it, create this file:

```text
day-89/account_practice.py
```

Code:

```python
class BankAccount:
    def __init__(self, owner, balance):
        self.owner = owner
        self.balance = balance

    def describe(self):
        return f"{self.owner}: ${self.balance}"

    def deposit(self, amount):
        if amount <= 0:
            return "Deposit must be positive."

        self.balance += amount
        return f"Deposited ${amount}."

    def withdraw(self, amount):
        if amount <= 0:
            return "Withdrawal must be positive."

        if amount > self.balance:
            return "Not enough money."

        self.balance -= amount
        return f"Withdrew ${amount}."


account = BankAccount("Mina", 100)

print(account.describe())
print(account.deposit(25))
print(account.withdraw(40))
print(account.describe())
print(account.withdraw(500))
print(account.describe())
```

You should see:

```text
Mina: $100
Deposited $25.
Withdrew $40.
Mina: $85
Not enough money.
Mina: $85
```

Notice the method names:

```text
describe()
deposit()
withdraw()
```

Each method belongs to the account.

Each method uses `self.balance` because the balance is stored on that particular account object.

Now add a second account:

```python
class BankAccount:
    def __init__(self, owner, balance):
        self.owner = owner
        self.balance = balance

    def describe(self):
        return f"{self.owner}: ${self.balance}"

    def deposit(self, amount):
        if amount <= 0:
            return "Deposit must be positive."

        self.balance += amount
        return f"Deposited ${amount}."

    def withdraw(self, amount):
        if amount <= 0:
            return "Withdrawal must be positive."

        if amount > self.balance:
            return "Not enough money."

        self.balance -= amount
        return f"Withdrew ${amount}."


mina = BankAccount("Mina", 100)
leo = BankAccount("Leo", 40)

print(mina.withdraw(30))
print(leo.deposit(10))
print(mina.describe())
print(leo.describe())
```

You should see:

```text
Withdrew $30.
Deposited $10.
Mina: $70
Leo: $50
```

The same class made both accounts.

Each object kept its own balance.

## Common Mistake

A common beginner mistake is changing a local name instead of changing the object's attribute.

Here is the mistake:

```text
class Score:
    def __init__(self, points):
        self.points = points

    def add_points(self, amount):
        points = self.points + amount


score = Score(10)
score.add_points(5)
print(score.points)
```

The line:

```text
points = self.points + amount
```

creates a local name called `points`.

It does not change `self.points`.

The object still has the old value.

Fix it by assigning back to the attribute:

```python
class Score:
    def __init__(self, points):
        self.points = points

    def add_points(self, amount):
        self.points = self.points + amount


score = Score(10)
score.add_points(5)
print(score.points)
```

You should see:

```text
15
```

You can also write the update with `+=`:

```python
class Score:
    def __init__(self, points):
        self.points = points

    def add_points(self, amount):
        self.points += amount


score = Score(10)
score.add_points(5)
print(score.points)
```

You should see:

```text
15
```

When a method should change the object, look for `self.attribute_name` on the left side of the assignment:

```text
self.points = ...
self.quantity -= ...
self.balance += ...
```

Another common mistake is forgetting the parentheses when calling a method.

```python
class Task:
    def __init__(self, title):
        self.title = title
        self.is_done = False

    def summary(self):
        return f"{self.title}: done={self.is_done}"


task = Task("Practice classes")

print(task.summary)
print(task.summary())
```

You will see something like:

```text
<bound method Task.summary of <__main__.Task object at 0x...>>
Practice classes: done=False
```

The first print shows the method object itself.

The second print calls the method.

Use parentheses when you want the method to run:

```text
task.summary()
```

## Debug It

Read this code:

```text
class InventoryItem:
    def __init__(self, name, quantity):
        self.name = name
        self.quantity = quantity

    def sell(self, amount):
        quantity -= amount


item = InventoryItem("pencil", 10)
item.sell(3)
print(item.quantity)
```

The method is trying to update `quantity`, but it forgot `self.`.

Inside a method, `quantity` by itself is not the same as `self.quantity`.

One correct version is:

```python
class InventoryItem:
    def __init__(self, name, quantity):
        self.name = name
        self.quantity = quantity

    def sell(self, amount):
        self.quantity -= amount


item = InventoryItem("pencil", 10)
item.sell(3)
print(item.quantity)
```

You should see:

```text
7
```

Now add a safety check:

```python
class InventoryItem:
    def __init__(self, name, quantity):
        self.name = name
        self.quantity = quantity

    def sell(self, amount):
        if amount > self.quantity:
            return "Not enough stock."

        self.quantity -= amount
        return f"Sold {amount}."


item = InventoryItem("pencil", 10)

print(item.sell(3))
print(item.quantity)
print(item.sell(20))
print(item.quantity)
```

You should see:

```text
Sold 3.
7
Not enough stock.
7
```

When you debug object code, ask:

- Is this value stored on the object with `self.`?
- Am I reading the same attribute name I created?
- Does this method need to return a value, update the object, or both?
- Did I accidentally create a local variable instead of updating an attribute?
- Did I call the method with parentheses?

## Read the Docs

Python's documentation uses the words attribute and method often.

For beginner code, read them this way:

```text
attribute
```

A value connected to an object.

```text
method
```

A function connected to an object.

You have already used many methods on built-in Python objects:

```python
message = "hello"
numbers = [3, 1, 2]

print(message.upper())
numbers.append(4)
print(numbers)
```

You should see:

```text
HELLO
[3, 1, 2, 4]
```

`message` is a string object, and string objects have an `upper()` method.

`numbers` is a list object, and list objects have an `append()` method.

Your classes can have methods too:

```text
item.sell(2)
account.withdraw(20)
task.mark_done()
```

### A Light Look At `__str__`

Some method names have double underscores before and after them.

You saw `__init__` yesterday.

Another useful one is:

```text
__str__
```

Python calls `__str__` when it needs a friendly string version of an object.

That includes this:

```text
print(object_name)
```

Here is a small example:

```python
class Task:
    def __init__(self, title):
        self.title = title
        self.is_done = False

    def mark_done(self):
        self.is_done = True

    def __str__(self):
        if self.is_done:
            return f"[x] {self.title}"

        return f"[ ] {self.title}"


task = Task("Practice object methods")

print(task)
task.mark_done()
print(task)
```

You should see:

```text
[ ] Practice object methods
[x] Practice object methods
```

You do not need `__str__` in every class.

It is useful when you want printed objects to look clean.

Without `__str__`, Python prints a technical-looking object description.

With `__str__`, you choose the friendly text.

## Mini Challenge

Create this file:

```text
day-89/password_entry.py
```

Write a `PasswordEntry` class with:

- a `site` attribute
- a `username` attribute
- a `password` attribute
- a `summary()` method that does not reveal the password
- a `change_password()` method
- a `__str__()` method

Starter code:

```python
class PasswordEntry:
    def __init__(self, site, username, password):
        self.site = site
        self.username = username
        self.password = password

    def summary(self):
        return f"{self.site}: {self.username}"

    def change_password(self, new_password):
        if len(new_password) < 8:
            return "Password must be at least 8 characters."

        self.password = new_password
        return "Password updated."

    def __str__(self):
        return self.summary()


entry = PasswordEntry("ExampleMail", "mina", "old-pass-123")

print(entry)
print(entry.change_password("short"))
print(entry.change_password("new-pass-456"))
print(entry.summary())
print(entry.password)
```

You should see:

```text
ExampleMail: mina
Password must be at least 8 characters.
Password updated.
ExampleMail: mina
new-pass-456
```

The `summary()` method hides the password.

The `change_password()` method controls how the password changes.

That same pattern will matter tomorrow when you manage more than one saved item.

## Real-World Use

Objects are useful when your program has several things with the same shape but different data.

An inventory app might have many items:

```text
InventoryItem("notebook", 5)
InventoryItem("pencil", 20)
InventoryItem("marker", 2)
```

Each item has its own quantity.

Each item can use the same methods:

```text
sell()
restock()
is_low_stock()
```

A password manager might have many entries:

```text
PasswordEntry("ExampleMail", "mina", "...")
PasswordEntry("StudySite", "mina42", "...")
PasswordEntry("GameHub", "mstar", "...")
```

Each entry has its own site, username, and password.

Each entry can use the same methods:

```text
summary()
change_password()
__str__()
```

Here is a small inventory example with several objects in a list:

```python
class InventoryItem:
    def __init__(self, name, quantity):
        self.name = name
        self.quantity = quantity

    def is_low_stock(self):
        return self.quantity < 5

    def restock(self, amount):
        self.quantity += amount

    def __str__(self):
        return f"{self.name}: {self.quantity} available"


items = [
    InventoryItem("notebook", 3),
    InventoryItem("pencil", 20),
    InventoryItem("marker", 2),
]

for item in items:
    if item.is_low_stock():
        item.restock(10)

for item in items:
    print(item)
```

You should see:

```text
notebook: 13 available
pencil: 20 available
marker: 12 available
```

This is the bridge to larger object-based programs:

```text
1. Make one class.
2. Create many objects from it.
3. Store the objects in a list.
4. Call methods on each object.
```

Day 90 will use that pattern.

## Recap

An attribute is data stored on an object.

A method is a function that belongs to an object.

Use dot notation to read an attribute:

```text
item.quantity
account.balance
task.title
```

Use dot notation with parentheses to call a method:

```text
item.sell(2)
account.deposit(25)
task.mark_done()
```

Inside a method, `self` means the current object.

If a method needs to read object data, use `self.attribute_name`.

If a method needs to update object data, assign to `self.attribute_name`.

Multiple objects made from the same class keep separate data.

Methods are a good place to put update rules, such as:

```text
Do not sell more items than are in stock.
Do not accept a password that is too short.
Do not withdraw more money than the account has.
```

`__str__` lets you choose how an object looks when printed.

You do not need it every time, but it is handy when objects need clean summaries.

## Lesson Checklist

Before moving on, make sure you can:

- explain that attributes are object data
- explain that methods are object actions
- create an object with attributes in `__init__`
- write a method that reads an attribute
- write a method that updates an attribute
- explain what `self` means
- create two objects from the same class
- show that the two objects keep separate state
- use a method to protect an update with an `if` check
- call methods with parentheses
- recognize the difference between `quantity` and `self.quantity`
- write a simple `__str__` method

## Exercises

### Exercise 1: Reading Attributes

Create this file:

```text
day-89/player_status.py
```

Write a `Player` class with `name`, `level`, and `coins` attributes.

Starter code:

```python
class Player:
    def __init__(self, name, level, coins):
        self.name = name
        self.level = level
        self.coins = coins

    def status(self):
        return f"{self.name} is level {self.level} with {self.coins} coins."


player = Player("Mina", 4, 120)

print(player.status())
```

You should see:

```text
Mina is level 4 with 120 coins.
```

### Exercise 2: Updating One Attribute

Create this file:

```text
day-89/coin_update.py
```

Add an `earn_coins()` method.

Starter code:

```python
class Player:
    def __init__(self, name, coins):
        self.name = name
        self.coins = coins

    def earn_coins(self, amount):
        self.coins += amount

    def status(self):
        return f"{self.name}: {self.coins} coins"


player = Player("Mina", 120)

print(player.status())
player.earn_coins(30)
print(player.status())
```

You should see:

```text
Mina: 120 coins
Mina: 150 coins
```

### Exercise 3: Add A Safety Check

Create this file:

```text
day-89/safe_spending.py
```

Add a method that prevents the player from spending more coins than they have.

Starter code:

```python
class Player:
    def __init__(self, name, coins):
        self.name = name
        self.coins = coins

    def spend_coins(self, amount):
        if amount > self.coins:
            return "Not enough coins."

        self.coins -= amount
        return f"Spent {amount} coins."

    def status(self):
        return f"{self.name}: {self.coins} coins"


player = Player("Mina", 120)

print(player.spend_coins(50))
print(player.status())
print(player.spend_coins(100))
print(player.status())
```

You should see:

```text
Spent 50 coins.
Mina: 70 coins
Not enough coins.
Mina: 70 coins
```

### Exercise 4: Multiple Objects

Create this file:

```text
day-89/two_items.py
```

Make two inventory objects from the same class.

Starter code:

```python
class InventoryItem:
    def __init__(self, name, quantity):
        self.name = name
        self.quantity = quantity

    def sell(self, amount):
        if amount > self.quantity:
            return "Not enough stock."

        self.quantity -= amount
        return f"Sold {amount} {self.name}."

    def summary(self):
        return f"{self.name}: {self.quantity}"


notebook = InventoryItem("notebook", 10)
pencil = InventoryItem("pencil", 3)

print(notebook.sell(4))
print(pencil.sell(1))
print(notebook.summary())
print(pencil.summary())
```

You should see:

```text
Sold 4 notebook.
Sold 1 pencil.
notebook: 6
pencil: 2
```

### Exercise 5: Add `__str__`

Create this file:

```text
day-89/task_string.py
```

Make printed tasks look friendly.

Starter code:

```python
class Task:
    def __init__(self, title):
        self.title = title
        self.is_done = False

    def mark_done(self):
        self.is_done = True

    def __str__(self):
        if self.is_done:
            return f"[x] {self.title}"

        return f"[ ] {self.title}"


task = Task("Review Day 89")

print(task)
task.mark_done()
print(task)
```

You should see:

```text
[ ] Review Day 89
[x] Review Day 89
```

### Exercise 6: Build A Small Password Entry

Create this file:

```text
day-89/password_exercise.py
```

Write a `PasswordEntry` class.

Requirements:

- store `site`, `username`, and `password`
- write `summary()` so it does not print the password
- write `change_password()` so it rejects passwords shorter than 8 characters
- print the entry using `__str__`

One possible solution:

```python
class PasswordEntry:
    def __init__(self, site, username, password):
        self.site = site
        self.username = username
        self.password = password

    def summary(self):
        return f"{self.site}: {self.username}"

    def change_password(self, new_password):
        if len(new_password) < 8:
            return "Password must be at least 8 characters."

        self.password = new_password
        return "Password updated."

    def __str__(self):
        return self.summary()


entry = PasswordEntry("StudySite", "mina42", "learn-python-123")

print(entry)
print(entry.change_password("tiny"))
print(entry.change_password("better-pass-456"))
print(entry)
```

You should see:

```text
StudySite: mina42
Password must be at least 8 characters.
Password updated.
StudySite: mina42
```

## Tiny Win

You can now write objects that do more than hold values.

They can answer questions:

```text
item.is_low_stock()
```

They can protect updates:

```text
account.withdraw(50)
```

They can print cleanly:

```text
print(task)
```

That is a strong step forward.

You are no longer only passing data into separate functions.

You are learning how to place data and the actions that belong to it in the same small, readable object.

## Tomorrow

Tomorrow you will turn this into a small project.

Day 90 will use classes to manage a collection of objects.

You will practice the pattern you saw today:

```text
1. Define a class.
2. Create several objects.
3. Store them in a list.
4. Use methods to update and display them.
```

That is the foundation for an inventory tracker, a tiny password organizer, and many other beginner-friendly apps.
