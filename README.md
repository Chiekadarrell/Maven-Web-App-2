# End-to-End Jenkins CI/CD Pipeline Project
<img width="525" alt="Maven Web App Arch" src="https://github.com/user-attachments/assets/1df7adfa-3083-4924-bb26-884f14e66541" />

## Project ToolBox 🧰
- Git: Git will be used to manage our application source code
- Github: Github is a free and open source distributed VCS designed to handle everything from small to very large projects with speed and efficiency
- Jenkins: Jenkins is an open source automation CI tool which enables developers around the world to reliably build, test, and deploy their software
- Maven: Maven will be used for the application packaging and building including running unit test cases
- SonarQube: SonarQube Catches bugs and vulnerabilities in your app, with thousands of automated Static Code Analysis rules
-  Nexus: Nexus Manage Binaries and build artifacts across your software supply chain
-  Ansible: Ansible will be used for the application deployment to both lower environments and production
-  Ansible: Ansible will be used for the application deployment to both lower environments and production
-  EC2: EC2 allows users to rent virtual computers (EC2) to run their own workloads and applications
-  Slack: Slack is a communication platform designed for collaboration which can be leveraged to build and develop a very robust DevOps culture. Will be used for Continuous feedback loop
-  Prometheus: Prometheus is a free software application used for event/metric monitoring and alerting for both application and infrastructure
-   Grafana: Grafana is a multi-platform open source analytics and interactive visualization web application. It provides charts, graphs, and alerts for the web when connected to supported data sources
-   Trivy: A security scanner used in Jenkins (or other CI/CD pipelines) to automate vulnerability scanning for your code, containers, and infrastructure-as-code.
-   Docker: To build an image
-   Kubernetes: Used for automating the deployment, scaling, and management of containerized applications

## Jenkins Complete CI/CD Pipeline Project Runbook

1. Create a GitHub Repository with the name Jenkins-Realworld-CICD-Project and push the code in this branch(main) to your remote repository (your newly created repository).

- Go to GitHub: https://github.com
- Login to Your GitHub Account
- Create a Repository called Jenkins-Realworld-CICD-Project
- Clone the Repository in the Repository directory/folder on your local machine
- Download the code in in this repository "Main branch": https://github.com/awanmbandi/realworld-cicd-pipeline-project.git
- Unzip the code/zipped file
- Copy and Paste everything from the zipped file into the repository you cloned in your local
- Open your Terminal
  - Add the code to git, commit and push it to your upstream branch "main or master"
  - Add the changes: git add -A
  - Commit changes: git commit -m "adding project source code"
  - Push to GitHub: git push
- Confirm that the code is now available on GitHub
  
2. Create An IAM Profile/Role For The Ansible Automation Engine (Dynamic Inventory)
   
- Create an EC2 Service Role in IAM with AmazonEC2FullAccess Privilege
- Navigate to IAM
  ![image](https://github.com/user-attachments/assets/460b43f9-c974-4dde-80bc-f669762cad90)
  - Click on Roles
  - Click on Create Role
  - Use Case: Select EC2
  - Click on Next
  - Attach Policy: AmazonEC2FullAccess
  - Click Next
  - Role Name: AWS-EC2FullAccess-Role
  - Click Create

 3. Jenkins/Maven/Ansible
  - Create a Jenkins VM instance
  - Name: Jenkins/Maven/Ansible
  - AMI: Amazon Linux 2
  - Instance type: t2.medium
  - Key pair: Select or create a new keypair
  - Security Group (Edit/Open): 8080, 9100 and 22 to 0.0.0.0/0
  - IAM instance profile: Select the AWS-EC2FullAccess-Role
  - User data (Copy the following user data): https://github.com/awanmbandi/realworld-cicd-pipeline-project/blob/maven-nexus-sonarqube-jenkins-install/jenkins-install.sh
  - Launch Instance

4. SonarQube
  - Create a SonarQube VM instance
  - Name: SonarQube
  - AMI: Ubuntu 20.04
  - Instance type: t2.medium
  - Key pair: Select a keypair
  - Security Group (Eit/Open): 9000, 9100 and 22 to 0.0.0.0/0
  - User data (Copy the following user data): https://github.com/awanmbandi/realworld-cicd-pipeline-project/blob/maven-nexus-sonarqube-jenkins-install/sonarqube-install.sh
  - Launch Instance

5. Nexus

