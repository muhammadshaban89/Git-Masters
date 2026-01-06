Lets Learn:
------------
- Installing **Git on RHEL**
- Running **git init**
- Using **git add**, **git commit**, **git status**, etc.


**1. Install Git on RHEL (RHEL 8 / RHEL 9)**

-  Step 1 — Update system  
```bash
sudo dnf update -y
```

- Step 2 — Install Git  

```bash
sudo dnf install git -y
```

-  Step 3 — Verify installation  
```bash
git --version
```


**2. Configure Git (Required Before First Commit)**

A): Set your identity (stored globally):

```bash
git config --global user.name "Muhammad"
git config --global user.email "you@example.com"
```
- This helps:

• 	Tracking who made which change.

• 	Accountability in teams.

• 	Clear audit trail.

- Your commits are linked to your online identity.
- If your email matches your GitHub account:

• 	Your commits show your profile picture.

• 	Contributions appear in your GitHub graph

B): Check your config:

```bash
git config --list
```

 **3. Initialize a Git Repository**

Inside any project folder:

```bash
git init
```

This creates a hidden `.git/` directory that stores all version history.

**4. Check Repository Status**

```bash
git status
```

Shows:
- new files  
- modified files  
- staged files  

**5. Add Files to Staging Area**

Add a single file:

```bash
git add filename
```

Add all files:

```bash
git add .
```


**6. Commit Changes**

```bash
git commit -m "Initial commit"
```

A commit = a snapshot of your project.


**7. View Commit History**

```bash
git log
```

Short version:

```bash
git log --oneline
```


**8. Add Remote Repository (GitHub / GitLab)**

```bash
git remote add origin https://github.com/username/repo.git
```

Check remotes:

```bash
git remote -v
```

**9. Push Code to Remote**

First push (sets upstream):

```bash
git push -u origin main
```

Later pushes:

```bash
git push
```

 **10. Pull Latest Changes**

```bash
git pull
```


**Quick Reference Table**

| Task | Command |
|------|---------|
| Install Git | `sudo dnf install git -y` |
| Initialize repo | `git init` |
| Check status | `git status` |
| Add files | `git add .` |
| Commit | `git commit -m "msg"` |
| Add remote | `git remote add origin URL` |
| Push | `git push -u origin main` |
| Pull | `git pull` |

 **DevOps Git Workflow Diagram (Text Version)**
 ```yaml
Developer → Feature Branch → Commit → Push → Pull Request
        → Code Review → Merge to Main → CI/CD Pipeline
        → Build → Test → Deploy → GitOps Sync (K8s)

```

Thanks:

👉Follow my LinkdIn Profile: www.linkedin.com/in/muhammad-shaban-45577719a
