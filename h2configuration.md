### CONFIGURE APPLICATION PROPERTIES

```
spring.datasource.url=jdbc:h2:mem:dbflg;DB_CLOSE_DELAY=-1;DB_CLOSE_ON_EXIT=FALSE
spring.datasource.platform=H2
spring.datasource.username= root
spring.datasource.password=
spring.datasource.driver-class-name=org.h2.Driver
spring.jpa.database=H2
spring.h2.console.enabled=true
spring.h2.console.path=/h2-console
spring.h2.console.settings.trace=false
spring.h2.console.settings.web-allow-others=false
```

### ADD NEW FILES TO RESOURCES 

![image](https://image.ibb.co/nfA0w9/Cattura.png)
data-h2.sql

Populate your database:

```
INSERT INTO EMPLOYEE (name, surname, salaryperhour) VALUES ('pippo', 'baudo', '15.00');
INSERT INTO EMPLOYEE (name, surname, salaryperhour) VALUES ('marco', 'rossi', '10.00');
INSERT INTO EMPLOYEE (name, surname, salaryperhour) VALUES ('mario', 'bianchi', '8.00');
INSERT INTO EMPLOYEE (name, surname, salaryperhour) VALUES ('antonio', 'verdi', '9.00');
```



### NOW GOING TO YOU CAN CONNECT TO YOUR DATABASE (http://localhost:8080/h2-console/)

![image](https://image.ibb.co/gqbFw9/Cattura.png)


### TEST YOUR DATABASE

```
 SELECT * FROM EMPLOYEE
```
And see the the results
