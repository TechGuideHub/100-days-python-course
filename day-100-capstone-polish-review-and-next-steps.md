# Day 100: Capstone Polish, Review, and Next Steps

**Focus:** Turning your capstone into a project you can trust, explain, and keep improving  
**You will practice:** reviewing a finished project, manual testing, fixing rough edges, improving `README.md`, checking `requirements.txt`, cleaning project files, making a Git snapshot, reflecting on progress, and choosing a next learning path  
**Estimated time:** 70-90 minutes

## Today's Goal

Today you will do the last pass on your capstone project.

This is not a day for adding a large new feature.

It is a day for making the project clearer, calmer, and easier to run.

By the end of today, you should be able to:

- review a project from the point of view of a new user
- run a manual test pass through the main workflow
- notice and fix small rough edges
- update `README.md` so another person can run the project
- check that `requirements.txt` matches the packages the project actually uses
- remove temporary files, debug prints, and unused notes
- make a final Git commit for the course version of the project
- write a short reflection on what you learned
- choose a next path after this course

The goal is not to make the capstone perfect.

The goal is to make it honest:

```text
It runs.
It explains itself.
It has a clear current version.
It gives you a next step.
```

That is enough for a serious beginner project.

## The Big Idea

Finishing a project is a skill.

Many beginners stop when the code works once.

That is understandable. Getting the program to work at all can take real effort.

But a useful project needs a final pass after the first working version.

During this pass, you ask:

- Can I run it from a fresh terminal?
- Does the main workflow still work?
- What happens when the user types something unexpected?
- Are the file names clear?
- Is the README accurate?
- Are the requirements accurate?
- Is there anything private, temporary, or confusing in the folder?
- Did I save a Git commit before moving on?

This is the difference between:

```text
I got it to work once.
```

and:

```text
I know what I built, I know how to run it, and I can improve it later.
```

That second sentence is the habit you are practicing today.

## The Mental Model

Think of today's work as four passes over the same project.

```text
Pass 1: User pass
  Run the project like someone who has never seen it before.

Pass 2: Code pass
  Read the files and fix small problems.

Pass 3: Project pass
  Check README, requirements, file names, and cleanup.

Pass 4: Snapshot pass
  Save the final course version with Git.
```

Do not try to do everything at once.

If you test, test.

If you edit the README, edit the README.

If you clean up files, clean up files.

Mixing all of those jobs together makes it easier to miss something.

The simple order is:

```text
Run it.
Review it.
Polish it.
Document it.
Clean it.
Commit it.
Reflect on it.
Choose what comes next.
```

That is today's map.

## Start With A Fresh Run

Open your capstone project and run it from the command line.

Use the same command that a reader would use.

For a simple project, that might be:

```text
python main.py
```

or:

```text
python capstone/main.py
```

If your README says a different command, use the README command.

That is the point.

The README should match reality.

As you run the project, take notes in a small file such as:

```text
day-100/review_notes.md
```

Your notes can be plain and short:

```text
- README says to run app.py, but the real file is main.py.
- Menu option 3 works.
- Empty input on the name prompt looks strange.
- requirements.txt lists rich, but the project does not import it.
- There is still a debug print in storage.py.
```

You are not judging the project.

You are collecting facts.

Facts are easier to fix than a vague feeling that the project is messy.

## Manual Testing

Manual testing means using the project yourself and checking the behavior.

You are not writing automated tests today unless your capstone already has them.

You are acting like a careful user.

For a command-line project, test at least these paths:

```text
start the program
read the first screen or menu
try the main successful workflow
try a second normal workflow
try an invalid choice
try empty input where it matters
try quitting
run the program again if it saves data
```

For each test, write down:

```text
What I did
What happened
Whether that result is okay
```

Example manual test notes:

```text
Test: Add a new task
Steps: Choose 1, type "study dictionaries", press Enter.
Result: Task appears in the list.
Status: Good.

Test: Choose an invalid menu option
Steps: Type 99 at the menu.
Result: Program says "Invalid choice" and shows the menu again.
Status: Good.

Test: Add an empty task
Steps: Choose 1, press Enter without typing a task.
Result: Blank task is saved.
Status: Needs fix.
```

