# Day 88: Introduction to Classes

**Focus:** Creating simple classes and making objects from them  
**You will practice:** class blueprints, objects, instances, `__init__`, `self`, attributes, simple methods, and common beginner mistakes with `self`  
**Estimated time:** 55-70 minutes

## Today's Goal

Today you will learn the first layer of object-oriented programming in Python.

That phrase can sound bigger than it is.

For now, a class is just a way to describe a new kind of thing your program can work with.

So far, you have used values Python already understands:

- strings
- integers
- floats
- booleans
- lists
- dictionaries
- files
- functions

Classes let you create your own kind of value.

By the end of today, you should be able to:

- explain that a class is a blueprint
- explain that an object is something made from a class
- use the word instance as another name for an object made from a class
- write a small class with `class`
- use `__init__` to set up a new object
- explain what `self` means inside a class
- store data on an object with attributes
- write and call one simple method
- recognize common `self` mistakes
- prepare for Day 89, where you will practice methods, attributes, and object behavior more deeply

Classes are not a replacement for functions or dictionaries.

They are another tool for keeping related data and behavior together.

## The Big Idea

A class is a blueprint.

An object is one thing built from that blueprint.

Here is a small `Student` class:

```python
class Student:
    def __init__(self, name, grade):
        self.name = name
        self.grade = grade


student = Student("Mina", 9)

print(student.name)
print(student.grade)
```

You should see:

```text
Mina
9
```

The class is:

```text
Student
```

The object is:

```text
student
```

The object has two attributes:

```text
name
grade
```

An attribute is a value stored on an object.

You get an attribute with dot notation:

```text
student.name
student.grade
```

The dot means:

```text
Look inside this object for this attribute.
```

You have already seen dot notation with modules:

```text
math.sqrt(25)
```

Now you are seeing it with objects:

```text
student.name
```

The idea is similar. The name before the dot tells Python where to look.

## The Mental Model

Think about a paper form.

The blank form says what information belongs together:

```text
Student form
- name
- grade
```

Each filled-out form is a separate student:

```text
Student("Mina", 9)
Student("Leo", 10)
Student("Ava", 8)
```

The class is the blank form.

Each object is one filled-out form.

Here is that idea in Python:

```python
class Student:
    def __init__(self, name, grade):
        self.name = name
        self.grade = grade


mina = Student("Mina", 9)
leo = Student("Leo", 10)

print(mina.name)
print(mina.grade)
print(leo.name)
print(leo.grade)
```

You should see:

```text
Mina
9
Leo
10
```

Both objects were made from the same class.

But each object keeps its own data.

`mina.name` is `"Mina"`.

`leo.name` is `"Leo"`.

They do not overwrite each other because they are two different objects.

### Class Names And Object Names

Python programmers usually write class names with capital letters at the start of each word:

```text
Student
Pet
Book
BankAccount
```

Object names are usually normal variable names:

```text
student
favorite_pet
book
account
```

This is not a new Python rule. It is a reading habit.

When you see:

```text
Student
```

you can guess it is probably a class.

When you see:

```text
student
```

you can guess it is probably one object made from that class.

## `__init__`

The `__init__` method runs when you create a new object.

The name has two underscores before `init` and two underscores after it:

```text
__init__
```

This kind of name is sometimes pronounced "dunder init" because "dunder" means "double underscore".

You do not call `__init__` directly in beginner code.

Python calls it for you when you create an object:

```python
class Book:
    def __init__(self, title, author):
        self.title = title
        self.author = author


book = Book("A Wrinkle in Time", "Madeleine L'Engle")

print(book.title)
print(book.author)
```

You should see:

```text
A Wrinkle in Time
Madeleine L'Engle
```

This line creates a new object:

```text
book = Book("A Wrinkle in Time", "Madeleine L'Engle")
```

Python does the setup like this:

```text
1. Create a new empty Book object.
2. Send that object into __init__ as self.
3. Send "A Wrinkle in Time" into __init__ as title.
4. Send "Madeleine L'Engle" into __init__ as author.
5. Run the code inside __init__.
6. Store the finished object in the variable book.
```

Inside `__init__`, these lines save data onto the object:

```python
class Book:
    def __init__(self, title, author):
        self.title = title
        self.author = author


book = Book("A Wrinkle in Time", "Madeleine L'Engle")

print(book.title)
print(book.author)
```

You should see:

```text
A Wrinkle in Time
Madeleine L'Engle
```

The left side creates or updates the attribute:

```text
self.title
self.author
```

The right side uses the value that was passed in:

```text
title
author
```

That difference matters.

