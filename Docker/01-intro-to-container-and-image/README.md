# Docker Images and Containers

## What is a Container?

A **container** is a lightweight, isolated environment that packages an application together with everything it needs to run, including:

* Application source code
* Runtime
* Libraries
* Dependencies
* Configuration files

Containers ensure that an application runs the same way regardless of where it is deployed.

### Benefits

* Highly portable across different environments
* Consistent development and production environments
* Easy to share with other developers and teams
* Faster deployment and simplified setup

---

## Where Do Containers Come From?

Containers are **created from Docker images**.

Docker images are usually stored in **container registries** (also called image repositories), which can be either public or private.

Some popular registries include:

* **Docker Hub** – The default public registry for Docker images.
* **GitHub Container Registry (GHCR)**
* **Amazon Elastic Container Registry (ECR)**
* **Google Artifact Registry**
* **Azure Container Registry (ACR)**

> **Note:** Registries store **images**, not running containers. Containers exist only while running on a Docker host.

---

## Why Use Containers in Development?

### Without Containers

When multiple developers work on the same project:

* Everyone installs dependencies manually.
* Installation steps may differ between operating systems.
* Different dependency versions can cause unexpected bugs.
* Setting up a new development environment takes time.

### With Containers

Using Docker:

* Dependencies are installed once inside the image.
* Every developer uses the same environment.
* The same Docker commands work across Windows, macOS, and Linux.
* Multiple versions of the same application or service can run without conflicts.
* New developers can start the project with just a few Docker commands.

---

## What is a Docker Image?

A **Docker image** is a lightweight, standalone, read-only, executable package that contains everything required to run an application.

It includes:

* Application source code
* Runtime (e.g., Node.js, Python, Java)
* System libraries
* Dependencies
* Environment configuration
* Startup command

Images are built once and can be shared through container registries.

---

## Image vs Container

A Docker **image** is a blueprint or template.

A Docker **container** is a running instance of that image.

You can create multiple containers from the same image, and each container runs independently.

```
Dockerfile
      │
      ▼
Docker Image
      │
docker run
      ▼
Docker Container (Running Application)
```
