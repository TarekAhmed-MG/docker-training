# 🚀 docker-training

A growing cheatsheet and training guide for Docker.
This section covers the **step-by-step process to build a Docker image**.

---

## 📑 Table of Contents

1. [Steps to Build a Docker Image](#-steps-to-build-a-docker-image)

    * [Add a Dockerfile to your project](#1-add-a-dockerfile-to-your-project)
    * [Write the Dockerfile](#2-write-the-dockerfile)
    * [Build the image](#3-build-the-image)
    * [Run a container from the image](#4-run-a-container-from-the-image)
2. [Explanation of Dockerfile Instructions](#-explanation-of-dockerfile-instructions)
3. [Quick Notes](#-quick-notes)
4. [Handy Commands](#-handy-commands)
5. [🐳 Docker Commands Cheat Sheet](#-docker-commands-cheat-sheet)
6. [Docker Image Layer System](#-docker-image-layer-system)

---

## 🛠️ Steps to Build a Docker Image

### 1. Add a Dockerfile to your project

* The `Dockerfile` defines the instructions for building the image.
* Place it in the root of your project (or in the directory you will build from).

---

### 2. Write the Dockerfile

A minimal Dockerfile typically includes:

```dockerfile
# Step 1: Start from a base image
FROM baseImage

# Step 2: (Optional) Set a working directory
WORKDIR /dir

# Step 3: Copy project files into the image
COPY . /folder

# Step 4: (Optional) Run build/install commands
RUN <your-build-command>

# Step 5: Document the port your app will use
EXPOSE port

# Step 6: Define the default runtime command
CMD ["your-program", "arg1", "arg2"]
```

---

## 🐳 Docker Commands Cheat Sheet

| Command                                   | Description                                          |                                                                                                                                                                                                |
| ----------------------------------------- | ---------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `docker pull <image>`                     | Download an image from Docker Hub (or registry).     |                                                                                                                                                                                                |
| `docker run <image>`                      | Start a container (pulls the image if not found).    |                                                                                                                                                                                                |
| `docker ps`                               | Show running containers.                             |                                                                                                                                                                                                |
| `docker ps -a`                            | Show all containers (running + stopped).             |                                                                                                                                                                                                |
| `docker stop <containerId>`               | Stop a running container.                            |                                                                                                                                                                                                |
| `docker rm <containerId>`                 | Remove a container.                                  |                                                                                                                                                                                                |
| `docker images`                           | List all images.                                     |                                                                                                                                                                                                |
| `docker rmi <imageId>`                    | Remove an image.                                     |                                                                                                                                                                                                |
| \$1                                       | `docker run -p <hostPort>:<containerPort> <image>`   | Publish a container port to the host (`host:container`). Use multiple `-p` flags for several ports. Optional: `-p <hostIP>:<hostPort>:<containerPort>` or `-p <hostPort>:<containerPort>/udp`. |
| `docker exec -it <containerId> /bin/bash` | Open interactive shell inside a container.           |                                                                                                                                                                                                |
| `docker run -it <image>`                  | Run a container interactively (keeps terminal open). |                                                                                                                                                                                                |

> **Tip:** If a container is still running, `docker rm` will fail. Use `docker stop <id>` first, or `docker rm -f <id>` to force removal.

---

### 🔑 Key Concepts

* **Image** → Blueprint containing app code + dependencies.
* **Container** → Running instance of an image.
* Typically, you start from a **base image** (e.g., `ubuntu`, `python`) and add your code on top so it executes inside the container.

---

### 🖼️ Visual: Image → Container → Running App

```mermaid
flowchart LR
    A[Docker Image<br>(Blueprint)] --> B[Container<br>(Instance of Image)]
    B --> C[Running Application]
```

# 🐳 Docker Image Layer System

Docker images are built in **layers**. Each instruction in a `Dockerfile` creates a new immutable layer on top of the previous one.  
Layers are **cached**, so if nothing changes in a layer, Docker reuses it to speed up builds.

---

## 🔹 How Layers Work
- **Base Layer**: The starting point (e.g., `FROM ubuntu:20.04`).
- **Instruction Layers**: Each `RUN`, `COPY`, or `ADD` creates a new layer.
- **Metadata Layers**: Instructions like `WORKDIR`, `ENV`, and `EXPOSE` also form layers.
- **Final Layer**: Defined by `CMD` or `ENTRYPOINT`.

---
