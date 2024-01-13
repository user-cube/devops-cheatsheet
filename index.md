---
title: Home
layout: home
nav_order: 1
last_modified_date: 2024-01-07
---

# DevOps Cheat Sheets

Welcome to the DevOps Cheatsheets Repository! This repository serves as a comprehensive resource for DevOps enthusiasts, providing a collection of cheatsheets and relevant information to help you navigate and master the DevOps role.

![DevOps](https://user-cube.github.io/devops-cheatsheet/assets/images/devops.jpg)

## Table of Contents

1. [Kubernetes](/devops-cheatsheet/docs/kubernetes)
   - [Kubernetes Basics](/devops-cheatsheet/docs/kubernetes/cheatsheets)
      - [Pods](/devops-cheatsheet/docs/kubernetes/cheatsheets)
2. [Git](/devops-cheatsheet/docs/git)
   - [Git Hooks](/devops-cheatsheet/docs/git/hooks)
   - [Git Contributors Information Change](/devops-cheatsheet/docs/git/contributors-data)
3. [CI/CD](/devops-cheatsheet/docs/cicd)
   - [GitHub Actions](/devops-cheatsheet/docs/cicd/actions)
      - [Test GitHub Actions Locally](/devops-cheatsheet/docs/cicd/actions/test-locally)
4. [Crontabs](/devops-cheatsheet/docs/crontab)
   - [Crontab Cheat Sheet](/devops-cheatsheet/docs/crontab/cheatsheets)
5. [Docker](/devops-cheatsheet/docs/docker)
   - [Docker Compose](/devops-cheatsheet/docs/docker/compose)
      - [Portainer Compose File](/devops-cheatsheet/docs/docker/compose/portainer)
      - [Redis Compose File](/devops-cheatsheet/docs/docker/compose/databases/redis)
      - [Postgres Compose File](/devops-cheatsheet/docs/docker/compose/databases/postgres)
      - [OpenSearch Compose File](/devops-cheatsheet/docs/docker/compose/opensearch)
   - [Dockerfiles](/devops-cheatsheet/docs/docker/dockerfiles)
6. [Tools & Tips](/devops-cheatsheet/docs/tols-and-tips)
   - [Tools](/devops-cheatsheet/docs/tols-and-tips/tools)
      - [K9S](/devops-cheatsheet/docs/tols-and-tips/tools/k9s)
      - [Kompose](/devops-cheatsheet/docs/tols-and-tips/tools/kompose)
      - [kubectl](/devops-cheatsheet/docs/tols-and-tips/tools/kubectl)
      - [Helmchart](/devops-cheatsheet/docs/tols-and-tips/tools/helmchart)

## How to Use

Feel free to explore the cheatsheets and resources available in this repository. Each cheatsheet is designed to provide quick and concise information to help you navigate the DevOps path effectively. Whether you are a beginner or an experienced user, you'll find valuable insights and tips.

## Contributing

We encourage contributions from the community! If you have additional cheatsheets, tips, or corrections, please submit a pull request. Together, we can make this repository a valuable reference for anyone working on DevOps path.

<ul class="list-style-none">
{% for contributor in site.github.contributors %}
  <li class="d-inline-block mr-1">
     <a href="{{ contributor.html_url }}"><img src="{{ contributor.avatar_url }}" width="32" height="32" alt="{{ contributor.login }}"></a>
  </li>
{% endfor %}
</ul>

## Issues

To enhance our collaborative efforts and streamline issue reporting, we have implemented three distinct templates for opening issues. These templates are designed to provide clear and structured information, ensuring a more efficient and effective problem-solving process.

1. **Error Reporting Template**:
If you encounter any bugs, glitches, or unexpected behavior within the project, please use the "Error Reporting" template. This template will guide you through providing essential details about the issue, such as the steps to reproduce it, the expected behavior, and any relevant error messages.

2. **Documentation Update Template**:
For issues related to outdated or inaccurate documentation, we encourage you to use the "Documentation Update" template. This template helps you articulate the specific changes required, ensuring a swift and precise update to our project's documentation. Your contributions to improving our documentation are highly valued.

3. **New Documentation Creation Template**:
Should you identify a need for new documentation or have insights on areas that lack proper documentation, please utilize the "New Documentation Creation" template. This template will guide you through proposing and creating new documentation, contributing to the project's overall comprehensiveness.

## License

This repository is licensed under the MIT License, ensuring that the information provided is freely accessible and can be used by the community.