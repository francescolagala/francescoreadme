###  Download Postman:

###  Rest Controller:

```
@RestController
@RequestMapping("/projects")
public class AjaxController {
	
	@Autowired
	public ProjectService ps;
	
	@RequestMapping(value = "/{id}", method = {RequestMethod.GET})
	public ProjectDTO getProject(@RequestParam ("id") Integer id) {
		 
	return ps.retrieveProjectById(id); 
	}

```

###  Simulate a call whit postman:

- Disable Spring Security.
- Configure postman call:

![image](https://image.ibb.co/mbCuX0/Postman.png)

###  Send the call and look for result.

TIPS: you can choose a format for response: xml, json, etc..

###  example.jsp :

```
<%@ taglib prefix="c" uri="http://java.sun.com/jsp/jstl/core" %>

<custom:mainLayout title="projectlist">
<jsp:body>

<h1> Lista progetti</h1>

<c:forEach items="${projects}" var="p">
<a class="tell-project-name" id="{p.id}" href="/getprojectname">Click for Project ${p.id} Name</a>
</c:forEach>
<script type="text/javascript" src="/static/js/example.js"></script>

</jsp:body>
</custom:mainLayout>

```

###  example.js (static/js/example.js):

We are listening for events "click" on element whit class="tell-project-name".
When someone clicks we have to retrieve the correct id
Then we perform an ajax call
And we use the result to retrieve the project name.

```
$('.tell-project-name').on('click', () => {

var retrievedid= /*... implement a way to retrieve project id ...*/ ;

var myObj = {
    		id: retrieveid,  			
    };
		
$.ajax({
        type: 'GET',
        contentType: 'application/json',
        url:  'projects'+id,
        data: JSON.srtingify(myObj),
        async: true,
        success: function(result) {
            alert('Project name: '+result.projectname); //projectname must be a real field of projectDTO class...
        }
   	});
	});

```

