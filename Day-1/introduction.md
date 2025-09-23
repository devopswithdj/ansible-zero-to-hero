# 🚀 Ansible Zero to Hero – Day 1  

Welcome to **Ansible Zero to Hero**, a hands-on journey to learn Ansible from scratch and grow into advanced usage. This repository will guide you step by step with practical examples, explanations, and exercises.  

---

## 📌 What is Ansible?  

Ansible is an **open-source automation tool** used for:  
- ✅ Configuration Management  
- ✅ Application Deployment  
- ✅ Orchestration (managing multiple servers easily)  
- ✅ Infrastructure as Code (IaC)  

It helps you **automate repetitive tasks** and manage thousands of servers with simple **YAML playbooks**.  

---


## 📌 Why Ansible (vs Python or Shell scripts)?  

- ✅ Declarative vs Imperative – In Ansible, you describe the desired state (e.g., “user should exist”), while scripts require step-by-step instructions.

- ✅ Idempotency – Ansible ensures running the same playbook multiple times won’t break things. Scripts need extra checks and conditions.

- ✅ Scalability – Managing hundreds of servers with scripts is painful; Ansible is built to handle thousands easily.

- ✅ Readability & Maintainability – YAML playbooks are human-friendly, reusable, and easier to share than long scripts.

- ✅ Rich Ecosystem – Ansible provides 1000s of ready-to-use modules for cloud, networking, databases, and more — scripts require you to build everything yourself.

---


## 🛠️ Prerequisites  

Before diving in, make sure you have:  
- A **Linux system** (Ubuntu/Debian/CentOS) or **WSL** on Windows  
- Basic understanding of **Linux commands**  
- Python (Ansible convertes YAML files into Python files - So all nodes must have python installed)  

---

## 📦 Installing Ansible (Quick Start)  

### On Ubuntu/Debian  
```bash
sudo apt update
sudo apt install -y ansible
```

### On CentOS/RHEL
```bash
sudo yum install -y epel-release
sudo yum install -y ansible
```
### On Windows
```
1) Enable WSL
    Open PowerShell as Administrator and run:
        wsl --install

2) Install and open Ubuntu from Start Menu and run:
    sudo apt update && sudo apt upgrade -y

3) Install ansible
    Inside ubuntu terminal run
        sudo apt install -y ansible

```

