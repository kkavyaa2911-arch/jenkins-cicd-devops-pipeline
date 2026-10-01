# Jenkins CI/CD DevOps Pipeline

A hands-on CI/CD project that automates testing, Docker image creation, deployment, and application health verification using Jenkins.

## Architecture

Developer Push
↓
GitHub Repository
↓
GitHub Webhook
↓
Jenkins Pipeline
↓
Automated Testing (Pytest)
↓
Docker Image Build
↓
Docker Container Deployment
↓
Application Health Check

## Technologies Used

- Jenkins
- Git & GitHub
- Docker
- Python
- Flask
- Pytest
- GitHub Webhooks
- ngrok

## Pipeline Stages

### 1. Checkout
Jenkins retrieves the latest source code from the GitHub repository.

### 2. Install Dependencies
A Python virtual environment is created and application dependencies are installed.

### 3. Automated Testing
Pytest automatically executes the application's test cases before deployment.

### 4. Docker Build
Jenkins builds a Docker image and tags it using the Jenkins build number.

Example:

```bash
docker build -t jenkins-flask-app:${BUILD_NUMBER} .
