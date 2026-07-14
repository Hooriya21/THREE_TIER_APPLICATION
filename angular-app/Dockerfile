# Stage 1: Build the Angular application
FROM node:20 AS build
WORKDIR /app

# Copy package files and install dependencies
COPY package*.json ./
RUN npm install

# Copy the rest of the application code and build it
COPY . .
RUN npm run build -- --configuration=production

# Stage 2: Serve the application using Nginx
FROM nginx:latest
# Copy the built artifacts from Stage 1 (adjust the path if your dist structure differs)
COPY --from=build /app/dist/angular-app/browser/ /usr/share/nginx/html/

EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]