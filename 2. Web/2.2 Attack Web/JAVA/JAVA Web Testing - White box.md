# Investigating Java Web Application  

## 1. Application Structure

- Locate the application's root directory
- Look for WAR (Web Application Archive) files
- Examine the `META-INF` folder for external library--> application.xml
- Examine the `WEB-INF` folder structure
	- Examine web.xml --> Maps URL and servlet. 
	- Servlet --> 
	- !../Attachments/Pasted image 20240703151954.png
	- https://en.wikipedia.org/wiki/Jakarta_Servlet

## 2. Configuration Files

- `web.xml`: Main configuration file
- `context.xml`: Context configuration
- `server.xml`: Server configuration (if using Tomcat)
- `.properties` files: Application-specific settings
- application.yml or application.yaml: Common in Spring Boot applications
- log4j.properties or logback.xml: Logging configurations

## 3. Source Code

- `.java` files: Java source code
- `.jsp` files: JavaServer Pages
- `.class` files: Compiled Java bytecode
-  `.jar` files: Look for files that is native to web application. 
	- `AdventNetAppManagerWebClient.jar` 
	-  Use JD-GUI to export in zip format. 
	-  Unzip and open the folder from Notepad ++
- 

## 4. Libraries

- `WEB-INF/lib` directory: Third-party JAR files
	- Look for what is being imported. 
	- 
- ![](https://i.imgur.com/F2IE5Ji.png)

-  Examine dependencies for known vulnerabilities
- Check for outdated libraries and update them


## 5. Database

- Look for database connection strings in configuration files
- Check for hardcoded credentials
- Examine ORM configurations (e.g., Hibernate, JPA)
- Review database queries for SQL injection vulnerabilities

## 6. Logging

- Locate log files (often in `logs` directory)
- Examine for sensitive information leakage

## 7. Security Mechanisms

- Investigate authentication methods
- Look for encryption/decryption implementations
- Check for input validation and sanitization

## 8. Static Resources

- Examine JavaScript files for client-side vulnerabilities
- Check CSS files for information leakage

## 9. Hidden Directories

- Look for backup files or hidden directories
- Check for version control files (e.g., `.git`)

## 10. Server Configuration

- Investigate web server configuration files
- Check for misconfigurations in server settings

## 11. API Endpoints

- Identify and test API endpoints
- Look for documentation files (e.g., Swagger)

## 12. Error Handling

- Examine custom error pages
- Look for stack traces or verbose error messages


## 13. Build and Deployment

- Review build scripts:
  - `build.xml` (Ant)
  - `pom.xml` (Maven)
  - `build.gradle` (Gradle)
- Check for security configurations in CI/CD pipelines
- Examine deployment configurations for sensitive data
- Look for environment-specific configuration files

## 14. External Integrations

- Review integrations with external services
- Check the security of API keys and tokens
- Ensure secure communication with external services (e.g., HTTPS)
- Verify proper error handling for external service failures
- Look for hardcoded endpoint URLs

## 15. Session Management

- Verify secure session handling:
  - Session timeouts
  - Secure cookies (HttpOnly, Secure flags)
  - Session ID generation
- Check for session fixation vulnerabilities
- Test for session hijacking possibilities
- Examine how session data is stored and protected

## 16. Configuration Management

- Ensure sensitive configuration is not hardcoded
- Use environment variables for sensitive data
- Verify configurations for different environments:
  - Development
  - Testing
  - Staging
  - Production
- Check for proper separation of configuration data
- Look for configuration versioning and change management


----

# Java Web Application Source Code Review Checklist

## 1. Security Vulnerabilities

- Input validation and sanitization
  - Look for `request.getParameter()`, `request.getHeader()`, etc.
- SQL Injection prevention
  - Check for use of prepared statements or ORM frameworks
- Cross-Site Scripting (XSS) prevention
  - Look for output encoding functions
- Cross-Site Request Forgery (CSRF) protection
  - Check for CSRF tokens in forms
- Authentication and authorization mechanisms
  - Review `login()`, `authenticate()`, `isAuthorized()` methods
- Session management
  - Look for `HttpSession` usage and handling

## 2. Sensitive Data Handling

- Encryption/decryption methods
  - Check for proper use of cryptographic functions
- Hardcoded credentials or secrets
  - Search for strings that look like passwords or API keys
- Logging practices
  - Ensure sensitive data isn't being logged

## 3. Error Handling and Logging

- Exception handling
  - Look for `try-catch` blocks and how exceptions are managed
- Custom error pages
  - Check for `error-page` entries in `web.xml`
- Logging practices
  - Review usage of logging frameworks (e.g., Log4j, SLF4J)

## 4. Performance and Resource Management

- Connection pooling
  - Check database connection handling
- Resource cleanup
  - Look for proper closing of resources (e.g., `close()` methods)
- Caching mechanisms
  - Review any implemented caching logic

## 5. Code Structure and Design

- Separation of concerns
  - Look for MVC pattern implementation
- Use of design patterns
  - Identify common patterns like Singleton, Factory, etc.
- Code duplication
  - Check for repeated code that could be refactored

## 6. Third-party Libraries

- Review imported libraries
  - Check `import` statements and `pom.xml` or `build.gradle`
- Look for known vulnerabilities in used versions

## 7. API Endpoints

- RESTful API implementations
  - Look for `@RestController`, `@GetMapping`, `@PostMapping`, etc.
- API security measures
  - Check for authentication/authorization on endpoints

## 8. Concurrency Handling

- Thread safety
  - Look for `synchronized` keyword, `volatile` variables
- Race conditions
  - Check shared resource access

## 9. Configuration Management

- Externalized configurations
  - Look for property files and how they're loaded
- Environment-specific settings
  - Check for different configs for dev/test/prod

## 10. Business Logic

- Core business logic implementation
  - Review key algorithms and processes
- Business rule validation
  - Check for proper validation of business rules
