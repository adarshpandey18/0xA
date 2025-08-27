# Docker

## Installing Docker

### Docker Editions
1. Docker CE : Community Edition
2. Docker EE : Enterprise Edition
3. Docker Enterprise 

### Docker Update Channel
1. Stable : gives you latest releases for general availability.
2. Test : gives pre-releases that are ready for testing before general availability.
3. Nightly : gives you latest builds of work in progress for next major release.
### Docker Support
- Docker CE releases of a year-month branch are supported with patches as needed for 7 months after the first year-month general availability release.
- Docker EE releases are supported 24 months after the first year-month general availability release.

### Docker Installation

#### 1. Windows
- Docker requires that Virtualization be enabled in BIOS  VT -x or AMD -V
- Docker and other virtualization software such as VirtualBox or VMWare can NOT run on the same host.
- Download Docker through web
- check docker after installation `docker version`
#### 2. MacOs
- downlaod docker --> go to application --> double click on docker --> click on open --> give password --> docker installed
- `docker version` to check the version of docker installed.

## Introduction to Docker
### Docker History
Docker didn't invent container but it made container easier to work with.

### What is Container ?
- A container is a standard unit of software that run a particular application and its associated processes.
- A container is portable and contains the software dependencies for a givena application
- It is commonly to run several container at once on a single unit host of machine

### Docker Container Benefits
- Container are self contained and do not alter the host system that are running on.
- Docker is lightweight
- Containers provide reproducible and consistent environments. If its works in development it will run on other environment
- Container have a smaller footprint than virtual machine.
- Using containers can reduce the number of server required
- Orchestrators can be used to manage multiple container
- Docker provides an easy to use way to create store and run container images.
- An easy to use image file format to use --> image repository is called docker hub where people share pre built images for easy to use.
- Docker originally used Aufs for container filesystem layer but has since moved to OverlayFS


### virtual machine vs containers
- Container are used for a single process or task, while virtual machine may run multiple process or task
- Container boot times are much quicker than virtual machines (as it uses host OS underlying)

### Docker Security
- Docker isolates container from each other.
- Multiple container on a host machine will always share the kernel of the host machine.
- Container escape might occur (explain)
- Docker uses isolation technique such as cgroup (control group) resouce quotas and namespaces.


### Docker Basics
- Docker uses container to run single process or a  small group of process to provide a service.
- A container image is required to start a container and these images  can be held in an online library called an image registry.
- To create a docker image you need a DockerFile

### Base Images and Layering
- A base image is a tiny but functioanl Operating System
- Docker uses a layered filesystem so that you can add to a base image
	- FROM debian:stable
- Changes made to the base image are actually stored in new layer and do not alter the base image.

### Microservices
- Microservices in a architectural style that structres an application as a collection of loosely coupled services.
- Microservices are easier to fix and test
- Each microservice can be deployed without the need to deploy the whole application
- Docker containner are ideal for microservices.

### Summary 
- A container is a standard unit of software that can run a particular application and its application processes.
- It is common to run several container at once a single host machine.

