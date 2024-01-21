## Deploying a Kubernetes-Based Application to DockerHub with MySQL and WordPress

![image](https://github.com/akpatiudo/word-express/assets/118566096/1c0f4ff8-77cb-49c8-a661-70c054e78236)

![image](https://github.com/akpatiudo/word-express/assets/118566096/f3b51652-9f25-49b3-a8a4-334a630040ab)

### Introduction

In today's dynamic IT landscape, deploying applications in a scalable and efficient manner is crucial. Kubernetes has emerged as a leading container orchestration platform, providing a robust framework for managing containerized applications. In this comprehensive guide, we will walk through the process of deploying a Kubernetes-based application to DockerHub using MySQL and WordPress as our example.

### Prerequisites

Before we begin, make sure you have the following prerequisites installed on your system:

Docker Desktop: Install Docker Desktop to deploy containerized applications locally.

kubectl: The Kubernetes command-line tool is necessary for interacting with Kubernetes clusters.

DockerHub Account: Sign up for a DockerHub account to store and share your Docker images.

### Step-by-Step Guide

Step 1:  Fork or Clone my Repository

Step 2: Deploy MySQL to AKS

Apply the MySQL secret:   kubectl apply -f mysql-secret.yaml  

### Encode a string to base64
this will extract the password string for  MYSQL_ROOT_PASSWORD in  mysql-secret.yaml file. if you are using bash terminal use :echo -n 'your-password' | base64
if you are using powershall use:

$base64EncodedString = [Convert]::ToBase64String([System.Text.Encoding]::UTF8.GetBytes("your-password"))

### Print the encoded string
Write-Host $base64EncodedString

put the generated password in your  mysql-secret.yaml file, MYSQL_ROOT_PASSWORD:<generated password>

Apply the MySQL deployment: kubectl apply -f mysql-deployment.yaml

Step 3: Deploy WordPress to AKS

Apply the WordPress deployment and service: kubectl kubectl apply -f wordpress-deployment.yaml
kubectl apply -f wordpress-service.yaml

A snippet of deployment code used

![image](https://github.com/akpatiudo/word-express/assets/118566096/78042669-762e-446e-9ba2-19070b5e566f)

Step 4: Monitor Deployment
Monitor the deployment status: kubectl get pods -w
kubectl get pod.
kubectl get all.
kubectl get svc wordpress-service --watch.
kubectl describe <pod name>

A snippet of monitoring  code used

![image](https://github.com/akpatiudo/word-express/assets/118566096/c28bd0e6-5826-45d0-bb1a-242c98597494)


Step 5: Access WordPress

Retrieve the WordPress service NodePort: kubectl get svc wordpress-service

Access WordPress in a web browser using the NodePort and external IP: http://<external-ip>:<node-port> 
the external-ip is your local ip address, if your mechain did not allocate to you you can use configip to access it, however, from the monitoring snippet, External-IP is pending, this often happen when using dockerhub, it takes time to allocate an Ip adress or might not allocate it
thus, you can use docker command to do this: <docker run -d -p 8080:80 --name my-wordpress wordpress:5.8.3-php7.4-apache > make sure is is the name of your image. 

### Conclusion
In conclusion, deploying a Kubernetes-based application to DockerHub with MySQL and WordPress involves several key steps. We started by building and pushing Docker images to DockerHub, followed by deploying MySQL and WordPress to AKS. Monitoring the deployment and accessing WordPress allowed us to validate our setup.

This guide provides a foundation for deploying other applications on Kubernetes, emphasizing the flexibility and scalability offered by container orchestration platforms. Feel free to explore further customization and optimization based on your specific use case.

License
This project is licensed under the MIT License.

With these step-by-step instructions, you can successfully deploy a Kubernetes-based application to DockerHub using MySQL and WordPress. Customize the guide according to your specific configurations and requirements.
