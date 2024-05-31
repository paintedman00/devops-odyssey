# Docker

## Table of Contents
1. [Introduction to Docker](##introduction-to-docker)
2. [Installation](#installation)
3. [Docker Basics](#docker-basics)
4. [Container Manipulation](#container-manipulation)
5. [Image Manipulation](#image-manipulation)
6. [Volumes and Bind Mounts](#volumes-and-bind-mounts)
7. [Networking](#networking)
8. [Docker Compose](#docker-compose)
9. [Docker Registry](#docker-registry)
10. [Advanced Docker Commands](#advanced-docker-commands)
11. [Docker Swarm](#docker-swarm)
12. [Security Best Practices](#security-best-practices)
13. [CI/CD Integration](#cicd-integration)
14. [Monitoring and Logging](#monitoring-and-logging)
15. [Docker on Kubernetes](#docker-on-kubernetes)
16. [Docker for Development](#docker-for-development)
17. [Best Practices](#best-practices)
18. [References](#references)

## 1. Introduction to Docker

### What is Docker?
Docker is an open platform for developing, shipping, and running applications. Docker enables you to separate your applications from your infrastructure so you can deliver software quickly.

### Docker Engine
Docker Engine is a client-server application with the following major components:
- A server (daemon process) called `dockerd`.
- A REST API to communicate with the daemon.
- A command line interface (CLI) client `docker`.

### Docker Architecture
Docker uses a client-server architecture:
- The Docker client communicates with the Docker daemon, which handles building, running, and distributing Docker containers.
- They can run on the same system or connect remotely.

### Docker Objects
- **Image**: A read-only template for creating containers, including the code, runtime, libraries, environment variables, and config files.
- **Container**: A runnable instance of an image. Containers are isolated from each other and the host system.
- **Network**: Connects Docker containers to each other and to external networks.
- **Volume**: Provides persistent storage for Docker containers.

## 2. Installation

### How to Install Docker
- **macOS**: Install using Homebrew or download from Docker's official website.
- **Windows**: Install using the Docker Desktop installer.
- **Linux**: Use the package manager for your distribution (e.g., `apt` for Ubuntu, `yum` for CentOS).

## 3. Docker Basics

### Hello World in Docker
```bash
docker run hello-world
```

### Basic Commands
- **List all Docker images**:
  ```bash
  docker images
  ```
- **Running Ubuntu Bash**:
  ```bash
  docker run -ti ubuntu:latest
  ```
- **List of containers**:
  ```bash
  docker ps -a
  ```
- **Docker commit**:
  ```bash
  docker commit <container_id> <new_image_name>
  ```

## 4. Container Manipulation

### Running and Managing Containers
- **Run a container**:
  ```bash
  docker run <image_name>
  ```
- **Start/Stop/Restart a container**:
  ```bash
  docker start/stop/restart <container_id>
  ```
- **Run a container in detached mode**:
  ```bash
  docker run -d <image_name>
  ```
- **Publish container ports to the host**:
  ```bash
  docker run -p <host_port>:<container_port> <image_name>
  ```
- **Execute commands inside a running container**:
  ```bash
  docker exec -it <container_id> <command>
  ```

### Inspecting Containers
- **List running containers**:
  ```bash
  docker ps
  ```
- **Fetch logs of a specific container**:
  ```bash
  docker logs <container_id>
  ```
- **Inspect detailed information about a container**:
  ```bash
  docker inspect <container_id>
  ```

## 5. Image Manipulation

### Building and Managing Images
- **Build an image from a Dockerfile**:
  ```bash
  docker build -t <image_name> .
  ```
- **Tag Docker images**:
  ```bash
  docker tag <image_id> <repository>:<tag>
  ```
- **List and remove Docker images**:
  ```bash
  docker images
  docker rmi <image_id>
  ```

### Sharing Images
- **Push an image to a Docker registry**:
  ```bash
  docker push <image_name>
  ```
- **Pull an image from a Docker registry**:
  ```bash
  docker pull <image_name>
  ```

## 6. Volumes and Bind Mounts

### Working with Volumes
- **Create a Docker volume**:
  ```bash
  docker volume create <volume_name>
  ```
- **List available Docker volumes**:
  ```bash
  docker volume ls
  ```
- **Mount a host directory or volume to a container**:
  ```bash
  docker run -v <host_path>:<container_path> <image_name>
  ```

### Working with Bind Mounts
- **Create and use bind mounts**:
  ```bash
  docker run -v /path/to/host:/path/to/container <image_name>
  ```

## 7. Networking

### Basic Network Commands
- **Create a Docker network**:
  ```bash
  docker network create <network_name>
  ```
- **List available Docker networks**:
  ```bash
  docker network ls
  ```
- **Inspect a Docker network**:
  ```bash
  docker network inspect <network_name>
  ```

### Connecting Containers
- **Connect a container to a network**:
  ```bash
  docker network connect <network_name> <container_name>
  ```
- **Disconnect a container from a network**:
  ```bash
  docker network disconnect <network_name> <container_name>
  ```

### Types of Docker Networks
- **Bridge Network**: Default network driver, suitable for container-to-container communication within the same host.
  ```bash
  docker network create --driver bridge my_bridge
  ```
- **Host Network**: Shares the host’s networking namespace.
  ```bash
  docker run --network host my_container
  ```
- **Overlay Network**: Suitable for multi-host networking, requires Docker Swarm or Kubernetes.
  ```bash
  docker network create -d overlay my_overlay
  ```
- **None Network**: Completely isolates the container.
  ```bash
  docker run --network none my_container
  ```

### Custom Networks
- **Creating a Custom Bridge Network**:
  ```bash
  docker network create my_custom_bridge
  docker run --network my_custom_bridge my_container
  ```

## 8. Docker Compose

### Docker Compose Basics
- **Start services**:
  ```bash
  docker-compose up
  ```
- **Stop services**:
  ```bash
  docker-compose down
  ```
- **List services**:
  ```bash
  docker-compose ps
  ```
- **Execute commands inside a running service**:
  ```bash
  docker-compose exec <service_name> <command>
  ```

### Advanced Usage
- **Using Multiple Compose Files**:
  ```yaml
  # docker-compose.yml
  version: '3'
  services:
    web:
      image: my_web_app:latest
      ports:
        - "80:80"

  # docker-compose.override.yml
  version: '3'
  services:
    web:
      environment:
        - DEBUG=true
  ```
  ```bash
  docker-compose -f docker-compose.yml -f docker-compose.override.yml up
  ```

- **Environment Variables in Compose**:
  ```yaml
  # docker-compose.yml
  version: '3'
  services:
    web:
      image: my_web_app:latest
      environment:
        - APP_ENV=production
  ```

## 9. Docker Registry

### Managing Docker Registry
- **Log in to a Docker registry**:
  ```bash
  docker login
  ```
- **Log out from a Docker registry**:
  ```bash
  docker logout
  ```
- **Search for Docker images**:
  ```bash
  docker search <term>
  ```

## 10. Advanced Docker Commands

### Clean Up Commands
- **Remove all unused Docker resources**:
  ```bash
  docker system prune
  ```
- **Remove all stopped containers**:
  ```bash
  docker container prune
  ```
- **Remove unused images**:
  ```bash
  docker image prune
  ```

### Docker Filesystem Commands
- **Copy files from a container to the host**:
  ```bash
  docker cp <container_id>:<container_path> <host_path>
  ```
- **Copy files from the host to a container**:
  ```bash
  docker cp <host_path> <container_id>:<container_path>
  ```

## 11. Docker Swarm

### Swarm Commands
- **Initialize a Docker swarm**:
  ```bash
  docker swarm init
  ```
- **Join a Docker swarm as a worker node**:
  ```bash
  docker swarm join
  ```
- **List the nodes in a Docker swarm**:
  ```bash
  docker node ls
  ```
- **Create a service in the Docker swarm**:
  ```bash
  docker service create --name <service_name> <image_name>
  ```
- **Scale the replicas of a service in

 the Docker swarm**:
  ```bash
  docker service scale <service_name>=<replicas>
  ```

## 12. Security Best Practices

### Docker Bench for Security
```bash
docker run -it --net host --pid host --cap-add audit_control \
  -v /var/lib:/var/lib -v /var/run/docker.sock:/var/run/docker.sock \
  --label docker_bench_security \
  docker/docker-bench-security
```

### User Namespaces
```json
{
  "userns-remap": "default"
}
```
Add to `/etc/docker/daemon.json`.

### Additional Security Practices
- Regularly update your Docker images.
- Use Docker's built-in security features (e.g., user namespaces, seccomp profiles).
- Scan images for vulnerabilities using tools like Clair or Trivy.

## 13. CI/CD Integration

### Using Docker with Jenkins
```groovy
pipeline {
    agent {
        docker {
            image 'maven:3-alpine'
            args '-v /root/.m2:/root/.m2'
        }
    }
    stages {
        stage('Build') {
            steps {
                sh 'mvn -B clean package'
            }
        }
    }
}
```

### Integrating Docker with CI Tools
- **GitHub Actions**: Use Docker containers to run jobs.
- **GitLab CI**: Define Docker images for different stages in the pipeline.

## 14. Monitoring and Logging

### Using Prometheus and Grafana
- Prometheus configuration for Docker monitoring.
- Grafana dashboards for visualizing Docker metrics.

### Docker's Built-in Stats and Events
- **Display live stream of container resource usage**:
  ```bash
  docker stats
  ```
- **Monitor Docker events**:
  ```bash
  docker events
  ```

## 15. Docker on Kubernetes

### Basic Kubernetes Concepts
- **Pods**: The smallest deployable units in Kubernetes.
  ```yaml
  apiVersion: v1
  kind: Pod
  metadata:
    name: my-pod
  spec:
    containers:
    - name: my-container
      image: my_image
  ```

### Differences Between Docker Swarm and Kubernetes
- Highlight key differences in orchestration, scalability, and complexity.

## 16. Docker for Development

### Using Docker for Local Development
- **Setting up a development environment with Docker**.
- **Using Docker volumes for live code reloading**.

### Example Development Setup
- **Dockerfile for a Node.js application**:
  ```Dockerfile
  FROM node:lts-alpine
  WORKDIR /app
  COPY package.json ./
  RUN npm install
  COPY . .
  CMD ["npm", "start"]
  ```

- **Docker Compose for development**:
  ```yaml
  version: '3'
  services:
    app:
      build: .
      volumes:
        - .:/app
      ports:
        - "3000:3000"
      environment:
        - NODE_ENV=development
  ```

## 17. Best Practices

### Optimizing Docker Images
- Use multi-stage builds to reduce image size.
- Embrace Alpine Linux for smaller, secure images.
- Avoid installing unnecessary packages.

### Security Practices
- Regularly update your Docker images.
- Use Docker's built-in security features (e.g., user namespaces, seccomp profiles).
- Scan images for vulnerabilities using tools like Clair or Trivy.

## 18. References
1. [Docker Documentation](https://docs.docker.com/)
2. [Docker Cheat Sheet](https://github.com/wsargent/docker-cheat-sheet)
3. [Docker Hub](https://hub.docker.com/)



