###  Enable Scheduling:

Simply put this annotation on your main class

```
@EnableScheduling

```

###  Simple Cronjob:

```
@Service
public class ScheduledLog {
	
  private final static Logger logger = LoggerFactory.getLogger(LoggingController.class);

	@Scheduled(fixedRate = 60000) //rate in millisecond === 60s
	public void getTime() {
  
  logger.info("current time is:"+System.currentTimeMillis());
  
  }
			
	}
```

###  CSV import: CsvMapper (interface):

Add fasterxml dependency.

```
    <dependency>
       <groupId>com.fasterxml.jackson.dataformat</groupId>
       <artifactId>jackson-dataformat-csv</artifactId>       
    </dependency>
    
```   

```
public interface CsvMapper {

	String fileToString() throws IOException;

	Map<Integer, String> lineEncoding(String s);
	
}

```

###  images.csv:

Our csv follows the pattern key,value

```
2,https://www.mastersonstaffing.com/wp-content/themes/Masterson/images/testimonials.jpg
```
where the key is the employee id and the value is the image path.

###  CSV import: CsvMapperImpl:

This is a custom implementation based on previous csv file.

```
@Service
public class CsvMapperImpl implements CsvMapper{
	
	@Override
	public String fileToString() throws IOException {
		
		    String userDir = System.getProperty("user.dir");
			
		    String myFilePath= userDir+"\\src\\main\\webapp\\imagesCsv";
		    
			  BufferedReader br = new BufferedReader(new FileReader(myFilePath));
		  	String result= br.readLine();
		  	br.close();
		    return result;
			
	}
	
	@Override
    public Map<Integer, String> lineEncoding(String s) {
			
		String[]splitted = s.split(",");
				
		Map <Integer,String> map = new HashMap <Integer,String>();
		
		for (int i=0; i<(splitted.length)/2;i++) {
			
			map.put((Integer.parseInt(splitted[2*i])), (splitted[(2*i)+1]));
		
		}
		
		return map;
		
	}
	

}
```

###  Set images link retrieved by csv into employees every day :

```

    @Scheduled(fixedRate = 86400000) //time in milliseconds === 1 day
    public void saveImageFromCsvToRespectiveEmployee() throws IOException {
		
		String s = mapper.fileToString();
		Map <Integer,String> map = mapper.lineEncoding(s);
		
		for (Map.Entry<Integer, String> entry : map.entrySet()) {
    
		EmployeeDTO imageToSaveEmployee = es.retrieveById(entry.getKey());
		imageToSaveEmployee.setImageDTO(entry.getValue());
		es.update(imageToSaveEmployee);	
		}
		

```
