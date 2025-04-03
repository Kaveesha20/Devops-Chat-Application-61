# Use official Node.js image as base
#FROM node:18

# Set working directory
#WORKDIR /app

# Copy package.json and package-lock.json
#COPY package*.json ./

# Install dependencies
#RUN npm install

# Copy the rest of the app files
#COPY . .

# Expose the port your app runs on
#EXPOSE 5000

# Start the application
#CMD ["npm", "start"]
# Use official Node.js image as base
FROM node:18

# Set working directory for the app
WORKDIR /app

# Copy package.json and package-lock.json to the working directory
COPY package*.json ./

# Install dependencies
RUN npm install

# Copy the rest of the application files to the container
COPY . .

# Expose the port your backend runs on (in your case, 5001 as updated previously)
EXPOSE 5001

# Start the application
CMD ["npm", "start"]

