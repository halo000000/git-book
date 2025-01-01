# do

## Docker Image

### 1.List all local images:

```docker
docker -t build image_name path_to_dockerfile
# Example
docker -t build myapp .

```

### 2. List all local images:

```docker
docker images
# Example
docker ls

```

### 3. Pull an image from Docker Hub:

```
docker pull image_name:tag
# Example
docker pull ubuntu:latest

```

### 4. Remove an image:

```
docker rmi image_name:tag
# Example
docker rmi ubuntu:latest

```

### 5.Tag an image:

```docker
docker tag image_name:tag image_name:tag
# Example
docker tag myapp:latest myapp:v1

```

### 6. Push an image to Docker Hub:

```docker
docker push image_name:tag
# Example
docker push myapp:v1

```

### 7. Inspect details of an image:

```docker
docker inspect image_name:tag
# Example
docker inspect myapp:v1

```

### 8. Save an image to a tar archive:

```docker
docker -o save image_name.tar image_name:tag
# Example
docker -o save myapp.tar myapp:v1

```

### 9. Load an image from a tar archive:

```docker
docker -i load image_name.tar
# Example
docker -i load image_name.tar

```

### 10. Prune unused images:

```docker
docker prune
# Example
docker system prune

```

## Docker Container

### 1. Build an image from a Dockerfile:

```docker
docker -t build image_name path_to_dockerfile
# Example
docker -t build myapp .

```

### 1. Run a container from an image:

```docker
docker run image_name:tag
# Example
docker run myapp:v1

```

### 2. Run a named container from an image:

```docker
docker --name run container_name image_name:tag
# Example
docker --name run my_container myapp:v1

```

### 3. List all running containers:

```docker
docker ps

```

### 4. List all containers (including stopped ones):

```docker
docker ps -a

```

### 5. Stop a running container:

```docker
docker stop container_name_or_id
# Example
docker stop my_container

```

### 6. Start a stopped container:

```docker
docker start container_name_or_id
# Example
docker start my_container

```

### 7. Run container in interactive mode:

```docker
docker -it run container_name_or_id
# Example
docker -it run my_container

```

### 8. Run container in interactive shell mode

```docker
docker -it run container_name_or_id sh
# Example
docker -it run my_container sh

```

### 9. Remove a stopped container:

```docker
docker rm container_name_or_id
# Example
docker rm my_container

```

### 10. Remove a running container (forcefully):

```docker
docker -f rm container_name_or_id
# Example
docker -f rm my_container

```

### 11. Inspect details of a container:

```docker
docker inspect container_name_or_id
# Example
docker inspect my_container

```

### 12.View container logs:

```docker
docker logs container_name_or_id
# Example
docker logs my_container

```

### 13. Pause a running container:

```docker
docker pause container_name_or_id
# Example
docker pause my_container

```

### 14. Unpause a paused container:

```docker
docker unpause container_name_or_id
# Example
docker unpause my_container

```

## Docker Volume

### 1. Create a named volume:

```docker
docker volume create volume_name
# Example
docker volume create my_volume

```

### 2. List all volumes:

```docker
docker volume ls
# Example
docker volume ls

```

### 3. Inspect details of a volume:

```docker
docker volume inspect volume_name
# Example
docker volume inspect my_volume

```

### 4. Remove a volume:

```docker
docker volume rm volume_name
# Example
docker volume rm my_volume

```

### 5. Run a container with a volume (mount):

```docker
docker --name -v run container_name volume_name:/path/in/container image_name:tag
# Example
docker --name -v run my_container my_volume:/app/data myapp:v1
```

### 6. Copy files between a container and a volume:

```docker
docker cp local_file_or_directory container_name:/path/in/
container
# Example
docker cp data.txt my_container:/app/data
```

## Network (Port Mapping):

### 1. Run a container with port mapping:

```docker
docker run --name container_name -p host_port:container_port image_name:tag
# Example
docker run --name my_container -p 8080:80 myapp:v1

```

### 2. List all networks:

```docker
docker network ls
# Example
docker network ls

```

### 3. Inspect details of a network:

```docker
docker network inspect network_name
# Example
docker network inspect my_network

```

### 4. Create a user-defined bridge network:

```docker
docker network create network_name
# Example
docker network create my_network

```

### 5. Connect a container to a network:

```docker
docker network connect network_name container_name
# Example
docker network connect my_network my_container

```

### 6. Disconnect a container from a network:

```docker
docker network disconnect network_name container_name
# Example
docker network disconnect my_network my_container

```

## Docker Compose

### 1. Create and start containers defined in a docker- compose.yml file:

```
docker compose up
# Example
docker compose up

```

This command reads the docker-compose.yml file and starts the defined services in the background.

### 2. Stop and remove containers defined in a docker-compose.yml file:

```
docker compose down
```

This command stops & removes the containers, networks, and volumes defined in the docker-compose.yml file.

### 3. Build or rebuild services:

```
docker compose build
```

This command builds or rebuilds the Docker images for the services defined in the docker compose.yml file.

### 4. List containers for a specific Docker Compose project:

```
docker compose ps
# Example
docker compose ps

```

