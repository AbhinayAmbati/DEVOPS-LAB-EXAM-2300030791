# ---- Stage 1: Build ----
FROM node:20-alpine AS build
WORKDIR /app

# Copy dependency definitions
COPY package*.json ./

# Install dependencies
RUN npm ci

# Copy the rest of your app
COPY . .

# Ensure vite binary is executable (after copy)
RUN chmod +x node_modules/.bin/vite

# Run build
RUN npm run build

# ---- Stage 2: Serve ----
FROM nginx:alpine

# Copy build output to nginx html directory
COPY --from=build /app/dist /usr/share/nginx/html

EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]
