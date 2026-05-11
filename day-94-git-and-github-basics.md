# Day 94: Git and GitHub Basics

**Focus:** Saving a useful history of your Python project  
**You will practice:** version control, `git init`, `git status`, `git add`, `git commit`, `git log`, `.gitignore`, commit messages, GitHub remotes, the idea of pushing, and choosing what not to commit  
**Estimated time:** 55-70 minutes

## Today's Goal

Today you will learn the basic Git workflow.

Git is a version control tool.

Version control means your project can keep a history of meaningful changes instead of becoming a pile of almost-finished folders:

```text
project-final/
project-final-real/
project-final-real-fixed/
project-final-real-fixed-2/
```

Git lets you keep one project folder and save snapshots as the project changes.

By the end of today, you should be able to:

- explain why version control is useful
- explain the difference between Git and GitHub
- create a local Git repository with `git init`
- check what changed with `git status`
- choose files for the next snapshot with `git add`
- save a snapshot with `git commit`
- read recent history with `git log`
- create a simple `.gitignore`
- explain why `.venv`, temporary files, secrets, and generated files should not be committed
- understand what a GitHub remote is
- understand what pushing means without needing to push anything today
- write clear beginner-friendly commit messages
- prepare for Day 95, where tests will make project changes easier to trust

This lesson is not about becoming a Git expert in one day.

It is about learning the small set of commands that make project history less scary.

## The Big Idea

Git saves snapshots of your project.

A snapshot is called a commit.

Each commit should represent one clear step:

```text
Create quiz question data
Add scoring function
Handle invalid menu choice
Fix typo in welcome message
```

A project with commits has a memory.

That matters because code changes often happen in small experiments:

```text
What if I rename this function?
What if I split this file?
What if I add tests tomorrow?
What if this change breaks something?
```

Without version control, you may be afraid to change working code.

With version control, you can make a clear snapshot before you try something new.

The most common beginner workflow is:

```text
git status
git add file_name.py
git commit -m "Describe the change"
git log
```

Read that as:

```text
Check what changed.
Choose what belongs in the next snapshot.
Save the snapshot with a message.
Look at the history.
```

That is the core loop.

## The Mental Model

Think of Git as having three main areas.

```text
working folder
  files you are editing now

staging area
  changes chosen for the next commit

repository history
  saved commits
```

The commands move changes through those areas:

```text
edit files
  |
  | git add
  v
staging area
  |
  | git commit
  v
repository history
```

The working folder is where your files live:

```text
day-94/
  notes.py
  README.md
```

The staging area is Git's waiting room for the next commit.

The repository history is where committed snapshots live.

This is why `git add` does not save the snapshot by itself.

`git add` only says:

```text
I want this change included in the next commit.
```

`git commit` says:

```text
Save the chosen changes as a new snapshot.
```

That split feels strange at first, but it gives you control.

You can edit three files and commit only two of them if the third file is not ready.

## Git And GitHub

Git and GitHub are related, but they are not the same thing.

Git is the tool that tracks project history.

GitHub is a website that can store a copy of a Git repository online.

You can use Git without GitHub.

For example, this is a local Git repository:

```text
day-94/
  .git/
  app.py
  README.md
```

The `.git` folder is where Git stores the project's history.

You normally do not edit `.git` by hand.

GitHub becomes useful when you want to:

- back up a project online
- share code with another person
- show a project in a portfolio
- work with others on the same project
- review changes before merging them

Today, you do not need a GitHub account.

You only need to understand the idea:

```text
local repository
  your project on your computer

remote repository
  another copy of the project somewhere else, often GitHub
```

A remote is a saved address for another repository.

The most common remote name is:

```text
origin
```

That name usually means:

```text
the main online copy of this project
```

## Starting A Repository With `git init`

To make Git start tracking a project, you use:

```text
git init
```

Use it inside the project folder you want to track.

For example, imagine this folder:

```text
day-94/
  app.py
  README.md
```

If you run:

```text
git init
```

Git creates a hidden folder:

```text
day-94/
  .git/
  app.py
  README.md
```

The `.git` folder stores the repository history and settings.

The project is now a local Git repository.

Important habit:

```text
Run git init once for a project.
```

You do not run it every day.

You run it when a folder becomes a Git project.

### Where To Run Commands

Git commands care about where your terminal is.

If your project is:

```text
day-94/
  app.py
  README.md
```

move into:

```text
day-94/
```

Then run Git commands there.

