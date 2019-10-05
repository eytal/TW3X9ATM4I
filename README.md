# A collection of resources from Redhat OpenShift Developer Bootcamp and containers

## For using and practicing Docker containers
with container orchestration
https://github.com/docker/labs

## For practicing bash
https://dev.to/awwsmm/101-bash-commands-and-tips-for-beginners-to-experts-30je

## Things to know when running on Windows
A container is a lightweight virtual machine that runs on top of the host OS (your main OS)
To run linux containers, you need to have a hypervisor which is a software for running virtual machines.
On windows, the hypervisor is called Hyper-V and is only available on Windows Professional and above

You may need to enable hardware virtualization in your system BIOS, usually this is enabled by default
It is strongly recommended to use Docker Desktop available for Windows Pro and MacOS

If you do use Windows Home, check out docker toolbox and docker engine
otherwise, you can run docker natively inside a Virtual Machine with linux installed, such as Ubuntu 

## Things to know about containers
Docker is not the only tool for containers, the Dockerfile and the commands are standardised.
Check out Cloud Native Computing Foundation, OCI 
### A good combination is: 
#### For use on linux systems.
- podman
- buildah
- skopeo

## Learning objectives to achieve
- Virtual machine vs containers - what is the difference?
- How does docker work?
- Container architecture with 3-tier architecture and microservices architecture
- How to build, run and deploy container images
- How to create a custom container image
- Build multi-container applications
- What is container orchestration
- Linux-based operating systems and what what is the linux kernel?
- What is OCI and alternatives to docker

## Essential instructions in the Dockerfile to know
> Checkout https://docs.docker.com/reference/

**You need to have a basic understanding of linux operating systems and bash**
> **bash:** cp, rm, rm -rf, chmod, chgrp, chown, mv, mkdir, cat, less, grep
>
> **package manager for linux distros**: yum, apt, apt-get, pacman 
- **FROM**
    - pulls an image from container image registries based on tag:version
- **RUN**
    - runs a command line in bash (take not this is only run during build of container image)  
- **COPY**
    - copies external files such as application source code and config files into container image during build
- **ADD**
    - copies external files such as .tar and .zip and extracts into destination directory, can use in place of COPY, but recommended to use only for extraction 
- **ENV**
    - Set environmental variables, can be passed in to the 
- **VOLUME**
    - set persistent volume in directories, usually used for database files 
- **EXPOSE**
    - opens up a port in the container to communicate in the internal container network
    - running docker standalone, causes it to run on localhost
- **CMD**
    - default command executable at container runtime, when container starts, can be overwritten
- **ENTRYPOINT**
    - similar to CMD but non-executable
- **WORKDIR**
    - sets current working directory for all commands to be run. 
- **ONBUILD**
    - commands to execute when building, good for reusing custom container images


**Best Practices**
- Move instructions in a dockerfile down as low as possible, to reduce container image size and reusability of image layers from docker cache
- Combine commands such as multiple RUN commands to reduce image layers
    - Chain RUN apt update -y with RUN apt-get install -y mysql default-jdk with RUN apt-get autoremove
        - RUN apt update -y && apt-get install -y mysql default-jdk && apt-get autoremove
- use CMD["echo","hello","world"] and ENTRYPOINT["echo","hello","world"] instead of CMD echo hello world etc.
    - reduces the number of sh being called
- Combine and chain ENTRYPOINT with CMD, as CMD can be overwritten, it can be used as command line arguments to the ENTRYPOINT. For example
    - ENTRYPOINT["echo"]
    - CMD["hello"]
    - docker run <image>:<tag> bye 
- Always start a Dockerfile in a new folder 
- One container for one process / one responsibility
    - One container each for backend / frontend/ database
     

### Process of creating container applications
- **Dockerfile** > **Container Image** > **Container**
- Usually an application consists of multiple containers
- 3 tier architecture, presentation tier, logic tier and data tier
- results in a container respectively for the frontend, backend and database
- each container communicates with one another in the internal container network
- good practie to only expose the web facing container to the host os / localhost

### Once you have good basics with docker containers
- Container orchestration with docker-compose
- Container services with pods with kubernetes
- PaaS with kubernetes using RedHat OpenShift

### Best practices with Kubernetes / OpenShift
- Pods are scalable, run 1 container per pod
- use multi-container pods only for logging services or splunk agent etc
- Study High Availability and clustering concepts
- Look at canary release and version control of container infrastructure





