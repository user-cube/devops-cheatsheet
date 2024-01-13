---
title: Commit Message Hook
layout: home
nav_order: 1
grand_parent: Git
parent: Git Hooks
permalink: docs/git/hooks/commit-msg
last_modified_date: 2024-01-13
---

# Commit Message

Incorporating the branch name into your commit messages can offer valuable context and simplify the process of tracing changes back to their origin.

Automating the inclusion of the branch name in commit messages can be accomplished using Git hooks. These are scripts that run at specific points in the Git workflow. For instance, you can create a pre-commit hook to automatically append the branch name to your commit messages. Here's an example of how you can achieve this using a pre-commit hook:

**Step 1**: Navigate to the .git/hooks directory in your Git repository.

```bash
cd /path/to/your/repo/.git/hooks
```

**Step 2**: Create a new file named commit-msg (if it doesn't already exist) and make it executable.

```bash
touch .git/hooks/commit-msg
chmod +x .git/hooks/commit-msg
```

**Step 3**: Add the following content to the file

```bash
#!/bin/bash

# Get the branch name
BRANCH_NAME=$(git symbolic-ref --short HEAD)

# List of disallowed branches
DISALLOWED_BRANCHES=("main" "master" "develop")

# Check if the obtained branch is in the disallowed branches list
if [[ " ${DISALLOWED_BRANCHES[@]} " =~ " ${BRANCH_NAME} " ]]; then
    echo "Branch not allowed. The main, master, and develop branches are not allowed."
    exit 1
fi

# Add the branch name to the commit message
sed -i.bak -e "1s/^/$BRANCH_NAME: /" "$1"

# Remove the backup file created by sed
rm "$1.bak"
```

This script retrieves the current branch name and appends it to the first line of the commit message. Modify the script as per your requirements.
Now, every time you make a commit, the branch name will be automatically added to the commit message.