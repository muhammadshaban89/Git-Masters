 **real, practical example** of reverting a **merge commit** using the `-m` flag.  

---

#  **Scenario: A merge commit broke production**

Your history looks like this:

```
A --- B --- C ----------- F (main)
               \        /
                D --- E   (feature)
```

Commit **F** is a *merge commit* created when you merged the feature branch into `main`.

But after deploying, you discover the feature introduced bugs.

You want to **undo the merge**, but without deleting history or force‑pushing.

This is where:

```
git revert -m 1 <merge-commit-hash>
```

comes in.

---

#  Why `-m 1` is needed

A merge commit has **two parents**:

- **Parent 1** → the branch you merged *into* (usually `main`)
- **Parent 2** → the branch you merged *from* (the feature branch)

`-m 1` means:

> “Keep parent 1 (main) as the base, and undo the changes introduced by the merge.”

If you used `-m 2`, Git would try to keep the feature branch as the base — almost never what you want.

---

# **Real Example**

### Step 1 — Identify the merge commit

```
git log --oneline
```

You see something like:

```
f3c9abc Merge branch 'feature-login'
a1b2c3d Fix typo
...
```

The merge commit hash is:

```
f3c9abc
```

### Step 2 — Revert the merge commit

```
git revert -m 1 f3c9abc
```

### What happens now?

- Git creates a **new commit** that undoes everything introduced by the merge.
- The feature branch changes are removed from `main`.
- History remains intact.
- No force push is required.

### Step 3 — Push safely

```
git push
```

---

# **What the history looks like after revert**

```
A --- B --- C ----------- F ----------- R (HEAD)
               \        /
                D --- E
```

Where:

- **F** = original merge commit  
- **R** = new revert commit that undoes F  

The feature branch is still preserved in history, but its changes are removed from the active branch.

---

# **Why this is the safest way to undo a merge**

- No history rewriting  
- No force push  
- No breaking teammates’ clones  
- Clean audit trail  
- Production is restored safely  

---

#  Bonus Example — Reverting a merge that caused conflicts

If reverting causes conflicts:

```
git revert -m 1 f3c9abc
# resolve conflicts
git add .
git revert --continue
```

---

