# docker-basics
### Why use Docker
  * Docker makes it really easy to install and run software without worrying about setup or dependencies
### What is Docker
  * Docker is a platform or ecosystem around creating and running containers
### What is Container
  * Container is a hardware program with its own isolated set of hardware resourses.
  * container is an instance of an image. It's sole purpose is to run one single program.
#### After installing, run docker version to see if it's installed correctly
### Using Docker Client (CLI)
  * Docker client communicates with docker server
  * If you run comman with docker run _____ from files within your docker hub like (hello-world, redis, busybox, etc.), The docker server will look into "Image cache". If the docker "image cache" inside your personal computer is empty, docker server will reach out to docker hub. 
  * docker hub is the repository of free public images that you can freely download and run on your personal computer. 
  * Docker server will take the file from docker hub, load it into memory, creates a container out of it, and runs a single program inside of it. 
