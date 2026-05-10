# Day 05: Numbers

**Focus:** Working with numbers in Python  
**You will practice:** integers, floats, arithmetic, variables, parentheses, and debugging calculations  
**Estimated time:** 35-45 minutes

## Today's Goal

Today you will learn how Python works with numbers.

By the end of this lesson, you should be able to:

- recognize integers and floats
- use Python as a calculator
- understand arithmetic operators
- control order of operations with parentheses
- store numbers in variables
- read number code out loud in plain English
- notice and fix common number mistakes

Numbers appear in scores, prices, ages, distances, timers, totals, averages, discounts, game health, bank balances, and many other ordinary programs.

Today is not about memorizing every math feature in Python. It is about becoming comfortable enough to ask Python small number questions and understand the answer.

## The Big Idea

Python can work with numbers directly.

```python
print(2 + 3)
```

Python prints:

```text
5
```

> Key idea: Programs often take numbers, perform a calculation, and produce a useful result.

A shopping program might calculate a total. A game might calculate a score. A fitness app might calculate distance. A school system might calculate an average grade.

```python
score = 10
bonus = 5
total_score = score + bonus

print(total_score)
```

The answer is:

```text
15
```

The program remembers two numbers, adds them, and shows the result. That is simple, but it is already the shape of many real programs.

## The Mental Model

Think of numbers in Python as values you can measure, combine, and compare.

Whole-number examples:

```python
7
42
0
-3
```

Decimal-number examples:

```python
3.5
19.99
0.25
-2.75
```

Python treats these as two common number types:

- `int` means integer, a whole number
- `float` means floating-point number, a number with a decimal point

You do not need to use the words `int` and `float` in every program yet, but you should recognize them.

```python
print(type(10))
print(type(10.5))
```

Python reports:

```text
<class 'int'>
<class 'float'>
```

The word `type` asks Python what kind of value something is.

For now, remember:

- `10` is an integer
- `10.5` is a float
- a decimal point usually makes a number a float

> Checkpoint: When you see a decimal point in a number literal, expect a `float`.

## Arithmetic Operators

Python uses operators to do arithmetic. An operator is a symbol that performs an operation.

| Operator | Meaning |
| --- | --- |
| `+` | addition |
| `-` | subtraction |
| `*` | multiplication |
| `/` | division |

```python
print(8 + 2)
print(8 - 2)
print(8 * 2)
print(8 / 2)
```

Python prints:

```text
10
6
16
4.0
```

Notice the last answer:

```text
4.0
```

In Python, `/` division gives a float, even when the answer is a whole number.

```python
print(8 / 2)
print(type(8 / 2))
```

That gives:

```text
4.0
<class 'float'>
```

That is not a mistake. It is Python's way of saying the value came from division, so the result is decimal-style.

## More Number Operators

Python has a few more number operators that are useful.

### Whole-Number Division

The `//` operator divides and keeps the whole-number part.

```python
print(10 // 3)
```

The result is:

```text
3
```

This means 3 fits into 10 three whole times.

### Remainder

The `%` operator gives the remainder after division.

```python
print(10 % 3)
```

This prints:

```text
1
```

This means 10 divided by 3 leaves a remainder of 1.

Whole-number division and remainder often work together.

```python
cookies = 10
people = 3

cookies_each = cookies // people
cookies_left = cookies % people

print(cookies_each)
print(cookies_left)
```

The output is:

```text
3
1
```

Each person gets 3 cookies, and 1 cookie is left.

### Powers

The `**` operator raises a number to a power.

```python
print(2 ** 3)
```

Python prints:

```text
8
```

This means:

```text
2 * 2 * 2
```

You will not need powers every day as a beginner, but it is useful to know what `**` means when you see it.

## Order of Operations

Python follows the usual order of operations. This matters when one line has more than one operator.

```python
print(2 + 3 * 4)
```

The answer is:

```text
14
```

Python multiplies first:

```text
3 * 4 is 12
2 + 12 is 14
```

If you want the addition to happen first, use parentheses.

```python
print((2 + 3) * 4)
```

Now the answer is:

```text
20
```

