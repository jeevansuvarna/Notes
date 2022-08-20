# Docker

Docker is a platform for developers to develop, ship and run applications

## Image

An image is an ordered collection of a root file system changes and the corresponding execution parameters
for use within container runtime.

## Container
A container is a runtime instance of a docker.

## Dockerfile
``` docker
FROM node:15 
WORKDIR /app 
COPY package.json . 
COPY npm install
COPY . ./
CMD ["node","index.js"]
```

## Interactive Mode command
```
exec -it [node-app] base 
```

## Command to build image

```docker
docker build -t node-app-image .
```

## To list all images

```docker
docker image ls
```

## To remove image
```
docker image rm ID
```

## Run the container

```docker
docker run -d --name node-app node-app-image
```

```docker
docker run -d -p 3000:3000 --name node-app node-app-image
```                

## Syncing Source code with bind mount

### Mac

```docker
docker run -v$(pwd)/app:ro -p 3000:3000 -d --name node-app node-app-image
```

### Windows
```docker
docker run -v%cd%/app:ro -p 3000:3000 -d --name node-app node-app-image
```

### Linux
```docker
docker run -v${pwd}/app:ro -p 3000:3000 -d --name node-app node-app-image
```

## Logger
``` docker
log node-app
```

# Docker Compose  
  Used to create one or more images.

FileName: docker-compose.yml

```docker
version: "3"
services:
  node-app:
    build: .
    ports:
      - "3000:3000"
    volumes:
      - ./:/app
      - app/node_modules
    environment:
      - PORT=3000
```

### Run Docker Compose - [build and runs Container]

```docker
docker-compose up -d --build
```

### Stop Docker Compose

```docker
docker-compose down -v
```

# Create Mulitple Image using Docker Compose

```docker
version: "3"
services:
  node-app:
    build: .
    ports:
      - "3000:3000"
    volumes:
      - ./:/app
      - app/node_modules
    environment:
      - PORT=3000
  mongo:
    image:mongo
    environment:
        - MONGO_USERNAME = xyx
        - MONGO_PASSWORD = xyz
```
