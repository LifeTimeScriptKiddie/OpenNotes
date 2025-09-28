---
{"dg-publish":true,"permalink":"/1-hack-like-a-script-kiddie/web/java/java-extenions/","noteIcon":"","created":"2025-04-15T14:11:19.605-04:00"}
---


















| File Type | Full Name                      | Primary Use                           | Contents                                                                                                                                                                        | Typical Extension |
| --------- | ------------------------------ | ------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------- |
| JAR       | Java Archive                   | Stand-alone applications or libraries | - Java class files<br>- Associated metadata<br>- Resources (text, images)                                                                                                       | .jar              |
| WAR       | Web Application Archive        | Web applications                      | - Servlets<br>- JSP files<br>- Java class files<br>- Static web pages (HTML, CSS, JS)<br>- Web resources<br>- Web deployment descriptor (web.xml)                               | .war              |
| EAR       | Enterprise Application Archive | Enterprise applications               | - Multiple JAR files<br>- Multiple WAR files<br>- Enterprise JavaBeans<br>- Application clients<br>- Resource adapters<br>- Application deployment descriptor (application.xml) | .ear              |

Additional Notes:
- JAR files can be executed directly if they contain a main class.
- WAR files are deployed to Java EE-compliant web servers like Tomcat or Jetty.
- EAR files are deployed to full Java EE application servers like WildFly or WebSphere.
- All these archive types are essentially ZIP files with a specific structure and can be examined using standard ZIP tools.