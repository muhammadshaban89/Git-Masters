
**1. Create a New Branch**

**Create branch (local only)**
```bash
git branch feature-login
```

**Create and switch to it**
```bash
git checkout -b feature-login
```

**2. Switch Between Branches**
```bash
git checkout main
git checkout feature-login
```

**3. Push a Branch to GitHub**
```bash
git push -u origin feature-login
```
`-u` sets upstream so future pushes are just:
```bash
git push
```

---

**4. Pull Latest Changes Into Your Branch**
- From remote branch:
```bash
git pull
```

- Pull from another branch (e.g., main → your branch)
```bash
git pull origin main
```

---

**5. Merge Branches**
- Merge a branch into the current branch
```bash
git merge feature-login
```

- Example: merge feature into main
```bash
git checkout main
git merge feature-login
```

**6. Delete Branches**

- Delete local branch
```bash
git branch -d feature-login
```

- Force delete (if not merged)
```bash
git branch -D feature-login
```

- Delete branch on GitHub
```bash
git push origin --delete feature-login
```

---

**7. List Branches**

- Local branches
```bash
git branch
```

- Remote branches
```bash
git branch -r
```
- Local + remote
```bash
git branch -a
```

**8. Rename a Branch**

Rename current branch
```bash
git branch -m new-name
```

**Rename and push to GitHub**
```bash
git push origin -u new-name
git push origin --delete old-name
```

**9. Create Branch from a Specific Commit**
```bash
git checkout -b hotfix-123 abcdef1
```


**10. Clean Up Stale Remote Branch References**
```bash
git fetch --prune
```
