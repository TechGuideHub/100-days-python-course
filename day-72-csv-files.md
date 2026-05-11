# Day 72: CSV Files

**Focus:** Reading and writing table-shaped data with Python's `csv` module  
**You will practice:** rows, columns, headers, `csv.reader`, `csv.DictReader`, `csv.writer`, `newline=''`, delimiters, and small tracker files  
**Estimated time:** 50-65 minutes

## Today's Goal

Today you will learn how to work with CSV files.

CSV stands for:

```text
comma-separated values
```

A CSV file stores table-shaped data as plain text.

It is not fancy. It is not a spreadsheet app. It is just text arranged in rows and columns.

Example:

```text
title,author,pages
Matilda,Roald Dahl,240
The Hobbit,J. R. R. Tolkien,310
A Wrinkle in Time,Madeleine L'Engle,256
```

This looks simple because it is simple.

Each line is a row.

Each comma separates one column from the next.

By the end of this lesson, you should be able to:

- explain what a CSV file is
- recognize rows, columns, and headers
- read a CSV file with `csv.reader`
- read a CSV file with `csv.DictReader`
- write rows with `csv.writer`
- include a header row
- use `newline=''` when opening CSV files
- avoid common comma and delimiter mistakes
- build a small book or grade tracker
- understand why CSV comes before JSON in this course

Yesterday, paths helped you point Python at the right file.

Today, CSV helps Python understand the shape of the data inside that file.

Tomorrow, JSON will give you another file format for data that is less table-shaped.

## The Big Idea

A CSV file is useful when your data looks like a table.

Think about a small book tracker:

```text
title,author,pages
Matilda,Roald Dahl,240
The Hobbit,J. R. R. Tolkien,310
A Wrinkle in Time,Madeleine L'Engle,256
```

The first row is usually the header row.

It names the columns:

```text
title
author
pages
```

Every row after that is one record.

In this file:

```text
Matilda,Roald Dahl,240
```

the values are:

```text
title: Matilda
author: Roald Dahl
pages: 240
```

You could try to read CSV text by splitting every line on commas.

That works only for the easiest files.

Python gives you a better tool:

```python
import csv
```

The `csv` module understands common CSV rules, including quoted values and different delimiters.

That means this lesson is not really about inventing a file parser.

It is about using the right built-in tool.

## The Mental Model

Think of a CSV file like a notebook page with columns.

The file stores text like this:

```text
name,score
Mina,9
Sam,8
Iris,10
```

Python can read that text one row at a time.

With `csv.reader`, each row becomes a list:

```python
["Mina", "9"]
```

That means you use indexes:

```python
name = row[0]
score = row[1]
```

With `csv.DictReader`, each row becomes dictionary-like data:

```python
{"name": "Mina", "score": "9"}
```

That means you use column names:

```python
name = row["name"]
score = row["score"]
```

Both are useful.

Use `csv.reader` when you want simple row lists.

Use `csv.DictReader` when the header names make your code easier to read.

One more habit matters when opening CSV files:

```python
newline=""
```

You will often see this described as `newline=''`.

Use it when opening CSV files, especially when writing them.

It helps Python and the `csv` module handle line breaks cleanly.

## Try It Yourself

Create a folder named:

```text
day-72
```

Today you will make two small files:

```text
day-72/books.csv
day-72/grades.csv
```

You can create them from Python, so you do not need to type the CSV by hand.

### Step 1: Write A Book CSV File

Create:

```text
day-72/write_books.py
```

Code:

```python
from pathlib import Path
import csv

folder = Path("day-72")
folder.mkdir(exist_ok=True)

books_path = folder / "books.csv"

with books_path.open("w", newline="") as file:
    writer = csv.writer(file)
    writer.writerow(["title", "author", "pages"])
    writer.writerow(["Matilda", "Roald Dahl", 240])
    writer.writerow(["The Hobbit", "J. R. R. Tolkien", 310])
    writer.writerow(["A Wrinkle in Time", "Madeleine L'Engle", 256])

print("Book file saved.")
```

Run it.

You should see:

```text
Book file saved.
```

Now open:

```text
day-72/books.csv
```

You should see something like:

```text
title,author,pages
Matilda,Roald Dahl,240
The Hobbit,J. R. R. Tolkien,310
A Wrinkle in Time,Madeleine L'Engle,256
```

The exact line endings may look slightly different depending on your editor.

The important part is the rows and columns.

This line creates a CSV writer:

```python
writer = csv.writer(file)
```

This line writes the header row:

```python
writer.writerow(["title", "author", "pages"])
```

Each line after that writes one book:

```python
writer.writerow(["Matilda", "Roald Dahl", 240])
```