`title` is a temporary parameter inside `__init__`.

`self.title` becomes part of the object.

## `self`

`self` means the current object.

When Python is setting up `mina`, `self` means `mina`.

When Python is setting up `leo`, `self` means `leo`.

That is how one class can create many separate objects.

```python
class Pet:
    def __init__(self, name, animal):
        self.name = name
        self.animal = animal


pet_one = Pet("Noodle", "cat")
pet_two = Pet("Scout", "dog")

print(pet_one.name)
print(pet_one.animal)
print(pet_two.name)
print(pet_two.animal)
```

You should see:

```text
Noodle
cat
Scout
dog
```

The class has one set of instructions.

Each object gets its own attributes.

It helps to read this line:

```text
self.name = name
```

as:

```text
Store the name value on this particular object.
```

Most Python programmers use the name `self`.

Technically, Python only cares that the first parameter is there. But using another name would confuse people reading your code.

Use `self`.

## Attributes

An attribute is data stored on an object.

You create an attribute by assigning to `self.attribute_name` inside the class:

```python
class Pet:
    def __init__(self, name, animal, age):
        self.name = name
        self.animal = animal
        self.age = age


pet = Pet("Noodle", "cat", 3)

print(pet.name)
print(pet.animal)
print(pet.age)
```

You should see:

```text
Noodle
cat
3
```

Attributes are useful when several values belong to the same thing.

Without a class, you might use a dictionary:

```python
pet = {
    "name": "Noodle",
    "animal": "cat",
    "age": 3,
}

print(pet["name"])
print(pet["animal"])
print(pet["age"])
```

You should see:

```text
Noodle
cat
3
```

The dictionary version is still useful.

The class version gives you a named kind of thing:

```text
Pet
```

That named kind of thing becomes more helpful when you add behavior to it.

## Simple Methods

A method is a function that belongs to a class.

Today, keep methods simple.

Here is a `Student` class with one method:

```python
class Student:
    def __init__(self, name, grade):
        self.name = name
        self.grade = grade

    def introduce(self):
        return f"Hi, I am {self.name} and I am in grade {self.grade}."


student = Student("Mina", 9)

print(student.introduce())
```

You should see:

```text
Hi, I am Mina and I am in grade 9.
```

This method:

```text
introduce
```

uses the object's attributes:

```text
self.name
self.grade
```

When you call:

```text
student.introduce()
```

Python automatically sends `student` into the method as `self`.

That is why you do not write:

```text
student.introduce(student)
```

The object before the dot is already the object being used.

Day 89 will spend more time on methods.

For today, the main point is:

```text
A method can read or change the data stored on its own object.
```

## Try It Yourself

Create a folder named:

```text
day-88
```

Inside it, create this file:

```text
day-88/student_practice.py
```

Code:

```python
class Student:
    def __init__(self, name, grade):
        self.name = name
        self.grade = grade

    def label(self):
        return f"{self.name}: grade {self.grade}"


student_one = Student("Mina", 9)
student_two = Student("Leo", 10)

print(student_one.label())
print(student_two.label())
```

You should see:

```text
Mina: grade 9
Leo: grade 10
```

Now add a third student:

```python
class Student:
    def __init__(self, name, grade):
        self.name = name
        self.grade = grade

    def label(self):
        return f"{self.name}: grade {self.grade}"


student_one = Student("Mina", 9)
student_two = Student("Leo", 10)
student_three = Student("Ava", 8)

print(student_one.label())
print(student_two.label())
print(student_three.label())
```

You should see:

```text
Mina: grade 9
Leo: grade 10
Ava: grade 8
```

Notice what changed.

You did not copy the class.

You made another object from the same blueprint.

## Common Mistake

The most common class mistakes are really `self` mistakes.

### Mistake 1: Forgetting `self` In The Method Definition

This code has a problem:

```python
class Student:
    def __init__(name, grade):
        name.name = name
        name.grade = grade


student = Student("Mina", 9)

print(student.name)
```

You will see an error similar to:

```text
TypeError: Student.__init__() takes 2 positional arguments but 3 were given
```

Python automatically passes the new object into `__init__`.

So `__init__` needs a first parameter for that object.

Fix it by writing `self` first:

```python
class Student:
    def __init__(self, name, grade):
        self.name = name
        self.grade = grade


student = Student("Mina", 9)

print(student.name)
```

You should see:

```text
Mina
```

### Mistake 2: Forgetting `self.` When Saving An Attribute

This code runs, but it does not save `name` on the object:

