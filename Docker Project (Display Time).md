
1 Frontend( NodeJS)

2 Backend (NodeJS)

3 Database  (Postgres)


Traffic flow

user -> frontend -> backend -> database

==Deployment flow== (Establish )

Database -> Backend -> Frontend


==Docker Network

If we want to establish a communication b/t 2 contaibers then we need to run that containers in same network

In docker we have 3 default networks
   1 bridge ( it will assign separate ip for each container) in realtime we will use bridge network
   2 host  ( our host ip will bind or assign to the container ) so we can create only one container when we use network as host
   3 none   ( our container will not get any ip) 

If we create any custom network then by default it will use bridge network


In docker we will use container names to talk with other container


postgress
==========

docker network create networkname 

docker run -d --name containername  -p hostport:containerport --network networkname  imagename

docker network create timing




docker run -d --name  postgres -e POSTGRES_DB=timing -e POSTGRES_USER=timingadmin -e POSTGRES_PASSWORD=mypassword11 --network timing postgres
docker ps

 docker inspect postgres | grep -i image    ip    network 



Backend
==========

docker run -d --name backend-api -p 3000:3000 -e PORT=3000 -e DB=timing -e DBUSER=timingadmin -e DBHOST=postgres -e DBPORT=5432 -e DBPASS=mypassword11 --network timing vinod99998888/node_app_backend 

docker ps

docker logs -f backend-api



frontend
==========

docker run -d --name frontend  -p 3001:3001 -e PORT=3001 -e API_HOST=http://backend-api:3000 --network timing vinod99998888/node_web_frontend


docker logs -f frontend



Multi stage Dockerfile
===========================

# ------------ Stage 1: Build the application ------------
FROM maven:3.9.6-eclipse-temurin-17 AS builder

# Set working directory
WORKDIR /app

# Copy pom.xml and download dependencies
COPY pom.xml .
RUN mvn dependency:go-offline

# Copy the source code
COPY src ./src

# Package the application (skip tests for faster build)
RUN mvn package -DskipTests

# ------------ Stage 2: Create the runtime image ------------
FROM eclipse-temurin:17-jre

# Set working directory
WORKDIR /app

# Copy the jar file from the builder stage
COPY --from=builder /app/target/*.jar app.jar

# Command to run the jar
ENTRYPOINT ["java", "-jar", "app.jar"]This is your new *vault*.

Make a note of something, [[create a link]], or try [the Importer](https://help.obsidian.md/Plugins/Importer)!

When you're ready, delete this note and make the vault your own.