# Mini Finance Website Deployment with Terraform & Ansible

![Terraform](https://img.shields.io/badge/IaC-Terraform-purple)
![Ansible](https://img.shields.io/badge/Automation-Ansible-red)
![Azure](https://img.shields.io/badge/Cloud-Microsoft%20Azure-blue)
![Nginx](https://img.shields.io/badge/Web%20Server-Nginx-green)
![DevOps](https://img.shields.io/badge/Practice-DevOps-orange)

# Mini Finance Website Deployment using Terraform and Ansible

This project demonstrates how to deploy a static website on **Microsoft Azure** using **Terraform for infrastructure provisioning** and **Ansible for configuration management**.

The goal of the project is to practice real-world **DevOps automation workflows**, where infrastructure is provisioned programmatically and application configuration is automated.

---

# Project Architecture

This project follows a simple DevOps deployment pipeline:

Terraform → Azure Infrastructure → Ansible → Web Server Configuration → Website Deployment

The website is hosted on an Azure Linux VM running **Nginx**.

## Architecture Diagram

The deployment architecture follows a typical DevOps workflow:

Developer
   │
   │ Terraform
   ▼
Azure Infrastructure
(Resource Group, VNet, Subnet, NSG)

   │
   ▼
Linux Virtual Machine (Ubuntu)

   │
   │ Ansible
   ▼
Nginx Web Server

   │
   ▼
Mini Finance Website
---

# Technologies Used

- Terraform
- Ansible
- Microsoft Azure
- Azure CLI
- Ubuntu Linux
- Nginx
- Git & GitHub
- SSH

---

# Project Structure
mini-finance-project
│
├── terraform
│ ├── main.tf
│ ├── variables.tf
│ ├── terraform.tfvars
│ └── outputs.tf
│
├── ansible
│ ├── inventory.ini
│ └── webserver-installation.yml
│
└── README.md


---

# Infrastructure Provisioned with Terraform

Terraform was used to create the following Azure resources:

- Resource Group
- Virtual Network
- Subnet
- Network Security Group
- Public IP Address
- Network Interface
- Linux Virtual Machine (Ubuntu)

### Network Configuration
VNet: 10.0.0.0/16
Subnet: 10.0.1.0/24


### Security Rules

The Network Security Group allows:

| Port | Purpose |
|-----|------|
| 22 | SSH Access |
| 80 | HTTP Web Traffic |

---

# VM Configuration

| Setting | Value |
|------|------|
| OS | Ubuntu 22.04 |
| Authentication | SSH Key |
| Web Server | Nginx |
| Deployment Tool | Ansible |

---

# Ansible Configuration

Ansible was used to automate server setup and deployment.

### Tasks performed by the playbook

1. Install Nginx
2. Enable and start Nginx service
3. Clone the Mini Finance website from GitHub
4. Copy website files to `/var/www/html`
5. Configure the Nginx web server
6. Restart Nginx

---

# Deployment Process

## Step 1 — Clone or Create the Project
mkdir mini-finance-project
cd mini-finance-project
mkdir terraform ansible


---

# Step 2 — Write Terraform Infrastructure

Inside the terraform folder create:
cd terraform
terraform init


---

# Step 4 — Plan Infrastructure
terraform plan -var-file="terraform.tfvars

---

# Step 5 — Deploy Infrastructure
terraform apply -var-file="terraform.tfvars"


Terraform will output the **public IP address** of the VM.

Example:

Terraform will output the **public IP address** of the VM.

Example:

Terraform will output the **public IP address** of the VM.

Example:
public_ip_address = "20.151.9.170"


---

# Step 6 — Configure Ansible Inventory

Update the Ansible inventory with the VM public IP.

File:
ansible/inventory.ini

Example:
[web]
20.151.9.170

[all:vars]
ansible_user=azureuser
ansible_ssh_private_key_file=/home/nice/.ssh/id_ed25519
ansible_python_interpreter=/usr/bin/python3

---

# Step 7 — Run Ansible Playbook

Navigate to the ansible folder:
cd ../ansible

Run:
ansible-playbook -i inventory.ini webserver-installation.yml

Ansible will:

- Install Nginx
- Deploy the website
- Restart Nginx

---

# Step 8 — Verify Deployment

Open your browser and visit:
http://<public-ip>

Example:
http://20.151.9.170/


You should see the **Mini Finance website running**.

---

# Challenges Faced and Solutions

## SSH Key Path Issue

Terraform initially failed because the default SSH key path did not exist in WSL.

**Solution**

Updated Terraform to use the correct key path.

---

## Azure VM Size Not Available

Azure returned the error:
SkuNotAvailable


for the VM size.

**Solution**

Checked available SKUs using:
az vm list-skus --location canadacentral


Then selected a supported VM size.

---

## Public IP Not Attached to NIC

The VM was running but could not be reached.

**Solution**

Verified the NIC configuration and recreated the infrastructure to correctly attach the public IP.

---

## SSH Key Permission Error

Ansible failed with:
WARNING: UNPROTECTED PRIVATE KEY FILE


because the private key was stored in a Windows mounted path.

**Solution**

Copied the key into the WSL `.ssh` directory and set secure permissions:
chmod 600 ~/.ssh/id_ed25519


---

# Key DevOps Concepts Practiced

This project demonstrates several important DevOps practices:

- Infrastructure as Code (Terraform)
- Configuration Management (Ansible)
- Cloud Infrastructure Automation
- Secure SSH Access
- Web Server Automation
- Cloud Networking
- Troubleshooting Cloud Deployment Issues

## DevOps Skills Demonstrated

This project demonstrates hands-on experience with:

- Infrastructure as Code (Terraform)
- Configuration Management (Ansible)
- Azure Cloud Infrastructure
- Linux Server Administration
- SSH Key Authentication
- Web Server Deployment (Nginx)
- Git Version Control
- Troubleshooting Cloud Networking

## Future Improvements

Possible improvements for this project:

- Use Terraform modules for reusable infrastructure
- Automate deployment using CI/CD (GitHub Actions)
- Add a Load Balancer
- Containerize the application with Docker
- Deploy using Kubernetes

---

# Learning Outcomes

Through this project I learned:

- How to deploy infrastructure on Azure using Terraform
- How to automate server configuration using Ansible
- How to troubleshoot networking and SSH issues
- How Terraform and Ansible integrate in a DevOps workflow
- Real-world cloud deployment debugging techniques

---

# Author

Nice Nwogu  
Cloud / DevOps Engineer in Training



