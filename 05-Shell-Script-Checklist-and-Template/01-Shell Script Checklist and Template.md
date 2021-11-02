***
# Shell Script Checklist and Template
***
***
* scripts are usually setup in the same manner - below is a checklist and boiler plate for shell scripts
***
***
# Checklist 
1) Verify the Shebang is at the top
2) Add comments defining the purpose of the script
3) Define your global variables
4) Define your functions and use local variables in the functions
5) Define the main logic of the script
6) Exit the script with an exit status (the exit status can also be defined in other areas of the script)

# Boilerplate template
```
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

# Exit with an explicit exit status.
exit 0
```