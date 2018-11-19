### Dependencies you'll need in this step:

```
    <!--dependency added to map employee and employeeDTO  -->	
				
    <dependency>
    	<groupId>ma.glasnost.orika</groupId>
    	<artifactId>orika-core</artifactId>
    	<version>1.5.2</version>
    </dependency>
    <dependency>
    	<groupId>net.rakugakibox.spring.boot</groupId>
    	<artifactId>orika-spring-boot-starter</artifactId>
   	<version>1.6.0</version>
    </dependency>
    
    <!-- dependency for the database h2. Pay attention to the scope  -->

    <dependency>
    	<groupId>com.h2database</groupId>
    	<artifactId>h2</artifactId>
    	<scope>runtime</scope>
    </dependency>
		
    <!-- you 'll need this dependency to use jpa repository  -->
		
    <dependency>
	<groupId>org.springframework.boot</groupId>
	<artifactId>spring-boot-starter-data-jpa</artifactId>
    </dependency>
			
```

### Employee Class

Write a simple Employee Class.
@Data is a lombok annotation used to generate automatically getters setters, required arguments constructor, tostring, equals and hash.
We are using javax.persistence annotations to indicate that this class is an entity wired to a table in our database

```
package it.springbootmvc.flg.model;

import java.io.Serializable;

import javax.persistence.*;

import lombok.Data;

@Data
@Entity
@Table(name = "EMPLOYEE")
public class Employee implements Serializable{

	@Id
	@GeneratedValue(strategy= GenerationType.AUTO)
	@Column(nullable = false)
	private Integer id;
	
	@Column(nullable = false)
	private String name;
	
	@Column(nullable = false)
	private String surname;
	
	@Column(nullable = false, name="salaryperhour")
	private Double salaryPerHour;


	public Employee() {
		super();
	}
		
}
```


[![image](https://image.ibb.co/b694Op/image.png)](h2configuration.md)
Configure h2-database

### EmployeeDTO class


[![image](https://image.ibb.co/cKBtKU/wiki.png)](https://en.wikipedia.org/wiki/Data_transfer_object)


```
package it.springbootmvc.flg.dto;

import java.io.Serializable;

import lombok.Data;

@Data
public class EmployeeDTO implements Serializable{

	
	public String nameDTO;
	
	public String surnameDTO;
	
	public Double salaryPerHourDTO;
	
	public Integer idDTO;

	public EmployeeDTO() {
		super();
	}
	
	public EmployeeDTO(String nameDTO, String surnameDTO, Double salaryPerHourDTO, Integer idDTO) {
		super();
		this.nameDTO = nameDTO;
		this.surnameDTO = surnameDTO;
		this.salaryPerHourDTO = salaryPerHourDTO;
		this.idDTO = idDTO;
	}
	

}

```

### EmployeeDAO interface

[![image](https://image.ibb.co/cKBtKU/wiki.png)](https://en.wikipedia.org/wiki/Data_access_object)

This interface must extends a Repository Class (For example CRUD repository) to provide some methods to query database
It is annotated whit @Repository

```
package it.springbootmvc.flg.dao;

import org.springframework.data.jpa.repository.JpaRepository;
import org.springframework.stereotype.Repository;
import it.springbootmvc.flg.model.*;

@Repository
public interface EmployeeDAO extends JpaRepository <Employee, Integer>{
	
}

```

### EmployeeMapper

This class is annotated whit @Component 
It must implements OkiraMapperFactoryConfigurer (or some other mapper)
This class is useful to map an employee (entity) whit an employeeDTO.

TIPS: if you use the same name for properties both in entity and dto you don't need to map the fields. 
They will be mapped by naming convention.

```
package it.springbootmvc.flg.mappers;

import org.springframework.stereotype.Component;

import it.springbootmvc.flg.dto.*;
import it.springbootmvc.flg.model.*;
import ma.glasnost.orika.MapperFactory;
import net.rakugakibox.spring.boot.orika.OrikaMapperFactoryConfigurer;

@Component
public class EmployeeMapper implements OrikaMapperFactoryConfigurer{

	@Override
	public void configure(MapperFactory orikaMapperFactory) {
		orikaMapperFactory.classMap(Employee.class, EmployeeDTO.class)
		.field("name", "nameDTO")
		.field("surname", "surnameDTO")
		.field("salaryPerHour", "salaryPerHourDTO")
		.field("id", "idDTO")


		.byDefault()
		.mapNulls(false)
		.mapNullsInReverse(true)
		.register();
	}
}


```

