# Basic Docker Commands

This document covers the most commonly used Docker commands for beginners.

---

# Pull an Image

Downloads an image from a Docker registry (Docker Hub by default).

```bash
docker pull <image-name>
```

### Example

```bash
docker pull nginx
docker pull node:22
docker pull mongo:8
```

---

# Run a Container

Creates and starts a new container from an image.

```bash
docker run <image-name>
```

### Example

```bash
docker run nginx
```

If the image doesn't exist locally, Docker automatically downloads it before running the container.

---

# Run a Container in Detached Mode

Runs a container in the background.

```bash
docker run -d <image-name>
```

### Example

```bash
docker run -d nginx
```

Without `-d`, the container runs in the foreground and attaches to your terminal.

with `-d` the container runs in background and allow you to
use same terminal for other commands.

---

# Run a Container with Port Mapping

Maps a port on your computer (host) to a port inside the container.

```bash
docker run -p <host-port>:<container-port> <image-name>
```

### Example

```bash
docker run -p 8080:80 nginx
```

Now you can access the application at:

```
http://localhost:8080
```

### How Port Mapping Works

```
Your Computer (Host)        Docker Container
      8080        ───────►       80
```

---

# Run with Detached Mode and Port Mapping

You will often use both options together.

```bash
docker run -d -p 8080:80 nginx
```

This:

* Starts the container
* Runs it in the background
* Maps port `8080` on your machine to port `80` inside the container

---

# List Running Containers

Shows only currently running containers.

```bash
docker ps
```

Example output:

```text
CONTAINER ID   IMAGE    STATUS         PORTS
8a3d21c4       nginx    Up 5 minutes   0.0.0.0:8080->80/tcp
```

---

# List All Containers

Shows both running and stopped containers.

```bash
docker ps -a
```

Example output:

```text
CONTAINER ID   IMAGE    STATUS
8a3d21c4       nginx    Exited (0)
f13b98aa       node     Up 10 minutes
```

---

# Stop a Running Container

Stops a running container gracefully.

```bash
docker stop <container-id-or-name>
```

### Example

```bash
docker stop 8a3d21c4
```

or

```bash
docker stop my-nginx
```

---

# Start a Stopped Container

Starts an existing stopped container.

```bash
docker start <container-id-or-name>
```

### Example

```bash
docker start my-nginx
```

---

# Naming a Container (Recommended)

Instead of remembering container IDs, give your container a name.

```bash
docker run --name my-nginx nginx
```

Now you can use:

```bash
docker stop my-nginx
docker start my-nginx
```

instead of using the container ID.

---

# Command Summary

| Command                                   | Description                           |
| ----------------------------------------- | ------------------------------------- |
| `docker pull <image>`                     | Download an image                     |
| `docker run <image>`                      | Create and start a container          |
| `docker run -d <image>`                   | Run a container in the background     |
| `docker run -p HOST:CONTAINER <image>`    | Map host and container ports          |
| `docker run -d -p HOST:CONTAINER <image>` | Run in background with port mapping   |
| `docker ps`                               | Show running containers               |
| `docker ps -a`                            | Show all containers                   |
| `docker stop <container>`                 | Stop a running container              |
| `docker start <container>`                | Start a stopped container             |
| `docker run --name NAME <image>`          | Create a container with a custom name |

---

# Quick Example

```bash
# Download the image
docker pull nginx

# Run nginx in the background
docker run -d -p 8080:80 --name my-nginx nginx

# View running containers
docker ps

# Stop the container
docker stop my-nginx

# Start it again
docker start my-nginx

# View all containers
docker ps -a
```

After running the container, open your browser and visit:

```
http://localhost:8080
```

If everything is working correctly, you should see the default **Welcome to nginx!** page.
