## Project Title: Deployment Strategy using Blue-Green Deployment
![Architecture-blue-green](https://github.com/user-attachments/assets/2790a8da-29b8-48a6-b971-13078b195ae8)

### What is Blue-Green Deployment?
Blue-Green deployment is a software release management strategy that reduces downtime and mitigates deployment risks. In this strategy, two production environments are maintained:

- Blue Environment: The current live application is running in the Blue environment.
- Green Environment: The new version of the application is deployed in the Green environment.
After the new version is deployed and tested in the Green environment, traffic is shifted from the Blue to the Green environment using a load balancer. If any issues arise after the switch, traffic can be rolled back to the Blue environment. This strategy allows for zero downtime during deployments and ensures a safe and efficient rollback mechanism.

### Project Summary:
The goal of this project is to implement a Blue-Green deployment strategy for an application consisting of a Java frontend and a MySQL database. The application will be deployed on AWS EKS with Docker containers for both the frontend and database services.

### Key Features:
- Two environments: Blue (current live) and Green (new release).
- Load balancer to switch traffic between Blue and Green environments.
- Zero downtime deployments with quick rollback if issues occur.
- Jenkins for Continuous Integration and Continuous Deployment (CI/CD).
- SonarQube for code quality analysis.

### Project Requirements:

- AWS Infrastructure:
   - EKS Cluster with 3 node groups of x.large instance types for application hosting.
 - EC2 Instances:
   - 1 server instance for hosting the application.
   - 1 Jenkins instance for CI/CD automation.
   - 1 Nexus instance for managing dependencies and artifacts.
   - 1 SonarQube instance for code quality checks.
 - Application Components:
 
   - Frontend: Java-based application.
 - Database: MySQL for the data layer.

- Toolset:

  - Docker for containerization.
  - SonarQube for static code analysis.
  - Terraform for infrastructure provisioning.
  - AWS CLI for managing AWS resources.
  - Sonatype Nexus for managing Maven dependencies.
  - Maven for building Java-based applications.
  - Trivy for security scanning of Docker images.

### Dependencies Tools and Packages:

  - Docker: Containerization of the frontend and backend services.
  - SonarQube: For static code analysis and quality gates.
  - Terraform: Infrastructure as Code (IaC) for provisioning AWS resources.
  - AWS CLI: For managing AWS resources and configuring infrastructure.
  - Sonatype Nexus: For artifact storage and management.
  - Maven: For building and packaging the Java application.
  - Trivy: For scanning Docker images for vulnerabilities.

### Application Architecture:

- Frontend: Java-based application running in Docker containers.
- Database: MySQL running in a container or managed through AWS RDS.

### Troubleshooting:

1.SonarQube Analysis: During initial configuration, I misconfigured the analysis settings by forgetting to add the . symbol, which caused the Java files in the current directory to be missed. This was fixed by adjusting the configuration file to 
  include the correct directory.

2.Docker Daemon Permission Issue: The Docker Daemon was not running, and I encountered a "permission denied" error. The issue was resolved by restarting the Docker service and adding Jenkins to the Docker group to grant it the necessary 
  permissions.

3. Docker Push Error: I mistakenly included the -t flag while attempting to push a Docker image, which is unnecessary for the docker push command. Removing the flag resolved the issue.
