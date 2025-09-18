# Docker

## Installing Docker

### Docker Editions

1. **Docker CE (Community Edition)** – free, open-source edition for developers and small teams.
    
2. **Docker EE (Enterprise Edition)** – commercial edition with additional features and enterprise support.
    
3. **Docker Enterprise** – broader enterprise platform that includes orchestration and advanced security.
    

### Docker Update Channels

1. **Stable** – latest releases intended for general availability.
    
2. **Test** – pre-releases ready for testing before general availability.
    
3. **Nightly** – latest work-in-progress builds for the next major release.
    

### Docker Support

- **Docker CE**: Each year-month release is supported with patches for **7 months** after GA.
    
- **Docker EE**: Each year-month release is supported for **24 months** after GA.
    

### Docker Installation

#### 1. Windows

- Requires **Virtualization enabled** in BIOS (Intel VT-x or AMD-V).
    
- Docker and other virtualization tools (VirtualBox, VMware) **cannot run simultaneously** on the same host.
    
- Download Docker Desktop from the official site.
    
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
    

#### 3. Linux (extra point added)

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

- A **container** is a standard unit of software that runs a particular application and its processes.
    
- It is **portable** and contains the software dependencies for an application.
    
- It is common to run **multiple containers on a single host machine**.
    

### Docker Container Benefits

- Containers are **self-contained** and do not alter the host system.
    
- Lightweight compared to virtual machines.
    
- Provide **reproducible and consistent environments**.
    
- Have a **smaller footprint** than VMs.
    
- Reduce the number of servers required.
    
- Easily managed with **orchestrators** (e.g., Kubernetes, Docker Swarm).
    
- Easy to **create, store, and run** container images.
    
- Use **Docker Hub** as an image repository for pre-built images.
    
- Initially used **AUFS** filesystem, now commonly uses **OverlayFS**.
    

### Virtual Machines vs Containers

- Containers are designed for a **single process or task**, while VMs may run multiple processes.
    
- Containers have **faster boot times** since they share the host OS kernel.
    

### Docker Security

- Containers are isolated from each other.
    
- Multiple containers share the host machine’s kernel.
    
- **Container escape** (security risk) may occur → attackers could break isolation.
    
- Docker uses isolation techniques:
    
    - **cgroups (control groups)** – enforce resource limits.
        
    - **Namespaces** – provide process isolation.
        

### Docker Basics

- Docker uses containers to run a **single process or a small group of processes**.
    
- A **container image** is required to start a container.
    
- Images are stored in an **image registry** (e.g., Docker Hub).
    
- To build an image, you need a **Dockerfile**.
    

### Base Images and Layering

- A **base image** is a minimal functional OS.
    
- Docker uses a **layered filesystem**:
    
    - Example:
        
        ```dockerfile
        FROM debian:stable
        ```
        
- Changes to the base image are stored in **new layers** without modifying the original base.
    

### Microservices

- An **architectural style** where applications are built as loosely coupled services.
    
- Easier to fix and test.
    
- Each microservice can be **deployed independently**.
    
- Containers are **ideal for microservices** due to isolation and portability.
    

### Summary

- A **container** is a unit of software that runs an application and its processes.
    
- Multiple containers can run on a **single host machine**.
    

---

## Basic Commands

### Getting Started

- Docker commands are the same across **Linux, macOS, and Windows**.
    

#### Starting Terminal

- **Windows**: Open CMD / PowerShell as Administrator.
    
- **macOS**: Open **Terminal** (Utilities folder).
    
- **Linux**: Open terminal.
    

#### Running a Container

- Run Debian container:
    
    ```bash
    docker run -dit debian
    ```
    
- Returns a container ID, e.g.:
    
    ```
    b96ca51ec34d16e6050a114e37b372cc804876ab8c7cd095fa7e067f308ef2b4b2
    ```
    

#### Options

- `-dit`
    
    - `d` – Detached (runs in background).
        
    - `i` – Interactive (keeps STDIN open).
        
    - `t` – Allocates a pseudo-terminal.
        

#### Checking Running Containers

```bash
docker ps
```

Output:

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

**Note:** If you run `docker run debian` without options, the container stops immediately because it is not detached.

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

Example:

```json
{
  "Id": "sha256:833c135acfe9521d7a0035a296076f98c182c542a2b6b5a0fd7063d355d696be",
  "RepoTags": ["debian:latest"],
  "Architecture": "amd64",
  "Os": "linux",
  "Size": 49289936,
  "RootFS": {
    "Type": "layers",
    "Layers": [
      "sha256:185e04da9d947141fd703dbf36361bdc2ff77cc27cbf500fb9f4881cb5ddbe95"
    ]
  }
}
```

#### Help Commands

- General help:
    
    ```bash
    docker --help
    ```
    
- Help for a subcommand:
    
    ```bash
    docker images --help
    ```
    

---
## Managing Docker Containers