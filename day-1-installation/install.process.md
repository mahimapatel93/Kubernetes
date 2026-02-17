Setup Kubernetes on Amazon EKS

You can follow the same procedure in the official AWS document:
Getting started with Amazon EKS – eksctl

Pre-requisites

An EC2 Instance

AWS EKS Setup
1. Setup kubectl
a. Download kubectl (Version 1.20)
curl -o kubectl https://amazon-eks.s3.us-west-2.amazonaws.com/1.19.6/2021-01-05/bin/linux/amd64/kubectl

b. Grant execution permission
chmod +x kubectl

c. Move kubectl to /usr/local/bin
sudo mv kubectl /usr/local/bin/

d. Verify installation
kubectl version --short --client

2. Setup eksctl
a. Download and extract latest release
curl --silent --location "https://github.com/weaveworks/eksctl/releases/latest/download/eksctl_$(uname -s)_amd64.tar.gz" | tar xz -C /tmp

b. Move binary to /usr/local/bin
sudo mv /tmp/eksctl /usr/local/bin/

c. Verify installation
eksctl version

3. Create IAM Role and Attach to EC2 Instance

Note: Create IAM user with programmatic access if your bootstrap system is outside AWS.

IAM user should have access to:

IAM

EC2

VPC

CloudFormation

Attach this IAM role to your EC2 instance.

4. Create Your Cluster and Nodes
Generic Command
eksctl create cluster \
  --name cluster-name \
  --region region-name \
  --node-type instance-type \
  --nodes-min 2 \
  --nodes-max 2 \
  --zones <AZ-1>,<AZ-2>

Example
eksctl create cluster \
  --name naresh \
  --region us-east-1 \
  --node-type t2.small \
  --nodes-min 2 \
  --nodes-max 2

5. Delete the EKS Cluster
eksctl delete cluster --name naresh --region ap-south-1

6. Validate Your Cluster

Check nodes:

kubectl get nodes


Create a test pod:

kubectl run test-pod --image=nginx


Check pods:

kubectl get pods

Docker and Minikube Install Process
EC2 Instance Requirement

Choose:

t2.medium  (2 CPU, 2GB RAM required)

Install Docker
Install Docker
sudo dnf install docker -y

Start Docker Service
sudo systemctl start docker.service

Enable Docker Service
sudo systemctl enable docker.service

Add ec2-user to Docker Group
sudo usermod -aG docker ec2-user

Apply group changes immediately
newgrp docker

Install Minikube
Download Minikube
curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64

Install Minikube
sudo install minikube-linux-amd64 /usr/local/bin/minikube

Start Minikube
minikube start

Check Status
minikube status

Install kubectl (General Kubernetes Setup)
Download kubectl
curl -LO https://storage.googleapis.com/kubernetes-release/release/$(curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt)/bin/linux/amd64/kubectl

Make kubectl executable
chmod +x kubectl

Move to /usr/local/bin
sudo mv kubectl /usr/local/bin/kubectl
