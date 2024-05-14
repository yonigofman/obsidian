
### Bash Scripting Cheat Sheet

|Command|Description|Example|
|---|---|---|
|`#!/bin/bash`|Shebang line indicating Bash interpreter|`#!/bin/bash`|
|`echo`|Prints text to the terminal|`echo "Hello, World!"`|
|Variables|Store and manipulate data|`name="John"`|
|`if` statement|Conditional execution|`if [ condition ]; then` <br> `statement` <br> `fi`|
|`for` loop|Iterate over a list of items|`for item in list; do` <br> `statement` <br> `done`|
|`while` loop|Execute statements while a condition is true|`while [ condition ]; do` <br> `statement` <br> `done`|
|`case` statement|Execute different actions based on a variable|`case $variable in` <br> `pattern1) statement;;` <br> `pattern2) statement;;` <br> `*) default statement;;` <br> `esac`|
|Functions|Define reusable code blocks|`my_function() {` <br> `statement` <br> `}`|

### Bash Scripting Best Practices

1. **Use descriptive variable names**: Make your code readable.
2. **Indentation**: Maintain consistent indentation for better readability.
3. **Error handling**: Check for errors and handle them gracefully.
4. **Comments**: Document your code to explain its purpose.
5. **Testing**: Test your scripts thoroughly before deploying them.

### Common Bash Commands

|Command|Description|
|---|---|
|`cd`|Change directory|
|`ls`|List directory contents|
|`cp`|Copy files or directories|
|`mv`|Move or rename files or directories|
|`rm`|Remove files or directories|
|`chmod`|Change file permissions|
|`grep`|Search for patterns in files|
|`awk`|Text processing tool|
|`sed`|Stream editor|

### File and Directory Operations

|Command|Description|Example|
|---|---|---|
|`touch`|Create an empty file|`touch file.txt`|
|`mkdir`|Create a new directory|`mkdir folder`|
|`rm -r`|Remove directory and its contents recursively|`rm -r folder`|
|`cp -r`|Copy directory and its contents recursively|`cp -r source_folder dest_folder`|
|`mv`|Move or rename files or directories|`mv file.txt new_location/`|

### Conditional Statements
  
#### If Statements for Strings

|Operator|Description|Example|
|---|---|---|
|`=`|Equal to|`if [ "$string1" = "$string2" ]; then`|
|`!=`|Not equal to|`if [ "$string1" != "$string2" ]; then`|
|`-z`|Empty string|`if [ -z "$string" ]; then`|
|`-n`|Non-empty string|`if [ -n "$string" ]; then`|
|`<`|Less than (in ASCII alphabetical order)|`if [ "$string1" \< "$string2" ]; then`|
|`>`|Greater than (in ASCII alphabetical order)|`if [ "$string1" \> "$string2" ]; then`|

#### If Statements for Numeric Values

|Operator|Description|Example|
|---|---|---|
|`-eq`|Equal to|`if [ "$x" -eq "$y" ]; then`|
|`-ne`|Not equal to|`if [ "$x" -ne "$y" ]; then`|
|`-gt`|Greater than|`if [ "$x" -gt "$y" ]; then`|
|`-lt`|Less than|`if [ "$x" -lt "$y" ]; then`|
|`-ge`|Greater than or equal to|`if [ "$x" -ge "$y" ]; then`|
|`-le`|Less than or equal to|`if [ "$x" -le "$y" ]; then`|

### Example Usage

#### String Comparison

```bash
string1="hello"
string2="world"

if [ "$string1" = "$string2" ]; then
	echo "Strings are equal"
else
	echo "Strings are not equal"
fi
```

#### Numeric Comparison

```bash
x=5
y=10

if [ "$x" -lt "$y" ]; then
  echo "$x is less than $y"
fi
```

#### Check If command executed successfully

```bash
if grep -q 'pattern' file.txt; then
  # If grep finds a match
  echo "Pattern found in file.txt"
  # Add your additional commands here
else
  # If grep does not find a match
  echo "Pattern not found in file.txt"
  # Add your additional commands here
fi
```
