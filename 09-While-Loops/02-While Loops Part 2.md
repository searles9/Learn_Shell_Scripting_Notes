***
# While Loops Part 2
***
***
# Read a file line by line
* you track the line number with a variable and then incrament through it.

```
#!/bin/bash

LINE_NUM=1
while read LINE
do
  echo "${LINE_NUM}: ${LINE}"
  ((LINE_NUM++))
done < /etc/fstab
```
# Reading the output of a command line by line:
* you run the command then pipe it to a while loop
```
#!/bin/bash

grep xfs /etc/fstab | while read LINE
do
  echo "xfs: ${LINE}"
done

```
# Reading pieces of each line:
* its assigning the first word of data to the FS variables, second word to the MP variable, third word to the rest of the line to the REST var
```
#!/bin/bash

FS_NUM=1
grep xfs /etc/fstab | while read FS MP REST
do
  echo "${FS_NUM}: file system: ${FS}"
  echo "${FS_NUM}: mount point: ${MP}"
  ((FS_NUM++))
done
```
# Break statement
* if you want to break a loops use the ```break``` statement
* it breaks the loops but not the script
```
#!/bin/bash

while true
do
  read -p "1: Show disk usage.  2: Show uptime. " CHOICE
  case "$CHOICE" in
    1)
      df -h
      ;;
    2)
      uptime
      ;;
    *) 
      break
      ;;
  esac
done
```
# Continue 
* it skips the iteration of the loops
```
#!/bin/bash

mysql -BNe 'show databases' | while read DB
do
  db-backed-up-recently $DB
  if [ "$?" -eq "0" ]
  then
    continue
  fi
  backup $DB
done
```