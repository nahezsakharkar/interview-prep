---
title: "Ansible Automation"
tags: ["devops","automation","ansible"]
difficulty: medium
status: revised
last_reviewed: 2026-10-02
---

# Ansible Automation

## Definition

Ansible is an open-source automation tool used for configuration management, application deployment, and task orchestration. Unlike Chef or Puppet, Ansible is **agentless**, meaning it doesn't require any software to be installed on the target nodes.

## Core Concepts

### 1. Agentless Architecture
Ansible connects to target nodes via **SSH** (for Linux) or **WinRM** (for Windows). It pushes small programs called "modules" to the target, executes them, and then removes them.

### 2. Playbooks
Playbooks are YAML files that describe the desired state of a system. They are **idempotent**, meaning if you run the same playbook twice, the second run will do nothing if the system is already in the desired state.

### 3. Inventory
An inventory file lists the hosts and groups that Ansible manages.
Example:
```ini
[webservers]
web1.example.com
web2.example.com

[dbservers]
db1.example.com
```

## Working Code Example: Web Server Setup

This playbook ensures that Nginx is installed, started, and that a custom HTML file is deployed.

```yaml
---
- name: Setup Web Servers
  hosts: webservers
  become: yes # Run as sudo
  tasks:
    - name: Install Nginx
      apt:
        name: nginx
        state: present
        update_cache: yes

    - name: Ensure Nginx is running
      service:
        name: nginx
        state: started
        enabled: yes

    - name: Deploy custom index.html
      copy:
        src: ./files/index.html
        dest: /var/www/html/index.html
        mode: '0644'
```

**Complexity**:
- **Time**: $O(H \cdot T)$ where $H$ is the number of hosts and $T$ is the number of tasks.
- **Space**: $O(1)$ on the target node (temporary module execution).

## Advanced Ansible Patterns

### 1. Roles
Roles allow you to break a playbook into reusable components (tasks, handlers, templates, vars). This is the standard way to organize large-scale automation.

### 2. Ansible Vault
Used to encrypt sensitive data (like API keys or DB passwords) within the playbook.
- Command: `ansible-vault encrypt vars/secrets.yml`

### 3. Handlers
Handlers are tasks that only run if a previous task notifies them.
**Example**: Restart Nginx only if the configuration file changed.
```yaml
- name: Copy nginx config
  template:
    src: nginx.conf.j2
    dest: /etc/nginx/nginx.conf
  notify: Restart Nginx

handlers:
  - name: Restart Nginx
    service:
      name: nginx
      state: restarted
```

## Interview questions

### Q1: What does "idempotency" mean in the context of Ansible?
**Model answer**: Idempotency means that applying an operation multiple times has the same effect as applying it once. In Ansible, a module checks the current state of the system first. If the system already matches the desired state (e.g., the package is already installed), the module does nothing. This prevents unnecessary restarts and configuration drifts.

### Q2: Why is Ansible's agentless architecture an advantage?
**Model answer**: It reduces the operational overhead and security risk. There is no need to install, update, or manage a client agent on every server. As long as the server has SSH and Python, Ansible can manage it.

### Q3: How do you handle secrets in Ansible?
**Model answer**: I use **Ansible Vault** to encrypt sensitive variables. The encrypted file is committed to Git, and the decryption password is provided at runtime via a password file or a prompt, ensuring that secrets are never stored in plain text.

### Q4: What is the difference between a Playbook and a Role?
**Model answer**: A Playbook is a single file (or a set of files) that maps hosts to tasks. A Role is a structured way to package those tasks, variables, and templates into a reusable directory format, allowing the same "role" (e.g., `common-security`) to be applied to different projects.

### Q5: How do you manage different environments (Dev/Prod) with one playbook?
**Model answer**: I use **Inventory Variables**. I create separate `group_vars` files for `dev` and `prod` (e.g., `group_vars/dev.yml` and `group_vars/prod.yml`). The playbook uses variables (e.g., `{{ db_host }}`), and Ansible loads the correct value based on which host group is being targeted.

## Related notes

- [CI/CD Strategies](../08-devops/ci-cd.md)
- [Jenkins](../08-devops/jenkins.md)
- [Linux Commands](../08-devops/linux-commands-cheat-sheet.md)
