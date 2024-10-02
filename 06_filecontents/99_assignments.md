# Assignment on file contents

## Task 1
Find out why you should use ‘less’ instead of ‘more’

## Task 2
Show the first line of the file /proc/meminfo to find out how much memory you’ve given to your Ubuntu Virtual machine.

## Task 3
Show the last line of the file passwd located in the folder etc of the root folder

## Task 4
Show the first 4 characters (=bytes) of the file /etc/passwd. Search the manpage of head to find out how to do it. You should see the name of a certain user. Who is this user? 

## Task 5
Use cat to put the following text in a new file "mytextfile" in your home folder:  
This is my text  
spaced over multiple lines  
inserted by cat.

## Task 6
Use the `echo` command three times to put the following text in a new file "myechotextfile" in your home folder:  
This is my text  
spaced over multiple lines  
inserted by echo.

 
More difficult: It is also possible to do this with just one `echo` command. But you will need to search for the right option to escape characters in the manpage of `echo`  

## Task 7
Use cat to copy the file .bashrc in your home folder to a new file named .bashrc.backup

## Task 8
When you add a new user, a new line is added to the file /etc/passwd. Show the contents of the file but in order from newest user to oldest user (other way around than normal) 

## Task 9
Use the tail command to keep the file /var/log/auth.log open, so that you see all new log entries appear when they happen. (You can press enter a few times to seperate the new coming lines) In a new Powershell window start a new ssh session and log in. Then log out again. Wat did you see in the logs?

## Task 10
Open the configuration file of ssh, `/etc/ssh/sshd_config`, with the _less_ command and try the search function to search for X11. This is something we'll use later on to enable screens to open over SSH.

## Task 11
Use nano to edit the text in the file "myechotextfile" you created earlier in your home folder:  
This is my text, edited,  
still spaced over multiple lines  
inserted by echo and edited by nano.  

## Task 12
Use cat with the end marker "LinuxIsFun" to overwrite the text in the file "myechotextfile" you created earlier in your home folder:  
This text is way more interesting.  
I still use multiple lines d'oh,  
just because I can.  

## Task 13
Print the full contents of the previously made files "mytextfile" and "myechotextfile" with only one command.

## Task 14
Get the last 10 created users and put them in the file "newestUsers" with only one command.

## Task 15
a. Open a new file, named _Linus Torvalds_ with `nano`. Copy the folowing text into the nano editor.  

```
linus Benedict torvalds, * , is a Finnish-American software engineer who is the creator and, historically, the main developer of the Linux kernel, used by Linux distributions and other operating systems such as Android. 
He also created the distributed version control system Git.

linus torvalds was born in Helsinki, Finland. His parents were campus radicals at the University of Helsinki in the 1960s. 
linus torvalds was born in Helsinki, Finland. His parents were campus radicals at the University of Helsinki in the 1960s. 

Torvalds attended the University of Helsinki from 1988 to 1996, graduating with a master's degree in computer science.
His academic career was interrupted after his first year of study when he joined the Finnish Navy Nyland Brigade in the summer of 1989, selecting the 11-month officer training program to fulfill the mandatory military service of Finland. 

He gained the rank of second lieutenant, with the role of an artillery observer. 

He bought computer science professor Andrew Tanenbaum's book Operating Systems: Design and Implementation, in which Tanenbaum describes MINIX, an educational stripped-down version of Unix. In 1990, Torvalds resumed his university studies, and was exposed to Unix for the first time.His MSc thesis was titled Linux: A Portable Operating System.

His interest in computers began with a Commodore VIC-20 at the age of 11 in 1981. He started programming for it in BASIC, then later by directly accessing the 6502 CPU in machine code (he did not utilize assembly language).
He wrote a Pac-Man clone, Cool Man. 

On 5 January 1991 he purchased an Intel 80386-based clone of IBM PC before receiving his MINIX copy, which in turn enabled him to begin work on Linux.

The first Linux prototypes were publicly released in late 1991. Version 1.0 was released on 14 March 1994.

Torvalds first encountered the GNU Project in 1991 when another Swedish-speaking computer science student, Lars Wirzenius, took him to the University of Technology to listen to free software guru Richard Stallman's speech. Torvalds used _____ GNU General Public License version 2 (GPLv2) for his Linux kernel.

The history of Linux 
Linus was born 28 December 1969 in Finland
```
  
b. Save the changes and exit nano  
c. Open the file again with nano  
d. Search for the text "1981" to know what happened that year  
e. The second paragraph holds two of the same lines. Use a shortcut to delete one of the two lines  
f. Search for 'linus' and replace with 'Linus'  
g. Select only the text 'born 28 December 1969' of the last line. Cut it and paste it on the first line where the asterisk is (\*)  
h. Search for 'torvalds' and replace with 'Torvalds'  
i. Goto line 9, column 80. Replace the dot (.) with an exclamation mark (!)  
j. Goto the last line of text. Cut the whole line. Undo the cut. Redo the cut  
k. Use Cut and Paste to move the last line of text to the top of the document  
l. Search the help within nano to find out how to show the 'total number of lines, words and characters'.   
m. Use two times a shortcut (ctrl+...) to save and quit nano   

## Task 16
Use the _head_ command to print everything in the _/etc/passwd_ file, without knowing the amount of lines in the file. You will have to search the manpage for a solution. Now try this with the _tail_ command.

## Task 17
We can use cat to print the contents of multiple files underneath eachother, but it is hard to figure out which part comes from which file. 
For example check:
```bash
student@linux-ess:~$ cat mytextfile myechotextfile
This is my text
spaced over multiple lines
inserted by cat.
This text is way more interesting.
I still use multiple lines d'oh,
just because I can.
```
We have seen 2 commands in this chapter where we can specify to print the filename aswell, check the man pages of the seen commands and find out which 2 commands can be used. Try them out and print the full contents of the files with the filenames.

## Optional Task
use the command `vimtutor` to learn how to use vim. What is so different with this editor? 
