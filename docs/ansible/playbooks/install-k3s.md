---
title: Install K3S and tools
layout: home
nav_order: 2
grand_parent: Ansible
parent: Ansible Playbooks
permalink: docs/ansible/playbooks/install-k3s-and-tools
last_modified_date: 2024-04-21
---

# Ansible Playbook: Install Kubernetes Locally

This Ansible playbook automates the installation of Kubernetes locally using k3s, as well as additional tools such as k9s and Helm.

## Requirements

- Ansible installed on the control machine
- `sudo` privileges on the target machine
- Internet access on the target machine

## How to Use

1. Clone this repository:

```bash
git clone https://github.com/user-cube/ansible-playbooks.git
```

2. Navigate to the playbook directory:

```bash
cd ubuntu/k3s/
```

3. Edit the `hosts` file to specify the target host where you want to install Kubernetes locally.

4. Run the playbook:

```bash
ansible-playbook k3s.yml
```

5. Once the playbook execution is complete, you should have Kubernetes installed locally, along with k9s and Helm.

## Customization

- Modify the playbook variables as needed to customize the installation process.
- Adjust the playbook tasks to suit your environment and requirements.

## Notes

- This playbook assumes you are running it on a Linux-based system.
- Ensure you have sufficient permissions and network access for the installation process to complete successfully.
- Review the playbook tasks and verify they meet your security and operational requirements.

## Code

You can find this code on [ansible-playbooks](https://github.com/user-cube/ansible-playbooks) repo.

```yaml
---
- name: Install Kubernetes Locally
  hosts: localhost
  become: yes
  become_method: sudo

  tasks:

    # Install k3s
    - name: Download k3s installation script
      get_url:
        url: "https://get.k3s.io"
        dest: "/tmp/install_k3s.sh"

    - name: Execute k3s installation script
      shell: "/bin/bash /tmp/install_k3s.sh"
      args:
        creates: /etc/rancher/k3s/k3s.yaml
      register: k3s_install_output
      environment:
        K3S_KUBECONFIG_MODE: "644"
        INSTALL_K3S_EXEC: "--disable=traefik"

    - debug:
        msg: "{{ k3s_install_output.stdout_lines }}"

    - name: Get user's home directory
      set_fact:
        user_home: "{% raw %} {{ lookup('env', 'HOME') }}{% endraw %}"
    
    - name: Create .kube directory
      file:
        path: "{{ user_home }}/.kube"
        state: directory
        owner: "{% raw %} {{ lookup('env', 'USER') }}{% endraw %}"
      become: no
    
    - name: Append export command to shell config
      ansible.builtin.lineinfile:
        path: "{{ user_home }}/.{{ shell_config }}"
        line: "export KUBECONFIG=~/.kube/config"
        insertafter: EOF
      become: no
      vars:
        shell_config: "{% raw %}{{ 'bashrc' if ansible_env.SHELL | regex_search('bash') else 'zshrc' }}{% endraw %}"

    # Copy k3s configuration to user's home directory
    - name: Copy k3s configuration to user's home directory
      copy:
        src: "/etc/rancher/k3s/k3s.yaml"
        dest: "{{ user_home }}/.kube/config"
        remote_src: yes
        owner: "{% raw %}{{ lookup('env', 'USER') }}{% endraw %}"
        mode: '0600'

    # Setup alias for kubectl
    - name: Append export command to shell config
      ansible.builtin.lineinfile:
        path: "{{ user_home }}/.{{ shell_config }}"
        line: "{{ item }}"
        insertafter: EOF
      become: no
      loop:
        - "alias k=kubectl"
        - "setNS() { kubectl config set-context --current --namespace=\"$@\" ; }"
      vars:
        shell_config: "{% raw %}{{ 'bashrc' if ansible_env.SHELL | regex_search('bash') else 'zshrc' }}{% endraw %}"
    
    # Install K9S
    - name: Install required packages
      apt:
        name: "{{ item }}"
        state: present
      loop:
        - wget
        - unzip
      tags:
        - k9s

    - name: Find latest k9s release version
      uri:
        url: "https://api.github.com/repos/derailed/k9s/releases/latest"
        return_content: yes
      register: latest_release
      tags:
        - k9s

    - name: Extract latest k9s release version
      set_fact:
        k9s_version: "{{ latest_release.json.tag_name }}"
      tags:
        - k9s

    - name: Download k9s binary
      get_url:
        url: "https://github.com/derailed/k9s/releases/download/{{ k9s_version }}/k9s_Linux_amd64.tar.gz"
        dest: "/tmp/k9s.tar.gz"
        mode: '0644'
      tags:
        - k9s

    - name: Extract k9s binary
      unarchive:
        src: "/tmp/k9s.tar.gz"
        dest: "/usr/local/bin"
        remote_src: yes
      tags:
        - k9s

    - name: Make k9s executable
      file:
        path: "/usr/local/bin/k9s"
        mode: '0755'
      tags:
        - k9s

    # Install helm
    - name: Install required dependencies
      package:
        name: "{{ item }}"
        state: present
      loop:
        - curl
        - tar

    - name: Fetch latest Helm version
      uri:
        url: https://api.github.com/repos/helm/helm/releases/latest
        return_content: yes
      register: helm_latest_release

    - set_fact:
        helm_version: "{% raw %}{{ helm_latest_release.json.tag_name | regex_replace('^v', '') }}{% endraw %}"

    - name: Download Helm binary
      get_url:
        url: "https://get.helm.sh/helm-v{{ helm_version }}-linux-amd64.tar.gz"
        dest: "/tmp/helm-v{{ helm_version }}-linux-amd64.tar.gz"

    - name: Extract Helm binary
      ansible.builtin.unarchive:
        src: "/tmp/helm-v{{ helm_version }}-linux-amd64.tar.gz"
        dest: /usr/local/bin
        remote_src: yes
        creates: "/usr/local/bin/linux-amd64/helm"

    - name: Ensure Helm binary is executable
      file:
        path: /usr/local/bin/helm
        state: link
        src: /usr/local/bin/linux-amd64/helm
        mode: u+x

    - name: Verify Helm installation
      command: helm version
      register: helm_version_output

    - debug:
        var: helm_version_output.stdout_lines
```