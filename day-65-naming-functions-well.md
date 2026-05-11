# Day 65: Naming Functions Well

**Focus:** Choosing function names that clearly describe one job  
**You will practice:** naming functions with verbs, avoiding vague names, matching names to return or print behavior, naming helper functions, and renaming messy functions  
**Estimated time:** 40-55 minutes

## Today's Goal

Today you will practice naming functions well.

You already know how to:

- define a function
- pass values into a function
- return a value
- print inside a function
- split a larger problem into smaller jobs

Now you need a habit that makes all of those skills easier to read.

Give each function a name that explains its job.

By the end of this lesson, you should be able to:

- choose function names that sound like actions
- avoid vague names like `do_stuff()` and `handle_data()`
- use names that match what the function returns or prints
- name small helper functions clearly
- rename messy functions without changing what the program does
- notice when a vague name means the function is doing too much
- prepare for Day 66, where you will practice common function mistakes

The main idea:

```text
A good function name tells the reader what job is about to happen.
```

The name does not need to explain every line inside the function.

It should explain the one job the function owns.

## The Big Idea

A function name is a promise.

If a function is named `calculate_total()`, the reader expects it to calculate a total and give that total back.

If a function is named `print_receipt()`, the reader expects it to print a receipt.

If a function is named `format_name()`, the reader expects it to build a cleaner name string.

Good function names usually start with a verb:

```text
calculate_total
print_receipt
format_name
count_completed_tasks
find_longest_word
get_active_users
is_passing
has_discount
```

The verb tells the reader what kind of action the function performs.

Compare these names:

```text
data()
thing()
work()
do_stuff()
process()
```

Those names do not tell you much.

You have to open the function and read every line before you know why it exists.

Now compare:

```text
clean_username()
calculate_average_score()
print_task_report()
count_overdue_tasks()
format_receipt_line()
```

These names are longer, but they are easier to trust.

They tell the reader what to expect before the reader sees the code.

Example:

```python
def calculate_total(prices):
    total = 0

    for price in prices:
        total += price

    return total


cart_prices = [20, 15, 5]
cart_total = calculate_total(cart_prices)
print("Total:", cart_total)
```

You should see:

```text
Total: 40
```

The name `calculate_total()` fits the job.

It calculates a number.

It returns the number.

The printing happens outside the function.

Now look at a weaker name:

```python
def do_stuff(prices):
    total = 0

    for price in prices:
        total += price

    return total


cart_prices = [20, 15, 5]
cart_total = do_stuff(cart_prices)
print("Total:", cart_total)
```

You should see:

```text
Total: 40
```

The program works.

But the name hides the meaning.

The reader has to inspect the function body to learn that `do_stuff()` calculates a total.

Working code can still be hard to read.

Good names reduce that extra work.

## The Mental Model

Think of a function name as a label on a drawer.

A drawer labeled `stuff` does not help much.

You have to open it and search.

A drawer labeled `receipts` is more useful.

You know what belongs inside it.

Function names work the same way.

The name should make the job easy to find.

The name should also help you decide whether the code inside belongs there.

If you name a function `count_vowels()`, this code fits:

```python
def count_vowels(word):
    count = 0

    for letter in word:
        if letter in "aeiou":
            count += 1

    return count


print(count_vowels("banana"))
```

You should see:

```text
3
```

The name says:

```text
count vowels
```

The function does exactly that.

It does not print a full report.

It does not ask for input.

It does not change a list.

It counts and returns the count.

If the function also printed a message, saved data, and asked for another word, the name would no longer fit.

That is a useful warning.

When a function name feels impossible to choose, the function may have more than one job.

## Try It Yourself

Create a file named:

```text
day-65/naming_functions.py
```

Work through these examples one at a time.

### Step 1: Rename A Vague Function

Start with this code:

```python
def thing(numbers):
    total = 0

    for number in numbers:
        total += number

    return total


scores = [8, 10, 7]
print(thing(scores))
```

You should see:

```text
25
```

The function works, but `thing()` does not explain the job.

Rename it:

```python
def calculate_total(numbers):
    total = 0

    for number in numbers:
        total += number

    return total


scores = [8, 10, 7]
print(calculate_total(scores))
```

You should see:

```text
25
```

The output did not change.

The name did.

That is often what a good rename does.

It makes the code easier to read without changing the result.

### Step 2: Use A Verb

Function names should usually sound like actions.

This name is weak:

```python
def report(tasks):
    print("Tasks:")

    for task in tasks:
        print("- " + task)


today_tasks = ["read", "practice", "review"]
report(today_tasks)
```

