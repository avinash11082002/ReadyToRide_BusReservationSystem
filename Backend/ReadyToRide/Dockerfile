FROM openjdk:17-jdk-slim

WORKDIR /app

# Copy Maven wrapper and pom.xml
COPY mvnw .
COPY mvnw.cmd .
COPY .mvn .mvn
COPY pom.xml .

# Make mvnw executable
RUN chmod +x ./mvnw

# Download dependencies
RUN ./mvnw dependency:go-offline -B -s .mvn/settings.xml

# Copy source code
COPY src src

# Build the application
RUN ./mvnw clean package -DskipTests -s .mvn/settings.xml

# Expose port
EXPOSE 8080

# Run the application
CMD ["java", "-Dspring.profiles.active=prod", "-jar", "target/ReadyToRide-0.0.1-SNAPSHOT.jar"]