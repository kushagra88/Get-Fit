# Step 1: Use a lightweight Node.js image for the build stage
FROM node:16-alpine as build

# Set the working directory in the container
WORKDIR /app

# Copy package.json and package-lock.json
COPY package*.json ./

# Install dependencies
RUN npm install

# Copy the rest of the project files
COPY . .

# Build the React app
RUN npm run build

# Step 2: Use a lightweight web server for serving the built app
FROM nginx:alpine

# Copy the built files from the previous stage
COPY --from=build /app/build /usr/share/nginx/html

# Expose the default port used by Nginx
EXPOSE 80

# Start Nginx
CMD ["nginx", "-g", "daemon off;"]