If you run Git commands from the wrong folder, Git may say it cannot find a repository.

That error usually means:

```text
You are not inside a Git project folder.
```

## Checking Changes With `git status`

The most useful Git command for beginners is:

```text
git status
```

Use it often.

It answers questions like:

- Is this folder a Git repository?
- Which files changed?
- Which files are new?
- Which files are staged?
- Is there anything to commit?

At the start of a new repository, you might see files listed as untracked.

Untracked means:

```text
Git sees the file, but it is not part of the repository history yet.
```

For example:

```text
Untracked files:
  app.py
  README.md
```

That does not mean the files are wrong.

It means Git is waiting for you to choose whether they should be tracked.

After you commit everything, `git status` may say there is nothing to commit.

That means:

```text
The working folder matches the latest saved snapshot.
```

## Choosing Files With `git add`

To include a file in the next commit, use:

```text
git add app.py
```

That stages `app.py`.

Staged means:

```text
chosen for the next commit
```

You can stage more than one file:

```text
git add app.py
git add README.md
```

You can also stage the current folder:

```text
git add .
```

That means:

```text
Stage changes under the current folder.
```

`git add .` is common, but do not use it blindly.

First run:

```text
git status
```

Check the list.

Then stage files only when they really belong in the next commit.

For beginners, this is a careful habit:

```text
git status
git add app.py
git status
```

The second `git status` helps you see what changed after staging.

## Saving A Snapshot With `git commit`

After staging changes, save them with:

```text
git commit -m "Add first version of app"
```

The `-m` means:

```text
message
```

The text inside quotes is the commit message.

A commit message should finish this sentence:

```text
This commit will...
```

Good messages:

```text
Add contact search function
Create README with setup notes
Ignore virtual environment files
Fix total calculation for empty cart
```

Weak messages:

```text
update
stuff
changes
final
fix
```

Short is fine.

Vague is not helpful.

When you read history later, the message should remind you what changed and why the change mattered.

### One Change Per Commit

A good commit is usually one related idea.

For example:

```text
Commit 1: Add price formatting helper
Commit 2: Use helper in receipt output
Commit 3: Add receipt examples to README
```

That is easier to understand than:

```text
Commit 1: Update project
```

You do not have to be perfect.

Just try to avoid mixing unrelated work:

```text
Add login menu, rewrite calculator, rename files, and edit notes
```

That commit would be hard to understand later.

## Reading History With `git log`

To see commits, use:

```text
git log
```

Git shows commit history with details such as:

```text
commit 1a2b3c4d...
Author: Your Name
Date:   ...

    Add first version of app
```

The long code after `commit` is a commit id.

It uniquely identifies a snapshot.

You do not need to memorize it.

For a shorter view, many developers use:

```text
git log --oneline
```

That gives a compact list like:

```text
1a2b3c4 Add first version of app
8e9f101 Create README
```

For today, the important idea is:

```text
git log shows the saved history.
```

## Ignoring Files With `.gitignore`

Not every file belongs in Git.

A `.gitignore` file tells Git which files and folders to ignore.

The file is named exactly:

```text
.gitignore
```

The dot at the start matters.

For a beginner Python project, a useful `.gitignore` can start like this:

```text
.venv/
__pycache__/
*.pyc
.pytest_cache/
.coverage
htmlcov/
*.tmp
*.log
temp/
```

This says:

```text
Do not commit the virtual environment.
Do not commit Python cache files.
Do not commit test cache or coverage output.
Do not commit temporary files.
Do not commit log files.
```

The `.venv/` line is especially important.

A virtual environment can contain many installed package files.

Those files can be large.

They also belong to one computer's setup, not to the project source code.

Commit this instead:

```text
requirements.txt
```

Do not commit this:

```text
.venv/
```

That way, another person can recreate the environment with the package list instead of downloading your entire local environment folder.

### What `.gitignore` Does Not Do

`.gitignore` prevents new ignored files from being tracked.

It does not magically remove files that were already committed.

So the best time to create `.gitignore` is early in the project.

A good beginner order is:

```text
Create project folder.
Create .gitignore.
Create README.md.
Create app.py.
Run git init.
Check git status.
Stage and commit the project files.
```

The exact order can vary, but the habit is useful:

```text
Think about what should not be committed before the first commit.
```

## What Not To Commit

Commit source files, notes, tests, and small project data that belong to the project.

Be careful with files that are private, generated, huge, or specific to your computer.

Usually commit:

