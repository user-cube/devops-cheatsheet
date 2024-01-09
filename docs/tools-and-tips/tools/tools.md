---
title: Tools
layout: home
parent: Tools & Tips
nav_order: 1
permalink: docs/tols-and-tips/tools
last_modified_date: 2024-01-08
---

# Tools

This page contains a list of tools that you can use on your local machine to make your life easier.

## Termius

Allows you to manage multiple remote access with diferent protocols.

![Termius](https://user-cube.github.io/devops-cheatsheet/assets/images/tools/termius.png)

[Download Termius](https://termius.com/download)

## K9S

Easy tool to interact with a Kubernetes environment.

![k9s](https://user-cube.github.io/devops-cheatsheet/assets/images/tools/k9s.png)

[Download K9S](https://k9scli.io/)

## K8S Lens

Easy tool to interact with a Kubernetes environment.

![K8S Lens](https://user-cube.github.io/devops-cheatsheet/assets/images/tools/k8s-lens.png)

[Download K8S Lens](https://k8slens.dev/)

## Fig

The next-generation command line.

![Fig](https://user-cube.github.io/devops-cheatsheet/assets/images/tools/fig.png)

[Download Fig](https://fig.io/)

## GitKraken

GitKraken Client makes Git actions easy, fast, and intuitive. By providing a seamless approach to visual Git with the commit graph, as well as lightning fast terminal capabilities with the built-in CLI, GitKraken Client has helped thousands of developers all over the world! GitKraken Client is compatible across operating systems and integrated with GitHub, GitLab, Bitbucket, Azure DevOps, Jira, and more.

![Kraken](https://user-cube.github.io/devops-cheatsheet/assets/images/tools/kraken.png)

[Download GitKraken](https://www.gitkraken.com/)

## Visual Studio Code

Visual Studio Code is a code editor redefined and optimized for building and debugging modern web and cloud applications.

![Code](https://user-cube.github.io/devops-cheatsheet/assets/images/tools/vscode.png)

[Download Visual Studio Code](https://code.visualstudio.com/)

## Cursor.sh

Cursor is an AI-first code editor designed for pair-programming. It offers features that aim to enhance productivity and efficiency for software engineers. The tool allows for easy migration of favorite vscode extensions, themes, and keybindings with just one click.

![Cursor](https://user-cube.github.io/devops-cheatsheet/assets/images/tools/cursor.png)

[Download Cursor](https://cursor.sh/)

## csv2md

### Install with:

```bash
npm install -g csv2md
```

Small tool to convert (larger) csv to markdown tables. Processes stdin or csv file.

### Usage

```bash
csv2md data.csv > data.md
```

Piping data is possible (and recommend for larger files):

```bash
csv2md < data.csv

    max_i | min_i | max_f | min_f
    ---|---|---|---
    -122.1430195 | -122.1430195 | -122.415278 | 37.778643
    -122.1430195 | -122.1430195 | -122.40815 | 37.785034
    -122.4194155 | -122.4194155 | -122.4330827 | 37.7851673
```

To write the resulting markdown to a file, use the familiar stream syntax:

```bash
csv2md < data.csv > data.md
```
### Pretty Markdown
The pretty / p option will pad cells to uniform width and uses beginning and ending |-delimiters by default:

```bash
csv2md -p < data.csv

  | max_i        | min_i        | max_f        | min_f      |
  |--------------|--------------|--------------|------------|
  | -122.1430195 | -122.1430195 | -122.415278  | 37.778643  |
  | -122.1430195 | -122.1430195 | -122.40815   | 37.785034  |
  | -122.4194155 | -122.4194155 | -122.4330827 | 37.7851673 |
```
It's much more human readable than the default inline-style but will disable stream processing.

You can find more information about this tool on their [official GitHub](https://github.com/pstaender/csv2md)