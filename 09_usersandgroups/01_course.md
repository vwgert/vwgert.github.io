# Users and groups
As with any operating system we will be working with different users on the system. We've been using the user `student`. We can confirm this by running the command `whoami`. Other commands we can run are `who` or `w`. These will show us all of the users that are logged in on the system (mind that both commands have a different output!).

## User management
### /etc/passwd
As we've seen before all system configuration is done using config files. The same is true for user management. User configuration is stored in the file `/etc/passwd`. It contains a list of user accounts together with some metadata seperated by colons:
```bash
student@linux-ess:~$ tail /etc/passwd
pollinate:x:105:1::/var/cache/pollinate:/bin/false
sshd:x:106:65534::/run/sshd:/usr/sbin/nologin
syslog:x:107:113::/home/syslog:/usr/sbin/nologin
uuidd:x:108:114::/run/uuidd:/usr/sbin/nologin
tcpdump:x:109:115::/nonexistent:/usr/sbin/nologin
tss:x:110:116:TPM software stack,,,:/var/lib/tpm:/bin/false
landscape:x:111:117::/var/lib/landscape:/usr/sbin/nologin
usbmux:x:112:46:usbmux daemon,,,:/var/lib/usbmux:/usr/sbin/nologin
student:x:1000:1000:student:/home/student:/bin/bash
lxd:x:999:100::/var/snap/lxd/common/lxd:/bin/false
```
The first account in this file is the `root` account:
```bash
student@linux-ess:~$ head -1 /etc/passwd
root:x:0:0:root:/root:/bin/bash
```

We can see more info than just usernames. These lines contain the user identifier (`1000` for `student`), home folder location, default shell, ... 

?> <i class="fa-solid fa-circle-info"></i> You can find more information about this file, the columns and the contents by running the command `man 5 passwd`.

### Adding users (useradd)
To add users we can simply use the `useradd` command. Its important to note that we have to run this command with `sudo` rights. This is because it is a system command that affects the entire system. To add a new user with the username `teacher` we could run the following command:
```bash
student@linux-ess:~$ sudo useradd -m -d /home/teacher -c "Teacher Account" teacher
[sudo] password for student:
student@linux-ess:~$ tail -3 /etc/passwd
student:x:1000:1000:student:/home/student:/bin/bash
lxd:x:999:100::/var/snap/lxd/common/lxd:/bin/false
teacher:x:1001:1001:Teacher Account:/home/teacher:/bin/sh
```
The `-d` takes in an argument and uses this argument as a path to where the homefolder has to be created. The `m` option (`create home`) will make sure the home folder actually gets created with the correct permissions. Lastly the `-c` (`comment`) option sets extra metadata to the user. 


?> <i class="fa-solid fa-circle-info"></i> Mind that the option -d is optional and if not specified it defaults to a directory with the same name as the username within the directory /home.


?> <i class="fa-solid fa-circle-info"></i> We can delete users by running the command `userdel -r teacher`. The option `-r` will also remove that user's homefolder.

As seen in the folder `/home` or in the file `/etc/passwd` the new user has been created:
```bash
student@linux-ess:~$ tail -1 /etc/passwd
teacher:x:1001:1001:Teacher Account:/home/teacher:/bin/sh
student@linux-ess:~$ ls -l /home
total 8
drwxr-x--- 5 student student 4096 Nov  4 16:04 student
drwxr-x--- 2 teacher teacher 4096 Nov  7 20:28 teacher
```

Every user has a userid (the third field in `/etc/passwd`). To view the userid of a user you can use the `id` command:
```bash
student@linux-ess:~$ id teacher
uid=1001(teacher) gid=1001(teacher) groups=1001(teacher)
```

#### Default values
The `useradd` command uses quite some default values. We can check these default values by running the following command:
```bash
student@linux-ess:~$ useradd -D
GROUP=100
HOME=/home
INACTIVE=-1
EXPIRE=
SHELL=/bin/sh
SKEL=/etc/skel
CREATE_MAIL_SPOOL=no
```
These settings are kept in the file `/etc/default/useradd` and can be changed at any time by altering the file or using `useradd -D [option]`.

?> <i class="fa-solid fa-circle-info"></i> Notice that the default value for the shell is `/bin/sh`. It is good practice to alter this to `/bin/bash` so that every new user that will be created in the future gets the `bourne again shell` as default (eg. sudo useradd -D --shell /bin/bash).

