# Build stage
FROM --platform=$BUILDPLATFORM mcr.microsoft.com/openjdk/jdk:17-ubuntu AS builder
WORKDIR /app
COPY . .
RUN apt-get update && apt-get install -y tar curl && ./mvnw clean package -DskipTests

# Runtime stage
FROM --platform=$TARGETPLATFORM mcr.microsoft.com/openjdk/jdk:17-ubuntu
WORKDIR /app
COPY --from=builder /app/target/*.jar app.jar
EXPOSE 8080
ENTRYPOINT ["java", "-jar", "app.jar"] 