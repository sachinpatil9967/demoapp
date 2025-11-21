# Multi-stage build for MERN application
# Stage 1: Build the React client
FROM node:18-alpine AS client-builder

WORKDIR /app/client

COPY client/package*.json ./

RUN npm install

COPY client/ ./

RUN npm run build

# Stage 2: Create the server image with built client
FROM node:18-alpine

WORKDIR /app

# Copy server package files
COPY server/package*.json ./server/

# Install server dependencies
WORKDIR /app/server
RUN npm install --production

# Copy server source code
COPY server/ ./

# Copy built client from stage 1
COPY --from=client-builder /app/client/build /app/client/build

WORKDIR /app/server

# Expose port
EXPOSE 5000

# Start the server
CMD ["npm", "start"]
