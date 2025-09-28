---
{"dg-publish":true,"permalink":"/1-hack-like-a-script-kiddie/web/php/php-vuln-py/","noteIcon":"","created":"2025-04-15T14:11:19.607-04:00"}
---
















```python
import os
import re
from colorama import init, Fore, Style

# Init colorama
init(autoreset=True)

vulnerable_functions = [
    "eval(", "exec(", "system(", "shell_exec(", "passthru(", "include(", "require(",
    "include_once(", "require_once(", "preg_replace(", "unserialize(",
    "file_get_contents(", "fopen(", "proc_open(", "popen(", "create_function(",
    "assert(", "dl(", "pcntl_exec(", "`", "call_user_func(",
    "call_user_func_array(", "get_defined_functions(", "array_search("
]


def search_vulnerable_functions(directory, functions_to_search):
    matches= []
    for root, _, files in os.walk(directory):
        for file in files:
            if file.endswith(".php"):
                file_path = os.path.join(root,file)
                with open(file_path, 'r', errors ='ignore') as f:
                    lines=f.readlines()
                    for i, line in enumerate(lines):
                        for func in functions_to_search:
                            if re.search(r'\b' + re.escape(func), line):
                                matches.append((file_path, i + 1, func, line.strip()))
    return matches


def print_matches(matches):
    for match in matches:
        file_path, line_number, func, line = match
        print (f"{Fore.GREEN}File: {file_path}, {Fore.CYAN}Line: {line_number}{Style.RESET_ALL}, Function: {Fore.RED}{func}{Style.RESET_ALL}, Code: {line}")



def main():
    print("Select the vulnerable functions to search for:")
    for i, func in enumerate(vulnerable_functions):
        print(f"{i+1}. {func}")

    choices = input("Enter the numbers of the functions to search for (comma-separated): ")
    selected_functions = [vulnerable_functions[int(choice) -1] for choice in choices.split(",")]

    custom_function = input("Enter a custom function to search for (or press Enter to skip): ")
    if custom_function:
        selected_functions.append(custom_function + "(")

    directory =input ("Enter the directory to search in: ")
    matches = search_vulnerable_functions(directory, selected_functions)

    if matches:
        print_matches(matches)

    else:
        print("No vulnerable functions found.")


if __name__ == "__main__":
    main()

```