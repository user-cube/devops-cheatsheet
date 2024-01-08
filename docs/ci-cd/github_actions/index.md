---
title: GitHub Actions
layout: home
nav_order: 1
parent: CI/CD
has_children: true
permalink: docs/cicd/actions/
last_modified_date: 2024-01-07
---

# GitHub Actions

GitHub Actions is a continuous integration and continuous delivery (CI/CD) platform provided by GitHub. It allows you to automate various tasks in your software development workflow directly within your GitHub repository. With GitHub Actions, you can define custom workflows to build, test, and deploy your code.

![GitHub Actions](https://user-cube.github.io/devops-cheatsheet/assets/images/github-actions.png)

Key features of GitHub Actions include:

- **Workflow**: A workflow is a series of automated steps that you define in a YAML file within your repository. Workflows can be triggered by events such as pushes to the repository, pull requests, issue comments, and more.

- **Jobs**: Each workflow consists of one or more jobs, which are separate sets of steps that run in parallel or sequentially. Jobs are defined in the workflow file and can be customized based on your requirements.

- **Steps**: Steps are individual tasks within a job. They can include actions (pre-built, reusable units of code), shell commands, or scripts. Steps define the actions to be taken during the workflow.

- **Actions**: Actions are reusable units of code that can be used across different workflows. They can be created by the community or by your team, and they encapsulate common tasks like building, testing, and deploying code.

- **Events**: Workflows are triggered by specific events, such as pushes to specific branches, pull requests, issue comments, scheduled events, etc. You can customize workflows to respond to the events that matter to your development process.

- **Environment Variables**: GitHub Actions allows you to set and use environment variables within your workflows. This flexibility enables you to parameterize your workflows and customize their behavior based on different conditions.

GitHub Actions supports a wide variety of programming languages, platforms, and tools, making it versatile for different development environments. It seamlessly integrates with the GitHub platform, allowing you to see the progress and results of your workflows directly within the GitHub interface.

To get started with GitHub Actions, you can create a .github/workflows directory in your repository and define your workflows using YAML files. GitHub provides documentation and a marketplace where you can find pre-built actions to use in your workflows.