FROM ubuntu:latest AS build

RUN apt-get update && apt-get install -y openjdk-17-jdk maven

WORKDIR /app
COPY demo /app

RUN mvn clean install

FROM openjdk:17-jdk-slim

EXPOSE 8080

ENV PORT 8080

COPY --from=build /app/target/*.jar app.jar

ENTRYPOINT ["java", "-Dserver.port=${PORT}", "-jar", "app.jar"]
