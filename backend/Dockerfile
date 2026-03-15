# Stage 1: Build
FROM node:20-alpine AS build

# Set working directory
WORKDIR /app

# Copy package files first (for caching)
COPY package.json package-lock.json ./

# Install dependencies
RUN npm ci --only=production

# Copy application source code
COPY . .

# Stage 2: Production
FROM node:20-alpine AS production

WORKDIR /app

# Copy only dependencies from build stage
COPY --from=build /app/node_modules ./node_modules

# Copy application source code
COPY --from=build /app ./

# Expose the port your app uses
EXPOSE 5000

# Set default command to run your app
CMD ["node", "index.js"]
