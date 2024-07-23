
---
title: TIL-5
date: 2024-07-23
---

Saving a shortcut for deleting many branches in git repository:
```
git branch | grep "refactor" | xargs git branch -D
```
```
