---
icon: docker
---

# Docker Beginner's Tutorial

## What is Docker?

Docker is a platform that allows developers to package applications and their dependencies into lightweight, portable containers. Containers can run on any system that supports Docker, ensuring consistency across different environments.

### Key Features of Docker

* **Portability:** Write once, run anywhere.
* **Isolation:** Separate containers for different applications.
* **Efficiency:** Containers use fewer resources than virtual machines.
* **Scalability:** Easily scale applications by running multiple containers.

### Why Do We Need Docker?

1. **Environment Consistency:** Avoid the "it works on my machine" problem.
2. **Faster Development:** Quickly set up environments and test changes.
3. **Simplified Deployment:** Package the application and dependencies together.
4. **Resource Efficiency:** Containers share the host OS, reducing overhead.

### How Docker Works

Docker utilizes a client-server architecture. The client communicates with the Docker daemon, which does the heavy lifting of building, running, and distributing Docker containers. Containers run on a Docker engine, which can work on any host with a Docker daemon installed.

### Difference Between Docker and Virtual Machines

While Docker containers and virtual machines (VMs) both provide isolation, they differ significantly. Docker containers are lightweight and share the host OS kernel, which makes them faster and more efficient. In contrast, VMs include a full OS with a hypervisor, resulting in more overhead and slower performance.

***

## Getting Started with Docker

### Installation

1. Download Docker Desktop from [Docker's official website](https://www.docker.com/).
2. Follow the installation instructions for your operating system.
3.  Verify installation by running:

    ```bash
    docker --version
    ```

***

## Creating a Docker Image with a Dockerfile

A **Dockerfile** is a script that contains instructions to build a Docker image.

### Example Dockerfile

Below is a sample Dockerfile for a simple Python application:

```dockerfile
# Use an official Python runtime as a base image
FROM python:3.9-slim

# Set the working directory inside the container
WORKDIR /app

# Copy the current directory's content to the container's /app directory
COPY . /app

# Install application dependencies
RUN pip install --no-cache-dir -r requirements.txt

# Expose the application port
EXPOSE 5000

# Command to run the application
CMD ["python", "app.py"]
```

### Explanation of Dockerfile Commands

* `FROM`: Specifies the base image (e.g., `python:3.9-slim`).
* `WORKDIR`: Sets the working directory inside the container.
* `COPY`: Copies files from the host to the container.
* `RUN`: Executes commands during the build process (e.g., install dependencies).
* `EXPOSE`: Documents the port the container will use.
* `CMD`: Specifies the command to run when the container starts.

### Build a Docker Image

To build a Docker image from the Dockerfile:

```bash
docker build -t my-python-app .
```

* `-t`: Tags the image with a name (`my-python-app`).
* `.`: Refers to the current directory containing the Dockerfile.

***

## Security Best Practices for Docker Images

### 1. Use Official Base Images

* Start with minimal and verified base images, such as those from trusted repositories like `python:3.9-slim`.

### 2. Minimize Layers

* Combine related commands into a single `RUN` instruction to reduce the image size.

```dockerfile
RUN apt-get update && apt-get install -y curl && rm -rf /var/lib/apt/lists/*
```

### 3. Avoid Hardcoding Secrets

* Never store sensitive data (e.g., passwords, API keys) in the Dockerfile. Use environment variables or secret management tools.

### 4. Use Multi-Stage Builds

* Use a build stage to compile or build your application, and a separate, smaller stage for the final image.

```dockerfile
FROM golang:1.18 AS builder
WORKDIR /app
COPY . .
RUN go build -o main .

FROM alpine:latest
COPY --from=builder /app/main .
CMD ["./main"]
```

### 5. Regularly Update Images

* Update base images and dependencies to fix vulnerabilities.

### 6. Scan Images for Vulnerabilities

* Use tools like `docker scan` to identify security issues:

```bash
docker scan my-python-app
```

***

## Using the `.dockerignore` File

The `.dockerignore` file is used to exclude files and directories from being included in the Docker image during the build process. This reduces the image size and improves security.

### Example `.dockerignore` File

```plaintext
# Ignore log files
*.log

# Ignore node_modules directory
node_modules/

# Ignore git files
.git

# Ignore temporary files
*.tmp
```

### Benefits of Using `.dockerignore`

* **Smaller Images:** Exclude unnecessary files, reducing image size.
* **Improved Build Performance:** Avoid copying large files or directories.
* **Enhanced Security:** Prevent sensitive files (e.g., `.env`) from being included.

To use `.dockerignore`, place it in the same directory as your Dockerfile. Docker automatically respects this file during the `docker build` process.

***

## Running a Docker Container

### Start a Container

Run a container using the built image:

```bash
docker run -d -p 5000:5000 --name my-container my-python-app
```

* `-d`: Runs the container in detached mode.
* `-p`: Maps host port 5000 to container port 5000.
* `--name`: Assigns a name to the container (`my-container`).

### View Running Containers

```bash
docker ps
```

### Stop a Container

```bash
docker stop my-container
```

### Remove a Container

```bash
docker rm my-container
```

***

## Managing Docker Images

### Pull an Image

Download an image from Docker Hub:

```bash
docker pull nginx
```

### Push an Image

Push a locally built image to Docker Hub:

```bash
docker push my-username/my-python-app
```

### Remove an Image

Delete a local image:

```bash
docker rmi my-python-app
```

***

## Working with Volumes

Volumes allow you to persist data outside of containers.

### Create and Attach a Volume

```bash
docker volume create my-volume
```

Run a container with a volume:

```bash
docker run -d -p 5000:5000 --name my-container -v my-volume:/app/data my-python-app
```

* `-v my-volume:/app/data`: Mounts the volume `my-volume` to `/app/data` inside the container.

### List Volumes

```bash
docker volume ls
```

### Remove a Volume

```bash
docker volume rm my-volume
```

***

## Docker Commands Cheat Sheet

| Command                                                               | Description                                  |
| --------------------------------------------------------------------- | -------------------------------------------- |
| `docker --version`                                                    | Check Docker version                         |
| `docker build -t <name> .`                                            | Build a Docker image                         |
| `docker run -d -p <host-port>:<container-port> --name <name> <image>` | Run a container                              |
| `docker ps`                                                           | List running containers                      |
| `docker ps -a`                                                        | List all containers (including stopped ones) |
| `docker stop <container>`                                             | Stop a running container                     |
| `docker rm <container>`                                               | Remove a container                           |
| `docker pull <image>`                                                 | Pull an image from Docker Hub                |
| `docker push <image>`                                                 | Push an image to Docker Hub                  |
| `docker rmi <image>`                                                  | Remove a Docker image                        |
| `docker volume create <name>`                                         | Create a volume                              |
| `docker volume ls`                                                    | List all volumes                             |
| `docker volume rm <name>`                                             | Remove a volume                              |
| `docker exec -it <container> <command>`                               | Execute a command inside a running container |
| `docker logs <container>`                                             | View logs of a container                     |
| `docker inspect <container>`                                          | Inspect detailed container information       |
| `docker images`                                                       | List all local Docker images                 |
| `docker scan <image>`                                                 | Scan a Docker image for vulnerabilities      |

***
