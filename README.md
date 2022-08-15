#	📽 Cinema Ticket Shop

**Java web-application that provides basic functionality for the movie-theatre service. It supports customer authentication and role based authorization, basic management of movies,  movie sessions, cinema halls, and  ticket ordering procedure.**

### 🎞️️ Features
---
This back-end application provides the following functionality via specified end-points:

**Available for all customers:**
1) New user registration **POST**: `/register` (the customer acquires the role 'USER' by default, the method body should contain 'email', 'password' and 'repeatPassword' attributes. The 'email' must contain '@' symbol and one or more symbols before and after it. The 'password' must be between 8 - 40 symbols length)
2) Display all cinema halls **GET**: `/cinema-halls`
3) Display all movies **GET**: `/movies`
4) Display all movie sessions for a certain movie available on a specific date **GET**: `/movie-sessions/available` (the method accepts 'movieId' and 'date' parameters)

**Available only for ADMIN:**
1) Add a new cinema hall **POST**: `/cinema-halls`(the method body should contain 'capacity' and 'description' attributes. The 'capacity' must be 10 or more and the 'description' length must not exceed 200 characters)
2) Add a new movie **POST**: `/movies`(the method body should contain 'title' and 'description' attributes. The 'title' must be present and the 'description' length must not exceed 200 characters)
3) Add a new movie session **POST**: `/movie-sessions`(the method body should contain 'movieId', 'cinemaHallId' and 'showTime' attributes. The 'movieId' and 'cinemaHallId' must be positive values and 'showTime' must be present)
4) Update movie session by its id **PUT**: `/movie-sessions/{id}` (the method body should contain ‘movieId’, ‘cinemaHallId’ and ‘showTime’ attributes. The 'movieId' and 'cinemaHallId' must be positive values and 'showTime' must be present)
5) Delete movie session by its id **DELETE**: `/movie-sessions/{id}`
6) Dsplay customer by its email **GET**: `/users/by-email` (the method accepts 'email' parameter)

**Available only for USER:**
1) Display all orders of the currently authenticated user **GET**: `/orders`
2) Create a new order for the currently authenticated user **POST**: `/orders/complete`
3) Add a ticket to the shopping cart of currenty authenticated user **PUT**: `/shopping-carts/movie-sessions` (the method accepts 'movieSessionId' parameter)
4) Display all ticket ids from shopphing cart of the currently authenticated user **GET**: `/shopping-carts/by-user`

### 🎞️ Structure
---
The project involves 8 models (see UML diagram) and implies 3-tier architecture with dao, service and controller layers. In addition, it contains data transfer objects (dto) for requests and responses. The authorization was implemented via role based access. There are 'ADMIN' and 'USER' roles.

![image-name](UML_diagram.jpg)

### 🎞️ Technologies used
---
* JDK 11
* Maven 3
* MySql 8
* Hibernate 5
* Spring (Core, MVC, Security) 5
* Tomcat 9

### 🎞️ How to run
---
**Requirements**
* Make sure you have MySQL and Tomcat Servers installed
* Use Tomcat Server version 9 to run this project

**Instruction**
1. Create a new schema in your database
2. In order to connect to the database, provide required properties in the file `src/main/resources/db.properties`
3. Add configuration to your local Tomcat Server:
   artifact to deploy: `cinema-ticket-shop:war exploded`
   application context path: `/`
4. When you run the program you will be prompted to a login page. By default the initial credantials are: username `admin@i.ua` password `admin123`. You can change them in `src/main/java/cinema/config/DataInitializer` class.
5. In order to send POST, PUT or DELETE requests you can use Postman [link](https://www.postman.com/)
