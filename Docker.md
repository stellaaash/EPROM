
# Important concepts
## Containers
Simply put, a container is **another process on your machine that has been isolated from all other processes on the host machine**.
That isolation leverages [[Kernel]] namespaces and [[cgroup]]s, both features of [[Linux]].
**Containers have a fixed filesystem by default**, your changes won't stick over to the next time you launch them, and two identical containers don't share filesystems.
For having persistent data stay even after shutting down a container instance, **you need volumes**.
## Volumes
Volumes allow to connect specific filesystem paths of the container back to the host machine.
**If a directory in the container is mounted, changes in that directory are also seen on the host machine.**
Thus, if you mount that same directory across container restarts, you'll have persistent storage.
There are **two types** of docker volumes: *named volumes* and *bind mounts*.
### Named Volumes
Named volumes are **great at just storing data**, without worrying about where the data is actually stored.
### Bind Mounts
With bind mounts, **you control the exact mountpoint on the host**.
When working on an application, you can use a bind mount to mount the source code into the container to let it see the code changes, and update the app directly for us to see the changes as we save.
Many languages provide tool to watch for changes and reload the application dynamically.
## Images
When running a container, **it uses an isolated filesystem**. This custom filesystem **is provided by a container image**.
Since the image contains the sheer filesystem of a container, **it must contain everything needed to run an application**:
- Dependencies
- Scripts
- Binaries
- Libraries
- etc...
The image also contains **other configuration for the container, such as environment variables, a default command to run, and other metadata**.
## Dockerfiles
Dockerfiles are **text-based scripts of instructions to create a container image**.
# Multi-Container Apps
Ideally when running multiple services in an app, **each container should run only one service, and do it well**.
This makes it way easier to scale individual services as demand rises (only up the database and not the actual website's resources).
It also helps when updating versions, you can update one container at a time instead of everything at once.
## Container Networking
By default, Docker containers **run in isolation**. You need to link them together in order to make them communicate.
The idea is simply to **put all the containers you need to talk on the same network**.
When you define an *alias* for your container in the network, what it does is **adding an A [[Domain Name System]] entry for the IP of the container and that alias**.
# Docker Compose
Docker Compose is **a tool that was developed to help define and share multi-container applications**.
With Compose, you can create a [[YAML]] file to define the services and, with a single command, can spin everything up or tear it al down.
The big advantage of this is that **you can just give a Compose file to someone and they'd be able to build an exact copy of your environment**.
# Cheatsheet
## Commands
```bash
# List currently running containers
docker ps
docker ps -a  # Also include not-running containers

# List all containers currently installed
docker container list -a

# Stop a container
docker stop container_id

# Runs an image in detached mode and maps port 80 of the host to port 80 in the container
docker run -d -p 80:80 path/to/image
# Runs an image in detached mode over port 3000, and maps the volume todo-db to /etc/todos
docker run -dp 3000:3000 -v todo-db:/etc/todos path/to/image
# Runs an image in detached mode over port 3000, and uses a bind mount to bind /home/user/todos from the host to /etc/todos in the container
docker run -dp 3000:3000 -v /home/user/todos:/etc/todos path/to/image
# Runs a shell with a command as soon as the container is finished loading
docker run -d -p 80:80 path/to/image sh -c "command -arguments"
# Runs a container on a network, specifying a distrinctive name for it to be identified with on that same network
docker run -d -p 80:80 path/to/image --network network_name --network-alias alias
# Run a container with an environment variable
docker run -d -p 80:80 path/to/image -e KEY=value

# Run a command inside of a container
docker exec container_id command arguments

# Create a new volume
docker volume create volume_name
# Inspect a volume
docker volume inspect volume_name

# Look at the logs for a container
docker logs -f container_id

# Create a new network
docker network create network-name

# Build and run a docker compose app
docker compose up
docker compose up -d  # In detached mode

# Stop a docker compose app
docker compose down

# See all logs of docker compose services running in real time
docker compose logs -f
docker compose logs -f app  # For a specific app

# Scan an image for security vulnerabilities
docker scout cves image_name
# See the individual layers of an image
docker image history image_name
```
## Dockerfiles
### Example one - Simple webapp
```dockerfile
FROM node:10-alpine
WORKDIR /app
COPY . .
RUN yarn install --production
CMD ["node", "/app/src/index.js"]
```