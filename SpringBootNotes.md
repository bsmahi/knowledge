# Spring Boot Framework
Spring Boot provides a web tool called **[Spring Initializer](http://start.spring.io)** to bootstrap an application quickly. 

@SpringBootApplication which is a combination of the following more specific spring annotations

#### @SpringBootApplication = @Configuration + @EnableAutoConfiguration + @ComponentScan
```java
package com.bsmlabs.lenskart;

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;

@SpringBootApplication
public class LenskartApplication {

	public static void main(String[] args) {
		SpringApplication.run(LenskartApplication.class, args);
	}
}
```

``@Configuration`` : Any class annotated with ``@Configuration`` annotation is bootstrapped by Spring and is also considered as a source of other bean definitions.

``@EnableAutoConfiguration`` : This annotation tells Spring to automatically configure your application based on the dependencies that you have added in the ``pom.xml`` file. **For example**, If ``spring-data-jpa`` or ``spring-jdbc`` is in classpath, then it automatically tries to configure a ``DataSource`` by reading the database properties from ``application.properties`` file.

``@ComponentScan`` : It tells Spring to scan and bootstrap other components defined in the current package (for example: com.bsmlabs.lenskart) and all the sub-packages.

The ``main()`` method calls Spring Boot's ``SpringApplication.run()`` method to launch the application.
