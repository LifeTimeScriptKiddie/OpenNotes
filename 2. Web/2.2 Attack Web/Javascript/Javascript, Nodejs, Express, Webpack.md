---
{"dg-publish":true,"permalink":"/1-hack-like-a-script-kiddie/web/javascript/javascript-nodejs-express-webpack/","noteIcon":"","created":"2025-04-15T14:11:19.605-04:00"}
---



















Javascript dangerous functions.

| Function             | Description                                                                                      | Potential Risks                                 |
| -------------------- | ------------------------------------------------------------------------------------------------ | ----------------------------------------------- |
| `eval()`             | Evaluates JavaScript code represented as a string                                                | Code injection, arbitrary code execution        |
| `setTimeout()`       | Executes a function or evaluates an expression after a specified number of milliseconds          | Code injection (if used with string arguments)  |
| `setInterval()`      | Repeatedly calls a function or evaluates an expression with a fixed time delay between each call | Code injection (if used with string arguments)  |
| `Function()`         | Creates a new Function object from a string of code                                              | Code injection, arbitrary code execution        |
| `document.write()`   | Writes a string of text to a document stream                                                     | Cross-site scripting (XSS), code injection      |
| `innerHTML`          | Sets or returns the HTML content of an element                                                   | Cross-site scripting (XSS)                      |
| `outerHTML`          | Sets or returns the HTML content including the element itself                                    | Cross-site scripting (XSS)                      |
| `location.href`      | Gets/sets the URL of the current window                                                          | Open redirect, phishing                         |
| `location.replace()` | Replaces the current document with a new one                                                     | Open redirect, phishing                         |
| `localStorage`       | Provides access to a web storage object                                                          | Data theft, insecure storage                    |
| `sessionStorage`     | Provides access to a web storage object                                                          | Data theft, insecure storage                    |
| `XMLHttpRequest`     | Interacts with servers                                                                           | Cross-site scripting (XSS), information leakage |
| `fetch()`            | Fetches resources across the network                                                             | Cross-site scripting (XSS), information leakage |


Critical files for nodeJS
```
bin/www
package.json
routes/
```

General folder architecture.
https://dev.to/shadid12/how-to-architect-a-node-js-project-from-ground-up-1n22

https://itnext.io/boost-nodejs-scalability-with-multi-processing-architecture-6d7bd03c892c



../app will look for app.js or app/index.js
debug, http are built-in module.
guacamole-lite is a third party module, should installed in `node_modules`







# Package.json
Under package.json, search for dependencies.
## Dependency - Webpack 


Module bundler for JS application used in Node.js projects. 
Webpack is most often
used to bundle external client side packages (like jQuery, Bootstrap, etc) and custom JavaScript
code into a single file to be served by a web server. This means that the frontend directory will
most likely contain all the frontend assets, including the code that started the WebSocket
connection. 

## Dependency - Express
Express is a web application framework. 
routes/ directory will contain the definitions to the endpoints. 





https://desosa2022.netlify.app/projects/expressjs/posts/essay_2/#fnref:1




Resources:
https://www.mohanarjun.com/routing_in_express_js_a_beginners_guide/



# Node.js global variable
https://www.knowledgehut.com/blog/web-development/node-js-global-variables

