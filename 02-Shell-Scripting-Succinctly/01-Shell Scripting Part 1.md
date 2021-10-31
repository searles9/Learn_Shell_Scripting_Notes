***
# Shell Scripting Part 1
***
***
# What is shell scripting
* A script is a series of commands
* Anything you type at the command line can be put into a script
* Scripts are great for automating tasks

### Simple shell script example
```
# !/bin/bash
echo "Scripting is fun!"
```
* make it executable: ```chmod 755 script.sh```
* run it: ```./script.sh```
* if the script is in your path (```echo $PATH```) you can just type the script name and it will execute, otherwise you need to use ```./scriptname.sh```
***
***
# What is the shebang?
* \# = sharp
* ! = bang
* #! = shebang
* you specify the interpreter by adding something after the shebang
```
# ex:
#! /bin/bash

# ex2:
#! /bin/csh
```
* if a script does not contain a shebang the commands are executed using your shell

### Running python scripts with a shell script...
* you can even run python scripts python scripts with shell scripting
```
#! /usr/bin/python
print "This is a Python script."
```
* add permissions to run it: ```chmod 755 hi.py```
* run it: ```./hi.py```
***
***
# Variables
* variables are key value pairs
* syntax:
```
VARIABLE_NAME="value"
```
* variables are case sensitive and should be uppercase by convention
* variables can contain letters, numbers and underscores but they cant start with a number
* "-" and "@" are not valid characters for variable names
* examples: 
```
#! /bin/bash
MY_SHELL="bash"
echo "I like the $MY_SHELL shell."
echo"I like the ${MY_SHELL} shell."  <--- helpful if u wanna add letters right after it
```
### assigning output of a command to a variable
* you can assign the output of a command to a variable:
```
SERVERNAME = $(hostname)

# you can also do this but you shouldn’t as its older syntax
SERVER_NAME=`command`
```

***
***
# Tests 
* you can run tests in your scripts
* basic syntax:
```
[ condition-to-check ]
```
* example:
```
[ -e /etc/passwd ]  <------returns true if the file exists
```
* there are plenty of test conditions you can use. Run ```help test``` at the command line to see what conditions you can use 