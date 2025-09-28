---
{"dg-publish":true,"permalink":"/1-hack-like-a-script-kiddie/web/javascript/node-js-handlebars/","noteIcon":"","created":"2025-04-15T14:11:19.605-04:00"}
---




















## Handlebars and Templating

```javascript
<ul>

  {{#each items}}  //{{#each items}} begins a loop over the items array.
	  <li>{{this}}</li>  //{{this}} refers to the current item in the iteration.
  {{/each}} 
  
</ul>

//{{/each}} ends the loop.



```
Handlebars uses double curly braces {{ }} for its expressions and helpers. For instance, {{each}} is used to iterate over arrays.

| Feature         | Handlebars Syntax                                           | EJS Syntax                                                                  |
| --------------- | ----------------------------------------------------------- | --------------------------------------------------------------------------- |
| Looping Syntax  | `{{#each users}} <p>{{this}}</p> {{/each}}`                 | `<% users.forEach(function(user){ %> <p><%= user %></p> <% }); %>`          |
| Template Engine | Handlebars                                                  | EJS                                                                         |
| Looping Method  | `each` helper                                               | JavaScript's `forEach` method                                               |
| Example Usage   | ```handlebars {{#each users}} <p>{{this}}</p> {{/each}} ``` | ```ejs <% users.forEach(function(user){ %> <p><%= user %></p> <% }); %> ``` |

Folder location:
node_modules/handlebars/dist/cjs
![](../OSWE_round1/11.%20Chips%20Prototype%20Pollution%20-%20JS,%20Nodejs/Reference%20-%20nodeJS/Images/Pasted%20image%2020240621231708.png)

```
my-project/
├── node_modules/
│   └── handlebars/
│       ├── dist/
│       │   ├── cjs/
│       │   ├── amd/
│       │   ├── esm/
│       │   └── ...
│       └── ...
├── public/
│   ├── css/
│   ├── js/
│   └── images/
├── views/
│   ├── layouts/
│   │   └── main.handlebars
│   ├── partials/
│   │   ├── header.handlebars
│   │   └── footer.handlebars
│   └── home.handlebars
├── routes/
│   └── index.js
├── config/
│   └── config.js
├── app.js
├── package.json
└── README.md

```
The node_modules/handlebars/dist/cjs folder is part of the Handlebars package installed via npm or yarn. This directory contains the CommonJS (CJS) distribution files of Handlebars, which are used in Node.js environments. These files are precompiled and ready for use, ensuring compatibility and performance in server-side applications


```javascript

### Key Files and Directories

- **base.js**: Contains the base configuration and initialization code for Handlebars.
- **compiler**:
  - `compiler.js`: Handles the compilation of Handlebars templates.
- **decorators**:
  - `decorators.js`: Manages decorators which are functions that can modify the behavior of Handlebars templates.
- **exception.js**: Handles exceptions and error reporting in Handlebars.
- **helpers**:
  - `helpers.js`: Contains the implementation of Handlebars helpers, which provide additional functionality in templates.
- **internal**:
  - `logger.js`: Handles logging within Handlebars.
  - `no-conflict.js`: Provides a no-conflict mode for Handlebars, restoring the original Handlebars global variable.
  - `runtime.js`: Contains the runtime-only functions of Handlebars, used when templates are precompiled.
  - `safe-string.js`: Ensures safe handling of strings to prevent XSS attacks.
  - `utils.js`: Contains utility functions used throughout Handlebars.
- **handlebars.js**: The main entry point for Handlebars, including both compilation and runtime functionalities.
- **handlebars.runtime.js**: The runtime-only version of Handlebars, used when templates are precompiled.
- **precompiler.js**: Handles precompilation of Handlebars templates.

```

---

## How does it work?
`Handlerbars Template` needs to be compiled by `Handlerbars compiler`. 

The process is User input --> (parse to AST) -->  Abstract Syntax Tree --> (precompile) --> Array of Opcode -->  (compile) -->Javascript



```javascript
Handlebars = require("handlebars")

ast = Handlebars.parse("hello {{ foo }}")

precompiled = Handlebars.precompile(ast)

eval("compiled = " + precompiled)

hello = Handlebars.template(compiled)
// executing a string of JavaScript code that assigns the value of the variable precompiled to the variable compiled.

hello({"foo": "student"})

```
Other way!
```javascript
//use Handlebars
const Handlebars = require("handlebars");

// Parse the template to ast format.
const ast = Handlebars.parse("hello {{ foo }}");

// Precompile the AST
const precompiled = Handlebars.precompile(ast);

// Create a new function from the precompiled template
const compiledFunction = new Function("return " + precompiled)();

// Generate the template function
const hello = Handlebars.template(compiledFunction);

// Use the template
const result = hello({ foo: "world" });
console.log(result); // Output: hello world

```

 Handlebars will create an AST, create the opcodes, and convert the opcodes to JavaScript code

![](../OSWE_round1/11.%20Chips%20Prototype%20Pollution%20-%20JS,%20Nodejs/Reference%20-%20nodeJS/Images/Pasted%20image%2020240621231956.png)
![](../OSWE_round1/11.%20Chips%20Prototype%20Pollution%20-%20JS,%20Nodejs/Reference%20-%20nodeJS/Images/Pasted%20image%2020240621232014.png)https://studysection.com/blog/javascript-handlebars/
![](../OSWE_round1/11.%20Chips%20Prototype%20Pollution%20-%20JS,%20Nodejs/Reference%20-%20nodeJS/Images/Pasted%20image%2020240621232033.png)


![](../OSWE_round1/11.%20Chips%20Prototype%20Pollution%20-%20JS,%20Nodejs/Reference%20-%20nodeJS/Images/Pasted%20image%2020240623140145.png)

ast.js = Abstract Syntax Tree
An abstract syntax tree (AST) is a data structure used in computer science to represent the structure of a program or code snippet

The syntax is "abstract"  the structural or content-related details.
https://en.wikipedia.org/wiki/Abstract_syntax_tree
![](../OSWE_round1/11.%20Chips%20Prototype%20Pollution%20-%20JS,%20Nodejs/Reference%20-%20nodeJS/Images/Pasted%20image%2020240623141344.png)
https://www.codecademy.com/resources/docs/general/developer-tools/abstract-syntax-tree

