# Docker

## Installing Docker

### Docker Editions

1. **Docker CE (Community Edition)** – Free, open-source edition for developers and small teams.
    
2. **Docker EE (Enterprise Edition)** – Commercial edition with additional features and enterprise support.
    
3. **Docker Enterprise** – Broader enterprise platform that includes orchestration and advanced security.
    

---

### Docker Update Channels

1. **Stable** – Latest releases intended for general availability.
    
2. **Test** – Pre-releases ready for testing before general availability.
    
3. **Nightly** – Latest work-in-progress builds for the next major release.
    

---

### Docker Support

- **Docker CE**: Each year-month release is supported with patches for **7 months** after GA.
    
- **Docker EE**: Each year-month release is supported for **24 months** after GA.
    

---

### Docker Installation

#### 1. Windows

- Requires **Virtualization enabled** in BIOS (Intel VT-x or AMD-V).
    
- Docker and other virtualization tools (VirtualBox, VMware) **cannot run simultaneously** on the same host.
    
- Download **Docker Desktop** from the official website.
    
- Verify installation:
    
    ```bash
    docker version
    ```
    

#### 2. macOS

- Download Docker Desktop → Move to Applications → Double-click Docker → Click **Open** → Enter password → Installed.
    
- Verify installation:
    
    ```bash
    docker version
    ```
    

#### 3. Linux

- Update packages:
    
    ```bash
    sudo apt-get update
    ```
    
- Install Docker:
    
    ```bash
    sudo apt-get install docker.io -y
    ```
    
- Verify installation:
    
    ```bash
    docker --version
    ```
    

---

## Introduction to Docker

### Docker History

- Docker did not invent containers but made them much **easier to use and manage**.
    

### What is a Container?

- A **container** is a standard unit of software that runs an application and its dependencies.
    
- Containers are **portable**, **isolated**, and **lightweight**.
    
- It is common to run **multiple containers** on a single host machine.
    

### Docker Container Benefits

- Containers are **self-contained** and do not alter the host system.
    
- Lightweight compared to virtual machines.
    
- Provide **reproducible and consistent environments**.
    
- Have a **smaller footprint** than VMs.
    
- Reduce the number of servers required.
    
- Managed easily with **orchestrators** (Kubernetes, Docker Swarm).
    
- Easy to **create, store, and run** container images.
    
- Use **Docker Hub** for sharing pre-built images.
    
- Initially used **AUFS**, now commonly uses **OverlayFS** for the filesystem.
    

### Virtual Machines vs Containers

- Containers run a **single process or service**, while VMs can run multiple.
    
- Containers have **faster startup times** since they share the host OS kernel.
    

### Docker Security

- Containers are **isolated from each other**.
    
- Multiple containers **share the same kernel**.
    
- **Container escape** can occur if isolation breaks (a potential security risk).
    
- Docker uses isolation techniques like:
    
    - **cgroups (control groups)** – Enforce resource limits.
        
    - **Namespaces** – Isolate processes.
        

### Docker Basics

- Docker runs **a single process or group of processes** inside containers.
    
- Containers are created from **images**, stored in **registries** (e.g., Docker Hub).
    
- **Dockerfile** defines instructions to build an image.
    

### Base Images and Layering

- A **base image** is a minimal functional OS used to build other images.
    
- Docker uses a **layered filesystem**:
    
    ```dockerfile
    FROM debian:stable
    ```
    
- Each modification adds a **new layer**; base layers remain unchanged.
    

### Microservices

- **Microservices architecture** divides applications into **independent, loosely coupled services**.
    
- Easier to fix, test, and deploy independently.
    
- Containers are **ideal for microservices**.
    

### Summary

- A **container** is a unit of software that runs an application and its processes.
    
- Multiple containers can run on a **single host machine**.
    

---

## Basic Commands

### Getting Started

- Docker commands are **the same on Linux, macOS, and Windows**.
    

#### Starting the Terminal

- **Windows**: Open CMD / PowerShell (Admin mode).
    
- **macOS**: Open **Terminal** (Utilities folder).
    
- **Linux**: Open terminal.
    

#### Running a Container

```bash
docker run -dit debian
```

Returns a container ID, e.g.:

```
b96ca51ec34d16e6050a114e37b372cc804876ab8c7cd095fa7e067f308ef2b4b2
```

#### Options

- `-d` – Detached (runs in background).
    
- `-i` – Interactive mode (keeps STDIN open).
    
- `-t` – Allocates a pseudo-terminal (interactive shell).
    

#### Checking Running Containers

```bash
docker ps
```

Example:

```
CONTAINER ID   IMAGE     COMMAND   CREATED          STATUS          PORTS     NAMES
b96ca51ec34d   debian    "bash"    43 seconds ago   Up 42 seconds             quirky_benz
```

#### Stopping a Container

```bash
docker stop <container_id>
docker stop <container_name>
```

> Example: `docker stop quirky_benz`

**Note:** Running `docker run debian` (without `-d`) will stop immediately after execution.

#### Viewing Downloaded Images

```bash
docker images
```

#### Inspecting an Image

```bash
docker inspect <image_id>
```

#### Help Commands

```bash
docker --help
docker images --help
```

---

## Managing Docker Containers

### Container Images

#### Pulling an Image

```bash
docker pull nginx
```

#### Listing Images

```bash
docker images
```

#### Viewing Image History

```bash
docker history nginx
```

#### View Full Image IDs

```bash
docker images --no-trunc
```

#### Tagging an Image

```bash
docker tag nginx:latest nginx:myblog_stable
```

#### Building an Image

```bash
docker build -t mynginx .
```

#### Removing Images

