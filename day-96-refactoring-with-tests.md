# Day 96: Refactoring with Tests

**Focus:** Improving code structure while keeping the same behavior  
**You will practice:** writing tests before changing code, using tests as guardrails, extracting functions, renaming carefully, simplifying conditionals, removing duplication, checking behavior before and after a refactor, and preparing cleaner code for a capstone project  
**Estimated time:** 60-75 minutes

## Today's Goal

Today you will practice refactoring.

Refactoring means changing the structure of code without changing what the code does.

That idea matters because working code is not always clear code.

Sometimes the first version of a program is:

- too long
- repetitive
- hard to name
- hard to test
- hard to explain
- scary to edit

Refactoring is how you improve that code after you understand it better.

By the end of today, you should be able to:

- explain what refactoring means
- explain why tests are useful before a refactor
- write a few tests that describe current behavior
- run those tests before changing code
- extract a helper function from a larger function
- rename variables so the code tells a clearer story
- simplify repeated conditionals
- remove duplicated calculations
- run the same tests after the refactor
- avoid changing behavior by accident
- prepare for Day 97, where you will plan your capstone project

The key rule is simple:

```text
First prove what the code does.
Then improve how the code is written.
Then prove it still does the same thing.
```

## The Big Idea

Refactoring is not the same as adding a feature.

Adding a feature changes what the program can do.

Refactoring changes how the program is organized.

Imagine you have a receipt program that already prints the correct total.

Feature change:

```text
Add a loyalty-points total to the receipt.
```

Refactor:

```text
Move the tax calculation into its own function.
```

The feature changes behavior.

The refactor should not.

That is why tests matter.

A test is a small check that says:

```text
For this input, this behavior should still happen.
```

Before refactoring, tests help you understand what the current code promises.

After refactoring, the same tests help you check whether you kept those promises.

Tests do not make refactoring perfect, but they give you guardrails.

Without tests, you may change a messy function and hope it still works.

With tests, you can change a messy function and check.

## The Mental Model

Think of refactoring like cleaning a room while keeping everything important.

You are allowed to:

- move things into better places
- label things more clearly
- remove duplicate piles
- make the walking path easier

You are not allowed to:

- throw away something the program still needs
- change the meaning of the room
- hide a broken item under the bed and call it done

In code, that means you can:

- extract a repeated calculation into a function
- rename `x` to `subtotal`
- replace a nested `if` block with clearer early returns
- move formatting into a helper
- split one long function into smaller functions

But the behavior should stay the same.

A useful beginner refactoring loop looks like this:

```text
1. Pick a small piece of working code.
2. Write tests for the behavior you want to protect.
3. Run the tests and make sure they pass.
4. Make one small refactoring change.
5. Run the tests again.
6. Repeat.
```

Do not refactor ten things at once.

Small steps make it easier to know which change caused a problem.

## Example

You will start with a working but messy receipt function.

The function takes a list of items, a customer kind, and a coupon code.

It returns a receipt as text.

Create this file:

```text
day-96/receipt.py
```

Add this first version:

```python
def make_receipt(items, customer_kind, coupon_code):
    subtotal = 0

    for item in items:
        subtotal = subtotal + item["price"] * item["quantity"]

    discount = 0

    if customer_kind == "member":
        if coupon_code == "SAVE10":
            discount = subtotal * 0.10
        else:
            discount = subtotal * 0.05
    else:
        if coupon_code == "SAVE10":
            discount = subtotal * 0.10
        else:
            discount = 0

    after_discount = subtotal - discount
    tax = after_discount * 0.08
    total = after_discount + tax

    lines = []
    lines.append("Receipt")
    lines.append(f"Subtotal: ${subtotal:.2f}")
    lines.append(f"Discount: ${discount:.2f}")
    lines.append(f"Tax: ${tax:.2f}")
    lines.append(f"Total: ${total:.2f}")

    return "\n".join(lines)
```

This function is not terrible.

It works.

But it asks your brain to hold too many details at once:

- adding item totals
- choosing a discount
- applying tax
- formatting money
- building receipt lines

Before you improve the structure, protect the behavior.

Create this file:

```text
day-96/test_receipt.py
```

Add:

