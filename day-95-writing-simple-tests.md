# Day 95: Writing Simple Tests

**Focus:** Checking small pieces of Python code automatically  
**You will practice:** testable functions, expected behavior, `assert`, passing tests, failing tests, edge cases, testing errors, naming tests clearly, running test files, and a light introduction to `unittest`  
**Estimated time:** 60-75 minutes

## Today's Goal

Today you will learn how to write simple tests for Python functions.

A test is a small check that asks:

```text
Does this code still behave the way I expect?
```

You have already tested programs many times by running them and looking at the output.

That is useful, but it has limits.

If a project has ten functions, checking all of them by hand after every change gets tiring. You may check the new feature and accidentally miss that an older feature broke.

Tests help with that.

By the end of today, you should be able to:

- explain what a test checks
- describe expected behavior before writing a test
- write simple tests with `assert`
- run a test file from the command line
- recognize the difference between a passing test and a failing test
- read a basic `AssertionError`
- test normal cases and edge cases
- test that a function raises an error
- explain why functions with `return` values are easier to test
- separate logic from `input()` and `print()`
- recognize the basic shape of a `unittest` test file
- prepare for Day 96, where tests will help you refactor code more safely

This lesson is not about memorizing a testing framework.

It is about making testing feel like a normal part of writing code.

## The Big Idea

A test is code that checks other code.

Here is a tiny function:

```python
def add(left, right):
    return left + right
```

Here is a tiny test:

```python
assert add(2, 3) == 5
```

Read that line as:

```text
I expect add(2, 3) to give back 5.
```

If the claim is true, Python keeps going.

If the claim is false, Python stops and shows an `AssertionError`.

That is the heart of beginner testing:

```text
Call a function.
Compare the result with the value you expect.
Let Python complain if the result is wrong.
```

Tests are useful because they turn your expectations into code.

Instead of thinking:

```text
I hope this still works.
```

you can run a file that checks:

```text
This still adds numbers.
This still handles zero.
This still formats prices.
This still raises an error for impossible input.
```

That changes how it feels to edit a project.

## The Mental Model

Most simple tests have three parts.

```text
arrange
  prepare the values

act
  call the function

assert
  check the result
```

For a small function, those three parts may fit on one line:

```python
assert add(2, 3) == 5
```

If you stretch it out, the shape is easier to see:

```python
left = 2
right = 3

result = add(left, right)

assert result == 5
```

The test says:

```text
Given 2 and 3,
when I add them,
then the result should be 5.
```

Tests are not magic.

They do not prove that your whole program is perfect.

They check specific examples.

Good tests choose examples that matter:

- ordinary values
- empty values
- boundary values
- invalid values
- values that caused bugs before

Each test is a small guardrail.

One guardrail is not enough for a whole road, but several well-placed guardrails help a lot.

## Start With A Testable Function

Some code is easy to test.

Some code is awkward to test.

This function is awkward:

```python
def add_numbers_from_user():
    left = float(input("Left number: "))
    right = float(input("Right number: "))
    print(left + right)
```

It does three jobs:

- asks the user for input
- adds numbers
- prints the result

That is fine for a tiny script, but it is hard to test automatically because the function waits for keyboard input and prints instead of returning a value.

This version is easier to test:

```python
def add(left, right):
    return left + right
```

Now the rule is separate:

```text
adding two numbers
```

The user conversation can live somewhere else:

```python
left = float(input("Left number: "))
right = float(input("Right number: "))

print(add(left, right))
```

This is the same habit you practiced when organizing projects:

```text
logic code
  functions that make decisions and return values

interface code
  input, print, command-line arguments, menus, files
```

Tests are usually easiest when they start with the logic code.

## A First Test With `assert`

Create this file:

```text
day-95/calculator.py
```

Add:

```python
def add(left, right):
    return left + right


def subtract(left, right):
    return left - right


def divide(left, right):
    if right == 0:
        raise ValueError("cannot divide by zero")

    return left / right


def format_price(amount):
    return f"${amount:.2f}"
```