#### /etc/skel
By default homefolders are created as a subdirectory of the `/home` directory. These folders aren't created from scratch. The contents of the folder `/etc/skel` are copied within each newly created homefolder. This means that if we alter any contents in this `skel` folder, this wil actually be copied to any new user that will be created in the future:

```bash
student@linux-ess:~$ ls -a /etc/skel
.  ..  .bash_logout  .bashrc  .profile
student@linux-ess:~$ sudo ls -a /home/teacher/
.  ..  .bash_logout  .bashrc  .profile
```

#### Default profile files
__.bashrc__: executed everytime a new shell (bash) is started

__.bash\_logout__: clears the screen when the user logs out

__.profile__: executed when user logs in

### Editing users (usermod & userdel)
To edit a user's account configuration, we can use the `usermod` command. This command has several options that we can use to edit specific settings. For example to edit the comment field of a user we can run the following command:
```bash
student@linux-ess:~$ grep student /etc/passwd
student:x:1000:1000:student:/home/student:/bin/bash
student@linux-ess:~$ sudo usermod -c "Student Account" student
student@linux-ess:~$ grep student /etc/passwd
student:x:1000:1000:Student Account:/home/student:/bin/bash
```

To edit the default shell for a specific user we could do the following:
```bash
student@linux-ess:~$ tail -3 /etc/passwd
student:x:1000:1000:Student Account:/home/student:/bin/bash
lxd:x:999:100::/var/snap/lxd/common/lxd:/bin/false
teacher:x:1001:1001:Teacher Account:/home/teacher:/bin/sh
student@linux-ess:~$ sudo usermod -s /bin/bash teacher
student@linux-ess:~$ tail -3 /etc/passwd
student:x:1000:1000:Student Account:/home/student:/bin/bash
lxd:x:999:100::/var/snap/lxd/common/lxd:/bin/false
teacher:x:1001:1001:Teacher Account:/home/teacher:/bin/bash
```

?> View the manpage of `usermod` for all possible options. 


?> If we want to create a user that cannot be logged into, we can change his shell to `/bin/false` or `/sbin/nologin`. The difference between these two is that `/sbin/nologin` gives a polite message that you cannot log in to this account before exiting. The option `/bin/false` directly exits without prompting anything. 

#### Setting user passwords
If we want to change our own password we can use the `passwd` command (without sudo!):
```bash
student@linux-ess:~$ passwd
Changing password for student.
Current password:
New password:
Retype new password:
passwd: password updated successfully
```

?> <i class="fa-solid fa-circle-info"></i> Note that your password has to be long and difficult enough, otherwise the new password will not be accepted.


?> <i class="fa-solid fa-circle-info"></i> Note that if we use `sudo passwd` that we are changing the password of the user root and not our own password!

​    

As seen in the previous commands we created a new user with the username `teacher` but we never gave it a password. To do this we can run the `passwd` command with `sudo` rights and with a username as argument. This forces setting a new password for that specific user:
```bash
student@linux-ess:~$ sudo passwd teacher
New password:
Retype new password:
passwd: password updated successfully
```

The password gets stored in the file `/etc/shadow` for security reasons. Regular users cannot view the contents of this file:
```bash
student@linux-ess:~$ tail -1 /etc/shadow
tail: cannot open '/etc/shadow' for reading: Permission denied
student@linux-ess:~$ sudo tail -1 /etc/shadow
teacher:$y$j9T$Vtf.U//c4/N/CB8LzHfnl0$5iCgijrpqXfaA3v18w/nAL2rl8BmiBYX5rn5rf.j6B7:19171:0:99999:7:::
```
As seen in the example above the password isn't shown in plaintext. This is because Linux systems use hashing algoritms to encrypt the passwords. The algoritm used here is called _sha512_.


## Substitute user (su)
You can log out a user using `logout` or `exit`. Of course you can log back in as a different user after logging out. With the command su (substitute user) you can temporarily work as another user:
```bash
student@linux-ess:~$ whoami; pwd
student
/home/student
student@linux-ess:~$ su - teacher
Password:
teacher@linux-ess:~$ whoami; pwd
teacher
/home/teacher
teacher@linux-ess:~$ exit
logout
student@linux-ess:~$ whoami; pwd
student
/home/student
```

