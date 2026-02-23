# FROM node:18 AS build
# WORKDIR /app
# COPY . ./
# RUN npm i && npm run build

# FROM nginx
# COPY --from=build /app/dist /usr/share/nginx/html
# EXPOSE 80
# CMD ["nginx", "-g", "daemon off;"]


# Stage 1: Build (Alpine use karke size kam kiya hai)
# FROM node:18-alpine AS build
# WORKDIR /app

# # Dependency files pehle copy karein (Layer Caching optimize karne ke liye)
# COPY package*.json ./
# RUN npm ci --quiet  
# # 'npm i' se behtar 'npm ci' hai CI environments ke liye

# # Baaki source code copy karein aur build karein
# COPY . .
# RUN npm run build

# # Stage 2: Production (Unprivileged/Lightweight)
# FROM nginx:alpine
# WORKDIR /usr/share/nginx/html

# # Default files delete karein aur build artifacts copy karein
# RUN rm -rf ./*
# COPY --from=build /app/dist .

# # Security: Nginx ko non-root user se chalana best practice hai
# # Note: Standard Nginx 80 port use karta hai jiske liye root chahiye hota hai. 
# # Agar aapko high security chahiye toh custom nginx.conf ke saath 8080 use karein.

# EXPOSE 80
# CMD ["nginx", "-g", "daemon off;"]


FROM node:18-alpine

# Create app directory
WORKDIR /app

# Copy package files
COPY package*.json ./

# Install dependencies
RUN npm install

# Copy source code
COPY . .

# Expose React default port
EXPOSE 3000

# Start React app
CMD ["npm", "start"]