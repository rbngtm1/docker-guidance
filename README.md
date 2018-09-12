# docker-basics
### Why use Docker
  * Docker makes it really easy to install and run software without worrying about setup or dependencies
### What is Docker
  * Docker is a platform or ecosystem around creating and running containers
### What is Container
  * Container is a hardware program with its own isolated set of hardware resourses.
  * container is an instance of an image. It's sole purpose is to run one single program.
  * Image is a single file with all the config required to run a program. 
  * To understand a container, you must of a little bit of background on how the operating system runs on your computer. 
    * Most operating system have Kernel. Kernel is running software process that governs access between all the programs that are running on your computer and all the physical hardware that is connected to your computer as well. 
    * Running program on your computer issues request to kernel to interact with a piece of hardware like CPU, Memory and Hard Drive. 
    * The hardware can be segmented by using namespacing; kernel will help to figure out the request and direct that call to desired segment in hardware.
      * Namespacing is not only used for segmenting hardware, it can be used for software elements as well. Forex: we can namespace a process to restrict the area of harddrive, network, interprocess communication and users.
      * Control Group is used to limit the amount of resource used per process. Note; Namespacing and control group belong to linux, not to windows not to MacOS. 
      * For instance: Namespacing is for saying this area of harddrive is for certain process. Control group can be used to limit the amout of "memory, CPU Usage, HD I/O, Network Bandwith" that the process can use
   * The entire running process plus the segment of the resource that it can talk to is what we refer to as a container. 
   * Container simply is a process or the group of processes that have grouping of resources specifically assigned to it.
   * **How does image create a container**
     * If we have image that contains file snapshot and startup command, the file snapshot is taken in the hard drive. In this case, if startup command is executed, the new instance of the process is created as running process and that created process is isolated to set of resouces in the file snapshot stored in hard drive. This is how images is taken into as run container. 
#### After installing, run docker version to see if it's installed correctly
### Using Docker Client (CLI)
  * Docker client communicates with docker server
  * If you run comman with docker run _____ from files within your docker hub like (hello-world, redis, busybox, etc.), The docker server will look into "Image cache". If the docker "image cache" inside your personal computer is empty, docker server will reach out to docker hub. 
  * docker hub is the repository of free public images that you can freely download and run on your personal computer. 
  * Docker server will take the file from docker hub, load it into memory, creates a container out of it, and runs a single program inside of it. 
#### How Docker is running on your computer?
  * When you installed docker for windows or docker for Mac, you installed a linux virtual machine. So, as long as the docker is running, you technically have linux virtual machine is running on your computer. Inside of this virtual machine is where all those containers are going to be created. Inside the virtual machine, we have linux kernel which is going to be hosting running process inside a container. It's Linux Kernel that's going to be incharge of isolating access to different hardware resources on your computer. You can see that you have different virtual machine running by typing "docker version" on terminal. 
### Manipulating Containers with the Docker Client 
#### Docker run in detail
    1 docker is reference to docker client
    2 run try to create and run a container
    3 image name : is name of image to use for this container. 
#### Overriding Default commands
    1 ex: In docker run busybox echo hi there; you will see hi there printed on your terminal.
    2 Whatever default command is included inside of the image is not going to be executed.
    3 ex: docker run busybox ls and docker run busybox echo hi there works fine but docker run hello-world doesn't even though it is part of docker hub because ls and echo executable are somewhere inside the folder of busybox
#### Listing Running Containers
    1 ps: list all the running containers
    2 docker ps: you will see headers for the table and entries for running container inside the table
    3 If you do-- docker run busybox ping google.com, and open another terminal to see docker ps; you will see running container
