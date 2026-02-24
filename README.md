# BrainTask
Brain Tasks App
Project Overview
This project demonstrates the end-to-end deployment of a React application to a production-ready Kubernetes environment using AWS DevOps services.
The application is containerized using Docker, stored in Amazon ECR, and deployed to Amazon EKS using a CI/CD pipeline built with AWS CodePipeline, CodeBuild, and CodeDeploy.
The React application runs on port 3000 and is exposed via a Kubernetes LoadBalancer.
Architecture Overview
GitHub → CodePipeline → CodeBuild → Amazon ECR → Amazon EKS → LoadBalancer
AWS Services Used:
•	Amazon EC2 (Amazon Linux)
•	Docker
•	Amazon ECR
•	Amazon EKS
•	Kubernetes (kubectl)
•	AWS CodeBuild
•	AWS CodeDeploy
•	AWS CodePipeline
•	Amazon CloudWatch (Monitoring & Logs)
Application Details
•	Application: Brain Tasks App (React)
•	Default Port: 3000
•	Containerized using Docker
•	Deployed on Kubernetes cluster (EKS)
Docker Setup
Dockerfile Created
•	Base Image: node:18-alpine
•	Installed dependencies
•	Built React app
•	Exposed port 3000
•	Started application using npm start
Docker Commands Used
docker build -t brain-taskss-app .
docker run -p 3000:3000 brain-tasks-app
Amazon ECR Setup
1.	Created ECR repository
2.	Tagged Docker image
3.	Pushed image to ECR
aws ecr get-login-password --region ap-south-1 | docker login --username AWS --password-stdin <account-id>.dkr.ecr.ap-south-1.amazonaws.com

docker tag brain-task-app:latest <account-id>.dkr.ecr.ap-south-1.amazonaws.com/brain-task-app:latest

docker push <account-id>.dkr.ecr.ap-south-1.amazonaws.com/brain-task-app:latest
Kubernetes (EKS) Deployment
Deployment YAML
•	Replica count: 2
•	Image pulled from ECR
•	Container port: 3000
Service YAML
•	Type: LoadBalancer
•	Exposed publicly
Deployment Commands
kubectl apply -f deployment.yaml
kubectl apply -f service.yaml
CI/CD Pipeline
Source Stage
•	Provider: GitHub (via GitHub App)
•	Branch: main

Build Stage (CodeBuild)
•	Managed Image: Amazon Linux
•	Used buildspec.yml
•	Built Docker image
•	Pushed image to ECR
•	Applied Kubernetes manifests
Deploy Stage
•	Deployment via EKS
•	Used kubectl inside CodeBuild

buildspec.yml 
Summary
•	Install Docker
•	Login to ECR
•	Build image
•	Push image
•	Update Kubernetes deployment
Monitoring
•	CloudWatch Logs used to monitor:
o	CodeBuild logs
o	CodePipeline execution
o	Deployment logs
Application Access
The application is exposed using a Kubernetes LoadBalancer.
LoadBalancer ARN:
http://afa19a13397b9454a91010599daefd8e-2059053323.ap-south-1.elb.amazonaws.com
Public URL:
http:// 13.232.104.62:3000