This file contains only functions.

It does not ask for input.

It does not print.

That makes it a good first file to test.

Now create:

```text
day-95/test_calculator.py
```

Add:

```python
from calculator import add, divide, format_price, subtract


def test_add_numbers():
    assert add(2, 3) == 5
    assert add(-2, 5) == 3


def test_subtract_numbers():
    assert subtract(10, 4) == 6
    assert subtract(4, 10) == -6


def test_divide_numbers():
    assert divide(10, 2) == 5
    assert divide(7, 2) == 3.5


def test_format_price():
    assert format_price(3) == "$3.00"
    assert format_price(3.5) == "$3.50"


test_add_numbers()
test_subtract_numbers()
test_divide_numbers()
test_format_price()

print("All simple tests passed.")
```

Run:

```text
python day-95/test_calculator.py
```

A successful run prints:

```text
All simple tests passed.
```

That one line is a good sign.

It means Python reached the end of the file without any assertion failing.

## What `assert` Does

An `assert` statement checks whether something is true.

This passes:

```python
assert 2 + 3 == 5
```

This fails:

```python
assert 2 + 3 == 6
```

When an assertion fails, Python raises:

```text
AssertionError
```

That error is useful.

It tells you:

```text
One of my expectations was wrong.
```

The expectation might be wrong because the code has a bug.

It might also be wrong because the test expected the wrong thing.

Both cases happen.

When a test fails, do not immediately assume the function is bad.

Ask:

- What did the test expect?
- What did the function actually return?
- Is the expectation correct?
- Did I call the function with the right values?
- Did a recent change alter the behavior on purpose?

Testing is not about blaming the code.

It is about getting a clear signal.

## A Failing Test

To see a failure, temporarily change this line in `day-95/test_calculator.py`:

```python
assert add(2, 3) == 5
```

to:

```python
assert add(2, 3) == 6
```

Run:

```text
python day-95/test_calculator.py
```

You should see an `AssertionError`.

The message will include a file name and a line number near the failed assertion.

That line number matters.

It points you to the exact expectation that failed.

After you see the failure, change the line back:

```python
assert add(2, 3) == 5
```

Run the test file again.

It should pass.

This is a useful beginner exercise because it teaches the full test loop:

```text
write an expectation
run the test
see it pass
make it fail on purpose
read the failure
fix it
run it again
```

If you have only seen passing tests, you have only learned half the tool.

Failing tests teach you what the warning light looks like.

## Test Names Should Say The Behavior

These function names are useful:

```python
def test_add_numbers():
    ...


def test_format_price():
    ...
```

They tell you what behavior the test is checking.

Weak test names are vague:

```python
def test_one():
    ...


def test_stuff():
    ...
```

Clear names help when something fails.

If Python shows:

```text
test_format_price
```

you already know the failure is probably connected to price formatting.

For beginner tests, use names shaped like:

```text
test_add_numbers
test_empty_list_total
test_divide_by_zero
test_format_price_with_cents
test_find_missing_contact
```

The name does not need to be clever.

It needs to be searchable and specific.

## Testing Edge Cases

An edge case is a value near the edge of what the function should handle.

For `add()`, ordinary values might be:

```python
assert add(2, 3) == 5
```

Edge cases might include:

```python
assert add(0, 0) == 0
assert add(-2, 5) == 3
```

For `format_price()`, ordinary values might be:

```python
assert format_price(3.5) == "$3.50"
```

Edge cases might include:

```python
assert format_price(0) == "$0.00"
assert format_price(1.999) == "$2.00"
```

For a function that works with a list, edge cases often include:

```text
empty list
one item
repeated items
very small number
very large number
missing value
```

You do not need to test every possible input.

That would be impossible.

Instead, choose examples that represent important situations.

For a beginner project, a good starting mix is:

```text
one normal case
one edge case
one invalid case if the function rejects bad input
```

## Testing Errors With Plain Python

Some functions should raise an error for invalid input.

In `day-95/calculator.py`, `divide()` raises `ValueError` when the right number is zero:

