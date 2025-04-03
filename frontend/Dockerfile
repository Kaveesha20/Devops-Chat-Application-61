
# Use Node.js as the base image
FROM node:18-alpine AS build

# Set working directory
WORKDIR /app

# Copy package.json and package-lock.json
COPY package.json package-lock.json ./

# Install dependencies
RUN npm install

# Copy project files
COPY . .

# Build the frontend
RUN npm run build

# Use nginx to serve the frontend
FROM nginx:alpine

# Copy built files to nginx
COPY --from=build /app/dist /usr/share/nginx/html

# Expose port 80
EXPOSE 80

# Start nginx
CMD ["nginx", "-g", "daemon off;"]
