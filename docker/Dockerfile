# Use a valid OpenJDK image tag
FROM openjdk:17-jdk-slim

# Copy the jar built by Maven (you already copy it into this folder in the pipeline)
ADD *.jar app.jar

# Run the app
ENTRYPOINT ["java", "-jar", "/app.jar"]
