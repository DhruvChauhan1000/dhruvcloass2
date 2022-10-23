# Create K8s Cluster, Deploy containerized stateless applications using K8s manifests

# Step 1: Install Cluster with Kind and Kubectl (init_kind.sh)
```
chmod 777 init_kind.sh
#!/bin/bash
    set -ex
    sudo yum update -y
    sudo yum install docker -y
    sudo systemctl start docker
    sudo usermod -a -G docker ec2-user
    curl -sLo kind https://kind.sigs.k8s.io/dl/v0.11.0/kind-linux-amd64
    sudo install -o root -g root -m 0755 kind /usr/local/bin/kind
    rm -f ./kind
    curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"
    sudo install -o root -g root -m 0755 kubectl /usr/local/bin/kubectl
    rm -f ./kubectl
    kind create cluster --config kind.yaml
````
    
# Step 2: Build and Deploy images into ECR Repo
```
docker build -t <name> -f <name of dockerfile> .
aws ecr create-repository --repository-name <name of repo> --image-scanning-configuration scanOnPush=true
```
