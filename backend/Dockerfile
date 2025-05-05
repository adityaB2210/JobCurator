# Stage 1: Build the app
FROM maven:3.9.8-eclipse-temurin-21 AS build

WORKDIR /app

# Copy only the necessary files to build the application
COPY . .

# Ensure the Maven wrapper is executable
RUN chmod +x ./mvnw

# Build the project and create the JAR
RUN ./mvnw clean package -DskipTests

# Debugging: List the contents of the target directory
RUN ls -l /app/target/

# Stage 2: Run the app
FROM eclipse-temurin:21-jdk

WORKDIR /app

# Copy the JAR file from the build stage
COPY --from=build /app/target/webApp-0.0.1-SNAPSHOT.jar /app/app.jar

EXPOSE 8080

CMD ["java", "-jar", "app.jar"]