```python
def divide(left, right):
    if right == 0:
        raise ValueError("cannot divide by zero")

    return left / right
```

You can test that with plain Python.

Add this function to `day-95/test_calculator.py`:

```python
def test_divide_by_zero():
    try:
        divide(10, 0)
    except ValueError:
        pass
    else:
        raise AssertionError("divide(10, 0) should raise ValueError")
```

Then add this call near the bottom:

```python
test_divide_by_zero()
```

The full bottom of the file should now look like this:

```python
test_add_numbers()
test_subtract_numbers()
test_divide_numbers()
test_format_price()
test_divide_by_zero()

print("All simple tests passed.")
```

Run:

```text
python day-95/test_calculator.py
```

The file should still pass.

The test means:

```text
Try to divide by zero.
If ValueError happens, good.
If no ValueError happens, fail the test.
```

That may look a little longer than a simple `assert`, but the idea is the same:

```text
Describe the behavior you expect.
Make Python complain if something else happens.
```

## Why `return` Values Help

Tests usually want to compare a result.

That is easier when a function returns a value.

Easy to test:

```python
def calculate_total(prices):
    total = 0

    for price in prices:
        total += price

    return total
```

Test:

```python
assert calculate_total([4, 5, 6]) == 15
assert calculate_total([]) == 0
```

Harder to test:

```python
def print_total(prices):
    total = 0

    for price in prices:
        total += price

    print(f"Total: {total}")
```

The second function prints the answer but does not return it.

Printing is not bad.

A command-line program needs to show information.

But if you mix all the logic into printing functions, tests become harder to write.

A cleaner split is:

```python
def calculate_total(prices):
    total = 0

    for price in prices:
        total += price

    return total


def print_total(prices):
    total = calculate_total(prices)
    print(f"Total: {total}")
```

Now you can test `calculate_total()` directly.

The printing function can stay small.

## Passing Tests Do Not Mean Perfect Code

Passing tests are useful, but they do not mean:

```text
This program has no bugs.
```

They mean:

```text
The checked examples behaved as expected.
```

That difference matters.

Suppose you test:

```python
assert add(2, 3) == 5
```

That does not check every number in the universe.

It checks one example.

If you also test:

```python
assert add(-2, 5) == 3
assert add(0, 0) == 0
```

you now have better coverage of the behavior.

Coverage means:

```text
how much of the behavior your tests check
```

You do not need to chase perfect coverage in this course.

The beginner goal is simpler:

```text
Write tests for the behavior you would be nervous to break.
```

## Running Tests

For plain `assert` tests, run the test file like any other Python file:

```text
python day-95/test_calculator.py
```

If all assertions pass, the script reaches the end.

If one assertion fails, Python stops at the first failure.

That is enough for small practice projects.

As projects grow, many Python teams use test tools that collect and run many tests.

Today you will only take a light look at the standard library tool named `unittest`.

Before that, remember the main habit:

```text
Keep test files separate from the code they test.
```

This shape is common:

```text
day-95/
  calculator.py
  test_calculator.py
```

The code lives in:

```text
day-95/calculator.py
```

The tests live in:

```text
day-95/test_calculator.py
```

The `test_` prefix is a common naming habit.

It tells people:

```text
This file checks code. It is not the main program.
```

## A Light Look At `unittest`

Python includes a testing module named `unittest`.

It gives you a more organized way to group tests.

You do not need it for the simplest examples, but you should recognize the shape.

Create:

```text
day-95/test_calculator_unittest.py
```

Add:

```python
import unittest

from calculator import add, divide, format_price, subtract


class CalculatorTests(unittest.TestCase):
    def test_add_numbers(self):
        self.assertEqual(add(2, 3), 5)
        self.assertEqual(add(-2, 5), 3)

    def test_subtract_numbers(self):
        self.assertEqual(subtract(10, 4), 6)
        self.assertEqual(subtract(4, 10), -6)

    def test_divide_numbers(self):
        self.assertEqual(divide(10, 2), 5)
        self.assertEqual(divide(7, 2), 3.5)

    def test_divide_by_zero(self):
        with self.assertRaises(ValueError):
            divide(10, 0)

    def test_format_price(self):
        self.assertEqual(format_price(3), "$3.00")
        self.assertEqual(format_price(3.5), "$3.50")


if __name__ == "__main__":
    unittest.main()
```

