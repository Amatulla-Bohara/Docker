# Docker


# Table of Contents
- [What and why ](#what-and-why)
- [Window and Mac](#window-and-mac)
- [Using Docker Client](#using-docker-client)
- [Container on Computer](#container-on-computer)
- [Docker on Computer](#docker-on-computer)
- [Docker run command](#docker-run-command)
- [Overriding the commands](#overriding-the-commands)
- [Listing running containers](#listing-running-containers)
- [Container Lifestyle](#container-lifestyle)
- [Restarting Stopped containers](#restarting-stopped-containers) 
- [Remove stopped containers](#remove-stopped-containers)
- [Retrieving logs output](#retrieving-logs-output)
- [Stopping container](#stopping-container)
- [Docker pull and push] (#docker-pull-and-push)



# What and why
### Why is Docker

While downloading any software we come across many errors and to execute this task without any errors.
To install the redis software we need to check the dependencies on the system but with docker it can be installwithin seconds.

command without docker => cmd from its official documentation
command using docker => docker run it redis

"It makes really easier to install and run software without worrying about setup or dependencies"

### What is docker

Docker is a platform or ecosystem around creating and running containers.
Docker Ecosystem consists of =>
Docker Client
Docker Server
Docker Machine
Docker Images
Docker Hub
Docker compose

IMAGE- single file with all the deps and config required to run a program
//Docker CLI reaches to dockerHub to download the image(redis)
CONTAINER- Instances of image.runs a program.
//It has its own isolated set of hardware, memory, networking technology, hardDrive space.


# Window and Mac

The package contains
docker client (Docker CLI)
Tool that we are going to issue commands to
docker server(Docker Daemon)
tool that is responsible for creating images, running containers etc.

you and I are interacting with CLI and in the nutshell Docker CLI is interacting with Docker server which is't visible to us as it is happening behind the scenes.

### INSTALLATION FOR LINUX

Ubuntu installation - https://docs.docker.com/engine/install/ubuntu/

Installing Docker on Linux
These steps listed below are for Ubuntu Desktop LTS. You can find the full official docs and steps for other Linux distributions here:

Ubuntu: https://docs.docker.com/install/linux/docker-ce/ubuntu/

CentOS: https://docs.docker.com/install/linux/docker-ce/centos/
(Note: Students have encountered issues when using CentOS or RHEL as the host related to Docker container communication. You may need to research some workaround for the errors you run into or search the QA for already posted solutions)

Debian: https://docs.docker.com/install/linux/docker-ce/debian/

1. Installation Steps
   Create Dockerhub account
   https://hub.docker.com/signup

2. Install Docker
   The Docker docs suggest setting up a Docker repository to install and update from.
   This is where you should start: https://docs.docker.com/engine/install/ubuntu/#install-using-the-repository

3. Login to the Dockerhub
   In order to push and pull images, you will need to login to the Dockerhub. In your terminal, run docker login and then enter your Dockerhub account's username and password.

4. Test Docker installation
   After completing the installation steps, test out Docker by running sudo docker run hello-world. This should download and run the test container printing "hello world" to your console.

5. Installing Docker Compose
   Navigate to the installation page:
   https://docs.docker.com/compose/install/#install-compose-as-standalone-binary-on-linux-systems
   Click the Linux Standalone Binary Tab:

Then, CTL+F to search for the Install Compose as standalone binary on Linux systems section on the page. Follow the instructions provided there to install the latest Docker Compose binary.

6. Testing Docker Compose
   After completing, test your installation by running docker-compose -v. This should print the version and build numbers to your console.

7. Run without Sudo
   Follow these instructions to run Docker commands without sudo:
   https://docs.docker.com/install/linux/linux-postinstall/#manage-docker-as-a-non-root-user

8. Start on Boot
   Follow these instructions so that Docker and its services start automatically on boot:
   https://docs.docker.com/install/linux/linux-postinstall/#configure-docker-to-start-on-boot

You may need to restart your system before starting the course material.


# Using Docker Client

 when we run the command "docker run hello-world" then some process occours at the backend and we get Hello from Docker! text displayed on our screen.

## How this happens?

 when we run the command "docker run hello-world" through CLI, that is, we are using Docker Client. Docker Client takes our command to Docker Server, this server checks the required image in image-cache. If it finds the image in image-cache, then it is easier and faster for the server to full-fill the demand of the client.
 //now there won't be any message "image not found"

## But what if the image is not found in the image cache?

Docker server goes to the Docker Hub and there it finds the required image this server then giver the output through docker client. 

//"purpose of the hello-world image is just to write the output - Hello from docker!"

Docker Hub is the free service where many images are available


                                   YOUR COMPUTER
                                 ____ \  
                                |     /  Docker Client                     DOCKER HUB
  COMMAND                       |              |                        _____________________
docker run hello-world-----------              |           -------------|-Hello-world       |
                                              \ /          |            | redis             |
                                        Docker Server-----------------> |         etc.      |
                                              |  or        |            |                   |
                                              |            |            |                   |
                                             \ /           |            |                   |
                                          Image Cache      |            |                   |
                                        |--------------|   |            |___________________|
                                        |Hello-world<--|----
                                        |              |
                                        |              |
                                        |--------------|



# Container on Computer


## What is Container and how it is created on your machine?

Before that lets have a look upon:-

## How your operating system runs on your computer?

Most operating system has something called kernel. 

kernel is a running software process that governs access between whatever programs are running on your computer and all the physical hardware that is connected to your computer as well!!

software processes running on your computer such as chrome, terminal, spotify, NodeJs. If you have previously worked with NodeJs then you might know that it is nodeJs which is directly connecting with computers hardware but it is KERNEL through which interacts with. software connects with the kernel through SYSTEM CALL.

SYSTEM CALL - Running program issues requests to kernel to interact with a piece of hardware.
## Hypothetical scenario

### what if we have process(software) running which has python v2 installed and nodeJs V3 installed and the hardware has access to python V2 then what happens?

Only chrome would function well as harddisk has python v2.

### we can solve this issue with the help of feature of operating system called NAMESPACING.

### In NAMESPACING we can have partitioning of the hardDisk. Isolating resources per process (or group of process)
### => Processes, Hard Drive, Network, Users, Hostnames, Inter process communication.
Here we can have partitioning for python v2 as well as python v3.

any of them from chrome or nodeJs wana access to harddisk through kernel via system call. In kernel it will get clear which process is making this system call(chrome/nodeJs) and according to this it gets hardware access. 

### CONTROL GROUPS (cgroups)
### Memory, CPU usage, HD input/output, network bandwidth

Limited amount of resources used per process


### CONTAINER 

chrome            -> system call -> kernal          -> hard disk 
(software process)                (decision making)   (python v2)

### container dosen't mean a physical system that exists inside a computer but it is a set of process of grouping a resources assigne to it. 
      Note - only portion of HARDWARE (RAM, CPU) is made availabe to the software process.

### IMAGE have "FS snapshots" and "startup commands"

FS snapshots - chrome, python
startup commands - >run chrome

## summary

when the container is created little part from the hardware is assigned and from image it has chrome and python. 
Through running a command we can start the process.


![Docker5](https://user-images.githubusercontent.com/85250069/186265660-3ec32c13-6cd2-4f9f-86d3-60b544ebfde3.PNG)


# Docker on Computer


## How Docker run on your computer?

NAMESPACE and CONTROL GROUPS are linux command. 

So you might be thinking how can linux commands run on windows. 
The answer is when we install Docker we actully install Linx virtual machine and all the containers share same linux kernel.

## output of docker version

In server section it has os specified which is linux os which the counter uses. 

![Docker6](https://user-images.githubusercontent.com/85250069/186267208-ed2b2380-a762-46af-83e8-33a5f8321607.PNG)


# Docker run command

## docker run command in detail

 somewhere in our system there is image or else we load it from docker hub. This image containes FS snapshots and Startup Commands. Container has some space where FS snapshots can be fit into hard drive segment for the process. Some resources are assigined to this container and then the startup command is run that is "run hello-world".
 
 ![Docker7](https://user-images.githubusercontent.com/85250069/186487594-23cd8d76-a659-4dd0-ac82-8dba63333b4a.PNG)

![Docker8](https://user-images.githubusercontent.com/85250069/186487639-3ce97e86-bbd4-4ec3-9826-411808d07ae3.PNG)


# Overriding the commands

## overriding docker run command 

docker echo hello there!! command will print out hello there!! 

Let's use docker run busybox ls it will display all the contents in busybox.

If we use busybox with echo then there is somewhere echo/ls present in the SF Snapshot. But in hello-world echo/ls doesn't work as there is no specification of echo/ls has been done in SF Snapshot of hello-world.

# Listing running containers


## Listing running Containers

To list all the containers up in the working state we use "docker ps".

here docker refers to the docker client and ps lists all the running containers.

"docker ps --all" lists all the conatiners created till now.

Now, lets take "docker run busybox echo hi there" it prints "hi there" but we cannot see its name in the running container list. Because it echo's out the written text and goes back into down state.

Now, lets try to use ping command in other terminal and execute the ps command in 1st terminal. So the command is "docker run busybox ping google.com". Now if we run ping command we get the output for ps command.

Note - use ctrl+c command to stop the requests of ping command.



# Container Lifestyle

creating and running a conatiner are two different tasks. 

docker run = docker create + docker start

create a container = "docker"(reference the docker client) "create"(try to create the container) "image name"(name of the image to use for this container)

start a container = "docker"(reference the docker client) "start"(try to create the container) "container id" ID the container to start

## what happens when the conatiner is only created and not started?

FS Snapshot from Image comes to the container and gets add in the hard drive segment for this process.

## what happens when the container is actually started?

Startup command is run on the container to actually start the container. example - "echo hi there!!".

##### docker create hello-world 
It gives the conatiner id as the output.

##### docker start -a "continer-id"
There will be welcome message printed from docker. "-a" is used to give whatever output is given by the conatiner. 

Note - without "-a" it will not give the container output but it just returns container ID if we use the command - "docker start container-id"


# Restarting Stopped containers

## Restarting stopped container

If we run a command "docker run busybox echo hi there!!" then the output will be "hi there!!" as soon as it gets executed the container gets stopped and its status becomes "Exited(0)".

To start the container or to start it again we use "docker start container-id" and this will return the container-id but if we use "-a" i.e. "docker start -a container-id" then it will return whatever there is value inside the container like in this case it is "hi there!!" and this statement cannot be modified.

# Remove stopped containers

## Removing stopped containers

"docker system prune" used to remove :

- all stopped containers
- all networks not used by at least one containers
- all dangling image
- all build cache

it will also give total reclaimed space after running this command.

now as you execute "docker ps --all" there is no container available which has been stopped.

### As and when you are done working with docker run this command in order to free up all the containers.

# Retrieving logs output


## Retrieving log outputs

### Get logs from a container using

#### docker logs container-id

if we use "docker start -a container-id" then it will give the output of the container but instead of it we can use "docker logs container-id" inorder to get the logs of the container in this case if we use "docker create busybox echo hi there" then the container-id is created these container returns container-id but if we use "docker logs container-id" it will return "hi there!!".



# Stopping container


## Stopping containers

There are two commands used to stop the container :

## 1. stop

It gives termination signal i.e. SIGTERM to the container and waits for 10sec. to complete its processes and then response back.

### docker stop container-id

## 2. Kill

It gives kill signal i.e. SIGKILL to the container and kills all the processes at that instant of time and responce back qwikly.

### docker kill container-id


example - 
docker run busybox ping google.com
docker ps //to get container-id
docker stop container-id //will take 10 sec. and return container-id
docker start container-id
docker kill container-id //instant reply by giving container-id



# Docker pull and push


