
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

### Bind Mounts

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
docker run -dp 3000:3000 -v todo-db:/etc/todos docker-101

# Run a command inside of a container
docker exec container_id command arguments

# Create a new volume
docker volume create volume_name
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