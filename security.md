- There are several ways to configure security. Spring boot provides a standard/basic autoconfiguration whit auto-generated login page
and some other features.
- In this project we've choosen a custom configuration strategy. 

###  Dependencies you'll need:

```
	<dependency>
	  	<groupId>org.springframework.boot</groupId>
		<artifactId>spring-boot-starter-security</artifactId>
	</dependency>
		
```

###  Custom UserDetails implementation:

Spring provides an implementation of this interface: import org.springframework.security.core.userdetails.UserDetails;

(MyUserDetails must be extended by Employee, otherwise Employee must implements UserDetails itself)

```
public class MyUserDetails implements UserDetails {

  private String username;
	
	private String password;
	
	private Roles role;
  
  ...
	
```
When you use this interface you must provide some method like

```

@Override
	public boolean getAuthorities() {
		// TODO add correct strategy to retrieve authority
		return true;
	}

```

###  Custom enum Roles:

Roles must implement GrantedAuthority 

```
public enum Roles implements GrantedAuthority{
	
	USER,
	ADMIN;

	@Override
	public String getAuthority() {
		return name();
	}

}
```

More information about Enums:
[![image](https://image.ibb.co/c2Bxg9/springgood.png)](https://www.baeldung.com/a-guide-to-java-enums)


###  Now we must implement a service to load our user:

We are going to implement the Spring interface org.springframework.security.core.userdetails.UserDetailsService; 

```
public class MyUserDetailsServiceImpl extends UserDetailsService{

@Override
	public UserDetails loadUserByUsername(String username) throws UsernameNotFoundException {

		//TODO: implement a way to retrieve users by email
		
		return null;
	}

}
```

###  Configure security:

- Our configuration class must implements org.springframework.security.config.annotation.web.configuration.WebSecurityConfigurerAdapter;

```
@Configuration
@EnableWebSecurity
public class BasicConfiguration extends WebSecurityConfigurerAdapter {
	
	@Autowired
	private UserDetailsService uds;
	
		 
	@Override
	protected void configure(AuthenticationManagerBuilder auth)
	  throws Exception {
	    auth.authenticationProvider(authenticationProvider());
      auth.userDetailsService(uds);
	}
	 
	@Bean
	public DaoAuthenticationProvider authenticationProvider() {
	    DaoAuthenticationProvider authProvider      //dao authentication strategy. Spring provides different strategies.
	      = new DaoAuthenticationProvider();
	    authProvider.setUserDetailsService(eds);    //This is our custom service
	    authProvider.setPasswordEncoder(encoder());  
	    return authProvider;
	}
	
  // To increase security we used password encoder.
  
	@Bean
	public PasswordEncoder encoder() {
	    return new BCryptPasswordEncoder(11);
	}
	 
    @Override
    protected void configure(HttpSecurity http) throws Exception {
    	
    	  http
    	     .userDetailsService(uds);
    	
        http
          .authorizeRequests()
          .antMatchers("/authentication").permitAll()
          .antMatchers("/home").permitAll()
          .antMatchers("/errorLogin").permitAll()
          .antMatchers("/searchEmployee").permitAll()
          .antMatchers("/h2-console/**").permitAll()
          .antMatchers("/addEmployee").hasAuthority("ADMIN")
          .anyRequest().authenticated()
          .and()
          .formLogin()
          .loginPage("/authentication")
          .defaultSuccessUrl("/home")
          .failureUrl("/errorLogin")
          .and()
          .logout().logoutSuccessUrl("/authentication");
        
        http.csrf().disable();
        http.headers().frameOptions().disable();
    }

  
}

```

###  Add login/logout/failure jsp's:

Here is an example for a simple login:

```
<form name='loginForm' action="/authentication" method='POST'>
      <table>
         <tr>
            <td>User:</td>
            <td><input type='text' name='username' value=''></td>
         </tr>
         <tr>
            <td>Password:</td>
            <td><input type='password' name='password' /></td>
         </tr>
         <tr>
            <td><button class="btn btn-default" type="submit" value="submit">Login</button></td>
         </tr>
      </table>
  </form>
```

TIPS: Spring security provides an useful html tag:

```
<%@ taglib prefix="sec" uri="http://www.springframework.org/security/tags"%>
```
