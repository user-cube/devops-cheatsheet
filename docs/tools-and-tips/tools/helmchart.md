---
title: Helmchart
layout: home
grand_parent: Tools & Tips
parent: Tools
nav_order: 4
permalink: docs/tols-and-tips/tools/helmchart
last_modified_date: 2024-01-09
---

# Helmchart

The Helm project offers two methods for obtaining and installing Helm. These are the official approaches for acquiring Helm releases. Additionally, the Helm community presents techniques for installing Helm through various package managers. Instructions for installation via these methods can be found below the official approaches.

Helm now features an installation script that automatically retrieves the latest Helm version and installs it locally.

You can download this script and execute it locally. It is well-documented, allowing you to review it and comprehend its operations before running it.

```bash
curl -fsSL -o get_helm.sh https://raw.githubusercontent.com/helm/helm/main/scripts/get-helm-3
chmod 700 get_helm.sh
./get_helm.sh
```