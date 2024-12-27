# Deveops_EthanAnnaelle

# Introduction

# Prerequisites

# 1.Creation of the web application

## Testing :
npm start

# 2.CI/CD Pipeline

# 3.Vagrant

# 4.Docker
To make the application compatible with environments like Docker Compose or Kubernetes, the first step is to create a Docker image of the application. This is achieved by defining a Dockerfile, which specifies the steps for building the image.

It's important to exclude unnecessary files and folders, that are not required in the image. To handle this, a .dockerignore file is used to specify which files and directories should be excluded during the build process.

## Build of the image
Before proceeding with the instructions, ensure that Docker is installed and running on your system.

First you have to go in the userapi folde :
```bash
docker compose up
```
Then you can execute this command :
```bash
docker build -t userapi/deveops_ethanannaelle .
```
## Publication of the image
After creating a [DockerHub](https://hub.docker.com/) account, the image will be online

```bash
docker tag userapi $YOUR_USERNAME/userapi-devops:latest
docker login
docker push $YOUR_USERNAME/userapi-devops:latest
```

<img width="959" alt="image" src="https://github.com/user-attachments/assets/ddd75e1d-8cdd-43ff-b62a-b7888a914b87" />


## 5.Docker Compose

## 6.Kubernetes

## 7.Istio