Note that root can become whoever he wants without the need to know that user's password:
```bash
student@linux-ess:~$ whoami; pwd
student
/home/student
student@linux-ess:~$ sudo su - teacher
teacher@linux-ess:~$ whoami; pwd
teacher
/home/teacher
teacher@linux-ess:~$ exit
logout
```

Note that to become root (without knowing his password) we can also use the `sudo su` command:
```bash
student@linux-ess:~$ whoami; pwd
student
/home/student
student@linux-ess:~$ sudo su - root
root@linux-ess:~# whoami
root
root@linux-ess:~# pwd
/root
root@linux-ess:~# exit
logout
```

We want to be mindful of commands that we run as the `root` user. This user can have permissions on all the files, folders and services on our system. This means that running commands as `root` can have a huge impact when being exploited.

?> <i class="fa-solid fa-circle-info"></i> Notice that if you use the minus (-) with the su command, that the profile of the new user will also be loaded and you will be put in the homedirectory of that user. If you do not use the minus (-) the profile of the user will not be loaded. You will still become the new user with his privileges, but you will remain in the current folder because his profile won't be loaded.

```bash
student@linux-ess:~$ whoami; pwd
student
/home/student
student@linux-ess:~$ sudo su root
root@linux-ess:/home/student# whoami; pwd
root
/home/student
root@linux-ess:/home/student# exit
exit
student@linux-ess:~$ whoami; pwd
student
/home/student
student@linux-ess:~$ sudo su - root        
root@linux-ess:~# whoami; pwd
root
/root
root@linux-ess:~# exit
logout
student@linux-ess:~$
```

## Group management

### View groupinfo of a user (id, groups)
To view the groups a user is member of we can use the commands `id` and `groups`:
```bash
student@linux-ess:~$ id student
uid=1000(student) gid=1000(student) groups=1000(student),4(adm),24(cdrom),27(sudo),30(dip),46(plugdev),110(lxd)
student@linux-ess:~$ groups student
student : student adm cdrom sudo dip plugdev lxd
```

### /etc/group
The file where the group info of the users is stored is `/etc/group`. We could also make changes to this file instead of using commands.
```bash
student@linux-ess:~$ grep student /etc/group
adm:x:4:syslog,student
cdrom:x:24:student
sudo:x:27:student
dip:x:30:student
plugdev:x:46:student
lxd:x:110:student
student:x:1000:
```


### Adding groups (groupadd)
If there's a need for new groups we can do it with the `groupadd` command:
```bash
student@linux-ess:~$ sudo groupadd ict
student@linux-ess:~$ tail -3 /etc/group
student:x:1000:
teacher:x:1001:
ict:x:1002:
```

?> We can delete groups using the command `groupdel`.

### Editing groups (groupmod)
If we need to change a group we can use `groupmod`:
```bash
student@linux-ess:~$ sudo groupmod -n it ict
student@linux-ess:~$ tail -3 /etc/group
student:x:1000:
teacher:x:1001:
it:x:1002:
```

### Edit group memberships (usermod & deluser)
If we want to add a user to a supplementary group we can also use the `usermod` command:
```bash
student@linux-ess:~$ sudo usermod -a -G it teacher
student@linux-ess:~$ id teacher
uid=1001(teacher) gid=1001(teacher) groups=1001(teacher),1002(it)
student@linux-ess:~$ groups teacher
teacher : teacher it
student@linux-ess:~$ grep it /etc/group
it:x:1002:teacher
```

?> <i class="fa-solid fa-circle-exclamation"></i> If we forget the `-a` (__add__) option the user will only be in the specified supplementary group and will be removed from all the groups he was in. This can be a serious problem if the user was the only one in the sudo group!

If we want to remove a user from a supplementary group we have a few options:
* specify all the supplementary groups he must remain in and don't use the -a option in the usermod command
* edit the group file `/etc/group` by hand and remove the username in the memberlist
* use the deluser command (in debian-based distros only):
```bash
student@linux-ess:~$ id teacher
uid=1001(teacher) gid=1001(teacher) groups=1001(teacher),1002(it)
student@linux-ess:~$ groups teacher
teacher : teacher it
student@linux-ess:~$ grep it /etc/group
it:x:1002:teacher
student@linux-ess:~$ deluser teacher it
student@linux-ess:~$ id teacher
uid=1001(teacher) gid=1001(teacher) groups=1001(teacher)
student@linux-ess:~$ groups teacher
teacher : teacher
student@linux-ess:~$ grep it /etc/group
it:x:1002:
```

