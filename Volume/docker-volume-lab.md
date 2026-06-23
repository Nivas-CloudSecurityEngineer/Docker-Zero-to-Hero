# Docker Volume Lab

## Objective

Learn how Docker Volumes persist data independently of containers.

---

## What is a Docker Volume?

A Docker Volume is managed by Docker and stores data outside the container filesystem.

Benefits:

* Data persists after container deletion
* Easy backup and migration
* Recommended for databases
* Managed by Docker

---

## Step 1: Create a Volume

```bash
docker volume create my-volume
```

Verify:

```bash
docker volume ls
```

Expected:

```text
DRIVER    VOLUME NAME
local     my-volume
```

---

## Step 2: Inspect the Volume

```bash
docker volume inspect my-volume
```

Example Output:

```json
[
  {
    "Name": "my-volume",
    "Driver": "local",
    "Mountpoint": "/var/lib/docker/volumes/my-volume/_data"
  }
]
```

---

## Step 3: Create a Container Using the Volume

```bash
docker run -dit \
  --name volume-container \
  -v my-volume:/app/data \
  ubuntu
```

---

## Step 4: Create Data Inside Container

Enter container:

```bash
docker exec -it volume-container bash
```

Create file:

```bash
echo "Docker Volume Demo" > /app/data/demo.txt
```

Verify:

```bash
cat /app/data/demo.txt
```

Output:

```text
Docker Volume Demo
```

Exit:

```bash
exit
```

---

## Step 5: Remove Container

```bash
docker rm -f volume-container
```

Volume still exists:

```bash
docker volume ls
```

---

## Step 6: Create New Container Using Same Volume

```bash
docker run -dit \
  --name volume-container-new \
  -v my-volume:/app/data \
  ubuntu
```

Access container:

```bash
docker exec -it volume-container-new bash
```

Verify file still exists:

```bash
cat /app/data/demo.txt
```

Output:

```text
Docker Volume Demo
```

This proves data persistence.

---

## Architecture

```text
+----------------+
| Docker Volume  |
|   my-volume    |
+----------------+
        |
  +-----+-----+
  |           |
Container1  Container2
```

---

## Cleanup

```bash
docker rm -f volume-container-new

docker volume rm my-volume
```

---

## Complete Workflow

```bash
docker volume create my-volume

docker run -dit \
  --name volume-container \
  -v my-volume:/app/data \
  ubuntu

docker exec -it volume-container bash

echo "Docker Volume Demo" > /app/data/demo.txt

docker rm -f volume-container

docker run -dit \
  --name volume-container-new \
  -v my-volume:/app/data \
  ubuntu

docker exec -it volume-container-new cat /app/data/demo.txt
```
