
FROM quay.io/devfile/maven:3.8.1-openjdk-11-slim

WORKDIR /build

# Build dependency offline to streamline build
COPY pom.xml .
RUN mvn dependency:go-offline

COPY src src
RUN mvn package -Dmaven.test.skip=true

FROM openjdk:11-jdk
COPY --from=0 /build/target/listenerTrasmision-1.0.jar /app/target/listenerTrasmision-1.0.jar

EXPOSE 8081
ENTRYPOINT [ "java", "-jar", "/app/target/listenerTrasmision-1.0.jar", "--server.port=8784" ]
