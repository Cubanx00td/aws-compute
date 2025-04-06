# Deploying a Static Web App with Docker on AWS Elastic Beanstalk

## 🌍 Overview
This project demonstrates how to deploy a simple static web application using Docker on AWS Elastic Beanstalk. AWS Elastic Beanstalk is a Platform as a Service (PaaS) that lets you deploy and manage applications in the AWS Cloud without worrying about the infrastructure that runs those applications.

## 🏗️ Architecture
The project includes:
* A static HTML page served using NGINX
* A Dockerfile that builds the application container
* Deployment to AWS Elastic Beanstalk using the AWS Management Console

## 🥪 Prerequisites
Before you begin, make sure you have:
* An AWS Account
* An IAM user with appropriate permissions for Elastic Beanstalk
* Docker installed on your local machine

## 🧱 Setup Instructions

### Step 1: Project Structure
Create a directory called `Compute` and add the following two files:

```
Compute/
├── Dockerfile
└── index.html
```

### Step 2: Create index.html
Add a basic HTML file named `index.html`. Example:

```html
<!DOCTYPE html>
<html>
<head>
    <title>Dockerized Web App</title>
</head>
<body>
    <h1>Welcome to my Dockerized Web App on AWS Elastic Beanstalk!</h1>
</body>
</html>
```

### Step 3: Create Dockerfile
In the same directory, add a `Dockerfile` with the following content:

```dockerfile
FROM nginx:latest
COPY index.html /usr/share/nginx/html/index.html
PORT 80
```

This Dockerfile uses the official NGINX image and serves your HTML file.

### Step 4: Create a ZIP Archive
Compress both the `Dockerfile` and `index.html` into a single ZIP file.

```
zip -r application.zip Dockerfile index.html
```

### Step 5: Deploy to Elastic Beanstalk using AWS Console

1. **Open the Elastic Beanstalk Console**
   * Sign in to the AWS Management Console
   * Navigate to the Elastic Beanstalk service

2. **Create a New Application**
   * Click on "Create Application"
   * Enter "nextwork-eb-docker" as the application name
   * Click "Create"

3. **Create a New Environment**
   * Within your application, click "Create a new environment"
   * Select "Web server environment"
   * Environment name: "nextwork-env"
   * Domain: Accept the default or customize
   * Platform: Select "Docker" from the platform dropdown
   * Application code: Choose "Upload your code"
   * Upload the ZIP file you created earlier
   * Click "Create environment"

4. **Monitor Deployment**
   * Elastic Beanstalk will create your environment and deploy your application
   * This process typically takes 5-10 minutes
   * You can monitor the events in real-time on the environment dashboard

5. **Access Your Application**
   * Once deployment is complete, click on the URL provided at the top of the environment dashboard
   * Your NGINX-served static page should load in the browser

## 🛠️ Configuration Details
* **Platform:** Docker running on 64bit Amazon Linux
* **Container:** NGINX serving static content
* **Deployment Method:** AWS Elastic Beanstalk via AWS Management Console
* **App Directory:** `Compute`

## 🚨 Troubleshooting

### Common Issues
* **Docker Build Fails**
   * Double-check your `Dockerfile` for syntax errors or incorrect paths
   * Ensure all necessary files are included in your ZIP archive
* **App Doesn't Load**
   * Ensure `index.html` is named correctly and placed in the correct directory
   * Check NGINX file path in the Dockerfile
* **Permission Errors**
   * Confirm your IAM user has Elastic Beanstalk, EC2, S3, and IAM permissions
* **Deployment Hangs or Fails**
   * Check the environment's "Events" tab in the Elastic Beanstalk console
   * Review the logs available in the "Logs" section of your environment

## 🔗 Additional Resources
* [AWS Elastic Beanstalk Documentation](https://docs.aws.amazon.com/elasticbeanstalk/)
* [Docker Documentation](https://docs.docker.com/)
* [NGINX Documentation](https://nginx.org/en/docs/)
* [AWS Elastic Beanstalk Docker Platform](https://docs.aws.amazon.com/elasticbeanstalk/latest/dg/create_deploy_docker.html)
