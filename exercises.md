# Git Workshop Exercises

---

## Setup

Before starting the exercises:

1. Clone the repository if you haven't already:

```bash
git clone <repository-url>

```

2. Open the repository in your code editor.
3. Open the terminal in your code editor and make sure that you are in the repository directory.

3. Fetch all branches and commits from the remote repository to ensure you have all the needed branches for the exercises.

```bash
git fetch --all

```

---

## Part 1: Merge Conflicts

### Setup

Before starting the merge conflict exercises:

1. Check out the `main` branch and pull the latest changes.
2. Create a new branch named `your-name-feature` from `main`.

```bash
git checkout main
git pull
git checkout -b your-name-feature
```

### Exercise 1: Merge Conflict on a Single Line

**Description:**  
Practice resolving a merge conflict caused by two branches editing the same line.

**Instructions:**

1. Edit line 29 of `index.html`.
2. Commit your change.
3. Make sure the source branch `1-merge-conflict-line` is up to date.
4. Merge `1-merge-conflict-line` into your branch.
5. Resolve the conflict and commit.

Note: Each line starting with 'git' e.g. `git add .` is a different command, so you should run them one at a time in your terminal. Make sure to replace `your-name-feature` with the actual name of your branch.

```bash

# create your own branch from main if you haven't already
git checkout main
git pull
git checkout -b your-name-feature

# Do and commit your changes
git add .
git commit -m "Edit line 29"

# Make sure the merge source branch is up to date (this is optional if you already have the latest changes, but it's good practice to check)
git checkout 1-merge-conflict-line
git pull

# Merge the source branch into your feature branch
git checkout your-name-feature
git merge 1-merge-conflict-line

# Resolve the conflict, then commit
git add .
git commit -m "Resolve merge conflict"
```

> **Things to remember:**
> - Always pull the latest changes for the source branch before merging.
> - You cannot change branches if you have uncommitted changes. Make sure to commit (or stash) your changes before switching branches. (We are not learning about stashing but you can look it up if you want to know how to save uncommitted changes without committing them.)
> - Make sure your target (feature) branch is checked out before you run `git merge`.
> - After resolving conflicts, you need to stage the resolved files before committing.

---

### Exercise 2: Merge Conflict on Several Lines

**Description:**  
Practice resolving a merge conflict where two branches have made different edits to the same list.

**Instructions:**

1. Edit the list starting at line 37 in `index.html` — you can add, remove, or modify items.
2. Commit your change.
3. Merge branch `2-merge-conflict-list` into your branch.
4. Resolve the conflict and commit.

```bash
# Do and commit your changes
git add .
git commit -m "Edit list"

# Make sure the merge source branch is up to date (this is optional if you already have the latest changes, but it's good practice to check)
git checkout 2-merge-conflict-list
git pull

# Merge the source branch into your feature branch
git checkout your-name-feature
git merge 2-merge-conflict-list

# Resolve the conflict, then commit
git add .
git commit -m "Resolve merge conflict"
```

---

### Exercise 3: Merge Conflict Across the Whole File

**Description:**  
Practice resolving a merge conflict where both branches have made broader changes to the same file.

**Instructions:**

1. Edit anything you like in `index.html`.
2. Commit your change.
3. Merge branch `3-merge-conflict-file` into your branch.
4. Resolve the conflict and commit.

```bash
# Do and commit your changes
git add .
git commit -m "Edit index.html"

# Make sure the merge source branch is up to date (this is optional if you already have the latest changes, but it's good practice to check)
git checkout 3-merge-conflict-file
git pull

# Merge the source branch into your feature branch
git checkout your-name-feature
git merge 3-merge-conflict-file

# Resolve the conflict, then commit
git add .
git commit -m "Resolve merge conflict"
```

---

### Exercise 4: Push Your Branch and Open a Pull Request

**Description:**  
Practice pushing a branch to the remote repository and creating a pull request to merge it into `main`.

**Instructions:**

1. Push your feature branch to the remote repository.
2. Go to GitHub and open a pull request to merge your branch into `main`.

```bash
git push -u origin your-name-feature
```

---

### Further Exercises (at home)

- Edit `styles.css` and merge branch `4-merge-conflicts-html-css` into your branch to practice CSS merge conflicts.
- Merge branches `mc-extra-1` and `mc-extra-2` into your branch and resolve any conflicts in `index.html`.


- Create pull requests to merge your branches into `main` for extra pull request practice (you are free to merge it yourself, but make sure to resolve all conflicts before merging).

**Remember:** How to keep your branch up to date with the latest changes from `main`:

```bash
git checkout main
git pull

git checkout -b your-name-feature

git merge main
# or:
git rebase main

git push

```

---

## Part 2: Git History & Advanced Commands

### Setup

Check out the `5-git-history-alterations` branch and create your own branch from it, then push it to the remote.

```bash
git checkout 5-git-history-alterations
git checkout -b your-name-git-history
git push -u origin your-name-git-history
```

