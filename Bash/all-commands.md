
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
