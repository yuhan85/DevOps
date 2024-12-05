# # Use an official Node runtime as a parent image
# FROM node:14-alpine

# # Set the working directory in the container
# WORKDIR /app

# # Copy package.json and package-lock.json
# COPY package*.json ./

# # Install app dependencies
# RUN npm install

# # Copy the current directory contents into the container
# COPY . . 

# # Build the app
# RUN npm run build

# # Make port 3000 available to the world outside this container
# EXPOSE ${PORT}

# # Define environment variable
# ENV REACT_APP_API_URL=http://localhost:5000
# ENV NODE_ENV=production
# ENV PORT=3000

# # Run the app when the container launches
# CMD ["npm", "start"]


# Stage 1: Build the React app
FROM node:14-alpine AS build
WORKDIR /app
COPY package*.json ./
RUN npm install
COPY . . 
RUN npm run build

# Stage 2: Serve the React app using Nginx
FROM nginx:alpine
COPY --from=build /app/build /usr/share/nginx/html

# Expose port 80 (Nginx default port)
EXPOSE 80

CMD ["nginx", "-g", "daemon off;"]
