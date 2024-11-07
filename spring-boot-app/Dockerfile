# Specify the base image
FROM adoptopenjdk/openjdk11:alpine-jre

# Allow artifact path to be overridden, with a default value
ARG artifact=target/spring-boot-web.jar

# Set the working directory inside the container
WORKDIR /opt/app

# Copy the artifact to the container
# Use double quotes to ensure proper substitution of the ARG
COPY "${artifact}" app.jar

# Set the entry point to run the jar
ENTRYPOINT ["java", "-jar", "app.jar"]
