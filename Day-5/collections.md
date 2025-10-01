### 1️⃣ What Are Ansible Collections?

An Ansible Collection is a packaged bundle of Ansible content:

- Modules (tasks that do work)

- Plugins (connection, lookup, filter, etc.)

- Roles (reusable sets of tasks and variables)

- Documentation & Tests

Think of a collection as a “container of automation content”
- larger and more flexible than a single role.

### 2️⃣ Why Use Collections?
| Benefit | Explanation |
| --- | --- |
| Modularity | Ship modules, roles, and plugins together as one versioned artifact. |
| Distribution | Publish to Ansible Galaxy or a private repo for easy sharing. |
| Versioning | Install specific versions (namespace.collection_name:1.2.3) to keep environments consistent. |
| Isolation | Different teams or vendors can maintain their own code independently of core Ansible. |

### 3️⃣ Key Differences: Roles vs. Collections
| Aspect | Role | Collection |
| --- | --- | --- |
| Scope | Tasks, templates, vars | Roles plus modules plugins, docs, tests |
| Packaging | Single folder | Versioned Python-style package with galaxy.yml |
| Distribution | Galaxy roles section | Galaxy collections section or private automation hub |
| Versioning | Optional tags/branches | Strict semantic versioning (e.g., 2.5.1) |

✅ Roles are great for configuration; collections shine when you need custom modules or plugins too.

### 4️⃣ Directory Structure of a Collection

A minimal collection might look like:

```collections
my_namespace/
└── my_collection/
    ├── README.md
    ├── galaxy.yml            # Metadata: name, version, dependencies
    ├── plugins/
    │   ├── modules/          # Custom modules
    │   └── filters/
    ├── roles/
    │   └── webserver/        # Regular Ansible role
    └── docs/
```

### 5️⃣ Installing a Collection

1) From Galaxy (Public)
```cmd
ansible-galaxy collection install community.general
ansible-galaxy collection list          # verify
```

2) From a Specific Version
```cmd
ansible-galaxy collection install amazon.aws:==5.5.0
```

3) From a Requirements File (Recommended)

requirements.yml
```cmd
collections:
  - name: community.general
    version: "7.3.0"
  - name: amazon.aws
    version: "5.5.0"
```

Install all:
```cmd
ansible-galaxy collection install -r requirements.yml
```

### 6️⃣ Using a Collection in a Playbook

Call modules or roles with the FQCN (Fully Qualified Collection Name):
```cmd
- hosts: localhost
  tasks:
    - name: Create an S3 bucket
      amazon.aws.s3_bucket:
        name: my-bucket
        state: present

    - name: Use a community.general role
      ansible.builtin.include_role:
        name: community.general.apache
```

- Collection = packaged automation (modules, roles, plugins) with semantic versioning.

- Install with ansible-galaxy collection install <namespace.collection>.

<i>"Collections are the modern standard for distributing and consuming Ansible automation at scale."</i>