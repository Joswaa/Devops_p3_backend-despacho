# 1: build con Maven
FROM maven:3.9-eclipse-temurin-17 AS build

WORKDIR /app

COPY pom.xml .
COPY src ./src

RUN mvn clean package -DskipTests

# 2: imagen final
FROM eclipse-temurin:17-jdk-alpine

WORKDIR /app

COPY --from=build /app/target/*.jar app.jar

ENV DB_ENDPOINT=localhost \
    DB_PORT=3306 \
    DB_NAME=test \
    DB_USERNAME=root \
    DB_PASSWORD=changeme

EXPOSE 8081

CMD ["java", "-jar", "app.jar"]