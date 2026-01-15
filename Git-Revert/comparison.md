# Core Idea
- **`git reset` rewrites history**  
- **`git revert` adds a new commit to undo changes**

Reset = *time travel*  
Revert = *anti‑commit*

---

# Example Setup
Imagine your commit history looks like this:

```
A — B — C — D (HEAD)
```

Commit **D** is bad and you want to undo it.

---

#  1) Using `git reset` (rewrites history)

## Example: Undo last commit but keep changes unstaged
```
git reset HEAD~1
```

### Result:
- Commit **D** is removed from history  
- Your code changes from D remain in your working directory  
- They are **unstaged**

New history:

```
A — B — C (HEAD)
```

### When to use:
- You have NOT pushed yet  
- You want to edit or reorganize the changes  
- You want to rewrite history cleanly

### NOT safe for shared branches.

---

## Example: Undo last commit and delete changes
```
git reset --hard HEAD~1
```

### Result:
- Commit **D** is removed  
- All changes from D are deleted  
- Working directory is clean

History:

```
A — B — C (HEAD)
```

---

# 2) Using `git revert` (safe for shared branches)

## Example: Undo last commit safely
```
git revert HEAD
```

### Result:
- Commit **D** stays in history  
- Git creates a NEW commit **E** that undoes D

New history:

```
A — B — C — D — E (HEAD)
```

### When to use:
- Commit is already pushed  
- Other people may have pulled it  
- You want a clean audit trail  
- You want to avoid force‑push

---

#  Side‑by‑Side Comparison

| Feature | `git reset` | `git revert` |
|--------|--------------|--------------|
| Rewrites history | ✔️ Yes | ❌ No |
| Creates new commit | ❌ No | ✔️ Yes |
| Safe on shared branches | ❌ No | ✔️ Yes |
| Removes commit from history | ✔️ Yes | ❌ No |
| Undo changes | ✔️ Yes (by moving HEAD) | ✔️ Yes (via new commit) |
| Requires force push | Often | Never |
| Keeps audit trail | ❌ No | ✔️ Yes |

---

#  Real‑World Scenarios

## Scenario 1 — You made a mistake locally  
Use **reset**:

```
git reset --soft HEAD~1
git commit -m "Better message"
```

##  Scenario 2 — You pushed a bad commit to main  
Use **revert**:

```
git revert HEAD
git push
```

## Scenario 3 — You want to remove 3 commits before pushing  
Use **reset**:

```
git reset --hard HEAD~3
```

##  Scenario 4 — You want to undo a merge commit on a shared branch  
Use **revert**:

```
git revert -m 1 <merge-hash>
```

---

# Quick Mental Model

### `reset`  
> “Pretend the bad commit never happened.”

### `revert`  
> “Acknowledge the bad commit, but create a new commit that undoes it.”

---
