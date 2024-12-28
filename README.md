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
Kubernetes, often abbreviated as K8s, is an open-source platform designed to automate the deployment, scaling, and management of containerized applications. It provides a framework to run distributed systems resiliently, ensuring the availability and scalability of applications.

## Installation of Kubernetes cluster in minikube
After the installation of minikube and kubectl on the computer, let's execute this command lines :

```bash
minikube start
```
<img width="857" alt="image" src="https://github.com/user-attachments/assets/5f0b5312-d920-4c17-a60b-9a5365374aa9" />

```bash
minikube status
```
<img width="670" alt="image" src="https://github.com/user-attachments/assets/f8313425-a4f2-4503-a842-b008bc068c67" />

Then, lets deploy the different needed tools to finally deploy the application :
```bash
kubectl apply -f redis-pv.yaml
```
<img width="800" alt="image" src="https://github.com/user-attachments/assets/4d6616b2-6c5f-448d-819a-a06fe057aca2" />

```bash
kubectl apply -f redis-pvc.yaml
```
<img width="795" alt="image" src="https://github.com/user-attachments/assets/379c0fbc-7338-4368-9778-85acd781467e" />

```bash
kubectl apply -f service.yaml
```
<img width="791" alt="image" src="https://github.com/user-attachments/assets/bea9025e-7121-4dfd-91d4-fdc0848e100b" />

```bash
kubectl apply -f deployment.yaml
```
<img width="816" alt="image" src="https://github.com/user-attachments/assets/4a5ef480-202c-4c55-b538-2d0ac075fbcf" />

# 7.Istio

