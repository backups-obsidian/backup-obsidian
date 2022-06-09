---
created: 2022-06-08 19:12
updated: 2022-06-08 23:33
---
---
**Links**: [[106 Git Index]]

---
## Why do we have a staging area?
-  A staging step in git allows you to continue making changes to the working directory, and *when you decide you wanna interact with version control, it allows you to record changes in small commits*.
- Suppose you have edited three files (`a.html`, `b.html`, and `c.html`). After that you need to commit all the changes so that the changes to `a.html` and `b.html` were a single commit, while the changes to `c.html` were not logically associated with the first two files and were done in a separate commit.

```bash
git add a.html
git add b.html
git commit -m "Changes for a and b"
```
```bash
git add c.html
git commit -m "Unrelated change to c"
```

> [!note]- Separating staging and committing, you get the chance to easily **customise what goes into a commit**.

## Git tracks the changes and not files
- Git concentrates on the **changes to a file, not the file itself**.
- A `git add file` command does not tell git to add the file to the repository, but to note the current state of the file for it to be committed later.

### Example:
- Suppose you have a file name `hello.html` you make a *first change* and then do a `git add hello.html`
- Now you make a second change in `hello.html`. 
- Now if you do a `git status` you will see the following
```bash
# On branch master
# Changes to be committed:
#   (use "git reset HEAD <file>..." to unstage)
#
#   modified:   hello.html
#
# Changes not staged for commit:
#   (use "git add <file>..." to update what will be committed)
#   (use "git checkout -- <file>..." to discard changes in working directory)
#
#   modified:   hello.html
```
- Note that `hello.html` is listed in the status twice. 
	- The first change is staged and ready for a commit. 
	- The second change is unstaged. 
	- If you were making a commit right now, second change would not have been saved to the repository.

## Checking out older versions
- When you checkout something you will be in *detached HEAD* state. You can look around, make experimental changes and commit them, and you can discard any commits you make in this state without impacting any branches by performing another checkout.
- If you want to create a new branch to retain commits you create, you may do so (now or later) by using `-b` with the checkout command again.
	- `git checkout -b new_branch_name`

## Discarding local changes (unstaged)
- `git restore` is a new command that has been introduced in Git 2.23 together with `git switch`. 
- Their purposes are to simplify and separate the use cases of `git checkout` that does too many things.
- `git checkout` can be used to switch branches (and also to create a new branch before switching to it). This functionality has been extracted into `git switch`.
	- `git switch` cannot be used to go to specific commits. This can only be done by `git checkout`
- `git checkout` can also be used to restore files to the state they were on a specified commit. This functionality has been extracted into `git restore`.
- Discarding local changes can still be performed by `git checkout` but the new commands are easier to use and less confusing.