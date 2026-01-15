What `git revert` actually does?
 ----------

- `git revert` **creates a new commit** that *undoes* the changes of a previous commit.

- It does **NOT** delete history.  
- It does **NOT** move HEAD backwards.  
- It does **NOT** rewrite commits.

This makes it **safe for shared branches** like `main`, `develop`, or production branches.

---
Why use `git revert` instead of `git reset`?
   ------
| Command | Behavior | Safe on shared branches |
|---------|----------|-------------------------|
| `git reset` | Rewrites history | ❌ No |
| `git revert` | Adds a new commit that undoes changes | ✔️ Yes |

---

Example 1 — Revert the last commit
---
You made a bad commit:

```
git commit -m "Breaks API"
```

To undo it safely:

```
git revert HEAD
```

Git opens your editor with a default message:

```
Revert "Breaks API"
```

After saving, your history looks like:

```
A — good commit
B — bad commit
C — revert of B   ← new commit that undoes B
```

The code is restored, and history stays intact.

---

Example 2 — Revert a specific commit by hash

---

Let’s say the commit hash is:

```
987abcd
```

Undo it:

```
git revert 987abcd
```

This creates a new commit that reverses the changes from that hash.

---

Example 3 — Revert multiple commits
---


Undo the last 3 commits:

```
git revert HEAD~3..HEAD
```

This creates **three new revert commits**, one for each original commit.

---

Example 4 — Revert a merge commit
---


This is common when a feature branch breaks production.

You need the `-m` flag to tell Git which parent to keep.

Example:

```
git revert -m 1 <merge-commit-hash>
```

- `-m 1` means: keep the first parent (usually the main branch)
- Git creates a new commit that undoes the merge

---

When should you use `git revert`?
---

Use revert when:

- You already pushed the commit  
- Other people may have pulled it  
- You want to undo something **without rewriting history**  
- You want a clean audit trail  
- You’re working on production or shared branches  

---

When should you NOT use revert?
---

Avoid revert when:

- You want to rewrite or clean up local commits  
- You haven’t pushed yet  
- You want to squash or reorganize commits  

In those cases, use:

- `git reset --soft`
- `git reset --mixed`
- `git commit --amend`
- `git rebase -i`

---

Quick summary
---


| Task | Best Command |
|------|--------------|
| Undo last commit (safe) | `git revert HEAD` |
| Undo specific commit | `git revert <hash>` |
| Undo merge commit | `git revert -m 1 <hash>` |
| Undo multiple commits | `git revert A..B` |
| Undo commit but rewrite history | `git reset` (unsafe on shared branches) |


