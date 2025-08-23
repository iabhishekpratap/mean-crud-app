# Use Node.js 18 base image
FROM node:18

# Create and set working directory
WORKDIR /app

# Copy package.json and package-lock.json
COPY package*.json ./

# Install frontend dependencies
RUN npm install

# Copy frontend source code
COPY . .

# Expose port 8081 (match your ng serve port)
EXPOSE 8081

# Start Angular dev server on port 8081, listen on all interfaces
CMD ["npx", "ng", "serve", "--host", "0.0.0.0", "--port", "8081"]
