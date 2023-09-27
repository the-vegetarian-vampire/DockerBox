# DockerBox
Playing with Docker contrainers.   
From Docker & Kubernetes: The Practical Guide

----

`--help`    
`docker --help`   
`docker run --help`   

`docker build .`

| flag  |  details |   
|---|---|
|`docker run IMAGE_NAME`|Create and start a new container based on image IMAGENAME (oruse the image id)|
|`docker ps` // `docker ps -a`|List all running containers // List all containers - including stopped ones|
| `-d`  |  detach // Run the container in detached mode - i.e. output printed by the container is not visible, the command prompt / terminal does NOT wait for the container to stop | 
| `-it` | for input // Run the container in "interactive" mode - the container / application is then prepared to receive input via the command prompt / terminal. You can stop the container with CTRL + C when using the -it flag |
| `-p`  |   | 
|  `-t NAME:TAG` | Assign a NAME and a TAG to an image  | 

`host.docker.internal` as address   
`docker container inspect`   

To quit: create a `new terminal`, run `docker ps`, grab <containerName>, and run `docker stop <containerName>`

----

Sample C++ image:   
```
# Base image   
FROM gcc:latest   

# Set working directory in container
WORKDIR /app

# Copy C++ source code into container
COPY . /app

# Compile C++ code
RUN g++ your_code.cpp -o your_program

# Command to run application
CMD ["./your_program"]
```
----

## Images
- Images are blueprints / templates for containers. They are read-only and contain the application as well as the necessary application environment (operating system, runtimes, tools)
    - pre built or build own

## Volumes
`volumes` - folder/file inside Docker container which is connected to some folder outside of the container

- Anonymous Volume - for single container `--rm` - can not be shared across volumes; creates folder locally [temporary]    
- Named Volume - not tied to any container, survive container shutdown; can share across multiple containers
- Bind Mount - Know where data is stored on a local machine; survive container shutdown

## Container Communication

----

## Docker Compose File

Docker-compose.yaml   
With docker extension auto-completion 
  - list of configurations here: [Docker Compose](https://docs.docker.com/compose/compose-file/)   

Sample:
```javascript
version: "3.8"
services:
  mongodb:
    image: 'mongo'
    volumes: 
      - data:/data/db
    # environment: 
    #   MONGO_INITDB_ROOT_USERNAME: max
    #   MONGO_INITDB_ROOT_PASSWORD: secret
      # - MONGO_INITDB_ROOT_USERNAME=max
    env_file: 
      - ./env/mongo.env
  backend:
    build: ./backend
    # build:
    #   context: ./backend
    #   dockerfile: Dockerfile
    #   args:
    #     some-arg: 1
    ports:
      - '80:80'
    volumes: 
      - logs:/app/logs
      - ./backend:/app
      - /app/node_modules
    env_file: 
      - ./env/backend.env
    depends_on:
      - mongodb
  frontend:
    build: ./frontend
    ports: 
      - '3000:3000'
    volumes: 
      - ./frontend/src:/app/src
    stdin_open: true
    tty: true
    depends_on: 
      - backend

volumes: 
  data:
  logs:

```


----
# Kubernetes

