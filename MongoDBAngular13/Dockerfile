# Use an official Node runtime as a parent image
FROM node:14.17.0 AS builder

# Set the working directory to /app
WORKDIR /app

# Copy package.json and package-lock.json to the container
COPY package*.json ./

# Install dependencies
RUN npm install

# Copy the rest of the application files to the container
COPY . .

# Build the Angular application
RUN npm run build --prod

# Use a smaller base image for production
FROM nginx:1.21.0-alpine

# Copy the build files to the Nginx web server directory
COPY --from=builder /app/dist/mongo-dbangular13 /usr/share/nginx/html

# Expose port 80
EXPOSE 80

# Start the Nginx web server
CMD ["nginx", "-g", "daemon off;"]