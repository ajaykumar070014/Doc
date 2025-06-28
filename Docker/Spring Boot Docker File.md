## 📄 `Dockerfile`
```
# Start from a Java runtime base image
FROM eclipse-temurin:17-jdk-jammy

# Set the working directory inside the container
WORKDIR /app

# Copy the Spring Boot fat JAR to the container
COPY target/sample-docker-0.0.1-SNAPSHOT.jar app.jar

# Expose the port that the app runs on
EXPOSE 8080

# Command to run the jar file
ENTRYPOINT ["java", "-jar", "app.jar"]

```

## 📦 `Build & Run Instructions`
## Step:1 Build your JAR:
### For POM.xml:
```
./mvnw clean package
```
### For Gradle:
```
./gradlew bootJar
```
### After Jar Build Check your target/ directory. You'll typically see something like:
```csharp
target/
├── classes/
├── demo-0.0.1-SNAPSHOT.jar  ← ✅ This is your fat JAR
└── ...
```
### ✅ So, update this line in your Dockerfile:
```
COPY target/demo-0.0.1-SNAPSHOT.jar app.jar
```
## Step:2 Build Docker image:
```
docker build -t my-spring-boot-app .
```
## Step:3 Run container:
```
docker run -p 8080:8080 my-spring-boot-app
```
