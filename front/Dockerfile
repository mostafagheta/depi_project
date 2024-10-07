# Step 1: Build the React application
FROM node:18-alpine AS build

# Set the working directory inside the container
WORKDIR /app

# Copy package.json and package-lock.json to the working directory
COPY package*.json ./

# Install the dependencies
RUN npm install --silent

# Copy the rest of the application code to the working directory
COPY . .

# Build the React application
RUN npm run build

# Step 2: Serve the React application using nginx
FROM nginx:alpine

# Copy the built files from the previous step to nginx's default directory
COPY --from=build /app/build /usr/share/nginx/html

# Expose port 80 to access the web app
EXPOSE 80

# Start nginx when the container starts
CMD ["nginx", "-g", "daemon off;"]
