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

### 3. 🛠 Install Dependencies on EC2

  - Install Git
    ```
    sudo apt install -y git
    ```
  - Clone Repository
    ```
    git clone https://github.com/channapd/chat-app.git
    cd chat-app
    ```
  - Install Docker & Docker Compose
    ```
    sudo apt install -y docker.io docker-compose
    sudo systemctl start docker                  
    sudo usermod -aG docker $USER                
    newgrp docker
    ```                                

### 4. ⚙️ Configuration Changes

  - Setup Environment Variables
    ```
    cd backend
    nano .env
    ```
    - Paste backend environment variables (MongoDB URI, PORT, JWT Secret and Cloudinary Credentials)
    - Save with: Ctrl + O, Enter, then Ctrl + X.
  - Update Frontend API URL
    ```
    nano docker-compose.yml
    ```
    - Change this line inside environment of frontend service:
      ```
      VITE_API_BASE_URL: "http://<ec2-ipv4-address>:5001/api"
      ```
  - Update CORS Origin in Backend
    ```
    cd backend/src
    nano index.js
    ```
    - Replace this line:
      ```
      origin: "http://<ec2-ipv4 address>:5173"
      ```
  - Update Cookie Options in Backend
    ```
    cd lib
    nano utils.js
    ```
    - Use:
      ```
      sameSite: "lax",
      secure: false
      ```

### 5. 🐳 Run the Application

Return to the root of the project and run:
```
docker-compose up --build
```
This builds and starts both frontend and backend containers.

### 6. 🌍 Access the App

Open your browser and go to:
```
http://<ec2-ipv4-address>:5173
```



