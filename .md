## Deploying a HTML Website with Docker and Nginx

This guide walks you through the complete workflow of deploying a simple HTML project inside a Docker container using Nginx. You'll learn how to run the application, make updates, and release new versions using Docker images.

---

### Prerequisite: Install Docker

Make sure Docker is installed on your system. To install on Ubuntu:

```bash
sudo apt update
sudo apt install docker.io -y
sudo systemctl start docker
sudo systemctl enable docker
```


#### Step 1: Create a Simple HTML Project

Start by creating a folder for your project:

```bash
mkdir html-docker-app
cd html-docker-app

```

Inside this folder, create a file named index.html with the following content:
```
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <title>Welcome</title>
</head>
<body>
  <h1>Hello from Version 1</h1>
</body>
</html>
```
#### Step 2: Dockerize the Application

Now, create a Dockerfile to serve this HTML using Nginx:

```# Use the official Nginx image

FROM nginx:alpine

# Copy HTML file to the Nginx default directory
COPY index.html /usr/share/nginx/html/index.html
```

Build the Docker image:
```
docker build -t html-app:v1 .
```

#### Step 3: Run the Container with Nginx
Now run the container:
```
docker run -d -p 8080:80 --name html-app-container html-app:v1
```
#### Step 4: Access the Application on Port 8080
Open your browser and go to:

```
http://localhost:8080
```
You should see:
```
Hello from Version 1
```
#### Step 5: Update Website for Version 2
Make changes to index.html :
```
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <title>Docker PostgreSQL Guide</title>
</head>
<body>
  <h1>Learning Docker: Accessing PostgreSQL, Exporting & Importing Data</h1>
  <p>This guide helps early learners understand PostgreSQL inside Docker containers — from setup to backup.</p>
  <!-- Add more steps and commands as needed -->
</body>
</html>
```
Now rebuild the Docker image with a new version tag:
```
docker build -t html-app:v2 .
```
Stop and remove the previous container:
```
docker stop html-app-container
docker rm html-app-container
```
Run the new version:
```bash
docker run -d -p 8080:80 --name html-app-container html-app:v2
```

Visit:

```arduino

http://localhost:8080
```
---
Now you're ready to deploy, update, and version your static sites easily!
