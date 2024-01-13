---
title: K9S
layout: home
grand_parent: Tools & Tips
parent: Tools
nav_order: 1
permalink: docs/tols-and-tips/tools/k9s
last_modified_date: 2024-01-09
---

# K9S

K9s is a terminal based UI for interacting with Kubernetes clusters. The project's goal is to simplify navigation, observation, and management of deployed applications in Kubernetes. K9s continuously monitors Kubernetes for changes and provides commands to interact with observed resources.

## Table of contents

## Features

- Information At Your Fingertips!
    - Real-time tracking of activities of resources running in your Kubernetes cluster.
- Standard or CRD?
    - Handling both Kubernetes standard resources and custom resource definitions.
- Cluster Metrics
    - Real-time tracking of metrics associated with resources such as pods, containers, and nodes.
- Power Users Welcome!
    - Providing standard cluster management commands such as logs, scaling, port-forwards, restarts…
    - Defining your own command shortcuts for quick navigation via command aliases and hotkeys.
    - Plugin support to extend K9s to create your very own cluster commands.
    - Powerful filtering mode to allow users to drill down and view workload-related resources.
- Error Zoom
    - Directly drill down to what’s wrong with your cluster’s resources.
- Skinnable and Customizable
    - Defining your very own look and feel via K9s skins.
    - Customizing/arranging which columns to display on a per-resource basis.
- Narrow or Wide?
    - Providing toggles to view minimal or full resource definitions
- MultiResources Views
    - Providing an overview of your cluster resources via Pulses and XRay views.
- We’ve got your RBAC!
    - Support for viewing RBAC rules such as cluster/roles and their associated bindings.
    - Reverse lookup to assert what a user/group or ServiceAccount can do on your clusters.

- Built-in Benchmarking
    - Benchmarking your HTTP services/pods directly from K9s to see how your application fares and adjust your resource requests/limits accordingly.
- Resource Graph Traversals
    - K9s provides easy traversal of Kubernetes resources and their associated resources.

## Setup and Install

To install K9S, please follow the instructions on the K9S confluence page.
To set up K9S to use the Kubernetes cluster, you need to configure the KUBECONFIG file. Please follow the setup guide present in the following confluence page: Kubernetes. If you are using multiple clusters, please follow the documentation for Configure Access to Multiple Clusters.
**Note**: The K9S tool is installed on the Kubernetes master node.

## Launch K9S

```bash
k9s
```

![k9s](https://user-cube.github.io/devops-cheatsheet/assets/images/tools/k9s-execute.png)

## Interact with K9S

### CLI Arguments

K9s CLI comes with various arguments that you can use to launch the tool with different configurations.

```bash
# List all available CLI options
k9s help
# Get info about K9s runtime (logs, configs, etc..)
k9s info
# Run K9s in a given namespace.
k9s -n mycoolns
# Run K9s and launch in pod view via the pod command.
k9s -c pod
# Start K9s in a non-default KubeConfig context
k9s --context coolCtx
# Start K9s in readonly mode - with all modification commands disabled
k9s --readonly
```

| Action                                                                         | Command                     | Comment                                                                |
|--------------------------------------------------------------------------------|-----------------------------|------------------------------------------------------------------------|
| Show active keyboard mnemonics and help                                        | ?                           |                                                                        |
| Show all available resource aliases                                             | ctrl-a                      |                                                                        |
| To exit K9s                                                                     | :q, ctrl-c                  |                                                                        |
| View a Kubernetes resource using singular/plural or short-name                 | :pod⏎                       | accepts singular, plural, short-name, or alias, i.e., pod or pods       |
| View a Kubernetes resource in a given namespace                                | :pod ns-x⏎                  |                                                                        |
| View filtered pods (New v0.30.0!)                                              | :pod /fred⏎                 | View all pods filtered by fred                                         |
| View labeled pods (New v0.30.0!)                                               | :pod app=fred,env=dev⏎      | View all pods with labels matching app=fred and env=dev                |
| View pods in a given context (New v0.30.0!)                                    | :pod @ctx1⏎                 | View all pods in context ctx1. Switches out your current k9s context!  |
| Filter out a resource view given a filter                                      | /filter⏎                    | Regex2 supported, i.e., fred\|blee, to filter resources named fred or blee|
| Inverse regex filter                                                           | /! filter⏎                  | Keep everything that doesn’t match.                                    |
| Filter resource view by labels                                                 | /-l label-selector⏎         |                                                                        |
| Fuzzy find a resource given a filter                                           | /-f filter⏎                 |                                                                        |
| Bails out of view/command/filter mode                                          | <esc>                       |                                                                        |
| Key mapping to describe, view, edit, view logs,…                               | d,v, e, l,…                 |                                                                        |
| To view and switch to another Kubernetes context (Pod view)                    | :ctx⏎                       |                                                                        |
| To view and switch directly to another Kubernetes context (Last used view)     | :ctx context-name⏎          |                                                                        |
| To view and switch to another Kubernetes namespace                             | :ns⏎                        |                                                                        |
| To view all saved resources                                                    | :screendump or sd⏎          |                                                                        |
| To delete a resource (TAB and ENTER to confirm)                                | ctrl-d                      |                                                                        |
| To kill a resource (no confirmation dialog, equivalent to kubectl delete –now) | ctrl-k                      |                                                                        |
| Launch pulses view                                                             | :pulses or pu⏎              |                                                                        |
| Launch XRay view                                                               | :xray RESOURCE [NAMESPACE]⏎ | RESOURCE can be one of po, svc, dp, rs, sts, ds, NAMESPACE is optional |
| Launch Popeye view                                                             | :popeye or pop⏎             | See popeye                                                             |