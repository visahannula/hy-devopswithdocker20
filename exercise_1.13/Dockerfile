FROM openjdk:8

EXPOSE 8080

WORKDIR /
RUN ["git", "clone", "https://github.com/docker-hy/spring-example-project.git"]

WORKDIR /spring-example-project
RUN ["./mvnw", "package"]

ENTRYPOINT [ "java" ]
CMD ["-jar", "./target/docker-example-1.1.3.jar"]