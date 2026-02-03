# Jenkins CI/CD Pipeline – Docker Deployment to AWS EC2

## Overview
This repository contains a Jenkins declarative pipeline that automates:

- Cloning source code from GitHub
- Building and testing a Docker image
- Pushing the image to Docker Hub
- Launching an AWS EC2 instance
- Deploying the Docker container on EC2

The pipeline runs on a **Windows Jenkins agent** using `bat` commands.

---

## Technologies Used
- Jenkins (Declarative Pipeline)
- Docker
- Docker Hub
- AWS EC2
- AWS CLI
- GitHub
- Ubuntu AMI

---

## Pipeline Stages

### 1. Clone GitHub Repository
Clones the application source code from the `main` branch.

---

### 2. Build Docker Image
Builds a Docker image using the Dockerfile in the repository.

---

### 3. Test Docker Image
Runs a basic test inside the container to verify the image.

---

### 4. Push Docker Image to Docker Hub
- Authenticates using Jenkins credentials
- Tags the image as `latest`
- Pushes the image to Docker Hub

---

### 5. Launch EC2 Instance and Deploy Container
This stage:
- Launches a new EC2 instance
- Waits until the instance is running
- Retrieves the public IP address
- Installs Docker on the EC2 instance
- Pulls the Docker image
- Runs the container on port **80**

---

## Environment Variables

| Variable | Description |
|--------|------------|
| IMAGE_NAME | Docker image name |
| REGION | AWS region |
| KEY_NAME | EC2 key pair name |
| SECURITY_GROUP | EC2 security group ID |
| INSTANCE_TYPE | EC2 instance type |
| AMI_ID | Ubuntu AMI ID |

---

## Jenkins Credentials Required

| Credential | Purpose |
|----------|--------|
| Docker Hub credentials | Push image to Docker Hub |
| AWS credentials | Launch and manage EC2 |

---

## Prerequisites
- Jenkins running on Windows
- Docker installed on Jenkins agent
- AWS CLI installed and configured
- SSH client available
- EC2 key pair (.pem file)
- Security group allowing ports 22 (SSH) and 80 (HTTP)

---

## Post Actions
The pipeline logs out from Docker Hub after execution.

---

## Notes
- Each pipeline run creates a new EC2 instance
- No automatic cleanup is included
- Intended for learning and demonstration purposes