```python
class Student:
    def __init__(self, name, grade):
        name = name
        grade = grade


student = Student("Mina", 9)

print(hasattr(student, "name"))
print(hasattr(student, "grade"))
```

You should see:

```text
False
False
```

The lines:

```text
name = name
grade = grade
```

only create local names inside `__init__`.

They do not attach anything to the object.

Use `self.name` and `self.grade`:

```python
class Student:
    def __init__(self, name, grade):
        self.name = name
        self.grade = grade


student = Student("Mina", 9)

print(hasattr(student, "name"))
print(hasattr(student, "grade"))
```

You should see:

```text
True
True
```

### Mistake 3: Passing `self` Yourself

This code has a problem:

```python
class Student:
    def __init__(self, name, grade):
        self.name = name
        self.grade = grade

    def label(self):
        return f"{self.name}: grade {self.grade}"


student = Student("Mina", 9)

print(student.label(student))
```

You will see an error similar to:

```text
TypeError: Student.label() takes 1 positional argument but 2 were given
```

The object before the dot is automatically passed as `self`.

Call the method like this:

```python
class Student:
    def __init__(self, name, grade):
        self.name = name
        self.grade = grade

    def label(self):
        return f"{self.name}: grade {self.grade}"


student = Student("Mina", 9)

print(student.label())
```

You should see:

```text
Mina: grade 9
```

## Debug It

Read this code:

```python
class Book:
    def __init__(self, title, author):
        title = title
        author = author


book = Book("The Hobbit", "J.R.R. Tolkien")

print(book.title)
```

It raises an error because `title` was never saved on `book`.

The fix is:

```python
class Book:
    def __init__(self, title, author):
        self.title = title
        self.author = author


book = Book("The Hobbit", "J.R.R. Tolkien")

print(book.title)
```

You should see:

```text
The Hobbit
```

When you debug a class, ask:

- Did I write `self` as the first parameter of each instance method?
- Did I use `self.attribute_name` when I wanted to save data on the object?
- Did I call the method through an object, such as `book.title` or `student.label()`?
- Did I accidentally pass `self` myself?
- Did I spell the attribute the same way everywhere?

Attribute spelling errors are common:

```python
class Pet:
    def __init__(self, name):
        self.name = name


pet = Pet("Noodle")

print(pet.name)
```

You should see:

```text
Noodle
```

If you wrote `self.Name` in one place and `pet.name` in another, Python would treat those as different names.

Case matters.

## Read the Docs

Python's official documentation often uses the word object.

You do not need to understand every advanced detail yet.

For now, know these terms:

```text
class
```

A blueprint for making objects.

```text
object
```

One actual value made from a class.

```text
instance
```

Another word for an object made from a particular class.

```text
attribute
```

A value stored on an object.

```text
method
```

A function stored on a class and called through an object.

You will see sentences like:

```text
student is an instance of Student.
```

That means:

```text
student is an object made from the Student class.
```

You may also see:

```text
str is a class.
```

That means strings are objects too:

```python
message = "hello"

print(type(message))
print(message.upper())
```

You should see:

```text
<class 'str'>
HELLO
```

The method call:

```text
message.upper()
```

works because `message` is a string object, and string objects know how to run `upper()`.

That is the same pattern you used with:

```text
student.label()
```

## Mini Challenge

Create this file:

```text
day-88/pet_card.py
```

Write a `Pet` class with:

- an `__init__` method
- a `name` attribute
- an `animal` attribute
- an `age` attribute
- a `summary()` method that returns one sentence

Starter code:

```python
class Pet:
    def __init__(self, name, animal, age):
        self.name = name
        self.animal = animal
        self.age = age

    def summary(self):
        return f"{self.name} is a {self.age}-year-old {self.animal}."


pet = Pet("Noodle", "cat", 3)

print(pet.summary())
```

You should see:

```text
Noodle is a 3-year-old cat.
```

Then create a second `Pet` object and print its summary too.

## Real-World Use

Classes show up when a program keeps working with the same kind of thing.

For example:

- a game might have `Player`, `Enemy`, and `Item` classes
- a school app might have `Student`, `Course`, and `Assignment` classes
- a bookstore app might have `Book`, `Customer`, and `Order` classes
- a drawing app might have `Circle`, `Rectangle`, and `Canvas` classes

You do not need a class for every group of data.

For small scripts, a dictionary can be enough.

Classes become helpful when:

- the same kind of thing appears many times
- each thing needs its own data
- the data and related actions belong together
- the names make the program easier to read

Here is a small example with books:

