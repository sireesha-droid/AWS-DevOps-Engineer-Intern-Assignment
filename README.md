# AWS DevOps Engineer Intern Assignment
## AWS EC2 Nginx Website Deployment

A simple personal info website deployed on an AWS EC2 (Ubuntu) instance using Nginx.

**Author:** Sireesha Manku
**College:** Siddartha Educational Academy Group of Institutions, Tirupati (Affiliated to JNTUA)
**Branch:** Computer Science and Engineering
**Email:** sireeshamanku24@gmail.com
**Deployment Date:** 09 July 2026

---

## 🌐 Live Site

http://18.60.109.52

---

## 🛠️ Tech Stack

- **Cloud Provider:** AWS EC2 (Ubuntu 22.04 LTS)
- **Web Server:** Nginx
- **Frontend:** HTML5 + CSS3

---

## 📋 Setup Steps

### 1. Launch EC2 Instance
- Launched an Ubuntu 22.04 LTS `t2.micro` instance on AWS EC2.
- Created a new key pair for SSH access.
- Created a Security Group with the following inbound rules:
  | Type  | Port | Source    |
  |-------|------|-----------|
  | SSH   | 22   | My IP     |
  | HTTP  | 80   | 0.0.0.0/0 |

### 2. Connect via SSH
```bash
chmod 400 your-key.pem
ssh -i your-key.pem ubuntu@18.60.109.52
```

### 3. Linux Basics / System Setup
```bash
sudo apt update && sudo apt upgrade -y
sudo apt install nginx -y

sudo systemctl status nginx
sudo systemctl restart nginx
sudo systemctl enable nginx

df -h       # disk usage
free -h     # memory usage
ps aux      # running processes
```

### 4. Deploy the Website
```bash
# uploaded index.html from local machine
scp -i your-key.pem index.html ubuntu@18.60.109.52:~/

# on the EC2 instance
sudo rm /var/www/html/index.nginx-debian.html
sudo mv ~/index.html /var/www/html/index.html
sudo systemctl restart nginx
```

Website is accessible at `http://18.60.109.52`.

### 5. (Bonus) Auto-restart Script
A shell script `restart_nginx.sh` is included to restart Nginx and log the result:
```bash
chmod +x restart_nginx.sh
./restart_nginx.sh
```

---

## 📁 Repository Contents

| File               | Description                                  |
|--------------------|-----------------------------------------------|
| `index.html`       | Website source (Name, College, Branch, Email, Date) |
| `README.md`        | This file — setup steps and commands used     |
| `restart_nginx.sh` | Bonus: shell script to restart Nginx          |

---

## 📝 Commands Reference

| Purpose               | Command                              |
|------------------------|--------------------------------------|
| Update packages        | `sudo apt update && sudo apt upgrade -y` |
| Install Nginx           | `sudo apt install nginx -y`         |
| Check Nginx status      | `sudo systemctl status nginx`       |
| Restart Nginx           | `sudo systemctl restart nginx`      |
| Enable Nginx on boot    | `sudo systemctl enable nginx`       |
| Disk usage               | `df -h`                             |
| Memory usage             | `free -h`                           |
| Running processes        | `ps aux`                            |
| Copy file to EC2         | `scp -i key.pem file ubuntu@IP:~/`  |

---

## Problems Faced

- Encountered "Permission denied" while editing `/var/www/html/index.html` because root permissions were required.
- Initially tried creating a directory in the root (`/`) directory, which failed due to insufficient permissions.
- Resolved both issues by using `sudo` where required and working from `/home/ubuntu`.

---

## Learnings

- Created and configured an AWS EC2 Ubuntu instance.
- Connected securely using SSH.
- Installed and managed the Nginx web server.
- Deployed a static HTML website.
- Used Linux commands for system administration.
- Learned basic Git and GitHub workflow.

---

## Time Taken

Approximately 2 hours.

---

## Overall Evaluation

| Requirement          | Status |
|-----------------------|--------|
| EC2 Setup              | ✅ |
| Linux Commands         | ✅ |
| Website Deployment     | ✅ |
| Git & GitHub           | ✅ |
| README                 | ✅ |
| Bonus (Shell Script)   | ✅ |
