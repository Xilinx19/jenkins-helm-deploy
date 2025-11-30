# Use Eclipse Temurin instead of deprecated openjdk images
FROM eclipse-temurin:17-jdk

# Copy the JAR built by Maven (your pipeline already copies it into ./docker)
COPY *.jar /app.jar

# Run the app
ENTRYPOINT ["java", "-jar", "/app.jar"]
# Use Eclipse Temurin instead of deprecated openjdk images
FROM eclipse-temurin:17-jdk

# Copy the JAR built by Maven (your pipeline already copies it into ./docker)
COPY *.jar /app.jar

# Run the app
ENTRYPOINT ["java", "-jar", "/app.jar"]