```python
from receipt import make_receipt


def test_regular_customer_without_coupon():
    items = [
        {"name": "Notebook", "price": 5.00, "quantity": 2},
    ]

    receipt = make_receipt(items, "regular", "")

    assert "Subtotal: $10.00" in receipt
    assert "Discount: $0.00" in receipt
    assert "Tax: $0.80" in receipt
    assert "Total: $10.80" in receipt


def test_member_gets_member_discount():
    items = [
        {"name": "Notebook", "price": 5.00, "quantity": 2},
    ]

    receipt = make_receipt(items, "member", "")

    assert "Subtotal: $10.00" in receipt
    assert "Discount: $0.50" in receipt
    assert "Tax: $0.76" in receipt
    assert "Total: $10.26" in receipt


def test_coupon_beats_regular_price():
    items = [
        {"name": "Backpack", "price": 20.00, "quantity": 1},
    ]

    receipt = make_receipt(items, "regular", "SAVE10")

    assert "Subtotal: $20.00" in receipt
    assert "Discount: $2.00" in receipt
    assert "Tax: $1.44" in receipt
    assert "Total: $19.44" in receipt


def test_multiple_items_are_added():
    items = [
        {"name": "Pen", "price": 1.50, "quantity": 3},
        {"name": "Bag", "price": 12.00, "quantity": 1},
    ]

    receipt = make_receipt(items, "regular", "")

    assert "Subtotal: $16.50" in receipt
    assert "Total: $17.82" in receipt


if __name__ == "__main__":
    test_regular_customer_without_coupon()
    test_member_gets_member_discount()
    test_coupon_beats_regular_price()
    test_multiple_items_are_added()
    print("All receipt tests passed.")
```

Run the tests from inside the `day-96` folder:

```text
python test_receipt.py
```

You should see:

```text
All receipt tests passed.
```

That message is your safety check.

Now you can refactor.

### Step 1: Extract The Subtotal Function

The first part of `make_receipt()` calculates the subtotal:

```python
subtotal = 0

for item in items:
    subtotal = subtotal + item["price"] * item["quantity"]
```

Move that job into its own function:

```python
def calculate_subtotal(items):
    subtotal = 0

    for item in items:
        subtotal += item["price"] * item["quantity"]

    return subtotal
```

This is called extracting a function.

You are taking a smaller job out of a larger function and giving it a name.

After that change, `make_receipt()` can say:

```python
subtotal = calculate_subtotal(items)
```

That line is easier to read because the function name explains the job.

### Step 2: Extract The Discount Rule

The discount logic is the most tangled part:

```python
if customer_kind == "member":
    if coupon_code == "SAVE10":
        discount = subtotal * 0.10
    else:
        discount = subtotal * 0.05
else:
    if coupon_code == "SAVE10":
        discount = subtotal * 0.10
    else:
        discount = 0
```

Look for duplicated behavior.

Both members and regular customers get 10 percent off with `SAVE10`.

Members get 5 percent off when there is no coupon.

Regular customers get no discount when there is no coupon.

That can become:

```python
def calculate_discount(subtotal, customer_kind, coupon_code):
    if coupon_code == "SAVE10":
        return subtotal * 0.10

    if customer_kind == "member":
        return subtotal * 0.05

    return 0
```

This version is shorter because each rule appears once.

It is also easier to test in your head:

```text
Coupon?
Member?
Otherwise no discount.
```

### Step 3: Extract Formatting

The receipt uses the same money format several times:

```python
${subtotal:.2f}
${discount:.2f}
${tax:.2f}
${total:.2f}
```

That format can become a helper:

```python
def format_money(amount):
    return f"${amount:.2f}"
```

Now the receipt lines can say:

```python
f"Subtotal: {format_money(subtotal)}"
```

The behavior is the same.

The meaning is clearer.

### Step 4: Replace The File With The Refactored Version

Now update `day-96/receipt.py`:

```python
TAX_RATE = 0.08
MEMBER_DISCOUNT_RATE = 0.05
COUPON_DISCOUNT_RATE = 0.10


def calculate_subtotal(items):
    subtotal = 0

    for item in items:
        subtotal += item["price"] * item["quantity"]

    return subtotal


def calculate_discount(subtotal, customer_kind, coupon_code):
    if coupon_code == "SAVE10":
        return subtotal * COUPON_DISCOUNT_RATE

    if customer_kind == "member":
        return subtotal * MEMBER_DISCOUNT_RATE

    return 0


def calculate_tax(amount):
    return amount * TAX_RATE


def format_money(amount):
    return f"${amount:.2f}"


def make_receipt(items, customer_kind, coupon_code):
    subtotal = calculate_subtotal(items)
    discount = calculate_discount(subtotal, customer_kind, coupon_code)
    taxable_amount = subtotal - discount
    tax = calculate_tax(taxable_amount)
    total = taxable_amount + tax

    lines = [
        "Receipt",
        f"Subtotal: {format_money(subtotal)}",
        f"Discount: {format_money(discount)}",
        f"Tax: {format_money(tax)}",
        f"Total: {format_money(total)}",
    ]

    return "\n".join(lines)
```

