---
title: ArgoCD CLI Tool
layout: home
nav_order: 1
grand_parent: CI/CD
parent: ArgoCD
permalink: docs/cicd/argocd/cli-tool
last_modified_date: 2024-01-13
---

# ArgoCD CLI Tool

The ArgoCD CLI tool provides a command-line interface for interacting with ArgoCD. It allows users to manage and automate ArgoCD operations from the command line, enabling tasks such as application management, configuration updates, and monitoring of deployment status.

The ArgoCD CLI tool offers a variety of commands for interacting with ArgoCD, including:

- Application management: Creating, updating, deleting, and syncing applications.
- Configuration management: Managing repositories, settings, and credentials.
- Access control: Managing users, roles, and permissions.
- Monitoring: Checking the status of deployments and synchronization.

By using the ArgoCD CLI tool, users can automate and script ArgoCD operations, integrate ArgoCD with other tools and workflows, and efficiently manage their Kubernetes deployments.

## Table of Contents

- [ArgoCD CLI Tool](#argocd-cli-tool)
  * [Table of Contents](#table-of-contents)
  * [Installation](#installation)
      - [Linux and WSL](#linux-and-wsl)
        * [ArchLinux](#archlinux)
        * [Homebrew](#homebrew)
        * [Download With Curl](#download-with-curl)
          + [Download latest version](#download-latest-version)
          + [Download concrete version](#download-concrete-version)
      - [Mac](#mac)
        * [Homebrew](#homebrew-1)
        * [Download With Curl](#download-with-curl-1)
      - [Windows](#windows)
        * [Download With PowerShell: Invoke-WebRequest](#download-with-powershell-invoke-webrequest)

## Installation
You can download the latest Argo CD version from [the latest release page of this repository](https://github.com/argoproj/argo-cd/releases), which will include the argocd CLI.

#### Linux and WSL

##### ArchLinux

```
pacman -S argocd
```

##### Homebrew

```bash
brew install argocd
```

##### Download With Curl

###### Download latest version

```bash
curl -sSL -o argocd-linux-amd64 https://github.com/argoproj/argo-cd/releases/latest/download/argocd-linux-amd64
sudo install -m 555 argocd-linux-amd64 /usr/local/bin/argocd
rm argocd-linux-amd64
```

###### Download concrete version

Set `VERSION` replacing `<TAG>` in the command below with the version of Argo CD you would like to download:

```bash
VERSION=<TAG> # Select desired TAG from https://github.com/argoproj/argo-cd/releases
curl -sSL -o argocd-linux-amd64 https://github.com/argoproj/argo-cd/releases/download/$VERSION/argocd-linux-amd64
sudo install -m 555 argocd-linux-amd64 /usr/local/bin/argocd
rm argocd-linux-amd64
```

You should now be able to run `argocd` commands.

#### Mac

##### Homebrew

```bash
brew install argocd
```

##### Download With Curl

You can view the latest version of Argo CD at the link above or run the following command to grab the version:


```bash
VERSION=$(curl --silent "https://api.github.com/repos/argoproj/argo-cd/releases/latest" | grep '"tag_name"' | sed -E 's/.*"([^"]+)".*/\1/')
```

Replace `VERSION` in the command below with the version of Argo CD you would like to download:

```bash
curl -sSL -o argocd-darwin-amd64 https://github.com/argoproj/argo-cd/releases/download/$VERSION/argocd-darwin-amd64
```

Install the Argo CD CLI binary:

```bash
sudo install -m 555 argocd-darwin-amd64 /usr/local/bin/argocd
rm argocd-darwin-amd64
```

After finishing either of the instructions above, you should now be able to run `argocd` commands.

#### Windows

##### Download With PowerShell: Invoke-WebRequest

You can view the latest version of Argo CD at the link above or run the following command to grab the version:

```powershell
$version = (Invoke-RestMethod https://api.github.com/repos/argoproj/argo-cd/releases/latest).tag_name
```

Replace `$version` in the command below with the version of Argo CD you would like to download:

```powershell
$url = "https://github.com/argoproj/argo-cd/releases/download/" + $version + "/argocd-windows-amd64.exe"
$output = "argocd.exe"

Invoke-WebRequest -Uri $url -OutFile $output
```

Also please note you will probably need to move the file into your PATH.

After finishing the instructions above, you should now be able to run `argocd` commands.