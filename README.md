# Akscluster
NGINX Deployment on Azure Kubernetes Service (AKS)
This repository demonstrates how to deploy NGINX on Azure Kubernetes Service (AKS) using Kubernetes.

Project Overview
This project involves setting up an Azure Kubernetes Service (AKS) cluster, deploying NGINX on the cluster, and exposing it via a LoadBalancer. The goal is to gain hands-on experience with AKS, Kubernetes, and the deployment process in the cloud.

Technologies Used
Azure Kubernetes Service (AKS)

Kubernetes

NGINX

kubectl

Azure CLI

Setup and Deployment
Prerequisites
An Azure account.

Azure CLI installed on your machine.

kubectl installed on your machine.

Access to Azure Kubernetes Cluster (ensure your Azure CLI is configured properly).

Steps to Deploy NGINX on AKS
Create an AKS Cluster:
First, create an Azure Kubernetes cluster by running the following command:

bash
Copy
Edit
az aks create --resource-group <Resource-Group-Name> --name <Cluster-Name> --node-count 3 --enable-addons monitoring --generate-ssh-keys
Get Credentials for the AKS Cluster:
Once the AKS cluster is created, use the following command to configure kubectl to use your new cluster:

bash
Copy
Edit
az aks get-credentials --resource-group <Resource-Group-Name> --name <Cluster-Name>
Deploy NGINX on AKS:
Create a deployment YAML file for NGINX. Here’s an example (nginx-deployment.yaml):

yaml
Copy
Edit
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-deployment
spec:
  replicas: 1
  selector:
    matchLabels:
      app: nginx
  template:
    metadata:
      labels:
        app: nginx
    spec:
      containers:
      - name: nginx
        image: nginx
        ports:
        - containerPort: 80
Apply the deployment by running:

bash
Copy
Edit
kubectl apply -f nginx-deployment.yaml
Expose the NGINX Deployment via LoadBalancer:

Now, expose the NGINX deployment using a LoadBalancer service:

bash
Copy
Edit
kubectl expose deployment nginx-deployment --type=LoadBalancer --name=nginx-service
Access the NGINX Web Server:
To get the external IP of the LoadBalancer, run the following command:

bash
Copy
Edit
kubectl get svc nginx-service
Once the external IP is provisioned, you can access your NGINX web server via the public IP, like so:

http
Copy
Edit
http://<External-IP>
Troubleshooting
Credentials Error: If you encounter an error with kubectl, ensure you have properly configured your Azure credentials by running az aks get-credentials.

Missing Pod Information: If your pods are not showing up, run kubectl get pods to verify the status of your deployment.

Project Files
nginx-deployment.yaml: YAML file for deploying NGINX on the cluster.

nginx-service.yaml: (Optional) YAML file for exposing the NGINX service with LoadBalancer.

License
This project is licensed under the MIT License – see the LICENSE file for details.

How to Contribute
Feel free to fork this project, make changes, and open a pull request if you have any improvements or suggestions. For any issues, please create an issue in the GitHub repository.
