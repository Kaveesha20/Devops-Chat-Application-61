
# # Use Node.js as the base image
# FROM node:18-alpine

# # Set working directory
# WORKDIR /app

# # Copy package.json and package-lock.json
# COPY package.json package-lock.json ./

# # Install dependencies
# RUN npm install

# # Copy project files
# COPY . .

# # Expose port
# EXPOSE 5000

# # Start the backend server
# CMD ["npm", "start"]
# Use Node.js as the base image
FROM node:18-alpine

# Set working directory
WORKDIR /app

# Copy package.json and package-lock.json
COPY package.json package-lock.json ./

# Install dependencies
RUN npm install

# Copy all project files (including src/, etc.)
COPY . .

# Copy the environment file
COPY .env .env

# Expose port
EXPOSE 5000

# Start the backend server
CMD ["npm", "start"]
