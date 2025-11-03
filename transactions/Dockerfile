# Use a stable Node base image (not Alpine)
FROM node:18-bullseye

# Set working directory
WORKDIR /app

# Install system dependencies
RUN apt-get update && apt-get install -y \
    ca-certificates \
    curl \
    gnupg \
    --no-install-recommends && \
    update-ca-certificates && \
    rm -rf /var/lib/apt/lists/*

# Copy package.json from src folder
COPY src/package*.json ./src/

# Change working directory so npm install runs where package.json is
WORKDIR /app/src

# Fix npm SSL and install dependencies
RUN npm config set strict-ssl false && \
    npm config set registry https://registry.npmjs.org/ && \
    npm install

# Copy the rest of the app
COPY . .

# Expose the app port
EXPOSE 4000

# Start the app
CMD ["node", "app.js"]