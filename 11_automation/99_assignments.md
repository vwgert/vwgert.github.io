# Assignment on automation

## Task 1
Make a directory called _bin_ in your homefolder.
    
  
## Task 2
Log out and log back in. Make sure your _bin_ folder is added to the variable PATH. Do you know why the folder is added to the variable PATH? (Hint: .profile)

```bash
student@linux-ess:~$ echo $PATH
/home/student/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/games:/usr/local/games:/snap/bin
```
  
  
## Task 3
Make a script, called _show.sh_, that asks for a path to a directory. Try to involve the username in the question (see the example). Use the `env` command to search for the right System variable to use.   
Show a listing of all the files within the given directory.  
Make the script executable and check if it works.  
  
Example:
```bash
student@linux-ess:~/bin$ show.sh
Dear student, please specify the dir:
/etc/ssl
certs  openssl.cnf  private
```
  
  
## Task 4
Alter the previous script. Search in the manpage of echo how you can keep the cursor behind the question: Please specify the dir: _
  
Example:
```bash
student@linux-ess:~/bin$ show.sh
Dear student, please specify the dir: /etc/ssl
certs  openssl.cnf  private
```
  
  
## Task 5
Alter the previous script. Catch three parameters in the script and add these to the `ls` command within the script.
Test the script with the parameters `-l`, `-a` and `-h`

Example:
```bash
student@linux-ess:~/bin$ show.sh -l -a -h
Dear student, please specify the dir: /etc/ssl
total 44K
drwxr-xr-x  4 root root 4.0K Nov  4 14:19 .
drwxr-xr-x 97 root root 4.0K Nov 12 13:41 ..
drwxr-xr-x  2 root root  16K Aug  9 11:58 certs
-rw-r--r--  1 root root  13K Jul  4 11:20 openssl.cnf
drwx------  2 root root 4.0K Jul  4 11:20 private
```

Also try to start the script with only 1 parameter (-l) or a contraction (-lah)
  
  
## Task 6

Try to run the script while being in another folder than the bin folder. Does it work by specifying only the name (no path)?  
Make a new directory in your homefolder, named _myscripts_.
Move the script _show.sh_ to the folder _myscripts_.
Try to run the script while being in another folder than the myscripts folder. Does it work by specifying only the name (no path)?
Fix this by adding the path to the right variable. Also make sure this path is known in the future. To test this you need to logout and login again.
Also use the `which` command to check if it works.
  
  
## Task 7
Alter the previous script. Firstly print the current date in the format as in the example. Search the manpage of `date` to find the right format.
  
Example:   
```bash
student@linux-ess:~/myscripts$ show.sh
Saturday, 12 November 2022
Dear student, please specify the dir: /
bin   dev  home  lib32  libx32      media  opt   root  sbin  srv       sys  usr
boot  etc  lib   lib64  lost+found  mnt    proc  run   snap  swap.img  tmp  var
```
   
   
## Task 8
Create a job to run once in about five minutes. The job has to place an overview of all logged in users into the file _/tmp/userlist_.
Besides the current ssh connection to the server, also login on the server itself.
After 5 minutes take a look at the file _/tmp/userlist_.
  
Example:
```bash  
student@linux-ess:~/myscripts$ cat /tmp/userlist
 17:10:15 up 14:42,  2 users,  load average: 0.20, 0.16, 0.10
USER     TTY      FROM             LOGIN@   IDLE   JCPU   PCPU WHAT
student  tty1     -                17:08    2:13   0.11s  0.05s -bash
student  pts/0    192.168.75.1     15:04    7.00s  0.25s  0.02s w
``` 
    
   
## Task 9
Create a personal cronjob which saves the text _Rebooted at_ and then the _date_ and _time_ to the file _~/rebootlog_.
Search the manpage of the crontab file, more precisely the _File Format_ section. Search for the text _reboot_. 
> Hint: when trying to format your date command: the `%`-sign has a special meaning in crontab.
  
## Task 10 
Create a Cronjob that makes a backup of all the homefolders (regular users and root) every sunday at 23:59 to the dir _/backups_. Put the backup in a tarball named homefolders.tar.gz.
Create the script and place it in _/scripts_.  
Create the cronjob.

PS: To test the cronjob change the time and day-of-the-week to within exactly 1 minute. Wait a minute and check if the tarball exists.