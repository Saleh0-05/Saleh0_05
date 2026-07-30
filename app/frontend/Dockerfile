# Stage 1: Build the React application
FROM node:20-alpine AS build
WORKDIR /app

# Copy dependencies first for better caching
COPY package*.json ./
RUN npm install

# Copy the rest of the application code
COPY . .

# Bypass the ESLint bug during the build
ENV DISABLE_ESLINT_PLUGIN=true

# Pass the API URL into the React build process
ARG REACT_APP_API_URL=http://localhost:5000
ENV REACT_APP_API_URL=$REACT_APP_API_URL

# Build the React app
RUN npm run build

# Stage 2: Serve the application with Nginx
FROM nginx:alpine

# Copy the finished build from Stage 1 into Nginx
COPY --from=build /app/build /usr/share/nginx/html

# Expose port 80 for Nginx
EXPOSE 80

# Start Nginx in the foreground
CMD ["nginx", "-g", "daemon off;"]
