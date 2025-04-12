# ------------------- Stage 1: Build Stage ------------------------------
FROM node:21 AS backend-builder

# Set the working directory to /app
WORKDIR /app

# Copy the package.json and package-lock.json for dependency installation
COPY package*.json ./

# Install dependencies
RUN npm install

# Copy the rest of the application code
COPY . .

# ------------------- Stage 2: Final Stage ------------------------------
FROM node:21-slim

# Set the working directory to /app
WORKDIR /app

# Copy built assets and dependencies from backend-builder stage
COPY --from=backend-builder /app .

# Check if .env.docker exists, if not fall back to .env.sample
COPY .env.docker .env.local || COPY .env.sample .env.local

# Expose port for the backend application
EXPOSE 5173

# Define the default command to run the application in development mode
CMD ["npm", "run", "dev", "--", "--host"]
