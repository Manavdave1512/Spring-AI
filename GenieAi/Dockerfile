# Build stage
FROM maven:3.6.3-openjdk-8 AS build
WORKDIR /app
COPY pom.xml . 
RUN mvn dependency:go-offline
COPY . .
RUN mvn clean package -DskipTests

# Run stage
FROM openjdk:8-jdk-slim
WORKDIR /app
EXPOSE 8080
COPY --from=build /app/target/GenieAi-0.0.1-SNAPSHOT.jar app.jar
ENTRYPOINT ["java", "-Xmx256m", "-Xms128m", "-jar", "app.jar"]