The writer handles commas between values for you.

You give it a list.

It writes a CSV row.

### Step 2: Read Every Row With `csv.reader`

Create:

```text
day-72/read_books_rows.py
```

Code:

```python
from pathlib import Path
import csv

books_path = Path("day-72") / "books.csv"

with books_path.open(newline="") as file:
    reader = csv.reader(file)

    for row in reader:
        print(row)
```

Run it after `books.csv` exists.

You should see:

```text
['title', 'author', 'pages']
['Matilda', 'Roald Dahl', '240']
['The Hobbit', 'J. R. R. Tolkien', '310']
['A Wrinkle in Time', "Madeleine L'Engle", '256']
```

Notice two things.

First, every row is a list.

Second, even the page numbers are strings:

```python
'240'
```

CSV files store text.

If you want a number, convert it:

```python
pages = int(row[2])
```

### Step 3: Skip The Header Row

The header row is useful, but it is not a book.

Change your reading code to this:

```python
from pathlib import Path
import csv

books_path = Path("day-72") / "books.csv"

with books_path.open(newline="") as file:
    reader = csv.reader(file)
    headers = next(reader)

    print("Columns:", headers)

    for row in reader:
        title = row[0]
        pages = int(row[2])
        print(f"{title} has {pages} pages.")
```

You should see:

```text
Columns: ['title', 'author', 'pages']
Matilda has 240 pages.
The Hobbit has 310 pages.
A Wrinkle in Time has 256 pages.
```

This line reads one row before the loop starts:

```python
headers = next(reader)
```

After that, the loop continues from the next row.

That is why the header row is not printed as a book.

### Step 4: Read Rows With `csv.DictReader`

Create:

```text
day-72/read_books_dicts.py
```

Code:

```python
from pathlib import Path
import csv

books_path = Path("day-72") / "books.csv"

with books_path.open(newline="") as file:
    reader = csv.DictReader(file)

    for book in reader:
        title = book["title"]
        author = book["author"]
        pages = int(book["pages"])
        print(f"{title} by {author}: {pages} pages")
```

You should see:

```text
Matilda by Roald Dahl: 240 pages
The Hobbit by J. R. R. Tolkien: 310 pages
A Wrinkle in Time by Madeleine L'Engle: 256 pages
```

This version is easier to read:

```python
book["title"]
```

is clearer than:

```python
row[0]
```

That clarity depends on the header row.

If your CSV file has headers, `DictReader` is often a good beginner choice.

### Step 5: Append One More Book

You practiced append mode when writing text files.

The same file mode works here.

Create:

```text
day-72/add_book.py
```

Code:

```python
from pathlib import Path
import csv

books_path = Path("day-72") / "books.csv"

with books_path.open("a", newline="") as file:
    writer = csv.writer(file)
    writer.writerow(["Clean Code", "Robert C. Martin", 464])

print("Book added.")
```

Run it once.

Then read the file again with one of your reader programs.

You should see the extra book at the end.

Be careful with append mode.

If you run this program five times, it will add the same book five times.

That is not a Python bug.

That is exactly what append mode means.

### Step 6: Build A Small Grade Tracker

Create:

```text
day-72/grade_tracker.py
```

Code:

```python
from pathlib import Path
import csv

folder = Path("day-72")
folder.mkdir(exist_ok=True)

grades_path = folder / "grades.csv"

grades = [
    ["Mina", "CSV basics", 9],
    ["Sam", "CSV basics", 8],
    ["Iris", "CSV basics", 10],
]

with grades_path.open("w", newline="") as file:
    writer = csv.writer(file)
    writer.writerow(["name", "assignment", "score"])
    writer.writerows(grades)

total = 0
count = 0

with grades_path.open(newline="") as file:
    reader = csv.DictReader(file)

    for row in reader:
        score = int(row["score"])
        total += score
        count += 1
        print(f"{row['name']}: {score}")

average = total / count
print(f"Average score: {average:.1f}")
```

You should see:

```text
Mina: 9
Sam: 8
Iris: 10
Average score: 9.0
```

This program does three useful things:

- creates a CSV file
- reads the CSV file back
- calculates something from the data

That is a common pattern.

Many real programs save data first, then load it later for reporting, searching, or summaries.

## Common Mistake

A common mistake is treating every comma as a safe place to split text.

This looks tempting:

```python
line = "The Little Book, Revised,Mina Rao,120"
parts = line.split(",")
print(parts)
```

You should see:

```text
['The Little Book', ' Revised', 'Mina Rao', '120']
```

That result has four pieces.

But the book title was meant to be one value:

```text
The Little Book, Revised
```

CSV has a way to handle commas inside values.

It uses quotes:

