# What is PHP?
* open-source server-side scripting language 
* designed primarily for web development. 


# Dangerous Functions
### Dangerous PHP Functions

| Function                 | Description                                                                                        | Potential Risks                                                                                                                                                                         |
| ------------------------ | -------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `eval()`                 | Evaluates a string as PHP code                                                                     | Code injection                                                                                                                                                                          |
| `exec()`                 | Executes an external program                                                                       | Command injection                                                                                                                                                                       |
| `system()`               | Executes an external program and displays output                                                   | Command injection                                                                                                                                                                       |
| `shell_exec()`           | Executes an external program and returns output                                                    | Command injection                                                                                                                                                                       |
| `passthru()`             | Executes an external program and displays raw output                                               | Command injection                                                                                                                                                                       |
| `include()`              | Includes and evaluates a specified file                                                            | File inclusion (LFI, RFI)                                                                                                                                                               |
| `require()`              | Includes and evaluates a specified file                                                            | File inclusion (LFI, RFI)                                                                                                                                                               |
| `include_once()`         | Includes and evaluates a specified file once                                                       | File inclusion (LFI, RFI)                                                                                                                                                               |
| `require_once()`         | Includes and evaluates a specified file once                                                       | File inclusion (LFI, RFI)                                                                                                                                                               |
| `preg_replace()`         | Performs a regular expression search and replace                                                   | Code execution with `/e` modifier                                                                                                                                                       |
| `unserialize()`          | Converts a stored representation into a PHP value                                                  | Object injection                                                                                                                                                                        |
| `file_get_contents()`    | Reads entire file into a string                                                                    | File inclusion, Information disclosure                                                                                                                                                  |
| `fopen()`                | Opens a file or URL                                                                                | File inclusion, Information disclosure                                                                                                                                                  |
| `proc_open()`            | Opens a process file pointer                                                                       | Command injection                                                                                                                                                                       |
| `popen()`                | Opens a pipe to a process                                                                          | Command injection                                                                                                                                                                       |
| `create_function()`      | Creates an anonymous function                                                                      | Code injection                                                                                                                                                                          |
| `assert()`               | Evaluates a string as a PHP expression                                                             | Code injection                                                                                                                                                                          |
| `dl()`                   | Loads a PHP extension at runtime                                                                   | Potential for arbitrary code execution                                                                                                                                                  |
| `pcntl_exec()`           | Executes a program in the current process space                                                    | Command injection                                                                                                                                                                       |
| Backticks (`\` `\`)      | Executes a command via shell                                                                       | Command injection                                                                                                                                                                       |
| `call_user_func()`       | Calls a user-defined function                                                                      | Potential for code injection                                                                                                                                                            |
| `call_user_func_array()` | Calls a user-defined function with parameters                                                      | Potential for code injection                                                                                                                                                            |
| get_defined_functions()  | Gets an array of all defined functions.                                                            | Call functions without using its name `echo get_defined_functions()["internal"][4]("hello world");`                                                                                     |
|                          |                                                                                                    | ```<br>echo get_defined_functions()["internal"][550]("whoami");<br><br><br><br>$arr = get_defined_functions ()['internal'] ;array_search('exec', $arr, True) ; print_r ($test) ;<br>``` |
| `array_search`           | Searches the array for a given value and returns the first corresponding key if successful<br><br> | `echo array_search(urldecode("%65%78%65%63"), get_defined_functions()["internal"]);<br>`                                                                                                |
|                          |                                                                                                    |                                                                                                                                                                                         |

## Chain get_defined_functions() and array_search together.
`echo get_defined_functions()["internal"][array_search(urldecode("%65%78%65%63"),get_defined_functions()["internal"])]("whoami");`



# PHP class and extends

In PHP, the keyword class is used to define a new class, which is a blueprint for creating objects. Classes encapsulate data and methods that operate on that data.

class test: This defines a new class named test.

extends tester: This indicates that test is a subclass of tester, inheriting its properties and methods. This is a way to implement inheritance in PHP, allowing test to reuse and extend the functionality of tester.

# PHP Encoding options

### PHP Encoding and Decoding Options

| Encoding Type             | Encode Function             | Decode Function             | Description                                                  |
| ------------------------- | --------------------------- | --------------------------- | ------------------------------------------------------------ |
| **HTML Encoding**         | `htmlspecialchars()`        | `htmlspecialchars_decode()` | Converts special characters to/from HTML entities            |
|                           | `htmlentities()`            | `html_entity_decode()`      | Converts all applicable characters to/from HTML entities     |
| **URL Encoding**          | `urlencode()`               | `urldecode()`               | Encodes/decodes a string to/from a URL                       |
|                           | `rawurlencode()`            | `rawurldecode()`            | Encodes/decodes a string for use in a URL, preserving spaces |
| **Base64 Encoding**       | `base64_encode()`           | `base64_decode()`           | Encodes/decodes data with Base64                             |
| **JSON Encoding**         | `json_encode()`             | `json_decode()`             | Encodes/decodes a value to/from JSON format                  |
| **Quoted-Printable**      | `quoted_printable_encode()` | `quoted_printable_decode()` | Converts a string to/from quoted-printable encoding          |
| **URL-encoded Functions** | `http_build_query()`        | `parse_str()`               | Generates/parses a URL-encoded query string                  |
| **Gzip Encoding**         | `gzencode()`                | `gzdecode()`                | Encodes/decodes data with Gzip compression                   |
| **Rot13 Encoding**        | `str_rot13()`               | `str_rot13()`               | Encodes/decodes a string using the ROT13 algorithm           |
| **Hexadecimal Encoding**  | `bin2hex()`                 | `hex2bin()`                 | Encodes/decodes data to/from hexadecimal representation      |
| **UU Encoding**           | `convert_uuencode()`        | `convert_uudecode()`        | Encodes/decodes data with uuencode                           |


# What is Event Sink?

An event sink is a class or function designed to receive incoming events from another object or function
https://en.wikipedia.org/wiki/Sink_(computing)

![](https://i.imgur.com/9XffX6J.png)



https://softwareengineering.stackexchange.com/questions/363397/how-does-an-event-listener-work

## Guard Clause
https://en.wikipedia.org/wiki/Guard_(computer_science)

# PHP Web application Architecture

![](https://i.imgur.com/Inaqqe0.png)


![](https://i.imgur.com/VdTh3jH.png)



https://www.php.net/manual/en/mongodb.overview.php
![](https://i.imgur.com/a5eAAmr.png)




https://wiki.dolibarr.org/index.php?title=File:ArchitectureClientServeurDolibarr.png

---

# Syntax
# :: Double colons
https://www.php.net/manual/en/language.oop5.paamayim-nekudotayim.php
Scope Resolution Operator (::) 
a token that allows access to a constant, static property, or static method of a class or one of its parents. 

# \`(Backtick)
https://www.php.net/manual/en/language.operators.execution.php
Execution Operators 
backticks (\`). Note that these are not single-quotes! PHP will attempt to execute the contents of the backticks as a shell command; the output will be returned 


# . (period)
https://www.php.net/manual/en/language.operators.string.php
String Operators
 The first is the concatenation operator ('.'), which returns the concatenation of its right and left arguments. The second is the concatenating assignment operator ('.='), which appends the argument on the right side to the argument on the left side.

## PHP Eval().

https://www.php.net/manual/en/function.eval.php





```php
<?php
// Start a simple web server with: php -S localhost:8080 eval_example.php

// Check if the user provided an input
if (isset($_GET['expression'])) {
    $userInput = $_GET['expression'];
    
    // Dangerous usage of eval
    $result = eval("return $userInput;");
    
    echo "Result: " . $result;
} else {
    echo 'Please provide a mathematical expression using the "expression" query parameter.';
}
?>

```

Execute the file with `php -S localhost:9999 ex1.php`

```
curl 'http://localhost:9999/?expression=%20system(%27ls%27);'

```

https://book.hacktricks.xyz/network-services-pentesting/pentesting-web/php-tricks-esp



# Bypass PHP Filtering
1. Reflection
Reflection is a feature in some programming languages that allows a program to inspect and modify its structure and behavior at runtime. 

```php
class Example {
    public $property = 'value';

    public function method() {
        return 'Hello, World!';
    }
}

$reflector = new ReflectionClass('Example');
$instance = $reflector->newInstance();
echo $reflector->getProperty('property')->getValue($instance); // Output: value
echo $reflector->getMethod('method')->invoke($instance); // Output: Hello, World!

```

https://en.wikipedia.org/wiki/Reflective_programming

https://www.php.net/manual/en/class.reflectionfunction.php

2. Different Encoding

PHP Encoding and Decoding Options

| Encoding Type             | Encode Function             | Decode Function             | Description                                                  |
| ------------------------- | --------------------------- | --------------------------- | ------------------------------------------------------------ |
| **HTML Encoding**         | `htmlspecialchars()`        | `htmlspecialchars_decode()` | Converts special characters to/from HTML entities            |
|                           | `htmlentities()`            | `html_entity_decode()`      | Converts all applicable characters to/from HTML entities     |
| **URL Encoding**          | `urlencode()`               | `urldecode()`               | Encodes/decodes a string to/from a URL                       |
|                           | `rawurlencode()`            | `rawurldecode()`            | Encodes/decodes a string for use in a URL, preserving spaces |
| **Base64 Encoding**       | `base64_encode()`           | `base64_decode()`           | Encodes/decodes data with Base64                             |
| **JSON Encoding**         | `json_encode()`             | `json_decode()`             | Encodes/decodes a value to/from JSON format                  |
| **Quoted-Printable**      | `quoted_printable_encode()` | `quoted_printable_decode()` | Converts a string to/from quoted-printable encoding          |
| **URL-encoded Functions** | `http_build_query()`        | `parse_str()`               | Generates/parses a URL-encoded query string                  |
| **Gzip Encoding**         | `gzencode()`                | `gzdecode()`                | Encodes/decodes data with Gzip compression                   |
| **Rot13 Encoding**        | `str_rot13()`               | `str_rot13()`               | Encodes/decodes a string using the ROT13 algorithm           |
| **Hexadecimal Encoding**  | `bin2hex()`                 | `hex2bin()`                 | Encodes/decodes data to/from hexadecimal representation      |
| **UU Encoding**           | `convert_uuencode()`        | `convert_uudecode()`        | Encodes/decodes data with uuencode                           |

3. Alternate String Modification


| Function           | Description                                              | Example                                                     |
| ------------------ | -------------------------------------------------------- | ----------------------------------------------------------- |
| `str_replace()`    | Replaces all occurrences of a substring with another     | `str_replace("world", "PHP", "Hello world")` → `Hello PHP`  |
| `str_ireplace()`   | Case-insensitive version of `str_replace()`              | `str_ireplace("WORLD", "PHP", "Hello world")` → `Hello PHP` |
| `substr_replace()` | Replaces a part of a string with another                 | `substr_replace("Hello world", "PHP", 6, 5)` → `Hello PHP`  |
| `strtr()`          | Translates certain characters or substrings              | `strtr("Hello world", "oe", "ea")` → `Halla warld`          |
| `substr()`         | Returns a part of a string                               | `substr("Hello world", 6, 5)` → `world`                     |
| `trim()`           | Strips whitespace or other characters from the ends      | `trim("  Hello world  ")` → `Hello world`                   |
| `rtrim()`          | Strips whitespace or other characters from the right end | `rtrim("  Hello world  ")` → `  Hello world`                |
| `ltrim()`          | Strips whitespace or other characters from the left end  | `ltrim("  Hello world  ")` → `Hello world  `                |
| `str_pad()`        | Pads a string to a certain length with another string    | `str_pad("Hello", 10, ".")` → `Hello.....`                  |
| `strtoupper()`     | Converts a string to uppercase                           | `strtoupper("Hello world")` → `HELLO WORLD`                 |
| `strtolower()`     | Converts a string to lowercase                           | `strtolower("Hello World")` → `hello world`                 |
| `ucfirst()`        | Capitalizes the first character of a string              | `ucfirst("hello world")` → `Hello world`                    |
| `ucwords()`        | Capitalizes the first character of each word in a string | `ucwords("hello world")` → `Hello World`                    |
| `strrev()`         | Reverses a string                                        | `strrev("Hello world")` → `dlrow olleH`                     |
| `addslashes()`     | Adds backslashes before certain characters               | `addslashes("Hello 'world'")` → `Hello \'world\'`           |
| `str_split()`      | Splits a string into an array                            | `str_split("Hello")` → `["H", "e", "l", "l", "o"]`          |
| `implode()`        | Joins array elements into a string                       | `implode("-", ["Hello", "world"])` → `Hello-world`          |
| `explode()`        | Splits a string by a delimiter into an array             | `explode(" ", "Hello world")` → `["Hello", "world"]`        |
| `strip_tags()`     | Strips HTML and PHP tags from a string                   | `strip_tags("ex<a>ec")` → `exec`                            |

### Examples

```php
// str_replace example
echo str_replace("world", "PHP", "Hello world"); // Output: Hello PHP

// str_ireplace example
echo str_ireplace("WORLD", "PHP", "Hello world"); // Output: Hello PHP

// substr_replace example
echo substr_replace("Hello world", "PHP", 6, 5); // Output: Hello PHP

// strtr example
echo strtr("Hello world", "oe", "ea"); // Output: Halla warld

// substr example
echo substr("Hello world", 6, 5); // Output: world

// trim example
echo trim("  Hello world  "); // Output: Hello world

// rtrim example
echo rtrim("  Hello world  "); // Output:   Hello world

// ltrim example
echo ltrim("  Hello world  "); // Output: Hello world  

// str_pad example
echo str_pad("Hello", 10, "."); // Output: Hello.....

// strtoupper example
echo strtoupper("Hello world"); // Output: HELLO WORLD

// strtolower example
echo strtolower("Hello World"); // Output: hello world

// ucfirst example
echo ucfirst("hello world"); // Output: Hello world

// ucwords example
echo ucwords("hello world"); // Output: Hello World

// strrev example
echo strrev("Hello world"); // Output: dlrow olleH

// addslashes example
echo addslashes("Hello 'world'"); // Output: Hello \'world\'

// str_split example
print_r(str_split("Hello")); // Output: Array ( [0] => H [1] => e [2] => l [3] => l [4] => o )

// implode example
echo implode("-", ["Hello", "world"]); // Output: Hello-world

// explode example
print_r(explode(" ", "Hello world")); // Output: Array ( [0] => Hello [1] => world )

// strip_tags example
echo strip_tags("<p>Hello <b>world</b></p>"); // Output: Hello world
