# Ansible Roles
---

### What is Ansible Role?

&nbsp;&nbsp;&nbsp;&nbsp;An Ansible role is a self-contained, reusable collection of tasks, variables, templates, files, and handlers organized in a standard directory structure.

Think of roles as modular building blocks:

Instead of writing one huge playbook, you break it into smaller, reusable components.

Each role performs a specific function (e.g., install Nginx, configure PostgreSQL, deploy an app).

<b>Analogy</b>:

Playbook = Recipe book
Role = Individual recipe (e.g., "How to bake a cake")

### Why use Ansible Roles?
- Reusability --&gt; Use the same role across multiple projects or environments.
- Maintainability --&gt; Easier to manage than giant monolithic playbooks.
- Collaboration --&gt; Teams can work on separate roles without conflicts.
- Scalability --&gt; Roles scale from small teams to large infrastructures.
- Community support --&gt; Ansible Galaxy offers thousands of ready-made roles.

### Standard Role Directory structure
```code
myrole/
├── defaults/        # Default variables (lowest precedence)
│   └── main.yml
├── vars/            # Variables with higher precedence
│   └── main.yml
├── tasks/           # Main list of tasks to execute
│   └── main.yml
├── handlers/        # Handlers (triggered by notify)
│   └── main.yml
├── templates/       # Jinja2 template files (.j2)
├── files/           # Static files to copy as-is
├── meta/            # Role metadata (dependencies, author, etc.)
│   └── main.yml
└── tests/           # Test inventory and playbooks

```

### Examples - Using nginx playbook from Day-3

1) Create a Role using <b><i>ansible-galaxy</i></b>
```ansible
ansible-galaxy init nginx

This creates below tree

├── nginx
│   ├── README.md
│   ├── defaults
│   │   └── main.yml
│   ├── files
│   ├── handlers
│   │   └── main.yml
│   ├── meta
│   │   └── main.yml
│   ├── tasks
│   │   └── main.yml
│   ├── templates
│   ├── tests
│   │   ├── inventory
│   │   └── test.yml
│   └── vars
│       └── main.yml
```

2) Add Tasks, Varaibles (if any)
```ansible

add tasks in nginx/tasks/main.yml

```

3) Call the Role from playbook
```ansible

- name: Install and configure Nginx
  hosts: web
  become: true # Run tasks with privilege escalation (e.g., sudo)
  roles:
    - nginx

```
4) Now simply run ansible-playbook
```ansible
ansible-playbook -i inventory.ini nginx-playbook.yaml
```

👌You have used Roles in Ansible

--&gt; Use Ansible Galaxy to easily import or export commonly used roles and use them in your projects.

`` Go through Ansible-Galaxy.md for more information on this 👍 ``