Run the same test file again:

```text
python test_receipt.py
```

You should still see:

```text
All receipt tests passed.
```

That is the point of this lesson.

You changed the structure.

You did not change the behavior.

## Refactoring Moves

There are many refactoring techniques, but beginners only need a few to become much more confident.

### Extract A Function

Use this when several lines have one clear job.

Before:

```python
subtotal = 0

for item in items:
    subtotal += item["price"] * item["quantity"]
```

After:

```python
def calculate_subtotal(items):
    subtotal = 0

    for item in items:
        subtotal += item["price"] * item["quantity"]

    return subtotal
```

Good signs that extraction may help:

- the larger function is hard to scan
- a group of lines has a name in your head
- you want to test one smaller rule
- the same code appears in more than one place

### Rename For Meaning

Renaming is one of the simplest refactors.

Before:

```python
x = subtotal - discount
y = x * 0.08
z = x + y
```

After:

```python
taxable_amount = subtotal - discount
tax = taxable_amount * 0.08
total = taxable_amount + tax
```

The math did not change.

The story did.

Good names reduce the number of comments you need.

### Simplify Conditionals

Nested conditionals can hide simple rules.

Before:

```python
def letter_grade(score):
    if score >= 90:
        return "A"
    else:
        if score >= 80:
            return "B"
        else:
            if score >= 70:
                return "C"
            else:
                return "Needs practice"
```

After:

```python
def letter_grade(score):
    if score >= 90:
        return "A"

    if score >= 80:
        return "B"

    if score >= 70:
        return "C"

    return "Needs practice"
```

The second version is not shorter by much, but it is easier to read.

Each `return` exits the function, so you do not need the extra `else` blocks.

Protect it with tests:

```python
assert letter_grade(95) == "A"
assert letter_grade(82) == "B"
assert letter_grade(70) == "C"
assert letter_grade(50) == "Needs practice"
```

### Remove Duplication

Duplicate code is not only annoying.

It is risky.

If the same rule appears in three places, you might update one copy and forget the others.

Before:

```python
if coupon_code == "SAVE10":
    discount = subtotal * 0.10
elif customer_kind == "member":
    discount = subtotal * 0.05
else:
    discount = 0
```

Better:

```python
def calculate_discount(subtotal, customer_kind, coupon_code):
    if coupon_code == "SAVE10":
        return subtotal * COUPON_DISCOUNT_RATE

    if customer_kind == "member":
        return subtotal * MEMBER_DISCOUNT_RATE

    return 0
```

Now the discount rule has one home.

## Try It Yourself

Create a folder named:

```text
day-96
```

Inside it, create:

```text
day-96/receipt.py
day-96/test_receipt.py
```

Use the first version of `receipt.py`.

Then write and run the tests.

Your first goal is not to refactor yet.

Your first goal is to get this message:

```text
All receipt tests passed.
```

After the tests pass, refactor one step at a time:

```text
1. Extract calculate_subtotal().
2. Run the tests.
3. Extract calculate_discount().
4. Run the tests.
5. Extract calculate_tax().
6. Run the tests.
7. Extract format_money().
8. Run the tests.
```

If a test fails, pause.

Do not keep refactoring.

The failing test is telling you that one of your changes may have changed behavior.

## Common Mistake

The most common mistake is refactoring and adding a new feature at the same time.

For example, imagine you are cleaning the receipt code and you also decide:

```text
I should add free shipping for members.
```

That may be a useful feature.

But it should be a separate step.

During a refactor, the question is:

```text
Does the same input still produce the same result?
```

If you add a feature at the same time, a failing test becomes harder to understand.

Did the test fail because the refactor broke old behavior?

Or did it fail because the feature intentionally changed behavior?

Keep those jobs separate:

```text
Refactor first.
Run tests.
Then add the feature.
Update or add tests for the feature.
```

Another common mistake is refactoring without first checking the current behavior.

Even if the current code looks ugly, it may contain rules you have not noticed yet.

Tests help you capture those rules before you move code around.

## Debug It

Refactoring bugs often look small, but they can change results.

### Problem 1: The Total Changed After Refactoring

You refactored the receipt code, and this test fails:

