# Set the base image to create the image for react app
FROM node:24-alpine

# Crate a user with permissions to run the app
# -S -> create a system user
# -G -> add the user to a group
# This is done to avoid running the app as root
# If the app is run as root, any vulnerability in the app can be exploited to gain access to the host system
# It's a good practice to run the app as a non-root user
RUN addgroup app && adduser -S -G app app

# set the user to run the app
USER app

# set the working directory to /app
WORKDIR /app

# Copy packges.json  and package-lock.json to the working directory
# This is done before copying the rest of the files to take advantage of docker's cache
# If the package.json and package-lock.json files haven't changes. docker will use the cached dependecies
COPY package*.json ./

# Sometimes the ownership of the files in the working directory is changed to root
# and thus the app can't access the files and throws an error -> EACCESS: permission denied
# to avoid this, change the ownership of the files to the root user
USER root

# Change the ownership of the /app dir to the app user
# chown -R <user>:<group> <directory>
# chown commands changes the user and/or group ownership of the given file
RUN chown -R app:app .

# Change the user back to the app user
USER app

# Install dependencies
RUN npm install

# Copy the rest of the files to the working directory
COPY . .

# Expose port 5173 to tell Docker that the container listens on the specified network ports at runtime
EXPOSE 5173

# Command to run the app
CMD ["npm", "run", "dev"]