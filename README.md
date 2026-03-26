# COMP120 – Assignment 3: GitHub Project Management
**Student:** Darius Pal  
**Course:** COMP120  
**License:** Apache 2.0

---

## Overview

This assignment teaches the core skills needed to manage a software project collaboratively using GitHub. Rather than focusing on writing code, the work here is about **process** — learning how a real development team organises work, tracks progress, and safely merges contributions from multiple people.

The five learning objectives are:

1. [Create and manage a project on GitHub](#1-create-and-manage-a-project-on-github)
2. [Use milestones to track progress](#2-use-milestones-to-track-progress)
3. [Create and assign issues](#3-create-and-assign-issues)
4. [Clone repositories and contribute using branches](#4-clone-repositories-and-contribute-using-branches)
5. [Manage collaborator access](#5-manage-collaborator-access)

---

## 1. Create and Manage a Project on GitHub

### What
A **GitHub repository** is the central store for every file, commit, and piece of history that belongs to a project. A **GitHub Project** (the kanban/board view) sits on top of a repository and gives a high-level view of work across multiple issues and pull requests.

### Why
- Without a single source of truth, team members end up with conflicting copies of code.
- A project board makes the state of every work item visible at a glance, replacing the need for status-update meetings.
- All changes are versioned, so nothing is ever truly lost.

### How

**Create the repository**
1. Log in to [github.com](https://github.com) and click **New** (top-left, or `+` → *New repository*).
2. Fill in a repository name (e.g. `comp120_Darius-Pal_assignment3`), choose *Public* or *Private*, and tick *Add a README file*.
3. Click **Create repository**.

**Create a Project board**
1. Inside the repository, click the **Projects** tab → **New project**.
2. Choose the *Board* template (columns: *To Do*, *In Progress*, *Done*).
3. Give the board a meaningful name (e.g. *Assignment 3 Board*) and click **Create project**.
4. Link the project to the repository under *Project settings → Linked repositories*.

**Day-to-day management**
- Drag cards between columns as work progresses.
- Use the *Insights* tab to view a burn-up or velocity chart over time.
- Archive cards once they are no longer relevant to keep the board clean.

---

## 2. Use Milestones to Track Progress

### What
A **milestone** groups a set of issues and pull requests under a shared deadline or goal. GitHub shows a live percentage-complete bar based on how many items in the milestone are closed.

### Why
- Milestones translate broad project phases (e.g. *Week 1 Setup*, *Sprint 2 – Core Features*) into measurable targets.
- The completion percentage gives an instant, honest answer to "how far along are we?" without requiring manual status reports.
- They prevent scope creep by making it clear which work belongs to the current phase.

### How

**Create a milestone**
1. Navigate to the repository → **Issues** tab → **Milestones** → **New milestone**.
2. Enter a title (e.g. *Sprint 1 – Project Setup*), an optional description, and a due date.
3. Click **Create milestone**.

**Assign issues to a milestone**
- When creating or editing an issue, use the *Milestone* dropdown on the right-hand side to attach it.
- You can bulk-assign from the Issues list by ticking several issues and using *Milestone* in the *Actions* menu.

**Track progress**
- The milestone list shows each milestone's due date and a `n/m issues closed` progress bar.
- When all issues are closed the milestone can be closed manually to archive it.

---

## 3. Create and Assign Issues

### What
An **issue** is a unit of work — it can represent a bug report, a feature request, a question, or any task that needs to be tracked. Issues are the primary way work is described, discussed, and assigned before any code is written.

### Why
- Writing an issue forces you to clearly describe the *problem* or *goal* before jumping to a solution.
- Issues create a permanent, searchable record of decisions and discussions.
- Assigning issues makes it explicit who owns a piece of work, preventing duplication and gaps.
- Linking an issue to a branch or pull request automatically closes it when the work is merged.

### How

**Create an issue**
1. Go to the repository → **Issues** → **New issue**.
2. Write a clear **title** (e.g. `Add README documentation for milestone workflow`).
3. In the body, describe:
   - **What** needs to be done.
   - **Why** it is needed (acceptance criteria or context).
   - **How** it might be approached (optional notes or links).
4. On the right panel:
   - **Assignees** – choose the person responsible.
   - **Labels** – tag the type of work (`bug`, `enhancement`, `documentation`, etc.).
   - **Milestone** – attach it to the relevant milestone.
   - **Project** – add it to the project board so it appears as a card.
5. Click **Submit new issue**.

**Close an issue automatically via a commit or PR**
- Include a closing keyword in a commit message or PR description:
  ```
  Fixes #12
  Closes #12
  Resolves #12
  ```
- When the branch is merged into the default branch, GitHub closes the linked issue automatically.

---

## 4. Clone Repositories and Contribute Using Branches

### What
**Cloning** downloads a full copy of a repository (all files and history) to your local machine. **Branches** are isolated lines of development — changes on a branch do not affect `main` until they are explicitly merged. A **pull request (PR)** is the formal mechanism to propose, review, and merge a branch back into `main`.

### Why
- Working directly on `main` is risky: one bad push can break the code for everyone.
- Branches sandbox changes so teammates can review them before they land in the shared codebase.
- The pull-request review step enforces a quality gate: at least one other person verifies the work.
- The full git history is preserved, making it easy to trace *when* and *why* each change was made.

### How

**Clone the repository**
```bash
# HTTPS (recommended for beginners — prompts for GitHub username/password or token)
git clone https://github.com/<username>/comp120_Darius-Pal_assignment3.git

# SSH (requires an SSH key set up in GitHub → Settings → SSH keys)
git clone git@github.com:<username>/comp120_Darius-Pal_assignment3.git

cd comp120_Darius-Pal_assignment3
```

**Create a feature branch**
```bash
# Always start from an up-to-date main
git checkout main
git pull origin main

# Create and switch to a new branch
# Convention: <type>/<short-description>  e.g. feature/add-readme or fix/typo-in-docs
git checkout -b feature/add-milestone-docs
```

**Make changes, stage, and commit**
```bash
# Edit files, then stage them
git add README.md            # stage a specific file
git add .                    # stage all changed files

# Commit with a descriptive message
# Convention: imperative mood, ≤72 characters
git commit -m "docs: add milestone workflow documentation"
```

**Push the branch to GitHub**
```bash
git push origin feature/add-milestone-docs
```

**Open a pull request**
1. GitHub will show a yellow banner: *"Compare & pull request"* — click it.
2. Set the **base** branch to `main` and the **compare** branch to your feature branch.
3. Write a title and description that explains *what* changed and *why*.
4. Link the relevant issue (e.g. `Closes #5`).
5. Request a review from a collaborator.
6. Once approved, click **Merge pull request** → **Confirm merge**.
7. Delete the feature branch (GitHub offers this automatically after merge).

**Keep your branch up to date (avoiding merge conflicts)**
```bash
# While working on a long-lived branch, periodically sync with main
git fetch origin
git rebase origin/main      # or: git merge origin/main
```

---

## 5. Manage Collaborator Access

### What
**Collaborators** are GitHub accounts that have been explicitly granted permission to read from or write to a repository. GitHub provides five permission levels: *Read*, *Triage*, *Write*, *Maintain*, and *Admin*.

| Role | Can do |
|---|---|
| **Read** | View and clone the repository, comment on issues and PRs |
| **Triage** | Read + manage issues and PRs (label, assign, close), cannot push code |
| **Write** | Triage + push code to branches, create and merge PRs |
| **Maintain** | Write + manage repository settings (topics, description, protected branches) |
| **Admin** | Full control, including adding/removing collaborators and deleting the repository |

### Why
- The **principle of least privilege**: give each person only the access they need to do their job, reducing the blast radius of mistakes or compromised accounts.
- Protected branches (requiring PRs and reviews before merging) enforce process even for collaborators who technically have write access.
- Audit logs under *Settings → Security log* record every permission change, providing accountability.

### How

**Add a collaborator**
1. In the repository, go to **Settings** → **Collaborators** (under *Access*).
2. Click **Add people**, search by GitHub username or email, and select the correct account.
3. Choose the appropriate role and click **Add \<username\> to this repository**.
4. The invited person receives an email and must accept the invitation before access is granted.

**Set up branch protection (recommended for teams)**
1. Go to **Settings** → **Branches** → **Add branch protection rule**.
2. Set *Branch name pattern* to `main`.
3. Enable:
   - *Require a pull request before merging* – prevents direct pushes.
   - *Require approvals* (set to at least 1) – at least one reviewer must approve.
   - *Require status checks to pass* – CI must be green before merging.
4. Click **Create**.

**Remove a collaborator**
1. **Settings** → **Collaborators** → find the person → **Remove**.
2. Their local clone still exists, but they lose push access immediately and can no longer see private repositories.

---

## Repository Structure

```
comp120_Darius-Pal_assignment3/
├── README.md   ← This file — full documentation for the assignment
└── LICENSE     ← Apache License 2.0
```

---

## Quick-Reference: Common Git Commands

| Task | Command |
|---|---|
| Clone a repo | `git clone <url>` |
| Check current status | `git status` |
| See what changed | `git diff` |
| Create and switch to a branch | `git checkout -b <branch-name>` |
| Switch to an existing branch | `git checkout <branch-name>` |
| Stage all changes | `git add .` |
| Commit staged changes | `git commit -m "message"` |
| Push branch to GitHub | `git push origin <branch-name>` |
| Pull latest changes | `git pull origin main` |
| View commit history | `git log --oneline` |
| List all branches | `git branch -a` |

---

## License

This project is licensed under the [Apache License 2.0](LICENSE).
