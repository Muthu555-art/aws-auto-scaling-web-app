# Auto-Scaling & Highly Available Web Application on AWS

## Project Summary
This project demonstrates how to build a **highly available and auto-scaling web application** on AWS using core cloud services.  
The application automatically distributes traffic across multiple EC2 instances and scales based on CPU usage, ensuring reliability and performance during traffic changes.

This project was built as a **hands-on learning and portfolio project** to understand real-world AWS infrastructure.

---

## Architecture Overview
The application follows a **load-balanced and auto-scaled architecture**:

Internet  
→ Application Load Balancer (ALB)  
→ Target Group  
→ Auto Scaling Group (2–4 EC2 instances)

The system ensures:
- High availability
- Fault tolerance
- Automatic scaling based on demand

---

## AWS Services Used

- **Amazon EC2** – Hosts the web application
- **Launch Template** – Defines EC2 configuration
- **Auto Scaling Group (ASG)** – Manages instance scaling
- **Application Load Balancer (ALB)** – Distributes traffic
- **Target Group** – Routes requests to healthy instances
- **Security Groups** – Controls network access
- **Amazon CloudWatch** – Monitors CPU utilization

---

## Key Features

- Minimum **2 EC2 instances** always running
- Maximum **4 EC2 instances** during high load
- CPU-based auto scaling (target 50% utilization)
- Health checks to remove unhealthy instances
- Load-balanced traffic distribution
- Automated server setup using user data script

---

## EC2 User Data Script

Each EC2 instance installs and starts a web server automatically:

```bash
#!/bin/bash
yum update -y
yum install -y httpd
systemctl start httpd
systemctl enable httpd
echo "<h1>Hello from $(hostname) - Auto Scaling Web Server</h1>" > /var/www/html/index.html
