***
# Shell Scripting Part 2
***
***
# Conditional statements
* you can make if, elif, else statements
* example 1:
```
if [condition-is-true]
then
    command N
elif  [condition-is-true]
then 
    command N
else
  command N
fi
```
* another example:
```
if [condition-is-true]
then
    command 1
fi
```
***
***
# For loops 
* you can make for loops if you want to perform an action on a list of items
```
for VARIABLE_NAME in ITEM_1 ITEM_N
do 
   command 1
   command 2
   command 3
done
```
* example: 
```
#! /bin/bash
COLORS="red green blue"

for COLOR in $COLORS
do
   echo "COLOR: $COLOR"
done

### OUTPUT
# COLOR: red
# COLOR: green
# COLOR: blue
```
* example 2 - renames all jpg files to include todays date before the filename:
```
#!/bin/bash

PICTURES=$(ls *jpg)
DATE=$(date +%F)
for PICTURE in $PICTURES
do
  echo "Renaming ${PICTURE} to ${DATE}-${PICTURE}"
  mv ${PICTURE} ${DATE}-${PICTURE}
done
```
***
***
# Positional paramaters
* these contain the contents of the command line
```
script.sh paramater1 paramater2 paramater3

$0: "script.sh"
$1: "paramater1"
$2: "paramater2"
$3: "paramater3"
$@: access all positional paramaters
```
* example 1 - archive a user:
```
./archive_user.sh user1
```
```
#!/bin/bash

USER=$1 # The first parameter is the user.

echo "Executing script: $0"
echo "Archiving user: $USER"

# Lock the account
passwd -l $USER

# Create an archive of the home directory.
tar cf /archives/${USER}.tar.gz /home/${USER}
```
* example 2 - use all paramaters:
```
./archive_user.sh user1 user2 user3
```
```
#!/bin/bash

echo "Executing script: $0"

for USER in $@
do
  echo "Archiving user: $USER"

  # Lock the account
  passwd -l $USER

  # Create an archive of the home directory.
  tar cf /archives/${USER}.tar.gz /home/${USER}
done
```
***
*** 
# Accept standart input
* syntax:
```
read -p "Prompt" VARIABLE
```
* standard input can be someone typing at a keyboard but it can also be the output of a command
* example - same archive script but with user input
```
#!/bin/bash

read -p "Enter a user name: " USER
echo "Archiving user: $USER"

# Lock the account
passwd -l $USER

# Create an archive of the home directory.
tar cf /archives/${USER}.tar.gz /home/${USER}
```
***
***
# Overview of basic shell scripting concepts
