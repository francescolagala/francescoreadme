###  To setup mailgun you'll need the following dependencies:

```		
	<dependency>
		<groupId>org.springframework.boot</groupId>
		<artifactId>spring-boot-starter-mail</artifactId>
	</dependency>	
	<dependency>
    	<groupId>net.sargue</groupId>
    	<artifactId>mailgun</artifactId>
    	<version>1.5.0</version>
	</dependency>
	<dependency>
   		 <groupId>com.sun.jersey</groupId>
   		 <artifactId>jersey-client</artifactId>
   		 <version>1.19.4</version>
	</dependency>
```

###  Step:
create a file credentials.properties
```
mailgun.api=□□□□□□□□□□□□□□□□□□□□□□□□□□□□□□□□□□□
mailgun.client.resource=□□□□□□□□□□□□□□□□□□□□□□□□□□□□□□□□□□□
mailgun.from=□□□□□□□□□□□□□□□□□□□□□□□□□□□□□□□□□□□
mailgun.is.enabled=false
```
ATTENTION!!! never share this file. Mailgun will disallow your account. 
(put it in your .gitignore file if you are working on a shared repository)

###  Assign Mailgun properties to send a simple message

```
package it.springbootmvc.flg.events.mailgun;

import javax.ws.rs.core.MediaType;

import org.springframework.beans.factory.annotation.Value;
import org.springframework.context.annotation.Configuration;
import org.springframework.context.annotation.PropertySource;

import com.sun.jersey.api.client.Client;
import com.sun.jersey.api.client.ClientResponse;
import com.sun.jersey.api.client.WebResource;
import com.sun.jersey.api.client.filter.HTTPBasicAuthFilter;
import com.sun.jersey.core.util.MultivaluedMapImpl;

import it.springbootmvc.flg.dto.EmployeeDTO;

@Configuration
@PropertySource("classpath:credential.properties")
public class MailgunConfig {

	@Value("mailgun.api")
	private String api;
	
	@Value("mailgun.client.resource")
	private String clientResource;
	
	@Value("mailgun.from")
	private String from;	
	
	@Value("mailgun.is.enabled")
	private Boolean isEnabled;
	
	public ClientResponse SendSimpleMessage(EmployeeDTO employeeDTO) {

		//System.out.println(mailgunFrom);
		
		if (this.isEnabled) {
			Client client = Client.create();
			client.addFilter(new HTTPBasicAuthFilter("api", this.getApi()));
			WebResource webResource = client.resource(this.getClientResource());
			MultivaluedMapImpl formData = new MultivaluedMapImpl();
			formData.add("from", this.getFrom());
			formData.add("to", ""+employeeDTO.getNameDTO()+" "+employeeDTO.getSurnameDTO()+" <"+employeeDTO.getEmailDTO()+">");
			formData.add("subject", "Registration Completed Successfully");
			formData.add("text", "Congratulations "+employeeDTO.getNameDTO()+" your registration has been successfully completed."
					+ " Your password is: "+employeeDTO.getPasswordDTO()+" please store it in a safe place. ");
			return webResource
					.type(MediaType.APPLICATION_FORM_URLENCODED)
					.post(ClientResponse.class, formData);}
		else
		{
			System.out.println("Mailgun is turned off, please check credentials.properties to turn it on");

			return null;
		}




	}

	//getters & setters

	
}

```
Attention!!! if you have some password encryption your message will result unreadable

