#  EpicBook DevOps Project (Fully Automated)

This project demonstrates how I automated the deployment of a full-stack Node.js application using **Terraform, Ansible, MySQL, Nginx, and PM2**.

The goal was simple:  
👉 **No manual setup. Everything should be automated end-to-end.**


---

##  Project Overview

EpicBook is a Node.js bookstore application connected to a MySQL database.

This project covers:
- Infrastructure provisioning (Terraform)
- Configuration management (Ansible)
- Application deployment (Node.js + PM2)
- Database setup and seeding (MySQL)
- Reverse proxy setup (Nginx)

---

##  Tech Stack

- **Cloud Provider:** Azure VM (Ubuntu 22.04)
- **Infrastructure as Code:** Terraform
- **Configuration Management:** Ansible
- **Backend:** Node.js (Express)
- **Database:** MySQL
- **Process Manager:** PM2
- **Web Server:** Nginx

---

##  Project Structure
```bash
epicbook-prod/
│
├── terraform/
│ ├── main.tf
│ ├── variables.tf
│ ├── terraform.tfvars
│ └── output.tf
│
├── ansible/
│ ├── inventory.ini
│ ├── site.yml
│ └── roles/
│ ├── common/
│ ├── mysql/
│ ├── nginx/
│ └── epicbook/
│
└── README.md
```

---

##  What This Project Automates

### ✅ Terraform
- Creates Azure VM
- Configures networking (Public IP, NSG)
- Injects SSH key automatically

### ✅ Ansible
- Installs Node.js, MySQL, Nginx
- Creates database and user
- Clones application repo
- Installs dependencies
- Seeds database (authors & books)
- Configures Nginx reverse proxy
- Starts app using PM2

---

##  Key Features

- Fully automated deployment (no manual SSH setup)
- Idempotent Ansible roles
- Database auto-seeding
- Production-ready Nginx config
- PM2 process management
- Clean separation of concerns

---

##  Challenges Faced

### ❌ SSH Authentication Issues
- Fixed by properly configuring SSH key in Terraform

### ❌ MySQL Access Denied (root)
- Resolved using proper authentication plugin and privileges

### ❌ Database Not Showing Books
- Fixed by automating database seeding using Ansible

### ❌ Port 8080 Already in Use
- Caused by multiple Node processes
- Fixed using PM2 process control

### ❌ Permission Errors (npm install)
- Resolved by correcting ownership of `/var/www/epicbook`

---

##  How to Deploy

### 1. Clone Repository
```bash
git clone <your-repo>
cd epicbook-prod
```
---

### 2. Provision Infrastructure (Terraform)

```bash
cd terraform
terraform init
terraform apply
```

---

### 3. Configure Server (Ansible)
```bash
cd ../ansible
ansible-playbook -i inventory.ini site.yml
```

### 4.SSH Access (Optional)
```bash
ssh azureuser@<public-ip>
```

## Database Seeding

The database is automatically seeded with:

- Authors
- Books

No manual SQL execution required


## Nginx Configuration
- Reverse proxy from port 80 → 8080
- Public access via browser
- Default site removed

---
## What I Learned
- How to integrate Terraform with Ansible
- Importance of idempotent automation
- Debugging real-world DevOps issues
- Managing application processes with PM2
- Handling Linux permissions properly
- Automating database initialization

## Future Improvements
- Add CI/CD pipeline (GitHub Actions)
- Dockerize the application
- Use Kubernetes for orchestration
- Add HTTPS with Let's Encrypt
- Implement monitoring (Prometheus + Grafana)
---

## Final Note

This project represents real-world DevOps challenges and solutions.
Everything was built with a focus on automation, scalability, and reliability.