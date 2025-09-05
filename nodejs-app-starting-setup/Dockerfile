# Step 1 get the base image
# FROM gives you the base image to use
FROM node

# docker from default runs commands in root, if you have a seperate directory folder and would like to run
# commands in it then you can add the command WORKDIR /directoryName to make docker run commands in there instead
WORKDIR /app


# Step 2 add files to your image - can use the COPY command.
#   COPY . .
# first dot is the path outside of the container where the files you want to copy into the image live
# second dot is the path inside the image where you want to store the files.
# containers have a seperate file system seperate to your system one.

#COPY . ./
# since we have a WORKDIR /app we dont need to define /app as the COPY Command below and can use ./ instead and use the realative path
# but its better to be explicit so we can trace steps

COPY . /app
# here we are copying everything into a new folder in the container called app.
# note we replace the second . with /app as we want to store in a specific folder called app

RUN npm install

# an image should be a template for a container, we shouldnt have any code in here to start servers or the likes such as RUN node server.js
# because they would be run every time an image is built and you are meant to run a container based on an image
# we want to have all the code and dependancies in an image and use containers to run the image

# docker containers are isolated so they also have their own networks, we need to allow the port to be listened to otherwise we wont be able to see the server
EXPOSE 80

CMD ["node", "server.js"]
# using CMD will run the command when a container is started - this should be the last step in your docker file



