JWT Spring Security Demo
Screenshot from running application

About
This is a demo for using JWT (JSON Web Token) with Spring Security and Spring Boot. I completely rewrote my first version. Now this solution is based on the code base from the JHipster Project. I tried to extract the minimal configuration and classes that are needed for JWT-Authentication and did some changes.

Build Status

Requirements
This demo is build with with Maven 3.6.x and Java 11.

Usage
Just start the application with the Spring Boot maven plugin (mvn spring-boot:run). The application is running at http://localhost:8080.

You can use the H2-Console for exploring the database under http://localhost:8080/h2-console:

Screenshot from h2-console login

Backend
There are three user accounts present to demonstrate the different levels of access to the endpoints in the API and the different authorization exceptions:

Admin - admin:admin
User - user:password
Disabled - disabled:password (this user is deactivated)
There are four endpoints that are reasonable for the demo:

/api/authenticate - authentication endpoint with unrestricted access
/api/user - returns detail information for an authenticated user (a valid JWT token must be present in the request header)
/api/persons - an example endpoint that is restricted to authorized users with the authority 'ROLE_USER' (a valid JWT token must be present in the request header)
/api/hiddenmessage - an example endpoint that is restricted to authorized users with the authority 'ROLE_ADMIN' (a valid JWT token must be present in the request header)
Frontend
I've written a small Javascript client and put some comments in the code that hopefully makes this demo understandable. You can find it at /src/main/resources/static/js/client.js.

Generating password hashes for new users
I'm using bcrypt to encode passwords. Your can generate your hashes with this simple tool: Bcrypt Generator

Using another database
Actually this demo is using an embedded H2 database that is automatically configured by Spring Boot. If you want to connect to another database you have to specify the connection in the application.yml in the resource directory. Here is an example for a MySQL DB:

spring:
  jpa:
    hibernate:
      # possible values: validate | update | create | create-drop
      ddl-auto: create-drop
  datasource:
    url: jdbc:mysql://localhost/myDatabase
    username: myUser
    password: myPassword
    driver-class-name: com.mysql.jdbc.Driver
Hint: For other databases like MySQL sequences don't work for ID generation. So you have to change the GenerationType in the entity beans to 'AUTO' or 'IDENTITY'.

You can find a reference of all application properties here.

Using Flyway
#81

Docker
This project has a docker image. You can find it at https://hub.docker.com/r/hubae/jwt-spring-security-demo/.

Questions
If you have project related questions please take a look at the past questions or create a new ticket with your question.

If you have questions that are not directly related to this project (e.g. common questions to the Spring Framework or Spring Security etc.) please search the web or look at Stackoverflow.

Sorry for that but I'm very busy right now and don't have much time.

Interesting projects
spring-security-pac4j a Spring Boot integration for Pac4j (a Java security engine that covers JWT beside others)
For more complex microservice environments take a look here: Using JWT with Spring Security OAuth
