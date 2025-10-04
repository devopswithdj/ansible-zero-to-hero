# 🛡️ Policy as Code (PaC) with Ansible

Policy as Code (PaC) is the practice of defining, managing, and enforcing security, compliance, and governance policies **in code**.  
With Ansible, you can codify these rules as playbooks or roles to automatically apply and enforce them across infrastructure.

---

## 📑 Table of Contents
- [1. What is Policy as Code?](#1-what-is-policy-as-code)
- [2. Why Use Policy as Code?](#2-why-use-policy-as-code)
- [3. How It Works with Ansible](#3-how-it-works-with-ansible)
- [4. Example Policies in Ansible](#4-example-policies-in-ansible)
  - [Security Policy](#-security-policy---ssh-settings)
  - [Compliance Policy](#-compliance-policy---package-versions)
  - [Access Policy](#-access-policy---user-accounts)
- [5. CI/CD Integration](#5-cicd-integration)
- [6. Best Practices](#6-best-practices)
- [📌 Quick Reference](#-quick-reference)
- [🧑‍🏭 Use case](#-use-case)

---

## 1. What is Policy as Code?
- Policies are **codified as YAML/Ansible playbooks** instead of being manual documents.  
- Enforced automatically at scale across environments.  
- Examples: Security rules, compliance checks, access control, configuration standards.

---

## 2. Why Use Policy as Code?
- ✅ **Consistency** – Same rules across all servers.  
- ✅ **Automation** – Removes manual checks.  
- ✅ **Auditability** – Policies live in Git, with history.  
- ✅ **Shift-Left Security** – Catch issues earlier.  
- ✅ **Scalability** – Works across 100s or 1000s of machines.

---

## 3. How It Works with Ansible
- Policies are written as **playbooks** or **roles**.  
- Run them regularly (cron, Tower/AWX, CI/CD).  
- They can **enforce** (fix drift) or just **audit** (report violations).  

---

## 4. Example Policies in Ansible

### 🔹 Security Policy – SSH Settings
```yaml
- name: Enforce Security Policy on SSH
  hosts: all
  become: yes
  tasks:
    - name: Ensure root login is disabled
      lineinfile:
        path: /etc/ssh/sshd_config
        regexp: '^PermitRootLogin'
        line: 'PermitRootLogin no'

    - name: Ensure password authentication is disabled
      lineinfile:
        path: /etc/ssh/sshd_config
        regexp: '^PasswordAuthentication'
        line: 'PasswordAuthentication no'

    - name: Restart SSH service
      service:
        name: sshd
        state: restarted
```

---

### 🔹 Compliance Policy – Package Versions
```yaml
- name: Enforce compliance - ensure correct package version
  hosts: all
  become: yes
  tasks:
    - name: Ensure OpenSSL is latest
      package:
        name: openssl
        state: latest
```

---

### 🔹 Access Policy – User Accounts
```yaml
- name: Enforce user policy
  hosts: all
  become: yes
  tasks:
    - name: Ensure only approved users exist
      user:
        name: "{{ item }}"
        state: present
      loop:
        - devuser
        - adminuser

    - name: Ensure disallowed users are absent
      user:
        name: badactor
        state: absent
```

---

## 5. CI/CD Integration
- Run `ansible-playbook` inside Jenkins, GitHub Actions, or GitLab CI.  
- Fail the pipeline if **policy drift** is detected.  
- Combine with:
  - **Ansible Lint** (YAML standards).  
  - **Open Policy Agent (OPA)** for advanced governance.  

---

## 6. Best Practices
- ✅ Store policies in **Git (GitOps)**.  
- ✅ Separate **enforcement** (fix issues) vs. **audit** (report only).  
- ✅ Encrypt sensitive variables with **Ansible Vault**.  
- ✅ Use **roles & collections** for modular policies.  
- ✅ Integrate with **external PaC tools** (OPA, Sentinel, Kyverno).  

---

## 📌 Quick Reference

| Concept | Example |
|---------|---------|
| **Security Policy** | Disable root login, disable password auth |
| **Compliance Policy** | Enforce latest package versions |
| **Access Policy** | Allow only specific users |
| **CI/CD** | Run Ansible policies in pipelines |
| **Storage** | Keep policies in Git, version controlled |
| **Tools** | Ansible Vault, Ansible Lint, OPA |

---
## 🧑‍🏭 Use case
- Setup PaC using Ansible to update versioning of all buckets to enabled.