```bash
docker rmi <image:tag>
docker rmi -f <image:tag>  # Force delete
```

#### Cleaning Up Unused Images

```bash
docker image prune
docker system prune -a
```

#### Checking Docker Disk Usage

```bash
docker system df
```

---

## Running and Managing Containers

### Running Containers

```bash
docker run -dit debian
```

#### Assigning a Name

```bash
docker run -dit --name web debian
```

#### Listing Containers

```bash
docker ps        # Running containers
docker ps -a     # All containers (including stopped)
docker ps -l     # Last created container
```

#### Auto-Restart on System Boot

```bash
docker run -dit --restart=always --name name debian
```

#### Remove Container Automatically

```bash
docker run --rm -dit debian
```

#### Viewing Logs

```bash
docker logs <container_name>
docker logs -f <container_name>  # Live logs
docker logs -t <container_name>  # Timestamps
```

---

## Exposing Containers to Public Network

#### Run Nginx and Expose Port

```bash
docker run --name our_nginx -d -p 8080:80 nginx
```

- **8080** → Host port (external)
    
- **80** → Container port (internal)
    

#### Verify

```bash
curl http://localhost:8080
```

#### Creating a Local Website

```powershell
mkdir webpages
cd webpages
echo "Hi from the container!" > index.html
```

#### Mount Local Directory to Container

```bash
docker run -p 8080:80 --name another_nginx -v ${PWD}/webpages:/usr/share/nginx/html:ro -d nginx
```

- `-v` → Mounts a volume (binds host folder to container path).
    
- `:ro` → Read-only mount.
    

---

## Connecting to Running Containers and Managing Output

### Entering and Connecting to Containers

```bash
docker run -it --name apache httpd /bin/bash
```

- We didn’t use `-d` because we want to run it in **foreground**.
    
- `/bin/bash` provides shell access.
    
- Use `exit` to leave the container shell.
    

#### Start Container in Background, Then Access

```bash
docker run -dit httpd
docker exec -it <container_id> /bin/bash
docker exec -it <container_id> sh
```

> Sometimes `sh` requires a full path (e.g. `/bin/sh`).

---

## Building Images with Dockerfiles

### Docker Registries

- **Docker Hub** is the default registry.
    
- The **registry** stores image repositories.
    
- A **repository** contains multiple image versions (tags).
    

```bash
docker pull docker.io/ubuntu:bionic
docker pull registry.hub.docker.com/library/ubuntu:bionic
```

> Both commands refer to different repository paths.

To run:

```bash
docker run -dit registry.hub.docker.com/library/ubuntu:bionic
```

#### Accessing Private Repositories

```bash
docker login
```

Prompts for Docker Hub **username** and **password**.

---

### Dockerfile Instructions

- `FROM` – Sets the base image.
    
- `CMD` – Defines the command to execute when the container runs.
    
- `RUN` – Executes commands while building the image.
    
- `EXPOSE` – Opens networking ports.
    
- `VOLUME` – Defines persistent storage paths.
    
- `COPY` – Copies files into the image.
    
- `LABEL` – Adds metadata (key-value pairs).
    
- `ENV` – Defines environment variables.
    
- `ENTRYPOINT` – Defines the executable to run when the container starts (use `CMD` to pass arguments).
    

#### Example

```dockerfile
FROM alpine:latest
LABEL maintainer="Adarsh Pandey"
ENTRYPOINT ["bin/ping"]
CMD ["www.docker.com"]
```

> The Dockerfile name should always be **"Dockerfile"** (capital D).

Build and run:

```bash
docker build -t adarsh/dockerping .
docker push adarsh/dockerping
docker run adarsh/dockerping
docker run adarsh/dockerping google.com
```

---

## Docker Volumes

### Managing Docker Volumes

#### Images

- Images are **portable and disposable**.
    
- Contain only required packages for their service.
    
- Ideally, you should be able to discard containers **without losing data**.
    

#### Volumes

- Use **volumes** to persist or share container data.
    
- Volumes can be **shared** between multiple containers.
    

#### Old Volume Method (-v)

```bash
docker run -v /dbdir:/var/lib/mysql -d mariadb
docker run --volume /dbdir:/var/lib/mysql -d mariadb
```

#### New Method (–mount)

```bash
docker volume create testdata
docker run -d --name withvolume --mount source=testdata,destination=/root/volume nginx
```

> No spaces allowed between mount parameters.

#### Volume Management

```bash
docker volume ls
docker volume inspect testdata
docker volume rm testdata
```

Example output:

```json
[
 {
   "CreatedAt": "2025-10-14T08:45:00Z",
   "Driver": "local",
   "Labels": {},
   "Mountpoint": "/var/lib/docker/volumes/testdata/_data",
   "Name": "testdata",
   "Options": {},
   "Scope": "local"
 }
]
```

#### Ephemeral Volumes

- Temporary volumes that are removed when the container stops.
    

---
## Docker Swarm

### Docker Swarm / Swarm Mode

#### Orchestrators

- **Auto scale up:** Adds more containers as workload increases.
    
- **Auto scale down:** Removes containers when workload decreases.
    
- **High availability:** Keeps essential services running.
    
- **Garbage collection:** Removes failed or stopped containers.
    

#### Docker Swarm

- Docker Swarm = **Swarm Mode**.
    
- Provides **high availability** by clustering Docker hosts.
    
- A **Node** is any system participating in the swarm.
    
- Components include **Docker Engines, Managers, and Workers**.
    
- **Replicas (Scaling):** Add containers to handle load.
    
- **Encrypts** communication between nodes.
    
- Provides **internal networking** and **service discovery**.
    

---
