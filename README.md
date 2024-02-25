# CICD Java Project
![Static Badge](https://img.shields.io/badge/jenkins-8A2BE2) ![Static Badge](https://img.shields.io/badge/Docker-0000) ![Static Badge](https://img.shields.io/badge/Sonarqube-%23CCBB2E) ![Static Badge](https://img.shields.io/badge/Kubernetes-%232E71CC) ![Static Badge](https://img.shields.io/badge/Maven-%23CC352E%20) ![Static Badge](https://img.shields.io/badge/Checkstyle-%23%23CC2EAF) ![Static Badge](https://img.shields.io/badge/Helm-%232E38CC) ![Static Badge](https://img.shields.io/badge/Slack-%23CC502E) ![Static Badge](https://img.shields.io/badge/Prometheus-%23CCBB2E) ![Static Badge](https://img.shields.io/badge/Grafana-%23CC502E)










## Table of Contents

- [Project Description](#project-description)
- [Installation and Usage](#installation-and-usage)
- [Key Learnings](#key-learnings)
- [Code Information](#code-information)
- [Contribution and License](#contribution-and-license)


## Project Description


The Vprofile Application is a Java-based platform designed to streamline user authentication and management tasks. With Vprofile, users can effortlessly log in, update their profiles, and engage with the community by sharing posts and thoughts. Additionally, users have the ability to register new accounts to join the platform.



## Installation and Usage


### Clone the Repository:

![Clone Repository](https://i.imgur.com/3Lcv1vX.png)
- Clone the project repository from the provided URL.

### Install Jenkins and Set Up Jenkins Plugins:

1. **Install Jenkins on a Server Instance:**
   - Set up Jenkins on a dedicated server by downloading and installing the Jenkins package according to your operating system's requirements.

2. **Install the Following Jenkins Plugins:**
   - Navigate to the Jenkins dashboard, click on "Manage Jenkins" -> "Manage Plugins" -> "Available" tab.
   - Search and install the following plugins:
     - Docker: Allows Jenkins to interact with Docker containers.
     - AWS: Provides integration with Amazon Web Services for deployment and management.
     - SonarQube: Integrates Jenkins with SonarQube for code quality analysis.
     - Slack: Enables Jenkins to send notifications to Slack channels.
     - Pipeline Utility Steps: Provides additional functionality for Jenkins Pipeline scripts.
     - Docker Pipeline: Allows Jenkins Pipeline to interact with Docker.
     - AWS SDK: Enables Jenkins to interact with AWS services programmatically.

### Prepare Environment:

1. **Ensure JDK 8 & 11 and Maven are Installed:**
   - Ensure that Java Development Kit (JDK) versions 8 and 11 are installed on the Jenkins server to build the application. Additionally, Maven should also be installed to manage dependencies and build the project.

2. **Set Up a Kubernetes Cluster for Deployment:**
   - Provision a Kubernetes cluster using a tool like KOPS on a cloud provider like AWS. Ensure that the necessary dependencies such as kubectl and helm are installed on the Jenkins server.

### Kubernetes Cluster Setup:

1. **Create a Kubernetes Cluster using KOPS in AWS:**
   - Follow the documentation provided by KOPS to create a Kubernetes cluster on AWS.

2. **Install OpenJDK-11, Docker, and Helm in the KOPS Server:**
   - SSH into the KOPS server and install the required dependencies such as OpenJDK-11, Docker, and Helm to facilitate the deployment process.

3. **Configure Jenkins to Use the KOPS Server as a Jenkins Slave:**
   - Set up the KOPS server as a Jenkins slave node to execute Helm commands during the deployment process.

### Configure Jenkins Pipeline:
![Clone Repository](https://i.imgur.com/uNg8Ucs.png)
1. **Create a Jenkins Pipeline Using the Provided Jenkinsfile:**
   - Define a Jenkins Pipeline script in the Jenkinsfile located in the root directory of your project repository. This Pipeline script will define the stages and steps of your CI/CD process.

2. **Update Jenkins Credentials with AWS and DockerHub Credentials:**
   - Navigate to "Manage Jenkins" -> "Manage Credentials" to add credentials for AWS (Access Key and Secret Key) and DockerHub (Username and Password) to enable Jenkins to interact with these services.

### SonarQube Setup:

1. **Install the Sonar Scanner Plugin in Jenkins:**
   - Install the Sonar Scanner plugin in Jenkins through the "Manage Plugins" section to enable code quality analysis.

2. **Configure SonarQube Scanner in Jenkins Global Tool Configuration:**
   - Configure SonarQube Scanner in Jenkins Global Tool Configuration by providing the path to the SonarQube Scanner installation directory.

3. **Obtain a SonarQube Token for Integration with Jenkins:**
   - Generate a SonarQube token from the SonarQube dashboard to allow Jenkins to authenticate and send analysis reports.

4. **Configure SonarQube Webhooks:**
   - Configure SonarQube webhooks to send analysis reports to Jenkins, enabling Jenkins to trigger subsequent pipeline stages based on code quality results.

### Execute Pipeline:

1. **Run the Jenkins Pipeline:**
   - Trigger the Jenkins pipeline to initiate the CI/CD process. Jenkins will execute the defined stages and steps, including building and publishing Docker images, and updating changes in Kubernetes using Helm charts.

### Access the Application:

1. **Access the Application:**
   - Once the deployment process is complete, access the deployed application using the provided URL or service endpoint. If not using ingress, obtain the LoadBalancer endpoint from the Kubernetes service to access the application. username: admin_vp password: dmin_vp

![Clone Repository](https://i.imgur.com/JkSoLxt.png)
![Clone Repository](https://i.imgur.com/oxDNjh5.png)


## Key Technologies
* **Java**: Programming language for backend development.
* **Maven**: Build automation tool for Java projects.
* **Docker**: Containerization platform for packaging applications.
* **Kubernetes**: Container orchestration system for managing containerized applications.
* **Helm**: Package manager for Kubernetes applications.
* **SonarQube**: Code quality management platform for static code analysis.
* **Jenkins**: Automation server for CI/CD pipelines.
* **Grafana & Promethus**: Monitering.



## Key Learnings

- Employed a **Multi-staged Dockerfile** alongside **Distroless images** to minimize image size and bolster security measures.
- Implemented an Nginx ingress controller for hosting and facilitating **path-based routing**.
- Utilized Horizontal Pod Autoscaler (**HPA**) in Kubernetes with a **CPU utilization threshold** set at 75%.
- During development, integrated with **AWS S3** to store artifacts, enhancing collaboration and version control.
- Gained proficiency in the **Jenkins Slave concept**, leveraging KOPS machines as Jenkins slaves to execute Helm charts due to the absence of native Helm plugins in Jenkins.
- Enhanced security by utilizing **ConfigMaps** for managing configurations and storing sensitive information securely in **Terraform Vault**.
- Skillfully managed **plugins and credentials** within Jenkins to ensure seamless integration and secure access control.
- Configure an** Elastic Block Store (EBS**) volume to preserve MySQL data securely within the AWS environment.







## Code Information
![Clone Repository](https://i.imgur.com/SIV7PEj.png)



![Clone Repository](https://i.imgur.com/gFCLe8j.png)

## Contribution

Pull requests are welcome. For major changes, please open an issue first
to discuss what you would like to change.

Please make sure to update tests as appropriate.

## License

[MIT](https://choosealicense.com/licenses/mit/)

