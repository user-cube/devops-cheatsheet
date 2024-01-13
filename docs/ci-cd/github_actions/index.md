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

GitHub Actions is a platform provided by GitHub for continuous integration and continuous delivery (CI/CD). It enables the automation of various tasks in the software development workflow directly within the GitHub repository. With GitHub Actions, custom workflows can be defined to build, test, and deploy code.

![GitHub Actions](https://user-cube.github.io/devops-cheatsheet/assets/images/github-actions.png)

Key features of GitHub Actions include:

- **Workflow**: A workflow is a series of automated steps defined in a YAML file within the repository. Workflows can be triggered by events such as pushes to the repository, pull requests, issue comments, and more.

- **Jobs**: Each workflow consists of one or more jobs, which are separate sets of steps that run in parallel or sequentially. Jobs are defined in the workflow file and can be customized based on requirements.

- **Steps**: Steps are individual tasks within a job. They can include actions (pre-built, reusable units of code), shell commands, or scripts. Steps define the actions to be taken during the workflow.

- **Actions**: Actions are reusable units of code that can be used across different workflows. They can be created by the community or by the team, and they encapsulate common tasks like building, testing, and deploying code.

- **Events**: Workflows are triggered by specific events, such as pushes to specific branches, pull requests, issue comments, scheduled events, etc. Workflows can be customized to respond to the events that matter to the development process.

- **Environment Variables**: GitHub Actions allows the setting and use of environment variables within workflows. This flexibility enables the parameterization of workflows and customization of their behavior based on different conditions.

GitHub Actions supports a wide variety of programming languages, platforms, and tools, making it versatile for different development environments. It seamlessly integrates with the GitHub platform, allowing the progress and results of workflows to be seen directly within the GitHub interface.

To get started with GitHub Actions, a .github/workflows directory can be created in the repository to define workflows using YAML files. GitHub provides documentation and a marketplace where pre-built actions can be found to use in workflows.
