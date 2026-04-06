# Docker Commands Cheat Sheet

## Container Management
- `docker run` - Run a container from an image  
- `docker ps` - List running containers  
- `docker stop` - Stop a running container  
- `docker start` - Start a stopped container  
- `docker restart` - Restart a container  
- `docker rm` - Remove a container  
- `docker logs` - Show container logs  
- `docker exec` - Execute a command inside a running container  
- `docker inspect` - Show detailed information about a container  
- `docker top` - Show running processes inside a container  
- `docker stats` - Show resource usage statistics  
- `docker diff` - Show filesystem changes  
- `docker pause` - Pause a container  
- `docker unpause` - Unpause a container  
- `docker kill` - Force stop a container  
- `docker wait` - Wait for container to stop  
- `docker attach` - Attach to a running container console  
- `docker port` - Show mapped ports  
- `docker cp` - Copy files between host and container  
- `docker commit` - Create image from container changes  
- `docker export` - Export container to tar  
- `docker import` - Import container from tar  

---

## Image Management
- `docker pull` - Pull image from registry  
- `docker push` - Push image to registry  
- `docker build` - Build image from Dockerfile  
- `docker images` - List images  
- `docker rmi` - Remove an image  
- `docker tag` - Tag an image  
- `docker history` - Show image history  
- `docker save` - Save image as tar  
- `docker load` - Load image from tar  

---

## Networking
- `docker network create` - Create network  
- `docker network connect` - Connect container to network  
- `docker network disconnect` - Disconnect container from network  

---

## Volumes
- `docker volume create` - Create volume  
- `docker volume ls` - List volumes  
- `docker volume rm` - Remove volume  

---

## Registry Authentication
- `docker login` - Log in to registry  
- `docker logout` - Log out of registry  

---

## System Management
- `docker system prune` - Remove unused objects  
- `docker system df` - Show disk usage  
- `docker system events` - Show system events  
- `docker system info` - Show system info  
- `docker system inspect` - Inspect Docker objects  
- `docker system logs` - Show Docker logs  
- `docker system version` - Show Docker version  

---

## Advanced Tools
- `docker buildx` - Build multi-platform images  
- `docker compose` - Manage multi-container apps  
- `docker swarm` - Manage Docker clusters  
