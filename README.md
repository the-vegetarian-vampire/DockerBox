# DockerBox
Playing with Docker contrainers.   
From Docker & Kubernetes: The Practical Guide

----

`--help` 

| flag  |   |   
|---|---|
| -d  |  detach | 
| -it | for input |
| -p  |   | 
|  -t |   | 

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
