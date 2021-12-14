# Grocery Service Application

## Introduction

This repository contains the source codes for the Grocery Service Application we developed. This application is web-based and linked to database through MySQL. Users are able to access to different functions within the application based on the roles signed. And the manager is capable of monitoring of the system and actions through some architectural improvements in this application.    

## Quickstart
We can simply run `make && make up` to start our service. For those that do not have `make` installed, we can effectively do the same thing by running the following:
```
docker build -t gatech/backend -f ./images/Dockerfile.backend ./backend
docker build -t gatech/frontend -f ./images/Dockerfile.frontend ./frontend
docker-compose -p gatech -f docker-compose.yml up -d
```
The first two commands are building the backend and frontend images defined by our dockerfiles, and the third is using docker-compose to deploy the service locally.
To break down the first command we can read it as "build an imageusing the `./images/Dockerfile.backend` file from the `./backend` directory and tag it as `gatech/backend`"
To break down the third command, we can read it as "deploy a service called `gatech` as defined in file `docker-compose.yml`

### docker-compose.yml
This file is well commented for additional details, and we recommend reading over this file to understand what is happening.

### Frontend
The front end service defines a single html file that calls our backend service and displays the delivery app. Our web service is deployed on port 8080
You should be able to navigate to [http://localhost:8080](http://localhost:8080) to view the page

### Backend
Our backend is a simple application controller that creates the services, saves the information to the database, and returns it as a response.
This service (as defined in our docker-compose file) is exposed on port 8080.

### Database
The database is postgres 9.6.12 for Docker.



## Instruction of manually building the application using MySQL

If you have difficulty with building the project using Docker, please follow the instruction below,

* The application can be connected to database through MySQL. Before running the application, please make sure that you have installed it.

* Please uncomment out the MySQL connection and update the MySQL database information (specifically, the "spring.datasource.username" and "spring.datasource.password") in the __"application.properties"__ under __src --> main --> resources__ folder using username and password of your MySQL connection and comment out PostgreSQL. 

* Please reload the __"pom.xml"__ in the backend folder after updating the connection information.

* Then one can manually build and run this application. 

* After running the application, please type "localhost:8080" in your web browser to start testing. Please check our video: https://www.youtube.com/watch?v=Ri6dP4TPlyU

* Because Cookie is applied in our project, please try to use "Logout" button to get back to the main page when using the web application. And if there is error related to "Invalid Cookie", please try to clear the browser history (especially the Cookies) to make the applciaiton run normally.



## Improvements

Compared with the existing project achieved in previous stages, we improved several architectural areas.

* Performance

    * We designed a web-based architecture for this project to make sure that it supports the successful implementation of both frontend and backend. Clients can interact with the application more easily.
    
    * Managers are allowed to monitor the system in realtime. We added the "View Inspection" function in manager page to provide the capability to check the running status of different components within the system, e.g., database, disk space, etc. Once the system is affected by any incidents and fall into malfunction, the manager can notice that quickly. 

* Traceability

    * Particular group of userAccounts (manager in this case) are able to track the log of actions taking place in the system. In the manager page, it allows to trace the action by entering a requestID. And the time, detailed action, and related backend documents will be retrieved.

* Authentication/Authorization

    * The Login system warrants the authentication in our application. Users will be granted with different roles and they can only access to particular functions accordingly. In the meanwhile, the application of Cookie in our project can let the system keeps record of the userAccount currently logging in. And it will make sure that the userAccounts are not able to trespass to functions that userAccounts with other roles are able to implement.  

