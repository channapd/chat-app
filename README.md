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
    
  | Configuration |            Value            |
  | ------------- | --------------------------- |
  | Name          | chat-app-ec2                |
  | AMI           | Ubuntu Server               |
  | Instance type | t2.micro                    |
  | Key pair      | Create or use existing key  |

  - EC2 Inbound Security Rules

  | Type | Protocol | Port Range | Source |    Description   |
  | ---- | -------- | ---------- | ------ | ---------------- |
  | SSH  |   TCP    |     22     |  My IP |  For SSH Access  |
  | Custom TCP | TCP | 5001 | 0.0.0.0/0 | Backend  |
  | Custom TCP | TCP | 5173 | 0.0.0.0/0 | Frontend |

  - Click Launch Instance

### 2. 🔑 Connect to EC2 via SSH

  - Go to EC2 Dashboard → Select your instance → Click Connect
  - Choose the SSH Client tab
  - Copy the connection command:
    ```
    ssh -i "chat-app.pem" ubuntu@<your-ec2-public-ip>
    ```
  - Open WSL or terminal:
    ```
    chmod 400 chat-app.pem         
    ssh -i "chat-app.pem" ubuntu@<your-ec2-public-ip>
    ```