```python
assert "Total: $10.26" in receipt
```

Ask:

- Did the subtotal stay the same?
- Did the discount stay the same?
- Did tax use the amount after discount?
- Did the money formatting still round to two decimal places?

In this project, tax should be calculated after the discount:

```python
taxable_amount = subtotal - discount
tax = calculate_tax(taxable_amount)
```

If you accidentally tax the original subtotal, the result changes.

### Problem 2: The Test Cannot Import The Function

You might see:

```text
ImportError
```

or:

```text
ModuleNotFoundError
```

Check:

- Are `receipt.py` and `test_receipt.py` in the same folder?
- Are you running the command from inside `day-96`?
- Is the function still named `make_receipt`?
- Did you rename a public function without updating the test?

Renaming helper variables is usually safe.

Renaming a function that other files import needs more care.

### Problem 3: The Tests Pass, But The Code Still Feels Messy

That can happen.

Passing tests only say the checked behavior still works.

They do not say the code is perfectly designed.

Refactoring is a series of small improvements.

After one pass, you might still notice:

- a function with too many parameters
- a name that could be clearer
- a test case that should be added
- a repeated rule that still needs one home

That is normal.

Make the next small improvement and run the tests again.

### Problem 4: You Are Not Sure What To Test

Start with behavior a user would notice.

For the receipt program, a user would notice:

- subtotal
- discount
- tax
- total

Then add one test for each rule:

- regular customer, no coupon
- member, no coupon
- regular customer, coupon
- more than one item

You do not need twenty tests before a small refactor.

You need enough tests to warn you if you accidentally change the important behavior.

## Read the Docs

Today, read documentation with one small purpose:

```text
How does Python run simple checks?
```

Useful pages:

```text
https://docs.python.org/3/reference/simple_stmts.html#the-assert-statement
https://docs.python.org/3/library/unittest.html
```

Look for:

- `assert`
- test case
- failure
- expected value
- actual value

For this course, plain `assert` is enough for many practice scripts.

A larger project often uses `unittest` or another test tool.

The idea stays the same:

```text
Name the behavior.
Run the check.
Change code.
Run the check again.
```

## Mini Challenge

Refactor a score function.

Create:

```text
day-96/scores.py
```

Start with this code:

```python
def score_message(score, attempts):
    if score >= 90:
        if attempts == 1:
            return "Excellent first try"
        else:
            return "Excellent"
    else:
        if score >= 70:
            if attempts <= 2:
                return "Good progress"
            else:
                return "Passed"
        else:
            return "Keep practicing"
```

Create:

```text
day-96/test_scores.py
```

Add:

```python
from scores import score_message


def test_score_messages():
    assert score_message(95, 1) == "Excellent first try"
    assert score_message(95, 3) == "Excellent"
    assert score_message(75, 2) == "Good progress"
    assert score_message(75, 4) == "Passed"
    assert score_message(50, 1) == "Keep practicing"


if __name__ == "__main__":
    test_score_messages()
    print("All score tests passed.")
```

Run:

```text
python test_scores.py
```

Then refactor `score_message()` so it is flatter:

```python
def score_message(score, attempts):
    if score >= 90 and attempts == 1:
        return "Excellent first try"

    if score >= 90:
        return "Excellent"

    if score >= 70 and attempts <= 2:
        return "Good progress"

    if score >= 70:
        return "Passed"

    return "Keep practicing"
```

Run the tests again.

You should see:

```text
All score tests passed.
```

The function now has the same behavior with less nesting.

## Real-World Use

Refactoring is part of normal programming.

Professional developers refactor when:

- a function has grown too large
- a rule is duplicated in several places
- a name no longer matches what the code does
- a project needs a new feature, but the old structure makes the feature hard
- tests are hard to write because the code mixes too many jobs

Tests make this work less risky.

For example, a receipt project might grow from:

```text
one file
one function
manual checks
```

into:

```text
receipt.py
discounts.py
taxes.py
formatting.py
tests
```

You would not usually make that jump all at once.

You would move one piece, run tests, move another piece, run tests, and keep going.

That habit also prepares you for the capstone.

In a capstone project, your first version may be messy because you are still discovering the problem.

That is okay.

Working first versions are allowed to be plain.

Tests and refactoring help you turn that first version into something easier to trust.

## Recap

Refactoring means improving code structure without changing behavior.

Tests help protect the behavior while you change the structure.

The beginner loop is:

```text
write tests
run tests
make one refactor
run tests again
repeat
```

You practiced these refactoring moves:

