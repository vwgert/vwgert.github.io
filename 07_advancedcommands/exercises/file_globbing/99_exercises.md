# Assignment on File globbing

## Task 1
Create a new folder named FileGlobEx with the files script.sh, scrupt.sh and scrApt.sh. Use the touch command to create the files. 

## Task 2
Try following command: ls scr[a-z]pt.*
- Alter the command so that it's no longer case sensitive and test  
  
## Task 3
Create the following files with only one command: script.sd, script.dh, script2.dh, script.ds, script2.ds, script2.dd, script3.ss and script3.ds

## Task 4
Search the folder for all files ending in .sh or .sd or .dh or .ds or .ss or .dd  
Try to solve this one time with square brackets and one time without

## Task 5
Search the folder for all files starting with scr, then one random character, followed by pt. After pt there may be an unspecified amount of characters, but the file needs to end with an h or an s

## Task 6
Make sure that the command ls /b* does not show the content of the found folders but the folders themselves. Search the man page for a solution

## Task 7
Show all files and directories ending with ".conf" found in the folder "/etc"

## Task 8
Show all files and directories ending with ".d" found in the folder "/etc", do not show the contents of these directories

## Task 9
Show all files and directories from the folder "/etc" that have "sh" somewhere in their name 

## Task 10
Show all files and directories from the folder "/etc"  which have exactly 10 characters in their name, do not show the contents of the found folders. 

## Task 11
Search in the "/etc" folder for a file that has "os" in its name followed by "release" somewhere. (If you've found the file you can take a look at it to find out what content it holds) 

## Task 12
Execute the following command and explain its result: 
```bash
ls -d /usr/share/bash-completion/completions/resolv*conf
```

## Task 13
Search for all files that start with two numbers from the folder "/etc/grub.d"

## Task 14
List all files that do not start with a number from the folder "/etc/grub.d"

## Task 15
Extra: Try all examples of file-globbing of the textbook again. Practice makes perfect ;-)
