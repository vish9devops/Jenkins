# Use an appropriate base image for Java 17 (OpenJDK 17 on Alpine)
FROM adoptopenjdk/openjdk17:alpine-jre

# Install Maven to build the Spring Boot project (if needed)
RUN apk add --no-cache maven && rm -rf /var/cache/apk/*

# Set the working directory in the container
WORKDIR /opt/app

# Copy the source code into the container (change this to the correct path)
COPY . /opt/app

# Debug: List files in the workspace to check if the source code and pom.xml are there
RUN ls -l /opt/app

# Build the project and create a JAR file inside the container
WORKDIR /opt/app/java-maven-sonar-argocd-helm-k8s/spring-boot-app
RUN mvn clean package

# List the target folder to confirm the JAR file was created
RUN ls -l /opt/app/java-maven-sonar-argocd-helm-k8s/spring-boot-app/target

# Copy the JAR file into the /opt/app directory to use as the entrypoint
COPY java-maven-sonar-argocd-helm-k8s/spring-boot-app/target/spring-boot-web.jar /opt/app/app.jar

# Set the entrypoint to run the Spring Boot application
ENTRYPOINT ["java", "-jar", "/opt/app/app.jar"]

# Expose the port your application is running on (if necessary)
EXPOSE 8080