- extracting functions
- renaming variables
- simplifying conditionals
- removing duplication
- creating constants for repeated numbers
- keeping behavior the same before and after the change

The most important habit is not a special trick.

It is patience.

Make one clear change.

Run the tests.

Then make the next change.

## Lesson Checklist

Before moving on, make sure you can:

- explain refactoring in your own words
- explain the difference between a refactor and a feature change
- write tests before changing working code
- run the same tests before and after a refactor
- extract a helper function from repeated or crowded code
- rename variables to show meaning
- simplify nested `if` statements
- remove duplicated rules
- keep public function names stable when tests import them
- use failing tests as clues during a refactor
- describe why refactoring prepares code for larger projects

## Exercises

### Exercise 1: Explain The Word

In your own words, answer:

```text
What does refactoring mean?
```

Include this idea:

```text
The behavior should stay the same.
```

### Exercise 2: Sort The Changes

Label each change as either:

```text
refactor
feature
```

Changes:

```text
Rename `x` to `subtotal`.
Add a new coupon named FREESHIP.
Move tax math into `calculate_tax()`.
Change the tax rate from 8 percent to 9 percent.
Replace repeated money formatting with `format_money()`.
Add a new line to the receipt showing loyalty points.
```

### Exercise 3: Write Receipt Tests

Create:

```text
day-96/test_receipt.py
```

Write at least three tests for `make_receipt()`.

Include:

- regular customer without coupon
- member without coupon
- regular customer with `SAVE10`

Run the tests before you refactor.

### Exercise 4: Extract `calculate_subtotal()`

Move the subtotal loop into a new function:

```python
def calculate_subtotal(items):
    subtotal = 0

    for item in items:
        subtotal += item["price"] * item["quantity"]

    return subtotal
```

Update `make_receipt()` to use it.

Run the tests again.

### Exercise 5: Extract `calculate_discount()`

Move the discount rules into:

```python
def calculate_discount(subtotal, customer_kind, coupon_code):
    if coupon_code == "SAVE10":
        return subtotal * 0.10

    if customer_kind == "member":
        return subtotal * 0.05

    return 0
```

Run the receipt tests again.

### Exercise 6: Extract `format_money()`

Create:

```python
def format_money(amount):
    return f"${amount:.2f}"
```

Use it for subtotal, discount, tax, and total.

Run the tests again.

### Exercise 7: Rename For Meaning

Rewrite this code with clearer names:

```python
x = subtotal - discount
y = x * 0.08
z = x + y
```

Use:

```python
taxable_amount
tax
total
```

Then explain why the new names are easier to read.

### Exercise 8: Simplify A Conditional

Refactor this function:

```python
def shipping_message(total):
    if total >= 50:
        return "Free shipping"
    else:
        if total >= 25:
            return "Reduced shipping"
        else:
            return "Standard shipping"
```

Keep the same behavior, but remove the extra nesting.

Before changing it, write these checks:

```python
assert shipping_message(60) == "Free shipping"
assert shipping_message(30) == "Reduced shipping"
assert shipping_message(10) == "Standard shipping"
```

### Exercise 9: Add A Missing Test

The receipt tests check a regular customer with `SAVE10`.

Add a test for a member with `SAVE10`.

Decide what should happen:

```text
Should the coupon discount beat the member discount?
```

For today's code, the answer is yes.

The member should get 10 percent off, not 5 percent off.

### Exercise 10: Refactor One Older Program

Choose one small program from an earlier day.

Do not pick a huge one.

Find one function or section that could be clearer.

Write two or three tests for the current behavior.

Then make one refactor:

- extract a function
- rename unclear variables
- remove duplicated code
- simplify a conditional

Run the tests before and after.

Write one sentence:

```text
The behavior stayed the same because...
```

## Tiny Win

You practiced one of the skills that makes larger projects feel possible.

You do not have to choose between working code and readable code.

You can write a first version, protect its behavior with tests, and then improve the structure step by step.

That is a real project habit.

## Tomorrow

Tomorrow is:

```text
Day 97: Capstone Planning
```

You are close to the end of the 100-day course.

The next step is to plan a capstone project that uses several skills together:

- functions
- files
- command-line input
- project organization
- Git habits
- tests
- refactoring

Today matters because capstone projects rarely start perfectly organized.

On Day 97, you will choose a project idea, define a small first version, list the main functions and files, and decide what tests would prove the important behavior.

The goal will not be to build everything at once.

The goal will be to make a plan that gives you a clear first step.
