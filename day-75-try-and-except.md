# Day 75: Try And Except

**Focus:** Catching errors your program can recover from  
**You will practice:** `try`, `except`, specific exception types, `ValueError`, `FileNotFoundError`, avoiding bare `except`, and using `else` and `finally` in small programs  
**Estimated time:** 45-60 minutes

## Today's Goal

Today you will learn how to keep a program alive when a normal, expected problem happens.

Yesterday, you looked at exceptions: the red error messages Python shows when something goes wrong.

Today you will use those exception names on purpose.

Instead of letting every exception stop the program, you will catch the ones you are ready to handle.

By the end of this lesson, you should be able to:

- wrap risky code in a `try` block
- catch a specific exception with `except ValueError`
- ask for input again after invalid input
- handle a missing file with `except FileNotFoundError`
- avoid bare `except`
- understand why catching every error can hide bugs
- use `else` when the `try` block succeeds
- use `finally` for cleanup messages
- prepare for Day 76, where you will debug problems more deliberately

The main idea:

```text
try says: attempt this code.
except says: if this specific problem happens, do this instead.
```

This does not mean errors are bad.

Errors are information.

`try` and `except` help you decide which errors your program can handle right now.

## The Big Idea

Here is a common beginner program:

```python
age_text = input("Age: ")
age = int(age_text)

print("Next year you will be", age + 1)
```

If the user types a number, it works.

Example run:

```text
Age: 20
Next year you will be 21
```

But if the user types something that cannot be converted to an integer, Python raises a `ValueError`.

Example input:

```text
Age: twenty
```

The problem is this line:

```python
age = int(age_text)
```

The `int()` function knows how to convert `"20"` into `20`.

It does not know how to convert `"twenty"` into a number.

You can handle that with `try` and `except`.

Code:

```python
age_text = input("Age: ")

try:
    age = int(age_text)
    print("Next year you will be", age + 1)
except ValueError:
    print("Please type your age as digits.")
```

Example run:

```text
Age: twenty
Please type your age as digits.
```

The program did not crash.

It noticed a specific problem and gave the user a useful message.

That is the job of `try` and `except`.

## The Mental Model

Think of `try` like saying:

```text
This might fail in a way I understand.
```

Think of `except` like saying:

```text
If that exact failure happens, here is my backup plan.
```

The shape looks like this:

```python
try:
    number = int("42")
except ValueError:
    print("That was not a number.")
```

Only the indented code inside the `try` block is being watched.

Only the exception named after `except` is being caught.

Example:

```python
text = "42"

try:
    number = int(text)
except ValueError:
    print("That was not a number.")

print("Program finished")
```

You should see:

```text
Program finished
```

Nothing went wrong, so the `except` block did not run.

Now change the text:

```python
text = "forty-two"

try:
    number = int(text)
except ValueError:
    print("That was not a number.")

print("Program finished")
```

You should see:

```text
That was not a number.
Program finished
```

The program tried to convert `"forty-two"`.

That raised a `ValueError`.

The matching `except ValueError` block ran.

Then the program continued after the `try` and `except`.

This is important:

```text
try and except should handle expected problems, not hide every possible bug.
```

If you spell a variable name wrong, that is usually a bug to fix.

If a user types `abc` when you asked for a number, that is a normal problem to handle.

## Try It Yourself

Create a folder named:

```text
day-75
```

Then create this file:

```text
day-75/age_check.py
```

Work through the steps one at a time.

### Step 1: Catch Invalid Number Input

Code:

```python
age_text = input("Age: ")

try:
    age = int(age_text)
    print("Next year you will be", age + 1)
except ValueError:
    print("Please type your age as digits.")
```

Run it once with a number:

```text
Age: 20
```

You should see:

```text
Next year you will be 21
```

Run it again with text:

```text
Age: twenty
```

You should see:

```text
Please type your age as digits.
```

The program has one backup plan.

That backup plan only runs when `int(age_text)` raises a `ValueError`.

### Step 2: Ask Again With A Loop

A friendly program often gives the user another chance.

Replace your code with this:

```python
while True:
    age_text = input("Age: ")

    try:
        age = int(age_text)
        break
    except ValueError:
        print("Please type your age as digits.")

print("Next year you will be", age + 1)
```

