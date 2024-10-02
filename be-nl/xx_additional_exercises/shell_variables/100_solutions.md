# Assignment Shell variables

## Task 1
Change the shell prompt to look like the following. Use man bash and search PROMPT for the options.

```
<empty line>
Fri Jan 18 10:24:45 – PTS4
student@ubuntu:~$ ls
dir1 dir2 file1
<empty line>
Fri Jan 18 10:24:59 – PTS4
student@ubuntu:~$
```
<br/>![](images/2022-08-15-14-54-02.png)

## Task 2
Make sure to always use this prompt
<br/>![](images/2022-08-15-14-54-15.png)
<br/>![](images/2022-08-15-14-54-21.png)


## Task 3
Use a command to show all set variables 
<br/>![](images/2022-08-15-14-54-35.png)
<br/>![](images/2022-08-15-14-54-40.png)
<br/>![](images/2022-08-15-14-54-48.png)

## Task 4
Try to show following text with the echo command on your screen. (Hint: Use multiple environment variables to show the text in bold underneath)
Hello, I am `student` and my home folder is `/home/student` on the pc with name `linux-ess-desktop`. You are now working in folder `/tmp`.

<br/>![](images/2022-08-15-14-55-40.png)

## Task 5
Create a variable named "myvar" with its content the text "super". Show the following text on screen using this variable.
```
Hello superwoman, I am superman !
```
<br/>![](images/2022-08-15-14-56-07.png)

## Task 6
Delete the previous variable and reprint the text.

<br/>![](images/2022-08-15-14-56-21.png)


## Task 7
Search for the command timedatectl in the man pages. How can we list alle time zones to set one of them. Set the time zone to Brussel. 

<br/>![](images/2022-08-15-14-56-59.png)
<br/>![](images/2022-08-15-14-57-05.png)


## Task 8
Search on the internet how to use "locale -a" and editing the file "/etc/default/locale" to change the date to English instead of German 

<br/>![](images/2022-08-15-14-57-18.png)
<br/>![](images/2022-08-15-14-57-23.png)
<br/>![](images/2022-08-15-14-57-28.png)

?> <i class="fa-solid fa-circle-info"></i>You will need to log out and log in to let the changes take effect.

## Task 9
Create a command that shows the following text with the current date on screen. (Hint: Use embedded shells.)

```
Today, it is <weekday>, <day> <month> <year>. The time is <hour>:<minute>
Example → Today, it is Wednesday, 10 August 2022. The time is 15:47.
```

<br/>![](images/2022-08-15-14-58-30.png)

## Task 10
Try and set the time to Dutch. Search the internet for "locale-gen"

<br/>![](images/2022-08-15-14-58-43.png)

?> <i class="fa-solid fa-circle-info"></i> You will need to log out and log in to let the changes take effect.

<br/>![](images/2022-08-15-14-59-00.png)


## Task 11
Try to print the following text on screen, make sure this is correct for each user. (Hint: Try this with and without quotes.)

```
=> The contents of my home folder:
Desktop
Documents
Downloads
examples.desktop
Music
Pictures
Public
Templates
Videos
```

<br/>![](images/2022-08-15-14-59-20.png)

?> <i class="fa-solid fa-circle-info"></i>  without the " " you’ll need to remove the arrow => to get an output. But the output will print everything on 1 
line. 

<br/>![](images/2022-08-15-14-59-42.png)