This command lists the containers for the services defined in the docker-compose.yml file.

### 5. View logs for services:

```
docker compose logs
# Example
docker compose logs

```

This command displays the logs for the services defined in the docker-compose.yml file.

### 6. Scale services to a specific number of containers:

```
docker compose up -d --scale service_name=number_of_containers
# Example
docker up -d --scale compose web=3
```

This command scales the number of containers for the specified service to the specified number.

### 7. Run a one-time command in a service:

```docker
docker compose run service_name command
# Example
docker compose run web echo "Hello World"
docker compose run web npm compose install

```

This command runs a one-time command in the specified service.

## Latest Docker

### 1. Initialize Docker inside an application

```docker
docker compose init
# Example
docker compose init

```

### 2. Watch the service/container of an application

```docker
docker compose watch 

```

It watches build context for service and rebuild/refresh containers when files are updated

## Dockerfile Reference

| **Command**    | **Syntax**                                      | **Description**                                                          |
| -------------- | ----------------------------------------------- | ------------------------------------------------------------------------ |
| **FROM**       | `FROM image_name:tag`                           | Specifies the base image for the Docker image.                           |
| **WORKDIR**    | `WORKDIR /path/to/directory`                    | Sets the working directory for subsequent instructions.                  |
| **COPY**       | `COPY source destination`                       | Copies files or directories from the build context to the container.     |
| **ADD**        | `ADD source destination`                        | Similar to `COPY`, but can also extract tar archives.                    |
| **RUN**        | `RUN command`                                   | Executes shell commands to install software or configure the image.      |
| **ENV**        | `ENV KEY=VALUE`                                 | Sets environment variables in the image.                                 |
| **ARG**        | `ARG VARIABLE_NAME=default_value`               | Defines variables that users can pass at build time.                     |
| **LABEL**      | `LABEL key="value"`                             | Adds metadata to an image in key-value pairs.                            |
| **USER**       | `USER username_or_uid`                          | Specifies the user or UID for running the image.                         |
| **EXPOSE**     | `EXPOSE port`                                   | Informs Docker that the container listens on a specific port at runtime. |
| **VOLUME**     | `VOLUME /path/to/volume`                        | Creates a mount point for external volumes or other containers.          |
| **CMD**        | `CMD ["executable", "param1", "param2"]`        | Provides default commands or parameters for the container at runtime.    |
| **ENTRYPOINT** | `ENTRYPOINT ["executable", "param1", "param2"]` | Configures the container to run as an executable.                        |

#### **Example Dockerfile**

```dockerfile
FROM node:20-alpine
WORKDIR /app
COPY package*.json ./
RUN npm install
COPY . .
EXPOSE 8080
ENV NODE_ENV=production
CMD ["node", "app.js"]
```

<figure><img src=".gitbook/assets/image.png" alt=""><figcaption></figcaption></figure>

```docker
# set the base image to create the image for react app
FROM node:20-alpine

# create a user with permissions to run the app
# -S -> create a system user
# -G -> add the user to a group
# This is done to avoid running the app as root
# If the app is run as root, any vulnerability in the app can be exploited to gain access to the host system
# It's a good practice to run the app as a non-root user
RUN addgroup app && adduser -S -G app app

# set the user to run the app
USER app

# set the working directory to /app
WORKDIR /app

# copy package.json and package-lock.json to the working directory
# This is done before copying the rest of the files to take advantage of Docker’s cache
# If the package.json and package-lock.json files haven’t changed, Docker will use the cached dependencies
COPY package*.json ./

# sometimes the ownership of the files in the working directory is changed to root
# and thus the app can't access the files and throws an error -> EACCES: permission denied
# to avoid this, change the ownership of the files to the root user
USER root

# change the ownership of the /app directory to the app user
# chown -R <user>:<group> <directory>
# chown command changes the user and/or group ownership of for given file.
RUN chown -R app:app .

# change the user back to the app user
USER app

# install dependencies
RUN npm install

# copy the rest of the files to the working directory
COPY . .

# expose port 5173 to tell Docker that the container listens on the specified network ports at runtime
EXPOSE 5173

# command to run the app
CMD npm run dev
```



## Docker Compose file

Here’s a table summarizing all the key syntax and commands for creating and configuring a Docker Compose file:

| **Directive**       | **Syntax**                                    | **Description**                                                                     |
| ------------------- | --------------------------------------------- | ----------------------------------------------------------------------------------- |
| **version**         | `version: '3.8'`                              | Specifies the Docker Compose file format version.                                   |
| **services**        | `services:`                                   | Defines the services (containers) that make up the application.                     |
| **image**           | `image: image_name:tag`                       | Specifies the image to use for the service.                                         |
| **build**           | `build:`                                      | Defines the build context and Dockerfile for building the image.                    |
| **ports**           | `ports:`                                      | Maps host ports to container ports (e.g., `- "8080:80"`).                           |
| **volumes**         | `volumes:`                                    | Defines named volumes for services or paths for persistent data.                    |
| **environment**     | `environment:`                                | Sets environment variables for a service.                                           |
| **networks**        | `networks:`                                   | Configures custom networks for inter-service communication.                         |
| **depends\_on**     | `depends_on:`                                 | Specifies dependencies between services, ensuring one starts before another.        |
| **command**         | `command: ["executable", "param1", "param2"]` | Overrides the default command specified in the Docker image.                        |
| **restart**         | `restart: always`                             | Configures the restart policy for the service (e.g., `always`, `on-failure`, `no`). |
| **container\_name** | `container_name: name`                        | Sets a custom name for the container.                                               |
| **logging**         | `logging:`                                    | Configures logging options (e.g., driver, options).                                 |
| volumes\_from       | `volumes_from:`                               | Mounts volumes from another service or container (e.g., - service\_name).           |

