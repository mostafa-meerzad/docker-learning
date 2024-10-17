# typically start with a base image
# we can start with linux and add node on top of it
# or we can just start with node! which are build on top of linux distributions
# these images are all defined in the dockerhub
# node build on top of linux alpine distribution which results in a very small image file
FROM node:alpine 
# here we say COPY all the files in the current directory into the app directory
# that image has a file-system and we're gonna create a directory called 'app'
COPY . /app
# here we specify the working directory to make file paths easier to work with
WORKDIR /app
# now using the CMD command we write the commands that start our application
# if we didn't specify the working-directory we had to write "CMD node app/app.js" because we've created an app directory withing that image
CMD node app.js
