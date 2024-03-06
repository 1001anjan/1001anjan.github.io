---
layout: default
title: Introduction & Setup
parent: Jenkins
grand_parent: CI/CD
nav_order: 1
---
### Jenkins
Jenkins is an open-source automation server that facilitates the continuous integration and continuous delivery (CI/CD) of software projects. It is designed to automate various tasks related to building, testing, and deploying software applications. Jenkins enables development teams to automate repetitive tasks, streamline workflows, and ensure the consistent integration and delivery of code changes.

Here's a breakdown of how Jenkins is used and its key features:

1. Continuous Integration (CI): Jenkins supports the practice of continuous integration, where code changes from different team members are frequently integrated into a shared repository. Jenkins automates the process of building the software whenever new code is pushed to the repository. It ensures that the newly added code doesn't break existing functionality by running automated tests.
2. Continuous Delivery/Deployment (CD): Jenkins also facilitates continuous delivery and deployment. Once the code is built and tested successfully, Jenkins can trigger the deployment process to various environments, such as development, staging, and production. This automation reduces the chance of human error and ensures consistent deployments.
3. Automation: Jenkins allows you to define workflows as pipelines, where you specify the steps that need to be executed, such as compiling code, running tests, packaging applications, and deploying them. These pipelines are typically written in a domain-specific language called Groovy, but Jenkins also offers a graphical user interface for creating and managing pipelines.
4. Plugins: Jenkins has a vast ecosystem of plugins that extend its functionality. These plugins cover a wide range of tasks, such as integrating with version control systems (e.g., Git, SVN), building tools (e.g., Maven, Gradle), testing frameworks (e.g., JUnit, Selenium), deployment tools, and notification services (e.g., email, Slack).
5. Scalability: Jenkins can be scaled to handle various projects and workflows simultaneously. You can set up distributed builds, where multiple Jenkins agents (nodes) handle different build tasks concurrently.
6. Monitoring and Reporting: Jenkins provides detailed logs and reports about build and deployment processes, making it easier to identify issues and monitor the health of your projects.

To use Jenkins:
1. Install and Set Up: Download and install Jenkins on a server or computer. Once installed, access its web interface to configure settings and manage plugins.
2. Create Jobs/Pipelines: Define jobs or pipelines that outline the tasks to be automated. A pipeline consists of stages, which represent different phases of the software development process.
3. Version Control Integration: Connect Jenkins to your version control system (e.g., Git) so that it can monitor repository changes and trigger build processes accordingly.
4. Configure Build and Test Steps: Set up build steps (e.g., compiling code) and test steps (e.g., running unit tests) within your pipeline.
5. Configure Deployment: Define deployment steps that specify how your application should be deployed to different environments.
6. Monitor and Troubleshoot: Monitor the execution of your pipelines, review logs, and address any issues that arise.
7. Extend with Plugins: Utilize Jenkins plugins to integrate with various tools and services that your development process relies on.


### Setup Jenkins using docker image
1. Pull Jenkins Image: Open a terminal/command prompt and run the following command to pull the official Jenkins image from Docker Hub:
   ```markdown
    docker pull jenkins/jenkins
   ```
2. Run Jenkins Container: Once the image is downloaded, use the following command to run a Jenkins container. Replace `/your/host/path` with the local directory path where you want to store Jenkins data (configurations, plugins, etc.) on your host machine.   
    ```markdown
     docker run -d -p 8080:8080 -p 50000:50000 -v /your/host/path:/var/jenkins_home --name jenkins jenkins/jenkins
    ```
   * `-d`: Run the container in detached mode.
   * `-p 8080:8080`: Map port 8080 on the host to port 8080 in the container (for Jenkins web interface).
   * `-p 50000:50000`: Map port 50000 on the host to port 50000 in the container (for Jenkins agents).
   * `-v /your/host/path:/var/jenkins_home`: Mount the specified directory on your host as the Jenkins home directory inside the container.
   * `--name jenkins`: Assign a name to the container (you can change "jenkins" to a name of your choice).
   * `jenkins/jenkins`: The name of the Docker image.
3. Access Jenkins Web Interface: Once the container is running, you can access the Jenkins web interface by opening a web browser and navigating to `http://localhost:8080`. If you're using a remote server, replace localhost with the server's IP address or domain name.
4. Unlock Jenkins: During the first access, you'll be prompted to provide an initial admin password. You can find this password in the logs of the Jenkins container. Run the following command to view the logs and find the password:
   ```markdown
    docker logs jenkins
    ``` 
5. Install Recommended Plugins: After unlocking Jenkins, you'll be prompted to install recommended plugins. Choose the "Install suggested plugins" option. This will install plugins necessary for basic Jenkins functionality.
6. Create Admin User: Once the plugins are installed, you can create an admin user and configure Jenkins settings.
7. Configure Security and Access: Jenkins by default is not fully secure, especially if exposed to the public internet. You should consider configuring security settings, setting up authentication, and possibly running Jenkins behind a reverse proxy with HTTPS for improved security.


To stop and remove the Jenkins container, you can use these commands:
```markdown
docker stop jenkins
docker rm jenkins
```

### Unlock Jenkins
`/var/jenkins_home/secrets/initialAdminPassword`
1. Find the Container ID or Name: 
    ```markdown
    docker ps
    ```
2. Run Commands Inside the Container:
   ```markdown
    docker exec -it <container_id_or_name> <command>
   ```
   ```markdown
   docker exec -it <container_id_or_name> <command>
   cat /var/jenkins_home/secrets/initialAdminPassword
   ```
3. Exit the Container: Once you're inside the container, you can use the `exit` command to leave the container's shell and return to your host's shell.  

---

### Install using Homebrew package manager
Jenkins can be installed using the Homebrew package manager. Homebrew formula: jenkins-lts This is a package supported by a third party which may be not as frequently updated as packages supported by the Jenkins project directly.

Sample commands:
* Install the latest LTS version: `brew install jenkins-lts`
* Start the Jenkins service: `brew services start jenkins-lts`
* Restart the Jenkins service: `brew services restart jenkins-lts`
* Update the Jenkins version: `brew upgrade jenkins-lts`
After starting the Jenkins service, browse to http://localhost:8080 and follow the instructions to complete the installation. 




 