Parentheses are not only for changing math. They also make your intention clear.

```python
print(10 + 5 * 2)
print(10 + (5 * 2))
```

Both lines print `20`. The second line is easier to read because it shows what you meant.

When in doubt, use parentheses. Readable code is better than clever-looking code.

## Numeric Variables

Numbers become more useful when you store them in variables.

```python
price = 25
quantity = 4

total = price * quantity

print(total)
```

The total is:

```text
100
```

The variable names make the calculation easier to understand.

Compare two versions of the same calculation.

```python
x = 25
y = 4
z = x * y
print(z)
```

This prints the right answer:

```text
100
```

This works, but the names do not explain the calculation.

```python
price = 25
quantity = 4
total = price * quantity
print(total)
```

Both versions print:

```text
100
```

Both programs do the same calculation and print `100`. The second program explains the calculation more clearly.

Good variable names reduce confusion before confusion starts.

## Example

Imagine you are writing a tiny program to calculate the cost of movie tickets.

Save as: `day-05/ticket_total.py`

```python
ticket_price = 12
number_of_tickets = 3
snack_cost = 8

ticket_total = ticket_price * number_of_tickets
final_total = ticket_total + snack_cost

print(ticket_total)
print(final_total)
```

The output is:

```text
36
44
```

Read it slowly:

- each ticket costs 12
- there are 3 tickets
- snacks cost 8
- ticket total is `12 * 3`
- final total is ticket total plus snacks

The computer does the arithmetic, but the programmer gives the values meaningful names. That is the real skill here.

## Try It Yourself

Create a file named `day-05/number_practice.py`.

Write this program.

```python
apples = 12
friends = 5

apples_each = apples // friends
apples_left = apples % friends

print(apples_each)
print(apples_left)
```

Run it.

Python prints:

```text
2
2
```

This means:

```text
Each friend gets 2 apples.
There are 2 apples left.
```

Now change the numbers:

```python
apples = 23
friends = 4
```

Run the program again.

The practice loop is the same as before:

1. change one thing
2. save the file
3. run the file
4. read the output
5. explain the result in plain English

Do not skip the last step. If you can explain the result in plain English, you are not just copying code. You are understanding it.

## Common Mistake

### Mistake 1: Putting numbers in quotation marks

This is a number:

```python
age = 12
```

This is text:

```python
age = "12"
```

They look similar to a person, but they are different to Python.

With real numbers, Python can do arithmetic.

```python
print(12 + 3)
```

Python prints:

```text
15
```

With text, Python does something different.

```python
print("12" + "3")
```

This prints:

```text
123
```

Python joins the two pieces of text together. It does not add them as numbers.

> Key idea: Quotation marks are for text. Numbers used for math should usually be written without them.

### Mistake 2: Expecting Python to guess your order

```python
total = 10 + 5 * 2
print(total)
```

Python prints:

```text
20
```

If you expected `30`, your idea was probably:

```text
Add 10 and 5, then multiply by 2.
```

But Python followed the normal order of operations:

```text
Multiply 5 by 2, then add 10.
```

Fixed code:

```python
total = (10 + 5) * 2
print(total)
```

With parentheses, it prints:

```text
30
```

Python will not guess your intention. Parentheses make your intention visible.

## Debug It

Here is a broken program.

Broken code:

```python
price = 20
quantity = 3

total = price quantity

print(total)
```

What is wrong?

The multiplication operator is missing. Python does not understand:

```text
price quantity
```

Fixed code:

```python
price = 20
quantity = 3

total = price * quantity

print(total)
```

Now it prints:

```text
60
```

Here is another program with a logic bug. It runs, but the calculation is wrong.

Broken code:

```python
minutes = 2
seconds = 30

total_seconds = minutes + 60 + seconds

print(total_seconds)
```

It prints:

```text
92
```

The programmer probably wanted:

```text
2 minutes and 30 seconds is 150 seconds.
```

Fixed code:

```python
minutes = 2
seconds = 30

total_seconds = minutes * 60 + seconds

print(total_seconds)
```

Corrected, it prints:

```text
150
```

