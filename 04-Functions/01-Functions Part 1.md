***
# Functions Part 1
***
***
* use functions to keep things dry
* if you are repeating yourself use a function
* functions support paramaters
* functions need to be defined before they can be used (shell scripts are not pre-compiled)
***
***
# There are 2 ways to create a function in a shell script
* **method 1 (syntax)**:
```
function function-name () {
    # code goes here
}
```
* **method 2 (syntax)**:
```
function-name () {
    # code goes here
}
```
* this is how you can **call the function**:
```
#!/bin/bash
function hello() {
    echo "Hello!"
}

#TO CALL IT JUST USE THE NAME
hello
```
***
***
# Functions can call other functions
```
#!/bin/bash
function hello() {
    echo "Hello!"
    now
}
function now() {
    echo "It's $(date +%r)"
}

hello
```
* This works because hello is called after hello and now are defined. if you call hellow before now it wont work.
***
***
# Positional paramaters
* Functions can accept paramaters
* The first paramater is stored in ```$1```, the second in ```$2```, etc...
* ```$0``` is still the sctipt name, not the function name
* ```$@``` contains all the paramaters 
* example:
```
#!/bin/bash
function hello() {
    echo "Hello $1"
}

hello Jason

#OUTPUT
# This outputs "hello Jason" - jason was the paramater
```
* example of using all the paramaters (like **kwargs in python):
```
#!/bin/bash

function hello() {
    for NAME in $@
    do
        echo "Hello $NAME"
    done
}

hello Jason Dan Ryan
#OUTPUT
# This outputs "hello Jason", "hello Dan", "hello Ryan" - it reads all the paramaters
```
***
***
# Reading variables in functions
* by default variables are global
* variables have to be defined before use. you can use a variable at the top then define it at the bottom 
```
#!/bin/bash
my_function() {
    echo "$GLOBAL_VAR"
}
GLOBAL_VAR=1
# The value of GLOBAL_VAR is available to my_function
my_function
```
***
***
# Local variables
* local variables can only be accessed within the function 
* create local variables using the ```local``` keyword
```
local LOCAL_VAR=1
```
* only functions can have local variables
* its best practice to keep variables local in functions