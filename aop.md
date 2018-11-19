###  Configuration

We need a simple class to Enable aspect and configure spring to look in our package (you can leave the class empty as in the example below)
```
@Configuration
@ComponentScan("it.springbootmvc.flg.aspects")
@EnableAspectJAutoProxy
public class AspectConfig{
	
}

```

###  Create Custom Annotation

You can define when and where you want use your annotation (retention and target)

```
@Retention(RUNTIME)
@Target(METHOD)
public @interface PrintClassName {

}

```

###  Aspect Behavior

We can define a behavior based on what we need: in this case we are using a pattern proxy whit annotation @Around that is a combination
of @Before and @After. 
we must define Object proceed = joinPoint.proceed() to define when the wrapped method should run (whit @After and @Before is unnecessary)

```
        @Around("@annotation(PrintClassName)")
	public Object logExecutionTime(ProceedingJoinPoint joinPoint) throws Throwable {
		
	    logger.info("before method: class= "+this.getClass().getSimpleName()+"");
	    
	    Object proceed = joinPoint.proceed();
	 
	    logger.info("after method: class= "+this.getClass().getSimpleName()+"");
	    
	    return proceed;
	}
```

Now you can put the annotation everywhere (but only on correct targets!!!) in your project to see how it works
