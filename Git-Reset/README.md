
Git-Reset:
-----------

- `git reset` is one of those commands that feels simple at first… until you realize it has **three different modes** and each one rewrites history in a different way.


**What `git reset` *really* does**

At its core, `git reset` moves **HEAD**, and optionally updates:
- the **index** (staging area)
- the **working directory**

Think of it as choosing how far back you want to rewind, and how destructive you want that rewind to be.

**The Three Modes**

1. **`git reset --soft <commit>`**
- Moves HEAD only  
- Keeps index and working directory untouched  
- Your changes stay staged  

**Use when:**  

You want to rewrite history but keep all changes staged for a new commit.

**Example:**  

You made a commit but want to rewrite the message or squash it.
```
git reset --soft HEAD~1
git commit -m "Better commit message"
```
2. **`git reset --mixed <commit>`** (default)

- Moves HEAD  
- Updates index  
- Leaves working directory unchanged  
- Your changes become *unstaged*  

**Use when:**  

You want to unstage files but keep the actual changes.

**Example:**  

You accidentally staged too many files:
```
git reset
```
(Equivalent to `git reset --mixed HEAD`)

3. **`git reset --hard <commit>`**
- Moves HEAD  
- Updates index  
- Updates working directory  
- **All uncommitted changes are lost**  

**Use when:**  
You want a clean slate and don’t care about losing local changes.

**Example:**  
```
git reset --hard HEAD~1
```

---

**Practical cheat sheet**

| Goal | Command |
|------|---------|
| Undo last commit but keep changes staged | `git reset --soft HEAD~1` |
| Undo last commit but keep changes unstaged | `git reset HEAD~1` |
| Unstage a file | `git reset <file>` |
| Throw away all local changes | `git reset --hard` |
| Reset branch to remote state | `git reset --hard origin/main` |

---
**Safety tip for real-world use**
  - Since you work with automation and shared repos:
  
**Never use `git reset --hard` on a branch others are using.**  
  - It rewrites history and will cause conflicts for everyone else.

------------
**How `git reset` interacts with `reflog`**

- Every time you move **HEAD**, Git records that movement in the **reflog**.

That includes:

- `git reset`
- `git checkout` / `git switch`
- `git commit`
- `git merge`
- `git rebase`
- `git pull` (because it moves HEAD)
- even `git stash`

So when you run:

```
git reset --hard HEAD~1
```

Git updates the branch pointer and HEAD, **but reflog keeps a record of where HEAD used to be**.

Example reflog snippet:

```
a1b2c3d HEAD@{0}: reset: moving to HEAD~1
f4e5d6a HEAD@{1}: commit: Add monitoring script
```

This means:

- Your commit is NOT gone  
- It’s just not referenced by any branch  
- Reflog still knows the exact commit hash  

This is why reflog is the ultimate safety net.

**Recovering from a bad reset**

This is the part every engineer should master.  
Let’s say you ran something destructive:

```
git reset --hard HEAD~3
```

…and suddenly realize you nuked work you needed.

**Step 1 — View the reflog**

```
git reflog
```

You’ll see something like:

```
abc1234 HEAD@{0}: reset: moving to HEAD~3
def5678 HEAD@{1}: commit: Add API integration
987abcd HEAD@{2}: commit: Fix DNS policy
654fedc HEAD@{3}: commit: Add cluster migration script
```

**Step 2 — Identify the commit you want to restore**

Let’s say you want `HEAD@{2}`.

**Step 3 — Reset back to it**

```
git reset --hard HEAD@{2}
```

Or using the commit hash:

```
git reset --hard 987abcd
```

Boom — your “lost” work is back.

**Recovering *specific* files after a bad reset**

- If you don’t want to reset the whole branch:

```
git checkout HEAD@{2} -- path/to/file
```

This restores just that file from the old commit.

**Recovering after a bad reset on a shared branch**

 - If you already pushed the bad reset:

**Option A — Fix locally, then force push (dangerous)**

```
git reset --hard HEAD@{2}
git push --force
```

Only do this if you’re sure no one else has pulled the bad state.

**Option B — Create a new commit that restores the old state (safe)**

```
git merge 987abcd
```

- This reintroduces the lost commit without rewriting history.

**Recovering after a bad reset AND you closed the terminal**

- Even if you forgot the commit hash, reflog still has it.

```
git reflog show main
```

or

```
git reflog show HEAD
```

Git keeps reflog entries for 90 days by default.

---

**Why reflog is your best friend**

- Because even after:

- `git reset --hard`
- `git rebase --abort` gone wrong
- `git checkout` to a detached HEAD
- deleting a branch
- force pushing the wrong thing

… commits are still recoverable **as long as reflog has a record**.


Thanks:

👉Follow my LinkdIn Profile: www.linkedin.com/in/muhammad-shaban-45577719a

👉Youtube Channel: http://www.youtube.com/@engrm.shaban5099

