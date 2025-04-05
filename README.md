# End-to-End Jenkins CI/CD Pipeline Project
<img width="525" alt="Maven Web App Arch" src="https://github.com/user-attachments/assets/1df7adfa-3083-4924-bb26-884f14e66541" />

###### Project ToolBox 🧰
- [Git](https://git-scm.com/) Git will be used to manage our application source code.
- [Github](https://github.com/) Github is a free and open source distributed VCS designed to handle everything from small to very large projects with speed and efficiency
- [Jenkins](https://www.jenkins.io/) Jenkins is an open source automation CI tool which enables developers around the world to reliably build, test, and deploy their software
- [Maven](https://maven.apache.org/) Maven will be used for the application packaging and building including running unit test cases
- [SonarQube](https://docs.sonarqube.org/) SonarQube Catches bugs and vulnerabilities in your app, with thousands of automated Static Code Analysis rules.
- [Nexus](https://www.sonatype.com/) Nexus Manage Binaries and build artifacts across your software supply chain
- [Ansible](https://docs.ansible.com/) Ansible will be used for the application deployment to both lower environments and production
- [EC2](https://aws.amazon.com/ec2/) EC2 allows users to rent virtual computers (EC2) to run their own workloads and applications.
- [Slack](https://slack.com/) Slack is a communication platform designed for collaboration which can be leveraged to build and develop a very robust DevOps culture. Will be used for Continuous feedback loop.
- [Prometheus](https://prometheus.io/) Prometheus is a free software application used for event/metric monitoring and alerting for both application and infrastructure.
- [Grafana](https://grafana.com/) Grafana is a multi-platform open source analytics and interactive visualization web application. It provides charts, graphs, and alerts for the web when connected to supported data sources.
- [Splunk](https://www.splunk.com/) Splunk is an innovative technology which searches and indexes application/system log files and helps organizations derive insights from the data.

# Jenkins Complete CI/CD Pipeline Project Runbook
1) Create a GitHub Repository with the name `Jenkins-Realworld-CICD-Project` and push the code in this branch(main) to 
    your remote repository (your newly created repository). 
    - Go to GitHub: https://github.com
    - Login to `Your GitHub Account`
    - Create a Repository called `Jenkins-Realworld-CICD-Project`
    - Clone the Repository in the `Repository` directory/folder on your `local machine`
    - Download the code in in this repository `"Main branch"`: https://github.com/awanmbandi/realworld-cicd-pipeline-project.git
    - `Unzip` the `code/zipped file`
    - `Copy` and `Paste` everything `from the zipped file` into the `repository you cloned` in your local
    - Open your `Terminal`
        - Add the code to git, commit and push it to your upstream branch "main or master"
        - Add the changes: `git add -A`
        - Commit changes: `git commit -m "adding project source code"`
        - Push to GitHub: `git push`
    - Confirm that the code is now available on GitHub

2) Create An IAM Profile/Role For The Ansible Automation Engine (Dynamic Inventory)
- Create an EC2 Service Role in IAM with AmazonEC2FullAccess Privilege 
- Navigate to IAM
  ![image](https://github.com/user-attachments/assets/460b43f9-c974-4dde-80bc-f669762cad90)
   - Click on `Roles`
    - Click on `Create Role`
    - Select `Service Role`
    - Use Case: Select `EC2`
    - Click on `Next` 
    - Attach Policy: `AmazonEC2FullAccess`
    - Click `Next` 
    - Role Name: `AWS-EC2FullAccess-Role`
    - Click `Create`

3) Jenkins/Maven/Ansible
    - Create a Jenkins VM instance 
    - Name: `Jenkins/Maven/Ansible`
    - AMI: `Amazon Linux 2`
    - Instance type: `t2.medium`
    - Key pair: `Select` or `create a new keypair`
    - Security Group (Edit/Open): `8080, 9100` and `22 to 0.0.0.0/0`
    - IAM instance profile: Select the `AWS-EC2FullAccess-Role`
    - User data (Copy the following user data): https://github.com/awanmbandi/realworld-cicd-pipeline-project/blob/maven-nexus-sonarqube-jenkins-install/jenkins-install.sh
    - Launch Instance

4) SonarQube
    - Create a SonarQube VM instance 
    - Name: `SonarQube`
    - AMI: `Ubuntu 20.04`
    - Instance type: `t2.medium`
    - Key pair: `Select a keypair`
    - Security Group (Eit/Open): `9000, 9100` and `22 to 0.0.0.0/0`
    - User data (Copy the following user data): https://github.com/awanmbandi/realworld-cicd-pipeline-project/blob/maven-nexus-sonarqube-jenkins-install/sonarqube-install.sh
    - Launch Instance

5) Nexus
    - Create a Nexus VM instance 
    - Name: `Nexus`
    - AMI: `Amazon Linux 2`
    - Instance type: `t2.medium`
    - Key pair: `Select a keypair`
    - Security Group (Eit/Open): `8081, 9100` and `22 to 0.0.0.0/0`
    - User data (Copy the following user data): https://github.com/awanmbandi/realworld-cicd-pipeline-project/blob/maven-nexus-sonarqube-jenkins-install/nexus-install.sh
    - Launch Instance

6) EC2 (Dev Environment)
    - Create a Development VM instance
    - Click `Add additional tags`
      - Tag 1: Name: `Name`, Value: `Dev-Env`
      - Tag 2: Name: `Environment`, Value: `dev`
    - AMI: `Amazon Linux 2`
    - Number: `3`
    - Instance type: `t2.micro`
    - Key pair: `Select a keypair`
    - Security Group (Eit/Open): `8080, 9100, 9997` and `22 to 0.0.0.0/0`
    - User data (Copy the following user data): https://github.com/awanmbandi/realworld-cicd-pipeline-project/blob/tomcat-splunk-installation/tomcat-ssh-configure.sh
    - Launch Instance

7) EC2 (Stage Environment)
    - Create a Staging VM instance
    - Click `Add additional tags`
      - Tag 1: Name: `Name`, Value: `Stage-Env`
      - Tag 2: Name: `Environment`, Value: `stage`
    - AMI: `Amazon Linux 2`
    - Number: `3`
    - Instance type: `t2.micro`
    - Key pair: `Select a keypair`
    - Security Group (Eit/Open): `8080, 9100, 9997` and `22 to 0.0.0.0/0`
    - User data (Copy the following user data): https://github.com/awanmbandi/realworld-cicd-pipeline-project/blob/tomcat-splunk-installation/tomcat-ssh-configure.sh
    - Launch Instance

8) EC2 (Prod Environment)
    - Create a Production VM instance
    - Click `Add additional tags`
      - Tag 1: Name: `Name`, Value: `Prod-Env`
      - Tag 2: Name: `Environment`, Value: `prod`
    - AMI: `Amazon Linux 2`
    - Number: `3`
    - Instance type: `t2.micro`
    - Key pair: `Select a keypair`
    - Security Group (Eit/Open): `8080, 9100, 9997` and `22 to 0.0.0.0/0`
    - User data (Copy the following user data): https://github.com/awanmbandi/realworld-cicd-pipeline-project/blob/tomcat-splunk-installation/tomcat-ssh-configure.sh
    - Launch Instance

9) Prometheus
    - Create a Prometheus VM instance 
    - Name: `Prometheus`
    - AMI: `Ubuntu 20.04`
    - Instance type: `t2.micro`
    - Key pair: `Select a keypair`
    - Security Group (Eit/Open): `9090` and `22 to 0.0.0.0/0`
    - IAM instance profile: Select the `AWS-EC2FullAccess-Role`
    - Launch Instance

10) Grafana
    - Create a Grafana VM instance
    - Name: `Grafana`
    - AMI: `Ubuntu 20.04`
    - Instance type: `t2.micro`
    - Key pair: `Select a keypair`
    - Security Group (Eit/Open): `3000` and `22 to 0.0.0.0/0`
    - Launch Instance 9000, 9100 and 22 to 0.0.0.0/0
  - User data (Copy the following user data): https://github.com/awanmbandi/realworld-cicd-pipeline-project/blob/maven-nexus-sonarqube-jenkins-install/sonarqube-install.sh
  - Launch Instance
    
11) Monitoring
    - Create a Grafana VM instance
    - Name: `Grafana`
    - AMI: `Ubuntu 20.04`
    - Instance type: `t2.micro`
    - Key pair: `Select a keypair`
    - Security Group (Eit/Open): `3000` and `22 to 0.0.0.0/0`
    - Launch Instance 9000, 9100 and 22 to 0.0.0.0/0
  - User data (Copy the following user data): https://github.com/awanmbandi/realworld-cicd-pipeline-project/blob/maven-nexus-sonarqube-jenkins-install/sonarqube-install.sh
  - Launch Instance

#### NOTE: Confirm and make sure you have a total of 9 VM instances



