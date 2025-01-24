### Step-by-Step Guide for Blue-Green Deployment Using EKS

---

### 1) Create an EC2 Instance

- **Name**: Server
- **Operating System**: Ubuntu Server 24.04
- **Instance Type**: t2.medium
- **Security Group**: Primary-SG
- **EBS Volume**: 20 GB

---

### 2) SSH to Server (EC2)

- Update the repository:
  ```bash
  sudo apt update
  ```

---

### 3) Install the AWS CLI from Amazon Documentation

- **Create an IAM User**:
  - Copy the access key and secret key.

- **Configure AWS CLI**:
  ```bash
  aws configure
  ```
  - Provide the access key, secret key, and region when prompted.

---

### 4) Install Terraform for EKS Cluster Provisioning (IaC)

- Install Terraform:
  ```bash
  sudo snap install terraform --classic
  ```

- Clone the repository:
  ```bash
  git clone https://github.com/Sudoharry/Blue-Green-Deployment.git
  ```

---

### 5) Change Directory

- Navigate to the cluster directory:
  ```bash
  cd Blue-Green-Deployment
  cd Cluster
  ```

---

### 6) Provision the EKS Cluster

- **Note**: Change the region and update `variable.tf` with the correct secret key name.

- Initialize and apply Terraform:
  ```bash
  terraform init
  terraform plan
  terraform apply -auto-approve
  ```

---

### 7) Launch 3 EC2 Servers

- **EBS Volume**: 25 GB each
- **Instance Type**: t2.medium
- **Names**:
  1. Jenkins
  2. SonarQube
  3. Nexus
- **Security Group Ports**: 9000, 8081, 8080

---

### 8) Configure Jenkins Server

- SSH into the Jenkins server.
- Update the repository:
  ```bash
  sudo apt update
  ```
- Install Jenkins by following the [official Jenkins documentation](https://www.jenkins.io/doc/).

---

### 9) Configure Nexus Server

- SSH into the Nexus server.
- Update the repository:
  ```bash
  sudo apt update
  ```
- Install Docker:
  ```bash
  sudo apt install docker.io -y
  sudo usermod -aG docker ubuntu
  newgrp docker
  ```
- Run the Nexus container:
  ```bash
  docker run -d -p 8081:8081 sonatype/nexus3
  ```
- Verify if Docker is running:
  ```bash
  docker ps
  ```

---

### 10) Configure SonarQube Server

- SSH into the SonarQube server.
- Update the repository:
  ```bash
  sudo apt update
  ```
- Install Docker:
  ```bash
  sudo apt install docker.io -y
  sudo usermod -aG docker ubuntu
  ```
- Run the SonarQube container:
  ```bash
  docker run -d -p 9000:9000 sonarqube:lts-community
  ```

---

### 11) Retrieve Nexus Password

- Get the password for Nexus:
  ```bash
  docker exec -it <container_id> /bin/bash
  cd sonatype-work
  cd nexus3
  cat admin.password
  ```
- Use this password to log in to the Nexus server.

---

### 12) Install Docker on Jenkins Server

- Install Docker:
  ```bash
  sudo apt install docker.io -y
  ```
- Add Jenkins to the Docker group:
  ```bash
  sudo usermod -aG docker jenkins
  sudo systemctl restart jenkins
  ```

---

### 13) Install Trivy on Jenkins Server

- Follow the [Trivy installation guide](https://aquasecurity.github.io/trivy/) for Ubuntu.

---

### 14) Install kubectl on Jenkins Server

- Install kubectl:
  ```bash
  sudo snap install kubectl --classic
  ```

---

### 15) Install kubectl on the Server Instance

- Install kubectl:
  ```bash
  sudo snap install kubectl --classic
  ```

---

### 16) Update kubeconfig for EKS

- Update the kubeconfig to connect to the EKS cluster:
  ```bash
  aws eks --region ap-south-1 update-kubeconfig --name devopsshack-cluster
  ```

