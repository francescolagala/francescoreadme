###  First of all we need a way to make our event Asynch:

We've choosen to use a Multicaster

```
@Configuration
public class AsynchronousSpringEventsConfig {
    @Bean(name = "applicationEventMulticaster")
    public ApplicationEventMulticaster simpleApplicationEventMulticaster() {
        SimpleApplicationEventMulticaster eventMulticaster 
          = new SimpleApplicationEventMulticaster();
         
        eventMulticaster.setTaskExecutor(new SimpleAsyncTaskExecutor());
        return eventMulticaster;
    }
}
```

###  Create a custom event:

We need to send a registration mail to our employees. so we need 2 simple methods:
retrieve the employee and send the mail.

```
public class MyEvent extends ApplicationEvent {
	
    private EmployeeDTO employeeDTO;
 
    public CustomSpringEvent(Object source, EmployeeDTO employeeDTO) {
        super(source);
        this.employeeDTO=employeeDTO;
    }
    
	public EmployeeDTO getEmployeeDTO() {
		return employeeDTO;
	}
	
	public void sendRegistrationMail() {
		
		MailgunConfig mailgun = new MailgunConfig();
		mailgun.SendSimpleMessage(employeeDTO);
	};
	
}


```

###  Create an Event Listener:

```
@Component
public class MyEventListener implements ApplicationListener<MyEvent> {
	
    @Override
    public void onApplicationEvent(MyEvent event) {
        //receiving custom event
    	
    	event.sendRegistrationMail();
    }
}
```
###  Crete and inject an envent publisher:

```

@Service
public class MyEventPublisher implements CustomSpringEventPublisherInterface{
	
    @Autowired
    private ApplicationEventPublisher applicationEventPublisher;
 
    public void doStuffAndPublishAnEvent(EmployeeDTO employeeDTO) {
        
        MyEvent event = new MyEvent(this, employeeDTO);
        applicationEventPublisher.publishEvent(event);
    }
}

```

We will inject this publisher in our EmployeeService because we need to send an email just on employee registration.
TIPS: if need to publish several event you can use AOP.

EmployeeService class:
```
@Autowired
public CustomSpringEventPublisherInterface publisher;
  
@Override
@AopAnnotation
public EmployeeDTO save(EmployeeDTO employeeDTO) {
		
...
  
publisher.doStuffAndPublishAnEvent(employeeDTO);
  
...
  
}

```
