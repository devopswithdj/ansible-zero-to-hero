### 1️⃣ What Is Ansible Galaxy?

Ansible Galaxy is:

🏪 <b>Public Repository / Marketplace</b>
A central hub for finding, sharing, and downloading reusable roles and collections for Ansible.

🛠️ <b>CLI Tool</b>
The ansible-galaxy command helps you create, publish, and manage roles or collections.

Think of it as GitHub for Ansible automation content.

### 2️⃣ Why Use Ansible Galaxy?
| Benefit | Description |
|---|---|
| Reuse | Skip writing common automation from scratch (e.g., Nginx, Docker, Kubernetes). |
| Community-driven | Thousands of open-source roles maintained by experts. |
| Standardization | Roles follow a consistent structure. |
| Private sharing | You can host internal Galaxy servers for your team. |

### 3️⃣ Two Key Concepts

Roles
Self-contained automation units (tasks, vars, templates).
Example: geerlingguy.nginx installs and configures Nginx.

Collections
Bundles of roles, modules, and plugins.
Example: amazon.aws includes AWS modules, plugins, and roles.

### 4️⃣ How It Works

Browse / Search
Visit https://galaxy.ansible.com
 to find roles/collections.

Install
Use <i>ansible-galaxy install or ansible-galaxy collection install </i>to pull content.

Reference in Playbooks
Call the role/collection directly in your playbook.

### 5️⃣ Installing Roles from Galaxy
```ansible
ansible-galaxy install <namespace>.<role_name>
```

Example:
```cmd
ansible-galaxy install geerlingguy.nginx
```

This downloads the role to the default ~/.ansible/roles/ directory.

To specify a custom path:

ansible-galaxy install -p roles/ geerlingguy.nginx

### 6️⃣ Using a Galaxy Role in a Playbook

```ansible
- hosts: web
  become: yes
  roles:
    - geerlingguy.nginx
```

Then run:
```ansible
ansible-playbook -i inventory.ini site.yml
```

### Example

#### Installing docker using ansible galaxy role
1) Create a account in https://galaxy.ansible.com/ by attaching github
2) use below command to install required role
```cmd
ansible-galaxy role install grzegorzfranus.docker
```
3) Create a playbook - docker-installation.yaml
```
docker-installation.yaml

---
- name: Install docker
  hosts: web
  become: true
  roles:
    - grzegorzfranus.docker


```
4) Apply the playbook and see the results on your Virtual Machine
```
ansible-playbook -i inventory.ini docker-installation.yaml
```

❤️You have setup docker on your servers just using Ansible Galaxy Roles !!!.