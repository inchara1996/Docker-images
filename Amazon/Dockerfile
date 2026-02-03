#Maven build

FROM maven:3.9.6-eclipse-temurin-17 AS builder

WORKDIR /app

COPY pom.xml .
COPY Amazon-Core/pom.xml Amazon-Core/pom.xml
COPY Amazon-Web/pom.xml Amazon-Web/pom.xml
COPY Amazon-Core Amazon-Core
COPY Amazon-Web Amazon-Web

RUN mvn clean install -pl Amazon-Web -am -DskipTests


# tomcat

FROM tomcat:9.0-jdk17-temurin

RUN rm -rf /usr/local/tomcat/webapps/*

COPY --from=builder /app/Amazon-Web/target/*.war /usr/local/tomcat/webapps/ROOT.war

EXPOSE 8080

CMD ["catalina.sh","run"]




