---
{"dg-publish":true,"permalink":"/1-hack-like-a-script-kiddie/web/regex/regex-syntax/","noteIcon":"","created":"2025-04-15T14:11:19.608-04:00"}
---

















https://regex101.com/

```bash
 grep -oP "/v$i/\S+"
  -P enables Perl-compatible regex. 
  -o only prints the matched parts. 

grep -rihEo '/v[0-9]+/[^ ]+' ./folder


-r: Recursively search through directories starting from the specified path.
-i: Ignore case differences (not strictly necessary here unless some paths are oddly cased).
-h: Suppress the prefixing of filenames on output. This is useful when you only want to see the matching lines.
-o: Output only the matching parts of the lines, not the entire lines.
-E: Interpret the pattern as an extended regular expression (ERE).


/v[0-9]+/: This matches any sequence starting with /v followed by one or more digits, and ending with a /. The [0-9]+ ensures that at least one digit is present.

[^ ]+: This matches one or more characters that are not spaces. It assumes that your API endpoints do not contain spaces. Adjust this part of the pattern if your endpoint structure includes other non-space delimiters or terminators.
	[] : Anything placed within these brackets is what the regular expression will look for.
	^ : When the caret symbol is inside of bracket, e.g. [^ ], it acts as negation. e.g. [^ ]+Everything except space. 
```

| **Syntax** | **Description**                                          | **Example** | **Matches**                                            |
| ---------- | -------------------------------------------------------- | ----------- | ------------------------------------------------------ |
| `.`        | Any character except newline                             | `a.b`       | `aab`, `acb`, `a1b`                                    |
| `^`        | Start of a string                                        | `^Hello`    | `Hello world` (matches `Hello` at the start)           |
| `$`        | End of a string                                          | `world$`    | `Hello world` (matches `world` at the end)             |
| `*`        | 0 or more of the preceding element                       | `a*`        | ``, `a`, `aaa`                                         |
| `+`        | 1 or more of the preceding element                       | `a+`        | `a`, `aaa`                                             |
| `?`        | 0 or 1 of the preceding element                          | `a?`        | ``, `a`                                                |
| `{n}`      | Exactly `n` occurrences of the preceding element         | `a{3}`      | `aaa`                                                  |
| `{n,}`     | At least `n` occurrences of the preceding element        | `a{2,}`     | `aa`, `aaa`                                            |
| `{n,m}`    | Between `n` and `m` occurrences of the preceding element | `a{2,3}`    | `aa`, `aaa`                                            |
| `?`        | 0 or 1 of the preceding element                          | `a?`        | ``, `a`                                                |
| `[abc]`    | Any one of the characters in the set                     | `[abc]`     | `a`, `b`, `c`                                          |
| `[^abc]`   | Any character not in the set                             | `[^abc]`    | `d`, `e`, `1`                                          |
| `[a-z]`    | Any character in the range                               | `[a-z]`     | `a`, `m`, `z`                                          |
| \|         | Alternation (OR)                                         | a\|b        | `a`, `b`                                               |
| `()`       | Grouping                                                 | `(abc)`     | `abc`                                                  |
| `\d`       | Any digit                                                | `\d`        | `0`, `9`, `5`                                          |
| `\D`       | Any non-digit                                            | `\D`        | `a`, `z`, `!`                                          |
| `\w`       | Any word character (alphanumeric + underscore)           | `\w`        | `a`, `1`, `_`                                          |
| `\W`       | Any non-word character                                   | `\W`        | `!`, `@`, ` `                                          |
| `\s`       | Any whitespace character                                 | `\s`        | ` `, `\t`, `\n`                                        |
| `\S`       | Any non-whitespace character                             | `\S`        | `a`, `1`, `!`                                          |
| `\b`       | Word boundary                                            | `\bword\b`  | Matches `word` in `word boundary` but not in `wording` |
| `\B`       | Non-word boundary                                        | `\Bword\B`  | Matches `word` in `swordsmith`                         |
| ?!         | negative lookahead                                       | (?!1\|2)    | Either 1 or 2                                          |
|            |                                                          |             |                                                        |



https://www3.ntu.edu.sg/home/ehchua/programming/howto/Regexe.html


https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Regular_expressions/Cheatsheet

https://www.geeksforgeeks.org/write-regular-expressions/

https://support.google.com/a/answer/1371417?hl=en