# What is JAVA?


https://dev.java/learn/
https://www.java.com/en/download/help/whatis_java.html
https://aws.amazon.com/what-is/java/

---

# JAVA Web Application






```mermaid
---
config:
  theme: base
  themeVariables:
    nodeTextColor: "#FFFFFF"
    primaryColor: "#000000"
    lineColor: "#FFFFFF"
    edgeLabelBackground: "#000000"
  gitGraph:
    showBranches: false
---


graph TD
    A[Client Browser] -->|HTTP/HTTPS| B[Load Balancer]
    B --> C[Web Server]
    C --> D[Java Web Container]
    D --> E[Java Web Application]
    E --> F[Business Logic Layer]
    F --> G[Data Access Layer]
    G --> H[(Database)]
    E --> I[External Services API]
    J[Caching Layer] --> E
    K[Authentication Service] --> E
classDef default fill:#000000,stroke:#FFFFFF,color:#FFFFFF;

```

	Client Browser: Where users interact with the application
	Load Balancer: Distributes incoming traffic across multiple web servers
	Web Server: Handles HTTP requests (e.g., Apache, Nginx)
	Java Web Container: Runs Java web applications (e.g., Tomcat, Jetty)
	Java Web Application: The actual application code
	Business Logic Layer: Contains core application logic
	Data Access Layer: Manages database interactions
	Database: Stores application data
	External Services API: Integrations with third-party services
	Caching Layer: Improves performance by caching frequently accessed data
	Authentication Service: Manages user authentication and authorization
---

# What is Servlet?

https://javatrainingschool.com/servlet-life-cycle/
