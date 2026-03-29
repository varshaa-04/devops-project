DevOps CI/CD Project

-------Overview

This project demonstrates an end-to-end DevOps pipeline for deploying a Python web application.

<img width="1000" height="1000" alt="ChatGPT Image Mar 29, 2026, 10_52_32 PM" src="https://github.com/user-attachments/assets/731c5b03-fe8b-46ab-8067-817e8f6edebc" />


It covers:

1. CI/CD automation using GitHub Actions

2. Containerization with Docker

3. Image storage in Amazon ECR

4. Deployment on AWS EC2

Infrastructure setup using Terraform

-----Architecture

Code → GitHub → GitHub Actions → Docker → ECR → EC2

-----Tech Stack

Python (Flask)

Docker

GitHub Actions

AWS (ECR, EC2)

Terraform

---- Project Structure
.
├── app.py
├── requirements.txt
├── Dockerfile
├── .github/workflows/pipeline.yml
└── terraform/
    ├── provider.tf
    └── ecr.tf

    
------ CI/CD Pipeline

The pipeline automatically:

Checks out code

Installs dependencies

Runs lint checks

Builds Docker image

Pushes image to ECR

Deploys to EC2


<img width="500" height="500" alt="Screenshot (16)" src="https://github.com/user-attachments/assets/a714fdc8-54c6-450e-82ce-33b6015986c6" />


Build image:

docker build -t my-devops-app .

Run container:

docker run -d -p 5000:5000 my-devops-app
---- AWS ECR

Login:

aws ecr get-login-password --region us-east-1 \
| docker login --username AWS --password-stdin <account-id>.dkr.ecr.us-east-1.amazonaws.com

Push image:

docker push <account-id>.dkr.ecr.us-east-1.amazonaws.com/my-devops-app:latest

<img width="500" height="500" alt="Screenshot (19)" src="https://github.com/user-attachments/assets/695cddb9-98d3-4bc1-bba9-a6ed76bdbdbf" />


<img width="500" height="500" alt="Screenshot (17)" src="https://github.com/user-attachments/assets/3827b79b-aa6d-44ee-90f3-276d640d3840" />

----- EC2 Deployment

Pull image:

docker pull <image>

Run:

docker run -d -p 5000:5000 --name app <image>

Access:

http://<EC2-IP>:5000

<img width="1000" height="1000" alt="Screenshot (18)" src="https://github.com/user-attachments/assets/cf788a09-3570-494a-8cc7-38ffa29f365a" />



====== Terraform

Initialize:

terraform init

Apply:

terraform apply

====== Creates ECR repository
------GitHub Secrets

Add these in GitHub Actions:

AWS_ACCESS_KEY_ID
AWS_SECRET_ACCESS_KEY
EC2_IP
EC2_USER
EC2_SSH_KEY

<img width="1000" height="1000" alt="image" src="https://github.com/user-attachments/assets/f91bbef2-eca3-41a0-8488-58ded674e5d3" />



⭐ Summary

This project demonstrates a complete CI/CD pipeline with real-world DevOps tools, from code commit to deployment.
