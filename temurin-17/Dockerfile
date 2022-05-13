#FROM openjdk:11-jre-slim
FROM maven:3-eclipse-temurin-17

ADD config/settings.xml /root/.m2/settings.xml

ENTRYPOINT ["/usr/local/bin/mvn-entrypoint.sh"]
CMD ["mvn"]