# Docker Compose

Docker Compose is a tool used to define and run **multi-container Docker applications** using a single YAML configuration file.

Instead of running multiple `docker run` commands, you define all your services in a `docker-compose.yml` (or `compose.yml`) file and start everything with one command.

---

# Why Use Docker Compose?

Imagine your MERN application requires:

- Backend
- MongoDB
- Redis
- Nginx

Without Docker Compose:

```bash
docker run ...
docker run ...
docker run ...
docker run ...
```

You have to manually:

- Create networks
- Create volumes
- Map ports
- Set environment variables
- Start containers in the correct order

With Docker Compose:

```bash
docker compose up
```

Everything starts automatically.

---

# Benefits

- Manage multiple containers easily
- Single configuration file
- Automatic network creation
- Automatic volume creation
- Easy environment variable management
- Easy container startup and shutdown
- Great for local development

---

# Docker Compose File

Docker Compose uses a YAML file.

Common filenames:

```
compose.yml
```

or

```
docker-compose.yml
```

Modern Docker recommends:

```
compose.yml
```

---

# Basic Structure

```yaml
services:
  service-name:
    image:
    container_name:
    ports:
    volumes:
    environment:
    depends_on:
    networks:

volumes:

networks:
```

---

# Simple Example

```yaml
services:
  mongodb:
    image: mongo
    container_name: mongodb
    ports:
      - "27017:27017"

  backend:
    build: .
    container_name: backend
    ports:
      - "5000:5000"
```

Start:

```bash
docker compose up
```

---

# Complete MERN Example

```yaml
services:

  mongodb:
    image: mongo
    container_name: mongodb
    restart: always

    ports:
      - "27017:27017"

    volumes:
      - mongodb-data:/data/db

    networks:
      - mern-network

  backend:
    build: .

    container_name: backend

    restart: always

    ports:
      - "5000:5000"

    depends_on:
      - mongodb

    environment:
      MONGO_URI: mongodb://mongodb:27017/mydatabase
      PORT: 5000

    networks:
      - mern-network

volumes:
  mongodb-data:

networks:
  mern-network:
```

Start everything:

```bash
docker compose up
```

---

# Explanation

## image

Downloads an image from Docker Hub.

```yaml
image: mongo
```

---

## build

Builds an image from your Dockerfile.

```yaml
build: .
```

Current directory:

```
.
```

Specific directory:

```yaml
build: ./backend
```

---

## container_name

Sets a custom container name.

```yaml
container_name: backend
```

Without this, Docker generates a random name.

---

## ports

Maps host ports to container ports.

```yaml
ports:
  - "5000:5000"
```

Format:

```
HOST:CONTAINER
```

---

## volumes

Mounts persistent storage.

```yaml
volumes:
  - mongodb-data:/data/db
```

---

## environment

Environment variables.

```yaml
environment:
  PORT: 5000
  NODE_ENV: production
```

Equivalent to:

```bash
-e PORT=5000
```

---

## depends_on

Starts services in dependency order.

```yaml
depends_on:
  - mongodb
```

This starts MongoDB before the backend.

**Important:** It does **not** wait until MongoDB is fully ready to accept connections. Your application should still handle retries.

---

## restart

Restart policy.

```yaml
restart: always
```

Options:

```yaml
restart: "no"
restart: always
restart: unless-stopped
restart: on-failure
```

---

## networks

Connects services to a network.

```yaml
networks:
  - mern-network
```

Docker Compose creates the network automatically.

---

# Named Volumes

Declare volumes at the bottom.

```yaml
volumes:
  mongodb-data:
```

Use inside a service:

```yaml
volumes:
  - mongodb-data:/data/db
```

---

# Named Networks

```yaml
networks:
  mern-network:
```

Attach services:

```yaml
networks:
  - mern-network
```

---

# Environment File (.env)

Instead of hardcoding values:

```yaml
environment:
  PORT: 5000
```

Use:

```yaml
environment:
  PORT: ${PORT}
  MONGO_URI: ${MONGO_URI}
```

Create `.env`

```env
PORT=5000
MONGO_URI=mongodb://mongodb:27017/mydatabase
```

Docker Compose automatically loads the `.env` file if it's in the same directory.

---

# Common Docker Compose Commands

## Start Services

```bash
docker compose up
```

---

## Start in Background

```bash
docker compose up -d
```

---

## Stop Services

```bash
docker compose down
```

---

## Stop and Remove Volumes

```bash
docker compose down -v
```

---

## View Running Containers

```bash
docker compose ps
```

---

## View Logs

```bash
docker compose logs
```

Follow logs:

```bash
docker compose logs -f
```

Specific service:

```bash
docker compose logs backend
```

---

## Restart Services

```bash
docker compose restart
```

Specific service:

```bash
docker compose restart backend
```

---

## Build Images

```bash
docker compose build
```

Rebuild without cache:

```bash
docker compose build --no-cache
```

---

## Start After Build

```bash
docker compose up --build
```

---

## Execute Commands Inside a Container

```bash
docker compose exec backend sh
```

MongoDB:

```bash
docker compose exec mongodb mongosh
```

---

## Stop Services

```bash
docker compose stop
```

---

## Start Stopped Services

```bash
docker compose start
```

---

## Pull Latest Images

```bash
docker compose pull
```

---

## Remove Stopped Containers

```bash
docker compose rm
```

---

# Docker Compose Lifecycle

```
compose.yml
      │
      ▼
docker compose up
      │
      ▼
Build Images (if needed)
      │
      ▼
Create Network
      │
      ▼
Create Volumes
      │
      ▼
Start Containers
```

---

# Docker Compose vs Docker Run

| Docker Run | Docker Compose |
|------------|----------------|
| One container at a time | Multiple containers |
| Long commands | Single YAML file |
| Manual networking | Automatic networking |
| Manual volumes | Automatic volumes |
| Difficult to maintain | Easy to maintain |
| Best for quick tests | Best for real projects |

---

# Best Practices

- Keep secrets in `.env`, not in `compose.yml`.
- Use named volumes for databases.
- Use `depends_on` for service startup order.
- Use service names (e.g., `mongodb`) instead of IP addresses.
- Version-control your `compose.yml` file.
- Don't commit sensitive `.env` files to Git.

---

# Real MERN Folder Structure

```
project/
│
├── backend/
│   ├── Dockerfile
│   └── ...
│
├── frontend/
│   ├── Dockerfile
│   └── ...
│
├── compose.yml
├── .env
└── README.md
```

---

# Quick Interview Questions

### What is Docker Compose?

A tool to define and manage multi-container Docker applications using a YAML file.

### Why use Docker Compose?

To start, stop, configure, and manage multiple containers with a single command.

### What is the difference between `image` and `build`?

- `image` pulls a prebuilt image from a registry (like Docker Hub).
- `build` creates an image from a local `Dockerfile`.

### Does `depends_on` wait until a database is ready?

No. It only controls the startup order. Applications should implement connection retries or health checks.

### Does Docker Compose create networks automatically?

Yes. If you don't define a network, Compose creates a default network for the project.

### What happens when you run `docker compose down -v`?

It stops and removes the containers, networks, and **named volumes** created by the Compose project.

### What is the difference between `docker compose stop` and `docker compose down`?

- `stop` stops containers but keeps them and the network.
- `down` stops and removes containers and the project network (and optionally volumes with `-v`).
