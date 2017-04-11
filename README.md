# time-tracker
Java (Maven) application for tracking time on the job

## Purpose

This purpose of this project is to show how to use Maven and Jenkins together.

## Docker images for run the pipeline defined in Jenkinsfile

### Jenkins

```sh
docker run -id --rm --name jenkins -p 8080:8080 -p 50000:50000 -v $(pwd)/jenkins_home:/var/jenkins_home jenkins:2.32.3
```

### Sonar

```sh
docker run -d --name sonarqube -p 9000:9000 -p 9092:9092 sonarqube
```

### Tomcat

```sh
docker run -d -p 8888:8080 -e TOMCAT_PASS="tomcat" cloudsire/tomcat:8-jre8
```

### Artifactory

```sh
docker run -d -p 8081:8080 mattgruter/artifactory
```
