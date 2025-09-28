# Java Servlets and Key Methods to Review

1. HttpServlet
   - `doGet(HttpServletRequest req, HttpServletResponse resp)`
   - `doPost(HttpServletRequest req, HttpServletResponse resp)`
   - `doPut(HttpServletRequest req, HttpServletResponse resp)`
   - `doDelete(HttpServletRequest req, HttpServletResponse resp)`
   - `doCopy`
   - `doOptions`
   - `service(HttpServletRequest req, HttpServletResponse resp)`
   - `init(ServletConfig config)`
   - `destroy()`

2. Filter
   - `doFilter(ServletRequest request, ServletResponse response, FilterChain chain)`
   - `init(FilterConfig filterConfig)`
   - `destroy()`

3. ServletContextListener
   - `contextInitialized(ServletContextEvent sce)`
   - `contextDestroyed(ServletContextEvent sce)`

4. HttpSessionListener
   - `sessionCreated(HttpSessionEvent se)`
   - `sessionDestroyed(HttpSessionEvent se)`

5. HttpServletRequest
   - `getParameter(String name)`
   - `getParameterValues(String name)`
   - `getHeader(String name)`
   - `getCookies()`
   - `getSession()`
   - `getAttribute(String name)`
   - `getRequestURI()`

6. HttpServletResponse
   - `setContentType(String type)`
   - `setHeader(String name, String value)`
   - `addCookie(Cookie cookie)`
   - `sendRedirect(String location)`
   - `getWriter()`
   - `getOutputStream()`

7. HttpSession
   - `setAttribute(String name, Object value)`
   - `getAttribute(String name)`
   - `removeAttribute(String name)`
   - `invalidate()`
   - `setMaxInactiveInterval(int interval)`

8. ServletContext
   - `getAttribute(String name)`
   - `setAttribute(String name, Object object)`
   - `getInitParameter(String name)`
   - `getRealPath(String path)`

9. Custom Authentication Servlets
   - `login(String username, String password)`
   - `logout()`
   - `isUserInRole(String role)`

10. File Upload Handling
    - `getPart(String name)` (in HttpServletRequest)
    - `write(String fileName)` (in Part interface)

11. WebSocket
    - `@OnOpen`
    - `@OnMessage`
    - `@OnClose`
    - `@OnError`

12. Spring Framework Controllers
    - Methods annotated with `@RequestMapping`, `@GetMapping`, `@PostMapping`, etc.
    - `@InitBinder` methods
    - `@ModelAttribute` methods
    - 