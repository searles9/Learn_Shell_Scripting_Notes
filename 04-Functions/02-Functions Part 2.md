***
# Functions Part 2
***
***
# Exit statuses (return codes) in functions
* functions have an exit status
* The return statement will return to the script from where it was called, while the exit statement will end the entire script from wherever it is encountered
* you can explicitly set a return code:
```
return <return code>
# this is different from the exit command used outside functions
```
* return codes can also be implicitly returned. The return code of the last command executed in the function will be what the return code will be
### valid exit codes
* valid exit coes range from 0-255
* 0 = sucess
* $? = the exit status
```
my_function
echo $?
```
* example of using an exit status with a function:
```
#!/bin/bash

function backup_file () {
  # This function creates a backup of a file.

  # Make sure the file exists.
  if [ -f "$1" ] 
  then
    # Make the BACKUP_FILE variable local to this function.
    local BACKUP_FILE="/tmp/$(basename ${1}).$(date +%F).$$"
    echo "Backing up $1 to ${BACKUP_FILE}"

    # The exit status of the function will be the exit status of the cp command.
    cp $1 $BACKUP_FILE
  else
    # The file does not exist, so return an non-zero exit status.
    return 1
  fi
}

# Call the function
backup_file /etc/hosts

# Make a decision based on the exit status of the function.
if [ $? -eq "0" ]
then
  echo "Backup succeeded!"
else
  echo "Backup failed!"
  # Abort the script and return a non-zero exit status.
  exit 1
fi
```