# Docker Bind Mount Lab

## Objective

Learn how to share files between the host machine and a Docker container using Bind Mounts.

---

## What is a Bind Mount?

A Bind Mount maps a host directory directly into a container.

Benefits:

* Real-time file synchronization
* Ideal for development
* Source code changes immediately visible inside container

---

## Step 1: Create Host Directory

Linux:

```bash
mkdir docker-bind-demo
cd docker-bind-demo
```

Create file:

```bash
echo "Hello from Host" > hostfile.txt
```

Verify:

```bash
cat hostfile.txt
```

---

## Step 2: Start Container with Bind Mount

```bash
docker run -dit \
  --name bind-container \
  -v $(pwd):/app \
  ubuntu
```

---

## Step 3: Verify Host File Inside Container

```bash
docker exec -it bind-container bash
```

Check:

```bash
ls /app

cat /app/hostfile.txt
```

Output:

```text
Hello from Host
```

---

## Step 4: Create File from Container

Inside container:

```bash
echo "Created from Container" > /app/containerfile.txt
```

Exit:

```bash
exit
```

---

## Step 5: Verify on Host

```bash
ls

cat containerfile.txt
```

Output:

```text
Created from Container
```

This proves two-way synchronization.

---

## Architecture

```text
Host Directory
     |
     |
     V
+------------+
|  Container |
|    /app    |
+------------+
```

---

## Key Difference

| Feature            | Volume | Bind Mount |
| ------------------ | ------ | ---------- |
| Managed by Docker  | Yes    | No         |
| Host Path Required | No     | Yes        |
| Data Persistence   | Yes    | Yes        |
| Development Usage  | Medium | High       |
| Production Usage   | High   | Medium     |

---

## Cleanup

```bash
docker rm -f bind-container

cd ..

rm -rf docker-bind-demo
```

---

## Complete Workflow

```bash
mkdir docker-bind-demo
cd docker-bind-demo

echo "Hello from Host" > hostfile.txt

docker run -dit \
  --name bind-container \
  -v $(pwd):/app \
  ubuntu

docker exec -it bind-container bash

cat /app/hostfile.txt

echo "Created from Container" > /app/containerfile.txt
```
