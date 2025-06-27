# 🚀 Chat App Deployment using Docker on AWS EC2

This project documents how I containerized and deployed a full-stack MERN chat application using Docker and hosted it on an AWS EC2 instance. The assignment aimed to evaluate my skills in infrastructure provisioning and DevOps practices.

## 📁 Project Structure
```
chat-app/  
├── backend/  
│   ├── Dockerfile  
│   └── ...  
├── frontend/  
│   ├── Dockerfile  
│   └── ...  
├── docker-compose.yml  
└── README.md  
```

## ✅ Assignment Steps

### 1. 🌐 Launch an EC2 Instance

  - Go to your AWS account → EC2 → Launch Instance
  - Configure the instance as follows:
  | Configuration | Value |
  | ------------- | ----- |
  | Name          | chat-app-ec2 |
  | AMI           | Ubuntu Server |
  | Instance type | t2.micro |
  | Key pair      | Create or use existing key |

