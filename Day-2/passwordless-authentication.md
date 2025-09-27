# 🔑Passwordless Authentication

---

### ❓ What is it?  

Passwordless authentication allows you to log in to remote servers using **SSH keys or Passwords** instead of typing passwords or passing key files each time.  

### 🤔 Why does Ansible need it?  

- Ansible connects to servers using **SSH**.  
- Without passwordless login, you would need to type your password or pass private key file for **every server, every task** → which is not practical.  
- Once password less authority is provided to control node -  automation becomes smooth, secure, and faster.  

---

### ⚙️ How to Set It Up?  

**Passwordless Authentication needs to be configured on the Control Node.**

1. **For Servers using SSH Keys as login mechanism**

```bash
ssh-copy-id -f "-o IdentityFile <PATH TO PEM FILE>" ubuntu@<INSTANCE-PUBLIC-IP>
```

The options have the following meaning:

- -f Don't check if the key is already configured as an authorized key on the server. Just add it. This can result in multiple copies of the key in authorized_keys files.
- -o ssh_option Pass -o ssh_option to the SSH client when making the connection. This can be used for overriding configuration settings for the client. See ssh command line options and the possible configuration options in ssh_config.
- ubuntu@&lt;INSTANCE-IP&gt;: This is the username (ubuntu) and the IP address of the remote server you want to access.

2. **Setup a new key if you do not have any key files setup previosuly**
```bash
ssh-keygen -t rsa -b 4096 #this adds a id_rsa.pub file
```

3. **For Servers using Passwords as login mechanism**

- Simply login to the machine from control node using below command and enter password when prompted

```bash
ssh-copy-id <username>@<Instance-IP>
```

- 🎃For AWS - By default password authentication is disabled - In order to enable it and setup passwordless authentication, you need to update ssh config in `/etc/ssh/ssh_config` or any related folders.
  - Go to the file `/etc/ssh/sshd_config.d/60-cloudimg-settings.conf`
  - Update `PasswordAuthentication yes`
  - Restart SSH -> `sudo systemctl restart ssh`

4. **To Test the Passwordless login use below command**

```bash
ssh <username>@<Instance-IP>
```

🥳 Voila! You have setup the communication between Control nodes and Managed nodes without any authentication.