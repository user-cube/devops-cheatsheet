---
title: Git Hooks
layout: home
nav_order: 1
parent: Git
permalink: docs/git/hooks
last_modified_date: 2024-01-07
---

## Git Hooks

Git hooks enable you to run custom scripts at different points in the Git workflow. Whether it's pre-commit checks or post-merge actions, Git hooks provide automation possibilities.

## Commit Message

Including the branch name in your commit messages can provide valuable context and make it easier to trace changes back to their source.

Automating the inclusion of the branch name in your commit messages can be achieved using Git hooks. Git hooks are scripts that run at certain points in the Git workflow. You can create a pre-commit hook to automatically append the branch name to your commit messages. Here's an example of how you could do this using a pre-commit hook:

**Step 1**: Navigate to your Git repository's .git/hooks directory.

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

# Get branch name
BRANCH_NAME=$(git symbolic-ref --short HEAD)

# List not allowed branches
DISALLOWED_BRANCHES=("main" "master" "develop")

# Check if the branch we get is on the disallowed branches
if [[ " ${DISALLOWED_BRANCHES[@]} " =~ " ${BRANCH_NAME} " ]]; then
    echo "Branch não permitida. As branches main, master e develop não são permitidas."
    exit 1
fi

# Add the branch name to the commit message
sed -i.bak -e "1s/^/$BRANCH_NAME: /" "$1"

# Remove the backup file created by sed
rm "$1.bak"
```

This script fetches the current branch name and appends it to the first line of the commit message. Adjust the script according to your needs.
Now, every time you make a commit, the branch name will be automatically added to the commit message.