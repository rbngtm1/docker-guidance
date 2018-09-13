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
    4 docker ps --all : list all containers that we have ever created
#### Container Lifecycle
    1 docker run = docker create + docker start
    2 ex: docker create hello world; you will see some long id
    3 copy that id and run -- docker start [that long id] and then docker start -a [that long id], it gives output from that thing.
    4 docker run by default will show all the logs or all the information out of the container
    5 docker start is not going to show information out of the container
#### Restarting Stopped Containers
    1 you can start the container by docker start CONTAINER_ID and docker start -a CONTAINER_ID
#### Removing Stopped Containers
    1 docker system prune
#### Retrieving Log Outputs
    1 docker logs CONTAINER_ID (Used to inspect a container and really see what's going on inside)
#### Stopping Containers
    1 docker stop CONTAINER_ID or docker kill CONTAINER_ID. You can do docker ps to see CONTAINER_ID.
#### Mulit-Command Containers
    1 Note: Reddis is an inmemory data store which is very commonly used with applications.
    2 ex: docker run redis, you can do docker run redis-cli on second terminal 
    3 the redis-cli will not work unless you add it into a container as a running process
    4 To execute 2nd command inside of a running container, we will do:
      docker : reference to the client
      exec : run another command
      -it : allow us to provide input to the container 
      CONTAINER_ID 
      commannd : command to execute 
    5 docker ps to copy redis containerid and do --docker exec -it CONTAINER_ID redis-cli
    6 keep winpty if you are in bash for windows before docker exec -it CONTAINER_ID redic-cli
    7 now you can write set myvalue 5
    8 get myvalue 
#### Getting a Command Prompt in a Container
    1 you can run command inside of your container without having to rerun docker exec all the time
    2 do docker ps and docker exec -it CONTAINER_ID sh
    3 after that you can change your directory to home directory by cd ~/ or do ls 
      or go to root directory by cd / and do ls to see root files and folders and also play aroud
      export b=5 and then echo $b; you can also do redis-cli; if you cannot get out by control C
      try control D or type exit.
#### Starting with a shell
    1 docker run -it busybox sh
    2 you can now try ls, echo sth, ping google.com, etc. 
#### Container Isolation 
    1 Containers donot share data 
    2 Forex: try docker run -it busybox sh in 2 terminal and do docker ps in 3rd, you will see 2 
      containers but if you create a file by touch hithere in 1st, you won't see that in 2nd.
### Creating a Production-Grade Workflow
#### Flow Specifics 
    1 the development flow process includes development, testion, deployment and its repeatition
    2 Our development workflow is going to revolve around creating a git hub repository, this repository
      can be deployed to outside hosting service
    3 Try github repos for 2 branches; one for feature and another master
    4 you can add code and make changes to update in feature branch; master will represent very clean
      working copy of code base
    5 Any change to master branch will automatically deployed to our hosting provider
    6 You are going to pull down the code base on the feature branch
    7 You will push the changes after you made some changes to the github repository to feature branch
    8 Once you push the changes, you will create a pull request to add the changes to feature branch 
      and merge them to the master branch. 
    9 Let's try to set up a work flow that is automatically going to take our application and push it
      to Travis CI. Travis CI pull down your code and run a test on your code base.
    10 After that, Travis CI will automatically push it to AWS hosting. 
#### Project Generation
    1 try node -v on your terminal, if you don't have it install
    2 do npm install -g create-react-app on your terminal 
    3 try create-react-app frontend
    4 go inside frontend folder by cd frontend
#### Necessary Commands
    1 npm run start: starts up a development server. For development use only
    2 npm test run: runs test associated with the project
    3 npm run build: Builds a production version of the application 
    4 in frontend folder; try npm run test and then npm run build 
    5 After that when you ls; you notice build folder is created
    6 cd build/static/js and try ls; you will see 2 file starting with main.
    7 do npm run start; you will be directed towards the localhost 3000
#### Create a Development Docker file
    1 on frontend folder; do code . to open visual studio code
    Inside Docker file: FROM node:alpine
                        WORKDIR '/app'
                        COPY package.json .
                        RUN npm install
                        COPY . .
                        CMD ["npm", "run", "start"]
    2 To load up the docker file and create the image; docker build -f Dockerfile.dev .
    3 You will notice that when we just installed the create-react-app tool and used it to generate 
      a new project. That tool automatically installed all of our dependencies into our project. 
    4 You have 2 copies of dependencies, you can delete node_modules folder
    5 After you fix the duplicate dependencies, your docker build -f Dockerfile.dev . will work much faster
#### Starting the Container

    
    
