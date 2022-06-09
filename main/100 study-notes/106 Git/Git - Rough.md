---
created: 2022-06-09 18:57
updated: 2022-06-09 22:19
---
---
**Links**: [[106 Git Index]]

---
- All you _need_ are `git checkout`, `git reset`, and `git revert`. These commands have been in Git all along.
- But `git checkout` has, in effect, two _modes of operation_. 
- One mode is **safe**: 
	- It won't accidentally destroy any unsaved work. 
- The other mode is **unsafe**: 
	- If you use it, and it tells Git to wipe out some unsaved file, Git assumes that (a) you knew it meant that and (b) you really did mean to wipe out your unsaved file, so Git immediately wipes out your unsaved file.
- This is not very friendly, so the Git folks finally—after years of users griping—split `git checkout` into two new commands.
	- `git switch`
	- `git restore`
- Git is really all about _commits_. 
	- Commits get stored _in_ the Git repository. 
	- The `git push` and `git fetch` commands transfer _commits_ whole commits, as an all-or-nothing deal to the other Git. 
	- You either have all of a commit, or you don't have it. 
- Each commit is numbered by its _hash ID_, which is unique to that one particular commit. 
	- It's actually **computed from what's in the commit**, which is how Git makes these numbers work across all Gits everywhere. 
	- This means that what is in the commit is frozen for all time: if you change anything, what you get is a new commit with a new number, and the old commit is still there, with its same old number.
- A _branch name_ holds the hash ID of one commit. This makes the branch name _find_ that commit, which in turn means two things:
    - that particular commit is the _tip commit_ of that branch; and
    - all commits leading up to and including that tip commit are _on_ that branch.
- Git Index and working tree:
	- They're separate from these but worth mentioning early, especially since the *index has three names*: Git sometimes calls it the _index_, sometimes calls it the _staging area_, and sometimes—rarely these days—calls it the _cache_. All three names refer to the same thing.

## Squashing in git
- Squashing in Git is *compressing all the commits to a single commit*. Squashing a commit many times or let say n time for n commits will squash it to a single commit.
	- ![[attachments/Pasted image 20220609221808.png]]