# Use the official Node.js 20 image as the base image
FROM node:20

# Set the working directory inside the container.
# If the directory doesn't exist, Docker creates it automatically.
WORKDIR /app

# Copy only package.json and package-lock.json first.
# This improves Docker layer caching because dependencies
# are installed only when these files change.
COPY package*.json ./

# Install project dependencies.
# This layer is cached until package.json changes.
RUN npm install

# Copy the remaining application source code.
COPY . .

# Inform Docker that the application listens on port 3000.
# This is documentation only; it does NOT expose the port.
EXPOSE 3000

# Default command executed when the container starts.
# Starts the Node.js application.
CMD ["npm", "start"]