# 🐧 Linux SSH & SCP Lab

In this lab, I explored **remote login and secure file transfer** using SSH and SCP. The lab involved setting up passwordless SSH between systems, inspecting default SSH ports, and securely copying files.

---

## 📋 Lab Overview

**Goal:**

* Understand SSH basics and default port usage
* Establish passwordless SSH login using key pairs
* Copy files between systems securely with SCP
* Know key file locations on Linux systems

**Learning Outcomes:**

* Use `ssh` to connect to remote systems
* Generate SSH key pairs with `ssh-keygen`
* Copy public keys to target servers with `ssh-copy-id`
* Copy files securely using `scp`
* Identify where public keys are stored (`authorized_keys`)

---

## 🛠 Step-by-Step Journey

### Step 1: SSH Basics

* Default SSH port: **22**
* Connecting to remote server as current user:

```bash
ssh <username>@<remote_server>
```

* For this lab, connecting as user `bob`:

```bash
ssh bob@devapp01
```

---

### Step 2: Passwordless SSH Setup

1. Generate SSH key pair on **local system**:

```bash
ssh-keygen -t rsa
# Accept default file location: ~/.ssh/id_rsa
# Leave passphrase empty
```

* Public key location: `~/.ssh/id_rsa.pub`

2. Copy public key to **target server** for passwordless login:

```bash
ssh-copy-id bob@devapp01
```

* Enter Bob’s password on the target server when prompted.
* Successful output: `Number of keys added: 1`

3. Test passwordless SSH login:

```bash
ssh bob@devapp01
```

---

### Step 3: Public Key Location on Target Server

* Public key copied to:

```
/home/bob/.ssh/authorized_keys
```

💡 **Tip:** This allows passwordless SSH authentication for the user.

---

### Step 4: Copying Files Using SCP

* Copy a file from **local machine** to **remote server** preserving permissions:

```bash
scp -p /path/to/local/file.tar.gz bob@devapp01:/home/bob/
```

* Flags used:

  * `-p` = preserve file permissions, modification times
  * `-r` = (optional) recursive, for directories

---

## ✅ Key Commands Summary

| Task                      | Command / Notes                                         |
| ------------------------- | ------------------------------------------------------- |
| SSH into remote server    | `ssh <user>@<server>`                                   |
| Generate SSH key pair     | `ssh-keygen -t rsa`                                     |
| Copy public key to server | `ssh-copy-id <user>@<server>`                           |
| Test passwordless SSH     | `ssh <user>@<server>`                                   |
| SCP file to remote server | `scp -p /local/path/file <user>@<server>:/remote/path/` |

---

## 💡 Notes / Tips

* Passwordless SSH reduces repeated password prompts and enables automated scripts.
* Public keys are stored in `~/.ssh/authorized_keys` on the **target server**.
* Use `scp -p` to preserve permissions when copying files.
* SSH key pairs consist of a **private key** (stay local) and a **public key** (placed on the server).

---

## 📌 Lab Summary

| Step                    | Status | Key Takeaways                                                          |
| ----------------------- | ------ | ---------------------------------------------------------------------- |
| SSH basics              | ✅      | Default port 22, connect as current user                               |
| Generate key pair       | ✅      | `ssh-keygen -t rsa`, private key local, public key `~/.ssh/id_rsa.pub` |
| Copy public key         | ✅      | `ssh-copy-id` adds key to `authorized_keys`                            |
| Test passwordless login | ✅      | Successful login without password prompt                               |
| Copy file using SCP     | ✅      | File transferred to remote server with preserved permissions           |

---

## ✅ References

* [SSH Keygen Documentation](https://www.ssh.com/ssh/keygen/)
* [SSH-Copy-ID Documentation](https://linuxize.com/post/how-to-setup-ssh-keys-on-linux/)
* [SCP Command Documentation](https://linuxize.com/post/how-to-use-scp-command-to-securely-transfer-files/)
