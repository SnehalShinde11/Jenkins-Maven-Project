# Jenkins Maven Project

**Name:** Snehal Shinde  
**Repository:** `SnehalShinde11/Jenkins-Maven-Project`  
**Branch:** `main`  
**Technologies:** Jenkins, Jenkins Pipeline, Jenkinsfile, Java, Maven, GitHub, SonarQube

---

# Project 1.1 – Implementing Jenkins Pipeline as Code Using Jenkinsfile

## Problem Statement Overview

The objective of this project is to implement a **Continuous Integration (CI) pipeline using Jenkins Pipeline as Code**.

Instead of configuring Jenkins jobs manually through the Jenkins UI, the pipeline configuration is defined in a **Jenkinsfile** and stored inside the GitHub repository.

This approach provides the following benefits:

- Version control of CI pipelines
- Reproducibility of builds
- Consistent pipeline configuration
- Better collaboration between developers and DevOps engineers
- Easy maintenance and tracking of pipeline changes

The project demonstrates how Jenkins can retrieve source code from GitHub and execute the Maven build pipeline defined in the Jenkinsfile.

---

## Solution Approach

The solution is implemented using **Jenkins Pipeline as Code**.

A Java Maven application is maintained in the GitHub repository along with its `pom.xml` and `Jenkinsfile`.

The `Jenkinsfile` defines the CI pipeline with the following stages:

1. **Checkout** – Retrieves the source code from the GitHub repository.
2. **Build** – Compiles the Java application using Maven.
3. **Test** – Executes the Maven test cases.
4. **Package** – Packages the application into a JAR file.
5. **Archive Artifact** – Archives the generated JAR file in Jenkins.

The Jenkins pipeline configuration is maintained as code, making the CI process version-controlled, reproducible, and easier to maintain.

---

## Dependencies

The following tools are required for this project:

- **Java JDK**
- **Apache Maven**
- **Git**
- **Jenkins**
- **GitHub**

### Verify Java

```bash
java -version
```

### Verify Maven

```bash
mvn -version
```

### Verify Git

```bash
git --version
```

---

## Jenkins Setup

### 1. Create a Pipeline Job

From the Jenkins dashboard:

```text
New Item → Pipeline
```

Provide a suitable job name and select **Pipeline**.

### 2. Configure Pipeline from SCM

Under the **Pipeline** section, configure:

```text
Definition:
Pipeline script from SCM

SCM:
Git
```

Repository URL:

```text
https://github.com/SnehalShinde11/Jenkins-Maven-Project.git
```

Branch:

```text
*/main
```

Script Path:

```text
Jenkinsfile
```

Save the Jenkins job configuration.

Jenkins will retrieve the `Jenkinsfile` from the GitHub repository and use it as the pipeline definition.

---

# Project 1.2 – Implementing Parallel CI Pipeline in Jenkins

## Problem Statement Overview

The objective of this project is to implement a **Parallel Continuous Integration (CI) pipeline using Jenkins**.

In a traditional Jenkins pipeline, stages are generally executed sequentially. This can increase the overall build time when multiple independent tasks need to be performed.

Jenkins provides the ability to execute independent stages in **parallel**, allowing multiple tasks to run simultaneously.

The purpose of this project is to demonstrate how parallel stages can be configured using a Jenkinsfile and how Jenkins can execute independent CI tasks concurrently.

---

## Solution Approach

The solution is implemented using **Jenkins Pipeline as Code** with parallel stages.

The existing GitHub repository from **Project 1.1** is reused for this project.

A separate pipeline definition is maintained in:

```text
Jenkinsfile2
```

The `Jenkinsfile2` contains parallel stages for independent CI activities.

By default, the pipeline uses:

```groovy
checkout scm
```

This allows Jenkins to retrieve the source code from the configured SCM repository without hardcoding the repository checkout configuration inside the pipeline.

The parallel pipeline helps reduce overall execution time by running independent stages simultaneously.

---

## Dependencies

The following tools are required for this project:

- **Java JDK**
- **Apache Maven**
- **Git**
- **Jenkins**
- **GitHub**

### Verify Java

```bash
java -version
```

### Verify Maven

```bash
mvn -version
```

### Verify Git

```bash
git --version
```

---

## Jenkins Setup

### 1. Create a Pipeline Job

From the Jenkins dashboard:

```text
New Item → Pipeline
```

Provide a suitable job name and select **Pipeline**.

