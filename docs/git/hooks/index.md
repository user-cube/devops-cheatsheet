---
title: Git Hooks
layout: home
nav_order: 1
parent: Git
has_children: true
permalink: docs/git/hooks
last_modified_date: 2024-01-13
---

# Git Hooks

Git hooks are customizable scripts that Git executes at specific points in the version control process. They are stored in the .git/hooks directory of a Git repository. There are two types of Git hooks: client-side and server-side. Client-side hooks are triggered by operations such as committing and merging, while server-side hooks are triggered by network operations such as receiving pushed commits.

One common use case for Git hooks is enforcing code style guidelines. By using a pre-commit hook, developers can ensure that their code adheres to a specific style guide before it is committed to the repository. This helps maintain a consistent codebase and reduces the need for manual code reviews focused on style issues.

Another use case for Git hooks is running tests before allowing a commit. A pre-commit hook can be used to automatically run unit tests or other checks to ensure that the code being committed meets certain quality standards. This helps catch issues early in the development process and prevents the introduction of buggy code into the repository.

Git hooks can also be used to send notifications when certain actions occur. For example, a post-receive hook on the server side can be used to trigger notifications or other automated processes when new commits are received. This can be useful for integrating Git with other systems or for keeping team members informed about changes to the repository.

One important thing to note about Git hooks is that they are not shared between repositories. Each Git repository has its own set of hooks, which allows for flexibility in customizing the behavior of different repositories. This means that hooks can be tailored to the specific needs and workflows of individual projects, making them a powerful tool for automating and enforcing development processes.

In summary, Git hooks are a versatile and powerful feature of Git that allow for the automation and customization of various aspects of the version control process. Whether it's enforcing code style guidelines, running tests, or integrating with other systems, Git hooks provide a flexible way to enhance and streamline development workflows.