Example run:

```text
Age: ten
Please type your age as digits.
Age: 10
Next year you will be 11
```

The loop keeps asking.

When conversion works, `break` leaves the loop.

Then the program can safely use `age` as an integer.

### Step 3: Catch A Missing File

Create this file:

```text
day-75/read_settings.py
```

Code:

```python
try:
    with open("day-75/settings.txt") as file:
        theme = file.read().strip()
except FileNotFoundError:
    theme = "light"

print("Theme:", theme)
```

Run it before creating `settings.txt`.

You should see:

```text
Theme: light
```

The file was missing.

The program used a fallback value.

Now create this text file:

```text
day-75/settings.txt
```

Put this inside it:

```text
dark
```

Run the program again.

You should see:

```text
Theme: dark
```

This is a good use of `try` and `except`.

A missing settings file is not always a disaster.

The program can choose a safe default and continue.

### Step 4: Use `else` For The Success Path

You can add `else` after `except`.

The `else` block runs only when the `try` block did not raise an exception.

Code:

```python
score_text = input("Score: ")

try:
    score = int(score_text)
except ValueError:
    print("Scores must be whole numbers.")
else:
    print("Saved score:", score)
```

Example run:

```text
Score: 8
Saved score: 8
```

Another example run:

```text
Score: eight
Scores must be whole numbers.
```

You do not need `else` every time.

But it can make your code clearer:

```text
try: do the risky part
except: handle the problem
else: continue only if the risky part worked
```

### Step 5: Use `finally` Briefly

You can add `finally` after `try` and `except`.

The `finally` block runs whether the `try` block succeeded or failed.

Code:

```python
text = input("Number: ")

try:
    number = int(text)
    print("Double:", number * 2)
except ValueError:
    print("That was not a valid number.")
finally:
    print("Input check finished.")
```

Example run:

```text
Number: 5
Double: 10
Input check finished.
```

Another example run:

```text
Number: five
That was not a valid number.
Input check finished.
```

For now, remember the simple version:

```text
finally always runs.
```

You will not need it in every beginner program.

It is useful when you want a final action to happen either way.

## Common Mistake

The most common mistake is catching too much.

Avoid this pattern:

```python
try:
    age = int(input("Age: "))
    print("Next year:", agee + 1)
except:
    print("Something went wrong.")
```

This is a bare `except`.

It catches almost everything.

That sounds helpful, but it can hide real bugs.

In the code above, the problem is not the user's input.

The problem is this typo:

```python
agee
```

The variable should be:

```python
age
```

If you use a bare `except`, Python may show only:

```text
Something went wrong.
```

That message does not help you find the typo.

Use a specific exception instead:

```python
try:
    age = int(input("Age: "))
    print("Next year:", age + 1)
except ValueError:
    print("Please type your age as digits.")
```

Now the program catches invalid number input.

It does not hide unrelated bugs.

A good beginner rule:

```text
Catch the error you expect.
Let surprising errors show you what to fix.
```

Another common mistake is putting too much code inside the `try` block.

Less helpful:

```python
try:
    name = input("Name: ")
    age = int(input("Age: "))
    message = "Hello, " + name
    print(message)
    print("Next year:", age + 1)
except ValueError:
    print("Please type your age as digits.")
```

Better:

```python
name = input("Name: ")

try:
    age = int(input("Age: "))
except ValueError:
    print("Please type your age as digits.")
else:
    message = "Hello, " + name
    print(message)
    print("Next year:", age + 1)
```

The risky part is the conversion to `int`.

Keep the `try` block close to the line that might raise the error you plan to catch.

## Debug It

This program is supposed to ask for a price and print the price with tax.

Broken code:

```python
price_text = input("Price: ")

try:
    price = int(price_text)
except ValueError:
    print("Please type a whole number.")

tax = price * 0.1
print("Tax:", tax)
```

The problem appears when the user types invalid input.

Example run:

```text
Price: free
Please type a whole number.
```

After that, the program tries to use `price`.

But `price` was never created, because `int(price_text)` failed.

That can lead to another error.

Fixed code:

