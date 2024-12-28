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

## Test of the image
To test the image you enter thic command :
``` bash
docker run -p 4000:4000 -d deveops_ethanannaelle/userapi-devops:latest
```
that allows you to see your website on the port 3000 :
<img width="959" alt="image" src="https://github.com/user-attachments/assets/90d93cbc-0777-4e53-940a-ddbd20838f12" />

# 5.Docker Compose

Execute :
```bash
docker compose up
```
<img width="784" alt="image" src="https://github.com/user-attachments/assets/0dba103f-cf93-40b2-b6e5-7ad8c8809dfd" />

To stop it :
```bash
docker compose down
```
<img width="785" alt="image" src="https://github.com/user-attachments/assets/bbc5a325-6771-4e7b-b84c-650d7b80356f" />



# 6.Kubernetes

# 7.Istio

