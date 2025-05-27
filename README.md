# Jenkins CI/CD Pipeline on AWS EC2

This project demonstrates how to set up a Jenkins server on an AWS EC2 instance to automate the CI process for a Python project.

##  Project Overview

-  Jenkins hosted on Ubuntu EC2 instance
-  CI job runs `pytest` to test a simple Python app
-  Pulls source code from GitHub
-  Publishes JUnit test results in Jenkins UI

---

##  Setup Guide

### 1. Launch EC2 Instance

- **AMI**: Ubuntu Server 22.04 LTS
- **Type**: t2.micro (free tier)
- **Ports to open**:
  - `22` (SSH)
  - `8080` (Jenkins Web UI)
  - `80` (optional)

### 2. Install Jenkins on EC2

sudo apt update
sudo apt install openjdk-17-jdk -y

curl -fsSL https://pkg.jenkins.io/debian-stable/jenkins.io-2023.key | sudo tee \
  /usr/share/keyrings/jenkins-keyring.asc > /dev/null

echo deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc] \
  https://pkg.jenkins.io/debian-stable binary/ | sudo tee \
  /etc/apt/sources.list.d/jenkins.list > /dev/null

sudo apt update
sudo apt install jenkins -y
sudo systemctl start jenkins
sudo systemctl enable jenkins

3. Access Jenkins
Visit: http://51.21.244.16:8080

Unlock Jenkins:

sudo cat /var/lib/jenkins/secrets/initialAdminPassword
Install suggested plugins

Create admin user

 Jenkins Job Setup
 Freestyle Project: python-ci
GitHub Repo: ViorelH/python-ci-cd-demo

Build Steps:

export PATH=$PATH:$HOME/.local/bin
pip install -r requirements.txt
pytest --junitxml=results.xml
Post-build Action:

Publish JUnit test result report

File: results.xml

 Example Output
Console logs showing test execution

JUnit report in Jenkins UI

 Optional Enhancements
Add GitHub Webhook to trigger Jenkins on push

Use a Jenkinsfile for pipeline-as-code

Build Docker images or deploy to Kubernetes

Secure Jenkins with Nginx + HTTPS

 Add Build Status Badge
Paste in your GitHub README.md:

![Build Status](http://51.21.244.16:8080/buildStatus/icon?job=python-ci)

 Author
ViorelH — DevOps CI/CD pipeline using Jenkins on AWS EC2.
