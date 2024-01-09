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

The Helm project provides two ways to fetch and install Helm. These are the official methods to get Helm releases. In addition to that, the Helm community provides methods to install Helm through different package managers. Installation through those methods can be found below the official methods.

Helm now has an installer script that will automatically grab the latest version of Helm and install it locally.

You can fetch that script, and then execute it locally. It's well documented so that you can read through it and understand what it is doing before you run it.

```bash
curl -fsSL -o get_helm.sh https://raw.githubusercontent.com/helm/helm/main/scripts/get-helm-3
chmod 700 get_helm.sh
./get_helm.sh
```