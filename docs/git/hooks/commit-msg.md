---
title: Commit Message Hook
layout: home
nav_order: 1
grand_parent: Git
parent: Git Hooks
permalink: docs/git/hooks/commit-msg
last_modified_date: 2024-05-19
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

# Get the name of the current branch
BRANCH_NAME=$(git symbolic-ref --short HEAD)

# Check if the current commit is a merge commit
if [ -e .git/MERGE_HEAD ]; then
  # It's a merge commit
  echo "Merge commit detected, skipping branch verifications."
else
  # It's not a merge commit, so check if the branch is allowed or not
  # List of disallowed branches
  DISALLOWED_BRANCHES=("main" "master" "production" "qa" "staging" "develop")

  # Check if the branch is in the list of disallowed branches
  if [[ " ${DISALLOWED_BRANCHES[@]} " =~ " ${BRANCH_NAME} " ]]; then
    echo "Branch not allowed. The disallowed branches are: ${DISALLOWED_BRANCHES[@]}"
    exit 1
  fi

  # Add the branch name to the beginning of the commit message
  sed -i.bak -e "1s/^/$BRANCH_NAME: /" "$1"

  # Remove the backup file created by sed
  rm "$1.bak"
fi

# Allow push after processing the commit (whether modifying the message or allowing a merge)
exit 0
```

This script retrieves the current branch name and appends it to the first line of the commit message. Modify the script as per your requirements.
Now, every time you make a commit, the branch name will be automatically added to the commit message.