```python
class Book:
    def __init__(self, title, author, pages):
        self.title = title
        self.author = author
        self.pages = pages

    def description(self):
        return f"{self.title} by {self.author}, {self.pages} pages"


book_one = Book("The Hobbit", "J.R.R. Tolkien", 310)
book_two = Book("Charlotte's Web", "E.B. White", 184)

print(book_one.description())
print(book_two.description())
```

You should see:

```text
The Hobbit by J.R.R. Tolkien, 310 pages
Charlotte's Web by E.B. White, 184 pages
```

The class keeps each book's data and book-related behavior in one place.

## Recap

A class is a blueprint for a new kind of object.

An object is one value made from that class.

An instance is an object made from a particular class.

`__init__` runs when a new object is created.

`self` means the current object.

Attributes are values stored on an object, such as:

```text
student.name
student.grade
```

Methods are functions that belong to objects, such as:

```text
student.label()
```

Today was the first step.

Day 89 will make classes feel more useful by adding more method practice and by showing how objects can change over time.

## Lesson Checklist

Before moving on, make sure you can:

- explain what a class is
- explain what an object is
- explain what an instance is
- create an object from a class
- write an `__init__` method
- use `self` as the first parameter in an instance method
- save data with `self.attribute_name`
- read attributes with dot notation
- write one simple method
- call a method through an object
- explain why you do not pass `self` yourself
- fix a missing `self.` mistake

## Exercises

### Exercise 1: Make A Student

Create this file:

```text
day-88/make_student.py
```

Write a `Student` class with `name` and `grade` attributes.

Starter code:

```python
class Student:
    def __init__(self, name, grade):
        self.name = name
        self.grade = grade


student = Student("Mina", 9)

print(student.name)
print(student.grade)
```

You should see:

```text
Mina
9
```

### Exercise 2: Make Three Objects

Create this file:

```text
day-88/three_students.py
```

Use the same `Student` class, then create three different student objects.

Starter code:

```python
class Student:
    def __init__(self, name, grade):
        self.name = name
        self.grade = grade


student_one = Student("Mina", 9)
student_two = Student("Leo", 10)
student_three = Student("Ava", 8)

print(student_one.name)
print(student_two.name)
print(student_three.name)
```

You should see:

```text
Mina
Leo
Ava
```

### Exercise 3: Add A Simple Method

Create this file:

```text
day-88/student_label.py
```

Add a `label()` method that returns the student's name and grade.

Starter code:

```python
class Student:
    def __init__(self, name, grade):
        self.name = name
        self.grade = grade

    def label(self):
        return f"{self.name}: grade {self.grade}"


student = Student("Mina", 9)

print(student.label())
```

You should see:

```text
Mina: grade 9
```

### Exercise 4: Create A Book Class

Create this file:

```text
day-88/book_practice.py
```

Write a `Book` class with `title`, `author`, and `pages` attributes.

Starter code:

```python
class Book:
    def __init__(self, title, author, pages):
        self.title = title
        self.author = author
        self.pages = pages


book = Book("The Hobbit", "J.R.R. Tolkien", 310)

print(book.title)
print(book.author)
print(book.pages)
```

You should see:

```text
The Hobbit
J.R.R. Tolkien
310
```

### Exercise 5: Fix The Missing Attribute

This code does not save the attributes correctly:

```python
class Pet:
    def __init__(self, name, animal):
        name = name
        animal = animal


pet = Pet("Noodle", "cat")

print(hasattr(pet, "name"))
print(hasattr(pet, "animal"))
```

You should see:

```text
False
False
```

Rewrite the class so `pet.name` and `pet.animal` work.

One correct version is:

```python
class Pet:
    def __init__(self, name, animal):
        self.name = name
        self.animal = animal


pet = Pet("Noodle", "cat")

print(pet.name)
print(pet.animal)
```

You should see:

```text
Noodle
cat
```

### Exercise 6: Explain `self`

In your own words, answer these questions:

- What does `self` mean?
- Why does `__init__` need `self` as its first parameter?
- Why do you write `student.label()` instead of `student.label(student)`?

Keep your answers short. One or two sentences for each question is enough.

## Tiny Win

You can now create your own kind of value in Python.

That is a big step.

Instead of only arranging strings, numbers, lists, dictionaries, and functions, you can give your program a new vocabulary:

```text
Student
Pet
Book
```

Those names make code easier to talk about.

They also prepare you for larger projects where many related pieces of data need to stay organized.

## Tomorrow

Tomorrow you will continue with classes.

Day 89 will focus on methods, attributes, and objects in more detail.

You will practice writing methods that read object data, update object data, and make objects feel more like useful pieces of a program instead of just containers for values.
