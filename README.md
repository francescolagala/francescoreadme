# Spring-Boot-Mvc Application

Hello and welcome.
This guide walks you through the process of creating a simple Spring Boot based application from scratch. 

## Getting Started (Prerequisites)

We can start istalling the following softwares:

- Spring Tool Suite 3.9.5
- Maven 3.5.4
- Tomcat 9.0.10
- Java 8 

[![image](https://image.ibb.co/b694Op/image.png)](installation.md)
### VIEW-CONTROLLER

- Configure a view resolver
- First controller
- First jsp page

[![image](https://image.ibb.co/b694Op/image.png)](viewresolver.md)
[![image](https://image.ibb.co/c2Bxg9/springgood.png)](https://www.baeldung.com/spring-mvc-view-resolver-tutorial)


### 3 tier architechture:

[![image](https://image.ibb.co/cKBtKU/wiki.png)](https://en.wikipedia.org/wiki/Multitier_architecture#Three-tier_architecture)


- Employee
- EmployeeDTO
- EmployeeDAO implementing JpaRepository
- EmployeeMapper implementing OkiraMapperFactoryConfigurer
- Connect to H2 (set up application.properties, create a data-h2.sql to populate database)

[![image](https://image.ibb.co/b694Op/image.png)](3layers.md)

### Model View Controller

- reach the Model through a service layer
- create a registration form in our View
- implement a POST request in our Controller

[![image](https://image.ibb.co/b694Op/image.png)](registration.md)

### Validation

- Standard validation (javax annotations)
- Create a custom annotation to validate a field
- Create a custom Validator to validate EmployeeDTO objects
- Help to validation: Convert blanks in Null values before validation

[![image](https://image.ibb.co/b694Op/image.png)](validation.md)

### Logging

- Logging rest controller to print logging levels : (trace, debug, info, error, warn)
- Logback-spring.xml configuration: define different appenders and rollover policies

[![image](https://image.ibb.co/b694Op/image.png)](logging.md)

### AoP - Aspect oriented Programming.

[![image](https://image.ibb.co/b694Op/image.png)](aop.md)

### Async Event / Mail (Mailgun)

[![image](https://image.ibb.co/b694Op/image.png)](async.md)

### Spring boot security Configuration

[![image](https://image.ibb.co/b694Op/image.png)](security.md)

### Adding a new Class Project. many-to-many hibernate configuration.

[![image](https://image.ibb.co/b694Op/image.png)](m2m.md)

### Ajax: Make a simple call. Testing whit postman.

[![image](https://image.ibb.co/b694Op/image.png)](postman.md)

### Ajax: Using Javascript an Jquery to perform a real ajax call.

[![image](https://image.ibb.co/b694Op/image.png)](js.md)

### Cronjob - CSV import

[![image](https://image.ibb.co/b694Op/image.png)](cronjob.md)

### Upload an image (Serialization and Deserialization)

[![image](https://image.ibb.co/b694Op/image.png)](upload.md) 

### Spring JMS. Manage a queue whit activeMQ

[![image](https://image.ibb.co/b694Op/image.png)](jms.md)


