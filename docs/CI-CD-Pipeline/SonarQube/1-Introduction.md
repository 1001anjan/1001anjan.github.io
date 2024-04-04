---
layout: default
title: Introduction & Setup
parent: SonarQube
grand_parent: CI/CD
nav_order: 1
---
### SonarQube
SonarQube is a widely used open-source platform for continuous inspection of code quality. It's designed to help developers and development teams identify and address technical debt, bugs, vulnerabilities, and code smells in their software projects. The term "Sonar" stands for sound navigation and ranging, which is a nod to the technology's ability to "navigate" through code and provide insights.

Key features of SonarQube include:
1. Code Quality Analysis: SonarQube analyzes source code for a wide range of programming languages and identifies issues related to code duplication, coding standards, potential bugs, security vulnerabilities, and more.
2. Metrics and Insights: The platform provides metrics and visualizations that help developers understand the overall health of their codebase. It generates reports, graphs, and dashboards that highlight areas for improvement.
3. Integration and Automation: SonarQube can be integrated into various development environments, build tools, and continuous integration/continuous deployment (CI/CD) pipelines. This enables automated code quality checks as part of the development workflow.
4. Custom Rules and Profiles: Users can customize rule sets to reflect their coding standards and project requirements. SonarQube supports a wide range of coding rules out-of-the-box and allows you to define your own custom rules.
5. Security Analysis: SonarQube's security analysis capabilities focus on identifying vulnerabilities and security weaknesses in the code, which is crucial for preventing security breaches.
6. Workflow Integration: Developers can receive notifications and feedback about code quality issues directly within their development environment, allowing for quick and efficient fixes.
7. Continuous Improvement: SonarQube promotes a culture of continuous improvement by providing actionable insights and feedback to developers, helping them write cleaner, safer, and more maintainable code over time.

It's important to note that SonarQube has its limitations and might not catch all issues. It's most effective when used as part of a broader strategy for code quality and security, which could include manual code reviews, unit testing, static analysis tools, and security testing.

### Setup using docker image
1. Install Docker: Make sure you have Docker installed on your system. You can download and install Docker from the official Docker website: https://www.docker.com/get-started
2. Pull the SonarQube Image:
   Open a terminal and run the following command to pull the official SonarQube Docker image:
   ```markdown
    docker pull sonarqube
   ```
3. Run SonarQube Container:
   After pulling the image, run a Docker container using the following command:
   ```markdown
   docker run -d --name sonarqube -p 9000:9000 sonarqube
   ```
4. This command does the following:
   * `-d`: Runs the container in detached mode.
   * `--name sonarqube`: Specifies a name for the container.
   * `-p 9000:9000`: Maps port 9000 on the host to port 9000 on the container.
   * `sonarqube`: Refers to the name of the Docker image.
5. Access SonarQube Web Interface:
Once the container is up and running, you can access the SonarQube web interface by opening a web browser and navigating to http://localhost:9000. The default credentials are:
* Username: admin
* Password: admin  

---

### Configure Gradle for SonarQube Analysis:

* Create a SonarQube Project:

   * Open your web browser and navigate to http://localhost:9000 (replace with your actual SonarQube server URL).
   * Log in using the default credentials (admin/admin).
   * Create a new project in SonarQube by clicking on the '+' icon next to "Projects".
   * Provide a project key, name, and any other relevant information.

In your Gradle project, you need to set up the SonarQube analysis configuration. Here's how you can do it:

Open your `build.gradle` file.

1. Add the SonarQube plugin to the build script:
   ```groovy
    plugins {
    id "org.sonarqube" version "$SupportedVersionAsPerGradleVersion"
    }
   ```
2. Configure the SonarQube properties:
   ```markdown
     sonarqube {
      properties {
      property "sonar.projectKey", "<Your Project Key>"
      property "sonar.projectName", "<Your Project Name>"
      property "sonar.host.url", "http://localhost:9000"
      property "sonar.login", "your_username"
      property "sonar.password", "your_password"
      }
   }
   ```
   Replace `<Your Project Key>`, `<Your Project Name>`, `your_username`, and `your_password` with your actual values.

   Please note that specifying the password in plain text within the build script is not recommended for security reasons. It's better to use environment variables or other secure credential management mechanisms.

3. Run SonarQube Analysis:
   ```markdown
   ./gradlew sonarqube
   ```


