---
title: Ansible Playbooks
layout: home
nav_order: 1
parent: Ansible
has_children: true
permalink: docs/ansible/playbooks
last_modified_date: 2024-01-13
---

# Ansible Playbooks

Ansible playbooks are written in YAML and consist of plays, which are a set of tasks to be executed on remote hosts. Each task can include modules, which are pre-built, reusable units of code. Playbooks can also define variables, handlers, and roles to organize and reuse tasks. Additionally, Ansible provides conditionals, loops, and error handling within playbooks. Finally, playbooks can be run using the ansible-playbook command-line tool.

Ansible playbooks are designed to be idempotent, meaning they can be run multiple times without changing the system state if the desired state is already achieved. Playbooks can also leverage Jinja2 templating for dynamic content and can include various built-in and custom modules to perform tasks such as package installation, file manipulation, service management, and more. Additionally, playbooks support the use of roles to encapsulate and reuse sets of tasks, making playbook organization and maintenance more manageable.

Ansible playbooks are a key component of infrastructure as code (IaC) and are used to automate the deployment, configuration, and orchestration of IT infrastructure. They enable the definition of complex, multi-step processes in a declarative manner, allowing for consistent and repeatable provisioning and management of systems. Additionally, playbooks can be integrated with version control systems and CI/CD pipelines to facilitate continuous delivery and deployment practices.

## Hello World

```yaml
---
# This playbook prints a simple debug message
- name: Hello World
  hosts: localhost
  connection: local

  tasks:
  - name: Print debug message
    debug:
      msg: Hello, world!
```

1. It defines a play with the name "Hello World" that targets the "localhost" and uses a local connection.

2. Within the play, there is a single task defined under the "tasks" section.

3. The task is named "Print debug message" and it uses the "debug" module to print the message "Hello, world!".

So, this playbook essentially executes a single task that prints the message "Hello, world!" when run on the localhost using a local connection.

![hello-world](https://user-cube.github.io/devops-cheatsheet/assets/images/ansible/ansible-hello-world.png)