You should see:

```text
Tasks:
- read
- practice
- review
```

`report()` is not terrible, but it is not as clear as it could be.

This version says what happens:

```python
def print_task_report(tasks):
    print("Tasks:")

    for task in tasks:
        print("- " + task)


today_tasks = ["read", "practice", "review"]
print_task_report(today_tasks)
```

You should see:

```text
Tasks:
- read
- practice
- review
```

The verb `print` matters.

The reader now knows this function displays something on the screen.

### Step 3: Match The Name To The Return Value

If a function returns a value, the name should make that value easy to guess.

Code:

```python
def get_initials(first_name, last_name):
    first_initial = first_name[0].upper()
    last_initial = last_name[0].upper()
    return first_initial + last_initial


initials = get_initials("mina", "patel")
print(initials)
```

You should see:

```text
MP
```

The name `get_initials()` tells the reader that the function gives back initials.

This name would be confusing:

```python
def print_initials(first_name, last_name):
    first_initial = first_name[0].upper()
    last_initial = last_name[0].upper()
    return first_initial + last_initial


initials = print_initials("mina", "patel")
print(initials)
```

You should see:

```text
MP
```

The code runs, but the name is misleading.

`print_initials()` sounds like it should print.

It actually returns a string.

A better name is `get_initials()` or `format_initials()`.

### Step 4: Match The Name To Printing

If a function prints, say so when it helps.

Code:

```python
def print_welcome_message(name):
    print("Welcome, " + name + ".")
    print("Glad you are here.")


print_welcome_message("Asha")
```

You should see:

```text
Welcome, Asha.
Glad you are here.
```

This function does not return a reusable value.

Its job is to display text.

The name says that clearly.

Now compare this:

```python
def get_welcome_message(name):
    print("Welcome, " + name + ".")
    print("Glad you are here.")


message = get_welcome_message("Asha")
print(message)
```

You should see:

```text
Welcome, Asha.
Glad you are here.
None
```

The name `get_welcome_message()` suggests that the function returns a message.

But the function prints and gives back `None`.

A name can make a bug easier to notice.

If the function prints, `print_welcome_message()` fits better.

If the function returns text, write it this way:

```python
def get_welcome_message(name):
    return "Welcome, " + name + "."


message = get_welcome_message("Asha")
print(message)
```

You should see:

```text
Welcome, Asha.
```

Now the name and behavior match.

### Step 5: Name Boolean Functions Like Questions

A function that returns `True` or `False` often reads well as a question.

Code:

```python
def is_passing(score):
    return score >= 60


print(is_passing(75))
print(is_passing(42))
```

You should see:

```text
True
False
```

The name `is_passing()` reads naturally:

```text
Is this score passing?
```

Other boolean names often start with:

```text
is
has
can
should
```

Examples:

```text
is_empty
has_discount
can_vote
should_show_warning
```

That style helps when you use the function inside an `if` statement.

Code:

```python
def has_discount(is_member, total):
    return is_member and total >= 50


if has_discount(True, 80):
    print("Discount applied.")
else:
    print("No discount.")
```

You should see:

```text
Discount applied.
```

The `if` line reads almost like a sentence.

### Step 6: Name Helper Functions By Their Smaller Job

A helper function is a smaller function used by another function.

It still deserves a clear name.

Code:

```python
def format_task(task):
    return "- " + task


def print_tasks(tasks):
    for task in tasks:
        print(format_task(task))


tasks = ["write notes", "practice functions", "read docs"]
print_tasks(tasks)
```

You should see:

```text
- write notes
- practice functions
- read docs
```

`format_task()` is a helper.

It handles one task.

`print_tasks()` handles the whole list.

The names show how the functions work together.

Helper names should not be vague just because the helper is small.

Avoid names like:

```text
helper()
fix()
part_two()
small_job()
```

Prefer names like:

```text
format_task()
clean_email()
count_matches()
build_summary_line()
```

Small jobs still need honest names.

### Step 7: Rename Without Changing Behavior

Renaming is a normal part of programming.

Start with this:

```python
def handle(items):
    count = 0

    for item in items:
        if item == "done":
            count += 1

    return count


statuses = ["done", "open", "done", "waiting"]
print(handle(statuses))
```

You should see:

```text
2
```

The function counts finished items.

Rename it:

```python
def count_done_items(items):
    count = 0

    for item in items:
        if item == "done":
            count += 1

    return count


statuses = ["done", "open", "done", "waiting"]
print(count_done_items(statuses))
```

You should see:

```text
2
```

When you rename a function, rename both places:

