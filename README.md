 Spring Boot & Docker Integration Demo.
 A lightweight Spring Boot application built with Java 11 and Maven, integrated with Docker, Docker Compose, and a Jenkins CI/CD pipeline for automated building and deployment.
---
##  Overview
This project serves as a starter template and demonstration for:
- Developing a basic REST API with **Spring Boot 2.6.7** and **Java 11**.
- Packaging the Spring Boot application inside a **Docker container** using a multi-stage approach.
- Coordinating deployments using **Docker Compose**.
- Orchestrating a continuous delivery workflow with a **Jenkins Pipeline**.
---
##  Tech Stack & Dependencies
- **Backend Framework**: Spring Boot `2.6.7` (Spring Web Starter)
- **Language**: Java 11 (AdoptOpenJDK JRE Hotspot)
- **Database Driver**: MySQL Connector Java (Runtime scope)
- **Build Tool**: Maven (with Maven Wrapper included)
- **Containerization**: Docker & Docker Compose
- **CI/CD**: Jenkins Pipeline (`Jenkinsfile`)
---

##  Getting Started
### Prerequisites
Ensure you have the following installed:
* **Java Development Kit (JDK) 11**
* **Maven** (or use the included `./mvnw`)
* **Docker** & **Docker Compose**
### Running Locally
1. **Clone the repository**:
   ```bash
   git clone https://github.com/israhadjhassine/exp1spring.git
   cd exp1spring
   ```
2. **Run using Maven Wrapper**:
   * On Linux/macOS:
     ```bash
     ./mvnw spring-boot:run
     ```
   * On Windows:
     ```cmd
     mvnw.cmd spring-boot:run
     ```
3. **Verify the App**:
   The application runs on `http://localhost:8080` by default.
---
## 🔌 API Endpoints
### Test Endpoint
* **URL**: `/test`
* **Method**: `GET`
* **Response**: `Hello World`
* **Example Request**:
  ```bash
  curl http://localhost:8080/test
  ```
---
##  Containerization & Deployment
### Dockerfile
The [Dockerfile](file:///d:/exp1spring/Dockerfile) packages the application to run in production:
* **Base Image**: `adoptopenjdk:11-jre-hotspot`
* **Port Expose**: Exposes port `8091`
* **Active Profile**: Starts the jar with the `prod` profile active:
  ```bash
  java -jar app.jar --spring.profiles.active=prod
  ```
### Docker Compose
The [docker-compose.yml](file:///d:/exp1spring/docker-compose.yml) defines the deployment setup:
* **Image**: Uses `hello-world` image (which is built via Jenkins as the Spring Boot app container).
* **Port Mapping**: Maps port `8084` on the host to port `8080` in the container.
To spin it up manually:
```bash
docker build -t hello-world .
docker-compose up -d
```
Access the Dockerized app at `http://localhost:8084/test`.
---
##  CI/CD Pipeline (Jenkins)
The repository includes a [Jenkinsfile](file:///d:/exp1spring/Jenkinsfile) defining a declarative pipeline with the following stages:
1. **Build**: Runs `mvn clean install` to compile and package the application.
2. **Clean up**: Deletes the Jenkins workspace to prepare for a fresh clone.
3. **Clone repo**: Clones the latest version of the repository from GitHub.
4. **Generate backend image**: Builds the Docker image from the Dockerfile and tags it as `hello-world`.
5. **Run docker compose**: Deploys the service in detached mode using `docker-compose up -d`.
