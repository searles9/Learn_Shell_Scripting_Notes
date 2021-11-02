***
# Case Statements
***
***
* case statements can sometimes be easier to read than complex if statements 
* if you find yourself using an if statement to compare the same variable over and over you can probably use a case statement instead
* patterns can include wildcards or pipes
* case statement **example syntax**:
```
case "$VAR" in 
    pattern_1)
         # commands
         ;;
    pattern_N)
         # commands
         ;;
esac
```
* example case statement:
* ```./script start```
* ```./script stop```
```
#!/bin/bash

case "$1" in
    start)
        /usr/sbin/sshd
        ;;
    stop)
        kill $(cat /var/run/sshd.pid)
        ;;
esac
```
* another example case:
```
#!/bin/bash

case "$1" in
    start)
        /usr/sbin/sshd
        ;;
    stop)
        kill $(cat /var/run/sshd.pid)
        ;;
    *)
        echo "Usage: $0 start|stop" 
        exit 1
        ;;
esac
```
* another similar example - notice multible patterns:
```
#!/bin/bash

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
* another example **asking for input from a user**:
```
#!/bin/bash

read -p "Enter y or n:" ANSWER

case "$ANSWER" in
    [yY]|[yY][eE][sS])
        echo "You answered yes."
        ;;
    [nN]|[nN][oO])
        echo "You answered no."
        ;;
   *)
        echo "Invalid answer."
        ;;
esac
```