```text
"The Little Book, Revised",Mina Rao,120
```

Use the `csv` module so Python understands that.

Code:

```python
import csv

line = '"The Little Book, Revised",Mina Rao,120'

reader = csv.reader([line])

for row in reader:
    print(row)
```

You should see:

```text
['The Little Book, Revised', 'Mina Rao', '120']
```

The comma inside the quoted title stayed inside the title.

That is one reason `csv.reader` is better than `.split(",")`.

Another common mistake is assuming every CSV-style file uses commas.

Some files use semicolons:

```text
name;score
Mina;9
Sam;8
```

For that kind of file, tell Python the delimiter:

```python
import csv

rows = [
    "name;score",
    "Mina;9",
    "Sam;8",
]

reader = csv.reader(rows, delimiter=";")

for row in reader:
    print(row)
```

You should see:

```text
['name', 'score']
['Mina', '9']
['Sam', '8']
```

The delimiter is the character that separates columns.

For normal CSV files, the delimiter is a comma.

For some exported files, it may be a semicolon or tab.

## Debug It

Here is a broken program.

It writes a CSV file, then tries to read it.

Broken code:

```python
from pathlib import Path
import csv

folder = Path("day-72")
folder.mkdir(exist_ok=True)

grades_path = folder / "grades.csv"

with grades_path.open("w") as file:
    writer = csv.writer(file)
    writer.writerow(["name", "score"])
    writer.writerow(["Mina", 9])

with grades_path.open() as file:
    reader = csv.reader(file)

    for row in reader:
        print(row["name"])
```

This code is broken because `csv.reader` gives you lists.

A list uses indexes:

```python
row[0]
```

It does not use column names:

```python
row["name"]
```

There is one more improvement to make.

When opening CSV files, include `newline=""`.

Fixed code:

```python
from pathlib import Path
import csv

folder = Path("day-72")
folder.mkdir(exist_ok=True)

grades_path = folder / "grades.csv"

with grades_path.open("w", newline="") as file:
    writer = csv.writer(file)
    writer.writerow(["name", "score"])
    writer.writerow(["Mina", 9])

with grades_path.open(newline="") as file:
    reader = csv.DictReader(file)

    for row in reader:
        print(row["name"])
```

You should see:

```text
Mina
```

The fix changed the reader:

```python
reader = csv.DictReader(file)
```

Now each row can be read by header name.

## Read the Docs

The Python documentation for `csv` is worth visiting when you need a reminder.

Look for these names:

```text
csv.reader
csv.writer
csv.DictReader
csv.DictWriter
```

You do not need to memorize every option.

For now, focus on these questions:

- Does the file have headers?
- What character separates the columns?
- Am I reading rows as lists or dictionaries?
- Do I need to convert text into numbers?
- Did I open the file with `newline=""`?

You can also ask Python for a quick reminder:

```python
import csv

print(csv.reader)
print(csv.DictReader)
print(csv.writer)
```

You should see information showing that these names come from the `csv` module.

It will not teach you the whole module, but it confirms that Python can find the tools.

## Mini Challenge

Build a tiny book tracker.

Create:

```text
day-72/book_tracker.py
```

Your program should:

- create `day-72/book_log.csv`
- write a header row with `title`, `status`, and `rating`
- write at least three books
- read the file back with `csv.DictReader`
- print only books with a rating of 4 or higher

Starter code:

```python
from pathlib import Path
import csv

folder = Path("day-72")
folder.mkdir(exist_ok=True)

log_path = folder / "book_log.csv"

books = [
    ["Matilda", "finished", 5],
    ["The Hobbit", "reading", 4],
    ["A Long Practice Book", "paused", 3],
]

with log_path.open("w", newline="") as file:
    writer = csv.writer(file)
    writer.writerow(["title", "status", "rating"])
    writer.writerows(books)

with log_path.open(newline="") as file:
    reader = csv.DictReader(file)

    for row in reader:
        rating = int(row["rating"])

        if rating >= 4:
            print(f"{row['title']}: {rating}/5")
```

You should see:

```text
Matilda: 5/5
The Hobbit: 4/5
```

After it works, change the data.

Add one more book.

Run the program again.

Check that the printed list changes.

## Real-World Use

CSV files are everywhere because they are simple.

You may see CSV files when you:

- export transactions from a finance app
- download student scores from a course tool
- move contact lists between apps
- save survey results
- collect product information
- prepare rows for a spreadsheet
- send simple reports between systems

CSV is good for table-shaped data:

```text
one row per thing
one column per detail
```

A grade tracker fits well:

```text
name,assignment,score
Mina,CSV basics,9
Sam,CSV basics,8
```

