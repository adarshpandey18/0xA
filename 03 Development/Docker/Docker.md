# Docker

## Installing Docker

### Docker Editions

1. **Docker CE (Community Edition)** – free, open-source edition for developers and small teams.
    
2. **Docker EE (Enterprise Edition)** – commercial edition with additional features and enterprise support.
    
3. **Docker Enterprise** – broader enterprise platform that includes orchestration and advanced security.
    

---

### Docker Update Channels

1. **Stable** – latest releases intended for general availability.
    
2. **Test** – pre-releases ready for testing before general availability.
    
3. **Nightly** – latest work-in-progress builds for the next major release.
    

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
    
- **Container escape** can occur if isolation breaks (potential security risk).
    
- Docker uses isolation techniques like:
    
    - **cgroups (control groups)** – enforce resource limits.
        
    - **Namespaces** – isolate processes.
        

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

- Docker commands are **same on Linux, macOS, and Windows**.
    

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

Example Output:

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

Output:

```
REPOSITORY   TAG       IMAGE ID       CREATED       SIZE
debian       latest    833c135acfe9   10 days ago   183MB
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

Downloads an image from Docker Hub and adds it to the local host.

#### Listing Images

```bash
docker images
```

#### Viewing Image History

```bash
docker history nginx
```

Displays each layer in the image build process.

#### View Full Image IDs

```bash
docker images --no-trunc
```

Shows the complete image ID.

#### Tagging an Image

```bash
docker tag nginx:latest nginx:myblog_stable
```

Creates an alias (`myblog_stable`) pointing to the same image (no copy is made).

#### Building an Image

```bash
docker build -t mynginx .
```

- `-t` – Tags the image with a name.
    
- `.` – Uses the current directory for the Dockerfile.
    

#### Removing Images

```bash
docker rmi <image:tag>
docker rmi -f <image:tag>  # Force delete
```

#### Cleaning Up Unused Images

```bash
docker image prune
```

Removes **dangling and unused** images.

```bash
docker system prune -a
```

Removes **unused containers, networks, and images**.

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

#### Stopping and Restarting

```bash
docker stop web
```

#### Auto-Restart on System Boot

```bash
docker run -dit --restart=always --name name debian
```

#### Force Stop

```bash
docker kill <container_name>
```

#### Remove a Container

```bash
docker rm <container_name>
```

#### Auto-Remove When Stopped

```bash
docker run --rm -dit debian
```

Removes the container automatically after it stops.

#### View Logs

```bash
docker logs <container_name>
docker logs --help
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

Returns HTTP 200 response with Nginx welcome page.

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
    
- `:ro` → Mounts directory as **read-only**.
    

This makes your local `index.html` accessible at `http://localhost:8080`.

---

## Connecting to Running Containers and Managing Output



---
