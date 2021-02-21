# Spring Boot - JWT Authentication using Spring Security & Spring Data JPA

## Dependency - database connection

```xml
<dependency>
  <groupId>mysql</groupId>
  <artifactId>mysql-connector-java</artifactId>
  <scope>runtime</scope>
</dependency>
```
## Application properties
The `application.properties` file should look like this :

```
spring.datasource.url= jdbc:mysql://localhost:3306/testdb?useSSL=false
spring.datasource.username= root
spring.datasource.password= 123456

spring.jpa.properties.hibernate.dialect= org.hibernate.dialect.MySQL5InnoDBDialect
spring.jpa.hibernate.ddl-auto= update

# App Properties
akashneil.app.jwtSecret= akashNeilSecretKey
akashneil.app.jwtExpirationMs= 86400000
```
## Run Spring Boot application
```
mvn spring-boot:run
```

## Setting up the database entries

Run following SQL insert statement

```
INSERT INTO roles(name) VALUES('ROLE_ADMIN');
INSERT INTO roles(name) VALUES('ROLE_MODERATOR');
INSERT INTO roles(name) VALUES('ROLE_USER');
```

The result should be like this:

|   id	|   name	     |
|---	|---	         |
|   1	| ROLE_ADMIN	 | 
|   2	| ROLE_MODERATOR |   
|   3	| ROLE_USER	     |

## Using the application 
### User Registration, User Login and Authorization process

To register a user, go to ``http://localhost:8080/api/auth/signup``

and send the following ``json`` as a ``POST`` :

```json
{ 
"username": "neil",
"email": "akash@neil.com", 
"password": "1234567",
"role": ["mod","user"]
}
```
To log in (``/api/auth/signin``), use ``POST`` and send json in the format :

```json
{
"username": "neil", 
"password": "1234567"
}
``` 

It will return something like the following :

```json
{
    "id": 1,
    "username": "neil",
    "email": "akash@neil.com",
    "roles": [
        "ROLE_USER",
        "ROLE_MODERATOR"
    ],
    "accessToken": "eyJhbGciOiJIUzUxMiJ9.eyJzdWIiOiJuZWlsIiwiaWF0IjoxNjEzOTIzMTQwLCJleHAiOjE2MTQwMDk1NDB9.Vzo6kaXVfdyp9qX3iIee3m0B0JlZe2urWEOn4qnBnyljxx-AN_n0dat_IJb8MXsZEY5p0VW4GS3IKpGPa43xuA",
    "tokenType": "Bearer"
}
```

To access user details, go to ``/api/test/user`` and do a ``GET`` after entering the above bearer access token in the header :

![user content](user_content.png)