Run it directly:

```text
python day-95/test_calculator_unittest.py
```

A successful run will look similar to:

```text
.....
----------------------------------------------------------------------
Ran 5 tests in 0.001s

OK
```

The dots represent passing test methods.

You can also ask `unittest` to discover that file:

```text
python -m unittest discover -s day-95 -p "test_calculator_unittest.py"
```

Read that command as:

```text
Use unittest.
Search inside day-95.
Run files matching test_calculator_unittest.py.
```

For now, the direct command is easier.

The discover command becomes more useful when a project has several test files.

## `assert` And `unittest`

Both styles check behavior.

Plain `assert` is small:

```python
assert add(2, 3) == 5
```

`unittest` is more structured:

```python
self.assertEqual(add(2, 3), 5)
```

Plain `assert` is a good first tool because it reads almost like a sentence.

`unittest` is useful because it can:

- find test methods
- run many tests
- show a summary
- provide helpers like `assertEqual`
- provide `assertRaises` for errors
- group related tests in a class

You do not have to choose one forever.

Today, prefer plain `assert` when you are checking small functions.

Use `unittest` enough to recognize it when you see it.

## Try It Yourself

Build the small calculator test project in steps.

### Step 1: Create The Folder

Create:

```text
day-95/
```

Inside it, you will create:

```text
day-95/calculator.py
day-95/test_calculator.py
day-95/test_calculator_unittest.py
```

### Step 2: Add The Calculator Functions

Put this in `day-95/calculator.py`:

```python
def add(left, right):
    return left + right


def subtract(left, right):
    return left - right


def divide(left, right):
    if right == 0:
        raise ValueError("cannot divide by zero")

    return left / right


def format_price(amount):
    return f"${amount:.2f}"
```

### Step 3: Add Plain `assert` Tests

Put this in `day-95/test_calculator.py`:

```python
from calculator import add, divide, format_price, subtract


def test_add_numbers():
    assert add(2, 3) == 5
    assert add(-2, 5) == 3


def test_subtract_numbers():
    assert subtract(10, 4) == 6
    assert subtract(4, 10) == -6


def test_divide_numbers():
    assert divide(10, 2) == 5
    assert divide(7, 2) == 3.5


def test_divide_by_zero():
    try:
        divide(10, 0)
    except ValueError:
        pass
    else:
        raise AssertionError("divide(10, 0) should raise ValueError")


def test_format_price():
    assert format_price(3) == "$3.00"
    assert format_price(3.5) == "$3.50"


test_add_numbers()
test_subtract_numbers()
test_divide_numbers()
test_divide_by_zero()
test_format_price()

print("All simple tests passed.")
```

Run:

```text
python day-95/test_calculator.py
```

You should see:

```text
All simple tests passed.
```

### Step 4: Make One Test Fail

Change:

```python
assert format_price(3) == "$3.00"
```

to:

```python
assert format_price(3) == "$3"
```

Run the test file again.

You should see an `AssertionError`.

Read the file name and line number.

Then change the assertion back:

```python
assert format_price(3) == "$3.00"
```

Run the file again and confirm that it passes.

### Step 5: Add One More Edge Case

Add this assertion inside `test_format_price()`:

```python
assert format_price(0) == "$0.00"
```

Run:

```text
python day-95/test_calculator.py
```

The test should still pass.

### Step 6: Add The `unittest` Version

Put this in `day-95/test_calculator_unittest.py`:

