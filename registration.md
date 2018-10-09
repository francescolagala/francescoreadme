### First Step: Create a get request, we need to provide an EmployeeDTO as model and return a view whit a form.

```
	@RequestMapping(value = "/add")
	public String addEmployee(ModelMap model){
		model.addAttribute("employeeDTO", new EmployeeDTO());
		return "addEmployee";

	}
			
```

### Create addEmploye.jsp
- Note that we are using a new tag library to use the tag <form:form>

```
<%@ page language="java" contentType="text/html; charset=ISO-8859-1" pageEncoding="ISO-8859-1"%>
<%@ taglib prefix="form" uri="http://www.springframework.org/tags/form"%>

<!DOCTYPE html>
<html>
<head>
<meta charset="ISO-8859-1">
<title>Page to add a new Employee</title>
</head>
<body>

<h2>REGISTRATION FORM</h2>

<form:form  method="POST" action="added" modelAttribute="employeeDTO">
             <table>
                <tr>
                    <td><form:label path="nameDTO">Name</form:label></td>
                    <td><form:input path="nameDTO"/>
                    </td>
                
                </tr>
                <tr>
                    <td><form:label path="surnameDTO">Surname</form:label></td>
                    <td><form:input path="surnameDTO"/>
                    </td>
                    
                </tr>
                 <tr>
                    <td><form:label path="salaryPerHourDTO"> Salary</form:label></td>
                    <td><form:input path="salaryPerHourDTO"/>
                    </td>
  
                </tr>
                      
                <tr>
                    <td><button class="btn btn-default" type="submit" value="submit">Create Employee</button></td>
                </tr>
                <tr>
                    <td><button class="btn btn-default" type="reset" value="reset">Reset Values</button></td>
                </tr>
                
            </table>
        </form:form>       


</body>
</html>
			
```

### Now we must provide a service that takes our EmployeeDTO and saves it as entity (using the employeeDAO interface)

```
package it.springbootmvc.flg.services;

import it.springbootmvc.flg.dto.EmployeeDTO;

public interface EmployeeService {

	EmployeeDTO save(EmployeeDTO employeeDto);
	
}

___________________________________________________________________________________________
package it.springbootmvc.flg.services.impl;


import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Service;
import it.springbootmvc.flg.dao.EmployeeDAO;
import it.springbootmvc.flg.dto.EmployeeDTO;
import it.springbootmvc.flg.model.Employee;
import it.springbootmvc.flg.services.EmployeeService;
import ma.glasnost.orika.MapperFacade;

@Service
public class EmployeeServiceImpl implements EmployeeService{
	
	
	@Autowired
	public EmployeeDAO employeeDAO;
	
	@Autowired
	public MapperFacade mapper;
	

	@Override
	public EmployeeDTO save(EmployeeDTO employeeDTO) {
		Employee entity = mapper.map(employeeDTO, Employee.class);
		Employee saved = employeeDAO.save(entity);
		employeeDTO.setIdDTO(saved.getId());
		return employeeDTO;
	}

	

}

			
```

### Now we can inject the service in our controller and provide a POST request 

```

@RequestMapping(value = "/added", method = RequestMethod.POST)
	public String add(@ModelAttribute("employeeDTO") EmployeeDTO employeeDTO,  ModelMap model){
		
		EmployeeDTO saved = employeeService.save(employeeDTO);
				
		return "congrats";		
	}
	
			
```

### Last but not least we need a congrats.jsp 

```

<%@ page language="java" contentType="text/html; charset=ISO-8859-1"
    pageEncoding="ISO-8859-1"%>
<!DOCTYPE html>
<html>
<head>
<meta charset="ISO-8859-1">
<title>Congratulation Page</title>
</head>
<body>

<h1>CONGRATULATION !!! successfully added an employee</h1>

</body>
</html>
	
			
```

###TIPS: try to check your database h2, if you've done everything right registring a new employee you shoud se him in the table.
