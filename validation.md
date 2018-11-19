###  Standard Validation (jaxax annotation)

We want to add a new employee using a form. So we need to validate EmployeeDTO fields.
This can be made simply adding some annotation on the fields that we need to validate

```
	@NotNull
        @Size(min=2, max=30)
	public String nameDTO;
	
	@NotNull
        @Size(min=2, max=30)
	public String surnameDTO;
	
        @NotEvil      //This will be our custom annotation for validation
	@NotNull
	public Double salaryPerHourDTO;
	
	public Integer idDTO;
```

###  Custom Annotation:

Create an annotation like this:

```
import static java.lang.annotation.ElementType.FIELD;
import static java.lang.annotation.RetentionPolicy.RUNTIME;

import java.lang.annotation.Documented;
import java.lang.annotation.Retention;
import java.lang.annotation.Target;

import javax.validation.Constraint;
import javax.validation.Payload;

@Documented
@Constraint(validatedBy = NotEvilValidator.class)
@Retention(RUNTIME)
@Target({ FIELD}) //says that this annotation can be applied just to fields
public @interface NotEvil {
	
    String message() default "Id cannot be 666";  //here you can provide a custom message
    Class<?>[] groups() default {};
    Class<? extends Payload>[] payload() default {};

}

```
Now we need a validator for this annotation:

```
import javax.validation.ConstraintValidator;
import javax.validation.ConstraintValidatorContext;

public class NotEvilValidator implements ConstraintValidator<NotEvil, Double> {

	@Override
	public void initialize(NotEvil constraintAnnotation) {
		
	}

	//This method is used to validate salaryPerHourDTO, we provided another annotation "@NotNull" on that field so
	//we must consider in our validation logic (value!=null && value==666)
  
	@Override
	public boolean isValid(Double value, ConstraintValidatorContext context) {
		
		if (value!=null && value==666)
		return false;
		else
	        return true;
	}
	
	

}

```
###  Validate EmployeeDTO

```
import org.springframework.validation.Errors;
import org.springframework.validation.Validator;
import it.springbootmvc.flg.dto.EmployeeDTO;

public class EmployeeValidator implements Validator {

        //We are using this class to validate Employees. If we use the standard annotations we can just validate fields,
	//here we can validate the whole object (in the aftermath)
	
	
        public boolean supports(Class clazz) {
        return EmployeeDTO.class.equals(clazz);
    }
   
	@Override
	public void validate(Object target, Errors errors) {
		
		 EmployeeDTO e = (EmployeeDTO) target;
		 
		 if (e.getNameDTO()!=null && e.getNameDTO().equalsIgnoreCase("francesco")) {
			 
			 errors.rejectValue("nameDTO", "8190", "I don't like this name, please use another name");
			 
		 }
		 
		
	}
}

```

###  Now we provided some constraints, but how our controller will manage this constraints?

```
//Attention to the order: @Valid must be the first and BindingResult result must follow object to validate

@RequestMapping(value = "/added", method = RequestMethod.POST)
	        public String add(@Valid @ModelAttribute("employeeDTO") EmployeeDTO employeeDTO, BindingResult result,  ModelMap model){
    
		EmployeeValidator validator = new EmployeeValidator();
		validator.validate(employeeDTO, result);
		
        //now we want that if there are some errors we well be redirected to the same form
    
		if (result.hasErrors()) {
		       return "addEmployee";
		    }	
        
        //otherwise we can procede saving the employee and giving the congrats page
		
		EmployeeDTO saved = employeeService.save(employeeDTO);
				
		return "congrats";		
	}
	

```

###  How our JSP changes?

we can use the tag <form:errors> to show the validation messages near the wrong fields

```
  <tr>
                    <td><form:label path="nameDTO">Name</form:label></td>
                    <td><form:input path="nameDTO"/>
                    <form:errors path="nameDTO" cssClass="error" /></td>
                
                </tr>
                <tr>
                    <td><form:label path="surnameDTO">Surname</form:label></td>
                    <td><form:input path="surnameDTO"/>
                    <form:errors path="surnameDTO" cssClass="error" /></td>
                    
                </tr>
                 <tr>
                    <td><form:label path="salaryPerHourDTO"> Salary</form:label></td>
                    <td><form:input path="salaryPerHourDTO"/>
                    <form:errors path="salaryPerHourDTO" cssClass="error" /></td>

```

### Convert Blanks in null

Now our form will not accept: names or surnames shortest than 2 charachters, null values, salary==666 and "francesco" as name,
but someone could fill all the forms whit blank spaces. Adding this method before the validation will help us:

```
        @InitBinder
	public void initBinder (WebDataBinder dataBinder) {
		StringTrimmerEditor ste = new StringTrimmerEditor(true);
		dataBinder.registerCustomEditor(String.class, ste);
	}
	
```
