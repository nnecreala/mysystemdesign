# Stage 1: Build
FROM maven:3.9-eclipse-temurin-25 AS builder
WORKDIR /build
COPY . .
RUN mvn clean package -DskipTests

# Stage 2: Run
FROM eclipse-temurin:25-jre
WORKDIR /app
COPY --from=builder /build/auth-service/target/auth-service.jar auth-service.jar
# Expose default port (customize as needed)
EXPOSE 8080

# JVM Configuration for containers
ENV JAVA_OPTS="-XX:+UseContainerSupport -XX:InitialRAMPercentage=50.0 -XX:MaxRAMPercentage=75.0 -XX:+UseG1GC -XX:+ExitOnOutOfMemoryError"

ENTRYPOINT ["sh","-c","java $JAVA_OPTS -jar auth-service.jar"]