---

### Exercise 5: git revert

**Description:**  
`git revert` creates a new commit that undoes the changes from a previous commit, without altering the existing commit history. This makes it safe to use on shared branches like `main`.

**Instructions:**

1. Make a change to any file and commit it.
2. Use `git log` to find the hash of that commit.
3. Revert the commit using its hash.
4. Push your changes.

```bash
# Make and commit some changes
git add .
git commit -m "Make some changes"

# Find the hash of the commit you just made (--oneline gives a compact view, press q to exit)
git log 
# or:
git log --oneline

# Revert the commit using its hash
# Note: this will open a text editor for the revert commit message — save and exit to complete
git revert <commit-hash>

git push
```

---

### Exercise 6: git commit --amend

**Description:**  
`git commit --amend` lets you modify the most recent commit — useful for fixing a typo in the commit message or including a forgotten change. Because amend rewrites history, it requires a force push.

**Instructions:**

1. Make some changes to a file and commit them.
2. Amend the commit to update the commit message using your terminal's text editor.
3. Force push the amended commit. (Commands such as `git commit --amend` rewrite commit history, so you need to force push to update the remote branch. It's good practice to use `--force-with-lease` flag instead of just `--force` to avoid accidentally overwriting someone else's work.)

```bash
# Make some changes and commit
git add .
git commit -m "Some changes"

# Amend the most recent commit (opens text editor to edit the message)
git commit --amend

# You can edit the commit message if you want. Save and exit the editor.

# Try pushing the amended commit (this will fail because the history has been rewritten)
git push

# Force push to update the remote branch with the amended commit
git push --force-with-lease
```

