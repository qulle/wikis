# Docker commands
A living document with useful docker commands, not intended as a complete docker reference. 

## Note
This use to be a private repo but i changed it to be public because of ease of access for me. Use it as a reference if you like it but `i am not accountable for what happens when you execute commands in you environment`, use with causion and Google commands that you don't know.

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
$ docker build . -t <IMAGE-NAME:TAG>     # Build image using name and tag
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
$ docker rmi <IMAGE-ID>     # Delete single image
$ docker image prune        # Delete dangling images
$ docker image prune -a     # Delete all unused images
```

### Save and load image (.tar)
```
$ docker save <IMAGE-ID> > <FILE.TAR>     # Save image 
$ docker load -i <FILE.TAR>               # Load image
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
$ docker inspect <CONTAINER-NAME>     # Get info about one container as JSON
$ docker logs <CONTAINER-NAME>        # Get logs about container
$ docker port <CONTAINER-ID>          # Show mapped ports of a container
$ docker diff <CONTAINER-ID>          # Show all modified files in a container
$ docker top <CONTAINER-ID>           # Show all running processes of a container
```

### Run container
```
$ docker run <IMAGE-NAME:TAG>                                 # Basic usage
$ docker run --name <CONTAINER-NAME> <IMAGE-NAME:TAG>         # Specify name
$ docker run -d <IMAGE-NAME:TAG>                              # Run container in detached mode (background mode not ockupying shell)
$ docker run -it <IMAGE-NAME:TAG>                             # Run container in interactive mode (-i = input, -t = echo output)
$ docker run -p 8080:80 <IMAGE-NAME:TAG>                      # Mapping local port 8080 to remote container port 80
$ docker run -P <IMAGE-NAME:TAG>                              # Mapping all ports
$ docker run --hostname <HOSTNAME:IP> <IMAGE-NAME:TAG>        # Assign hostname to container
$ docker run -v <HOST-DIR:CONTAINER-DIR> <IMAGE-NAME:TAG>     # Map local directory into container directory
$ docker run --rm <IMAGE-NAME:TAG>                            # Remove container when stopped
```

### Execute command in the container
```
$ docker exec -it <CONTAINER-NAME> npm -v        # Displays the npm version
$ docker exec -it <CONTAINER-NAME> /bin/bash     # Enter shell of container
```

### Copy files to/from container
```
$ docker cp <CONTAINER:SOURCE> <HOST-TARGET>     # Copy from container to host
$ docker cp <HOST-TARGET> <CONTAINER:SOURCE>     # Copy from host to container
```

### Create new image from running container
```
$ apt-get update                                              # Update to enable installation of programs
$ apt-get install npm                                         # Install npm through the shell of a running container
$ docker commit <CONTAINER-NAME> <NEW-IMAGE-NAME>             # Create image that will have npm installed
```

### Basic container manipulations
```
$ docker start <CONTAINER-NAME>                               # Start container
$ docker stop <CONTAINER-NAME>                                # Stop container
$ docker restart <CONTAINER-NAME>                             # Restart container
$ docker rename <OLD-CONTAINER-NAME> <NEW-CONTAINER-NAME>     # Rename container
$ docker rm <CONTAINER-NAME>                                  # Delete container
$ docker rm <CONTAINER-NAME> --force                          # Delete running container
$ docker container prune                                      # Delete stopped containers
```

## 4. Troubleshooting
- If a container is started/run and immediately stops, try running in detached mode (not using the -d flag) to get output in the terminal.
