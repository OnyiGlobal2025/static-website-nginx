# Static Website Deployment on EC2 with Nginx, HTTPS & CI/CD

##  Overview
This project demonstrates the end-to-end deployment of a production-ready static website on an AWS EC2 instance using **Nginx** as the web server, secured with **HTTPS (Let’s Encrypt)**, and automated with **GitHub Actions CI/CD**.

Any change pushed to the GitHub repository is automatically deployed to the live server without manual file transfer or server login.

---

##  Architecture Overview
The deployment architecture follows this flow:

- Developer pushes code to GitHub
- GitHub Actions pipeline is triggered
- Pipeline connects securely to EC2 via SSH
- Website files are synchronized to the server using `rsync`
- Nginx serves the updated content over HTTPS

---

##  Technologies Used
- **AWS EC2** – Compute instance hosting the website
- **Ubuntu Linux** – Server operating system
- **Nginx** – Web server
- **Let’s Encrypt (Certbot)** – SSL/TLS certificates
- **GitHub Actions** – CI/CD automation
- **SSH & rsync** – Secure file synchronization
- **HTML / CSS / JavaScript** – Website technologies

---

##  Deployment Flow
1. Provisioned an EC2 instance on AWS
2. Installed and configured Nginx
3. Created a custom project directory under `/var/www`
4. Configured an Nginx server block for the domain
5. Pointed domain DNS records to the EC2 public IP
6. Secured the site with HTTPS using Certbot
7. Created a GitHub Actions workflow for CI/CD
8. Stored SSH credentials securely using GitHub Secrets
9. Automated deployment using `rsync` on every push

---

##  CI/CD Pipeline Details
- **Trigger:** Push to the `main` branch
- **Pipeline Steps:**
  - Checkout repository
  - Configure SSH using GitHub Secrets
  - Sync files to EC2 using `rsync`
- **Result:** Live website updates automatically after each push

---

##  Security Considerations
- SSH key-based authentication (no passwords)
- Private SSH keys stored securely in GitHub Secrets
- HTTPS enforced to encrypt all traffic
- Correct Linux file ownership to allow CI/CD without unsafe sudo usage

---

##  Challenges & Solutions

### Permission Denied During CI/CD Deployment
**Issue:**  
GitHub Actions failed to deploy files to the web directory.

**Cause:**  
The deployment directory was owned by `root`, while GitHub Actions connected as the `ubuntu` user.

**Solution:**  
Updated directory ownership to allow automated deployments:

`sudo chown -R ubuntu:ubuntu /var/www/okorojeremiah`

This resolved the permission issue without compromising security.



## Screenshots

![Ec2 Running](/screenshots/Ec2-running.png)


![Github Actions](/screenshots/github-actions-success.png)


![Https Domain](/screenshots/https-domain.png)


![Nginx page](/screenshots/nginx-page.png)




## Key Learnings

CI/CD pipelines depend heavily on correct Linux permissions

Separating project directories improves maintainability and security

HTTPS is essential for production-ready applications

Automation eliminates manual deployment errors and inconsistencies


## Author

Onyedika Okoro

Cloud/DevOps Engineer