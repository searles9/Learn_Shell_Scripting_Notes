***
# Wildcards in Shell Scripts
***
***
* wildcards are useful for when you want to work on a group of files or directories 
* example:
```
#!/bin/bash
cd /var/www
cp *.html /var/www-just-html
```
* in a for loop example:
```
#!/bin/bash

cd /var/www
for FILE in *.html
do
    echo "Copying $FILE"
    cp $FILE /var/www-just-html
done
```
* another example: 
```
#!/bin/bash

for FILE in /var/www/*.html
do
    echo "Copying $FILE"
    cp $FILE /var/www-just-html
done
```
* you need to change to the directory you want to work in - or you need to specify the directory in the command