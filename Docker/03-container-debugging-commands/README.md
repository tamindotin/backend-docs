# Docker Container Debugging Commands

These commands help you inspect, debug, and interact with running Docker containers.

---

# View Container Logs

Displays the output (stdout and stderr) of a container.

```bash
docker logs <container_name_or_id>
```

### Example

```bash
docker logs my-nginx
```

---

# Follow Logs in Real Time

Continuously streams new log output.

```bash
docker logs -f <container_name_or_id>
```

### Example

```bash
docker logs -f my-nginx
```

Useful for monitoring an application while it is running.

---

# Show Last N Lines of Logs

Displays only the most recent log entries.

```bash
docker logs --tail 20 <container_name_or_id>
```

### Example

```bash
docker logs --tail 50 my-nginx
```

---

# Execute a Command Inside a Running Container

Runs a single command inside an already running container.

```bash
docker exec <container_name_or_id> <command>
```

### Example

```bash
docker exec my-nginx ls
```

Output:

```
bin
etc
usr
var
...
```

---

# Open an Interactive Shell Inside a Container

Starts an interactive terminal session.

```bash
docker exec -it <container_name_or_id> bash
```

### Example

```bash
docker exec -it my-nginx bash
```

If Bash is not installed:

```bash
docker exec -it my-nginx sh
```

---

## What do `-i` and `-t` mean?

### `-i` (Interactive)

Keeps STDIN open so you can type commands.

### `-t` (TTY)

Allocates a terminal, making the shell behave like a normal Linux terminal.

Together:

```bash
docker exec -it my-nginx bash
```

means:

> Open an interactive terminal inside the running container.

---

# Run a Single Command Without Opening a Shell

```bash
docker exec my-nginx pwd
```

Output:

```
/
```

Another example:

```bash
docker exec my-nginx cat /etc/os-release
```

---

# Check Running Processes Inside a Container

```bash
docker exec my-nginx ps aux
```

Useful for verifying that your application is actually running.

---

# Check Environment Variables

```bash
docker exec my-nginx env
```

Shows all environment variables available inside the container.

---

# Check Current Working Directory

```bash
docker exec my-nginx pwd
```

---

# List Files Inside a Container

```bash
docker exec my-nginx ls
```

Or with details:

```bash
docker exec my-nginx ls -la
```

---

# Inspect a Container

Shows detailed information about a container in JSON format.

```bash
docker inspect <container_name_or_id>
```

### Example

```bash
docker inspect my-nginx
```

Useful information includes:

- Container ID
- Image
- Network settings
- Mounted volumes
- Environment variables
- Port mappings
- IP address
- Restart policy

---

# View Resource Usage

Displays CPU, memory, and network usage of running containers.

```bash
docker stats
```

Example output:

```
CONTAINER ID   NAME       CPU %   MEM USAGE
a1b2c3d4       my-nginx   0.03%   18MiB
```

Press **Ctrl + C** to stop monitoring.

---

# Common Debugging Workflow

Suppose your container isn't working.

### Step 1

Check if it's running.

```bash
docker ps
```

### Step 2

View logs.

```bash
docker logs my-container
```

### Step 3

Open a shell.

```bash
docker exec -it my-container bash
```

(or `sh` if Bash isn't installed)

### Step 4

Inspect files or configuration.

```bash
ls
cat .env
```

### Step 5

Check running processes.

```bash
ps aux
```

### Step 6

Exit the container.

```bash
exit
```

---

# Summary

| Command | Purpose |
|----------|---------|
| `docker logs` | View container logs |
| `docker logs -f` | Follow logs in real time |
| `docker logs --tail 20` | Show last N log lines |
| `docker exec` | Run a command inside a container |
| `docker exec -it bash` | Open an interactive Bash shell |
| `docker exec -it sh` | Open an interactive SH shell |
| `docker inspect` | View detailed container information |
| `docker stats` | Monitor CPU and memory usage |
