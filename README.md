# Deveops_EthanAnnaelle
This work has been made by Ethan Berneau and Annaëlle Houzelle, ING4, GR01, Cybersécurity-INTER

# Introduction

# Prerequisites
To run this project, you will need all these softwares and app :

- [Git](https://git-scm.com/)
- [NodeJS](https://nodejs.org/en)
- [npm](https://www.npmjs.com/)
- [Redis](https://redis.io/)
- [Vagrant](https://www.vagrantup.com/)
- [VirtualBox](https://www.virtualbox.org/)
- [Docker](https://www.docker.com/)
- [Docker Compose](https://docs.docker.com/compose/)
- [Minikube](https://minikube.sigs.k8s.io/docs/start/)
- [kubectl](https://kubernetes.io/docs/tasks/tools/)

Except the first part, all this tp is working on windows and not on linux.

# 1.Creation of the web application

## Testing :
npm start

# 2.CI/CD Pipeline
This repository includes a CI/CD pipeline implemented using GitHub Actions. The pipeline is triggered on every push or accepted pull request and is composed of two distinct jobs:

1. **Continuous Integration (CI)**
2. **Continuous Deployment (CD)**

Following best practices, these jobs are separated to ensure clarity and modularity, even though they could theoretically be combined into one. Each job is executed on a clean GitHub-hosted runner to mimic a production environment and ensure reproducibility.

---
## **Continuous Integration (CI)**

The Continuous Integration job verifies that any new code (pushed or merged) integrates seamlessly with the existing codebase. This is achieved through a series of automated tests.
![image](https://github.com/user-attachments/assets/3692b4b4-fbd2-427b-aaad-ab2e5c202ceb)

## **Continuous Deployment (CD)**

The Continuous Deployment job deploys the application to Netlify. By automating this process, we ensure that every successful change is live on the deployment platform without manual intervention.
![image](https://github.com/user-attachments/assets/a3222e0a-130b-4e28-bf29-6a48dc28dc20)

#### Deploy to Netlify
```bash
npm install -g netlify-cli
netlify deploy --dir=src --prod
```
Relies on environment variables for authentication (`NETLIFY_AUTH_TOKEN` and `NETLIFY_SITE_ID`).

The deployment job only runs if the CI job passes successfully. This prevents buggy code from being deployed to production.

![netlify image](https://github.com/user-attachments/assets/7708d00e-ce60-48dc-85aa-c3be9d42c7f1)

---

## **Pipeline Overview**

When the CI/CD pipeline is triggered, the following workflow is executed:

1. **CI Job**:
   - Installs Node.js and Redis.
   - Runs the test suite.
   - Builds and pushes the Docker image to DockerHub.

2. **CD Job**:
   - Builds the application.
   - Deploys the application to Netlify.

If all steps complete successfully, the application is live on Netlify, and the Docker image is up to date on DockerHub.

---
Result: 
![image](https://github.com/user-attachments/assets/908aa224-339d-4683-86f0-0b3dd1a94460)

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

To check if the deployment works well
```bash
kubectl get pods
```
<img width="554" alt="image" src="https://github.com/user-attachments/assets/93d3c5cc-5c47-464b-a9c1-0bd7721d2174" />

```bash
kubectl logs nodejs-app-deployment-69cb8f9d85-tb2cg
```
<img width="808" alt="image" src="https://github.com/user-attachments/assets/52b889ab-7cac-4dcf-b4ea-7f75b563faa2" />

```bash
kubectl logs redis-deployment-74dd9754c8-s8pwv
```
<img width="917" alt="image" src="https://github.com/user-attachments/assets/a9c4ead3-40e1-466e-be5d-8a3d5862f89b" />

To open the Nodejs pod on port 3000 :
```bash
minikube service nodejs-app-service
```
<img width="959" alt="image" src="https://github.com/user-attachments/assets/795637d2-180a-4463-b7da-a5988effb2a3" />
<img width="959" alt="image" src="https://github.com/user-attachments/assets/1e8a3a03-fc88-41bc-84b0-4ca2fde3473d" />

Finally, if you want to delete the deployment and the application, you only have to :
```bash
kubectl delete deployment redis-deployment
kubectl delete deployment nodejs-app-deployment
kubectl delete service nodejs-app-service
kubectl delete service redis-service
kubectl delete pvc redis-pvc
kubectl delete pv redis-pv
```

# 7.Istio
After the installation of isio, we go in its repertory 
```bash
cd istio
```

Firt we have to delete minikube from istio
```bash
minikube delete
```
Then, give more ressources to istio, and run :
```bash
minikube start --cpus 6 --memory 8192
```
<img width="853" alt="image" src="https://github.com/user-attachments/assets/776402a9-1b2e-4ea6-b249-3c68ebc7503b" />

Then we had C:\Users\Annaëlle\Desktop\ING4\DeveOps - BAUM Stéphan\Deveops_EthanAnnaelle\istio\bin
to the path of windows, and we execute 
```bash
istioctl version
```
and 
```bash
istioctl
```
<img width="959" alt="image" src="https://github.com/user-attachments/assets/f38b2d81-d3e8-467d-a4e6-e2c529d3a122" />

Then we execute :
```bash
kubectl get ns
kubectl get pods
```
<img width="860" alt="image" src="https://github.com/user-attachments/assets/3aeff193-7ec1-4f88-a419-49446ce09568" />

Now we install istio :
```bash
istioctl install
```
<img width="764" alt="image" src="https://github.com/user-attachments/assets/b09097db-fd6d-441d-b24f-5d96ea6569c7" />
And we check if the 2 pods are well created :
```bash
kubectl get ns
kubectl get pod -n istio-system
```
<img width="799" alt="image" src="https://github.com/user-attachments/assets/62fbf54f-ea76-493b-81d9-1eee70146ebc" />

We create a namespace :
```bash
kubectl label namespace default istio-injection=enabled
```
and check if it works 
```bash
kubectl get ns default --show-labels
```
<img width="844" alt="image" src="https://github.com/user-attachments/assets/b19b3506-ac47-4800-a166-df94750c7563" />

We now have to apply the manifest we create :
```bash
kubectl apply -f manifest.yaml
```
<img width="799" alt="image" src="https://github.com/user-attachments/assets/648ce5e9-590d-404c-8b95-1cbed59e7f50" />

Check the pods :
```bash
kubectl get pods
```
<img width="708" alt="image" src="https://github.com/user-attachments/assets/7b84bdeb-9080-4bfb-953a-7080dbb993dc" />

## Install Addon
Now let's install addon to have all the functionnalities 
```bash
kubectl apply -f addons/
```
<img width="761" alt="image" src="https://github.com/user-attachments/assets/f8390462-8f74-4401-b8b5-a95db326d255" />

And to check the pods :
```bash
kubectl get pods -n istio-system
```
<img width="831" alt="image" src="https://github.com/user-attachments/assets/f9339e56-7375-4c4f-a285-94e56e518682" />

To check all the services previously created :
```bash
kubectl get services -n istio-system
```
<img width="900" alt="image" src="https://github.com/user-attachments/assets/07786935-dfc0-46f0-bbc7-66dc13878861" />

We can test the kialy dashboard :
```dash
kubectl port-forward svc/kiali -n istio-system 20001
```
<img width="951" alt="image" src="https://github.com/user-attachments/assets/31165ee6-9b03-4d1b-90d5-89be9208d192" />

<img width="959" alt="image" src="https://github.com/user-attachments/assets/17d48f38-179b-4ed1-a319-c3b61f67bbba" />

We can also see the pods managing by isio :
<img width="959" alt="image" src="https://github.com/user-attachments/assets/6113048e-f7e0-4649-92bc-411f5e2c584d" />

To check if all the services are working well :
```bash
kubectl get services -n istio-system
```
<img width="865" alt="image" src="https://github.com/user-attachments/assets/5033dd3e-fbac-4ee6-b62a-03fe870aa059" />






