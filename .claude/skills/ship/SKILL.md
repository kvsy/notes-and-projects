---
name: ship
description: Stage all changes, commit with a generated message, and push to master. Use when the user wants to commit and push everything.
disable-model-invocation: true
---

## Current State
- Branch: !`git branch --show-current`
- Status: !`git status --short`
- Diff: !`git diff HEAD`

1. If nothing to commit, stop and say so.
2. Generate a concise commit message from the diff.
3. Run:
   ```
   git add -A
   git commit -m "<message>"
   git push origin master
   ```
   If push fails, retry with `git push origin main`.
4. Show `git log --oneline -1` to confirm.
