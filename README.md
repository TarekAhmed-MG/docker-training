# 🚀 docker-training

A growing cheatsheet and training guide for Docker.  
This section covers the **step-by-step process to build a Docker image**.

---

## 📑 Table of Contents

1. [Steps to Build a Docker Image](#-steps-to-build-a-docker-image)
    - [Add a Dockerfile to your project](#1-add-a-dockerfile-to-your-project)
    - [Write the Dockerfile](#2-write-the-dockerfile)
    - [Build the image](#3-build-the-image)
    - [Run a container from the image](#4-run-a-container-from-the-image)
2. [Explanation of Dockerfile Instructions](#-explanation-of-dockerfile-instructions)
3. [Quick Notes](#-quick-notes)
4. [Handy Commands](#-handy-commands)
5. [What’s Next](#-whats-next)

---

## 🛠️ Steps to Build a Docker Image

### 1. Add a Dockerfile to your project

- The `Dockerfile` defines the instructions for building the image.
- Place it in the root of your project (or in the directory you will build from).

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

