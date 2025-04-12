# ------------------- Stage 1: Build Stage ------------------------------
FROM node:21 AS frontend-builder

# Set the working directory
WORKDIR /app

# Copy dependency files
COPY package*.json ./

# Install dependencies
RUN npm install

# Copy the full frontend code
COPY . .

# ------------------- Stage 2: Final Stage ------------------------------
FROM node:21-slim

# Set the working directory
WORKDIR /app

# Copy built assets and dependencies from the frontend-builder stage
COPY --from=frontend-builder /app .

# Copy .env.docker if it exists, otherwise fallback to .env.sample
COPY .env.docker .env.local || COPY .env.sample .env.local

# Expose frontend port
EXPOSE 5173

# Start the frontend in dev mode
CMD ["npm", "run", "dev", "--", "--host"]

