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

## If Your postgres inside the docker then

```
docker network create my-network; docker run -d --name my-postgres --network my-network -e POSTGRES_DB=postgres -e POSTGRES_USER=postgres -e POSTGRES_PASSWORD=postgres -p 5433:5432 postgres:latest; docker build -t springboot-app .; docker run -d --name my-springboot --network my-network -e DB_HOST=my-postgres -e DB_PORT=5432 -e DB_NAME=postgres -e DB_USERNAME=postgres -e DB_PASSWORD=postgres -p 8080:8080 springboot-app
```
