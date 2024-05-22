# Bash Shell Scripting Notes

## Table of Contents
1. [Introduction](#introduction)
2. [Basic Commands](#basic-commands)
   1. [Executing a Shell Script](#executing-a-shell-script)
   2. [First Line of a Shell Script](#first-line-of-a-shell-script)
   3. [Printing/Displaying](#printingdisplaying)
   4. [Comments](#comments)
   5. [Variables](#variables)
   6. [Using Variables](#using-variables)
   7. [Command Substitution](#command-substitution)
   8. [Quotes in Bash](#quotes-in-bash)
   9. [Export Variables](#export-variables)
   10. [Accepting User Input (STDIN)](#accepting-user-input-stdin)
3. [Control Structures](#control-structures)
   1. [Tests](#tests)
   2. [The `if` Condition](#the-if-condition)
   3. [The `if-else` Condition](#the-if-else-condition)
   4. [The `if-elif-else` Condition](#the-if-elif-else-condition)
   5. [The `for` Loop](#the-for-loop)
   6. [The `while` Loop](#the-while-loop)
   7. [Switch-Case Statements](#switch-case-statements)
4. [Advanced Topics](#advanced-topics)
   1. [Positional Parameters](#positional-parameters)
   2. [Chaining Commands](#chaining-commands)
   3. [Exit Statuses](#exit-statuses)
   4. [Functions](#functions)
   5. [Debugging Shell Scripts](#debugging-shell-scripts)
   6. [Logging](#logging)
   7. [File Types (DOS/WINDOWS vs UNIX/LINUX)](#file-types-doswindows-vs-unixlinux)
5. [Best Practices](#best-practices)

## Introduction

Any series of terminal commands can be put into a script. The shell, which is an interpreter, reads the script and executes those commands. Shell Scripting is useful to automate tasks, performing complex execution, etc.

## Basic Commands

### Executing a Shell Script

Give execute permission to your script. Example: `chmod +x /path/to/yourscript.sh`

And to run your script: `/path/to/yourscript.sh`

We can also use the relative path if it is known: `./yourscript.sh` (`./` is necessary if the directory is not in `$PATH`!)

### First Line of a Shell Script

When we create a shell script and wish to run it, we need to make sure it has the execute permission. Use `chmod` command to add it, if execute permission does not exist.

Every script STARTS with a line like this:

`#!/path/to/interpreter`

The `#` (sharp) and `!` (bang/exclamation) are collectively known as the 'SHEBANG'. The first line tells us which interpreter (Shell) is supposed to execute this script!

Examples:
- `#!/bin/csh` = c shell
- `#!/bin/ksh` = k shell
- `#!/bin/zsh` = z shell
- `#!/bin/bash` = bash shell

You don't have to use a shell as an interpreter: Example: `#!/usr/bin/python` => Uses the python interpreter (Hence, a python script)

### Printing/Displaying

`echo` command = It prints the supplied argument/string. Every echo statement prints on a NEW LINE.

Example: `echo "Hello World!"` => Output: `Hello World!`

### Comments

Every line other than the first line (#! /bin/..) that STARTS with a `#` (pound/sharp/hash) marks a comment.

```bash
#!/bin/bash

# Let's print something        => A comment

echo "Hello There"

# End of printing                => A comment
```

- If `#` STARTS on the line, the WHOLE LINE is IGNORED.
- If `#` appears in the MIDDLE of a line, anything to the RIGHT of a `#` is IGNORED.

### Variables

Storage locations that have a name. They are 'name-value' pairs.

Syntax: `VARIABLE_NAME="Value"`

**NOTE: NO SPACES before or after the `=`**

- The variable names are CASE-SENSITIVE!.
- And, by "convention", they are usually in UPPERCASE.

### Using Variables

Precede the variable name with a `$` sign. Example:
```bash
MY_SHELL="bash"
echo "This script uses the $MY_SHELL shell"
```
Output: This script uses the bash shell.

Alternatively: (Optional)

Enclose the variable in curly brackets `{}` and precede it with a `$`, Example:
```bash
MY_SHELL="bash"
echo "I am ${MY_SHELL}ing shell"
```
Output: I am bashing on my keyboard

### Command Substitution

```bash
VAR_NAME=$(command)
```

(or)

```bash
VAR_NAME=`command`
```

(Command enclosed with backticks: Older Scripts)

### Quotes in Bash

```bash
echo "The user is $USER" --> The user is John
echo 'The user is $USER' --> The user is $USER
```

### Export Variables

In every user home directory there is a hidden file called `.bashrc`. If you place export variable and value in this file, it will become a permanent export variable. We often use it for setting environment variables like `JAVA_HOME`, `MAVEN_HOME`. If you want to add an export variable globally for all users, then edit `/etc/profile` and add export variable.

```bash
ls -a
vi .bashrc (edit this file and update export variable)
export JAVA_HOME="usr/bin/jvm"
```

### Accepting User Input (STDIN)

`read` command.

Syntax: `read -p "PROMPT" VARIABLE`

Example:
```bash
read -p "Enter a UserName: " USER
echo "ARCHIVING $USER"
```

## Control Structures

### Tests

Syntax: `[ condition-to-test-for ]`

Returns true if the test passes, else false. Example:

`[ -e /etc/passwd ]` = tests if the '/etc/passwd' file exists.

#### File Operator Tests

General Test Syntax: `[ -flag fileOrDirPath]`
Flags:
- `-d` = True if file is a directory
- `-e` = True if file exists
- `-f` = True if file exists and is a regular file
- `-s` = True if file exists and is NOT empty
- `-r` = True if file is readable by you
- `-w` = True if file is writable by you
- `-x` = True if file is executable by you

#### String Operator Tests

General Test Syntax: `[ -flag STRING]`

Flags:
- `-z` = True if STRING is empty
- `-n` = True if STRING is NOT empty

Equality Tests:
- `STRING1 = STRING2` = True if strings are equal
- `STRING1 != STRING2` = True if strings are NOT equal

#### Arithmetic Operator Tests

General Test Syntax: `[ arg1 -flag arg2]`

Flags:
- `-eq` = True if arg1 equals arg2
- `-ne` = True if arg1 is NOT equal to arg2
- `-lt` = True if arg1 is LESS THAN arg2
- `-le` = True if arg1 is LESS THAN OR EQUAL TO arg2
- `-gt` = True if arg1 is GREATER THAN arg2
- `-ge` = True if arg1 GREATER THAN OR EQUAL TO arg2

### The `if` Condition

```bash
if [ condition-is-true ]
then
    command 1
    command 2
    ...
    command N
fi
```

### The `if-else` Condition

```bash
if [ condition-is-true ]
then
    commands 1 ... N
else
    commands 1 ... N
fi
```

### The `if-elif-else` Condition

```bash
if [ condition-is-true ]
then
    commands 1 ... N
elif [ condition-is-true ]
then
    commands 1 ... N
else
    commands 1 ... N
fi
```

### The `for` Loop

```bash
for VARIABLE_NAME in ITEM_1 ... ITEM_N
do
    command 1
    command 2
    ...
    command N
done
```

First item in the block is assigned to the variable and commands are executed, next item in the block is assigned to the variable and commands are executed again, and so on ...

Example:
```bash
for COLOR in red green blue
do
    echo "COLOR: $COLOR"
done
```

Output:
```bash
COLOR: red
COLOR: green
COLOR: blue
```

### The `while` Loop

Loop control (Alternative to `for`)

Syntax:
```bash
while [ CONDITION_IS_TRUE ]
do
    command 1
    command 2
    ...
    command N
done
```

### Switch-Case Statements

(Similar to `Switch-Case`) => Testing for multiple values. Use in place of many 'if-elif-elif-elif...' scenarios!

Syntax:
```bash
case "$VAR" in


    pattern_1)
        #commands go here
        ;;
    pattern_N)
        #commands go here
        ;;
esac
```

Examples:
```bash
case "$1" in
    start)
        /usr/sbin/sshd                        # Executes the script at the specified path!
        ;;
    stop)
        kill $(cat /var/run/sshd.pid)
        ;;
esac
```

Example with wildcards and pipes:
```bash
case "$1" in
    start|START)
        /usr/sbin/sshd
        ;;
    stop|STOP)
        kill $(cat /var/run/sshd.pid)
        ;;
    *)
        echo "Usage: $0 start|stop" ; exit 1
        ;;
esac
```

## Advanced Topics

### Positional Parameters

Syntax (On the CLI): `$ script.sh parameter1 parameter2 parameter3`

- `$0` = "script.sh" (The script itself)
- `$1` = "parameter1"
- `$2` = "parameter2"
- `$3` = "parameter3"

We can Assign Positional Parameters to Variables. Example:

`USER=$1`

#### The `$@`:

`$@` contains all the parameters starting from Parameter 1 to the last parameter. It can be used to loop over parameters. Example:
```bash
for USER in $@
do
    echo "Archiving user : $USER"
    ...
    ...
done
```

### Chaining Commands

- `&&` => AND => Executes commands one after the other UNTIL one of them FAILS. (in that case -> short-circuiting)

(It executes commands as long as they are returning exit statuses `0`. STOPS as soon as a command does NOT return `0`)

Syntax: `cmd1 && cmd2 && ...`

- `||` => OR => Executes commands one after the other UNTIL one of them SUCCEEDS. (in that case -> short-circuiting)

(It executes commands as long as they are returning exit statuses NOT `0`. STOPS as soon as a command returns `0`)

Syntax: `cmd1 || cmd2 || ...`

- `;` => Semicolon => Executes commands ONE AFTER ANOTHER without checking the exit statuses/return codes.

(It is the same as/equivalent to executing each of the commands on a separate line)

Syntax: `cmd1 ; cmd2 ; ...`

### Exit Statuses

Every command returns an exit status. Range of the status is from `0 - 255`. It is used for Error checking.

- `0`                         = Success
- Other than `0`         = Error condition

**Use `man` on the command to find out what exit status means what (for the command).**

#### The `$?`: (Return code/exit status)

`$?` contains the return code (exit status) of the 'previously executed' command.

Example:
```bash
ls /not/here
echo "$?"
```

Output: `2` is echoed, which is the return command.

Example:
```bash
HOST="google.com"
ping -c 1 $HOST                # -c tells the command to send only 1 packet to test connection
if [ "$?" -eq "0" ]
then
    echo "$HOST reachable."
else
    echo "$HOST unreachable."
fi
```

#### Storing return code/exit status in a variable:

Example: 
```bash
ping -c 1 "google.com"
RETURN_CODE=$?                # Now, we can use the variable RETURN_CODE anywhere in the script.
```

### Functions

Reduces script length, **"DRY"(Don't Repeat Yourself) - concept of functions**.

A function:
- Is a block of reusable code.
- Must be defined before use.
- Has parameter support.
- It can return an "exit status/return code".

**Method 1:**
```bash
function function-name() {
    # code goes here
}
```

**Method 2:**
```bash
function-name() {
    # code goes here
}
```

#### Calling a function:

`function-name`

We do **NOT** use parentheses `()` in the function like in other programming languages. Functions need to be defined before they are used. (In Top Down order of parsing) (That is, Function Definition must have been scanned (Top->Down parsing) before the call to the function)

**Functions can call other functions**

#### Parameters to functions:

`function-name parameter1 parameter2 ...`

- `$1`, `$2`, ... = Parameter1, Parameter2, ...
- `$@` = Array of all the parameters

Example:
```bash
function hello() {
    echo "Hello, $1"
}
hello Jason
```

Output: `"Hello, Jason"`

#### Variable Scope:

- ALL Variables are GLOBAL by Default!
- Variables have to be DEFINED before Use.

Therefore, All variables defined 'before' a 'function call' can be accessed within it. Those that are defined 'after' the 'function call' **cannot** be accessed.

#### Local Variables:

Variables that can be accessed only within the function that it is declared. Use the keyword `local`.

Syntax: `local LOCAL_VAR=someValue`

Only functions can have local variables! (Try to keep variables local inside a function)

#### Exit Status/Return Code of functions:

- Explicitly: `return <RETURN_CODE>`

Note: For the WHOLE SCRIPT, we used the `exit <RETURN-CODE>` command. For functions, it is `return` keyword.

- Implicitly: The exit status of the last command executed within the function.

Exit status range: `0 to 255`

- `0` = Success
- All other values = errors of some kind

- `$?` = gets the exit status of last executed command (after execution of cmd)/function (after the call)/script (terminal))

### Debugging Shell Scripts

'bug' => Means error

- Examine inner workings of your script
- Get to the Source/Root of the problem
- Fix Bugs (errors)

#### `-x` option:

Debug Whole script:

- `#!/bin/bash -x` = prints commands and their arguments as they execute. That is: Values of variables, values of wildcard matches.

- Debug from command line: 
    - `set -x` = Start Debugging
    - `set +x` = Stop Debugging

Example: 
```bash
$ set -x
$ ./scriptName.sh
<output>
$ set +x
```

- Debug only a portion of the code:
Example:
```bash
#!/bin/bash
...
set -x
echo $VAR_NAME
set +x
...
```

#### Exit on Error:

- `-e` flag. (Exit immediately if a command exists with a non-zero status.)

Syntax: `#!/bin/bash -e`

Example: It can be combined with the trace (-x) option.
- `#!/bin/bash -e -x`
- `#!/bin/bash -ex`
- `#!/bin/bash -xe`
- `#!/bin/bash -x -e`

#### Print Shell Input Lines (As they are being read):

- `-v` flag. (Can also be combined with -x and -e.)

Prints input lines before (without) any substitutions and expansions are performed. Therefore, All the lines of the shell script are printed as they are, and the outputs of printing commands (like echo) are also displayed.

- `#!/bin/bash -vx` = Useful, because we can see trace (substituted input) lines as well as shell script lines!

### Logging

`Syslog` => Uses standard facilities and severities to categorize messages.

- `Facilities`: `kern`, `user`, `mail`, `daemon`, `auth`, `local0`, `local7`, etc.
- `Severities`: `emerg`, `alert`, `crit`, `err`, `warning`, `notice`, `info`, `debug`.

#### Log files locations are CONFIGURABLE:

1. '/var/log/messages' 

(or)

2. '/var/log/syslog'

(Location depends on system)

#### Logging with `logger`:

`logger` is a command line utility - used for logging 'syslog' messages. By default, it creates `user.notice` messages.

1. Basic logging message: `logger "Message"`

2. Logging message with facility and severity: Syntax: `logger -p facility.severity "Message"` 

Example: `logger -p local0.info "Message"`

3. Tagging the log message: Use the `-t` option followed by tagName

Usually you want to use the script's name as tag in order to easily identify the source of the log message. `logger -t myscript -p local0.info "Message"`

4. Include PID (Process ID) in the log message: use `-i` option: `logger -i -t myscript "Message"`

5. Additionally display log message on screen (apart from already logging it to the log file): use `-s` option

Example: `logger -s -p local0.info "Message"`

### File Types (DOS/WINDOWS vs UNIX/LINUX)

Control character is used to represent end of line in both DOS and Unix text files.

Control Character:
1. Unix/Linux: Line Feed
2. DOS: Carriage return & a Line Feed (2 characters)

- `cat -v script.sh` = View the file along with the carriage returns (^M)

When opening Linux/Unix text files on a DOS/Windows system: We may see one long line without new lines.

And, in the opposite: We may see additional characters on Unix/Linux (`^M`). => Might run into errors while executing the files.

Therefore, need to

 remove the carriage returns in order to run the file. The shebang `#!` is very important.

#### Knowing what type of file: (To which shell does the script belong to?)

`file script.sh` 

Example Output: 
- `script.sh: Bourne-Again shell script, ASCII text executable` => UNIX script,
- `script.sh: Bourne-Again shell script, ASCII text executable, with CRLF line terminators` => DOS script,

#### Converting DOS text scripts to UNIX scripts:

- `dos2unix script.sh` => Removes incompatible characters (example: DOS carriage returns) in DOS to match with UNIX text scripts. (So that we can run it on UNIX/LINUX)

Confirm the removal of incompatible characters by running `file script.sh` again to see what type of shell the script runs in. (Should be one of the unix shells that you are using.)

#### Converting UNIX text scripts to DOS scripts:

- `unix2dos script.sh` => Does the opposite of dos2unix. (So that we can run it on DOS/WINDOWS)

## Best Practices

1. Does your script start with a shebang?
2. Does your script include a comment describing the purpose of the script?
3. Are the global variables declared at the top of your script, following the initial comment(s)?
4. Have you grouped all of your functions together following the global variables?
5. Do your functions use local variables?
6. Does the main body of your shell script follow the functions?
7. Does your script exit with an explicit exit status?
8. At the various exit points, are exit statuses explicitly used?

**EXAMPLE**
```bash
#!/bin/bash
#
# <Replace with the description and/or purpose of this shell script.>

GLOBAL_VAR1="one"
GLOBAL_VAR2="two"

function function_one() {
    local LOCAL_VAR1="one"
    # <Replace with function code.>
}

# Main body of the shell script starts here.
#
# <Replace with the main commands of your shell script.>

# Exit with an explicit exit status. Example: exit 0
```

---

# Learning Bash

## Table of Contents
1. [Bash Scripting](#bash-scripting)
2. [Data Structures](#data-structures)
3. [Strict Mode](#strict-mode)
4. [Functions](#functions)
5. [Variables](#variables)
   1. [Built-in Variables](#built-in-variables)
6. [Regular Expressions and Globbing](#regular-expressions-and-globbing)
7. [String Manipulation](#string-manipulation)
8. [Debugging](#debugging)
9. [Best Practices](#best-practices)
10. [Further Reading](#further-reading)
11. [Version](#version)

## Bash Scripting

A Bash *script* or *program* is simply a file that contains Bash commands. Your `.bash_profile` and `.bashrc` files are Bash scripts. You can run a Bash script using the `source my_script` command or using `bash my_script` (or by adding `#!/usr/bin/env bash` to the start of your script and making your file executable, i.e. `chmod 755 my_script`) but there is an important difference between the two. Using `source` causes the commands in the script to be run as if they were part of your login session, whereas using `bash` will run the script in a *subshell*. This means that a copy of the shell, which is a subprocess of the parent, is invoked.

Subshells inherit the following from their parents:

- The current directory
- Environment variables
- Standard input, output, and error, plus any other open file descriptors
- Signals that are ignored

Subshells do not inherit the following from their parents:

- Shell variables
- Handling of signals that are not ignored

## Data Structures

[Bash variables are untyped](https://tldp.org/LDP/abs/html/untyped.html) and they are essentially character strings but if a variable contains only digits, Bash allows simple arithmetic operations.

```bash
x=1985
echo $(( x - 1 ))
```

    1984

Note what happens when a variable is a string.

```bash
x='nine'
echo $(( x - 1 ))
```

    -1

```bash
x=nineteeneightyfour
echo $(( x - 1 ))
```

    -1

Be careful when using untyped variables.

```bash
x=nineteeneightyfour
xx=$(( x - 1 ))
echo $(( xx + 1985))
```

    1984

Bash supports indexed arrays and associative arrays (also known as hashes or dictionaries). Since Bash variables are untyped, array elements can contain characters and numbers.

The easiest way to manually create an indexed array is to use parentheses. Arrays are zero-indexed.

```bash
fruits=( apple banana cherry durian elderberry )

echo ${fruits[0]}
```

    apple

Negative indexing is supported.

```bash
fruits=( apple banana cherry durian elderberry )
echo ${fruits[-1]}
echo ${fruits[-2]}
```

    elderberry
    durian

Use this syntax to refer to all elements.

```bash
fruits=( apple banana cherry durian elderberry )
echo ${fruits[@]}
```

    apple banana cherry durian elderberry

Associative arrays must be declared before they are created using `declare` and `-A`. Elements are referenced using square brackets not braces.

```bash
declare -A fruits_hash

fruits_hash=(
  [a]=apple
  [b]=banana
  [c]=cherry
  [d]=durian
  [e]=elderberry
)

echo ${fruits_hash[a]}
echo ${fruits_hash[c]}
```

    apple
    cherry

Use the following syntax to get the array length.

```bash
fruits=( apple banana cherry durian elderberry )
echo ${#fruits[@]}
```

    5

Use the following syntax to get all the indexes.

```bash
fruits=( apple banana cherry durian elderberry )
echo ${!fruits[@]}
```

    0 1 2 3 4

Loop through each element.

```bash
fruits=( apple banana cherry durian elderberry )
for i in ${fruits[@]}; do
  echo ${i}
done
```

    apple
    banana
    cherry
    durian
    elderberry

Loop through each element’s index.

```bash
fruits=( apple banana cherry durian elderberry )
for i in ${!fruits[@]}; do
  echo ${i}
done
```

    0
    1
    2
    3
    4

Loop through each element’s index, i.e. the key.

```bash
declare -A fruits_hash

fruits_hash=(
  [a]=apple
  [b]=banana
  [c]=cherry
  [d]=durian
  [e]=elderberry
)
for i in ${!fruits_hash[@]}; do
  echo ${i}
done
```

    e
    d
    c
    b
    a

Use `unset` to delete an element (even if it is in the middle of an array).

```bash
fruits=( apple banana cherry durian elderberry )
unset fruits[3]
echo ${fruits[@]}
```

    apple banana cherry elderberry

## Strict Mode

Notes adapted and expanded from [Better Bash Scripting in 15 Minutes](https://robertmuth.blogspot.com/2012/08/better-bash-scripting-in-15-minutes.html).

Starting Bash scripts with the following:

```bash
#!/usr/bin/env bash
set -o nounset
set -o errexit
```

will deal with two very common errors:

1.  Referencing undefined variables, which defaults to ''
2.  Ignoring failing commands

They are the same as `-u` and `-e`, which you may be familiar with when using the unofficial Bash strict mode `set -euo pipefail`. The longer versions are more readable and therefore may be more preferable.

Sometimes you do not want a script to exit when a command fails and this can be achieved by using the following idiom:

```bash
#!/usr/bin/env bash
set -o nounset
set -o errexit

# the grep command will cause the script to exit because grep returns an exit
# code > 0 when it has no matches
# grep nothing README.md

# use the following to ignore a "failing" command
if ! grep nothing README.md ; then
   >&2 echo "Failure ignored"
fi

>&2 echo "Done"
exit 0
```

## Functions

The basic syntax of a function is:

```bash
function_name(){
}
```

When passing arguments to Bash functions:

- The passed parameters are `$1`, `$2`, `$3`, ..., `$n`, corresponding to the position of the parameter after the function’s name.
- The `$0` variable is reserved for the function’s name (but this doesn’t seem like the case in the example below).
- The `$#` variable holds the number of positional parameters/arguments passed to the function.
- The `$*` and `$@` variables hold all positional parameters/arguments passed to the function.
- When double-quoted, `"$*"` expands to a **single string** separated by space (or what IFS is set to) - "$1 $2 \$n".
- When double-quoted, `"$@"` expands to separate strings - "$1" "$2" "$n

".
- When not double-quoted, `$*` and `$@` are the same.

```bash
my_func(){
   echo $0
   echo function name is ${FUNCNAME[0]}
   echo first arg is $1
   echo $# args passed
   echo $*
   echo $@
}

my_func one two three
```

    bash
    function name is my_func
    first arg is one
    3 args passed
    one two three
    one two three

Bash lets you define functions that behave like other commands.

```bash
extract_comment(){
  grep "^#"
}

cat script/ignore_exit_code.sh | extract_comment
```

    #!/usr/bin/env bash
    # the grep command will cause the script to exit because grep returns an exit
    # code > 0 when it has no matches
    # grep nothing README.md
    # use the following construct to ignore a "failing" command

Redirect input to the function.

```bash
extract_comment(){
  grep "^#"
}
comments=$(extract_comment < script/ignore_exit_code.sh)
echo ${comments}
```

    #!/usr/bin/env bash # the grep command will cause the script to exit because grep returns an exit # code > 0 when it has no matches # grep nothing README.md # use the following construct to ignore a "failing" command

Function to sum numbers (one per line) in a file. Local scope is achieved using `local`, which means that the variable is only visible within a block of code, i.e. the function.

```bash
# iterating over stdin
sum_line(){
    local sum=0
    local line=''
    while read line ; do
        sum=$((${sum} + ${line}))
    done
    >&2 echo ${sum}
}

echo -e '1\n2\n3\n4\n5' > num.txt
sum_line < num.txt

rm num.txt
```

    15

A classic logger that makes use of `$@`, which contains all arguments passed to the function.

```bash
log(){
   local prefix="[$(date +%Y/%m/%d\ %H:%M:%S)]: "
   >&2 echo "${prefix} $@"
}
log "INFO" "a message"
```

    [2023/08/28 00:55:23]:  INFO a message

## Variables

Use `local` to set local scoping for variables but this seems to be for use with functions only.

```bash
local x=14
```

    bash: line 1: local: can only be used in a function

Use `readonly` to set immutable variables.

```bash
readonly x=1984
echo ${x}

x=2023
```

    1984
    bash: line 4: x: readonly variable

Note that you cannot `unset` a readonly variable; it exists until the shell exits.

Assign variable or output an error, which is a useful shortcut to check whether an argument was passed to a function.

```bash
say(){
   smt=${1?Error: missing input}
   echo ${smt}
}

# this exits with a code of 1
say
# echo $?
# 1
```

    Error in running command bash

Functions work as intended when an argument is passed.

```bash
say(){
   smt=${1?Error: missing input}
   echo ${smt}
}

say meow
```

    meow

You can also set a default value, instead of exiting with an error.

```bash
say2(){
   smt=${1:-something}
   echo ${smt}
}

say2

say2 nothing
```

    something
    nothing

### Built-in Variables

Some useful built-in variables.

- `$0` - name of the script
- `$n` - positional parameters to script/function
- `$$` - PID of the script
- `$!` - PID of the last command executed (and run in the background)
- `$?` - exit status of the last command (`${PIPESTATUS}` for pipelined commands)
- `$#` - number of parameters to script/function
- `$@` - all parameters to script/function (sees arguments as separate word)
- `$*` - all parameters to script/function (sees arguments as single word)

## Regular Expressions and Globbing

Globbing is a method for creating patterns that are used for matching; use `==` for string matching with globbing.

Globbing will return true.

```bash
t="abc123"

[[ "$t" == abc* ]] && echo True
```

    True

Literal matching is turned on with quotes.

```bash
t="abc123"
[[ "$t" == 'abc*' ]] || echo False
[[ "$t" == "abc*" ]] || echo False
```

    False
    False

Use `=~` for regular expression matching, which is only supported using double brackets.

```bash
t="abc123"
[[ "$t" =~ [abc]+[123]+ ]] && echo True
```

    True

Literal matching is turned on again with quotes.

```bash
t="abc123"
[[ "$t" =~ "abc*" ]] || echo False
```

    False

## String Manipulation

Length of a string.

```bash
#  01234567890123456789
f="path1/path2/file.ext"
echo ${#f}
```

    20

Slicing syntax: `${<var>:<start>}` or `${<var>:<start>:<length>}` where the position is 0-based.

Start from position 6.

```bash
#  01234567890123456789
f="path1/path2/file.ext"
echo ${f:6}
```

    path2/file.ext

Start from position 6, and output 5 characters.

```bash
f="path1/path2/file.ext"
echo ${f:6:5}
```

    path2

Negative indexing; note the space before “-”.

```bash
f="path1/path2/file.ext"
echo "${f: -8}"
```

    file.ext

Single substitution with globbing.

```bash
f="path1/path2/file.ext"
echo ${f/path?/path3}
```

    path3/path2/file.ext

Global substitution with globbing.

```bash
f="path1/path2/file.ext"
echo ${f//path?/path3}
```

    path3/path3/file.ext

Splitting; note the space before the right brace, which is used for the splitting.

```bash
f="path1/path2/file.ext"
sep="/"
array=(${f//${sep}/ })
echo ${array[@]}
```

    path1 path2 file.ext

Deletion with globbing; delete everything before the period.

```bash
f="path1/path2/file.ext"
echo ${f#*.}
```

    ext

Non-greedy deletion at the start of the string.

```bash
f="path1/path2/file.ext"
echo ${f#*/}
```

    path2/file.ext

Use extra `#` for greedy deletion at the start of the string.

```bash
f="path1/path2/file.ext"
echo ${f##*/}
```

    file.ext

Non-greedy deletion starting from the string end; delete everything until matching a `/` (including the `/`).

```bash
f="path1/path2/file.ext"
echo ${f%/*}
```

    path1/path2

Greedy deletion from the end.

```bash
f="path1/path2/file.ext"
echo ${f%%/*}
```

    path1

## Debugging

To perform a syntax check/dry run of a Bash script:

```bash
bash -n script/ignore_exit_code.sh
```

To produce a trace of every command executed run:

```bash
bash -v script/ignore_exit_code.sh
```

    #!/usr/bin/env bash
    set -o nounset
    set -o errexit

    # the grep command will cause the script to exit because grep returns an exit
    # code > 0 when it has no matches
    # grep nothing README.md

    script_dir=$(realpath $(dirname $0))
    infile=${script_dir}/../README.md

    # use the following construct to ignore a "failing" command
    if ! grep -q not_going_to_find_this ${infile} ; then
       >&2 echo "Failure ignored; continuing..."
    fi

    if grep -q e ${infile} ; then
       >&2 echo "The letter [e] was found in ${infile}"
    fi
    The letter [e] was found in /home/runner/work/learning_bash/learning_bash/script/../README.md

    >&2 echo "Done"
    Done
    exit 0

To produce a trace of the expanded command use:

```bash
bash -x script/ignore_exit_code.sh
```

    + set -o nounset
    + set -o errexit
    +++ dirname script/ignore_exit_code.sh
    ++ realpath script
    + script_dir=/home/runner/work/learning_bash/learning_bash/script
    + infile=/home/runner/work/learning_bash/learning_bash/script/../README.md
    + grep -q not_going_to_find_this /home/runner/work/learning_bash/learning_bash/script/../README.md
    + grep -q e /home/runner/work/learning_bash/learning_bash/script/../README.md
    + echo 'The letter [e

] was found in /home/runner/work/learning_bash/learning_bash/script/../README.md'
    The letter [e] was found in /home/runner/work/learning_bash/learning_bash/script/../README.md
    + echo Done
    Done
    + exit 0

`-v` and `-x` can also be made permanent by adding `set -o verbose` and `set -o xtrace` to the script.

## Best Practices

- Start each script with `#!/usr/bin/env bash` then with `set -euo pipefail`

  - `-e` is short for `errexit` and if a command fails your script will exit.
  - `-u` is short for `nounset` and your script will exit when a variable is undeclared.
  - `pipefail` sets the result of a pipeline to a non-zero status if any command in the pipeline had a non-zero status.
  - `set -euo pipefail` can be split up if you think it is more readable

```bash
set -o nounset
set -o errexit
set -o pipefail
```

- Note that some commands exit with a non-zero status, even if it did "not fail".

```bash
echo hi | grep no
echo $?
```

    1

- I prefer using `${var}` instead of `$var` for all variables.

- I also prefer snake_case over camelCase.

- Warnings and errors should go to `STDERR` and I like to include the redirection at the front because it is more readable. The following commands are the same; you be the judge of which is more readable.

```bash
>&2 echo ERROR
echo ERROR >&2
```

    ERROR
    ERROR

- To make variables local to a function, declare them with the `local` builtin command.

- Use `$()` instead of backticks ``` `` ``` because it is easier to specify and see nested subshells using `$()`.

- Use `[[]]` (double brackets) over `[]` because it offers syntactical improvements and new functionality

  - `||` - logical or (double brackets only)
  - `&&` - logical and (double brackets only)
  - `<` - string comparison (no escaping necessary within double brackets)
  - `=` - string matching with globbing
  - `==` - string matching with globbing (double brackets only)
  - `=~` - string matching with regular expressions (double brackets only)
  - `-n` - string is non-empty
  - `-z` - string is empty
  - `-eq` - numerical equality
  - `-lt` - numerical comparison
  - `-ne` - numerical inequality

- Avoid temporary files by using the `<()` operator, which transforms a command into something that can be used as a filename,
  e.g. `diff <(wget -O - URL1)   <(wget -O - URL2)`.

- Heredocs are handy for passing multi-line strings to a command. Note how variable interpolation is set.

Variable interpolation.

```bash
var=test
cat << EOF
one
${var}
three
EOF
```

    one
    test
    three

No variable interpolation.

```bash
var=test
cat << 'EOF'
one
${var}
three
EOF
```

    one
    ${var}
    three

- If your script is getting big (over 100 lines), consider splitting it up into functions stored in different files.

- Lastly, if your code is getting too complicated, consider using another programming language. They all have their advantages and disadvantages, so try to pick one that suits your problem. Python is often a good choice for many different problems.

## Further Reading

- [Advanced Bash scripting guide](https://tldp.org/LDP/abs/html/)
- [Bash reference manual](https://www.gnu.org/software/bash/manual/bash.html)

## Version

Bash version used to generate this document.

```bash
bash --version
```

    GNU bash, version 5.1.16(1)-release (x86_64-pc-linux-gnu)
    Copyright (C) 2020 Free Software Foundation, Inc.
    License GPLv3+: GNU GPL version 3 or later <http://gnu.org/licenses/gpl.html>

    This is free software; you are free to change and redistribute it.
    There is NO WARRANTY, to the extent permitted by law.
```
```



CHeetSHeet : 


```markdown
# Bash Commands Cheat Sheet

## Basic Commands
- **Execute Script**: `chmod +x /path/to/script.sh && /path/to/script.sh`
- **Shebang**: `#!/bin/bash`
- **Print/Display**: `echo "Hello World!"`
- **Comments**: `# This is a comment`
- **Variable Assignment**: `VARIABLE_NAME="Value"`
- **Using Variables**: `echo $VARIABLE_NAME`
- **Command Substitution**: `VAR=$(command)`
- **Quotes**: 
  - Double Quotes: `echo "The user is $USER"`
  - Single Quotes: `echo 'The user is $USER'`
- **Export Variables**: `export VARIABLE_NAME="Value"`
- **User Input**: `read -p "Enter input: " VARIABLE`

## Control Structures
- **Test Syntax**: `[ condition ]`
- **File Tests**:
  - `-d` : True if directory
  - `-e` : True if file exists
  - `-f` : True if regular file
  - `-s` : True if file is not empty
  - `-r` : True if file is readable
  - `-w` : True if file is writable
  - `-x` : True if file is executable
- **String Tests**:
  - `-z STRING` : True if string is empty
  - `-n STRING` : True if string is not empty
  - `STRING1 = STRING2` : True if strings are equal
  - `STRING1 != STRING2` : True if strings are not equal
- **Arithmetic Tests**:
  - `-eq` : Equal
  - `-ne` : Not equal
  - `-lt` : Less than
  - `-le` : Less than or equal
  - `-gt` : Greater than
  - `-ge` : Greater than or equal

## Conditions and Loops
- **If Condition**:
  ```bash
  if [ condition ]; then
    commands
  fi
  ```
- **If-Else Condition**:
  ```bash
  if [ condition ]; then
    commands
  else
    commands
  fi
  ```
- **If-Elif-Else Condition**:
  ```bash
  if [ condition ]; then
    commands
  elif [ condition ]; then
    commands
  else
    commands
  fi
  ```
- **For Loop**:
  ```bash
  for VAR in list; do
    commands
  done
  ```
- **While Loop**:
  ```bash
  while [ condition ]; do
    commands
  done
  ```
- **Case Statement**:
  ```bash
  case "$VAR" in
    pattern1)
      commands
      ;;
    pattern2)
      commands
      ;;
  esac
  ```

## Advanced Topics
- **Positional Parameters**:
  - `$0` : Script name
  - `$1` : First parameter
  - `$@` : All parameters
- **Chaining Commands**:
  - `cmd1 && cmd2` : AND
  - `cmd1 || cmd2` : OR
  - `cmd1 ; cmd2` : Sequential
- **Exit Status**:
  - `echo $?` : Last command exit status
- **Functions**:
  ```bash
  function_name() {
    commands
  }
  ```
  - **Local Variables**: `local VAR=value`
  - **Return from Function**: `return <exit_status>`
- **Debugging**:
  - Start Debugging: `set -x`
  - Stop Debugging: `set +x`
  - Exit on Error: `#!/bin/bash -e`
  - Verbose Mode: `#!/bin/bash -v`
- **Logging**:
  - Basic Logging: `logger "Message"`
  - Facility and Severity: `logger -p local0.info "Message"`
  - With Tag: `logger -t tagname "Message"`
  - Include PID: `logger -i "Message"`
- **File Type Conversion**:
  - Convert DOS to UNIX: `dos2unix filename`
  - Convert UNIX to DOS: `unix2dos filename`
```

 ```markdown
## String Manipulation
- **String Length**: `${#VAR}`
- **Substring Extraction**: `${VAR:START:LENGTH}`
- **Single Substitution**: `${VAR/OLD/NEW}`
- **Global Substitution**: `${VAR//OLD/NEW}`
- **Remove Shortest Match from Start**: `${VAR#PATTERN}`
- **Remove Longest Match from Start**: `${VAR##PATTERN}`
- **Remove Shortest Match from End**: `${VAR%PATTERN}`
- **Remove Longest Match from End**: `${VAR%%PATTERN}`

## Globbing and Regular Expressions
- **Globbing Match**: `[[ "$VAR" == pattern ]]`
- **Regex Match**: `[[ "$VAR" =~ regex ]]`

## Arrays
- **Indexed Array Declaration**: `ARRAY=(val1 val2 val3)`
- **Access Element**: `${ARRAY[INDEX]}`
- **All Elements**: `${ARRAY[@]}`
- **Array Length**: `${#ARRAY[@]}`
- **All Indices**: `${!ARRAY[@]}`
- **Associative Array Declaration**: `declare -A ARRAY`
- **Set Associative Array Element**: `ARRAY[key]=value`
- **Access Associative Element**: `${ARRAY[key]}`
- **Unset Element**: `unset ARRAY[INDEX]`

## Process Management
- **Get PID of Last Command**: `echo $!`
- **Kill Process by PID**: `kill PID`
- **Run Command in Background**: `command &`
- **List Running Jobs**: `jobs`
- **Bring Job to Foreground**: `fg %job_number`
- **Send Job to Background**: `bg %job_number`

## File and Directory Operations
- **List Files**: `ls`
- **Change Directory**: `cd /path/to/dir`
- **Copy File**: `cp source destination`
- **Move/Rename File**: `mv source destination`
- **Remove File**: `rm filename`
- **Create Directory**: `mkdir dirname`
- **Remove Directory**: `rmdir dirname`
- **Remove Directory Recursively**: `rm -r dirname`
- **Check File Type**: `file filename`
- **Change File Permissions**: `chmod permissions filename`
- **Change File Ownership**: `chown user:group filename`
- **Create Symbolic Link**: `ln -s target linkname`

## Networking
- **Ping Host**: `ping -c 4 hostname`
- **Get IP Address**: `hostname -I`
- **Download File**: `wget URL`
- **Transfer File**: `scp source user@host:destination`

## Text Processing
- **Print File Content**: `cat filename`
- **Print Line Numbers**: `nl filename`
- **Print First Lines**: `head -n N filename`
- **Print Last Lines**: `tail -n N filename`
- **Find Pattern in File**: `grep "pattern" filename`
- **Count Lines, Words, Characters**: `wc filename`
- **Sort Lines**: `sort filename`
- **Unique Lines**: `uniq filename`
- **Cut Columns**: `cut -d "delimiter" -f fields filename`
- **Replace Text**: `sed 's/old/new/g' filename`
- **Stream Editor for Filtering and Transforming Text**: `awk 'pattern {action}' filename`

## Miscellaneous
- **Display Disk Usage**: `du -sh /path/to/dir`
- **Display Free Disk Space**: `df -h`
- **Show System Uptime**: `uptime`
- **Show Running Processes**: `ps aux`
- **Clear Terminal Screen**: `clear`
- **Display Calendar**: `cal`
- **Show Current Date and Time**: `date`

## Exit and Return Codes
- **Get Last Command Exit Status**: `echo $?`
- **Exit Script with Status**: `exit STATUS_CODE`
- **Return from Function with Status**: `return STATUS_CODE`

## Debugging and Testing
- **Syntax Check**: `bash -n script.sh`
- **Verbose Output**: `bash -v script.sh`
- **Execution Trace**: `bash -x script.sh`

## Environment Variables
- **List All Environment Variables**: `printenv`
- **Get Value of Environment Variable**: `echo $VARIABLE`
- **Set Environment Variable**: `export VARIABLE=value`
- **Unset Environment Variable**: `unset VARIABLE`

## Redirection and Pipelines
- **Redirect Output to File**: `command > file`
- **Append Output to File**: `command >> file`
- **Redirect Input from File**: `command < file`
- **Redirect Output and Errors to File**: `command > file 2>&1`
- **Pipe Command Output**: `command1 | command2`