```python
import unittest

from calculator import add, divide, format_price, subtract


class CalculatorTests(unittest.TestCase):
    def test_add_numbers(self):
        self.assertEqual(add(2, 3), 5)
        self.assertEqual(add(-2, 5), 3)

    def test_subtract_numbers(self):
        self.assertEqual(subtract(10, 4), 6)
        self.assertEqual(subtract(4, 10), -6)

    def test_divide_numbers(self):
        self.assertEqual(divide(10, 2), 5)
        self.assertEqual(divide(7, 2), 3.5)

    def test_divide_by_zero(self):
        with self.assertRaises(ValueError):
            divide(10, 0)

    def test_format_price(self):
        self.assertEqual(format_price(3), "$3.00")
        self.assertEqual(format_price(3.5), "$3.50")
        self.assertEqual(format_price(0), "$0.00")


if __name__ == "__main__":
    unittest.main()
```

Run:

```text
python day-95/test_calculator_unittest.py
```

Then try:

```text
python -m unittest discover -s day-95 -p "test_calculator_unittest.py"
```

Both commands should run the `unittest` tests.

## Common Mistake

The most common testing mistake is writing tests for code that is still tangled with input and printing.

Problem:

```python
def get_discounted_price():
    price = float(input("Price: "))
    discount = float(input("Discount: "))
    final_price = price - discount
    print(final_price)
```

That function can be used by a person, but it is awkward for a test.

Better:

```python
def get_discounted_price(price, discount):
    return price - discount
```

Now you can test the rule:

```python
assert get_discounted_price(20, 5) == 15
assert get_discounted_price(20, 0) == 20
```

The program can still ask the user for values:

```python
price = float(input("Price: "))
discount = float(input("Discount: "))

print(get_discounted_price(price, discount))
```

The split makes both parts easier to understand.

### Mistake 1: Testing The Wrong Thing

This test checks that Python can add numbers:

```python
assert 2 + 3 == 5
```

That is fine when learning `assert`, but it does not check your program.

Prefer:

```python
assert add(2, 3) == 5
```

Now the test checks your function.

### Mistake 2: Writing A Test Without A Clear Expectation

Weak:

```python
result = format_price(3)
assert result
```

That only checks whether `result` is truthy.

It does not check the actual format.

Better:

```python
assert format_price(3) == "$3.00"
```

The better test states the exact behavior.

### Mistake 3: Forgetting To Run The Test File

Writing a test file does not help unless you run it.

After changing code, run:

```text
python day-95/test_calculator.py
```

For a `unittest` file, run:

```text
python day-95/test_calculator_unittest.py
```

Testing is a habit, not just a file.

### Mistake 4: Ignoring A Failing Test

If a test fails, do not delete the test just to make the project look clean.

First decide:

```text
Is the code wrong?
Is the test wrong?
Did the expected behavior change on purpose?
```

If the expected behavior changed, update the test carefully.

If the code is wrong, fix the code.

The failing test is doing its job.

### Mistake 5: Testing Too Much At Once

This test is hard to diagnose:

```python
def test_everything():
    assert add(2, 3) == 5
    assert subtract(10, 4) == 6
    assert divide(10, 2) == 5
    assert format_price(3) == "$3.00"
```

If it fails, you have to inspect the line to know which behavior broke.

This is clearer:

```python
def test_add_numbers():
    assert add(2, 3) == 5


def test_subtract_numbers():
    assert subtract(10, 4) == 6
```

Small tests are easier to read.

## Debug It

Use these situations to practice reading test problems.

### Problem 1: `ModuleNotFoundError`

Message:

```text
ModuleNotFoundError: No module named 'calculator'
```

Likely causes:

- `calculator.py` is not in the same folder as the test file
- the file name is misspelled
- the test was run from an unexpected location

For today's layout, check that you have:

```text
day-95/
  calculator.py
  test_calculator.py
```

Then run:

```text
python day-95/test_calculator.py
```

### Problem 2: `AssertionError`

Message:

```text
AssertionError
```

Meaning:

```text
An assert statement expected True, but got False.
```

What to check:

- Which line failed?
- What value did the function return?
- What value did the test expect?
- Is the function wrong, or is the test expectation wrong?

A quick debugging move is to print the result temporarily:

```python
result = format_price(3)
print(result)
assert result == "$3.00"
```

