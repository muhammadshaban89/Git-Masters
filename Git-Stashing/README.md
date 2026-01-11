Git Stashing 
---------------
- **Git stashing** is a way to *temporarily save* your uncommitted changes without committing them.  
- It lets you switch branches, pull updates, or work on something else **without losing your work**.

Think of it as putting your changes in a safe “drawer” until you’re ready to use them again.

---

**What Git Stash Does?**

When you run `git stash`, Git:

- Saves your modified files  
- Saves your staged files  
- Restores your working directory to a clean state  
- Lets you switch branches safely  

Your changes are stored in a stack called the **stash list**.


**Most Useful Git Stash Commands**

**Save your changes**
```
git stash
```
**Save changes with a message**
```
git stash push -m "my work in progress"
```

**Show all stashes**
```
git stash list
```

**Apply the most recent stash**
```
git stash apply
```

**Apply and remove from stash list**
```
git stash pop
```

**Delete a specific stash**
```
git stash drop stash@{2}
```

**Clear all stashes**
```
git stash clear
```

---

**Example Workflow**

You’re working on `feature-x`, but you need to switch to `main` quickly:

```
git stash
git checkout main
```

Later, return to your work:

```
git checkout feature-x
git stash pop
```

Your changes come back exactly as they were.


**When to Use Git Stash**

Use stashing when:

- You want to switch branches but have uncommitted changes  
- You’re not ready to commit yet  
- You want to test something temporarily  
- You need to pull updates without merging your unfinished work


**Stash Only Specific Files**

**Method 1 — Directly specify the files**
```
git stash push path/to/file1 path/to/file2
```

Example:
```
git stash push src/app.js src/config.yaml
```

Only those files are stashed; everything else stays untouched.

**Method 2 — Stash only staged files**
Useful when you want full control:

```
git add file1 file2
git stash push --staged
```

This stashes only what you staged.

---

**Stash Untracked Files**

By default, Git **does NOT stash untracked files**.  

To include them:

- **Include untracked files**
```
git stash push -u
```

- In Git, “untracked files” are files in your working directory that Git is not monitoring yet.
-  They exist on disk, but they are not part of the repository, not staged, and not committed.

**Include untracked + ignored files**
```
git stash push -a
```

Flags:
- `-u` = include untracked  
- `-a` = include untracked + ignored  


**Stash With `--keep-index`**
This option is extremely useful when you want to test only the staged changes.

**What it does**

- Stashes **unstaged** changes  
- Keeps **staged** changes in your working directory  

**Command**
```
git stash push --keep-index
```

**Why it’s useful**

Imagine you staged a fix but still have messy work in the same file.  
You want to run tests only on the staged fix.

```
git add fix.js
git stash push --keep-index
```

Now:
- Your staged fix stays  
- All other changes disappear temporarily  
- You can test cleanly  

---

How Stashing Works Internally


**1. A stash is actually two commits**
When you run `git stash`, Git creates:

- One commit for **staged changes**  
- One commit for **unstaged changes**  

These are stored under:
```
refs/stash
```

**2. Stashes form a stack**
Each stash is stored like:
```
stash@{0}
stash@{1}
stash@{2}
```

**3. A stash is just a commit with a special message**
You can inspect it:
```
git show stash@{0}
```

**4. Applying a stash is a merge**
When you run:
```
git stash apply
```
Git performs a **three‑way merge** between:

- Your current working tree  
- The stash commit  
- The base commit  

Conflicts can happen just like a normal merge.

**5. `stash pop` = apply + delete**
```
git stash pop
```
is equivalent to:
```
git stash apply
git stash drop
```


**Quick Summary Table**

| Task | Command |
|------|---------|
| Stash specific files | `git stash push file1 file2` |
| Stash untracked files | `git stash push -u` |
| Stash all (tracked + untracked + ignored) | `git stash push -a` |
| Stash only unstaged changes | `git stash push --keep-index` |
| View stash list | `git stash list` |
| Apply stash | `git stash apply` |
| Apply + remove | `git stash pop` |




