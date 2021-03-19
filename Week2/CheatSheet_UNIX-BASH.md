### Shell Novice command list

===

Command |             Usage              |Description
:--------|:--------------------|:-----------------------------
PS1 |`PS1='$'`| set the command prompt to `$`
whoami|`whoami`| display logged in user
pwd |`pwd`| print working directory
ls|`ls`|list directory contents
ls|`ls -F`|list files and show directories with a `/` appended to the end
ls|`ls -F Desktop`|list files on the Desktop. This will work if you are in home directory. Otherwise, full path is needed.
ls|`ls --help`|help on the listing command (`--help` can be used with any command)
man|`man ls`|manual command, can pull the manuals for the given command. Use arrow keys to navigate. `b` and `spacebar` to go page by page. Use `q` to "quit" the manual and go back to the prompt.
man|`man ls`|some useful flags for `ls` command  `-a` (list all) `-t` (sort by time) `-l` (list in long format) `-h` (list in human readable form). These flags can be combined e.g. `-alht`. -Flah'
`.`|`.`| current directory
`..`|`..`| parent directory
`/`|`/`|root directory on the computer
`~`|`~`|home directory
`-`|`-`|previous directory
cd|`cd ~/Desktop`|"change directories" to users Desktop under home directory
cd|`cd ..`| move to the parent directory
cd|`cd /`|move to root directory for the system
mkdir|`mkdir thesis`|create a directory named thesis in the current working directory (TIP: do not have spaces in file names)
nano|`nano draft.txt`|create a file "draft.txt" and open it for editing in `nano` editor. `CTRL+O` for writing data. `CTRL+X` to exit file and go back to shell.
rm|`rm draft.txt`|delete file "draft.txt" in current directory (User `-r -i` flags for removing directoties)
mv|`mv thesis/draft.txt thesis/quotes.txt`|rename file "draft.txt" to "quotes.txt"
cp|`cp thesis/draft.txt thesis/quotes.txt`|copy file "draft.txt" to "quotes.txt" in thesis folder
file name extentions| `.txt .sh .png .pdf .mp3 .xlx .csv .tsv .doc`| file name suffix after the `.` represents the file type
wc|`wc test.txt`|word count `-c` for bytes `-l` for lines `-m` for characters `-w` for words
`*`| `*`|wildcard - matches zero or more characters
`?`|`?`|wildcard - matches single character
`>`|`wc -l *.txt > lengths.txt`|(redirect output to file) count the lines in all files that end with `txt` and save the results to a file named "lengths.txt"
cat| `cat lengths.txt` | prints the contents of files one after another (for one file - just the contents of one file)
sort| `sort -n lengths.txt` | sort the contents of the file "lengths.txt" using numerical sort
head| `head -n 1 lengths.txt`| print the first line of the file "lengths.txt"
`|`|`|`|pipe command - redirect the output of one command as input of next
`|`|`wc -l *.pdb | sort -n | head -n 1`|count all the lines in files ending with `.pdb` and sort numerically and then give the first line of the output
`<`|`wc < document.txt`| read input to read from file named "document.txt"
tail|`tail -n 5 lengths.txt`| get the last five lines from file "lengths.txt"
`>>`|`wc -l *.txt >> lengths.txt`|(redirect output to file) count the lines in all files that end with `txt` and **append** the results to a file named "lengths.txt"
uniq|`uniq salmon.txt`|remove duplicates from file "salmon.txt" (only removes **adjacent** duplicates)
cut|`cut -d , -f 2 animals.txt`| cut the contents of file "animals.txt" using `,` as delimeter and select the second field
loops|`for variable in listvariable` <br> `do` <br>   `dosomething` <br> `done`| for loop, dosomething on variable until all the variables in the listvariable have been used
echo|`echo $value`|prints the variable $value to console
CTRL+A|`CTRL+A`|move to beginning of line
CTRL+E|`CTRL+E`|move to end of line
history|`history | tail -n `|list the history of commands and filter the last five commands
`!`|`!233`|run the 233rd command from history
`!!`|`!!`|run the last command from history
`!$`|`!$`|last word from previous command (useful for retrieving previous parameters)
`$n`|`$1`|first command line parameter passed to the script, (nth parameter using `$n`)
`@`|`@`|list of all of the command line parameters passed to the script
grep|`grep not file.txt`|find lines with the word "not" in `file.txt`. `-w` will give word boundary match. `-n` will give the line number for match. `-v` invert match (match lines witout the word)
regular expression|`grep -E ^.o`| `^` matches start of line (`.` matches single character - `*` matches zero or more characters) `o` matches letter "o"
find|`find .`| lists names of all files and directories under current directory `.`
find|`find . -type d`| lists names of all **directories** under current directory `.`
find|`find . -type f`| lists names of all **files** under current directory `.`
find|`find . -name '*.txt'`| lists names of all files and directories that end in `.txt` under current directory `.`
`$( )`|`echo $(find . -name '*.txt')`|inserts command output from find command into echo command


====

### TIPS:
* Help on all these commands is available using `man` (and/or `info` command on MacOS)
* **StackOverflow** http://stackoverflow.com/ is a great resource if you are stuck.
* Searching **Google** for `man <commandname>` lists the man pages for the command in your browser.

====

### Usefule Regular Expression Matches

Regular Expression | Matches
--------------------|---------------
`^`|start of line
`$`|match end of line
`\`|escape the next character e.g. `\^` means match the character "^" and not match start of line
`[ ]`|match **any** characters in brackets e.g. [abc] matches `a` or `b` or `c`
`-`|match a range `[0-9]` to match numbers 0 to 9
`[^ ]`|match all except listed in brackets e.g. `[^0-9]` to match everything except numbers 0 to 9
`.`|single character of any value
`*`|zero or more characters of any value
`A`|upper case A
`a`|lowercase a
`\d`|any single digit
`\D`|any single non-digit character
`\w`|any alphanumeric character


The original list can be found here: https://thejacksonlaboratory.github.io/introduction-to-hpc/cheatsheet/
Copyright © 2016 Software Carpentry Foundation
