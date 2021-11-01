***
# Exit Statuses and Return Codes
***
***
# Exit Status / Return Code
* every command returns an exit status
* exit status aka return code
* the codes range from 0 to 255
* **0 = the command ran successfully**
* anything other than 0 is an error or warning
* these codes can be used for error checking
* you can use ```man``` or ```info``` to find the meaning of an exit status
* ex: ```grep``` will return 1 if no search pattern is found
* ```$?``` contains the return code of the previously executed command
```
ls /not/here/
echo "$?"
# it will output 2
```
* example of using an error code:
```
#!/bin/bash

HOST="google.com"

ping -c 1 $HOST

if [ "$?" -eq "0" ]
then
  echo "$HOST reachable."
else
  echo "$HOST unreachable."
fi
```
* another example - only checking for an error:
```
#!/bin/bash

HOST="google.com"

ping -c 1 $HOST

if [ "$?" -ne "0" ]
then
  echo "$HOST unreachable."
fi

```
* another example - assign the return code to a variable: 
```
#!/bin/bash

HOST="google.com"

ping -c 1 $HOST
RETURN_CODE=$?

if [ "$RETURN_CODE" -ne "0" ]
then
  echo "$HOST unreachable."
fi
```
***
***
# Using && or || with exit statuses 
* you can also use && or || with return codes
* && = and
```
# both will run
# the second command will only run if the first command succeeds 
mkdir /tmp/bak && cp test.txt /tmp/bak
```
* || = or
```
# if the first command suceeds then the second command will not run
# if the first command fails then the second command will be run
cp test.txt /tmp/bak/ || cp test.txt /tmp
```
### and &&
* example of using &&
```
#!/bin/bash
HOST="google.com"
ping -c 1 $HOST && echo "$HOST reachable."
```
### or ||
* example of using ||
```
#!/bin/bash
HOST="google.com"
ping -c 1 $HOST || echo "$HOST unreachable."
```
***
***
# Chaining multible commands together on a single line with a semicolon
* you can chain several seperate commands together with a semicolon to ensure they all get executed 
* the semi colon does not check the exit status of the previous command
```
cp test.txt /tmp/bak/ ; cp test.txt /tmp
```
***
***
# Creating an exit status for your shell script
* your shell script returns an exit status when its run
* you can control the exit status in the script
* by default the exit code will be whatever code the last command returns
* to control the exit status use the ```exit``` command
* example: 
```
# end of script
exit 0
```
* whenever the exit code is reached the shell script will stop running
* example of using an exit code in a script:
```
#!/bin/bash
HOST="google.com"
ping -c 1 $HOST

if [ "$?" -ne "0" ]
then
  echo "$HOST unreachable."
  exit 1
fi

exit 0
```
* if another script is calling your script the exit codes can be useful tools