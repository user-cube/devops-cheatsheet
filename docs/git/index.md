---
title: Git
layout: home
nav_order: 3
has_children: true
permalink: docs/git
last_modified_date: 2024-01-07
---

# Git

Git, the distributed version control system, is a versatile tool that empowers developers to manage their source code efficiently. While many are familiar with the basic commands, there exists a treasure trove of advanced tricks that can elevate your Git workflow to new heights. In this exploration, we'll delve into a set of Git tricks that go beyond the basics, offering insights and techniques to enhance your version control experience.

![Git logo](../../assets/images/git_logo.png)

## Interactive Rebase Magic:
Interactive rebase is a powerful feature that allows you to rewrite commit history. It lets you squash, edit, or reorder commits before pushing them to a remote repository. Mastering interactive rebase can lead to cleaner and more organized commit histories.

```bash
git rebase -i HEAD~n
```

## Stash Like a Pro:
The stash command is handy for temporarily shelving changes, but did you know you can create multiple stashes, name them, and even apply or drop specific stashes selectively?

```bash
git stash save "Work in Progress"
git stash list
git stash apply stash@{2}
```

## Reflog Rescues:
The Git reflog keeps a record of all changes to the repository, including resets and branch updates. When you accidentally lose a commit or branch, the reflog can be a lifesaver.

```bash
git reflog
git reset HEAD@{n}
```

## Bisect for the Win:
The git bisect command helps pinpoint the commit that introduced a bug by performing a binary search through the commit history. It's a valuable tool for efficiently identifying when a bug was introduced.

```bash
git bisect start
git bisect good <commit>
git bisect bad <commit>
```

## Custom Aliases:
Save time and keystrokes by creating custom Git aliases. These can be set up in your Git configuration file (~/.gitconfig) to simplify complex commands.

```bash
git config --global alias.lg "log --oneline --all --graph --decorate"
git lg
```

## Worktrees Wonders:
Git worktrees allow you to have multiple working directories for the same repository. This is especially useful when you need to work on different features simultaneously without switching branches.

```bash
git worktree add -b feature-branch ../feature-branch
```

## Git Hooks Mastery:
Git hooks enable you to run custom scripts at different points in the Git workflow. Whether it's pre-commit checks or post-merge actions, Git hooks provide automation possibilities.

```bash
.git/hooks/pre-commit
.git/hooks/post-merge
```

By incorporating these advanced Git tricks into your workflow, you can streamline your development process, troubleshoot issues more efficiently, and maintain a cleaner version control history. Experiment with these techniques to discover the ones that best fit your workflow, and unlock the full potential of Git for your projects.