Remove the temporary print after you understand the problem.

### Problem 3: The Test File Prints Nothing

If the file prints nothing, that might be fine.

A test file with only assertions may produce no output when everything passes.

In today's plain test file, this line gives you a small success message:

```python
print("All simple tests passed.")
```

Many real test tools do not rely on your own success print.

They show their own summary.

### Problem 4: The Function Prints Instead Of Returning

Problem:

```python
def double(number):
    print(number * 2)
```

Test attempt:

```python
assert double(4) == 8
```

That fails because `double(4)` returns `None`.

Fix the function:

```python
def double(number):
    return number * 2
```

Now this test works:

```python
assert double(4) == 8
```

### Problem 5: The Test Has Not Been Called

In a plain Python test file, defining a function is not enough.

This defines the test:

```python
def test_add_numbers():
    assert add(2, 3) == 5
```

This runs the test:

```python
test_add_numbers()
```

If you forget the call, the test function sits there unused.

`unittest` handles this differently.

It finds methods that start with `test_` inside a `unittest.TestCase` class.

Plain assert files need your calls unless you use a separate test runner.

## Read the Docs

Today, read documentation with two small questions in mind:

```text
What does assert do?
What does unittest provide?
```

Useful pages:

```text
https://docs.python.org/3/reference/simple_stmts.html#the-assert-statement
https://docs.python.org/3/library/unittest.html
```

In the `unittest` documentation, look for these names:

```text
TestCase
assertEqual
assertRaises
unittest.main
test discovery
```

You do not need every feature.

For now, the useful pattern is:

```python
import unittest


class SomethingTests(unittest.TestCase):
    def test_some_behavior(self):
        self.assertEqual(actual_value, expected_value)


if __name__ == "__main__":
    unittest.main()
```

The details will make more sense after you have written a few simple tests by hand.

## Mini Challenge

Create a small task helper and test it.

Create:

```text
day-95/tasks.py
```

Add:

```python
def count_done(tasks):
    total = 0

    for task in tasks:
        if task["done"]:
            total += 1

    return total


def has_task(tasks, title):
    for task in tasks:
        if task["title"].lower() == title.lower():
            return True

    return False
```

Create:

```text
day-95/test_tasks.py
```

Add tests using plain `assert`.

Start with this data:

```python
tasks = [
    {"title": "Write notes", "done": True},
    {"title": "Practice tests", "done": False},
    {"title": "Review project", "done": True},
]
```

Your tests should check:

- `count_done(tasks)` returns `2`
- `count_done([])` returns `0`
- `has_task(tasks, "Write notes")` returns `True`
- `has_task(tasks, "write notes")` returns `True`
- `has_task(tasks, "Missing task")` returns `False`

Run:

```text
python day-95/test_tasks.py
```

Add a final success print if you want:

```python
print("Task tests passed.")
```

The goal is not to build a whole task manager yet.

The goal is to practice checking small task rules before a larger project appears.

## Real-World Use

Tests become valuable when projects change.

Imagine you have a price function:

```python
def format_price(amount):
    return f"${amount:.2f}"
```

Later, you decide to support discounts, taxes, or different currencies.

Without tests, you might change the function and hope the older behavior still works.

With tests, you can check it:

```python
assert format_price(3) == "$3.00"
assert format_price(3.5) == "$3.50"
assert format_price(0) == "$0.00"
```

The tests become a memory of what the program promised.

That memory helps when:

- fixing bugs
- cleaning old code
- renaming functions
- splitting one file into several files
- adding new features
- checking edge cases you might forget by hand

Tests also work well with Git.

Git tells you what changed.

Tests tell you whether important behavior still works.

Together, they make experiments less stressful.

## Recap

A test is code that checks other code.

The simplest useful pattern is:

```python
assert function_call() == expected_value
```

Use tests to describe expected behavior.

Start with small functions that return values.

Separate logic from `input()` and `print()` when you can.

Run plain assert tests like this:

```text
python day-95/test_calculator.py
```

