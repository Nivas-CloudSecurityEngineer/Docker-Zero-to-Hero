# Docker Networking Lab: Two Containers in the Same Network

## Objective

Create two Docker containers that can communicate with each other using a custom bridge network.

---

## Prerequisites

* Docker installed
* Docker daemon running

Verify:

```bash
docker --version
docker ps
```

---

## Step 1: Create a Custom Network

Create a bridge network named `my-network`.

```bash
docker network create my-network
```

Verify:

```bash
docker network ls
```

Expected output:

```text
NETWORK ID     NAME         DRIVER    SCOPE
xxxxxx         my-network   bridge    local
```

---

## Step 2: Create Container 1

```bash
docker run -dit \
  --name container1 \
  --network my-network \
  ubuntu
```

Verify:

```bash
docker ps
```

---

## Step 3: Create Container 2

```bash
docker run -dit \
  --name container2 \
  --network my-network \
  ubuntu
```

Verify:

```bash
docker ps
```

---

## Step 4: Inspect the Network

```bash
docker network inspect my-network
```

Look for:

```json
"Containers": {
    "container1": {},
    "container2": {}
}
```

---

## Step 5: Test Connectivity

Access Container 1:

```bash
docker exec -it container1 bash
```

Install ping:

```bash
apt update
apt install -y iputils-ping
```

Ping Container 2:

```bash
ping container2
```

Expected:

```text
64 bytes from container2 ...
64 bytes from container2 ...
```

Stop ping:

```bash
Ctrl + C
```

---

## Step 6: Verify DNS Resolution

Inside container1:

```bash
getent hosts container2
```

Example output:

```text
172.18.0.3 container2
```

---

## Network Diagram

```text
+-------------------+
|    my-network     |
+-------------------+
      |       |
      |       |
+-----------+ +-----------+
|container1 | |container2 |
+-----------+ +-----------+
```

---

## Cleanup

Remove containers:

```bash
docker rm -f container1 container2
```

Remove network:

```bash
docker network rm my-network
```

Verify:

```bash
docker network ls
```

---

## Complete Workflow

```bash
docker network create my-network

docker run -dit --name container1 --network my-network ubuntu

docker run -dit --name container2 --network my-network ubuntu

docker network inspect my-network

docker exec -it container1 bash

apt update && apt install -y iputils-ping

ping container2
```
