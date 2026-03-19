# Builder stage
FROM node:20-alpine AS builder

# Set working directory
WORKDIR /app

# Accept backend URL as a build argument
ENV VITE_API_URL=http://localhost:5000/api

# Copy package files and install dependencies
COPY package*.json ./

RUN npm install 

# Copy the rest of the source code
COPY . .

# Build the frontend (Vite will use VITE_BACKEND_APP_URL)
RUN npm run build

# Nginx stage
FROM nginx:alpine

# Copy built frontend
COPY --from=builder /app/dist /usr/share/nginx/html

# Copy Nginx config
COPY nginx.conf /etc/nginx/conf.d/default.conf

# Expose port 80
EXPOSE 80

# Start Nginx
CMD ["nginx", "-g", "daemon off;"]