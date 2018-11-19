###  Import bootstrap and jquery dependency:

NB: There are several ways to get bootstrap and jquery. This is a back-end based application so we choose to import them whit maven.
In a complete application is preferable to import this dependency whit softwares like npm.

```
        <dependency>
           <groupId>org.webjars</groupId>
           <artifactId>bootstrap</artifactId>
           <version>3.3.7-1</version>
        </dependency>
        <dependency>
           <groupId>org.webjars</groupId>
           <artifactId>jquery</artifactId>
           <version>3.1.1</version>
        </dependency>
```

###  Configure Resource Handler:

```
@Configuration
@EnableWebMvc
public class MvcConfig extends WebMvcConfigurerAdapter {

  ...

@Override
	public void addResourceHandlers(ResourceHandlerRegistry registry) {
	    registry
	      .addResourceHandler("/static/**")
	      .addResourceLocations("/static/");
	    
	    registry.addResourceHandler("/jquery/**") //
        .addResourceLocations("classpath:/META-INF/resources/webjars/jquery/3.1.1/");

        registry.addResourceHandler("/bootstrap/**") //
        .addResourceLocations("classpath:/META-INF/resources/webjars/bootstrap/3.3.7-1/");	      
	}
  
  ...

```

###  Create a paths to store static resources and tags:

![image](https://image.ibb.co/hBNskL/frontend-path.png)

###  Create mainLayout.tag:

In the head you must load bootstrap and jquery min js so you'll get them in every page that uses this main layout.
Tag <jsp:doBody> indicates where the body will be generated.

```
<jsp:directive.attribute name="title" required="true" rtexprvalue="true" />
<!DOCTYPE>
<html>
<head>
    <title>${title}</title>
    <meta charset="UTF-8">
    <meta name="description" content="employee project">
    
    <link href="/static/css/style.css" rel="stylesheet"/>  
    <link href="/bootstrap/css/bootstrap.min.css" rel="stylesheet"/>
    <script src="/jquery/jquery.min.js"></script> 
    
    
    
</head>
<body>

        <jsp:doBody />
   
</body>

</html>

```

###  Create custom style.css:

```
h1{
color:red
}

...other properties...

```

###  Apply main layout to your jsp:

```

<custom:mainLayout title="homepage">
<jsp:body>

<h1> ... here goes your jsp body... this message will be red (because we defined this property in mystyle.css) </h1>

<a class="btn btn-default" href="/somewhere">Go somewhere</a>

</jsp:body>
</custom:mainLayout>

```

NOW YOU CAN USE SOME CLASSES PROVIDED BY BOOTSRAP CSS or you can define other properties in your style.css
. An example is class="btn btn-default" provided by bootsrap and the red color for text in tag h1 defined in style.css

