# Assignment on Filters

## Task 1
Show the last five users created on the system, from newest to oldest. Show only the usernames

## Task 2
What is the option to use grep case insensitive?

## Task 3
Show the lines and line numbers from the file linux.txt that contain the word unix or Unix. Search the manpage of grep to find a solution.
Try to find two solutions. One with the use of square brackets and one without.

Example of linux.txt:

```
I'm working with Linux
It know something about Minix
The foundation is Unix
unix
Minix
Unix
Test
Test
Test
```

## Task 4
Show the lines from linux.txt that contain the word Linux, Minix or Unix. Use the option _-e_ multiple times to search for each string.

## Task 5
Count the number of lines that contain the word Unix in the file linux.txt. The result is a number that reflects the number of lines. Search the manpage to find a solution  

## Task 6
Show all lines from the file linux.txt that start with a capital. 

?> <i class="fa-solid fa-circle-info"></i> Capital letters can be matched using [A-Z]  
  
?> <i class="fa-solid fa-circle-info"></i> The start of a line can be matched using ^


## Task 7
Print the password file, ordered by userid. Search for this option in the manpage. Search section 5 of the manpage of passwd to find out which field holds the userid. Search the manpage of sort to find out how to sort numeric fields. In the result the user `nobody` must be the last one  


## Task 8
Start with the ls command of the root-folder (/) and try to end with a list of files and folders separated by spaces. Use the tr command to translate all new line characters to spaces.


## Task 9
Go to your homefolder. Paste all shown files and folders (not the hidden ones) from the directory one after the other and count the number of words. The result is only a number 

## Task 10
Show all installed packages with apt, but only show the name and version in alphabetical order.

?> <i class="fa-solid fa-circle-info"></i> Hint: You need to use tr to make it easier.   
  
?> <i class="fa-solid fa-circle-info"></i> Hint: You only need to use tr and cut once. 

## Task 11
How many installed packages are there on your system?
