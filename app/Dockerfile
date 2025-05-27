# Build stage
FROM --platform=$BUILDPLATFORM mcr.microsoft.com/openjdk/jdk:17-ubuntu AS builder
WORKDIR /app

# Copy only the necessary files for building
COPY ./app .

# Make mvnw executable and install dependencies
RUN chmod +x mvnw && \
    apt-get update && \
    apt-get install -y tar curl && \
    ./mvnw clean package -DskipTests && \
    ls -l target/ && \
    cp target/*.jar target/app.jar

# Runtime stage
FROM --platform=$TARGETPLATFORM mcr.microsoft.com/openjdk/jdk:17-ubuntu
WORKDIR /app
COPY --from=builder /app/target/app.jar app.jar
RUN ls -l /app/
EXPOSE 8080
ENTRYPOINT ["java", "-jar", "app.jar"] 