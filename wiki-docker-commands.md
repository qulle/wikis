# Docker commands
A living document with useful docker commands, not intended as a complete docker reference. 

## Note
This used to be a private repo but i changed it to be public because of ease of access for me. Use it as a reference if you like it but `i am not accountable for what happens when you execute commands in your environment`. Use with causion and Google commands that you don't know.

## 0. What is docker?
*Docker is containerization platform, meaning that it enables you to package your applications into images and run them as containers on any platform that can run Docker*

### Basic flow
Dockerfile --> `$ docker build` --> Docker Image --> `$ docker run` --> Docker Container

## 1. Dockerfile
*Instructions that form a recipe for how to create a image.*

### Basic example
```dockerfile
FROM ubuntu:latest
CMD ["echo", "Dockerfile test"]
```

### Embedding local application into image
```dockerfile
FROM scratch                   # Scratch is a pre existing image with the bare minimum to create from.
COPY ./some-application /      # Copy from current directory into root.
CMD ["/some-application"]      # Run the application when the container is run
```

### More complex example, building .net core project and store in image.
```dockerfile
FROM mcr.microsoft.com/dotnet/sdk:5.0 AS build-env
WORKDIR /app

COPY *.csproj ./
RUN dotnet restore
 
COPY . ./
RUN dotnet publish -c Release -o out
 
FROM mcr.microsoft.com/dotnet/aspnet:5.0
WORKDIR /app
EXPOSE 80
COPY --from=build-env /app/out .
ENTRYPOINT ["dotnet", "WebStore.dll"]
```

### Build Dockerfile to image with tagging
Naming convention `<Docker Hub ID>/Project Name>:<Tag Version>`
```
$ docker build .                         # Build image anonymous
$ docker build . -t <image-name:tag>     # Build image using name and tag
```

Use `.dockerignore` to exclude files and directories from the build process. 

## 2. Image
*Stack of one or many existing images that together form a new configured image.*

### List available images
```
$ docker images
```

### Get image (from hub.docker.com)
```
$ docker pull centos           # If no tag :latest will be used
$ docker pull ubuntu:18.04     # Specific version
```

### Publish image (at hub.docker.com)
 ```
$ docker push <IMAGE-NAME>
```

### Delete image
```
$ docker rmi <image-id>     # Delete single image
$ docker image prune        # Delete dangling images
$ docker image prune -a     # Delete all unused images
```

### Save and load image (.tar)
```
$ docker save <image-id> > <file.tar>     # Save image 
$ docker load -i <file.tar>               # Load image
```

## 3. Container
*A container is an instance of an image.*

### List available containers
```
$ docker ps        # list running containers
$ docker ps -a     # list all containers
```

### Get information about containers
```
$ docker status                       # Get info about running containers
$ docker inspect <container-name>     # Get info about one container as JSON
$ docker logs <container-name>        # Get logs about container
$ docker port <container-id>          # Show mapped ports of a container
$ docker diff <container-id>          # Show all modified files in a container
$ docker top <container-id>           # Show all running processes of a container
```

### Run container
```
$ docker run <image-name:tag>                                 # Basic usage
$ docker run --name <container-name> <image-name:tag>         # Specify name
$ docker run -d <image-name:tag>                              # Run container in detached mode (background mode not ockupying shell)
$ docker run -it <image-name:tag>                             # Run container in interactive mode (-i = input, -t = echo output)
$ docker run -p 8080:80 <image-name:tag>                      # Mapping local port 8080 to remote container port 80
$ docker run -P <image-name:tag>                              # Mapping all ports
$ docker run --hostname <hostname:ip> <image-name:tag>        # Assign hostname to container
$ docker run -v <host-dir:container-dir> <image-name:tag>     # Map local directory into container directory
$ docker run --rm <image-name:tag>                            # Remove container when stopped
```

### Execute command in the container
```
$ docker exec -it <container-name> npm -v        # Displays the npm version
$ docker exec -it <container-name> /bin/bash     # Enter shell of container
```

### Copy files to/from container
```
$ docker cp <container:source> <host-target>     # Copy from container to host
$ docker cp <host-target> <container:source>     # Copy from host to container
```

### Create new image from running container
```
$ apt-get update                                              # Update to enable installation of programs
$ apt-get install npm                                         # Install npm through the shell of a running container
$ docker commit <container-name> <new-image-name>             # Create image that will have npm installed
```

### Basic container manipulations
```
$ docker start <container-name>                               # Start container
$ docker stop <container-name>                                # Stop container
$ docker restart <container-name>                             # Restart container
$ docker rename <old-container-name> <new-container-name>     # Rename container
$ docker rm <container-name>                                  # Delete container
$ docker rm <container-name> --force                          # Delete running container
$ docker container prune                                      # Delete stopped containers
```

## 4. Troubleshooting
- If a container is started/run and immediately stops, try running in detached mode (not using the -d flag) to get output in the terminal.
