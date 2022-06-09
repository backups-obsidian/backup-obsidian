---
created: 2022-06-09 22:14
updated: 2022-06-09 22:31
---
---
**Links**: [[106 Git Index]]

---
## Branching
- Branches in Git are incredibly lightweight as well. 
	- There is no storage / memory overhead with making many branches
- **Branches are simply pointers to a specific commit -- nothing more**. 
- This is why many Git enthusiasts chant the mantra:
> branch early, and branch often

> [!note] A branch essentially says **I want to include the work of this commit and all parent commits**

### Merging
Merging in Git creates a special commit that has two unique parents. A commit with two parents essentially means "I want to include all the work from this parent over here and this one over here, _and_ the set of all their parents."

> [!tip]+ In merge the (current branch : `branch-1`) `git merge branch-2`. This means make `branch-2` parent of `branch-1`.
> - Parent means behind
> - If making parent not possible then get me there.
> - `git merge my-parent` - for remembering

> Rebase is like make parent but not exactly at the same location preserve my commits
- Show difference

#### Example: Merging
- Initial state:
	- ![[attachments/Pasted image 20220609213233.png]]
- Merge `bugFix` into `main` 
	- Notice we are on the `main` branch
	- This essentially means make `bugFix` parent of `main`
	- `git merge bugFix`
	- ![[attachments/Pasted image 20220609213327.png]]
	- If `c3` was not there and main was at `c1` then it would have directly moved to `c2` if we did `git merge bugFix` from `main` : `main` says making `bugFix` parent not possible so get me there.
- `main` now points to a *commit that has two parents*. If you follow the arrows up the commit tree from `main`, you will hit every commit along the way to the root. 
- This means that `main` contains all the work in the repository now.
- Merging `main` to `bugFix`: making parent not possible get me there.
	- `git checkout bugFix; git merge main`
	- ![[attachments/Pasted image 20220609214112.png]]

#### Example : Simple Merge
- Initial state:
	- ![[attachments/Pasted image 20220609222826.png]]
- `git checkout main; git merge test`
	- ![[attachments/Pasted image 20220609222902.png]]
## Rebase
- The second way of **combining work between branches** is _rebasing._ 
- Rebasing essentially takes a set of commits, "copies" them, and plops them down somewhere else.
- The advantage of rebasing is that it can be used to *make a nice linear sequence of commits*. 
	- The commit log / history of the repository will be a lot cleaner if only rebasing is allowed.

### Example 1 : Rebase
- Initial state:
	- ![[attachments/Pasted image 20220609214541.png]]
	- we are on `bugFix`
- `git rebase main` : make `main` parent of `bugFix`
	- ![[attachments/Pasted image 20220609214611.png]]
- Rebasing from `main`
	- ![[attachments/Pasted image 20220609214754.png]]
- `git rebase bugFix` : making parent not possible, get me there.
	- ![[attachments/Pasted image 20220609214810.png]]
	- Since `main` was an ancestor of `bugFix`, git simply moved the `main` branch reference forward in history.

> [!caution] Notice that we have changed commits from `c2` to `c2'` and `c3` to `c3'` since Rebasing changes the commit history.

### Example 2 : Rebase
- Initial state:
	- ![[attachments/Pasted image 20220609222441.png]]
- `git checkout test; git rebase main`
	- ![[attachments/Pasted image 20220609222523.png]]
	- Note the dashes, your commit history has been changed

## HEAD
- **HEAD is the symbolic name for the currently checked out commit -- it's essentially what commit you're working on top of**.
- HEAD always points to the most recent commit which is reflected in the working tree. 
- *Most git commands which make changes to the working tree will start by changing HEAD*.
- **Detaching HEAD just means attaching it to a commit instead of a branch**. 
	- This is what it looks like beforehand: `HEAD -> main -> C1`
		- ![[attachments/Pasted image 20220609220909.png]]
	- And now it's: `HEAD -> C1`
		- ![[attachments/Pasted image 20220609220921.png]]
