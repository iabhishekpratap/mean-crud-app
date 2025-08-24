# MEAN Stack Application Deployment with Jenkins CI/CD

## 📋 Project Overview

This project involves containerizing and deploying a full-stack MEAN (MongoDB, Express.js, Angular, Node.js) application using Docker, Docker Compose, and implementing a CI/CD pipeline with Jenkins.

## 🏗️ Architecture

The application consists of:
- **Frontend**: Angular application served by Nginx
- **Backend**: Node.js with Express.js API
- **Database**: MongoDB running in a Docker container
- **Reverse Proxy**: Nginx routing requests 
- **CI/CD**: Jenkins pipeline for automated build and deployment

## 📁 Repository Structure

```
├── backend/
│   └── Dockerfile
|    |__ testing-webhook-trigger 
├── frontend/
│   └── Dockerfile
|   |__ testing-webhook
|__ 
└── README.md
```

## 🚀 Quick Start

### Prerequisites

- Docker and Docker Compose installed on your Ubuntu VM
- Jenkins installed and configured on your Ubuntu VM
- Docker Hub account
- Ubuntu VM (AWS, Azure, or other cloud provider)

### Deployment Steps

1. **Clone the repository to your Ubuntu VM:**
   ```bash
   git clone <your-repository-url>
   cd mean-app
   ```

2. **Set up environment variables:**
   Create a `.env` file in the root directory with the following variables:
   ```
   MONGODB_URI=mongodb://mongodb:27017/mean-app
   DOCKERHUB_USERNAME=your-dockerhub-username
   DOCKERHUB_TOKEN=your-dockerhub-token
   ```

3. **Start the application with Docker Compose:**
   ```bash
   docker-compose up -d
   ```

4. **Access the application:**
   Open your browser and navigate to `http://your-vm-ip-address`

## 🔧 Jenkins CI/CD Pipeline

### Pipeline Configuration

The Jenkins pipeline is configured through a `Jenkinsfile` that defines the following stages:

1. **Checkout**: Pull the latest code from the repository
2. **Build Backend**: Build the Node.js backend Docker image
3. **Build Frontend**: Build the Angular frontend Docker image
4. **Push Images**: Push images to Docker Hub
5. **Deploy**: Deploy the application to the Ubuntu VM

### Jenkins Setup

1. Install Jenkins on your Ubuntu VM
2. Install required plugins:
   - Docker Pipeline
   - SSH Agent
   - Git
3. Configure credentials in Jenkins:
   - Docker Hub credentials
   - SSH credentials for deployment server
4. Create a new pipeline job and point it to the Jenkinsfile in your repository

### Automated Deployment

The pipeline automatically:
- Builds Docker images when changes are pushed to the repository
- Pushes images to Docker Hub
- Deploys the application to the production server
- Restarts containers with the updated images

## 🌐 Nginx Configuration

The Nginx reverse proxy is configured to:
- Serve the Angular frontend on the root path `/`
- Proxy API requests to the backend service at `/api`
- Make the application accessible on port 80

## 📊 Screenshots

The repository includes screenshots of:
- Jenkins pipeline configuration and execution
- Docker image build and push process
- Application deployment and working UI
- Nginx setup and infrastructure details

## 🛠️ Troubleshooting

### Common Issues

1. **Port conflicts**: Ensure ports 80, 3000, and 27017 are available
2. **Docker permissions**: Add your user to the docker group: `sudo usermod -aG docker $USER`
3. **Jenkins permissions**: Ensure Jenkins has permissions to run Docker commands
4. **MongoDB connection**: Verify the connection string and that MongoDB is running

### Useful Commands

```bash
# Check running containers
docker ps

# View logs for a specific container
docker logs <container_name>

# Restart services
docker-compose restart

# Rebuild and restart containers
docker-compose up -d --build

# View Jenkins logs
sudo tail -f /var/log/jenkins/jenkins.log
```

## 📝 Additional Notes

- The application runs on port 80 for HTTP access
- MongoDB data is persisted using Docker volumes
- Environment variables are used for configuration
- The Jenkins pipeline requires proper credential setup

## 📞 Support

For issues related to this deployment, please check:
1. Docker and Docker Compose documentation
2. Jenkins documentation
3. MongoDB documentation

---

This implementation provides a robust, containerized MEAN stack application with an automated Jenkins CI/CD pipeline for seamless deployments.