```text
app.py
helpers.py
README.md
requirements.txt
tests/
small example data files
```

Usually do not commit:

```text
.venv/
__pycache__/
*.pyc
*.tmp
*.log
.pytest_cache/
htmlcov/
secret keys
password files
large downloads
personal notes that do not belong to the project
```

Secrets deserve special care.

A secret is anything that gives access to an account or service:

```text
API keys
passwords
private tokens
database connection strings
```

If you commit a secret and push it to GitHub, you should treat that secret as exposed.

Changing the Git history later does not guarantee the secret is safe.

The safer habit is:

```text
Never commit secrets.
```

Use example files instead:

```text
.env.example
```

An example file can show the names of settings without real values:

```text
API_KEY=put-your-key-here
```

The real private file might be:

```text
.env
```

And `.gitignore` should include:

```text
.env
```

## GitHub Remotes

A local repository lives on your computer.

A remote repository lives somewhere else.

GitHub is a common place for remote repositories.

When a local repository is connected to a GitHub repository, Git stores a remote name and address.

The command often looks like:

```text
git remote add origin https://github.com/account/project-name.git
```

You do not need to run that today.

Just read it:

```text
git remote add
```

means:

```text
Save a new remote connection.
```

```text
origin
```

is the remote's short name.

```text
https://github.com/account/project-name.git
```

is the remote repository address.

The exact address depends on the GitHub account and project name.

This course will not use a real account name in examples.

The concept matters more than the specific URL today.

## The Push Concept

After you have local commits, pushing sends those commits to a remote repository.

The command often looks like:

```text
git push -u origin main
```

Read it as:

```text
Send my local commits to the remote named origin.
Use the main branch.
Remember this connection for future pushes.
```

The `-u` part sets an upstream relationship.

That means future pushes can often be shorter:

```text
git push
```

Again, you do not need to push today.

For today, remember this direction:

```text
commit
  save changes locally

push
  send local commits to a remote copy
```

Commit first.

Push after.

GitHub cannot receive work that has not been committed yet.

## Try It Yourself

This practice is written so you can read and reason about the commands without needing a live GitHub account.

Create a practice folder in your normal course work area:

```text
day-94/
```

Inside it, imagine these files:

```text
day-94/
  README.md
  notes.py
  .gitignore
```

### Step 1: Write A README

Create:

```text
day-94/README.md
```

Add a short project note:

```text
# Git Practice

This folder is for practicing Git command reading.
```

### Step 2: Write A Small Python File

Create:

```text
day-94/notes.py
```

Add:

```python
def summarize_note(note):
    return note.strip().capitalize()


print(summarize_note("  practice git carefully  "))
```

If you run the file with Python, you should see:

```text
Practice git carefully
```

### Step 3: Create `.gitignore`

Create:

```text
day-94/.gitignore
```

Add:

```text
.venv/
__pycache__/
*.pyc
.pytest_cache/
*.tmp
*.log
temp/
```

This tells Git to ignore local environment files, cache files, and temporary files.

### Step 4: Read The Init Command

The command for starting Git in the project would be:

```text
git init
```

You would run it from inside:

```text
day-94/
```

Afterward, the project would contain a hidden `.git` folder.

### Step 5: Read The Status Command

The command for checking the project state would be:

```text
git status
```

At this point, Git would likely show these files as new:

```text
README.md
notes.py
.gitignore
```

### Step 6: Read The Add Commands

To stage one file:

```text
git add notes.py
```

To stage the project files you created:

```text
git add README.md
git add notes.py
git add .gitignore
```

To stage all current folder changes:

```text
git add .
```

For practice, explain which version you would choose and why.

### Step 7: Read The Commit Command

A good first commit command would be:

```text
git commit -m "Create Git practice project"
```

That message is specific enough to be useful later.

It says what the commit does.

### Step 8: Read The Log Command

After committing, the history command would be:

```text
git log --oneline
```

You would expect to see a short commit id and your message:

```text
1a2b3c4 Create Git practice project
```

The exact id would be different.

## Common Mistake

Beginners usually do not make one Git mistake.

They make a small chain of understandable mistakes.

### Mistake 1: Running Commands In The Wrong Folder

Problem:

```text
git status
```

shows an error because the terminal is not inside the project repository.

Fix:

```text
Move into the project folder first.
```

For this lesson, that folder is:

```text
day-94/
```

### Mistake 2: Forgetting To Stage Before Committing

Problem:

