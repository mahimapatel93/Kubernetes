# 🚀 Setup Kubernetes on Amazon EKS (EKS + Docker + Minikube)

You can follow the official AWS documentation here:  
https://docs.aws.amazon.com/eks/latest/userguide/getting-started-eksctl.html

---

## 📌 Pre-requisites

- An EC2 Instance
- IAM Role attached to EC2 with permissions:
  - IAM
  - EC2
  - VPC
  - CloudFormation

> Note: If your bootstrap system is outside AWS, create an IAM user with programmatic access.

---

# ☁️ AWS EKS Setup

---

## 1️⃣ Install kubectl (For EKS)

### Download kubectl
```sh
curl -o kubectl https://amazon-eks.s3.us-west-2.amazonaws.com/1.19.6/2021-01-05/bin/linux/amd64/kubectl
Make it executable
chmod +x kubectl
Move to system path
sudo mv kubectl /usr/local/bin/
Verify installation
kubectl version --short --client
2️⃣ Install eksctl
Download latest release
curl --silent --location \
"https://github.com/weaveworks/eksctl/releases/latest/download/eksctl_$(uname -s)_amd64.tar.gz" \
| tar xz -C /tmp
Move binary
sudo mv /tmp/eksctl /usr/local/bin/
Verify installation
eksctl version
3️⃣ Create IAM Role
Attach an IAM Role to your EC2 instance with the following permissions:

IAM

EC2

VPC

CloudFormation

4️⃣ Create EKS Cluster
Generic Command
eksctl create cluster \
  --name <cluster-name> \
  --region <region-name> \
  --node-type <instance-type> \
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
Cluster creation takes approximately 10–15 minutes.

5️⃣ Validate Cluster
Check Nodes
kubectl get nodes
Create Test Pod
kubectl run test-pod --image=nginx
Check Pods
kubectl get pods
6️⃣ Delete EKS Cluster
eksctl delete cluster --name naresh --region ap-south-1
🐳 Docker + Minikube Setup (Local Kubernetes)
EC2 Instance Requirement
t2.medium  (Minimum 2 CPU, 2GB RAM required)
🐳 Install Docker
Install Docker
sudo dnf install docker -y
Start Docker Service
sudo systemctl start docker.service
Enable Docker Service
sudo systemctl enable docker.service
Add ec2-user to Docker Group
sudo usermod -aG docker ec2-user
Apply Group Changes
newgrp docker
Verify Docker
docker --version
docker ps
🚀 Install Minikube
Download Minikube
curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64
Install Minikube
sudo install minikube-linux-amd64 /usr/local/bin/minikube
Start Minikube
minikube start
Check Status
minikube status
📦 Install kubectl (General Kubernetes Setup)
Download kubectl
curl -LO https://storage.googleapis.com/kubernetes-release/release/$(curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt)/bin/linux/amd64/kubectl
Make Executable
chmod +x kubectl
Move to Path
sudo mv kubectl /usr/local/bin/kubectl
Verify
kubectl version --client
✅ Final Verification Commands
kubectl get nodes
kubectl get pods
minikube status
docker ps