### 2. Configure Pipeline from SCM

Under the **Pipeline** section, configure:

```text
Definition:
Pipeline script from SCM

SCM:
Git
```

Repository URL:

```text
https://github.com/SnehalShinde11/Jenkins-Maven-Project.git
```

Branch:

```text
*/main
```

### 3. Configure Jenkinsfile2

Since this project uses `Jenkinsfile2` instead of the default `Jenkinsfile`, configure the Script Path as:

```text
Jenkinsfile2
```

The final configuration should be:

```text
Definition: Pipeline script from SCM
SCM: Git
Repository: https://github.com/SnehalShinde11/Jenkins-Maven-Project.git
Branch: */main
Script Path: Jenkinsfile2
```

Save the Jenkins job configuration.

---

# Project 1.3 – Jenkins Master-Agent Distributed Build Architecture

## Problem Statement Overview

The objective of this project is to implement a **Jenkins Master-Agent distributed build architecture**.

In this architecture, the Jenkins Master (Controller) manages the CI/CD environment, while Jenkins Agent nodes execute build and test workloads. This allows Jenkins to distribute workloads across multiple machines instead of running every job on a single server.

This architecture provides the following benefits:

- Distributed build execution
- Improved scalability
- Better resource utilization
- Parallel job execution
- Environment-specific builds
- Isolation of workloads
- Reduced load on the Jenkins Controller

---

## Solution Approach

The solution uses a Jenkins Controller and one or more Jenkins Agent nodes.

The Jenkins Controller is responsible for:

- Managing Jenkins configuration
- Scheduling builds
- Managing jobs and pipelines
- Managing credentials and global configuration
- Assigning workloads to appropriate agents

The Jenkins Agents are responsible for:

- Executing build commands
- Running Maven builds
- Running automated tests
- Checking out source code
- Generating build artifacts

A label is assigned to the agent so that Jenkins pipelines can explicitly select the appropriate node for execution.

The overall architecture can be represented as:

```text
                    GitHub Repository
                           |
                           v
                 +-------------------+
                 | Jenkins Controller |
                 |      (Master)      |
                 +---------+---------+
                           |
              +------------+------------+
              |                         |
              v                         v
      +---------------+         +---------------+
      | Jenkins Agent |         | Jenkins Agent |
      |    Node 1     |         |    Node 2     |
      +---------------+         +---------------+
              |                         |
              v                         v
        Maven / Java              Maven / Java
          Builds                    Builds
```

The Controller schedules the build and assigns the workload to an available Agent.

---

## Dependencies

The following components are required:

- **Jenkins Controller (Master)**
- **Jenkins Agent node(s)**
- **Java JDK**
- **Apache Maven**
- **Git**
- Network connectivity between Controller and Agent
- SSH connectivity or another supported Jenkins Agent launch method
- Jenkins credentials for connecting to the Agent

### Verify Java

```bash
java -version
```

### Verify Maven

```bash
mvn -version
```

### Verify Git

```bash
git --version
```

---

## Jenkins Master-Agent Setup

### 1. Prepare the Agent Machine

Create or configure a separate machine or VM that will be used as a Jenkins Agent.

Install the required dependencies:

```text
Java
Git
Maven
```

Verify the installations:

```bash
java -version
mvn -version
git --version
```

### 2. Create a Jenkins Agent

From the Jenkins dashboard:

```text
Manage Jenkins → Nodes
```

Select:

```text
New Node
```

Provide an appropriate node name, for example:

```text
java-agent
```

Select:

```text
Permanent Agent
```

Example configuration:

```text
Name:
java-agent

Remote root directory:
/home/jenkins

Labels:
java-agent

Usage:
Use this node as much as possible
```

### 3. Configure Agent Launch Method

Configure the appropriate launch method based on the environment.

For an SSH-based setup:

```text
Launch agents via SSH
```

Provide:

- Agent host
- SSH credentials
- Host key verification strategy
- Java configuration if required

Save the configuration.

Jenkins will establish communication with the Agent and make it available for build execution.

---

## Verify Agent Status

After configuring the Agent, navigate to:

```text
Manage Jenkins → Nodes → java-agent
```

The Agent should appear as:

```text
Online
```

The node information should show the assigned label:

```text
java-agent
```

This confirms that the Jenkins Controller can communicate with the Agent.

---

## Configure Pipeline to Run on Agent

