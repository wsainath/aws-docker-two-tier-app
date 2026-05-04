# Containerized Two-Tier Web Application Deployment on AWS EC2 using Docker

## Project Overview

This project demonstrates deployment of a containerized two-tier web application on AWS EC2 using Docker. It includes a web layer using Nginx and a database layer using MySQL, with persistent storage and container restart policies for resilience.

---

## Architecture

**AWS EC2 (Ubuntu 24.04 LTS)**

* Docker Engine

  * Nginx Container (Web Layer)
  * MySQL Container (Database Layer)
* Docker Volume for Persistent Storage

---

## Technologies Used

* AWS EC2
* Ubuntu Server 24.04 LTS
* Docker
* Nginx
* MySQL 8
* SSH (PuTTY)

---

## Implementation Steps

### 1. EC2 Instance Setup

* Created Ubuntu EC2 instance in ap-south-1 (Mumbai)
* Configured security group:

  * Port 22 (SSH)
  * Port 80 (HTTP)
  * Port 3306 (MySQL)

### 2. Docker Installation

```bash
sudo apt update && sudo apt upgrade -y
sudo apt install docker.io -y
sudo systemctl start docker
sudo systemctl enable docker
```

### 3. Deploy Nginx Container

```bash
docker run -d --name nginx-web --restart unless-stopped -p 80:80 nginx
```

### 4. Deploy MySQL Container

```bash
docker volume create mysql-data

docker run -d \
--name mysql-db \
--restart unless-stopped \
-v mysql-data:/var/lib/mysql \
-e MYSQL_ROOT_PASSWORD=Root@123 \
-e MYSQL_DATABASE=projectdb \
-p 3306:3306 \
mysql:8
```

### 5. Custom Webpage Deployment

Replaced default Nginx page with custom HTML project page.

### 6. Validation

* Verified containers using:

```bash
docker ps
```

* Verified persistent volume:

```bash
docker volume ls
```

* Tested deployment through browser using EC2 public IP.

---

## Key Features

* Cloud-based deployment on AWS EC2
* Containerized architecture
* Persistent database storage using Docker volumes
* Automatic service restart using restart policies
* Remote server management using SSH
* Cost-optimized deployment

---

## Challenges Faced

### Dynamic Public IP Change

Issue: EC2 public IP changed after stop/start.

Solution: Updated PuTTY host configuration manually.

### MySQL Authentication Issue

Issue: Access denied error.

Solution: Connected directly through Docker container shell.

### AWS RDS Cost Constraints

Issue: RDS exceeded budget.

Solution: Implemented MySQL container inside EC2.

---

## Learning Outcomes

* AWS EC2 provisioning
* Docker container lifecycle management
* Container networking
* Persistent storage management
* Linux server administration
* Cloud cost optimization

---

## Future Enhancements

* CI/CD pipeline using GitHub Actions
* Kubernetes deployment
* Load balancing
* Monitoring and logging
* Infrastructure as Code using Terraform
