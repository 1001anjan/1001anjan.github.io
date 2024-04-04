---
layout: default
title: Introduction & Setup
parent: Nexus
grand_parent: CI/CD
nav_order: 1
---
### Nexus

Nexus Repository Manager is a widely used artifact repository manager developed by Sonatype. It serves as a central hub for storing, managing, and distributing software artifacts such as JAR files, Docker images, npm packages, and more. Artifact repositories are essential components of modern software development, enabling teams to efficiently manage dependencies, share components, and ensure the traceability and consistency of their software builds.

Key features of Nexus Repository Manager include:

* Artifact Hosting: Nexus allows you to host various types of software artifacts, such as JAR files, WAR files, Docker images, npm packages, and more. This centralizes the storage of artifacts, making them easily accessible to development and deployment processes.
* Dependency Management: Nexus helps manage dependencies for software projects. It stores and caches external dependencies, reducing the need to repeatedly download them from the internet. This speeds up build processes and ensures consistent dependencies across teams.
* Proxying External Repositories: Nexus can act as a proxy to external repositories (like Maven Central, npm Registry, etc.), which helps in minimizing external network dependencies, ensuring reliable access, and improving build times.
* Security and Access Control: Nexus offers fine-grained access control and security features. You can control who has access to which repositories and artifacts, enhancing security and compliance with organizational policies.
* Repository Formats: Nexus supports multiple repository formats, including Maven, npm, NuGet, Docker, PyPI, RubyGems, and more. This makes it versatile and suitable for a wide range of development ecosystems.
* Search and Discovery: Nexus provides a search interface to discover and locate artifacts, making it easier to find the components you need for your projects.
* Integration with CI/CD: Nexus can seamlessly integrate with Continuous Integration/Continuous Deployment (CI/CD) pipelines. It ensures that artifacts are readily available for automated builds and deployments.
* Artifacts Lifecycle Management: Nexus allows you to manage the lifecycle of artifacts, including versioning, snapshot/release management, and retention policies.
* High Availability and Scaling: Nexus offers options for high availability setups and scalability, enabling organizations to ensure reliable access to artifacts even in demanding environments.

Nexus Repository Manager helps software development teams improve their efficiency, reliability, and security by providing a central repository for managing artifacts and dependencies. It's widely used in the software industry to streamline development workflows and ensure that applications are built on a solid foundation of reliable components.

### Setup Nexus using docker image
To install Nexus Repository Manager as a Docker image, you can follow these steps:

1. Install Docker:
   If you haven't already, you need to install Docker on your machine. You can download and install Docker from the official Docker website for your specific operating system.
2. Pull Nexus Docker Image:
   Open a terminal or command prompt and run the following command to pull the Nexus Docker image from Docker Hub:
   ```markdown
   docker pull sonatype/nexus3
   ```
3. Run Nexus Container:
   Once the image is downloaded, you can run a Docker container using the pulled image. Run the following command:
   ```markdown
   docker run -d -p 8081:8081 --name nexus sonatype/nexus3
   ```
   This command will start a Docker container named "nexus" in the background. It maps port 8081 from the container to port 8081 on your host machine.
4. Access Nexus Web UI:
   After the container is up and running, you can access the Nexus Repository Manager's web interface by opening your web browser and navigating to:
   ```markdown
   http://localhost:8081
   ```
   The first time you access the Nexus UI, it might take a while to initialize. You'll need to wait until the Nexus application is fully up and running.
5. Initial Configuration:
   When you access the Nexus web interface for the first time, you might be asked for an initial admin password. To retrieve the password, you can check the Docker logs:  
   ```markdown
   docker logs nexus
   ```

### `build.gradle` configuration to publish library
```groovy

apply plugin: 'maven-publish'

bootJar.enabled = false
jar.enabled = true

publishing {
	publications {
		mavenJava(MavenPublication) {
			artifact jar
			groupId = 'com.example.mongodb'
			artifactId = "mongoReactor"
			version = "1.0.1-releases"
		}
	}
	repositories {
		maven {
			name = "snapshots"
			url = uri("http://localhost:8081/repository/test-repo/")
			credentials {
				username = "admin"
				password = "admin"
			}
			allowInsecureProtocol = true

		}
		maven {
			name = "releases"
			url = uri("http://localhost:8081/repository/test-repo/")
			credentials {
				username = "admin"
				password = "admin"
			}
			allowInsecureProtocol = true

		}
	}
}
```
### Gradle command to publish artifactory 
```markdown
./gradlew publish
```
#### Note
* make sure you create new repository and give proper access to the user to upload the jar file.

To configure a Nexus repository to allow uploading and hosting JAR files, you need to create a repository in Nexus that is set up to handle Maven artifacts. Here's a step-by-step guide on how to configure Nexus to upload and host JAR files:

1. Access Nexus Web Interface:
   Open your web browser and navigate to the Nexus server's web interface. Log in with an account that has administrative privileges.
2. Create a Maven Repository:
   Nexus uses repositories to organize and store artifacts. To host JAR files, you'll create a Maven repository:
   * Click on "Repositories" in the left navigation menu.
   * Click the "+ Create repository" button.
   * Choose "Maven (hosted)" repository type.
   * Fill in the repository configuration details, including Repository Name, HTTP Port, and Storage Location. You can choose a name like "my-jars" for the repository.
   * Click "Create repository". 
3. Repository Configuration:
   Once the repository is created, you might need to configure it:
   * Ensure the "Version Policy" is set according to your use case. For hosting JAR files, you might set it to "Release" or "Mixed."
   * Configure any other settings based on your requirements.

---
If you want to persist the data in a Docker container even after it is stopped or removed, you can use Docker volumes. Volumes allow you to store data outside of the container, making it independent of the container's lifecycle. This is especially useful for cases like Nexus repositories where you want to preserve the data even if the container is stopped, removed, or replaced.

Here's how you can use Docker volumes with the Nexus container:

1. Create a Docker Volume:
   Before running the Nexus container, create a Docker volume that will be used to store the Nexus data:
   ```markdown
    docker volume create nexus-data
   ```
2. Run the Nexus Container with a Volume:
   Run the Nexus container using the created volume:
   ```markdown
    docker run -d -p 8081:8081 --name nexus -v nexus-data:/nexus-data sonatype/nexus3
   ```
   In this command, `-v nexus-data:/nexus-data` maps the Docker volume named "nexus-data" to the `/nexus-data` directory inside the container.
3. Stopping and Starting:
   You can stop and start the container as needed. The data stored in the volume will be preserved across container restarts, stops, and removals.
4. Backup and Restore:
   Using volumes makes it easier to back up and restore your Nexus data. You can create a backup of the Docker volume, which will contain all the Nexus data, configuration, and repositories. You can then restore this backup by creating a new volume from the backup.

Using Docker volumes is a recommended practice for persisting data across container instances. It provides data durability and makes managing containerized applications more robust. Remember to regularly back up important data to external storage or cloud solutions to ensure the safety of your valuable data.








