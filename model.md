###  ImageController:

Image Facade must implement methods to store file somewhere. 
TIPS: you can convert the file in bytes and store it in your database as Blob.

```
@Autowired
ImageFacade imageFacade;



@RequestMapping(value = "/upload", method = {RequestMethod.POST})
@ResponseStatus(value = HttpStatus.OK)
	public void upload(@RequestParam("file") MultipartFile filez,@RequestParam("ownerId") Integer ownerId) throws IOException, ElementNotFound {

		imageFacade.saveEmployeeImage(ownerid, filez);
    
	}
	

```

###  ImageFacade:

Here we use a custom FileService interface It provides 2 method to serialize/deserialize a file and store it on a paht.

```
void saveToPath(MultipartFile fileToSave) throws IOException;
String getPathToString(MultipartFile fileToGetPath);
```

```
@Service
public class ImagesFacadeImpl implements ImageFacade {
	
	@Autowired
	public FileService fileService;     
	
	@Autowired
	public EmployeeService es;
	
	public void saveEmployeeImage(ownerid, filez) throws IOException, ElementNotFound{

    saver.saveToPath(filez);	
		EmployeeDTO imageToSaveEmployee = es.retrieveById(ownerId);
		imageToSaveEmployee.setImageDTO(saver.getPathToString(filez));
		es.update(imageToSaveEmployee);				    
    
	}
		

```

###  Form to upload a file:

```
      <h3>File Upload:</h3>
      Select a file to upload: <br />
      <form action = "upload" method = "post"
         enctype = "multipart/form-data">
         <input type = "file" name = "file" size = "50" />
         <br />
         <input type = "hidden" name = "ownerid" value= "${employee.id} />
         <input type = "submit" value = "Upload File" />
      </form>

```

###  Handle Exception:

```
@ControllerAdvice
public class ExceptionHandlerController {

	  
	  @ResponseStatus(code = HttpStatus.USUPPORTED_MEDIA_TYPE)
	  @ExceptionHandler(value = IOException.class)
	  public String handleTeapot(IOException ex) {
	    
	    return "failedtowritefile";
	  }
	  
	  @ResponseStatus(HttpStatus.NOT_FOUND)
	  @ExceptionHandler(value = ElementNotFound.class)
	  public String elementNotFound(ElementNotFound ex) {
	    
	    return "notfound";
	  }


}

```


