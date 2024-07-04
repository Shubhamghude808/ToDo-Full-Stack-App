# ToDo Full Stack Application with Spring Boot and React
<img src="https://github.com/Shubhamghude808/ToDo-Full-Stack-App/assets/112695994/cee0ffc6-28f9-4e76-bbf6-f16153e89661" alt="Example Image" width="300">

## Features

- **User Authentication**: Secure user registration and login using JWT (JSON Web Tokens).
- **Task Management**: Create, read, update, and delete tasks.
- **Responsive Design**: User-friendly interface that works on both desktop and mobile devices.
- **RESTful API**: Backend API endpoints for managing users and tasks.
- **Database Integration**: Persistent storage of user and task data using a relational database (e.g., MySQL or PostgreSQL).
- **Validation and Error Handling**: Comprehensive validation and error handling on both frontend and backend.

## Technologies Used

- **Backend**: 
  - Spring Boot
  - JSON web token(JWT) (for authentication and authorization)
  - Spring HATEOAS (for creating REST representations)
  - JPA/Hibernate (for database interactions)
  - H2/MySQL (for database)
  - Swagger (for generating documents of REST APIs)
  
- **Frontend**:
  - React
  - Axios (for API calls)
  - React Router (for navigation)
  - React useState Hook (for state management)

## Running the Application

- REST API - Import into Eclipse as Maven Project. Run `restfulwebservices.RestfulWebServicesApplication` as a Java Application. Check Authentication and REST API Sections for executing REST APIs.
- React Application - Import `frontend/todo-app` into Visual Studio Code. Run `npm install` followed by `npm start`
- http://localhost:3000/ with credentials Shubham/git808
  
### Default Credentials

- **Username**: `Shubham`
- **Password**: `git808`
  
> Look at  `Creating New Users` section for creating new users.



## Authentication

All REST API are protected by JWT Authentication with Spring Security. 

POST to http://localhost:5000/authenticate

```
{
  "username":"Shubham",
  "password":"git808"
}
```

Response
```
{
"token": "eyJhbGciOiJIUzUxMiJ9.eyJzdWIiOiJpbjI4bWludXRlcyIsImV4cCI6MTU2MjIzNDM1OSwiaWF0IjoxNTYxNjI5NTU5fQ.yvkFtYAp8yGClDo7D5wtXyPSnUPtxu8A7A9YCl9FJdjR0di_yAaPcSTR6liN5bIu1SnOJuSZp94pYSYzU_BNEw"
}
```

Use the token in the headers for all subsequent requests.

`Authorization` : `Bearer ${token}`

Example 

`Authorization` : `Bearer eyJhbGciOiJIUzUxMiJ9.eyJzdWIiOiJpbjI4bWludXRlcyIsImV4cCI6MTU2MjIzNDM1OSwiaWF0IjoxNTYxNjI5NTU5fQ.yvkFtYAp8yGClDo7D5wtXyPSnUPtxu8A7A9YCl9FJdjR0di_yAaPcSTR6liN5bIu1SnOJuSZp94pYSYzU_BNEw`


## Creating New Users

Look at /src/main/resources/data.sql for existing users.

You can create new users by encrypting password with Bcrypt - Use Rounds 10 - https://www.browserling.com/tools/bcrypt 

```
INSERT INTO USER (ID, USERNAME, PASSWORD, ROLE) 
VALUES (3, 'USERNAME', 'BCRYPT_ENCRyPTED_PASSWORD','ROLE_USER');
```


## Hello World URLS

- http://localhost:5000/hello-world

```txt
Hello World
```

- http://localhost:5000/hello-world-bean

```json
{"message":"Hello World - Changed"}
```

- http://localhost:5000/hello-world/path-variable/in28minutes

```json
{"message":"Hello World, in28minutes"}
```

## TODO Resource Details

- GET - http://localhost:5000/users/in28minutes/todos

```
[
  {
    "id": 10001,
    "username": "Shubham",
    "description": "Learn JPA",
    "targetDate": "2019-06-27T06:30:30.696+0000",
    "done": false
  },
  {
    "id": 10002,
    "username": "Shubham",
    "description": "Learn Data JPA",
    "targetDate": "2019-06-27T06:30:30.700+0000",
    "done": false
  },
  {
    "id": 10003,
    "username": "Shubham",
    "description": "Learn Microservices",
    "targetDate": "2019-06-27T06:30:30.701+0000",
    "done": false
  }
]
```

#### Retrieve a specific todo

- GET - http://localhost:5000/users/in28minutes/todos/10001

```
{
  "id": 10001,
  "username": "Shubham",
  "description": "Learn JPA",
  "targetDate": "2019-06-27T06:30:30.696+0000",
  "done": false
}
```

#### Creating a new todo

- POST to http://localhost:5000/users/in28minutes/todos with BODY of Request given below

```
{
  "username": "Shubham",
  "description": "Learn to Drive a Car",
  "targetDate": "2030-11-09T10:49:23.566+0000",
  "done": false
}
```

#### Updating a new todo

- http://localhost:5000/users/in28minutes/todos/10001 with BODY of Request given below

```
{
  "id": 10001,
  "username": "Shubham",
  "description": "Learn to Drive a Car",
  "targetDate": "2045-11-09T10:49:23.566+0000",
  "done": false
}
```

#### Delete todo

- DELETE to http://localhost:5000/users/in28minutes/todos/10001

## H2 Schema - Created by Spring Boot Auto Configuration

```
Hibernate: drop table todo if exists
Hibernate: drop table user if exists
Hibernate: drop sequence if exists hibernate_sequence
Hibernate: drop sequence if exists user_seq
Hibernate: create sequence hibernate_sequence start with 1 increment by 1
Hibernate: create sequence user_seq start with 1 increment by 1
Hibernate: create table todo (id bigint not null, description varchar(255), is_done boolean not null, target_date timestamp, username varchar(255), primary key (id))
Hibernate: create table user (id bigint not null, password varchar(100) not null, role varchar(100) not null, username varchar(50) not null, primary key (id))
Hibernate: alter table user add constraint UK_sb8bbouer5wak8vyiiy4pf2bx unique (username)
```


## H2 Console

- http://localhost:5000/h2-console
- Use `jdbc:h2:mem:testdb` as JDBC URL 

