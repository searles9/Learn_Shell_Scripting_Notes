***
# Debugging Essentials
***
***
* there are built in bash options for debugging
* bug = error
* debug to help find the root of unexpected behavior 

# Debugging options
* you can include options after the shebang to specify how you want to debug
* ex:
```
#!/bin/bash -x
```
* ```-x``` = prints commands as they exiecute (It shows the commands run, not the variables, but the actual values. Same with expansions. It wouldnt show wildcards, it would show what the wildcard actually finds)
* ```+x``` = stops debugging
* you can also set debugging at the command line like this:
```
set -x # start
set +x # storp
```
### methods
* use the set commands to only debug a portion of the script
* add the ```-x``` next to the shebang to debug the whole script

### -e (exit on error)
* ```-e``` can be used to exit immediatly on errors
* options that do not take arguments can be combined
```
#!/bin/bash -ex
#!/bin/bash -xe
#!/bin/bash -e -x
#!/bin/bash -x -e
```

### -v (print shell input lines)
* ```-v``` = prints shell input lines as they are read
* it can be combined with other options
* it **prints the data before any variables or expansions are applied** (unline -x)
```
#!/bin/bash -v
TEST_VAR="test

# OUTPUT: TEST_VAR="test
```
* if you use ```-vx``` together you can see the command before subsitutuion and expansion and the command after its executed

### get more info
* you can get more info on the set command and other options that are availible
```
help set | less
```