A Jenkins Pipeline can target a specific Agent using its label.

Example:

```groovy
pipeline {
    agent {
        label 'java-agent'
    }

    stages {

        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build') {
            steps {
                sh 'mvn clean compile'
            }
        }

        stage('Test') {
            steps {
                sh 'mvn test'
            }
        }

        stage('Package') {
            steps {
                sh 'mvn package'
            }
        }
    }
}
```

In this configuration, Jenkins schedules the pipeline on the Agent having the label:

```text
java-agent
```

The build commands are therefore executed on the Agent rather than directly on the Jenkins Controller.

---

## Expected Result

After successfully configuring the Master-Agent architecture:

1. Jenkins Controller receives the build request.
2. Jenkins identifies an available Agent.
3. Jenkins assigns the pipeline to the Agent.
4. The Agent checks out the source code.
5. Maven executes the build and test stages.
6. The application is packaged.
7. Build artifacts are generated.
8. Jenkins reports the build result.

This demonstrates **distributed build execution using Jenkins Master-Agent architecture**.

---

# Project 1.4 – Jenkins + SonarQube Quality Gate Pipeline

## Problem Statement Overview

The objective of this project is to integrate **Jenkins with SonarQube** to perform automated code quality analysis as part of a Continuous Integration (CI) pipeline.

SonarQube analyzes the source code and identifies potential issues related to:

- Bugs
- Vulnerabilities
- Code smells
- Code coverage
- Maintainability
- Reliability
- Security

The Jenkins pipeline is configured to execute SonarQube analysis during the CI process and use the **SonarQube Quality Gate** to determine whether the code meets the defined quality standards.

### Project Repository

The Java project used for SonarQube analysis is maintained in the following GitHub repository:

`https://github.com/demo1orgtoday/SonarQubeCoverageJava`

---

## Solution Approach

The solution integrates **Jenkins, SonarQube, and GitHub** to automate code quality analysis.

The implementation consists of the following tasks:

1. Install and configure SonarQube.
2. Install the required SonarQube plugin in Jenkins.
3. Configure the SonarQube server in Jenkins.
4. Create a Jenkins Pipeline job.
5. Create a Jenkinsfile containing the SonarQube analysis and Quality Gate configuration.
6. Execute the Jenkins pipeline.
7. Verify the SonarQube analysis results and Quality Gate status.

The pipeline allows code quality analysis to become an integrated part of the CI process rather than being performed manually.

---

## Dependencies

The following components are required:

- **Jenkins**
- **SonarQube**
- **Java JDK**
- **Apache Maven**
- **Git**
- **GitHub**
- **Jenkins SonarQube Scanner plugin**

### Verify Java

```bash
java -version
```

### Verify Maven

```bash
mvn -version
```

### Verify Git

```bash
git --version
```

---

# Repository Structure

```text
Jenkins-Maven-Project/
│
├── src/
│   └── main/
│       └── java/
│           └── com/
│               └── example/
│                   └── App.java
│
├── pom.xml
├── Jenkinsfile
├── Jenkinsfile2
├── README.md
└── Jenkins-Project .pdf
```

### Pipeline Files

| File | Project | Purpose |
|---|---|---|
| `Jenkinsfile` | Project 1.1 | Jenkins Pipeline as Code |
| `Jenkinsfile2` | Project 1.2 | Parallel CI Pipeline |
| `pom.xml` | Project 1.1, 1.2 & 1.3 | Maven project configuration |
| `App.java` | Project 1.1, 1.2 & 1.3 | Java application source code |
| `README.md` | Project 1.1, 1.2, 1.3 & 1.4 | Project documentation |

---

# Assignment Details

**Name:** Snehal Shinde

### Project 1.1
**Implementing Jenkins Pipeline as Code Using Jenkinsfile**

**Pipeline File:** `Jenkinsfile`

### Project 1.2
**Implementing Parallel CI Pipeline in Jenkins**

**Pipeline File:** `Jenkinsfile2`

### Project 1.3
**Jenkins Master-Agent Distributed Build Architecture**

**Architecture:** Jenkins Controller/Master + Jenkins Agent

### Project 1.4
**Jenkins + SonarQube Quality Gate Pipeline**

**SonarQube Project Repository:**  
`https://github.com/demo1orgtoday/SonarQubeCoverageJava`

### Primary Repository

`https://github.com/SnehalShinde11/Jenkins-Maven-Project`

**Branch:** `main`
