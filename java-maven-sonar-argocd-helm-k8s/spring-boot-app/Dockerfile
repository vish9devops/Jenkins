# Use Eclipse Temurin OpenJDK 17 (Alpine) base image
FROM eclipse-temurin:17-alpine

# Install Maven
RUN apk update && \
    apk add --no-cache maven && \
    rm -rf /var/cache/apk/*

# Set the working directory in the container
WORKDIR /opt/app

# Copy the source code into the container
COPY . /opt/app

# Debug: List files in the working directory for debugging purposes
RUN ls -l /opt/app

# Build the project and create a JAR file
WORKDIR /opt/app/java-maven-sonar-argocd-helm-k8s/spring-boot-app
RUN mvn clean package

# List the target folder to confirm the JAR file was created
RUN ls -l /opt/app/java-maven-sonar-argocd-helm-k8s/spring-boot-app/target

# Copy the JAR file into the /opt/app directory to use as the entrypoint
COPY java-maven-sonar-argocd-helm-k8s/spring-boot-app/target/spring-boot-web.jar /opt/app/app.jar

# Set the entrypoint to run the Spring Boot application
ENTRYPOINT ["java", "-jar", "/opt/app/app.jar"]

# Expose the port your application is running on (if necessary)
EXPOSE 8081
