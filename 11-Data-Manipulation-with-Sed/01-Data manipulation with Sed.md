***
# Data Manipulation and Text Transformation with Sed
***
***
* Sed = Stream Editior
* A stream is data that travels from:
1.  One process to another through a pipe
2. One file to another as a redirect
3. One device to another
* standard input = standard input stream
* standard ouptut = standard output stream 
* standard error = standard error stream 
* these streams are typically textual data
* sed search patterns are regular expressions - so you can use regular expression search calls

* sed is used to perform text transformations on streams
* examples:
1. subsitute some text for other text
2. remove lines
3. append text after given lines
4. insert text before certian lines
* sed is used programatically not interactivley 


* sed is a standalone built in
```
type -a sed
```
* get info:
```
man sed
```

# Using SED
* make a file to work with
```
echo "Dwight is the assistant regional manager" > manager.txt
cat manager.txt 
```
### find and replace
* use the subsitute command which is represented with the letter ```s```
* sed is case sensitive - if nothing matches it returns no alterations
```
sed 's/assistant/assistant to the/' manager.txt
# sed 's/search term/replacement text/' inputfile.txt
```
* you can add the ```i``` tag to check for upper and lower case
```
# file.txt: I like books.
sed 's/BOOKS/money/i' file.txt
```
##### NOTE:
* use one > to add text to the file
```
echo "txt" > test.txt
```
* use two >> to append text to a file
```
echo "add line 2" >> test.txt
```
### continue
* sed reads all lines when using subsitute 
* sed only replaced the first occurance on the line by default
* to make sed find and replace all results on a line use the ```g``` (global) flag
```
sed 's/origintext/newtext/g' file.txt
```
* if you want to replace a certian occurance, like the second or fourth use that as a flag like this:
```
sed 's/origintext/newtext/2' file.txt
```
* to leave the original file unaltered and make a new file do this:
```
sed 's/origintext/newtext/2' file.txt > newfile.txt
```
* This command will make a bakcup file with the original text, it will then do an inplace update on the original file (dont use a space after ```-i```)
```
sed -i.bak 's/origintext/newtext/' file.txt
```
* to make a new file with only the lines that were replaced use ```w```
```
sed 's/origintext/newtext/wg file.txt' linesonly.txt
```
### sed can work in a pipeline
* example:
```
cat like.txt | sed 's/originaltext/newtxt/g'
```
### find and replace paths or forward slashes / 
* 1 method is to escape the forward slashes 
```
echo '/home/myusr/' | sed 's/\/home/\/myusr/\/home/\/user2/' file.txt
```
* you can set a custom delimiter so you dont have to use escape characters..example using ```#```:
```
echo '/home/jason' | sed 's#/home/myusr#/home/user2#'
```


## when should you use sed for find and replace
* sed is good to use if you are changing template files, you can have placeholders and then replace those values

### remove lines using sed 
* remove lines containing your term
```
sed '/This word/d' file.txt
```
* sed uses regular expressions you could do something like this to remove comments. notice the ```^```... that is a regular expression looking for ```#``` as the first character
```
sed '/^#/d' config.txt
```
*  to run multible sed commands at the same time seperate them with ```;```
```
sed '/^#/d' ; /^$/d ; s/apache/httpd/' config.txt
```
* another method of running multible sed commands (using -e):
```
sed -e '/^#/d' -e '/^$/d' -e 's/apache/httpd/' config.txt
```
* you can also use a file that contains search patterns
```
# searchfile.sed
/^#/d
/^$/d
s/apache/httpd/
```
```
sed -f searchfile.sed myscript.txt
```

### sed addresses
* addresses define what lines sed should run on - if no address is defined sed runs on all lines
* example or only running on line 2:
```
sed '2 s/apache/httpd/' config.txt
# this does the same:
sed '2s/apache/httpd/' config.txt
```
* example of only running on lines that contain the word Group
```
sed '/Group/ s/apache/httpd/' config.txt
```
* example of making a range using a ,
```
sed '1,3 s/apache/httpd/' config.txt
```