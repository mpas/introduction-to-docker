# Copies in our code and compiles
FROM openjdk:11-jdk as builder
WORKDIR /opt/app/src
COPY /src/*.java ./
RUN javac *.java

# Perform static code analysis
FROM sonarsource/sonar-scanner-cli as sonarqube
WORKDIR /opt/app/src
COPY --from=builder /opt/app/src ./
RUN sonar-scanner -Dsonar.host.url=http://host.docker.internal:9000 -Dsonar.projectKey=helloworld -Dsonar.sources=. 

# Run unit tests
# Run integration tests

# Create application
FROM openjdk:11-jdk as application
WORKDIR /opt/app/src
COPY --from=builder /opt/app/src/*.class ./
CMD java HelloWorld