?> <i class="fa-solid fa-circle-info"></i> The primary group of a user is specified in `/etc/passwd` and is the default group set on a new file or directory created by that user.

?> <i class="fa-solid fa-circle-info"></i> A user knows a change in group membership only when he logs in. So after a change a user has to login again to notice the difference.


In the example below we see that user student's `primary` group is changed to 'it' and this is shown by the id and grep of the passwd-file. However the groups-command does not show the change of group, also when we create a new file, the old primary group is still used. As explaned before, we need to log out and in again to get the changes to happen. This is also shown in the example.
```bash
student@linux-ess:~$ grep student /etc/passwd
student:x:1000:1000:Student Account:/home/student:/bin/bash
student@linux-ess:~$ id student
uid=1000(student) gid=1000(student) groups=1000(student),4(adm),24(cdrom),27(sudo),30(dip),46(plugdev),110(lxd)
student@linux-ess:~$ groups
student : student adm cdrom sudo dip plugdev lxd
student@linux-ess:~$ ls -l
total 16
drwxr-xr-x 5 student student 4096 Nov  9 15:04 Documents
drwxr-xr-x 2 student student 4096 Oct 28 14:54 Downloads
drwxr-xr-x 6 student student 4096 Oct 23 12:22 linuscraft
drwx------ 5 student student 4096 Oct 19 15:07 snap
student@linux-ess:~$ sudo usermod -g it student
[sudo] password for student:
student@linux-ess:~$ grep student /etc/passwd
student:x:1000:1999:Student Account:/home/student:/bin/bash
student@linux-ess:~$ id student
uid=1000(student) gid=1999(it) groups=1999(it),4(adm),24(cdrom),27(sudo),30(dip),46(plugdev),110(lxd)
student@linux-ess:~$ id 
uid=1000(student) gid=1000(student) groups=1999(it),4(adm),24(cdrom),27(sudo),30(dip),46(plugdev),110(lxd)
student@linux-ess:~$ groups student
student : it adm cdrom sudo dip plugdev lxd
student@linux-ess:~$ groups 
student : student adm cdrom sudo dip plugdev lxd
student@linux-ess:~$ ls -l
total 16
drwxr-xr-x 5 student it 4096 Nov  9 15:04 Documents
drwxr-xr-x 2 student it 4096 Oct 28 14:54 Downloads
drwxr-xr-x 6 student it 4096 Oct 23 12:22 linuscraft
drwx------ 5 student it 4096 Oct 19 15:07 snap
student@linux-ess:~$ touch test
student@linux-ess:~$ ls -l
total 16
drwxr-xr-x 5 student it      4096 Nov  9 15:04 Documents
drwxr-xr-x 2 student it      4096 Oct 28 14:54 Downloads
drwxr-xr-x 6 student it      4096 Oct 23 12:22 linuscraft
drwx------ 5 student it      4096 Oct 19 15:07 snap
-rw-r--r-- 1 student student    0 Nov 18 14:02 test
student@linux-ess:~$ exit
```

Notice in the example above that when we changed the primary group, all the user student's files were also edited to the new primary group of this user. But because we didn't update the groups by logging out and in again, our old primary group is used for the new file. In the Permissions chapter of this course we'll learn how to change the groupowner to correct this mistake. If we log in again, we see that our groups are updated.

```bash
ssh student@ip-address # Log in again
student@linux-ess:~$ touch test2
student@linux-ess:~$ ls -l
total 16
drwxr-xr-x 5 student it      4096 Nov  9 15:04 Documents
drwxr-xr-x 2 student it      4096 Oct 28 14:54 Downloads
drwxr-xr-x 6 student it      4096 Oct 23 12:22 linuscraft
drwx------ 5 student it      4096 Oct 19 15:07 snap
-rw-r--r-- 1 student student    0 Nov 18 14:02 test
-rw-r--r-- 1 student it         0 Nov 18 14:04 test2
student@linux-ess:~$ groups
student : it adm cdrom sudo dip plugdev lxd
student@linux-ess:~$ id
uid=1000(student) gid=1999(it) groups=1999(it),4(adm),24(cdrom),27(sudo),30(dip),46(plugdev),110(lxd)
```