A book tracker fits well:

```text
title,status,rating
Matilda,finished,5
The Hobbit,reading,4
```

But not every kind of data fits CSV neatly.

Imagine a book that has:

- title
- author
- chapters
- notes for each chapter
- quotes
- reading dates

That data starts to feel nested.

CSV can become awkward there.

That is one reason tomorrow's format matters.

JSON is often better when data has lists inside dictionaries or dictionaries inside dictionaries.

## Recap

CSV files store rows and columns as plain text.

The first row often contains headers.

Use `csv.reader` when you want each row as a list.

Use `csv.DictReader` when your file has headers and you want to use column names.

Use `csv.writer` to write rows.

Use `writer.writerow(...)` for one row.

Use `writer.writerows(...)` for many rows.

Open CSV files with `newline=""`, especially when writing.

Do not rely on `.split(",")` for real CSV files.

Commas can appear inside quoted values.

Some files use a delimiter other than a comma.

## Lesson Checklist

- [ ] I can explain what CSV means.
- [ ] I can identify rows, columns, and headers.
- [ ] I can create a CSV file with `csv.writer`.
- [ ] I can write a header row.
- [ ] I can read rows with `csv.reader`.
- [ ] I can skip a header row with `next(reader)`.
- [ ] I can read rows with `csv.DictReader`.
- [ ] I can convert CSV text values into numbers.
- [ ] I know why `.split(",")` can break.
- [ ] I can use `delimiter=";"` when a file is not comma-separated.
- [ ] I can use `newline=""` when opening CSV files.

## Exercises

### Exercise 1: Create A People CSV

Create:

```text
day-72/people.py
```

Write a CSV file named:

```text
day-72/people.csv
```

The file should have these headers:

```text
name,city,age
```

Add at least three people.

Then open the CSV file in your editor and check the rows.

### Exercise 2: Read The People CSV

Create:

```text
day-72/read_people.py
```

Use `csv.reader` to print each row from `people.csv`.

Then change the program so it skips the header row and prints sentences like:

```text
Mina lives in Pune.
```

Use your own names and cities.

### Exercise 3: Use `DictReader`

Rewrite your people reader with `csv.DictReader`.

Use column names instead of indexes.

Your code should use:

```python
row["name"]
row["city"]
row["age"]
```

Convert `age` to an integer before comparing it.

Print only people who are 18 or older.

### Exercise 4: Track Practice Time

Create:

```text
day-72/practice_log.py
```

Write a CSV file with these columns:

```text
date,topic,minutes
```

Add at least four rows.

Read the file back and print the total number of practice minutes.

### Exercise 5: Find Long Books

Use `day-72/books.csv`.

Read the file with `csv.DictReader`.

Print only books with more than 300 pages.

Remember that `pages` starts as text.

Convert it with:

```python
int(row["pages"])
```

### Exercise 6: Add One Row

Create:

```text
day-72/add_grade.py
```

Open `day-72/grades.csv` in append mode.

Add one new grade row.

Then run your grade reader again.

Check that the new row appears.

### Exercise 7: Explain The Header Row

In your own words, answer these questions:

```text
What is a header row?
Why does DictReader need it?
When might you skip it?
```

Keep your answer short.

The goal is clarity, not a long paragraph.

### Exercise 8: Fix The Split Problem

This code gives the wrong number of columns:

```python
line = '"Tea, Large",drink,120'
print(line.split(","))
```

Rewrite it with `csv.reader`.

The result should keep `Tea, Large` as one value.

### Exercise 9: Try A Different Delimiter

Use this data:

```python
rows = [
    "item;price",
    "tea;120",
    "rice;250",
]
```

Read it with:

```python
csv.reader(rows, delimiter=";")
```

Print each row.

Then change the delimiter to a comma and run it again.

Explain what changed.

### Exercise 10: Choose The Reader

For each situation, choose `csv.reader` or `csv.DictReader`.

```text
The file has a header row and you want readable code.
The file has no header row.
You only need to print raw rows.
You want to use names like row["score"].
You are quickly checking what a file contains.
```

Write one sentence explaining your favorite choice.

## Tiny Win

You can now move data between Python and spreadsheet-style files.

That is a practical skill.

Small programs can now save rows, read them later, and calculate useful summaries.

Even better, you learned when not to parse text by hand.

Using the `csv` module is the cleaner habit.

## Tomorrow

Tomorrow is:

```text
Day 73: JSON Files
```

CSV is great for flat tables.

JSON is better when data has more shape.

For example, a book can have a title, a list of chapters, and notes for each chapter.

That kind of nested data is awkward in CSV.

Tomorrow you will learn how Python reads and writes JSON so your programs can save richer data.
