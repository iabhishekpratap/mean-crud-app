# MEAN Stack Application Deployment with Jenkins CI/CD

## 📋 Project Overview

This project involves containerizing and deploying a full-stack MEAN (MongoDB, Express.js, Angular, Node.js) application using Docker, Docker Compose, and implementing a CI/CD pipeline with Jenkins.

## 📁 Repository Structure

```
MEAN-CRUD-APP/
├── backend/
│   ├── Dockerfile
│   └── (backend code)
│   └── testing-webhook-trigger        # test file for webhook backend
├── frontend/
│   ├── Dockerfile
│   └── (frontend code)
│   └── testing-webhook                # test file for webhook frontend
├── docker-compose.yml                 # Local development
├── docker-compose.server.yml          # Server/AWS deployment
├── Jenkinsfile.docker-push            # CI: Build and push images to DockerHub
├── Jenkinsfile.deploy-app             # CD: Deploy application on server 
├── nginx-default.conf                 # Nginx reverse proxy config file
├── README.md
└── testing-webhook                    # Test file for webhook (github)
```
## 🚀 Steps of Deployment on the AWS Server

## Provision EC2 Instance
Launch an EC2 instance in the default VPC. Configure the security group to allow inbound traffic on: 22 (SSH), 80 (HTTP), 443 (HTTPS), 8080 (Backend), 8081 (Application), and 9090 (Jenkins).

## Install Required Software
Install Jenkins, Docker, and Docker Compose on the EC2 server. Ensure Jenkins is accessible on port 9090.

## Configure Jenkins
Add necessary plugins in Jenkins. Configure GitHub credentials, Docker Hub credentials, and set up GitHub webhook integration.

## Set Up Docker and Docker Compose
Prepare the server with Docker and Docker Compose to manage the frontend, backend, and MongoDB containers.

## MongoDB with Persistent Storage
Run MongoDB in a Docker container using a persistent volume to ensure data is not lost during container updates or redeployment.

## Implement CI Pipeline
Use the first ```Jenkinsfile.docker-push``` to detect changes in the GitHub repository. If changes occur in the frontend or backend, build the respective container and push it to Docker Hub. After pushing, remove the local image to save space.

## Implement CD Pipeline
Use the second ```Jenkinsfile.deploy-app``` to monitor Docker Hub. When a new image is pushed (frontend or backend), the pipeline pulls the image, removes any existing containers, and deploys the updated version automatically.

## Configure Nginx for Reverse Proxy
Use ```nginx-default.conf``` to configure Nginx so the application is accessible directly via the server's IP on ports 80 and 443.

## Access the Application
After deployment, access the application through the EC2 public IP or domain. Jenkins remains on port 9090 for CI/CD management.

## 🚀 Local Testing

### 1. Clone the Repository
```bash
git clone <https://github.com/iabhishekpratap/mean-crud-app>
cd mean-crud-app
```

### 3. Build and Start the Application
```bash
# Build and start all containers in detached mode
docker-compose up --build -d
```

### 4. Verify Container Status
```bash
# Check if all containers are running successfully
docker-compose ps
```
### 5. Access the Application
Open your web browser and navigate to:
```
http://localhost:8081
```

### 6. Verify Application Functionality
Test the CRUD operations:

1. **Create** - Add new records through the UI
2. **Read** - View the list of existing records
3. **Update** - Modify existing records
4. **Delete** - Remove records from the system


To stop and remove all containers, networks, and volumes:
```bash
docker-compose down -v
```

## 📊 Screenshots

The repository includes screenshots of:

- Jenkins pipeline configuration and execution

![CI Pipeline Run](./screenshots%20/image_13.png)
![CI Pipeline Run](./screenshots%20/image_14.png)


- Webhook

![CI Pipeline Run](./screenshots%20/image_12.png)


- DockerHub

![CI Pipeline Run](./screenshots%20/image_2.png)
![CI Pipeline Run](./screenshots%20/image_3.png)


- DockerCompose

![CI Pipeline Run](./screenshots%20/image_5.png)


- AWS 

![CI Pipeline Run](./screenshots%20/image_4.png)


- Docker image build and push process

![CI Pipeline Run](./screenshots%20/image_10.png)
![CI Pipeline Run](./screenshots%20/image_11.png)


- Application deployment and working UI

![CI Pipeline Run](./screenshots%20/image_7.png)
![CI Pipeline Run](./screenshots%20/image_8.png)
![CI Pipeline Run](./screenshots%20/image_9.png)


- Nginx setup and infrastructure details

![CI Pipeline Run](./screenshots%20/image_1.png)
![CI Pipeline Run](./screenshots%20/image_6.png)


##  Support

For issues related to this deployment, please check:
1. Docker and Docker Compose documentation
2. Jenkins documentation
3. MongoDB documentation

This implementation provides a robust, containerized MEAN stack application with an automated Jenkins CI/CD pipeline for seamless deployments.