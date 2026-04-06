# 🐳 Docker Zero to Hero Guide

A complete beginner-to-advanced guide to mastering Docker 🚀

---


## 📌 Table of Contents

- What is Docker?
- Why Docker?
- Before Docker (Traditional Deployment)
- Docker Architecture
- Installing Docker (Ubuntu)
- Docker Basics
- Docker Images
- Docker Containers
- Docker Lifecycle
- Docker Commands Cheat Sheet
- Dockerfile (Core Concept)
- Docker Image Layers
- Volumes & Networking
- Best Practices
- Real-world Workflow

---

## 🧠 1. What is Docker?

Docker is a containerization platform that allows you to package applications along with their dependencies into a standardized unit called a container.

**👉 Think of it like:**

- A lightweight virtual machine
- But faster and more efficient

## ❓ 2. Why Docker?

**Problems Before Docker:**

"Works on my machine" issue 😤

- Dependency conflicts
- Environment mismatch (Dev vs QA vs Prod)
  
Docker Solves:

- ✅ Consistent environments
- ✅ Faster deployments
- ✅ Isolation between applications

<img width="960" height="540" alt="image" src="https://github.com/user-attachments/assets/f2afacba-2513-49c8-8b68-44a277f474e0" />


## 🕰️ 3. Before Docker (Traditional Deployment)

Old Approach:
✅ Scalability & portability

```
App → Install Dependencies → Configure OS → Run
```

**Problems:**

Manual setup
Hard to replicate
Error-prone

**With Docker:**

```
App + Dependencies → Docker Image → Run Anywhere
```

## 🏗️ 4. Docker Architecture

<img width="1024" height="519" alt="image" src="https://github.com/user-attachments/assets/e3b9d2c3-26c4-4b47-9bd7-198e55077ded" />



```
+---------------------+
|   Docker Client     |
+----------+----------+
           |
           v
+---------------------+
|   Docker Daemon     |
|  (Engine)           |
+----------+----------+
           |
    +------+------+
    |             |
    v             v
Images        Containers

```

Components:

- Docker Client → CLI (docker command)
- Docker Daemon → Runs containers
- Docker Images → Blueprint
- Docker Containers → Running instances

---

## 🐧 5. Install Docker (Ubuntu)

```copy
# Update packages
sudo apt update

# Install dependencies
sudo apt install apt-transport-https ca-certificates curl software-properties-common -y

# Add Docker GPG key
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -

# Add repo
sudo add-apt-repository \
   "deb [arch=amd64] https://download.docker.com/linux/ubuntu focal stable"

# Install Docker
sudo apt update
sudo apt install docker-ce -y

# Start Docker
sudo systemctl start docker
sudo systemctl enable docker

# Verify
docker --version
```

Run without sudo:

```copy
sudo usermod -aG docker $USER
newgrp docker
```
---

## 📦 6. Docker Basics
Check version:

```
docker --version
```

---

## 🖼️ 7. Docker Images

What is an Image?

A read-only template used to create containers.

Commands:

```
# List images
docker images

# Pull image
docker pull nginx

# Remove image
docker rmi nginx
```

---

## 📦 8. Docker Containers

What is a Container?

A running instance of an image

Commands:

```
# Run container
docker run -d -p 80:80 nginx

# List running containers
docker ps

# List all containers
docker ps -a

# Stop container
docker stop <container_id>

# Remove container
docker rm <container_id>

```
---

## 🔄 9. Docker Lifecycle

```
Create → Start → Stop → Restart → Delete
```

Flow:
docker create
docker start
docker stop
docker restart
docker rm

## 📜 10. Docker Commands Cheat Sheet


| Command       | Description                  |
| ------------- | ---------------------------- |
| docker run    | Run container                |
| docker ps     | List containers              |
| docker images | List images                  |
| docker build  | Build image                  |
| docker pull   | Download image               |
| docker push   | Upload image                 |
| docker exec   | Run command inside container |
| docker logs   | View logs                    |
| docker stop   | Stop container               |
| docker rm     | Remove container             |

---

## 🧾 11. Dockerfile (Core Concept)

What is Dockerfile?

A script with instructions to build Docker images.

Example:

```
# Base image
FROM node:18

# Set working directory
WORKDIR /app

# Copy files
COPY package.json .

# Install dependencies
RUN npm install

# Copy rest of code
COPY . .

# Expose port
EXPOSE 3000

# Start app
CMD ["npm", "start"]

```
Build Image:

```
docker build -t my-app .
```

Run:

```
docker run -p 3000:3000 my-app
```

---

## 🧱 12. Docker Image Layers

Each Docker image consists of layers.

Example Layers:

```
Base OS Layer
↓
Node Layer
↓
Dependencies Layer
↓
Application Code Layer

```
Benefits:

- Faster builds (cache)
- Reusability
- Efficient storage


---

## 💾 13. Volumes & Networking

Volumes (Data Persistence)

```
docker volume create mydata
docker run -v mydata:/data nginx
```

Networking

```
# Create network
docker network create mynet

# Run container in network
docker run -d --network mynet nginx
```
---

## ⚡ 14. Best Practices

- ✅ Use small base images (alpine)
- ✅ Minimize layers
- ✅ Use .dockerignore
- ✅ Avoid running as root
- ✅ Tag images properly


## 🌍 15. Real-world Workflow

```
# 1. Write Dockerfile
# 2. Build image
docker build -t my-app .

# 3. Run container
docker run -d -p 3000:3000 my-app

# 4. Push to Docker Hub
docker tag my-app username/my-app
docker push username/my-app
```

---
