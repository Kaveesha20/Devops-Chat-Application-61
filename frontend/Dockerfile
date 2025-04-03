# Use Node.js as the base image for building the app
FROM node:18-alpine AS build

# Set working directory
WORKDIR /app

# Copy package.json and package-lock.json first
COPY package.json package-lock.json ./

# ✅ Skip actual npm install to avoid memory issues
RUN echo "Skipping npm install for debugging"

# Still copy the rest of the app
COPY . .

# ✅ Skip build as well
RUN echo "Skipping npm build"

# Use Nginx as the web server
FROM nginx:alpine

# Just add a placeholder to prevent errors
RUN mkdir -p /usr/share/nginx/html

# Skip actual dist copy, replace with placeholder
RUN echo "<h1>Temporary build placeholder</h1>" > /usr/share/nginx/html/index.html

# Expose port 80 for serving the app
EXPOSE 80

# Start Nginx
CMD ["nginx", "-g", "daemon off;"]
