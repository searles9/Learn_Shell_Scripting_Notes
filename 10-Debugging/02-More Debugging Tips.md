***
# More Debugging Tips
***
***
* you can create your own debugging code (instead of using the build in code)
* you can make your own special variable called DEBUG:
```
DEBUG=true
DEBUG=false
# to use booleans dont add quotes to the true or false
```
* example of using a debug character:
```
#!/bin/bash

DEBUG=true

if $DEBUG
then
  echo "Debug mode ON."
else
  echo "Debug mode OFF."
fi

#----------------
#!/bin/bash

DEBUG=true
$DEBUG && echo "Debug mode ON."
#----------------
#!/bin/bash

DEBUG=false
$DEBUG || echo "Debug mode OFF."
```
* this kind of debugging can be useful when you want to skip over commands that may take a long time to run
### using echo for debugging
```
# this will echo the command
#!/bin/bash

DEBUG="echo"
$DEBUG ls

# commenting out debug means its set to 
# nothing and will run the command like normal
#!/bin/bash

#DEBUG="echo"
$DEBUG ls

```

* example debug function:
```
#!/bin/bash

debug() {
  echo "Executing: $@"
  $@
}

debug ls
```

### PS4 
* PS4 controls what is displayed before a line when using the -x option 
* The default value is "+"
* Bash variables: BASH_SOUCE, LINENO (line of the script), etc
```
#!/bin/bash -x

PS4='+ $BASH_SOURCE : $LINENO : '

TEST_VAR="test"
echo "$TEST_VAR"

# normal output: test
# output after changing ps4: ./test.sh : 6 : test
```
* more complex example: 
```
#!/bin/bash -x

PS4='+ ${BASH_SOURCE}:${LINENO}:${FUNCNAME[0]}() '

debug() {
  echo "Executing: $@"
  $@
}

debug ls
```
### DOS vs Linux (Unix) file types
* files contain a control character to represent the end of the line
* for linux systems the control character is a line feed
* for DOS (windows) systems it contains 2 characters like shown below
* ex: note the ```^M```
```
cat -v script # to display non printable characters like carrige returns

# test text^M
```
* if you start getting odd errors in your script check to see if there are carriage returns at the end of the lines ( you dont want the carrige returns)
* to check if the file has carriage returns you can use the ```file``` command
```
file script.sh
# this will warn if there are CFLR line terminators
```
* to remove the carriage returns you can use the ```dos2unix``` utility - its usually not installed by default
```
dos2unix script.sh
```
* if you want to add carriage returns so a file can be used on dos you can use the ```unixtodos``` utility
##### How do you end up with carriage returns?
* If you use a windows editor and then upload the file to linux you may end up with carriage returns 
* or if you past from windows into a linux terminal 
* or if you paste fro ma web browser into a terminal 