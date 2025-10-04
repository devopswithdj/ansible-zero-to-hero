# Ansible Error Handling

Error handling in Ansible allows you to control how playbooks behave when tasks fail.  
By default, if a task fails on a host, Ansible **stops executing further tasks on that host**.  
With error handling mechanisms, you can make playbooks more **resilient**, **controlled**, and **predictable**.

---

## 📑 Table of Contents
- [1. Default Behavior](#1-default-behavior)
- [2. Ignoring Errors](#2-ignoring-errors)
- [3. Custom Failure Conditions (`failed_when`)](#3-custom-failure-conditions-failed_when)
- [4. Example Use Case](#4-example-use-case)
---

## 1. Default Behavior
- A failed task stops execution on that host.
- Other hosts continue execution independently.

---

## 2. Ignoring Errors
Use `ignore_errors: yes` to continue even if a task fails.

```yaml
- name: Install optional package
  apt:
    name: optionalpkg
    state: present
  ignore_errors: yes
```

## 3. Custom Failure Conditions (`failed_when`)
Define custom logic for failure.

```yaml
- name: Check /etc/passwd
  command: cat /etc/passwd
  register: result
  failed_when: "'root' not in result.stdout"
```

## 4. Example Use Case
--&gt; Check if the instances have latest openssl and openssh installed, if not ignore them.
    - Then check if docker is installed or not
    - Then only if docker is not installed, install it.

Hint: Use conditionals to check the docker version.

✅Solution can be found in error-handling.yaml
