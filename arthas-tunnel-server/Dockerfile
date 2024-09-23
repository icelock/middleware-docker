FROM openjdk:11

WORKDIR /app

COPY arthas-tunnel-server-4.0.1-fatjar.jar /app


ENTRYPOINT ["java","-jar","arthas-tunnel-server-4.0.1-fatjar.jar"]


# java -jar -Darthas.enable-detail-pages=true arthas-tunnel-server-4.0.1-fatjar.jar