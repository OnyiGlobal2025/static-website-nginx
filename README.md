# Static Website Deployment on EC2 with Nginx, HTTPS & CI/CD

##  Project Overview
This project demonstrates the deployment of a static website on an AWS EC2 instance using **Nginx** as the web server, secured with **HTTPS via Let's Encrypt**, and automated using **GitHub Actions CI/CD**.

Any change pushed to the GitHub repository is automatically deployed to the live server without manual intervention.

---

##  Architecture Overview

- Developer pushes code to GitHub
- GitHub Actions pipeline is triggered
- Pipeline connects securely to EC2 via SSH
- Website files are synced to the Nginx web directory
- Nginx serves the updated content over HTTPS

---

##  Technologies Used

- **AWS EC2** – Virtual server hosting the website
- **Nginx** – Web server
- **Let’s Encrypt (Certbot)** – HTTPS/SSL certificates
- **GitHub Actions** – CI/CD automation
- **SSH & rsync** – Secure file transfer
- **Linux (Ubuntu)** – Server operating system

---

##  Deployment Steps Summary

1. Created an EC2 instance on AWS
2. Installed and configured Nginx
3. Created a custom project directory under `/var/www`
4. Configured Nginx server block for the domain
5. Pointed domain DNS to EC2 public IP
6. Secured the website using HTTPS with Certbot
7. Created a GitHub Actions workflow for CI/CD
8. Configured SSH authentication for GitHub Actions
9. Automated file deployment using `rsync`

---

##  CI/CD Workflow

- Trigger: `git push` to the `main` branch
- GitHub Actions:
  - Checks out the repository
  - Loads SSH private key securely from GitHub Secrets
  - Syncs website files to EC2 using `rsync`
- Website updates instantly after a successful pipeline run

---

##  Security Considerations

- SSH access restricted using key-based authentication
- Private keys stored securely in GitHub Secrets
- HTTPS enabled to encrypt traffic
- Correct Linux file permissions applied to avoid security risks

---

##  Challenges & Solutions

### Issue: Permission Denied During CI/CD Deployment
**Cause:**  
The deployment directory was owned by `root`, while GitHub Actions connected as `ubuntu`.

**Solution:**  
Updated ownership of the project directory:
```bash
sudo chown -R ubuntu:ubuntu /var/www/okorojeremiah

## 📷 Screenshots

### EC2 Instance Running
![EC2 Running](screenshots/ec2-running.png)

### Nginx Web Server
![Nginx Page](screenshots/nginx-page.png)

### Live Website with HTTPS
![HTTPS Enabled](screenshots/https-domain.png)

### GitHub Actions CI/CD Pipeline
![CI/CD Success](screenshots/github-actions-success.png)

