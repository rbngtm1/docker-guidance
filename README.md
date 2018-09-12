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
      * Control Group is used to limit the amount of resource used per process.
      * For instance: Namespacing is for saying this area of harddrive is for certain process. Control group can be used to limit the amout of "memory, CPU Usage, HD I/O, Network Bandwith" that the process can use
#### After installing, run docker version to see if it's installed correctly
### Using Docker Client (CLI)
  * Docker client communicates with docker server
  * If you run comman with docker run _____ from files within your docker hub like (hello-world, redis, busybox, etc.), The docker server will look into "Image cache". If the docker "image cache" inside your personal computer is empty, docker server will reach out to docker hub. 
  * docker hub is the repository of free public images that you can freely download and run on your personal computer. 
  * Docker server will take the file from docker hub, load it into memory, creates a container out of it, and runs a single program inside of it. 
