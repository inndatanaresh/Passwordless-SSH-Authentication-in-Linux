# Passwordless SSH Authentication in Linux

This guide explains how to set up passwordless SSH authentication between a slave node and a master server in a Linux environment. This setup enhances security and simplifies access for users without the need to share passwords or IP addresses.

---

## Master Server Setup

**Set the hostname of the master server:**

```bash
sudo hostnamectl set-hostname master-server
```

---

## Slave Node Setup

### Step 1: Generate SSH Key

Generate a new RSA key pair (press Enter three times when prompted):

```bash
ssh-keygen -t rsa
```

### Step 2: Copy the Public Key to the Master

Use `ssh-copy-id` to send the public key to the master server:

```bash
ssh-copy-id -i /home/<username>/.ssh/id_rsa.pub <username>@master-server
```

Replace `<username>` with the appropriate user (e.g., `divya`).

### Step 3: Test SSH Connection

Verify that you can log into the master without entering a password:

```bash
ssh master-server
```

---

## Notes for Multi-User Access

* When other users need to log into the master server:

  1. They should first SSH into the slave machine using the IP address:

     ```bash
     ssh <user>@<slave-ip>
     ```
  2. From the slave, they can SSH into the master using its hostname:

     ```bash
     ssh master-server
     ```

This prevents exposing the master’s IP address and avoids password sharing.

---

## Purpose

The main objective of setting up passwordless SSH is to:

* Avoid sharing SSH passwords with users, especially third parties
* Enhance security by using SSH keys instead of passwords
* Simplify access using DNS names instead of IP addresses

---

End of Document
