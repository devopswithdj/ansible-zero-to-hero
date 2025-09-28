# Setup AWS EC2 - Covers Roles, Collections, Variables & Vault

1) Complete steps provided in pre-requisite.md --&gt; this installs boto3 and sets up the vault password file & AWS Creds.

2)  Install required amazon aws collection from Ansible Galaxy https://galaxy.ansible.com/ui/repo/published/amazon/aws/
```cmd
ansible-galaxy collection install amazon.aws
```

3) setup a role - ec2 & setup a playbook.yaml --&gt; used later when setting up EC2
```cmd
cd Day-5

mkdir ec2-module

cd ec2-module

ansible-galaxy init ec2

touch ../../ec2-instance.yaml

tree

```

Running above commands should result in following tree structure

```cmd
.
├── collections.md
├── ec2-creation.md
├── ec2-module
│   ├── ec2
│   │   ├── README.md
│   │   ├── defaults
│   │   │   └── main.yml
│   │   ├── files
│   │   ├── handlers
│   │   │   └── main.yml
│   │   ├── meta
│   │   │   └── main.yml
│   │   ├── tasks
│   │   │   └── main.yml
│   │   ├── templates
│   │   ├── tests
│   │   │   ├── inventory
│   │   │   └── test.yml
│   │   └── vars
│   │       └── main.yml
│   ├── ec2-instance.yaml
│   ├── group_vars
│   │   └── all
│   │       └── pass.yml
│   └── vault.pass

```

4) Run the playbook after you update the tasks, vars and ec2-instance.yaml.
```cmd
ansible-playbook -i ../inventory.ini ec2-instance.yaml --vault-password-file vault.pass
```

😍Voila you have created EC2 instance using Ansible Galaxy Collections 🎉🎊!!!

⚠️Once testing is done don't forget to decommission the infrastructure 💵