```python
price_text = input("Price: ")

try:
    price = int(price_text)
except ValueError:
    print("Please type a whole number.")
else:
    tax = price * 0.1
    print("Tax:", tax)
```

Now the tax calculation happens only if the conversion worked.

Here is another broken program.

It is supposed to load a note from a file, or use a fallback note if the file is missing.

Broken code:

```python
try:
    with open("day-75/note.txt") as file:
        note = file.read().strip()
except ValueError:
    note = "No note yet."

print(note)
```

The problem is that a missing file does not raise `ValueError`.

It raises `FileNotFoundError`.

Fixed code:

```python
try:
    with open("day-75/note.txt") as file:
        note = file.read().strip()
except FileNotFoundError:
    note = "No note yet."

print(note)
```

When you debug `try` and `except`, ask these questions:

- Which line is likely to fail?
- What exception type does that line raise?
- Am I catching that exact exception?
- Did I put too much code inside the `try` block?
- After the `except` block runs, does the rest of the program still make sense?

Tomorrow you will turn questions like these into a fuller debugging strategy.

## Read the Docs

Python's official tutorial explains errors and exceptions here:

[Python docs: Errors and Exceptions](https://docs.python.org/3/tutorial/errors.html)

Today, focus on these terms:

- `try`
- `except`
- `else`
- `finally`
- exception type names such as `ValueError` and `FileNotFoundError`

Python also lists built-in exception types here:

[Python docs: Built-in Exceptions](https://docs.python.org/3/library/exceptions.html)

Do not try to memorize the full list.

Instead, practice recognizing exception names when Python shows them.

Try this:

```text
Find ValueError in the built-in exceptions page.
Find FileNotFoundError in the built-in exceptions page.
Write one sentence for each in your own words.
```

Documentation is easier to read when you are looking for one small thing.

## Mini Challenge

Build a small points checker.

Create:

```text
day-75/points_checker.py
```

The program should:

- ask the user for points
- convert the input to an integer
- print a message if the points are 100 or more
- print a different message if the points are under 100
- catch invalid number input with `ValueError`

Starter code:

```python
points_text = input("Points: ")

try:
    points = int(points_text)
except ValueError:
    print("Please type points as a whole number.")
else:
    if points >= 100:
        print("Bonus unlocked")
    else:
        print("Keep going")
```

Example run:

```text
Points: 120
Bonus unlocked
```

Another example run:

```text
Points: many
Please type points as a whole number.
```

After it works, change the program so it asks again until the user types a valid number.

## Real-World Use

`try` and `except` show up in real programs whenever something outside your control might go wrong.

Examples:

- a user types text when the program needs a number
- a settings file has not been created yet
- a saved game file is missing
- a report file cannot be opened
- a piece of text cannot be converted into the format you expected

Here is a small example that reads a saved high score.

If the file is missing, it starts from zero.

Code:

```python
try:
    with open("day-75/high_score.txt") as file:
        high_score = int(file.read())
except FileNotFoundError:
    high_score = 0
except ValueError:
    high_score = 0

print("High score:", high_score)
```

This program handles two expected problems:

```text
The file might not exist yet.
The file might not contain a valid number.
```

You can also combine those exceptions when the backup plan is the same:

```python
try:
    with open("day-75/high_score.txt") as file:
        high_score = int(file.read())
except (FileNotFoundError, ValueError):
    high_score = 0

print("High score:", high_score)
```

Both versions are fine.

The important part is that the program names the errors it expects.

It does not catch every possible error and pretend everything is okay.

## Recap

Today you learned how to catch specific errors with `try` and `except`.

You used this pattern:

```python
try:
    number = int("12")
except ValueError:
    print("That was not a number.")
```

You handled invalid user input:

```python
try:
    age = int(input("Age: "))
except ValueError:
    print("Please type your age as digits.")
else:
    print("Next year:", age + 1)
```

You handled a missing file:

```python
try:
    with open("day-75/settings.txt") as file:
        theme = file.read().strip()
except FileNotFoundError:
    theme = "light"

print("Theme:", theme)
```

You learned that:

- `try` contains code that might fail
- `except ValueError` catches a number conversion problem
- `except FileNotFoundError` catches a missing file problem
- specific exceptions are safer than bare `except`
- `else` runs when the `try` block succeeds
- `finally` runs whether the `try` block succeeds or fails
- catching errors should not hide bugs you need to fix

The biggest habit:

```text
Catch expected problems by name.
```

## Lesson Checklist

- [ ] I can write a `try` and `except` block.
- [ ] I can explain what the `try` block does.
- [ ] I can explain what the `except` block does.
- [ ] I can catch `ValueError` when converting input.
- [ ] I can catch `FileNotFoundError` when opening a file.
- [ ] I can avoid bare `except`.
- [ ] I can explain why catching every error can hide bugs.
- [ ] I can use `else` after `except`.
- [ ] I can explain that `finally` always runs.
- [ ] I can choose a simple fallback when a file is missing.

## Exercises

### Exercise 1: Convert A Number Safely

Create:

```text
day-75/safe_number.py
```

Ask the user for a number.

If the input is valid, print double the number.

If it is not valid, print:

```text
Please type a whole number.
```

Use `except ValueError`.

### Exercise 2: Ask Until It Works

Create:

```text
day-75/ask_until_number.py
```

Ask the user for a whole number until they type one correctly.

Then print:

```text
Accepted: number
```

Replace `number` with the number they typed.

### Exercise 3: File Fallback

Create:

```text
day-75/load_username.py
```

Try to read:

```text
day-75/username.txt
```

If the file exists, print:

```text
Hello, name
```

If the file is missing, print:

```text
Hello, guest
```

Use `except FileNotFoundError`.

### Exercise 4: Fix The Bare Except

This code catches too much:

```python
try:
    total = int(input("Total: "))
    print("Half:", totl / 2)
except:
    print("Could not calculate.")
```

Fix it so invalid input is handled with `except ValueError`, but the typo is not hidden.

Then fix the typo too.

### Exercise 5: Use `else`

Create:

```text
day-75/divide_by_two.py
```

Ask the user for a whole number.

Use `try` and `except ValueError` for the conversion.

Use `else` to print half the number only when conversion works.

### Exercise 6: Add A Fallback Score

Create:

```text
day-75/load_score.py
```

Try to read a number from:

```text
day-75/score.txt
```

If the file is missing, use `0`.

If the file contains text that is not a number, use `0`.

Print:

```text
Score: 0
```

or the score from the file.

### Exercise 7: Keep The Try Block Small

Rewrite this code so only the conversion is inside the `try` block:

```python
name = input("Name: ")

try:
    age = int(input("Age: "))
    print("Name:", name)
    print("Age next year:", age + 1)
except ValueError:
    print("Please type your age as digits.")
```

Use `else` for the lines that should run only after a successful conversion.

### Exercise 8: Name The Exception

For each situation, write the exception you would expect to catch.

Choose from:

```text
ValueError
FileNotFoundError
```

Situations:

```text
The user types "ten" and the program runs int("ten").
The program tries to open a missing settings file.
The program reads "abc" from a score file and runs int("abc").
The program tries to open a missing username file.
```

### Exercise 9: Improve The Message

Start with this code:

```python
try:
    minutes = int(input("Minutes practiced: "))
except ValueError:
    print("Bad input.")
else:
    print("Nice work practicing for", minutes, "minutes.")
```

Change the error message so it tells the user exactly what to do.

### Exercise 10: Explain The Flow

Read this code:

```python
text = "hello"

try:
    number = int(text)
except ValueError:
    print("Could not convert text.")
else:
    print("Number:", number)
finally:
    print("Done checking.")
```

Write down:

```text
Which line raises the error?
Which block runs because of that error?
Does the else block run?
Does the finally block run?
What gets printed?
```

Then run the code and compare your answers.

## Tiny Win

You can now write programs that handle normal user mistakes without falling over.

That is a practical skill.

You are not ignoring errors.

You are listening to them, naming them, and choosing a clear next step.

## Tomorrow

Tomorrow is:

```text
Day 76: Debugging Strategy
```

Today you learned how to catch expected problems.

Tomorrow you will look at a bigger debugging process:

```text
read the error
find the line
check your assumptions
make one small change
run the program again
```

`try` and `except` are one tool.

Debugging is the broader habit of understanding what your program is really doing.
