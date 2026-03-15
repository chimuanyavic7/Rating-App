# ========================
# Stage 1: Build
# ========================
FROM node:20-alpine AS build

# Set working directory
WORKDIR /app


# Install dependencies efficiently
COPY package.json package-lock.json ./
RUN npm ci 

# Copy source code
COPY . .

# Pass environment variable at build time
ARG VITE_API_URL
ENV VITE_API_URL=$VITE_API_URL


# Build the React app with VITE_API_URL baked in
RUN npm run build

# ========================
# Stage 2: Production
# ========================
FROM nginx:alpine AS production

# Copy built files from the build stage
COPY --from=build /app/dist /usr/share/nginx/html

# Optional: copy custom Nginx config
# COPY nginx.conf /etc/nginx/conf.d/default.conf

# Expose port 80
EXPOSE 80

# Start Nginx
CMD ["nginx", "-g", "daemon off;"]