```text
git commit -m "Add notes file"
```

does not commit anything because no changes were staged.

Fix:

```text
git status
git add notes.py
git status
git commit -m "Add notes file"
```

The second status check helps you confirm the file is staged.

### Mistake 3: Committing `.venv`

Problem:

```text
.venv/
```

appears in the list of files to commit.

Fix:

Add this to `.gitignore`:

```text
.venv/
```

Then check status again.

The virtual environment should not be part of the project history.

### Mistake 4: Using Vague Commit Messages

Problem:

```text
git commit -m "stuff"
```

Fix:

```text
git commit -m "Add note formatting helper"
```

Future you should be able to skim the log and understand the project story.

### Mistake 5: Thinking GitHub Saves Unsaved Local Work

GitHub stores commits that you push.

It does not automatically save every file on your computer.

The order is:

```text
edit files
git add
git commit
git push
```

If you skip the commit, there is nothing new to push.

## Debug It

Read each situation and decide what the learner should check.

### Problem 1: Git Says There Is No Repository

Message:

```text
fatal: not a git repository
```

Likely cause:

```text
The terminal is not inside a folder that has been initialized with Git.
```

What to check:

```text
Am I inside day-94/?
Has git init been run for this project?
```

### Problem 2: A File Is Untracked

Status says:

```text
Untracked files:
  notes.py
```

Meaning:

```text
Git sees notes.py, but it is not part of the repository history yet.
```

Possible next command:

```text
git add notes.py
```

Then commit when the staged changes look right.

### Problem 3: Nothing Happens When Committing

Status says:

```text
nothing to commit
```

Meaning:

```text
There are no staged changes waiting to be saved.
```

Possible reasons:

- you already committed the latest changes
- you forgot to save the file in your editor
- you forgot to run `git add`
- the file is ignored by `.gitignore`

The next useful command is:

```text
git status
```

### Problem 4: The Wrong File Is Staged

Imagine this staged list:

```text
README.md
debug.log
```

The `debug.log` file probably should not be committed.

What should you do conceptually?

```text
Unstage debug.log.
Add *.log to .gitignore.
Commit README.md and .gitignore if they are ready.
```

Today you only need the concept.

The important lesson is not to commit temporary log files just because they appeared.

### Problem 5: GitHub Has No New Code

Someone says:

```text
I edited the files, but GitHub did not change.
```

Questions to ask:

- Did you stage the changes?
- Did you commit the changes?
- Did you push the commits to the remote?
- Are you looking at the correct repository and branch?

The main idea:

```text
GitHub receives commits, not random unsaved editor changes.
```

## Read the Docs

Today, documentation reading means learning to recognize command shapes.

You do not need to memorize every option.

Look at these command patterns:

```text
git init
git status
git add README.md
git commit -m "Create README"
git log --oneline
```

Ask these questions:

- What is the main Git command?
- Does it need a file name?
- Does it save history, or only show information?
- Does it affect the local repository or a remote repository?

For example:

```text
git status
```

shows information.

It does not save a snapshot.

```text
git commit -m "Create README"
```

saves a snapshot of staged changes.

```text
git push
```

sends committed work to a remote.

When reading Git documentation, start with the job you want done:

```text
start tracking this project
check what changed
choose files for a commit
save a commit
read commit history
send commits to a remote
```

Then connect the job to the command.

## Mini Challenge

Write a command plan for a small project.

Do not use a real GitHub account for this challenge.

Just write the commands and a short note beside each one.

Scenario:

```text
You created day-94/todo.py.
You created day-94/README.md.
You created day-94/.gitignore.
You want to save the first project snapshot.
```

Your plan should include:

```text
git init
git status
git add
git commit
git log
```

One possible answer:

```text
git init
Start Git history for this folder.

git status
Check which files are new.

git add README.md
Choose README.md for the first commit.

git add todo.py
Choose todo.py for the first commit.

git add .gitignore
Choose .gitignore for the first commit.

git status
Confirm the right files are staged.

git commit -m "Create todo practice project"
Save the first project snapshot.

git log --oneline
Check that the commit appears in history.
```

Now improve it by adding one sentence:

```text
I did not commit .venv because environments should be recreated, not stored in Git.
```

## Real-World Use

Git becomes more valuable as projects get less linear.

In a beginner script, you may write a few lines and run the file.

In a larger project, you may:

- rename a function
- add a new file
- update a README
- install a package
- create a test
- change old code so the test passes
- remove a print statement used for debugging