A passing assertion lets the program continue.

A failing assertion raises `AssertionError`.

Test normal cases and edge cases.

For invalid input, test that the function raises the error you expect.

Python also includes `unittest`, which groups tests in classes and provides helpers such as:

```python
self.assertEqual(actual, expected)
self.assertRaises(ValueError)
```

For today, plain `assert` is enough for most practice.

The main win is learning to turn expectations into repeatable checks.

## Lesson Checklist

Before moving on, make sure you can:

- explain what a test is
- write an `assert` statement
- read `assert add(2, 3) == 5` as an expectation
- create a separate test file
- import functions into a test file
- run a plain test file
- recognize a passing test
- recognize a failing test
- read an `AssertionError` line number
- explain what an edge case is
- test a function that raises `ValueError`
- explain why returning values makes functions easier to test
- separate logic code from input and printing
- recognize the basic shape of a `unittest.TestCase`
- run a simple `unittest` file

## Exercises

### Exercise 1: Test A Greeting Function

Create:

```text
day-95/greetings.py
```

Write:

```python
def make_greeting(name):
    return f"Hello, {name}!"
```

Create:

```text
day-95/test_greetings.py
```

Write tests for:

```text
Mina
Leo
an empty string
```

Think carefully about the empty string.

What should the function return?

Write the behavior you expect as an assertion.

### Exercise 2: Test A Total Function

Create:

```text
day-95/totals.py
```

Write:

```python
def calculate_total(prices):
    total = 0

    for price in prices:
        total += price

    return total
```

Create tests for:

- several prices
- one price
- an empty list
- decimal prices

### Exercise 3: Make A Test Fail On Purpose

Choose one passing test.

Change the expected value so it is wrong.

Run the test file.

Write down:

- the error type
- the file name
- the line number
- which expectation failed

Then fix the test and run it again.

### Exercise 4: Refactor For Testing

Start with this function:

```python
def show_discounted_price():
    price = float(input("Price: "))
    discount = float(input("Discount: "))
    print(price - discount)
```

Rewrite it into two parts:

```python
def get_discounted_price(price, discount):
    return price - discount
```

and a small user-facing part that asks for input and prints.

Then write at least three tests for `get_discounted_price()`.

### Exercise 5: Test An Error

Create:

```text
day-95/ages.py
```

Write:

```python
def get_age_group(age):
    if age < 0:
        raise ValueError("age cannot be negative")

    if age < 13:
        return "child"

    if age < 20:
        return "teen"

    return "adult"
```

Write plain `assert` tests for:

- age `8`
- age `13`
- age `19`
- age `20`
- age `-1` raising `ValueError`

### Exercise 6: Convert One Test To `unittest`

Choose one plain assert test file from today.

Create a second file that uses `unittest`.

Use this shape:

```python
import unittest


class MyTests(unittest.TestCase):
    def test_some_behavior(self):
        self.assertEqual(1 + 1, 2)


if __name__ == "__main__":
    unittest.main()
```

Replace `1 + 1` with a call to one of your functions.

Run the file directly.

### Exercise 7: Choose Edge Cases

For each function idea, list two edge cases you would test.

```text
find_longest_word(words)
calculate_average(scores)
is_valid_username(username)
get_first_item(items)
format_phone_number(number)
```

You do not have to write the functions.

Just practice choosing useful test cases.

### Exercise 8: Explain Testing In Your Own Words

Answer these questions:

- What does a test check?
- Why are functions with return values easier to test?
- What does `AssertionError` mean?
- Why should you test edge cases?
- How do tests help before refactoring?

Keep each answer short.

## Tiny Win

You can now make Python check your expectations for you.

That is a practical milestone.

You are not only running a program and hoping you noticed everything.

You are starting to build a small safety net around the behavior that matters.

## Tomorrow

Tomorrow is:

```text
Day 96: Refactoring With Tests
```

Today you wrote tests for small functions.

Tomorrow you will use tests before changing code.

That is where tests become more than practice.

They help you clean up a program while keeping its behavior steady.
