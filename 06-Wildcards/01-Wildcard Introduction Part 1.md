***
# Wildcard Introduction Part 1
***
***
* a wildcard is a character or string used to pattern matching 
* globbing expands the wildcard patterns into a list of files and or directories (paths)
* Wildcards can be used with most commands (ls, rm, cp)

***
***
# 2 main wildcards
### *
* \* - matches zero or more characters
```
*.txt
a*
a*.txt
```
### ?
* ? - matches only one character
```
?.txt # anything.txt
a? # a<anything>
a?.txt  # a<anything>.txt
```
***
***
# Character classes
* [] - a character class
* matches any of the characters included between the brackets
* matches only one of the characters
```
can[nt]

# it will match
can
cat
candy
catch
```
* you can also do the inverse and exclude characters with ```[!]```
* it also matches onle one character
```
[!aeiou]* # matching all words that dont start with a voul

# it will match
baseball
cricket
```
* with character classes you can use a range - ex:
```
[a-g]*
[3-6]*
```
### Named character classes
* you can use pre defined named character classes
```
[[:alpha:]] # lower and uppercase letters
[[:alnum:]] # upper and lowercase letters - and decimal digits
[[:digit:]] # numbers 0-9
[[:lover:]] # lowercase letters
[[:space:]] # whitespace
[[:upper:]] # upper case letters
```
***
***
# Matching wildcard patterns
* if you want to match a wild card character you can use an escape character ```\```
```
*\?

# will match
done?
```