Manual testing is not fancy.

It is careful attention.

That attention catches many beginner bugs.

## A Small Manual Test Helper

If your project has a few pure functions, you can also make a tiny check script.

A pure function is a function that can be called with normal values and checked without typing into `input()`.

For example, suppose your capstone has this function:

```python
def clean_task(text):
    return text.strip()
```

You could check it with:

```python
def clean_task(text):
    return text.strip()


checks = [
    ("  study Python  ", "study Python"),
    ("", ""),
    ("   ", ""),
]

for original, wanted in checks:
    result = clean_task(original)

    if result == wanted:
        print(f"PASS: {original!r}")
    else:
        print(f"FAIL: {original!r} gave {result!r}, wanted {wanted!r}")
```

You should see:

```text
PASS: '  study Python  '
PASS: ''
PASS: '   '
```

This is not a replacement for proper tests.

It is a bridge between manual testing and automated testing.

It lets you check a small piece of behavior without clicking through the whole program or typing into menus.

## Fixing Rough Edges

A rough edge is not always a crash.

Sometimes the program technically works, but it is confusing or unpleasant to use.

Common capstone rough edges:

- a menu option does not match what the code actually does
- an error message is too vague
- empty input creates strange data
- saved data appears in the wrong place
- a file has an old name from an earlier idea
- there are debug prints mixed with normal output
- the project has unused functions from experiments
- the README explains yesterday's version, not today's version

Fix small rough edges before adding anything new.

Good polish work:

```text
Change "Done" to "Task saved."
Reject an empty task name.
Rename helper2.py to storage.py.
Remove a print used only for debugging.
Update the README run command.
Delete an unused sample file.
```

Risky polish work:

```text
Rewrite the whole project.
Add a login system.
Switch storage formats.
Install a new package for one small display change.
Rename every file without a reason.
```

Today is a closing pass.

Keep the changes small enough that you can test them.

## Improving User Input

Many beginner projects become better when they handle input gently.

For example, this function rejects empty names:

```python
def clean_name(name):
    cleaned = name.strip()

    if cleaned == "":
        return None

    return cleaned
```

A short check:

```python
def clean_name(name):
    cleaned = name.strip()

    if cleaned == "":
        return None

    return cleaned


print(clean_name("  Ada  "))
print(clean_name(""))
print(clean_name("   "))
```

You should see:

```text
Ada
None
None
```

That tiny function gives the rest of the program a clear rule:

```text
Real text becomes cleaned text.
Blank text becomes None.
```

Then the menu code can respond:

```python
def clean_name(name):
    cleaned = name.strip()

    if cleaned == "":
        return None

    return cleaned


user_text = "  Ada  "
name = clean_name(user_text)

if name is None:
    print("Please enter a name.")
else:
    print(f"Saved {name}.")
```

Small helper functions like this often make a capstone feel more stable.

## README Review

Your `README.md` is the front door of the project.

It does not need to be long.

It needs to be accurate.

A beginner-friendly README should answer:

- What is this project?
- What does it do?
- What version of Python does it use, if that matters?
- How do I install any needed packages?
- How do I run it?
- What are the main files?
- Where is saved data stored, if the project saves data?
- What is one limitation or future improvement?

A useful README shape:

````md
# Task Tracker

A command-line app for saving and listing small tasks.

## How To Run

```text
python main.py
```

## Requirements

This project uses only the Python standard library.

## Files

- `main.py` starts the program.
- `tasks.py` contains task rules.
- `storage.py` loads and saves task data.
- `data/tasks.json` stores saved tasks.

## Notes

The project currently runs in the terminal.
Future improvements could include due dates, search, or automated tests.
````

Make sure your README does not promise features that are not built.

Simple and true is better than impressive and inaccurate.

## Requirements Review

The `requirements.txt` file should list third-party packages.

It should not list standard library modules.

Usually do not list these:

```text
json
csv
pathlib
datetime
random
statistics
sqlite3
tkinter
```

Those come with Python.

If your project imports a third-party package, it may belong in `requirements.txt`.

Examples:

```text
requests
rich
pytest
flask
pandas
```

If your capstone uses no third-party packages, your `requirements.txt` can say:

```text
# This project currently uses only the Python standard library.
```

Check your imports.

For each import, ask:

```text
Did this come with Python, or did I install it with pip?
```

If you installed it with `pip`, it probably belongs in `requirements.txt`.

If it came with Python, it usually does not.

## Project Cleanup

Before the final commit, clean the folder.

You are looking for files that do not belong in the project history.

Usually keep:

```text
main.py
helper modules
README.md
requirements.txt
tests/
small example data
.gitignore
```

Usually remove or ignore:

```text
__pycache__/
*.pyc
.pytest_cache/
*.tmp
*.log
old scratch files
debug output files
large generated files
private notes
files with real passwords or API keys
```

Be careful with data files.

Some data belongs in the project:

```text
data/sample_tasks.json
data/example_inventory.json
```

Some data should stay private:

```text
data/my_real_passwords.json
data/private_clients.csv
```

If a file contains personal information, passwords, tokens, or private records, do not commit it.

Use a small example file instead.

## `.gitignore` Review

A Python capstone should usually have a `.gitignore`.

A solid beginner version is:

```text
.venv/
__pycache__/
*.pyc
.pytest_cache/
.coverage
htmlcov/
*.tmp
*.log
.env
```

Read each line as a project boundary:

```text
Keep environments out.
Keep caches out.
Keep temporary files out.
Keep private settings out.
```

If your project creates a local database, a private data file, or generated reports, decide whether those files should be committed.

Do not guess.

Ask:

```text
Would another person need this exact file to understand or run the project?
Does this file contain private information?
Can the program recreate this file?
Is this file huge compared with the code?
```

Those questions usually make the decision clearer.

## Git Snapshot

After the project runs, the README is accurate, and the folder is clean, make a Git snapshot.

Start by checking what changed:

```text
git status
```

Read the list carefully.

You should understand every file shown.

Then stage the final capstone files:

```text
git add main.py README.md requirements.txt .gitignore
```

Your project may have different files, so adjust the command.

For example:

```text
git add main.py tasks.py storage.py data/sample_tasks.json README.md requirements.txt .gitignore
```

Check again:

```text
git status
```

If the staged list looks right, commit:

```text
git commit -m "Polish capstone project"
```

Then read the recent history:

```text
git log --oneline
```

The exact commit message can be different.

Good final-course commit messages:

```text
Polish capstone project
Update capstone README and cleanup files
Finalize task tracker course version
Prepare capstone for review
```

Avoid:

```text
final
done
stuff
last last
```

Future you deserves a clearer note.

## User Testing

If possible, ask one person to try the project.

This does not need to be formal.

Give them only the README and the project folder.

Ask them to:

- run the project
- complete the main workflow
- tell you where they got confused
- tell you what worked
- tell you what they expected to happen when something did not

Do not explain everything while they test.

Watch where the README is unclear.

Watch where the program output is unclear.

Watch where they type something you did not expect.

One user test can reveal more than another hour of staring at the code.

If no one is available, do a pretend-new-user pass yourself:

```text
Close the editor.
Open the README.
Follow only the README.
Do not use memory.
Write down anything missing.
```

That can still catch real problems.

## Reflection Without Drama

A final reflection is not a speech.

It is a short note that helps you see your own progress.

Create or update:

```text
day-100/review_notes.md
```

Answer these questions:

- What can this project do now?
- What was the hardest part to build?
- What bug taught you something useful?
- Which part of the code is clearest?
- Which part would you improve next?
- What Python idea feels more comfortable than it did earlier?
- What still feels confusing?
- What kind of project do you want to build next?

Keep the answers practical.

Example:

```text
The hardest part was saving and loading JSON without losing the existing data.
The clearest part is tasks.py because the functions have small jobs.
The next improvement would be automated tests for adding and completing tasks.
I still need more practice with imports and project layout.
```

This kind of note is useful because it gives your next study session a starting point.

## Choosing Your Next Path

After this course, do not try to study everything at once.

Pick one direction for the next few weeks.

Here are five good beginner paths.

### Path 1: Web Apps

Choose this if you want to build projects people use in a browser.

Study next:

- HTML basics
- CSS basics
- how web requests work
- Flask or Django
- templates
- forms
- simple databases

Starter project ideas:

```text
personal notes app
habit tracker
recipe collection
small booking form
portfolio project page
```

### Path 2: Automation

Choose this if you like saving time and working with files.

Study next:

- `pathlib`
- CSV files
- Excel files
- PDFs
- command-line arguments
- scheduled scripts
- error logging

Starter project ideas:

```text
rename a folder of files
sort downloads by type
combine CSV reports
send yourself a summary email
clean repeated spreadsheet rows
```

### Path 3: Data

Choose this if you like patterns, tables, charts, and questions.

Study next:

- CSV review
- `pandas`
- data cleaning
- grouping and filtering
- charts
- notebooks
- careful data storytelling

Starter project ideas:

```text
personal spending summary
movie ratings analysis
weather history chart
study time report
sales or inventory summary
```

### Path 4: APIs

Choose this if you like connecting your program to other services.

Study next:

- HTTP basics
- JSON review
- `requests`
- API keys
- rate limits
- error handling
- saving API results

Starter project ideas:

```text
weather lookup tool
movie search app
currency converter
GitHub profile summary
book search helper
```

### Path 5: Testing And Code Quality

Choose this if you want to make your projects easier to trust.

Study next:

- `pytest`
- test cases
- fixtures
- edge cases
- refactoring
- type hints
- docstrings

Starter project ideas:

```text
add tests to your capstone
test a calculator module
test a text cleanup module
test JSON loading and saving
refactor one older course project
```

There is no single correct next path.

The best next path is the one that makes you build again soon.

## Try It Yourself

Use this order for today's capstone pass.

### Step 1: Open The Project

Find your capstone folder.

Do not edit anything yet.

Read the file names and remind yourself what each file does.

### Step 2: Run The Project

Run the command from the README.

If there is no README command, write down that problem.

Then run the project using the command you believe is correct.

### Step 3: Make Manual Test Notes

Create:

```text
day-100/review_notes.md
```

Write at least five test notes:

```text
Test:
Steps:
Result:
Status:
```

At least one test should use invalid or empty input.

### Step 4: Fix Three Small Things

Choose three small fixes.

Good choices:

```text
clearer menu text
better empty input handling
removed debug print
README command corrected
unused file removed
requirements.txt corrected
```

Do not choose a full rewrite.

### Step 5: Review The README

Make sure it includes:

- project name
- short description
- run command
- requirements note
- main file list
- saved data note, if needed
- one future improvement

### Step 6: Review Requirements

Open `requirements.txt`.

Check whether each listed package is really used.

Add missing third-party packages.

Remove standard library modules.

If there are no third-party packages, say so in the file.

### Step 7: Clean The Folder

Remove or ignore cache files, temporary files, logs, and private files.

Check `.gitignore`.

Make sure `.venv/`, `__pycache__/`, and `.env` are not being committed.

### Step 8: Make A Git Commit

Use:

```text
git status
git add ...
git status
git commit -m "Polish capstone project"
git log --oneline
```

Do not use `git add ...` literally.

Replace it with the files that belong in your project snapshot.

### Step 9: Write A Short Reflection

At the bottom of your review notes, add:

```text
What I built:
What I fixed today:
What I understand better now:
What I want to study next:
```

Keep it specific.

## Common Mistake

The common mistake on a final project day is trying to make the project impressive instead of making it dependable.

Impressive is tempting.

Dependable is more useful.

### Mistake 1: Adding A Big Feature At The End

Problem:

```text
The project works, so I will add a large new feature before finishing.
```

Risk:

```text
The new feature creates new bugs, and there is no time left to polish the project.
```

Better:

```text
Write the feature idea in the README or review notes as a future improvement.
Commit the stable version first.
```

### Mistake 2: Trusting One Successful Run

Problem:

```text
The project worked once with perfect input.
```

Risk:

```text
The project may fail when input is blank, data is missing, or the user chooses the wrong menu option.
```

Better:

```text
Test the normal path and at least two uncomfortable paths.
```

### Mistake 3: Leaving The README Behind

Problem:

```text
The code changed, but the README still describes an older version.
```

Risk:

