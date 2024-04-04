---
layout: default
title: Introduction & Setup
parent: Dependency Tracker
grand_parent: CI/CD
nav_order: 1
---
### Dependency-Track
Dependency-Track is an open-source platform designed to help organizations identify and reduce risk in the software supply chain. It focuses on managing and tracking the dependencies of software components (libraries, frameworks, modules, etc.) used in your applications. This is important because these dependencies can introduce vulnerabilities that could be exploited by attackers.

Dependency-Track offers features like:
1. Dependency Analysis: It can scan your project's dependencies and identify known vulnerabilities associated with them.
2. Continuous Monitoring: Dependency-Track can continuously monitor the security status of your software components and notify you if new vulnerabilities are discovered in any of them.
3. Vulnerability Management: It helps you prioritize and manage vulnerabilities by providing details about the vulnerabilities and suggesting possible remediation actions.
4. Risk Metrics: The platform can calculate risk scores based on the severity of vulnerabilities and other factors, aiding in making informed decisions about which vulnerabilities to address first.
5. Integration: Dependency-Track can be integrated into your DevOps pipeline to automate vulnerability scanning and management, ensuring that you're aware of any security issues as early as possible in the development process.
6. Component Inventory: It maintains an inventory of all the components and their versions used in your projects, making it easier to track and manage them over time.

### Install Dependency-Track using docker image
* Install Docker: Make sure you have Docker installed on your system. You can download and install Docker from the official Docker website.
* Pull the Dependency-Track Image: Open a terminal and use the docker pull command to download the Dependency-Track Docker image from Docker Hub. The command might look something like this:
   ```markdown
   docker pull owasp/dependency-track
   ```
* Run the Docker Container: After pulling the image, you can create and run a Docker container using the image. You'll need to configure environment variables and potentially expose ports depending on your setup. Here's a basic example:
  Create database 
  ```markdown
  CREATE DATABASE dependencytrackdb;
  ```
  ```markdown
  docker run -d --name dependency-track \
  -p 8080:8080 \
  -e DB_CONNECTION_STRING=jdbc:postgresql://db-host:5432/dependencytrackdb \
  -e DB_USER=your_db_user \
  -e DB_PASS=your_db_password \
  owasp/dependency-track
  ```
  Replace `db-host`, `your_db_user`, and `your_db_password` with your actual database information.
* Access Dependency-Track: Once the container is running, you should be able to access Dependency-Track's web interface by opening a web browser and navigating to http://localhost:8080 (or the appropriate IP address if you're running Docker on a remote server).

* Default user: admin , password: admin

---



 


