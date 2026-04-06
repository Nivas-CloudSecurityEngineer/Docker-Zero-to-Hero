# Dockerfile Commands Guide


<img width="806" height="570" alt="image" src="https://github.com/user-attachments/assets/9bc5fcb7-7e5b-4838-b17e-76015147c5d3" />


## FROM
**Purpose:** Specifies the base image for your Docker image.  
**Syntax:** `FROM <image>[:<tag>] [AS <name>]`  

**Usage:**
- Choose a base image with the required runtime.
- Optionally specify a version using a tag.
- Use `AS` for naming stages in multi-stage builds.

---

## WORKDIR
**Purpose:** Sets the working directory inside the container.  
**Syntax:** `WORKDIR /path/to/directory`  

**Usage:**
- Defines where subsequent commands run.
- Prefer absolute paths for consistency.

---

## COPY
**Purpose:** Copies files from host to container.  
**Syntax:** `COPY <src>... <dest>`  

**Usage:**
- Copy files or directories into the container.
- Supports wildcards for multiple files.

---

## RUN
**Purpose:** Executes commands during build time.  
**Syntax:** `RUN <command>`  

**Usage:**
- Install dependencies and setup environment.
- Each `RUN` creates a new layer (cached).

---

## EXPOSE
**Purpose:** Documents the ports used by the container.  
**Syntax:** `EXPOSE <port>`  

**Usage:**
- Indicates which port the app listens on.
- Does not actually publish the port.

---

## CMD
**Purpose:** Defines default command at container startup.  
**Syntax:**  
- `CMD ["executable", "param1", "param2"]`  
- `CMD command param1 param2`  

**Usage:**
- Default runtime command.
- Can be overridden.

---

## ENV
**Purpose:** Sets environment variables.  
**Syntax:** `ENV <key> <value>`  

**Usage:**
- Configure app settings.
- Accessible during runtime.

---

## ARG
**Purpose:** Defines build-time variables.  
**Syntax:** `ARG <name>[=<default>]`  

**Usage:**
- Used only during build.
- Can be overridden with `--build-arg`.

---

## LABEL
**Purpose:** Adds metadata to the image.  
**Syntax:** `LABEL <key>=<value>`  

**Usage:**
- Store author, version, or description info.

---

## VOLUME
**Purpose:** Creates a persistent data volume.  
**Syntax:** `VOLUME ["/path/to/volume"]`  

**Usage:**
- Persist data outside container lifecycle.
- Share data between containers.

---

## Additional Tips

### Multi-Stage Builds
- Use multiple `FROM` statements.
- Separate build and runtime environments.

### Best Practices
- Minimize layers.
- Combine commands where possible.
- Use lightweight base images.

---

# How to write Dockerfile 

```
# Use the official Node.js image as the base image
FROM node:14

# Set the working directory inside the container
WORKDIR /app

# Copy package.json and package-lock.json into the container
COPY package*.json ./

# Install dependencies
RUN npm install

# Copy the rest of the application code into the container
COPY . .

# Expose port 3000
EXPOSE 3000

# Set environment variables
ENV NODE_ENV=production
ENV PORT=3000

# Define a build-time argument
ARG APP_VERSION=1.0.0
LABEL version=$APP_VERSION

# Add metadata to the image
LABEL maintainer="Your Name <your.email@example.com>"
LABEL description="Example Node.js application Dockerfile"

# Create a mount point as a volume in the container
VOLUME /app/data

# Command to run the application
CMD ["node", "app.js"]
```
---

## Conclusion
Dockerfile commands define how Docker images are built and run.  
Understanding these commands helps in creating efficient, scalable, and reusable containerized applications.
