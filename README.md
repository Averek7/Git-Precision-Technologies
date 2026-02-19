# Fix the Broken Repository

Link to Google Doc: https://docs.google.com/document/d/112M-6uOQxuuxCL2jl1ls7CnCbLNFIPaiy8i6OGaljV4/edit?usp=sharing

## Overview

This repository originally contained:
- A mixed commit with unrelated changes
- An incorrect modification to todo.txt
- A leaked secret file
- Merge conflicts between branches
- An accidentally lost commit

All issues were identified and resolved while preserving history integrity.

---

## Task 1 – Inspection

Identified:
- Mixed commit: 2ee27fa ("quick fix")
- Incorrect content: 1af39ec
- Secret exposure: 2811388

---

## Task 2 – Clean Commit History

Used interactive rebase:

    git rebase -i 12516f6

Split the mixed commit into:
- docs: add features section to README
- docs: update project status in notes
- feat: add initial project configuration file

---

## Task 3 – Safe Revert

Used:

    git revert 1af39ec

Reason:
- Preserves shared history
- Creates explicit correction commit
- Avoids force push

---

## Task 4 – Merge Conflict Resolution

Merged:

    git merge feature/login

Resolved conflicts in:
- README.md
- notes.txt

Combined valid changes from both branches.

---

## Task 5 – Remove Leaked Secrets

Removed `secrets.txt`:

    git rm secrets.txt

In production I would:
- Rotate credentials immediately
- Revoke compromised keys
- Purge history with git filter-repo
- Add secret scanning
- Use environment variables

---

## Task 6 – Rebase and Sync

Verified that feature/login was already aligned with main.

Generally prefer:

    git rebase main

For:
- Linear history
- Cleaner PRs
- Fewer merge commits

---

## Task 7 – Recover Lost Commit

Used:

    git reflog

Recovered orphaned commit:

    git checkout -b recovered-quick-fix 2ee27fa

Reflog tracks HEAD movements even when commits are unreachable.

