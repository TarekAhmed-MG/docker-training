#########################################################
# Step 1: Choose a base image
#########################################################
# Every Dockerfile must start with a base image.
# This acts like the "foundation" for your container.
# Example: `node` includes Node.js + npm pre-installed.
# You can also choose a lighter image such as `node:18-alpine`
# to reduce the image size.
FROM node

#########################################################
# Step 2: Set the working directory inside the container
#########################################################
# By default, Docker runs all commands in the root (/) directory.
# It's best practice to create a separate folder for your app.
# WORKDIR will create the folder if it doesn’t exist
# and switch into it for subsequent instructions.
WORKDIR /app

#########################################################
# Optimization => since docker files are built on layers
# we now just copy the json package and do npm install before copying the code
# This is becuase docker rebuilds the changed layer and all the other layers after it,
# this saves having to RUN npm install every time we change the code.
#########################################################
COPY package.json /app

#########################################################
# Step 3: Install dependencies
#########################################################
# RUN executes a command during the build process
# (this happens once when the image is created).
# In this case we install Node.js dependencies inside the container,
# so our app is self-contained and portable.
RUN npm install

#########################################################
# Step 4: Copy files into the image
#########################################################
# Containers have their own isolated filesystem.
# COPY takes files from your local machine (build context)
# and moves them into the container's filesystem.
#
# Syntax: COPY <source on host> <destination in container>
#
# Example: COPY . ./
#   - The first `.` means "all files from current directory (host)"
#   - The second `.` means "place them in current WORKDIR (/app)"
#
# Here we explicitly use `/app` to make it clearer where files go.
COPY . /app

#########################################################
# Step 5: Expose a port (optional) still need to do docker run with the -p tag with localPort:containerPort to see
#########################################################
# Containers have isolated networks — if we don’t expose a port,
# no external traffic can reach our app.
# EXPOSE documents the port the container listens on.
# Note: EXPOSE itself doesn’t actually publish the port —
# we still need to map it using `docker run -p`.
EXPOSE 80

#########################################################
# Step 6: Set the startup command
#########################################################
# CMD specifies the default command to run *when a container starts*.
# This should be a long-running process like starting a server.
#
# Difference from RUN:
# - RUN executes at build time (bakes things into the image)
# - CMD executes at runtime (when container starts)
#
# Syntax: CMD ["executable", "param1", "param2"]
CMD ["node", "server.js"]