#### **Example Docker Compose File**

```yaml
version: '3.8'

services:
  mongo:
    image: mongo:latest
    ports:
      - "27017:27017"
    volumes:
      - mongo_data:/data/db
    environment:
      - MONGO_INITDB_ROOT_USERNAME=admin
      - MONGO_INITDB_ROOT_PASSWORD=admin

  api:
    build:
      context: ./api
      dockerfile: Dockerfile
    depends_on:
      - mongo
    ports:
      - "5000:5000"
    environment:
      - MONGO_URI=mongodb://admin:admin@mongo:27017/mydatabase
    networks:
      - mern_network

  client:
    build:
      context: ./client
      dockerfile: Dockerfile
    depends_on:
      - api
    ports:
      - "3000:3000"
    networks:
      - mern_network

volumes:
  mongo_data:

networks:
  mern_network:
```

Example of volumes\_from Usage:

```yaml
version: '3.8'

services:
  db:
    image: postgres:latest
    volumes:
      - db_data:/var/lib/postgresql/data

  api:
    build:
      context: ./api
    depends_on:
      - db
    volumes_from:
      - db
    ports:
      - "5000:5000"

volumes:
  db_data:
```

```yaml
# specify the version of docker-compose
version: "3.8"

# define the services/containers to be run
services:
  # define the frontend service
  # we can use any name for the service. A standard naming convention is to use "web" for the frontend
  web:
    # we use depends_on to specify that service depends on another service
    # in this case, we specify that the web depends on the api service
    # this means that the api service will be started before the web service
    depends_on: 
      - api
    # specify the build context for the web service
    # this is the directory where the Dockerfile for the web service is located
    build: ./frontend
    # specify the ports to expose for the web service
    # the first number is the port on the host machine
    # the second number is the port inside the container
    ports:
      - 5173:5173
    # specify the environment variables for the web service
    # these environment variables will be available inside the container
    environment:
      VITE_API_URL: http://localhost:8000

    # this is for docker compose watch mode
    # anything mentioned under develop will be watched for changes by docker compose watch and it will perform the action mentioned
    develop:
      # we specify the files to watch for changes
      watch:
        # it'll watch for changes in package.json and package-lock.json and rebuild the container if there are any changes
        - path: ./frontend/package.json
          action: rebuild
        - path: ./frontend/package-lock.json
          action: rebuild
        # it'll watch for changes in the frontend directory and sync the changes with the container real time
        - path: ./frontend
          target: /app
          action: sync

  # define the api service/container
  api: 
    # api service depends on the db service so the db service will be started before the api service
    depends_on: 
      - db

    # specify the build context for the api service
    build: ./backend
    
    # specify the ports to expose for the api service
    # the first number is the port on the host machine
    # the second number is the port inside the container
    ports: 
      - 8000:8000

    # specify environment variables for the api service
    # for demo purposes, we're using a local mongodb instance
    environment: 
      DB_URL: mongodb://db/anime
    
    # establish docker compose watch mode for the api service
    develop:
      # specify the files to watch for changes
      watch:
        # it'll watch for changes in package.json and package-lock.json and rebuild the container and image if there are any changes
        - path: ./backend/package.json
          action: rebuild
        - path: ./backend/package-lock.json
          action: rebuild
        
        # it'll watch for changes in the backend directory and sync the changes with the container real time
        - path: ./backend
          target: /app
          action: sync

  # define the db service
  db:
    # specify the image to use for the db service from docker hub. If we have a custom image, we can specify that in this format
    # In the above two services, we're using the build context to build the image for the service from the Dockerfile so we specify the image as "build: ./frontend" or "build: ./backend".
    # but for the db service, we're using the image from docker hub so we specify the image as "image: mongo:latest"
    # you can find the image name and tag for mongodb from docker hub here: https://hub.docker.com/_/mongo
    image: mongo:latest

    # specify the ports to expose for the db service
    # generally, we do this in api service using mongodb atlas. But for demo purposes, we're using a local mongodb instance
    # usually, mongodb runs on port 27017. So we're exposing the port 27017 on the host machine and mapping it to the port 27017 inside the container
    ports:
      - 27017:27017

    # specify the volumes to mount for the db service
    # we're mounting the volume named "anime" inside the container at /data/db directory
    # this is done so that the data inside the mongodb container is persisted even if the container is stopped
    volumes:
      - anime:/data/db

# define the volumes to be used by the services
volumes:
  anime:
```

