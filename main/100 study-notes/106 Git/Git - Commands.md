---
created: 2022-06-08 19:22
updated: 2022-06-09 00:00
---
---
**Links**: [[106 Git Index]]

---
## Staging
- `git add` : stage the changes
	- `git add <file-name>`
	- `git add .` : 
	- `git add -A` : to stage all the changes

### Discarding local changes (before staging) (tracked)
- `git restore` : **discard the changes before staging**. It only works if the files have been tracked previously.
	- `git restore .`
	- `git restore <file-name>`
- In older versions of git it was `git checkout -- <file-name>`. For more info read [[Git - Staging & Committing#Discarding local changes unstaged|Discarding local changes unstaged]]

### Discarding local changes (untracked)
- *If the file isn't tracked by git, it's not git's job to remove it*. Just use normal shell commands, like `rm` instead of `git rm`.
- If you want to delete **all** untracked files, you could do a `git clean`. 
- `git clean -n` : Dry run files
- `git clean -nd` : Dry run files and folders
- `git clean -f` : Remove untracked files
- `git clean -fd` : Remove untracked files and folders
- `git clean -fx` : To remove ignored and non ignored files

### Cancel Staged changes (before committing)
- `git restore --staged <file-name>` : Unstage the changes, i.e. remove them from the staging area.
- `git reset HEAD <file-name>` : older way of doing it.
- `git reset .`


## Committing
- `git commit` : open editor for typing the commit messages

## History
- `git log`
- `git log --pretty=oneline`
- `git log --pretty=format:"%h %ad | %s%d [%an]" --graph --date=short` : most useful.

### Checking out older versions
- `git checkout <hash>`

## Tagging
- Generally used for **tagging versions**.
- `git tag <tag-name>` : to tag a specific commit
- If you want to *tag older commits* for reference and easy jumping then `git checkout <hash>`, `git tag <tag-name>`
	- We can easily jump between commits using tag-names `git checkout <tag-name>`
- `git tag`: to list all the tags