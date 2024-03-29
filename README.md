# Minimal Reproducible example for [OpenJ9 issue #6720](https://github.com/eclipse/openj9/issues/6720)

## Debug JVM Docker Image build
The `openj9-jdk8-docker` folder contains a Dockerfile to build the OpenJ9 jdk8 Docker build with the debug version provided by @pshipton
This image is also available as **gyuuu/openj9:jdk8-20190906-184840**

The `openj9-jdk11-docker` folder contains a Dockerfile to build the OpenJ9 jdk11 Docker build with the debug version provided by @pshipton
This image is also available as **gyuuu/openj9:jdk11-20190906-184832**

## Debug JVM Docker image with Maven build
The `openj9-jdk8-maven-docker`folder contains a Dockerfile to build the previously mentioned OpenJ9 jdk8 Docker image with maven for building the project

The `openj9-jdk11-maven-docker`folder contains a Dockerfile to build the previously mentioned OpenJ9 jdk8 Docker image with maven for building the project

## Demo Spring Boot application
Basic Spring Boot Hello World application for testing.
Can be built with with multi stage docker build 
**Shared classes cache is created during test execution** using **Surefire** plugin's **argLine** configuration provided in the **pom.xml**