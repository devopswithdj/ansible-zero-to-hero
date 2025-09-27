# Ansible Inventory
---

### What is Ansible Inventory 🛠️?
&nbsp;&nbsp;&nbsp;&nbsp;The inventory is the source of truth that tells Ansible which machines to manage and how to reach them.

- Think of it as a phonebook for your infrastructure.
- It lists hosts (servers, VMs, containers, network devices, etc.) and optional groups (web, db, prod, staging, etc.).

Without an inventory, Ansible wouldn’t know where to run your playbooks.

### 🤷‍♂️Why is it used?
| Purpose | Example|
| --- | --- |
| Define hosts | “Manage all web servers in aws us-east-1.” |
| Group hosts | Run tasks only on [db] group or [web] group. |
| Store variables | Set ansible_user=ubuntu or app_env=prod per host/group. |
| Dynamic scaling | Auto-discover servers from cloud providers (AWS, Azure, GCP, Kubernetes). |

In short:
Inventory = Target selection + Connection instructions + Variables.

### How It Works (Execution Flow)

1) Read inventory file:
Ansible loads inventory (default: /etc/ansible/hosts or specified with -i).

2) Parse groups and hosts:
Groups can be nested. Variables can live at host, group, or global level.

3) Match Playbook targets:
The hosts: keyword in your playbook is matched against inventory groups/hosts.

4) Connect & Execute:
Uses SSH (or other connection plugins) to run modules/tasks on matching hosts.

### Inventory Types
| Type| Description| Typical Use |
| --- | --- | --- |
| Static (INI/YAML)| Manually written list of servers.| Small/medium setups, quick demos. |
|Dynamic| Inventory is generated at runtime by a script or plugin (e.g., AWS, Azure, Kubernetes).| Auto-scaling environments, cloud-native infra. |
| Multiple Sources| Combine static + dynamic.| Hybrid setups. |
---

### Examples
#### A. Simple Static Inventory (INI format)

```code
inventory.ini

[web]
192.168.1.10 ansible_user=ubuntu ansible_port=22
192.168.1.11 ansible_user=ubuntu

[db]
db1.example.com ansible_user=postgres

[all:vars]
ansible_python_interpreter=/usr/bin/python3


Usage:

ansible -i inventory.ini web -m ping
ansible-playbook -i inventory.ini site.yml
```

#### B. Static Inventory (YAML format)

```code
inventory.yml

all:
  vars:
    ansible_python_interpreter: /usr/bin/python3
  children:
    web:
      hosts:
        web1:
          ansible_host: 192.168.1.10
          ansible_user: ubuntu
        web2:
          ansible_host: 192.168.1.11
    db:
      hosts:
        db1:
          ansible_host: db1.example.com
          ansible_user: postgres


Run:

ansible all -i inventory.yml -m ping
```

#### C. Dynamic Inventory (AWS EC2 example)

```code
Install plugin: pip install boto3

Create aws_ec2.yml:

plugin: amazon.aws.ec2
regions:
  - us-east-1
filters:
  tag:Environment: production
keyed_groups:
  - key: tags.Role
    prefix: ''


Use it:

ansible-inventory -i aws_ec2.yml --list
ansible-playbook -i aws_ec2.yml deploy.yml


Ansible queries AWS API and automatically lists all matching instances.
```