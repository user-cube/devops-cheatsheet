---
title: Pre Push Hook
layout: home
nav_order: 1
grand_parent: Git
parent: Git Hooks
permalink: docs/git/hooks/pre-push
last_modified_date: 2024-01-13
---

# Lock push if build is not ok

You can use a Git hook to automatically build your project and check for errors before allowing a push. Git hooks are scripts that run automatically at certain points in the Git workflow. In your case, you can use a pre-push hook.

Here's an example of a pre-push hook that builds your project and checks for errors:

1. Navigate to your Git repository.

2. Inside the .git directory, there's a hooks directory. If there isn't a pre-push file already, you can create one.

3. Open or create the pre-push file and add the following script:

```bash
#!/bin/bash

echo "Building project..."
# Add your build commands here

# For example, if you're using a build tool like Maven:
# mvn clean install

# Check if the build was successful
if [ $? -ne 0 ]; then
  echo "Error: Build failed. Push aborted."
  exit 1
fi

echo "Build successful. Checking for errors..."
# Add commands to check for errors
# For example, if you're running tests:
# mvn test

# Check if there are any errors
if [ $? -ne 0 ]; then
  echo "Error: Tests failed. Push aborted."
  exit 1
fi

echo "No errors found. Push allowed."
exit 0

```

Save the file and make it executable:

```bash
chmod +x pre-push
```

Now, every time you run git push, this script will be executed. If the project build or tests fail, the push will be aborted.

**Note**: Adjust the build and error-checking commands according to your project's build system and testing framework. Additionally, this example assumes a Unix-like environment. If you're using Windows, you might need to adapt the script accordingly.