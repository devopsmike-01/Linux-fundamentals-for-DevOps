# Linux-fundamentals-for-DevOps
- This repo is maintained by [Devops with Mike](https://www.youtube.com/@DevOpsWithMike0/videos/)
- For interview preparation, use this platform [Wandaprep](http://www.wandaprep.com/)
- Visit my website for more inquiries and support [DevOpswithMike](https://devopswithmike.tech/).

## Introduction
Welcome to the Linux Fundamentals for DevOps Engineers repository! This repository is designed to provide a comprehensive guide for individuals looking to build or strengthen their Linux knowledge specifically tailored for DevOps roles. As a DevOps engineer, Linux is a cornerstone of your toolkit, providing the foundation for managing servers, automating deployments, and handling cloud infrastructures.
Whether you are a beginner exploring the world of Linux or an experienced IT professional aiming to refine your skills, this repository will cover essential concepts, commands, and use cases that are indispensable in DevOps workflows.

## What is Linux?
Linux is a free, open-source, Unix-like operating system kernel that powers a vast range of systems—from personal computers and servers to smartphones, embedded systems, and cloud infrastructures.
- It was first introduced by **Linus Torvalds** in 1991 and has since grown into a major player in the tech industry.
- Unlike proprietary operating systems, Linux thrives on its **community-driven development**, ensuring flexibility, security, and robustness.

## Key Attributes of Linux:

- **Open Source**: Anyone can use, modify, and distribute Linux freely.
- **Multitasking**: Handles multiple tasks and users efficiently.
- **Customizability**: Its modular nature allows tailored solutions for various needs.

## Linux Distributions
Linux distributions (or "distros") are variations of Linux that bundle the kernel with additional software, utilities, and package managers to suit specific needs. Here are some popular distros relevant for DevOps Engineers:

| Distribution | Key Features | Use Cases in DevOps |
|---|---|---|
| Ubuntu | Beginner-friendly, extensive community support. | CI/CD pipelines, container development. |
| CentOS/AlmaLinux | Enterprise-focused, known for stability and security. | Server management, enterprise apps. |
| Debian | Highly stable and community-driven. | Server provisioning, package management. |
| Red Hat Enterprise Linux (RHEL) | Industry-standard, support for enterprise needs. | Cloud deployments, virtualization. |
| Amazon Linux | Optimized for AWS environments. | Cloud-native workloads on AWS. |
| Kali Linux | Security tools for penetration testing. | Security audits and vulnerability scans. |

## Common Linux Use Cases in DevOps
Linux plays a pivotal role in modern DevOps workflows. Here’s how
Here are examples of how Linux is used in each of the DevOps use cases mentioned above:

### Server Administration

**Example Use Case**:
You are hosting a web application on an Nginx web server. As part of routine maintenance:
1. You need to add a new domain to your server.
2. Create a directory for the new site, configure a virtual host, and restart Nginx.

#### Steps in Linux:
* Create a new directory:

```
mkdir -p /var/www/newdomain.com/html 
```

* Assign permissions:

```chown -R $USER:$USER /var/www/newdomain.com/html  
chmod -R 755 /var/www/newdomain.com 
``` 

* Edit the virtual host configuration file:

```
nano /etc/nginx/sites-available/newdomain.com 
``` 

* Enable the site and reload Nginx:

```ln -s /etc/nginx/sites-available/newdomain.com /etc/nginx/sites-enabled/  
systemctl reload nginx
```  

### Containerization

**Example Use Case:**
You are tasked with containerizing an application and deploying it using Docker.

#### Steps in Linux:
1. Write a `Dockerfile` to define the app environment:
```
FROM ubuntu:20.04  
RUN apt-get update && apt-get install -y python3  
COPY app.py /app/app.py  
CMD ["python3", "/app/app.py"]  
```

2. Build the Docker image:
```
docker build -t my-python-app .  
```
3. Run the container:
```
docker run -d -p 5000:5000 my-python-app  
```

This enables isolated deployment of applications, perfect for scaling and managing dependencies in DevOps workflows.

### Configuration Management

**Example Use Case**:
You need to configure multiple Linux servers to install **Apache HTTP Server** using **Ansible**.
#### Steps in Linux

1. Create an Ansible inventory file:
```
[webservers]  
server1.example.com  
server2.example.com  
```

2. Write a playbook (apache-install.yml):
```
- name: Install Apache  
  hosts: webservers  
  tasks:  
    - name: Install Apache  
      apt:  
        name: apache2  
        state: present  
```
3. **Run the playbook**
```
ansible-playbook -i inventory apache-install.yml  
```

This automates server provisioning and configuration with consistent results.

### CI/CD Pipelines

**Example Use Case:**
You are setting up a Jenkins pipeline to build, test, and deploy a Node.js application.

#### Steps in Linux

1. Write a `Jenkinsfile` to define the pipeline:
```
pipeline {  
    agent any  
    stages {  
        stage('Build') {  
            steps {  
                sh 'npm install'  
            }  
        }  
        stage('Test') {  
            steps {  
                sh 'npm test'  
            }  
        }  
        stage('Deploy') {  
            steps {  
                sh './deploy.sh'  
            }  
        }  
    }  
}
``` 

2. Configure Jenkins on a Linux server to execute the pipeline.

This helps automate the entire lifecycle of application development and delivery.

### Monitoring and Logging

**Example Use Case**:
You want to monitor CPU usage and memory consumption on a Linux server using **Prometheus** and visualize it with **Grafana**.

#### Steps in Linux
1. Install Prometheus and set it up:
```
sudo apt-get install prometheus  
```
Configure `prometheus.yml `to scrape metrics:

```
scrape_configs:  
  - job_name: 'node_exporter'  
    static_configs:  
      - targets: ['localhost:9100']  
```
2. Install and configure Grafana:
```
sudo apt-get install grafana 
``` 

Connect Grafana to Prometheus to visualize data.
This setup helps identify and address performance bottlenecks in real-time.

### Cloud Computing

**Example Use Case**:
You need to automate the creation of an **EC2 instance** and deploy a web application using **AWS CLI**.

#### Steps in Linux:

1. Use AWS CLI to create an EC2 instance:

```
aws ec2 run-instances --image-id ami-0abcdef12345 --count 1 --instance-type t2.micro --key-name MyKeyPair --security-group-ids sg-903004f8 --subnet-id subnet-6e7f829e 
```

2. SSH into the instance and deploy the application:

```
ssh -i MyKeyPair.pem ec2-user@<instance-public-ip>  
```

Install the application (e.g., Apache):

```
sudo yum install httpd  
sudo systemctl start httpd
```  

This simplifies launching and managing cloud infrastructure using Linux tools.

