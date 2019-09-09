#### tagging a container
  * docker build -t robingautam/redis:latest
  * docker run robingautam/redis
#### Alternative for using Dockerfile (example)
  * docker run -it alpine sh
  * apk add --update redis
  * In another terminal, docker ps {copy the container id}
  * docker commit -c 'CMD["redis-server"]' 862d3c373c6e 
  * Doing this will create a custom redis image out of base image of apline
  * If you want to access the redis image directly from docker hub, you may do--> docker run redis
#### COPY 
  * COPY ./ ./ {Path to folder from your machine && place to copy stuff to inside the container}
#### tagging a container
  * If we build a custom image by modifying a base image, we will use docke build . after making changes in Docker file
  * Then we will run our image using docker run <container id> created by docker build .
  * But there is a alternate to that, you can create a tag by something like this:
  * docker build -t robingautam/simpleweb .  {Here simpleweb is the working directory}{you don't need to specify :latest because by default it takes latest}
  * Then we can run our image by docker run robingautam/simpleweb
#### add stdin for the image build by docker file
  * docker exec -it eefkkdk234 sh
#### Steps
  * docker build -t robingautam/simpleweb .
  * docker run -p 8080:8080 robingautam/simpleweb
  * In another terminal, docker ps , and docker exec -it <container-id> sh
#### Installing docker compose
  * sudo curl -L "https://github.com/docker/compose/releases/download/1.24.1/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
  * sudo chmod +x /usr/local/bin/docker-compose
#### stopping containers
  * docker run -d <container-id> or docker-compose up -d
  * docker-compose down (to stop containers) or docker stop(container-id)
#### Docker compose
  * docker-compose up
  * if you make changes inside docker-compose.yml then, docker-compose up --build
#### Build giving a custom name for docker file
  * docker build -f {dockerfile.dev} .
#### Docker volumes
  * Setting up the mapping between files or folder inside a docker container to files or foler in local folder
  * docker run -p 3000:3000 -v /app/node_modules <here this is just a placeholder for folder inside a container> -v $(pwd):/app <image-id>