This is an important kind of debugging. Sometimes Python finds the problem and shows an error. Sometimes the code runs, but the result does not make sense.

When that happens, ask:

- What did I expect?
- What did Python actually print?
- Which calculation connects the two?
- Are my variables named clearly?
- Do I need parentheses?

Debugging number code often means checking the calculation one small piece at a time.

## Read the Docs

Look up the numeric types section in Python's official documentation.

Do not try to read the whole page. Your task is only to find examples of these operators:

```text
+
-
*
/
//
%
**
```

Documentation can feel dense early on. Use it as a reference, not as a book you must finish.

## Mini Challenge

Create a file named `day-05/receipt_calculator.py`.

Write a small program that calculates a simple receipt.

Use these values:

```python
item_price = 15
quantity = 3
tax = 4
```

Your program should calculate:

- the subtotal
- the final total after tax

```python
item_price = 15
quantity = 3
tax = 4

subtotal = item_price * quantity
final_total = subtotal + tax

print(subtotal)
print(final_total)
```

It should print:

```text
45
49
```

Once it works, change the numbers and run it again.

Then add one more variable:

```python
discount = 5
```

Update your final total so the discount is subtracted.

The goal is not to make a fancy receipt yet. The goal is to practice turning a plain-English idea into numeric steps.

## Real-World Use

Numbers appear in almost every kind of program.

Examples:

- a game subtracts health when a player takes damage
- a store calculates price, tax, discounts, and change
- a calendar counts days until an event
- a music app tracks the length of a song
- a weather app shows temperature
- a sports app updates scores
- a budget app adds income and expenses

The formulas may become more complicated later, but the basic pattern stays familiar:

```text
store numbers
calculate with them
show or use the result
```

That is what you practiced today.

## Recap

Today you learned:

- integers are whole numbers
- floats are numbers with decimals
- Python can add, subtract, multiply, and divide
- `/` gives a float result
- `//` gives whole-number division
- `%` gives the remainder
- `**` means power
- Python follows order of operations
- parentheses make calculations clearer
- numeric variables make programs easier to read
- quotation marks turn numbers into text
- debugging number code means comparing expected results with actual results

Main idea: numbers let programs calculate useful answers from simple values.

## Exercises

### Exercise 1

Write a program that prints the answers to these calculations.

Calculations to use:

```text
7 + 5
20 - 8
6 * 4
24 / 3
```

Before you run the program, write down what you expect each answer to be.

### Exercise 2

Create these variables:

```python
length = 8
width = 5
```

Calculate and print the area of a rectangle.

Hint:

```text
area = length * width
```

### Exercise 3

Write a program that converts minutes to seconds.

Start with:

```python
minutes = 7
```

It should print:

```text
420
```

### Exercise 4

Use `//` and `%` to divide 17 candies among 4 people.

Your program should print:

- how many candies each person gets
- how many candies are left

### Exercise 5

Fix this code.

Broken code:

```python
price = 30
quantity = 2
total = price quantity
print(total)
```

### Exercise 6

Fix this code so it prints `30`.

Broken code:

```python
answer = 10 + 5 * 2
print(answer)
```

### Exercise 7

Predict the output before running the code.

```python
print(9 / 2)
print(9 // 2)
print(9 % 2)
```

Then run it and compare.

### Exercise 8

Write a small program for a game score.

Use these variables:

```python
base_score = 100
coins = 7
coin_value = 5
```

Calculate and print the final score.

Hint:

```text
final score = base score + coins times coin value
```

## Lesson Checklist

Before moving on, check that you can:

- tell the difference between an `int` and a `float`
- use `+`, `-`, `*`, `/`, `//`, `%`, and `**`
- explain why `8 / 2` prints `4.0`
- use parentheses to control or clarify a calculation
- store numbers in variables with clear names
- spot a missing operator in number code
- compare expected output with actual output

## Tiny Win

Yesterday, variables gave you a way to name information.

Today, numbers gave those variables something useful to do.

You can now write small programs that calculate totals, convert units, divide items, and check your own reasoning against Python's output.

That is a quiet but important step.

## Tomorrow

Tomorrow, you will work with strings: Python's way of handling text.