**Tip:** When `git commit --amend` opens the text editor, save and exit without changing anything to keep the original message, or edit it as needed. See the [Terminal Text Editor Quick Reference](#terminal-text-editor-quick-reference) at the bottom of this file.

**Extra exercise at home:** If you want to amend without changing the commit message and opening the editor at all, use `git commit --amend --no-edit`.

---

### Exercise 7: git reset

**Description:**  
`git reset` moves the HEAD pointer back to a previous commit, effectively undoing one or more commits. The default mode (`--mixed` but you don't need to write this) keeps the changes in your working directory but unstages them, allowing you to make adjustments before recommitting.

**Note**: HEAD is a pointer that always points to the latest commit in your current branch. When you reset to a previous commit, you are moving the HEAD pointer back in history. This means that the commits that were ahead of the reset point will no longer be part of the branch's history.

Because reset rewrites history, it requires a force push.

**Instructions:**

1. Use `git log` to find the hash of a commit you want to reset to.
2. Reset to that commit (default mode).
3. Re-commit the changes if needed, then force push.

```bash
# Find the hash of the commit you want to reset to (--oneline gives a compact view, press q to exit)
git log
git log --oneline

# Reset to the chosen commit (mixed reset — keeps changes in working directory)
git reset <commit-hash>

# Re-commit the changes
git add .
git commit -m "Reset to previous commit"

# Force push the changes to the remote repository
git push --force-with-lease
```

**Extra exercises at home:** 
- Try using `git reset --soft <commit-hash>` to keep changes staged. See how it differs from the default mixed reset.
- Try using `git reset --hard <commit-hash>` to discard all the changes and commits after the specified commit. See how it differs from the default mixed reset. Be careful with this one, as it will delete any uncommitted changes permanently and cannot be undone. Discarded commits can be recovered using `git reflog`. 

---

### Exercise 8: git rebase

**Description:**  
`git rebase` moves your branch's commits on top of another branch, creating a cleaner, linear history. Unlike `git merge`, it rewrites commit history and requires a force push.

> **Remember:** Always use `git merge` when merging into `main`. Use `git rebase` only in your own feature branch.

**Instructions:**

1. Make sure `6-git-rebase` is up to date.
2. Rebase your branch onto `6-git-rebase`.
3. Resolve any conflicts that arise and continue the rebase.
4. Force push the rebased branch.

```bash
# Make sure you have the latest changes from the target branch
git checkout 6-git-rebase
git pull

# Switch back to your branch and start the rebase
git checkout your-name-git-history
git rebase 6-git-rebase

# If there are conflicts, resolve them then continue
git add .
git rebase --continue

# Push the rebased branch
git push --force-with-lease
```

**Note:** If you want to abort the rebase and return to the state before starting it, you can use `git rebase --abort`.

---

### Exercise 9: git cherry-pick

**Description:**  
`git cherry-pick` lets you apply the changes from a specific commit onto your current branch, without merging the entire source branch.

**Instructions:**

1. Find the hash of a commit from the `7-git-cherry-pick` branch.
2. Cherry-pick that commit onto your branch.
3. Resolve any conflicts if needed, then push.

```bash
# Find the hash of the commit you want to cherry-pick (--oneline gives a compact view, press q to exit)
git log --oneline 7-git-cherry-pick

# Cherry-pick the commit using its hash
git cherry-pick <commit-hash>

# If there are conflicts, resolve them and continue
git add .
git cherry-pick --continue

# Push your changes
git push
```

**Note:** If you want to abort the cherry-pick and return to the state before starting it, you can use `git cherry-pick --abort`.

---

### Exercise 10: git rebase -i (Interactive Rebase)

**Description:**  
Interactive rebase (`git rebase -i`) lets you edit, reorder, squash, or drop commits in your branch. It's useful for cleaning up your commit history before merging into `main`.

**Instructions:**

1. Use `git log` to review your recent commits.
2. Start an interactive rebase for the last 2 commits.
3. In the editor, change `pick` to `squash` (or `s`) for the second commit.
4. Edit the combined commit message when prompted, then save.
5. Force push the result.

```bash
# Review your recent commits (--oneline gives a compact view, press q to exit)
git log --oneline

# Start interactive rebase for the last 2 commits
git rebase -i HEAD~2
# or: 
git rebase -i <commit-hash>

# In the editor: change "pick" to "squash" for the second commit, save and exit
# Edit the combined commit message when prompted, save and exit

# Push the updated history
git push --force-with-lease
```

**Note:** If you want to abort the rebase and return to the state before starting it, you can use `git rebase --abort`.

**Extra exercise at home:** 
- Try using `git rebase -i` to drop a commit by changing `pick` to `drop` (or `d`) in the interactive rebase editor. This will remove the commit from your branch's history. Dropping commits can cause conflicts if the dropped commit is a dependency for later commits, so be prepared to resolve any conflicts that arise.
- Try using `git rebase -i` to edit a commit message by changing `pick` to `edit` (or `e`) for the commit you want to edit. This will pause the rebase process at that commit, allowing you to amend the commit message or make additional changes before continuing the rebase.
- Try using `git rebase -i` to reorder commits by changing the order of the lines in the interactive rebase editor. This will change the order of the commits in your branch's history. Reordering commits can cause conflicts if the commits depend on each other, so be prepared to resolve any conflicts that arise. See the [Git Rebase Interactive Mode Documentation](https://git-scm.com/docs/git-rebase#_interactive_mode) how to cut and paste lines in the interactive rebase editor to reorder commits.

---

### Exercise 11: git reflog

**Description:**  
`git reflog` records every movement of the HEAD pointer, including commits lost through `reset` or `rebase`. It's your safety net for recovering work that seems gone.

**Instructions:**

1. Run `git reflog` to view the history of HEAD movements.
2. Find the hash of a commit you previously reset or rebased away.
3. Create a new branch from that commit to recover it.
4. Push the recovered branch.

```bash
# View the reflog
git reflog

# Create a new branch from the recovered commit hash
git checkout -b recovered-commit <commit-hash>

# Push the recovered branch
git push -u origin recovered-commit
```


---

## Terminal Text Editor Quick Reference

Git opens a text editor for commands like `git commit --amend`, `git rebase -i`, and `git merge` (when writing a merge commit message). The default is usually **vim**, but it may be **nano** depending on your setup.

---

### Vim

Vim is a modal editor — it has separate modes for navigating and editing text.

| Action | Command |
|---|---|
| Enter insert mode (start typing) | `i` |
| Exit insert mode | `Esc` |
| Save and exit | `:wq` then `Enter` |
| Exit without saving | `:q!` then `Enter` |
| Save without exiting | `:w` then `Enter` |
| Move cursor | Arrow keys (or `h` `j` `k` `l`) |
| Delete current line | `dd` (in normal mode) |
| Paste (line you just deleted) | `p` (in normal mode) |
| Undo | `u` (in normal mode) |

**Typical workflow in vim:**
1. Vim opens — you are in **normal mode**.
2. Press `i` to enter **insert mode** and edit the text.
3. Press `Esc` to return to **normal mode**.
4. Type `:wq` and press `Enter` to save and exit.

> **Stuck in vim?** Press `Esc` a couple of times, then type `:q!` and hit `Enter` to exit without saving.

---

### Nano

Nano is simpler than vim — you can type immediately when it opens.

| Action | Command |
|---|---|
| Save (write out) | `Ctrl + O`, then `Enter` to confirm |
| Exit | `Ctrl + X` |
| Save and exit | `Ctrl + O` → `Enter` → `Ctrl + X` |
| Cut line | `Ctrl + K` |
| Paste | `Ctrl + U` |
| Search | `Ctrl + W` |

The available shortcuts are shown at the bottom of the nano window (`^` means `Ctrl`).

---

### Less (read-only pager)

`git log` and some other git commands open output in `less`, a read-only pager for scrolling through text. You cannot type or edit in less — press `q` to get back to the terminal.

> **Tip:** Use `git log --oneline` to get a compact one-line-per-commit view that is easier to read and less likely to fill the screen.
