# Use Maven to build the application
FROM maven:3.9.5-openjdk-17-slim AS build

WORKDIR /app

# Copy pom.xml and download dependencies
COPY pom.xml .
RUN mvn dependency:go-offline -B

# Copy source code and build
COPY src ./src
RUN mvn clean package -DskipTests

# Runtime stage
FROM openjdk:17-jdk-slim

WORKDIR /app

# Install Docker CLI for code execution
RUN apt-get update && apt-get install -y \
    docker.io \
    && rm -rf /var/lib/apt/lists/*

# Copy the built JAR file
COPY --from=build /app/target/*.jar app.jar

# Create temp directory for judge
RUN mkdir -p /tmp/judge

# Expose port
EXPOSE 8080

# Run the application
ENTRYPOINT ["java", "-jar", "app.jar"]

