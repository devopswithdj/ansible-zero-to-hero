# 🚀 Ansible Zero to Hero

Welcome to **Ansible Zero to Hero**, a hands-on journey to learn Ansible from scratch and grow into advanced usage. This repository guides you step by step with practical examples, explanations, and exercises.

---

## 📚 Table of Contents

- [Introduction](Day-1/introduction.md)
- [Day 2: Passwordless Authentication](Day-2/passwordless-authentication.md)
- [Day 3: Inventory Management](Day-3/inventory.md)
- [Day 4: Roles & Ansible Galaxy](Day-4/Roles.md) | [Ansible Galaxy](Day-4/Ansible-Galaxy.md)
- [Day 5: AWS EC2 Automation, Collections, Vault](Day-5/ec2-creation.md) | [Collections](Day-5/collections.md) | [Pre-requisites](Day-5/pre-requisite.md)
- [Day 6: EC2 Management Playbooks](Day-6/create_ec2.yaml)
- [Day 7: Error Handling](Day-7/error-handling.md)
- [Day 8: Ansible Vault](Day-8/ansible-vault.md)
- [Assets](assets/)

---

## 📝 What You'll Learn

- **Ansible Basics:** What is Ansible, why use it, and how to install it.
- **Inventory Management:** Static and dynamic inventories, grouping, and variables.
- **Roles & Reusability:** Modularizing playbooks with roles and using Ansible Galaxy.
- **AWS Automation:** Creating and managing EC2 instances using Ansible collections and vault for secrets.
- **Error Handling:** Making playbooks resilient and predictable.
- **Security:** Encrypting secrets with Ansible Vault.
- **Best Practices:** Structure, idempotency, and collaboration.

---

## 🛠️ Getting Started

1. **Clone the Repository**
   ```sh
   git clone https://github.com/yourusername/ansible-zero-to-hero.git
   cd ansible-zero-to-hero
   ```

2. **Install Ansible**
   - [See Introduction for OS-specific instructions](Day-1/introduction.md)

3. **Set Up Passwordless SSH**
   - [Follow Day 2 instructions](Day-2/passwordless-authentication.md)

4. **Explore and Run Playbooks**
   - Inventories and playbooks are organized by day for progressive learning.
   - Example:
     ```sh
     ansible-playbook -i Day-3/inventory.ini Day-3/nginx-playbook.yaml
     ```

5. **AWS Automation**
   - [See Day 5 for EC2 setup and vault usage](Day-5/ec2-creation.md)

---

## 💡 References

- [Official Ansible Documentation ↗️](https://docs.ansible.com/)
- [Ansible GitHub](https://github.com/ansible/ansible)

---

## 🤝 Contributing

Pull requests and suggestions are welcome! Please open an issue first to discuss what you would like to change.

---

Happy Automating! 🎉
