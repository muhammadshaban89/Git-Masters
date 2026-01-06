
Overview:
------------
- In the earliest days of programming, software development was simple and done by very small teams.
- There were no version control tools, and developers managed code manually.

How developers worked:

• 	Code was stored on punch cards, magnetic tapes, or floppy disks.

• 	Developers kept manual backups of files.

• 	Multiple versions were saved as:

    program_v1
    program_v2
    program_final
    program_final_final
    
so:    

- Collaboration was extremely difficult.
- If someone overwrote a file, the work was lost forever.
- No history, no rollback, no branching.
- As software grew larger and teams became bigger, manual methods failed.
- This led to the creation of the first generation of Version Control Systems.


Source Code Management (SCM)
-----------------------------

- is the overall practice of tracking and managing code changes.
- SCM refers to the **process and tools** used to manage source code changes during software development.

**What SCM does:**

- Tracks every change in code  
- Helps teams collaborate  
- Prevents conflicts  
- Stores history  
- Supports branching and merging

Version Control System (VCS)
----------------------------

- A Version Control System is a software tool that tracks changes to files over time.
- It allows developers to record versions, compare changes, collaborate, and restore previous states.
- A VCS is the **software tool** that performs SCM tasks.
  
 **What a VCS provides:**
- History of all changes  
- Ability to revert to older versions  
- Collaboration support  
- Branching and merging  
- Conflict resolution  

Examples:
- Git  
- SVN  
- Mercurial  
- CVS
- There are two types of **VCS: Centralized (one main server) and Distributed**(every developer has a full copy).

**1:Centralized Version Control System (CVCS)**
  
- A centralized system has **one main server** that stores the code.  
- Developers connect to this server to commit or update code.

**How CVCS works:**
```
Developer → Central Server → Repository
```

**Pros:**
- Simple to understand  
- Easy to manage permissions  
- One source of truth
  
 **Cons:**
- If the server goes down → **no one can work**  
- If the server is corrupted → **history is lost**  
- Slower for large teams  

 Examples:
- SVN  
- CVS  
- Perforce

**2"Distributed Version Control System (DVCS)**  

- A distributed system gives **every developer a full copy of the repository**, including full history.

**How DVCS works:**
```
Developer has full repo locally  
↓  
Can commit, branch, merge offline  
↓  
Push/pull to remote server (GitHub, GitLab)
```

**Pros:**
- Work offline  
- Faster operations (local commits)  
- Every developer has a backup  
- Better branching and merging  
- More secure and scalable  

**Cons:**
- Slightly more complex for beginners  

Examples:
- Git  
- Mercurial  
- Bazaar  


**CVCS vs DVCS — Comparison Table**

| Feature | Centralized (CVCS) | Distributed (DVCS) |
|--------|---------------------|---------------------|
| Repository location | One central server | Every developer has full copy |
| Offline work | ❌ No | ✅ Yes |
| Speed | Slower (network dependent) | Fast (local operations) |
| Backup | Single point of failure | Multiple backups |
| Branching | Harder | Very easy |
| Examples | SVN, CVS | Git, Mercurial |


**In Simple Words**
- **SCM** = managing code changes  
- **VCS** = tool that does SCM  
- **CVCS** = one central repo  
- **DVCS** = every developer has full repo (Git)

Thanks:

👉Follow my LinkdIn Profile: www.linkedin.com/in/muhammad-shaban-45577719a

