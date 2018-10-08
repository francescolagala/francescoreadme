### First of all you'll need to add some dependency to your pom.xml :

```
<!-- tomcat.server dependencies -->
	
	<dependency>
		<groupId>org.springframework.boot</groupId>
		<artifactId>spring-boot-starter-tomcat</artifactId>
		<scope>provided</scope>
	</dependency>
	<dependency>
		<groupId>org.apache.tomcat.embed</groupId>
		<artifactId>tomcat-embed-jasper</artifactId>
	</dependency>
  
  <!-- javax servlet dependency -->
	
	<dependency>
      <groupId>javax.servlet</groupId>
      <artifactId>jstl</artifactId>
    </dependency>
			
```

### Configure a View Resolver:

```
package it.springbootmvc.flg.resolvers;

import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;
import org.springframework.web.servlet.ViewResolver;
import org.springframework.web.servlet.config.annotation.EnableWebMvc;
import org.springframework.web.servlet.config.annotation.WebMvcConfigurerAdapter;
import org.springframework.web.servlet.view.InternalResourceViewResolver;
import org.springframework.web.servlet.view.JstlView;

@Configuration
@EnableWebMvc
public class ViewConfig extends WebMvcConfigurerAdapter {

	
	@Bean
    public ViewResolver internalResourceViewResolver() {
        InternalResourceViewResolver vr = new InternalResourceViewResolver();
        vr.setViewClass(JstlView.class);
        vr.setPrefix("/WEB-INF/view/");
        vr.setSuffix(".jsp");
        vr.setOrder(1);
        return vr;
    }
}
```
### Add a simple Controller :

```
package it.springbootmvc.flg.controllers;

import org.springframework.stereotype.Controller;
import org.springframework.web.bind.annotation.RequestMapping;

@Controller
public class HelloController {

	@RequestMapping(value = "/hello")
	public String login() {

		return "hellopage";


	}
}		
```

### Create a path to store your views like in the following schema
![image](https://image.ibb.co/fcddg9/path.png)

Your hellopage.jsp 

```
<%@ page language="java" contentType="text/html; charset=ISO-8859-1"
    pageEncoding="ISO-8859-1"%>
<!DOCTYPE html>
<html>
<head>
<meta charset="ISO-8859-1">
<title>this is my hello page</title>
</head>
<body>

<h1>Hello and Welcome to this project</h1>

</body>
</html>
```