```text
Another person cannot run the project, and future you may not remember the correct command.
```

Better:

```text
Run the project using only the README instructions.
Update anything that is wrong.
```

### Mistake 4: Committing Local Junk

Problem:

```text
The commit includes cache folders, logs, test output, or private files.
```

Risk:

```text
The project history becomes noisy or unsafe.
```

Better:

```text
Check git status carefully.
Use .gitignore.
Only commit files that belong to the project.
```

### Mistake 5: Calling It Done Without A Snapshot

Problem:

```text
The final version exists only as unsaved working folder changes.
```

Risk:

```text
You can lose track of which version was the finished course version.
```

Better:

```text
Make one clear Git commit after the final review pass.
```

## Debug It

Use these situations to practice final-day thinking.

### Problem 1: The README Command Fails

README says:

```text
python app.py
```

But the real starter file is:

```text
main.py
```

What to fix:

```text
Update the README command to match the real project.
```

Then run the README command again.

### Problem 2: Blank Input Creates Bad Data

The user presses Enter at a name prompt.

The project saves:

```text
""
```

or creates a blank item in a list.

What to fix:

```text
Strip the input.
Check whether it is empty.
Show a helpful message instead of saving it.
```

### Problem 3: requirements.txt Lists The Wrong Things

The file says:

```text
json
pathlib
requests
```

But the project imports only:

```python
import json
from pathlib import Path
```

What to fix:

```text
Remove json and pathlib because they come with Python.
Remove requests unless the project really imports and uses it.
```

If no third-party packages are used, the file can say:

```text
# This project currently uses only the Python standard library.
```

### Problem 4: Git Status Shows Cache Files

`git status` shows:

```text
__pycache__/
```

What to fix:

```text
Add __pycache__/ to .gitignore.
Do not stage the cache folder.
```

Cache files are created by Python.

They are not part of the project source code.

### Problem 5: The Program Works Only From One Folder

The project runs when you are inside the project folder, but fails from the folder above it.

Likely cause:

```text
The code may depend on the current terminal location.
```

What to check:

```text
File paths for saved data.
README run command.
Whether storage code uses a stable path based on the file location.
```

For many beginner projects, using `Path(__file__).parent` in storage code can help the program find files beside the script.

## Read the Docs

Today, documentation reading should support your capstone.

Choose one question that matters to your project.

Examples:

```text
How does pathlib build file paths?
How does json.dump differ from json.dumps?
How does argparse read command-line arguments?
How does pytest name test files?
How does requests handle a failed API call?
```

Read only enough to answer the question.

Then write two notes:

```text
What I learned:
Where I used it or might use it:
```

Documentation is easier to read when you arrive with a job.

Do not read randomly for hours.

Use the docs to make one project decision clearer.

## Mini Challenge

Make a one-page capstone review report.

Put it in:

```text
day-100/review_notes.md
```

Use this structure:

```text
# Capstone Review

## Project Summary

## Manual Tests

## Fixes Made

## Files Checked

## Git Snapshot

## Next Step
```

Under `Manual Tests`, include at least five tests.

Under `Fixes Made`, include at least three small improvements.

Under `Files Checked`, mention:

```text
README.md
requirements.txt
.gitignore
main project files
```

Under `Git Snapshot`, write the commit message you used.

Under `Next Step`, choose one path:

```text
web
automation
data
APIs
testing
```

## Real-World Use

Professional developers do final passes all the time.

Before sharing work, they often check:

- Does the app start?
- Does the main workflow work?
- Are setup instructions current?
- Are dependencies listed correctly?
- Are temporary files excluded?
- Are secrets kept out?
- Is there a clear commit?
- Is there a short note about what changed?

The tools may become more advanced later.

You might use automated tests, code formatters, continuous integration, pull requests, issue trackers, deployment checks, and code review.

But the habit underneath is the same:

```text
Check the work before you hand it to someone else.
Make the project explain itself.
Save a clean point in history.
```

You practiced that habit today.

## Recap

Today you polished your capstone project.

You reviewed it as a user, not only as the person who wrote the code.

You practiced manual testing:

```text
normal input
invalid input
empty input
quitting
saved data
```

