---
title: Test GitHub Actions Locally
layout: home
nav_order: 1
grand_parent: CI/CD
parent: GitHub Actions
permalink: docs/cicd/actions/test-locally
last_modified_date: 2024-01-07
---

# Test GitHub Actions Locally

GitHub Actions makes it easy to automate all your software workflows, now with world-class CI/CD. Build, test, and deploy your code right from GitHub. Make code reviews, branch management, and issue triaging work the way you want.

## Table of Contents

- [Test GitHub Actions Locally](#test-github-actions-locally)
  * [Table of Contents](#table-of-contents)
  * [Getting started](#getting-started)
  * [Installing Docker](#installing-docker)
    + [Windows](#windows)
    + [Linux (Ubuntu)](#linux-ubuntu)
    + [MacOS](#macos)
  * [Install Act](#install-act)
    + [Windows](#windows-1)
    + [Linux](#linux)
    + [MacOS](#macos-1)
  * [Run Github Actions locally](#run-github-actions-locally)
    + [Access to GitHub Token](#access-to-github-token)
    + [Generate PAT for Github](#generate-pat-for-github)
    + [Use MacOs to avoid plaintext](#use-macos-to-avoid-plaintext)
  * [Conclusions](#conclusions)

## Getting started
In order to test Github Actions Workflows locally you will need the following tools:

- Git
- Docker
- act

## Installing Docker

![GitHub Actions](https://user-cube.github.io/devops-cheatsheet/assets/images/docker.png)

### Windows 

First we need to enable WSL, open Powershell as Administrator and run:

```powershell
Enable-WindowsOptionalFeature -Online -FeatureName Microsoft-Windows-Subsystem-Linux
```

After this you will need to restart your computer. Once the computer is restarted you should be able to execute the following command:

```powershell
wsl --list
```

Now you just need to go to the Docker website and download the [Docker Desktop client](https://docs.docker.com/desktop/install/windows-install/). This will automatically install Docker for you.

### Linux (Ubuntu)

In order to install Docker on Ubuntu you can run the following commands:

```bash
# Add Docker's official GPG key:
sudo apt-get update
sudo apt-get install ca-certificates curl gnupg
sudo install -m 0755 -d /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
sudo chmod a+r /etc/apt/keyrings/docker.gpg

# Add the repository to Apt sources:
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu \
  $(. /etc/os-release && echo "$VERSION_CODENAME") stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
sudo apt-get update
sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```

If you want to run docker without sudo you can execute the following command:

```bash
sudo groupadd docker
sudo usermod -aG docker $USER
```

If you are using another Linux Distro you can find more information about how to install Docker on the [Docker documentation](https://docs.docker.com/desktop/install/mac-install/).

### MacOS

In order to use Docker on MacOS you just need to install the .dmg package from Docker [official documentation](https://docs.docker.com/desktop/install/mac-install/).

## Install Act

You can find more information about installing act in their [official documentation](https://github.com/nektos/act?tab=readme-ov-file#installation-through-package-managers).

![Act](https://user-cube.github.io/devops-cheatsheet/assets/images/act.gif)

### Windows

To install act on Windows you can use one of the following:

```powershell
choco install act-cli
```

or

```powershell
scoop install act
```

or

```powershell
winget install nektos.act
```

### Linux

On Linux you can install it by using the following command:

```bash
curl -s https://raw.githubusercontent.com/nektos/act/master/install.sh | sudo bash
```

### MacOS

In MacOS you can install it using brew. To install brew you can execute the following command:

```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

After installing brew you can install act by executing the following command:

```bash
brew install act
```

## Run Github Actions locally

![Act log](https://user-cube.github.io/devops-cheatsheet/assets/images/act-log.png)

Now that we have our environment set we just need to clone the git repository we want to test. Once we have the repo cloned we need to get into the root folder where we can find the folder `.github/workflows`.

You can see the available workflows by executing the command:

```bash
act --list
```

To execute workflows we can execute the following command:

```bash
act -W .github/workflows
```

To execute a specific workflow we can execute the following command:

```bash
act -W .github/workflows/<workflow_name>
```

If you only want to run a job inside a workflow you can execute the following command:

```bash
act -j <job_name>
```

If you are using an ARM based CPU add the following flag at the end of the command: `--container-architecture linux/amd64`.

You can find more about this tool on the [Beginner’s guide](https://github.com/nektos/act/wiki/Beginner's-guide) from act.

### Access to GitHub Token

GitHub [automatically provides](https://docs.github.com/en/actions/security-guides/automatic-token-authentication#about-the-github_token-secret) a `GITHUB_TOKEN` secret when running workflows inside GitHub.

If your workflow depends on this token, you need to create a [personal access token](https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/managing-your-personal-access-tokens) and pass it to act as a secret:

```bash
act -s GITHUB_TOKEN=[insert token or leave blank and omit equals for secure input]
```

If [GitHub CLI](https://cli.github.com/) is installed, the gh auth token command can be used to automatically pass the token to act:

```bash
act -s GITHUB_TOKEN="$(gh auth token)"
```

WARNING: `GITHUB_TOKEN` will be logged in shell history if not inserted through secure input or (depending on your shell config) the command is prefixed with a whitespace.

### Generate PAT for Github

- Verify your email address, if it hasn’t been verified yet.
- In the upper-right corner of any page, click your profile photo, then click Settings.

![PAT](https://user-cube.github.io/devops-cheatsheet/assets/images/gh-pat.png)

- In the left sidebar, click Developer settings.

- In the left sidebar, under Personal access tokens, click Tokens (classic).

- Select Generate new token, then click Generate new token (classic).

- In the “Note” field, give your token a descriptive name.

- To give your token an expiration, select Expiration, then choose a default option or click Custom to enter a date.

- Select the scopes you’d like to grant this token. To use your token to access repositories from the command line, select repo. A token with no assigned scopes can only access public information. For more information, see “Scopes for OAuth apps.”

- Click Generate token.

- Optionally, to copy the new token to your clipboard, click .

![PAT2](https://user-cube.github.io/devops-cheatsheet/assets/images/gh-pat2.png)

- To use your token to access resources owned by an organization that uses SAML single sign-on, authorize the token. For more information, see “Authorizing a personal access token for use with SAML single sign-on” in the GitHub Enterprise Cloud documentation.

You can find more information about Github Personal Access Tokens on [Github Documentation](https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/managing-your-personal-access-tokens#creating-a-personal-access-token-classic).

### Use MacOS to avoid plaintext

![Keychain](https://user-cube.github.io/devops-cheatsheet/assets/images/macos-keychain.png)

On your terminal you can generate a generic secret by executing the following command:

```bash
security find-generic-password -a ${USER} -s github_pat_<ACCOUNT> -w
```

Export Github Token:

```bash
export GITHUB_TOKEN=$(security find-generic-password -a ${USER} -s github_pat_<ACCOUNT> -w)
```

If you want you can add it to your `~/.bashrc` or `~/.zshrc` file. In this case you will need to reload your configurations, you can do it by executing the following command:

```bash
source ~/.zshrc # Change it to ~/.bashrc if you are using bash instead of zsh
```

Edit act configurations file available on `~/.actrc` and add the following line:

```bash
-s GITHUB_TOKEN=$GITHUB_TOKEN
```

By doing this every time you run act the build will automatically add your Personal Access Token to the execution.

## Conclusions

In conclusion, testing GitHub Actions workflows locally without the need for constant commits provides a valuable efficiency boost for developers dealing with multiple workflows. By leveraging tools such as Git, Docker, and Act, developers can simulate GitHub Actions in their local environment, allowing for quicker and more iterative testing.

The process involves setting up Docker, installing Act, and then running GitHub Actions workflows locally by cloning the repository and navigating to the root folder containing the workflows. Act commands facilitate the execution of entire workflows, specific workflows, or individual jobs within workflows.

Additionally, managing GitHub tokens is crucial for workflows that depend on the GITHUB_TOKEN secret. Developers can create personal access tokens (PAT) through GitHub’s Developer settings, with options to customize expiration dates and scopes. To seamlessly integrate the token with Act, developers can pass it as a secret during execution.

For enhanced security on macOS, the use of a generic secret avoids exposing the token in plaintext. Developers can export the GitHub token to an environment variable, ensuring a more secure handling of sensitive information during testing. Automating this process by editing the Act configurations file further streamlines the testing workflow.

In essence, the approach outlined in this article empowers developers to iterate and refine GitHub Actions workflows locally, fostering a more efficient and reliable software development lifecycle.