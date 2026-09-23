# pipeline-ci-demo

A minimal Java 17 Maven application intended for Jenkins continuous integration.

## Project structure

```text
pipeline-ci-demo/
├── src/
│   └── main/
│       └── java/
│           └── com/example/
│               └── App.java
├── pom.xml
├── Jenkinsfile
└── README.md
```

## Prerequisites

- Java Development Kit (JDK) 17 or newer
- Apache Maven 3.9 or newer
- Jenkins with configured tools named `jdk17` and `maven3` (for the included pipeline)

## Build and run locally

```bash
mvn clean package
java -jar target/pipeline-ci-demo-1.0.0-SNAPSHOT.jar
```

Expected output:

```text
Hello from the Jenkins Maven CI demo!
```

## Jenkins

Create a Pipeline job that uses this repository as its source. Jenkins automatically reads the root-level `Jenkinsfile`, checks out the source, builds the JAR with Maven, and archives the build artifact.

If your Jenkins global tool names differ, update `jdk 'jdk17'` and `maven 'maven3'` in the `Jenkinsfile`.