```text
the function definition
the function call
```

In this example:

```text
def count_done_items(items):
```

and:

```text
print(count_done_items(statuses))
```

must use the same name.

## Common Mistake

A common mistake is choosing a name that is too general.

Broken code:

```python
def process(data):
    total = 0

    for number in data:
        total += number

    return total / len(data)


scores = [80, 90, 100]
print(process(scores))
```

You should see:

```text
90.0
```

The code works, but the name is weak.

`process()` could mean almost anything:

```text
clean the data
sort the data
print the data
save the data
calculate something from the data
```

The function really calculates an average.

Fixed code:

```python
def calculate_average(numbers):
    total = 0

    for number in numbers:
        total += number

    return total / len(numbers)


scores = [80, 90, 100]
print(calculate_average(scores))
```

You should see:

```text
90.0
```

Better names often come from the answer to this question:

```text
What does this function do in one short sentence?
```

For this function:

```text
It calculates the average.
```

So the name can be:

```text
calculate_average
```

If the answer is:

```text
It does a few things with the user and the report.
```

the function probably needs to be split.

## Debug It

Naming bugs are not always syntax bugs.

Sometimes the program runs, but the names point the reader in the wrong direction.

Broken code:

```python
def get_total(prices):
    total = 0

    for price in prices:
        total += price

    print("Total:", total)


cart = [12, 8, 5]
total = get_total(cart)
print("With shipping:", total + 3)
```

This code prints the total inside the function, then breaks when the program tries to add shipping.

The name `get_total()` suggests that the function returns a total.

But it does not return anything.

In Python, that means it gives back `None`.

The fix depends on the job you want.

If the program needs to use the total, return it:

Fixed code:

```python
def calculate_total(prices):
    total = 0

    for price in prices:
        total += price

    return total


cart = [12, 8, 5]
total = calculate_total(cart)
print("Total:", total)
print("With shipping:", total + 3)
```

You should see:

```text
Total: 25
With shipping: 28
```

If the function's only job is to display the total, name it that way:

```python
def print_total(prices):
    total = 0

    for price in prices:
        total += price

    print("Total:", total)


cart = [12, 8, 5]
print_total(cart)
```

You should see:

```text
Total: 25
```

The important part is that the name and behavior agree.

Use this small checklist when a function name feels wrong:

- Does the name start with a useful action word?
- Does the function do one job?
- Does the name say whether the function prints, returns, formats, counts, finds, or checks something?
- If the function returns `True` or `False`, does the name read like a question?
- If the function is a helper, does the helper name explain its smaller job?

## Read the Docs

Python's official tutorial explains function definitions here:

