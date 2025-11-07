# Stage 1: Build the app
FROM maven:3.9.5-jdk-21 AS builder

WORKDIR /app

# Use the container's Maven (no mvnw required)
COPY pom.xml ./
COPY src ./src

# Batch mode (-B) for CI, skip tests to speed up image builds
RUN mvn -B clean package -DskipTests

# Stage 2: Run the app
FROM eclipse-temurin:21-jdk

WORKDIR /app
COPY --from=builder /app/target/*.jar app.jar

EXPOSE 2000

ENTRYPOINT ["java", "-jar", "app.jar"]