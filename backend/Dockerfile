# Use Node.js 18 base image
FROM node:18

# Create and set working directory
WORKDIR /app

# Copy package.json and package-lock.json
COPY package*.json ./

# Install backend dependencies
RUN npm install

# Copy backend source code
COPY . .

# Expose port 8080 as backend listens here
EXPOSE 8080

# Start backend server
CMD ["node", "server.js"]
