---
title: "Git Reference"
date: 2021-03-31T15:59:19-05:00
toc: false
---

A living doc.

<!--more-->

{{< table >}}
| Task | Syntax |
| --- | --- |
| Init new repo | `git init` |
| Configure local user name | `git config --local user.name "<USERNAME>"` |
| Configure local user email | `git config --local user.email "<EMAIL>"` |
| List local configuration | `git config --local --list` |
| Create new branch from current branch | `git checkout -b <BRANCH>` |
| Create remote branch from local branch | `git push --set-upstream origin` |
| Checkout existing branch | `git checkout <BRANCH>` |
| Delete local branch | `git branch -D <BRANCH>` |
| Delete all local branches except for current banch | `git branch \| grep -v '^*' \| xargs git branch -D` |
| Delete remote branch | `git push --delete --force origin <BRANCH>` |
| List local branches | `git branch` |
| List remote branches | `git branch -r` |
| Show status | `git status` |
| Show diff | `git diff` |
| Stage all changes | `git add .` |
| Commit staged changes | `git commit -m "<MESSAGE>"` |
| Push local branch to remote branch | `git push` |
| Merge remote branch into local branch | `git pull origin <BRANCH>` |
| Show commit log | `git log` |
| Show pretty commit log | `git log --oneline` |
| Show who last touched each line of a file | `git blame <FILE>` |
| Unstage all changes | `git reset` |
| Undo all modified files | `git checkout .` |
| Delete untracked files | `git clean -f -d` |
| Interactively rebase last n commits | `git rebase -i HEAD~n` |
| Cleanup local repo | `git gc` |
| Track case-only filename changes | `git mv -f` |
| Ignore a file that was already committed | `git rm -r --cached . && git add .` |
{{< /table >}}
