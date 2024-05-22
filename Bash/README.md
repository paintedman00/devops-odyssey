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
