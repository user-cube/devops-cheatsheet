---
title: Home
layout: home
nav_order: 1
last_modified_date: 2024-04-25
---

# <img src="https://user-cube.github.io/devops-cheatsheet/assets/images/devops-logo.png" alt="logo" width="100"/> DevOps Cheat Sheets

[![CI](https://github.com/user-cube/devops-cheatsheet/actions/workflows/ci.yml/badge.svg)](https://github.com/user-cube/devops-cheatsheet/actions/workflows/ci.yml) [![Deploy Jekyll site to Pages](https://github.com/user-cube/devops-cheatsheet/actions/workflows/pages.yml/badge.svg)](https://github.com/user-cube/devops-cheatsheet/actions/workflows/pages.yml)



Welcome to the DevOps Cheatsheets Repository! This repository serves as a comprehensive resource for DevOps enthusiasts, providing a collection of cheatsheets and relevant information to help you navigate and master the DevOps role.

![DevOps](https://user-cube.github.io/devops-cheatsheet/assets/images/devops.jpg)

## Table of Contents

## Table of Contents

1. [Kubernetes](/docs/kubernetes)
   - [Kubernetes Cheat Sheets](/docs/kubernetes/cheatsheets)
      - [Pods](/docs/kubernetes/cheatsheets/pods)
      - [Services](/docs/kubernetes/cheatsheets/services)
      - [Deployments](/docs/kubernetes/cheatsheets/deployments)
      - [ConfigMaps](/docs/kubernetes/cheatsheets/config-maps)
      - [Secrets](/docs/kubernetes/cheatsheets/secrets)
      - [Networking](/docs/kubernetes/cheatsheets/networking)
      - [Storage](/docs/kubernetes/cheatsheets/storage)
      - [Security](/docs/kubernetes/cheatsheets/security)
   - [K3S](/docs/kubernetes/k3s)
      - [Ingress Nginx on K3S](/docs/kubernetes/k3s/ingress-nginx)
   - [Kubernetes DNS](/docs/kubernetes/dns/)
      - [DNS Debugging](/docs/kubernetes/dns/debug)
2. [Git](/docs/git)
   - [Git Hooks](/docs/git/hooks)
      - [Commit Message Hook](/docs/git/hooks/commit-msg)
      - [Pre Push Hook](/docs/git/hooks/pre-push)
   - [Git Contributors Information Change](/docs/git/contributors-data)
3. [CI/CD](/docs/cicd)
   - [GitHub Actions](/docs/cicd/actions)
      - [Test GitHub Actions Locally](/docs/cicd/actions/test-locally)
   - [ArgoCD](/docs/cicd/argocd/)
      - [ArgoCD CLI Tool](/docs/cicd/argocd/cli-tool)
      - [ArgoCD Create Local Users](/docs/cicd/argocd/local-users)
      - [ArgoCD Add New Repositories](/docs/cicd/argocd/new-repositories)
      - [ArgoCD LDAP Integration](/docs/cicd/argocd/ldap-integration)
      - [ArgoCD HelmChart](/docs/cicd/argocd/helmchart)
   - [Heroku](/docs/cicd/heroku/)
      - [Sending Webhook Messages from Heroku to Discord](/docs/cicd/heroku/static-pages)
4. [Crontabs](/docs/crontab)
   - [Crontab Cheat Sheet](/docs/crontab/cheatsheets)
5. [Docker](/docs/docker)
   - [Run containers with SSL on development environments](/docs/docker/run-with-ssl)
   - [Docker Compose](/docs/docker/compose)
      - [Portainer Compose File](/docs/docker/compose/portainer)
      - [Redis Compose File](/docs/docker/compose/databases/redis)
      - [Postgres Compose File](/docs/docker/compose/databases/postgres)
      - [OpenSearch Compose File](/docs/docker/compose/opensearch)
   - [Dockerfiles](/docs/docker/dockerfiles)
      - [Ansible Playbooks on Docker](/docs/docker/dockerfiles/ansible)
6. [Sonarqube](/docs/sonarqube)
7. [GitHub](/docs/github)
   - [GitHub Pages](/docs/github/pages)
      - [Custom DNS](/docs/github/pages/custom-dns)
8. [Ansible](/docs/ansible/)
   - [Ansible Playbooks](/docs/ansible/playbooks)
      - [Test Playbooks On Docker](/docs/ansible/playbooks/test-on-docker)
      - [Install K3S and tools](/docs/ansible/playbooks/install-k3s-and-tools)
9. [Tools & Tips](/docs/tools-and-tips)
   - [Tools](/docs/tools-and-tips/tools)
      - [K9S](/docs/tools-and-tips/tools/k9s)
      - [Kompose](/docs/tools-and-tips/tools/kompose)
      - [kubectl](/docs/tools-and-tips/tools/kubectl)
      - [Helmchart](/docs/tools-and-tips/tools/helmchart)

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

## Join our Discord

We invite you to join our Discord community to connect with other DevOps enthusiasts, share insights, and seek help from the community. Let's grow together in our DevOps journey!

[Join Discord](https://discord.gg/FZmfkZpJUg)


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
