### 1) Create a EC2 instance
      - Name: Server
      - Ubuntu Server 24.04
      - Instance Type: t2.medium
      - Security Group: Primary-SG
      - EBS Volume: 20 GB
      
### 2) SSH to Server (EC2)
      - Update repo: sudo apt update

### 3) Install the AWS CLI from Amazon documentation  
      - Create IAM user and copy the access key and secret key
      - Configure the AWS using: 
           Command: ```aws configure```
      - configured the access key, secret key and region

### 4) Install Terrform for EKS cluster provision (IaC)
      - Install: sudo snap install terraform --classic
      - Clone the repository: 
      ```git clone https://github.com/Sudoharry/Blue-Green-Deployment.git```

### 5) Change directory
      ``` cd Blue-Green-Deployment ```
      ``` cd Cluster ```

### 6) Provision the EKS cluster now,
      Note: Change the region and go to variable.tf and within that change the secret key name. Then, initialize the terraform init
      ```
      - terraform init
      - terraform plan
      - terraform apply -auto-approve
      ```
### 7) Launch 3 EC2 server

      - EBS: 25GB each
      - Instance type: t2.medium

      - Name:
      1) Jenkins
      2) SonarQube
      3) Nexus

      - Security group: 9000, 8081, 8080
      
### 8) Go to Jenkins Server

     - Update repo: ``` sudo apt update ```
     - Install Jenkins- Follow the official document on Jenkins.
     
### 9) Go to Nexus Server

     - Update repo : ``` sudo apt update ```
     - Install docker - ``` sudo apt install docker-io -y ```
        ``` sudo usermod -aG docker ubuntu ```
        ``` newgrp docker ```
    - Run the docker: 
      ``` docker run -d -p 8081:8081 sonatype/nexus3
    - Check docker ps  (Is docker is runnnig or not)  

### 10) Go to SonarQube Server

     - Update repo : ``` sudo apt update ```
     - Install docker - ``` sudo apt install docker-io -y ```
        ``` sudo usermod -aG docker ubuntu ```
    - Run the docker: 
      ``` docker run -d -p 9000:9000 sonarqube:lts-community ```

### 11) Go to Nexus Server
      
      - For password:
       ``` docker exec -it <container id> /bin/bash
      ``` bash
          cd sonatype-work
          ls
          cd nexus3/
          ls
          cat admin.password
      ``` 
      - Use this password to login into Nexus server

 ### 12) Go to Jenkins Server

       - Install docker from official website(search on google docker install on ubuntu)

       ``` sudo usermod -aG docker jenkins
       ``` sudo systemctl restart jenkins ```
       
### 13) On Jenkins Server install Trivy

        - Go to Trivy installation for Ubuntu (Aquasecurity)
        - Follow the steps and Install it.

### 14) On Jenkins Server install kubectl
        
        - ```sudo snap install kubectl --classic ```

### 15) On Server-Instance

       ``` sudo snap install kubectl --classic ```
       
### 16) On Server

        ``` aws eks --region ap-south-1 update-kubeconfig --name devopsshack-cluster ```
        
     

     
      
