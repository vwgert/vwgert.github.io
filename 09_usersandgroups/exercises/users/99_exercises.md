# Assignment on Users

## Task 1
The definition of users is kept in the file /etc/passwd. This file has 1 line for each user. Each of these lines is divided into 7 fields, separated by a ":". Give a description of each of these fields:

Field 1: ________<br />
Field 2: ________<br />
Field 3: ________<br />
Field 4: ________<br />
Field 5: ________<br />
Field 6: ________<br />
Field 7: ________<br />


## Task 2
Back in the early days of Unix, the file /etc/passwd didn’t only keep user-information, it also contained a coded version of the password. This was a weak point in the security of the Unix system of course, because everyone can read the /etc/passwd file and thus could see the coded passwords. For a hacker the next step would be to create a tool to decode these passwords, for example: cracker. After this problem was recognized, it was decided that the passwords were to be kept in a different file. This file would only be accessible by the user root, who’s ID is used to run the passwd and login programs. 
What is the name of the file with the coded passwords? 



## Task 3
Create a user with following characteristics:  
User-name:	    john<br />
User-ID:	    1111<br />
Group-ID:	    100 (=users)<br />
Description:	John Doe<br />
Home-dir:	    /home/john<br />
Shell:		    /bin/bash<br />
  
   
## Task 4
Check the changed files:
What is changed in the file /etc/passwd?

## Task 5
What is changed in the file /etc/shadow?
  
?> <i class="fa-solid fa-circle-info"></i> After a user is created, its password is set to "!", which means that this name cannot be used to log in. To make this possible you need to give John a password. Set John’s password to "January".
  
## Task 6
What is changed in the file /etc/group?

## Task 7
What is changed in the directory /home? 

## Task 8
The user John is now created on your system. Now John should be able to ask information about himself.<br /> 
Log in as John and execute the following command: 
```bash
id
```

## Task 9
Remove the user John from your system using the command:  userdel –r john<br />
What is changed in the file /etc/passwd?

## Task 10
What is changed in the file /etc/shadow?


## Task 11
What is changed in the file /etc/group?

## Task 12
Does the directory /home/john still exist? 


## Task 13
Create a user Sarah, by only specifying the username and that she must have a home folder. 

## Task 14
Examine the files that have been modified<br />
What is changed in the file /etc/passwd?

## Task 15
What is changed in the file /etc/shadow?

## Task 16
What is changed in the file /etc/group?


## Task 17
What is changed in the directory /home?

## Task 18
Give the user Sarah a password

## Task 19
Try to log in as Sarah

## Task 20
Remove the user Sarah, but keep her home folder

## Task 21
Delete Sarah’s home folder
