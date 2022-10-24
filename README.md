# Create K8s Cluster, Deploy containerized stateless applications using K8s manifests

# Step 1: Create Cluster
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
docker build -t < name > -f <name of dockerfile> .
aws ecr create-repository --repository-name < name of repo > --image-scanning-configuration scanOnPush=true
```
# Step 3: My Deployment Sequence
```
1. Create SQL Pod in designated namespace
2. Create SQL Service (ClusterIP)
3. Create APP Service (NodePort)
4. Create APP Pod 
5. Create SQL Replica Set
6. Create APP Replica Set
7. Create SQL Deployment
8. Create APP Deployment
```
# Extras:

## Command to create the files from Step 3
```
kubectl create -f < filename.yaml >
```
## Command to do Port Forward
```
kubectl port-forward < name of pod > 8081:8080 -n < namespace the pod is deployed in >
```
## Verify the Running Status of Pods
```
kubectl get pods (For Default Namespace)
kubectl get pods -n < namespace pod is deployed in >
```
## Verify Everything that is Running
```
kubectl get all (For Default Namespace)
kubectl get all -n < namespace >
```
### Correct Git Push Sequence
```
git config --global user.name "YOUR_USER_NAME"
git config --global user.email YOUR_EMAIL_ADDRESS
git init
git add . or git add <filename>
git commit -m "MESSAGE"
git add
git remote add origin YOUR_GITREPO_HTTPS_ADDRESS
git push -u origin main
```
