# Spring-Boot-Mvc Application

Hello and welcome.
This guide walks you through the process of creating a simple Spring Boot based application from scratch. 

## Getting Started (Prerequisites)

We can start istalling the following softwares:

- Spring Tool Suite 3.9.5
- Maven 3.5.4
- Tomcat 9.0.10
- Java 8 

[![image](https://image.ibb.co/ktS01L/sett.png)](installation.md)

### VIEW-CONTROLLER

- Configure a view resolver
- First controller
- First jsp page

[![image](https://image.ibb.co/c2Bxg9/springgood.png)](https://www.baeldung.com/spring-mvc-view-resolver-tutorial)
[![image](https://image.ibb.co/cKBtKU/wiki.png)](https://en.wikipedia.org/wiki/Model%E2%80%93view%E2%80%93controller)
[![image](https://image.ibb.co/kbE3op/solution_2480514_1280.png)](viewresolver.md)

### 3 tier architechture:

- Employee
- EmployeeDTO
- EmployeeDAO implementing JpaRepository
- EmployeeMapper implementing OkiraMapperFactoryConfigurer
- Connect to H2 (set up application.properties, create a data-h2.sql to populate database)

[![image](https://image.ibb.co/cKBtKU/wiki.png)](https://en.wikipedia.org/wiki/Multitier_architecture#Three-tier_architecture)
[![image](https://image.ibb.co/kbE3op/solution_2480514_1280.png)](3layers.md)

### Registration Form

- reach the Model through a service layer
- create a registration form in our View
- implement a POST request in our Controller

[![image](https://image.ibb.co/c2Bxg9/springgood.png)](https://www.baeldung.com/spring-mvc-form-tutorial)
[![image](https://image.ibb.co/kbE3op/solution_2480514_1280.png)](registration.md)

### Validation

- Standard validation (javax annotations)
- Create a custom annotation to validate a field
- Create a custom Validator to validate EmployeeDTO objects
- Help to validation: Convert blanks in Null values before validation

[![image](https://image.ibb.co/c2Bxg9/springgood.png)](https://www.baeldung.com/javax-validation)
[![image](https://image.ibb.co/cKBtKU/wiki.png)](https://en.wikipedia.org/wiki/Data_validation)
[![image](https://image.ibb.co/kbE3op/solution_2480514_1280.png)](validation.md)

### Logging

- Logging rest controller to print logging levels : (trace, debug, info, error, warn)
- Logback-spring.xml configuration: define different appenders and rollover policies

[![image](https://image.ibb.co/c2Bxg9/springgood.png)](https://www.mkyong.com/logging/logback-xml-example/)
[![image](https://image.ibb.co/kbE3op/solution_2480514_1280.png)](logging.md)

### AoP - Aspect oriented Programming.

- Configuration class
- Create custom annotations
- Define aspects behavior

[![image](https://image.ibb.co/c2Bxg9/springgood.png)](https://www.baeldung.com/spring-aop-annotation)
[![image](https://image.ibb.co/cKBtKU/wiki.png)](https://en.wikipedia.org/wiki/Aspect-oriented_programming)
[![image](https://image.ibb.co/kbE3op/solution_2480514_1280.png)](aop.md)

### Spring boot security Configuration

- Custom UserDetails implementation
- Custom UserDetailsService implementation
- Basic Configuration

[![image](https://image.ibb.co/c2Bxg9/springgood.png)](https://www.baeldung.com/security-spring)
[![image](https://image.ibb.co/cKBtKU/wiki.png)](https://en.wikipedia.org/wiki/Cross-cutting_concern)
[![image](https://image.ibb.co/kbE3op/solution_2480514_1280.png)](security.md)

### Async Event

- Event Creation
- Publisher
- Listener

[![image](https://image.ibb.co/c2Bxg9/springgood.png)](https://www.baeldung.com/spring-events)
[![image](https://image.ibb.co/cKBtKU/wiki.png)](https://it.wikipedia.org/wiki/Publish/subscribe)
[![image](https://image.ibb.co/kbE3op/solution_2480514_1280.png)](async.md)

### Mailgun

- mailgun credentials.properties
- mailgun send a message whit user credentials at registration

[![image](https://image.ibb.co/kbE3op/solution_2480514_1280.png)](mailgun.md)

### Adding a new Class Project. many-to-many hibernate configuration.

- Add new classes to project
- Create a custom jointable

[![image](https://image.ibb.co/c2Bxg9/springgood.png)](https://www.baeldung.com/hibernate-many-to-many)
[![image](https://image.ibb.co/cKBtKU/wiki.png)](https://en.wikipedia.org/wiki/Many-to-many_(data_model))
[![image](https://image.ibb.co/kbE3op/solution_2480514_1280.png)](m2m.md)

### Integrate bootstrap and jquery.

- Import jquery and bootstrap dependency
- Configure Resource Resolver
- Create a custom main layout tag 
- Create a custom style.css

[![image](https://image.ibb.co/ktS01L/sett.png)](https://o7planning.org/en/10749/using-twitter-bootstrap-in-spring-boot)
[![image](https://image.ibb.co/cKBtKU/wiki.png)](https://en.wikipedia.org/wiki/JQuery)
[![image](https://image.ibb.co/cKBtKU/wiki.png)](https://en.wikipedia.org/wiki/Bootstrap_(front-end_framework))
[![image](https://image.ibb.co/kbE3op/solution_2480514_1280.png)](bootstrap.md)

### RestController: Make a simple ajax-call.

- Download Postman
- Create a rest controller
- Create a simple method
- Test it whit Postman
- Use Javascript an Jquery to perform a real ajax call

[![image](https://image.ibb.co/hYVEX0/postman.png)](https://www.getpostman.com/)
[![image](https://image.ibb.co/cKBtKU/wiki.png)](https://en.wikipedia.org/wiki/Ajax_(programming))
[![image](https://image.ibb.co/kbE3op/solution_2480514_1280.png)](postman.md)

### Upload an image (Serialization and Deserialization)

- Upload a multipart file
- Store it's bytes
- Retrieve the file

[![image](https://image.ibb.co/c2Bxg9/springgood.png)](https://www.baeldung.com/spring-file-upload)
[![image](https://image.ibb.co/cKBtKU/wiki.png)](https://en.wikipedia.org/wiki/Serialization)
[![image](https://image.ibb.co/kbE3op/solution_2480514_1280.png)](upload.md) 

### Cronjob - CSV import

- Example Cronjob: log something whit a fixedRate.
- Import values from csv every day.

[![image](https://image.ibb.co/c2Bxg9/springgood.png)](https://www.baeldung.com/spring-scheduled-tasks)
[![image](https://image.ibb.co/cKBtKU/wiki.png)](https://en.wikipedia.org/wiki/Comma-separated_values)
[![image](https://image.ibb.co/kbE3op/solution_2480514_1280.png)](cronjob.md)

### Spring JMS. Manage a queue whit activeMQ

- Installation
- Configuration
- ProducerResource / ProducerResourceImpl
- Consumer

[![image](https://image.ibb.co/ktS01L/sett.png)](http://activemq.apache.org/download.html)
[![image](https://image.ibb.co/cKBtKU/wiki.png)](https://en.wikipedia.org/wiki/Java_Message_Service)
[![image](https://image.ibb.co/kbE3op/solution_2480514_1280.png)](jms.md)


