# 🔐 Ansible Passwordless Authentication

Ansible communicates over SSH, so having to enter a password each time can interrupt automation. We fix that by using either:
- A `.pem` key (for cloud VMs like AWS EC2)
- SSH key pairs (`ssh-keygen`)

---

## ✅ METHOD 1: Using `.pem` File (Cloud VMs like AWS EC2)

This method is used when connecting to remote machines (like EC2) where you already have a `.pem` file provided.

### 🔸 Step 1: Copy the public key to the server using `.pem`

```bash
ssh-copy-id -f "-o IdentityFile=<PATH-TO-PEM-FILE>" ubuntu@<INSTANCE-IP>

This command tells SSH to use  .pem file and copy the public key to the remote server's authorized list. This enables passwordless access.

### 🔸 Step 2: Test the SSH login

ssh -i ~/dev-key.pem ubuntu@13.233.56.78
Now we  should be  able to logged in without entering a password.

---

## ✅ METHOD 2: Using ssh-keygen (Local Keys)
This is used when we are working on local servers or VMs without .pem files.

🔸 Step 1: Generate SSH key pair

ssh-keygen
This creates:

A private key (~/.ssh/id_rsa)

A public key (~/.ssh/id_rsa.pub)

🔸 Step 2: Copy the public key to the server

ssh-copy-id ubuntu@<INSTANCE-IP>
This adds  public key to the authorized_keys file on the remote machine.

🔸 Step 3: Test  SSH login

ssh ubuntu@192.168.1.10
we should get in without a password!