Those changes should not all blend together.

Git helps you make a clear trail:

```text
Create project structure
Add file loading helper
Add tests for file loading
Fix missing-file error message
Update README setup notes
```

This also prepares you for tests.

Tomorrow, you will start learning how tests help you check that code still works after a change.

Git and tests work well together:

```text
Git tells you what changed.
Tests tell you whether behavior still works.
```

When both habits are present, you can edit with more confidence.

## Recap

Git tracks project history.

GitHub can store a remote copy of a Git repository online.

The beginner workflow is:

```text
git status
git add file_name.py
git commit -m "Describe the change"
git log --oneline
```

`git init` starts Git in a project folder.

`git status` shows what changed.

`git add` stages changes for the next commit.

`git commit` saves staged changes as a snapshot.

`git log` shows commit history.

`.gitignore` tells Git which files to ignore.

For Python projects, a useful `.gitignore` often includes:

```text
.venv/
__pycache__/
*.pyc
.pytest_cache/
*.tmp
*.log
```

Do not commit secrets, passwords, local virtual environments, caches, temporary files, or large generated outputs.

Commit messages should be clear enough to help you understand the history later.

## Lesson Checklist

Before moving on, make sure you can:

- explain version control in your own words
- explain that Git is local history and GitHub can host a remote copy
- describe what `git init` does
- describe what `git status` shows
- explain the difference between unstaged and staged changes
- explain why `git add` comes before `git commit`
- write a specific commit message
- explain why `.venv/` belongs in `.gitignore`
- list at least three things that should not be committed
- explain that pushing sends commits to a remote repository

## Exercises

### Exercise 1: Explain Version Control

In your own words, answer:

```text
What problem does version control solve?
```

Keep the answer to two or three sentences.

Include the idea of saving project history.

### Exercise 2: Match The Command To The Job

Match each command to its job:

```text
git init
git status
git add app.py
git commit -m "Add app"
git log --oneline
```

Jobs:

```text
Start Git in this folder.
Check what changed.
Choose app.py for the next commit.
Save the staged changes.
Show a short history.
```

### Exercise 3: Write A `.gitignore`

Create a `.gitignore` plan for a Python project.

It should include:

```text
.venv/
__pycache__/
*.pyc
.pytest_cache/
*.tmp
*.log
```

Then write one sentence explaining why `.venv/` should not be committed.

### Exercise 4: Improve The Commit Messages

Rewrite these weak messages:

```text
update
fix
stuff
final changes
```

Make them specific.

Possible improved versions:

```text
Add menu loop for todo app
Fix total when cart is empty
Create README setup instructions
Remove temporary debug output
```

### Exercise 5: Choose What To Commit

You have these files:

```text
app.py
README.md
requirements.txt
.venv/
debug.log
secret_key.txt
tests/test_app.py
__pycache__/
```

Write two lists:

```text
commit
do not commit
```

One reasonable answer:

```text
commit:
app.py
README.md
requirements.txt
tests/test_app.py

do not commit:
.venv/
debug.log
secret_key.txt
__pycache__/
```

Then explain why `secret_key.txt` is risky.

### Exercise 6: Read A Status Story

Imagine `git status` says:

```text
Changes to be committed:
  new file: README.md

Untracked files:
  notes.py
```

Answer:

- Which file is staged?
- Which file is untracked?
- If you commit right now, which file will be included?
- What command would stage `notes.py`?

### Exercise 7: Explain Local And Remote

Answer these questions:

```text
What is a local repository?
What is a remote repository?
Why might GitHub be useful?
What does pushing send?
```

Keep each answer short.

### Exercise 8: Prepare For Day 95

Tomorrow you will start learning about tests.

Write a short note answering:

```text
Why would Git be useful before changing code to add tests?
```

Your answer should include these ideas:

- Git records what changed
- a commit can mark the working version before an experiment
- tests help check behavior after the change

## Tiny Win

You now know the basic shape of a professional project habit:

```text
check what changed
choose the right files
save a clear commit
keep private and generated files out of history
```

That habit is small, but it changes how coding feels.

You are no longer just editing one fragile folder.

You are building a project with memory.

## Tomorrow

Tomorrow is:

```text
Day 95: Introduction To Tests
```

You will learn why tests exist, how they describe expected behavior, and how they make code changes less risky.

Today's Git lesson gives you the other half of that safety net:

```text
Git records the change.
Tests check the behavior.
```
