---
title: Contributors Information Change
layout: home
nav_order: 1
parent: Git
permalink: docs/git/contributors-data
last_modified_date: 2024-01-11
---

# Git Contributors Information Change

This script can be useful if you've been using an incorrect email address for your Git commits and you want to update them retrospectively. After running this script, be cautious when pushing the changes to a remote repository, especially if others have cloned the repository. The rewritten history may cause issues for collaborators, so it's often recommended to coordinate with them before applying such changes.

Here's a breakdown of what the script does:

- Set Variables:
    - `OLD_EMAIL`: The old email address that you want to replace.
    - `CORRECT_NAME`: The correct name you want to associate with the commits.
    - `CORRECT_EMAIL`: The correct email address you want to associate with the commits.

- Performing the Replacement:
    - The script then uses `git filter-branch` with the `--env-filter` option.
    - It checks if the current commit's committer email (`GIT_COMMITTER_EMAIL`) matches the old email (`OLD_EMAIL`). If it does, it updates the committer name and email to the correct values.
    - It performs the same check and update for the author information (`GIT_AUTHOR_EMAIL`).

- Tag and Branch Update:
    - The `--tag-name-filter cat` ensures that tags are also updated.
    - The `--branches --tags` specifies that the script should operate on all branches and tags.

## Script

```bash
cat <<EOL >> information-change.sh
#!/bin/sh

git filter-branch --env-filter '
OLD_EMAIL="<OLD_EMAIL>"
CORRECT_NAME="<NAME>"
CORRECT_EMAIL="<NEW_EMAIL>"

if [ "\$GIT_COMMITTER_EMAIL" = "\$OLD_EMAIL" ]
then
    export GIT_COMMITTER_NAME="\$CORRECT_NAME"
    export GIT_COMMITTER_EMAIL="\$CORRECT_EMAIL"
fi
if [ "\$GIT_AUTHOR_EMAIL" = "\$OLD_EMAIL" ]
then
    export GIT_AUTHOR_NAME="\$CORRECT_NAME"
    export GIT_AUTHOR_EMAIL="\$CORRECT_EMAIL"
fi
' --tag-name-filter cat -- --branches --tags
EOL

chmod +x information-change.sh

./information-change.sh
```

After executing the script you will need to force push your code:

```bash
git push --force --tags origin 'refs/heads/*'
```