[Python tutorial: Defining Functions](https://docs.python.org/3/tutorial/controlflow.html#defining-functions)

Today, do not try to study every advanced detail.

Look for the function names in the examples.

Ask:

- What action does this name describe?
- What values go into the function?
- Does the function return a value?
- Does the name help me guess what the function does?

You can also look at built-in Python function names you already know:

```text
print
len
sorted
sum
max
min
```

Some built-in names are short because they are used constantly.

Your own function names can usually be more specific.

For example:

```text
calculate_cart_total
find_highest_score
print_daily_summary
format_customer_name
```

Specific names are easier to read in your own programs.

## Mini Challenge

Rename this small program.

Code:

```python
def a(words):
    longest = ""

    for word in words:
        if len(word) > len(longest):
            longest = word

    return longest


def b(word):
    return word.upper()


def c(words):
    word = a(words)
    print(b(word))


names = ["Mina", "Alexander", "Jo"]
c(names)
```

You should see:

```text
ALEXANDER
```

The output is fine.

The names are not.

Try to rename:

```text
a
b
c
```

Possible answer:

```python
def find_longest_word(words):
    longest = ""

    for word in words:
        if len(word) > len(longest):
            longest = word

    return longest


def format_as_uppercase(word):
    return word.upper()


def print_longest_word(words):
    word = find_longest_word(words)
    print(format_as_uppercase(word))


names = ["Mina", "Alexander", "Jo"]
print_longest_word(names)
```

You should see:

```text
ALEXANDER
```

This version is longer.

But it is much easier to follow.

You can read the final line and understand the program's main job:

```text
print_longest_word(names)
```

## Real-World Use

Good function names matter more as programs grow.

In a small file, you can read everything.

In a larger project, you often read one function call and need to understand what it means without opening every function.

A contact app might use names like:

```text
add_contact
find_contact_by_name
format_contact
print_contact_summary
```

A shopping app might use:

```text
calculate_subtotal
apply_discount
calculate_tax
print_receipt
```

A quiz app might use:

```text
count_correct_answers
calculate_score_percent
is_passing_score
print_score_report
```

Notice the pattern.

The names are not clever.

They are useful.

They tell you what the program is doing.

Good names also make future changes easier.

If you need to change receipt formatting, `format_receipt_line()` is a natural place to look.

If you need to change the score rule, `is_passing_score()` is a natural place to look.

If everything is named `process()` and `handle()`, you have to hunt.

## Recap

Today you practiced naming functions well.

A good function name should:

- describe one clear job
- usually start with a verb
- be specific enough to help the reader
- match whether the function returns or prints
- make boolean functions read like questions
- give helper functions honest names
- make messy code easier to understand after a rename

Some useful verbs are:

```text
calculate
count
find
format
get
print
clean
build
check
convert
```

Use the verb that matches the job.

Not every function needs a long name.

But every function needs a useful name.

## Lesson Checklist

- [ ] I can explain why function names should describe actions.
- [ ] I can replace vague names like `do_stuff()` with clearer names.
- [ ] I can choose names that match return values.
- [ ] I can choose names that match printed output.
- [ ] I can name boolean functions with `is`, `has`, `can`, or `should`.
- [ ] I can name helper functions by their smaller jobs.
- [ ] I can rename a function definition and its calls.
- [ ] I can notice when a vague name means a function may be doing too much.

## Exercises

### Exercise 1: Choose Better Names

Write better names for these functions:

```text
do_stuff()
thing()
process()
part_one()
helper()
```

Use the job descriptions below:

```text
prints a menu
counts completed tasks
formats a phone number
checks if a user is logged in
calculates the final bill
```

Example answers:

```text
print_menu()
count_completed_tasks()
format_phone_number()
is_logged_in()
calculate_final_bill()
```

### Exercise 2: Rename The Function

This code works, but the function name is weak.

```python
def work(names):
    clean_names = []

    for name in names:
        clean_names.append(name.strip().title())

    return clean_names


students = [" mina ", "SAM", " leena"]
print(work(students))
```

Rename the function.

One possible name:

```text
clean_names
```

After renaming, the function call should use the new name too.

### Exercise 3: Return Or Print

Look at this function:

```python
def get_report(title, total):
    print(title)
    print("Total:", total)
```

Does the name fit?

If the function should print, rename it.

If the function should return text, rewrite it so the name fits.

### Exercise 4: Boolean Name

Write a function named `is_even(number)`.

It should return `True` if the number is even.

It should return `False` otherwise.

Try this:

```python
def is_even(number):
    return number % 2 == 0


print(is_even(4))
print(is_even(7))
```

You should see:

```text
True
False
```

### Exercise 5: Name The Helpers

Write a small program with these functions:

```text
format_item(item)
print_items(items)
print_shopping_list(items)
```

Use this data:

```python
items = ["rice", "milk", "apples"]
```

The program should print:

```text
Shopping List
-------------
- rice
- milk
- apples
```

### Exercise 6: Rename Messy Code

Rename the functions in this program.

Do not change the output.

```python
def x(scores):
    total = 0

    for score in scores:
        total += score

    return total / len(scores)


def y(average):
    return average >= 60


def z(scores):
    average = x(scores)
    print("Average:", average)
    print("Passing:", y(average))


quiz_scores = [70, 80, 90]
z(quiz_scores)
```

You should see:

```text
Average: 80.0
Passing: True
```

Possible names:

```text
calculate_average
is_passing
print_score_report
```

### Exercise 7: Spot The Mismatch

This function name and behavior do not match.

```python
def print_full_name(first_name, last_name):
    return first_name + " " + last_name
```

Choose one fix:

```text
Rename it to format_full_name.
Keep the name and make it print.
```

Both can be correct.

The important part is making the name match the job.

### Exercise 8: One Sentence Test

Pick three functions from your own recent files.

For each one, write:

```text
Function name:
One-sentence job:
Does the name match the job?
Better name:
```

If a function needs a long sentence with the word "and" several times, it may be doing too much.

## Tiny Win

Open one older practice file.

Find one function name that could be clearer.

Rename only that function and its calls.

Run the file again.

If the output stays the same and the code reads better, that is a real improvement.

Small renames build good habits.

## Tomorrow

Tomorrow you will study common function mistakes.

You will practice bugs like:

- forgetting to call a function
- forgetting `return`
- mixing up parameters and arguments
- using a variable outside its scope
- printing when the program needed a returned value
- returning too early

Good names will help you catch many of those mistakes faster.
