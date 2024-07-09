# Step 1: Build the application using the official Maven image
FROM maven:latest as build

# Set the working directory in the Docker image
WORKDIR /app

# Copy the Maven configuration file
COPY pom.xml .

# Copy the source code of the application
COPY src ./src

# Package the application
RUN mvn clean package -DskipTests

# Step 2: Create the final image with OpenJDK 17
FROM openjdk:17

# Set the working directory in the Docker image
WORKDIR /app

# Copy the built jar file from the build stage
COPY --from=build /app/target/*.jar app.jar

# Command to run the application
ENTRYPOINT ["java", "-jar", "app.jar"]