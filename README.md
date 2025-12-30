# Multi-Server-Website-Deployment-Automation-Using-Ansible



# 🚀 Multi-Server Website Deployment Automation Using Ansible

## 📌 Project Overview

This project demonstrates how to **automate the deployment of a website across multiple servers** using **Ansible** on AWS EC2 instances.
Instead of manually configuring each server, Ansible is used to centrally manage and deploy configurations efficiently, securely, and consistently.

The setup includes:

* One **Ansible Control Node**
* Multiple **Target Web Servers**
* Secure SSH authentication
* Automated configuration using Ansible playbooks

---

## 🛠️ Technologies Used

* **AWS EC2**
* **Amazon Linux 2**
* **Ansible**
* **SSH**
* **Linux**
* **YAML**

---

## 🏗️ Architecture

* **Ansible Machine (Control Node)**

  * Manages and deploys configurations
  * SSH access from trusted IP

* **Web Servers (Managed Nodes)**

  * Receive deployments from Ansible
  * Allow HTTP traffic on port 80
  * SSH access only from Ansible Security Group

---

## 🔐 Security Groups Configuration

### 1️⃣ Ansible Machine Security Group

* SSH (Port 22): Allowed from your public IP

### 2️⃣ Server Security Group

* SSH (Port 22): Allowed **only from Ansible SG**
* HTTP (Port 80): Allowed from anywhere

---

## ⚙️ Setup & Implementation Steps

### Step 1: Create Security Groups

* Create **Ansible SG**
* Create **Server SG** with restricted SSH access

---

### Step 2: Launch EC2 Instances

* Launch **Ansible Machine**

  * OS: Amazon Linux 2
* Launch **Server Instances**

  * Attach `server-sg`
  * Use imported Ansible public key

---

### Step 3: Generate SSH Key Pair on Ansible Machine

```bash
ssh-keygen -t rsa -b 2048
```

---

### Step 4: Import Public Key into AWS EC2

* Import the generated public key as:

  ```
  ansible-pub-key
  ```

---

### Step 5: Test SSH Connectivity

```bash
ssh ec2-user@<private-ip>
```

---

### Step 6: Install Ansible on Control Node

```bash
sudo yum update -y
sudo amazon-linux-extras install ansible2 -y
```

---

### Step 7: Create Ansible Inventory File

Example:

```ini
[webservers]
10.0.1.10
10.0.1.11
```

---

### Step 8: Create Ansible Playbook

* Playbook handles automated website deployment
* Written in YAML

---

### Step 9: Test Ansible Connectivity

```bash
ansible all --key-file ~/.ssh/id_rsa -i inventory -m ping -u ec2-user
```

---

### Step 10: Configure Ansible Defaults

Create `ansible.cfg`:

```ini
[defaults]
remote_user = ec2-user
inventory = inventory
private_key_file = ~/.ssh/id_rsa
```

---

### Step 11: Run the Playbook

```bash
ansible-playbook deploy-techmax.yml
```

---

## ✅ Outcome

* Successfully deployed a website across multiple servers
* Centralized configuration management
* Secure and scalable automation
* Reduced manual server setup effort

---


## 🎯 Key Learning Highlights

* Ansible inventory management
* SSH key-based authentication
* AWS security group best practices
* Infrastructure automation
* Multi-server orchestration

---

## 👨‍💻 Author

**[Your Name]**
DevOps Engineer | Linux | Ansible | AWS

---

## ⭐ Future Improvements

* Add load balancer integration
* Implement Ansible roles
* Use dynamic AWS inventory
* CI/CD pipeline integration

---


