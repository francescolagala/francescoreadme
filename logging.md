###  Step add a rest controller that prints messages:

Rest Controllers simplifies the process of creating RestFul Services. While the traditional MVC controller relies on the View technology, the RESTful web service controller simply returns the object
```
@RestController
@RequestMapping(value="/log/")
public class LoggingController {
 
    private final static Logger logger = LoggerFactory.getLogger(LoggingController.class);
 
    @RequestMapping("/test")
    public String index() {
        logger.trace("A TRACE Message");
        logger.debug("A DEBUG Message");
        logger.info("An INFO Message");
        logger.warn("A WARN Message");
        logger.error("An ERROR Message");
 
        return "Howdy! Check out the Logs to see the output...";
    }
}
```
Whit this simply controller we are going to show the differents levels of log. Now if we go to the page localhost:8080/log/test we will
see the result in the log and the string "howdy....." in our page

###  Logback-spring.xml configuration: define different appenders and rollover policies

```
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE xml>
<configuration>



	<appender name="STDOUT" class="ch.qos.logback.core.ConsoleAppender">
		<layout class="ch.qos.logback.classic.PatternLayout">
			<Pattern>
				%d{yyyy-MM-dd HH:mm:ss} [%thread] %-5level %logger{36} - %msg%n
			</Pattern>
		</layout>
	</appender>
	
	<appender name="LOCAL-INFO"
		class="ch.qos.logback.core.rolling.RollingFileAppender">
		<file>${CATALINA_HOME}/logs/flg/local/info.log</file>
		<encoder class="ch.qos.logback.classic.encoder.PatternLayoutEncoder">
			<Pattern>
				%d{yyyy-MM-dd HH:mm:ss} [%thread] %-5level %logger{36} - %msg%n
			</Pattern>
		</encoder>

		<rollingPolicy class="ch.qos.logback.core.rolling.TimeBasedRollingPolicy">
			<fileNamePattern>${CATALINA_HOME}/logs/flg/local/archived/info.%d{yyyy-MM-dd}.%i.log
                        </fileNamePattern>
			<timeBasedFileNamingAndTriggeringPolicy
				class="ch.qos.logback.core.rolling.SizeAndTimeBasedFNATP">
				<maxFileSize>100MB</maxFileSize>
			</timeBasedFileNamingAndTriggeringPolicy>
		</rollingPolicy>

	</appender>

	<appender name="LOCAL-ERROR"
		class="ch.qos.logback.core.rolling.RollingFileAppender">
		<filter class="ch.qos.logback.classic.filter.LevelFilter">
        <level>ERROR</level>
        <onMatch>ACCEPT</onMatch>
        <onMismatch>DENY</onMismatch>
        </filter>
		<file>${CATALINA_HOME}/logs/flg/local/error.log</file>
		<encoder class="ch.qos.logback.classic.encoder.PatternLayoutEncoder">
			<Pattern>
				%d{yyyy-MM-dd HH:mm:ss} [%thread] %-5level %logger{36} - %msg%n
			</Pattern>
		</encoder>
		<rollingPolicy class="ch.qos.logback.core.rolling.TimeBasedRollingPolicy">
			<fileNamePattern>${CATALINA_HOME}/logs/flg/local/archived/error.%d{yyyy-MM-dd}.%i.log
                        </fileNamePattern>
			<timeBasedFileNamingAndTriggeringPolicy
				class="ch.qos.logback.core.rolling.SizeAndTimeBasedFNATP">
				<maxFileSize>10MB</maxFileSize>
			</timeBasedFileNamingAndTriggeringPolicy>
		</rollingPolicy>
	</appender>
	
	<!-- Send logs to both console and file audit -->
	
	<logger name="it.springbootmvc.flg" level="INFO" additivity="false">
		<appender-ref ref="LOCAL-ERROR" />
		<appender-ref ref="LOCAL-INFO" />
		<appender-ref ref="STDOUT" />	
	</logger>
	<root level="INFO">
		<appender-ref ref="LOCAL-ERROR" />
		<appender-ref ref="LOCAL-INFO" />
		<appender-ref ref="STDOUT" />	
	</root>
	
</configuration>
```

Here we are defining 3 different appenders: first one will print messages directly in console. we can define a pattern to show messages as we need.
Second appender is an appender created to store logs on a file. it is based on catalinahome (because it is the conventional directory for many loggers).
we define also an archive in wich we want to store our logs whitin certain rolling-time-policy.
Third appender is very similar: the only difference is that we are defining a filter to accept only ERROR messages. 
(if we don't provide tags onmatch and on mismatch the filter will accept messages UP TO error level.)

Then we define the root level of our log and a logger that searchs in all the project (name="it.springbootmvc.flg").
Now if we go in the tomcat installation directory we should see the result.