You looked for rough edges:

```text
unclear messages
old README instructions
debug prints
unused files
wrong requirements
missing .gitignore entries
```

You checked the project files:

```text
README.md
requirements.txt
.gitignore
source files
data files
```

You made or planned a final Git snapshot:

```text
git status
git add
git commit
git log --oneline
```

You also chose a next direction:

```text
web
automation
data
APIs
testing
```

That is a complete final course day.

Not because the project is perfect.

Because it is reviewable, explainable, and ready for the next version.

## Lesson Checklist

Before moving on, make sure you can:

- [ ] run your capstone from the command line
- [ ] test the main workflow manually
- [ ] test at least one invalid input
- [ ] test at least one empty input
- [ ] write clear manual test notes
- [ ] fix a small rough edge without rewriting the project
- [ ] update `README.md` with the correct run command
- [ ] explain what belongs in `requirements.txt`
- [ ] remove or ignore temporary files
- [ ] explain why secrets should not be committed
- [ ] read `git status` before committing
- [ ] make a clear final capstone commit
- [ ] describe one thing you learned from the project
- [ ] choose one next learning path

## Exercises

### Exercise 1: Run From The README

Open your capstone README.

Follow only the instructions in the README.

Answer:

- Did the project run?
- Was any step missing?
- Was any command wrong?
- What did you update?

### Exercise 2: Write Five Manual Tests

Write five manual test notes for your capstone.

Use this format:

```text
Test:
Steps:
Result:
Status:
```

Include:

- one normal workflow
- one invalid menu choice or invalid value
- one empty input
- one quit or exit path
- one saved-data check, if your project saves data

### Exercise 3: Improve One Error Message

Find one confusing message in your project.

Replace it with a clearer one.

For example:

```text
Bad:
Error

Better:
Please enter a number from 1 to 4.
```

Run the project again and trigger that message on purpose.

### Exercise 4: Check requirements.txt

Open your Python files and list every import.

Separate them into two groups:

```text
standard library
third-party
```

Then update `requirements.txt`.

Do not list standard library modules.

### Exercise 5: Check .gitignore

Open `.gitignore`.

Make sure it handles common Python project files:

```text
.venv/
__pycache__/
*.pyc
.pytest_cache/
*.tmp
*.log
.env
```

Then run:

```text
git status
```

Check whether any cache, temporary, or private files still appear.

### Exercise 6: Clean One File

Pick one source file from your capstone.

Look for:

- old comments that no longer help
- debug prints
- unused functions
- unclear names
- repeated code that could be one helper

Make one small improvement.

Run the project after the change.

### Exercise 7: Make The Final Commit

After testing and cleanup, make a final course commit.

Use a clear message such as:

```text
Polish capstone project
```

Then run:

```text
git log --oneline
```

Write down the latest commit message in your review notes.

### Exercise 8: Write A Project Summary

In five to eight sentences, explain your capstone.

Include:

- what it does
- who it is for
- how to run it
- what files matter most
- what you would improve next

This summary can help you talk about the project later.

### Exercise 9: Choose One Next Path

Choose one:

```text
web
automation
data
APIs
testing
```

Write:

```text
I choose:
Because:
My first next project will be:
The first skill I need to learn is:
```

Keep it realistic.

A small next project is better than a giant idea that never starts.

### Exercise 10: Revisit An Early Lesson

Open one project or exercise from the first half of the course.

Notice what looks different to you now.

Write three notes:

```text
What I understand now:
What I would write differently:
What still looks useful:
```

This is a good way to see progress without exaggerating it.

## Tiny Win

You now have a way to finish a beginner Python project.

Not just by stopping.

By checking it, explaining it, cleaning it, and saving a clear version.

That is a practical skill you can reuse on every project after this course.

## Tomorrow

There is no Day 101 in this course.

Tomorrow can be the first day of your next path.

Choose one small action:

```text
Web: build a tiny Flask page.
Automation: write a script that organizes one folder.
Data: load one CSV file and summarize it.
APIs: call one public API and print one useful result.
Testing: add three pytest tests to your capstone.
```

Keep the first step small enough to finish.

The next project does not need to prove everything.

It only needs to keep you building.
