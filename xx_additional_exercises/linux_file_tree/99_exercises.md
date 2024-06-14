# Assignment Linux file tree

## Task 1
Add the following text in the given files, on desktop and server:

```bash
/etc/profile		→  echo "/etc/profile executed" >> /tmp/mylog
/etc/bash.bashrc	→  echo "/etc/bash_bashrc executed" >> /tmp/mylog
~/.profile		→  echo "~/.profile executed" >> /tmp/mylog
~/.bashrc		→  echo "~/.bashrc executed" >> /tmp/mylog
```

→ Look at which texts appeard in the file /tmp/mylog on start-up, login, start of the Gnome terminal and start of a subshell (= type bash)


## Task 2
Find out what the command su does. 
Run the command su <other_user> and su - <other_user> and observe the difference
Run the command "su student" and "su – student" and observe the difference with the previous task


## Task 4
Add a few lines to the (new) file ~/.bash_aliases of your home directory, so that in the future, if needed, confirmation is asked to execute the commands rm, mv and cp. 


## Task 5
Close the terminal-window and start a new one (or type bash). Test if all aliases are known. 


## Task 6
Make sure that this is added automatically in the home folder of all newly created users. 
To do this, add .bash_aliases to the folder /etc/skel. This is the folder that is copied to new homefolder on creation. 


## Task 7
Add a new user via the GUI


## Task 8
Log in with the new user and test if the aliases are known 


## Task 9
Log out and log in again with the original user (created at installation) 


## Task 10
Remove the use you just created



## Task 11
Try to see all files from /etc that end in .conf with the ls-command. Try this while you’re in the /etc folder and when you’re in your home folder


## Task 12
Look at the general logfile with the command less. Go directly to the last line and go up again to see a few lines


## Task 13
How many hard disks are In your vm and how many partitions do each of them have? This is visible in the directory /dev. The special files of disks start with sd. The number in the filename indicates the partition. 


## Task 14
If the CDROM is mounted, you should’ve a subdirectory in /media. Check this


## Task 15
Create a file in the folder /tmp. Restart Ubuntu and check if the file is still present
