# Use an official Node.js image as a base, specifying the version
FROM node:20.10.0

# Set the working directory in the container
WORKDIR /app

# Copy the package.json and yarn.lock files
COPY package.json yarn.lock ./

# Install the dependencies using yarn
RUN yarn install

# Copy the rest of the application code
COPY . .

# Expose the port the application runs on
EXPOSE 8800

# Command to run the application using yarn
CMD ["yarn", "start"]
