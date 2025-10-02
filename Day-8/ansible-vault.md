# 🔐 Ansible Vault Cheatsheet

Ansible Vault is a feature that lets you **encrypt sensitive data** (like passwords, API keys, certificates) inside your Ansible projects.  
This prevents exposing secrets in plaintext when sharing or storing playbooks in version control.

---

## 📑 Table of Contents
- [1. What is Ansible Vault?](#1-what-is-ansible-vault)
- [2. Why is it Used?](#2-why-is-it-used)
- [3. How Does it Work?](#3-how-does-it-work)
- [4. Vault Commands](#4-vault-commands)
- [5. Using Vault in Playbooks](#5-using-vault-in-playbooks)
- [6. Example Workflow](#6-example-workflow)
- [7. Best Practices](#7-best-practices)
- [📌 Quick Reference](#-quick-reference)

---

## 1. What is Ansible Vault?
- A built-in Ansible tool to **encrypt files, variables, and secrets**.  
- Uses **AES256 encryption** by default.  
- Files stay encrypted at rest and are only decrypted **in memory** at runtime.  

---

## 2. Why is it Used?
- ✅ Protect sensitive information (passwords, tokens, keys).  
- ✅ Prevent secrets from being exposed in GitHub/Version Control.  
- ✅ Share playbooks securely across teams.  
- ✅ Meet compliance and security policies.  

---

## 3. How Does it Work?
- Encrypts files with a **vault password**.  
- At playbook execution, Ansible decrypts automatically (when given the password).  
- Supports both **full file encryption** and **inline variable encryption**.  

---

## 4. Vault Commands

### 🔹 Create a Vault File
```bash
ansible-vault create secrets.yml
```

### 🔹 Encrypt an Existing File
```bash
ansible-vault encrypt vars.yml
```

### 🔹 View Encrypted File
```bash
ansible-vault view secrets.yml
```

### 🔹 Edit Encrypted File
```bash
ansible-vault edit secrets.yml
```

### 🔹 Decrypt File
```bash
ansible-vault decrypt secrets.yml
```

### 🔹 Re-key (Change Password)
```bash
ansible-vault rekey secrets.yml
```

---

## 5. Using Vault in Playbooks

### Encrypted Variables File
```yaml
# secrets.yml (encrypted)
db_user: admin
db_password: myS3cretPass
```

### Playbook
```yaml
- hosts: dbservers
  vars_files:
    - secrets.yml
  tasks:
    - name: Configure Database
      mysql_user:
        name: "{{ db_user }}"
        password: "{{ db_password }}"
        priv: '*.*:ALL'
```

### Run with Vault
```bash
ansible-playbook db_setup.yml --ask-vault-pass
```
or
```bash
ansible-playbook db_setup.yml --vault-password-file ~/.vault_pass.txt
```

---

## 6. Example Workflow

1. Create secrets file:
   ```bash
   ansible-vault create secrets.yml
   ```

2. Add sensitive data (in editor):
   ```yaml
   api_key: "12345-SECRET"
   ```

3. Reference it in playbook:
   ```yaml
   - hosts: web
     vars_files:
       - secrets.yml
     tasks:
       - name: Use secret
         debug:
           msg: "API Key is {{ api_key }}"
   ```

4. Run with password prompt:
   ```bash
   ansible-playbook web.yml --ask-vault-pass
   ```

---

## 7. Best Practices
- 🔒 Store **vault password** securely (never commit it to Git).  
- 🔒 Use `--vault-password-file` for automation (CI/CD pipelines).  
- 🔒 Encrypt only what’s necessary (keep playbooks readable).  
- 🔒 Consider external secret managers (AWS Secrets Manager, Azure Key Vault, HashiCorp Vault) for enterprise usage.  
- 🔒 Rotate Vault passwords periodically.  

---

## 📌 Quick Reference

| Command                        | Purpose                               |
|--------------------------------|---------------------------------------|
| `ansible-vault create file.yml` | Create new encrypted file             |
| `ansible-vault encrypt file.yml` | Encrypt existing file                 |
| `ansible-vault view file.yml`   | View encrypted file                   |
| `ansible-vault edit file.yml`   | Edit encrypted file                   |
| `ansible-vault decrypt file.yml` | Decrypt file                          |
| `ansible-vault rekey file.yml`  | Change vault password                 |
| `--ask-vault-pass`             | Prompt for password at runtime        |
| `--vault-password-file`        | Use password file (automation)        |

---
