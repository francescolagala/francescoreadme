###  Download Postman:

###  Rest Controller:

```
@RestController
@RequestMapping("/projects")
public class AjaxController {
	
	@Autowired
	public ProjectService ps;
	
	@RequestMapping(value = "/{id}", method = {RequestMethod.GET})
	public ProjectDTO getStartDate(@RequestParam ("id") Integer id) {
		 
	return ps.retrieveProjectById(id); 
	}

```

###  Simulate a call whit postman:

- Disable Spring Security.
- Configure postman call:

![image](https://image.ibb.co/mbCuX0/Postman.png)

###  Send the call and look for result.

TIPS: you can choose a format for response: xml, json, etc..
