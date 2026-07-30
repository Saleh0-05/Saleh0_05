# Use a lightweight version of Node.js
FROM node:20-alpine

# Set the working directory inside the container
WORKDIR /app

# Copy package.json and package-lock.json first (for caching)
COPY package*.json ./

# Install backend dependencies
RUN npm install

# Copy the rest of the backend source code
COPY . .

# Expose the port your Node.js server listens on (from your compose file)
EXPOSE 3002

# The command to start your backend server (adjust "start" if your script is different)
CMD ["npm", "start"]
