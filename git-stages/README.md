
 **The Three Stages of Git**

Git has **3 main stages** where your files live during the workflow:

- 1. **Working Directory (Working Tree)**
- 2. **Staging Area (Index)**  
- 3. **Repository (.git directory)**  

These stages represent the lifecycle of your changes.


**1. Working Directory (Working Tree)**  
This is where you **edit files**.

- You create, modify, or delete files here.  
- Git sees these changes as **unstaged**.  
- Nothing is saved in Git history yet.

**Commands related:**
```bash
git status
git diff
```

**2. Staging Area (Index)**  
This is a **temporary holding area** where you prepare changes before committing.

- You choose which changes to include in the next commit.  
- Only staged files will be committed.  
- Think of it as “packing your changes”.

**Command:**
```bash
git add filename
git add .
```

---

**3. Repository (.git directory)**  
This is where Git **permanently stores your commits**.

- Once you commit, your changes become part of the project history.  
- Stored inside the hidden `.git/` folder.  
- Safe, versioned, and recoverable.

**Command:**
```bash
git commit -m "message"
```

**Git Stages Workflow (Simple Diagram)**

```
[ Working Directory ]
        |
        | git add
        v
[ Staging Area ]
        |
        | git commit
        v
[ Repository ]
```

**In Simple Words**
- **Working Directory** → You are editing files  
- **Staging Area** → You select what to save  
- **Repository** → Git saves it permanently  

 **Useful Commands for Each Stage**

| Stage | Purpose | Commands |
|-------|---------|----------|
| Working Directory | Edit files | `git status`, `git diff` |
| Staging Area | Prepare files | `git add`, `git reset` |
| Repository | Save history | `git commit`, `git log` |
