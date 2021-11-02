***
# While Loops Part 1
***
***
* a loop that continues while a condition is true
* **syntax**:
```
while [ CONDITION_IS_TRUE ]
do 
  command 1
  command 2
done
```
* if the command doesnt return an exit code of 0 it stops the loop
* the while loop will never exit if the condition is always true
* infinite loops example:
```
while true
do
  command N
  sleep 1
done
```
* example of controlling how many times a while loop loops (using an incramented index)
```
#!/bin/bash

INDEX=1
while [ $INDEX -lt 6 ]
do
  echo "Creating project-${INDEX}"
  mkdir /usr/local/project-${INDEX}
  ((INDEX++))
done
```
* example of allowing user input to control a while loop:
```
#!/bin/bash

while [ "$CORRECT" != "y" ]
do
  read -p "Enter your name: " NAME
  read -p "Is ${NAME} correct? " CORRECT
done
```
* example of checking the return code of a command
* while the ping is sucessful run the commands
```
#!/bin/bash

while ping -c 1 app1 >/dev/null
do
  echo "app1 still up..."
  sleep 5
done

echo "app1 down, continuing."
```