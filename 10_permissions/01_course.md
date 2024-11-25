# Permissions

From the very start, Unix (and thus Linux) was built as a multiuser operating system. Having multiple users on the same system means you need a way to keep users from accessing files from other users, and keep regular users from accessing files and programs that are intended to be used only by the system administrator. On the other hand users also need to be able to share files with others so they can collaborate effectively. As a system administrator being able to lock down or grant access to files is one the most important steps in keeping a system secure. 

As you have seen in the previous section, your system already comes with a sensible set of file permissions. As a regular user you have full control in your own homefolder. You can create, edit and remove files and folders within your own home-directory `/home/student`. If you try to create or alter a file outside your homefolder you will get an error (permission denied). The only exception is the directory _/tmp_. Eg: You are able to see the user database in `/etc/passwd` but cannot edit it as a regular user. Sometimes a regular user isn't even allowed to see the contents of a certain file or directory. Eg: `/etc/shadow` holds the passwords of users, that is why you are not even allowed to read it. 

Permission errors are a common source of problems. Understanding and manipulating file permissions is a crucial step in becoming a competent Linux admin.

?> <i class="fa-solid fa-circle-info"></i> Just because you can, doesn't mean you should. When troubleshooting permission errors always remember that permissions are your first line of defense against malicious actors. Always ask yourself why a program or a user should have access, and handle with caution. Don't just grant permissions to get rid of the error!

## Octal notations

When looking at the extended info for a file using `ls` with the `-l` option (=long listing), you'll see three sets of three permissions applied to the file. The possible permissions are: **r**ead, **w**rite and e**x**ecute. Permission to read a file's content, permission to change a file's content and permission to execute a file as a script or program. When a permission is not granted, you'll find a - in the position of the permission denied. 

```bash
student@linux-ess:~/course$ ls -l
total 4
-rw-rw-r-- 1 student student    0 okt  2 19:36 config
drwxrwxr-x 2 student student 4096 okt  2 19:36 folder
-rw-rw-r-- 1 student student    0 okt  2 19:36 rights.jpg
-rw-rw-r-- 1 student student    0 okt  2 19:36 test.txt
```

?> <i class="fa-solid fa-circle-info"></i> The first character is a _-_ (minus) for a regular file and a _d_ for a directory. There are also some special characters: _b_ for block files, _c_ for character device files, _p_ for pile files, _l_ for symbolic link files and _s_ for socket files.


?> <i class="fa-solid fa-circle-info"></i> Directories in Linux have the same set of permissions. But because you need execute to access files in the directory, there is little you can do without it. The common permissions are rwx for a directory where you can do everything, r-x for a read-only directory, and ofcourse --- when you want to block access completely. 

There are three sets because there are three different sets of people that permissions can be applied to. The first set describes the permissions for the owner of the file (the first name behind the permissions), the second applies to everyone that is a member of the group that owns the file (the second name). The last set is for everyone who doesn't fall under one of the first two categories. So in short: The three sets apply to **userowner**, **groupowner** and **others**, in that order.

When a user creates a file he automatically becomes the owner of that file. The group that owns the file is determined by the user's **primary group**. By default a user's primary group is a group with the same name as the username, which is why you'll often see owner and group owner have the same name (like _student student_ in the above example). The `/dev` folder, that contains the files representing your hardware, is one of the places where you'll find files owned by the root-user with a different group as owner.

```bash
student@linux-ess:~$ ls -l /dev/s[dr]?
brw-rw---- 1 root disk   8, 0 Nov 11 10:44 /dev/sda
brw-rw---- 1 root cdrom 11, 0 Nov 11 10:43 /dev/sr0
```

File permissions are written on disk as a field of bits in the file's properties. A bit is set to 1 when a permission is granted, 0 when it's not. So rwxrw-r-- becomes 111110100. Because humans are not very good at parsing binary sequences, they are represented as as octal numbers, numbers from 0 to 7 (000 to 111 in binary). To calculate the octal number remember that read is worth 4, write 2 and execute 1. Add those you need and you'll get the octal notation. The example above becomes 764 (rwx = 4+2+1=7,      rw- = 4+2+0=6,        r-- = 4+0+0=4).



| **Binary** | **Octal** | **Permission (rwx)** | **Short Description**                           |
| ---------- | --------- | -------------------- | ----------------------------------------------- |
| `000`      | `0`       | `---`                | No permissions: cannot read, write, or execute. |
| `001`      | `1`       | `--x`                | Execute only: can run as a program.             |
| `010`      | `2`       | `-w-`                | Write only: can modify but not read.            |
| `011`      | `3`       | `-wx`                | Write and execute: modify and run as a program. |
| `100`      | `4`       | `r--`                | Read only: can view but not modify or execute.  |
| `101`      | `5`       | `r-x`                | Read and execute: view and run as a program.    |
| `110`      | `6`       | `rw-`                | Read and write: view and modify.                |
| `111`      | `7`       | `rwx`                | Full permissions: view, modify, and execute.    |



## Changing permissions (chmod)

To change the permissions on a file you can use the `chmod` command.

To add or substract permissions of a file you can use the following method, where _rwx_ stands for the rights you want to add or substract, and _ugo_ stands for userowner, groupowner and others respectively. If you don't specify for who you want the change, it is changed on all three:

```bash
student@linux-ess:~$ touch test  
student@linux-ess:~$ ls -l test
-rw-rw-r-- 1 student student 0 Nov 11 13:11 test
student@linux-ess:~$ chmod +x test  
student@linux-ess:~$ ls -l test   
-rwxrwxr-x 1 student student 0 okt  2 19:36 test  
student@linux-ess:~$ chmod g-w test  
student@linux-ess:~$ ls -l test   
-rwxr-xr-x 1 student student 0 okt  2 19:36 test  
student@linux-ess:~$ chmod go-rx test
student@linux-ess:~$ ls -l test 
-rwx------ 1 student student 0 okt  2 19:36 test
```

When completely rewrite permissions you can also use chmod with an octal notation: 

```bash
student@linux-ess:~$ touch config  
student@linux-ess:~$ ls -l config  
-rw-rw-r-- 1 student student    0 okt  2 19:36 config
student@linux-ess:~$ chmod 600 config 
student@linux-ess:~$ ls -l config
-rw------- 1 student student    0 okt  2 19:36 config
student@linux-ess:~$ chmod 744 config
student@linux-ess:~$ ls -l config
-rwxr--r-- 1 student student    0 okt  2 19:36 config
```

The latter option is faster when you have to completely rewrite permissions (since you don't need to check the existing permissions, just overwrite). The former can be practical for making quick changes like making a file executable.

## Changing ownership (chgrp, chown)

Besides changing the permissions of a file, you'll also need to change to whom these permissions apply to, by changing the user or group that owns the file. You will need sudo to assign files to different users/groups.

To change the group owner of a file or directory, you can use the `chgrp` command. To change this recursively use the `-R` option

```bash
student@linux-ess:~$ ls -l course/
total 4
-rwxr--r-- 1 student student    0 okt  2 19:36 config
drwxrwxr-x 2 student student 4096 okt  2 19:36 folder
-rw-rw-r-- 1 student student    0 okt  2 19:36 rights.jpg
-rw-rw-rw- 1 student student    0 okt  2 19:36 test.txt
student@linux-ess:~$ sudo chgrp -R it course/
student@linux-ess:~$ ls -l course/
total 4
-rwxr--r-- 1 student it    0 okt  2 19:36 config
drwxrwxr-x 2 student it 4096 okt  2 19:36 folder
-rw-rw-r-- 1 student it    0 okt  2 19:36 rights.jpg
-rw-rw-rw- 1 student it    0 okt  2 19:36 test.txt
student@linux-ess:~$ ls -ld course/
drwxrwxr-x 3 student it 4096 okt  2 19:36 course/
```
The `chown` command is more versatile, it allows you to change owner and/or group. It has the same -R option to change an entire file-tree.

```bash
student@linux-ess:~/course$ sudo chown teacher rights.jpg #changes the owner
student@linux-ess:~/course$ ls -l rights.jpg
-rw-rw-r-- 1 teacher it    0 okt  2 19:36 rights.jpg
student@linux-ess:~/course$ sudo chown teacher:root config folder #changes owner and group
student@linux-ess:~/course$ ls -l 
total 4
-rwxr--r-- 1 teacher root    0 okt  2 19:36 config
drwxrwxr-x 2 teacher root 4096 okt  2 19:36 folder
-rw-rw-r-- 1 teacher it        0 okt  2 19:36 rights.jpg
-rw-rw-rw- 1 student it        0 okt  2 19:36 test.txt
student@linux-ess:~/course$ sudo chown :it config #changes the group
student@linux-ess:~/course$ ls -l config
-rwxr--r-- 1 teacher    it        0 okt  2 19:36 config
```



## Default permissions (umask)

Another important aspect we need to look at are the default permissions. What permissions are applied when you create new files and folders? 

The maximum permissions for new files is 666, so -rw-rw-rw-. New files are never created with execute permissions. This is enforced by the kernel. It is of course possible to add the execute bit after file creation using `chmod`, but it always requires a conscious decission for security reasons. Folders don't have this limitation as a folder without an execute bit set is quite useless. 

```bash
student@linux-ess:~/course$ touch file
student@linux-ess:~/course$ mkdir folder
student@linux-ess:~/course$ ls -l
total 4
-rw-rw-r-- 1 student student    0 okt 15 15:56 file
drwxrwxr-x 2 student student 4096 okt 15 15:56 folder
```
As you can see, we don't get the expected -rw-rw-rw- for the file, nor drwxrwxrwx for the folder. This is because most distributions are more strict than the Linux kernel allows. Using the kernel default would mean created files and folders are writable by every user on the system. They are however readable by `other` so beware of this with sensitive files.

The exact configuration of permissions for new files and folders is set by the `umask`. This is a value that defines the 'mask' that is applied for all newly created files and folders. To see the current mask, use the command `umask`.

```bash
student@linux-ess:~/course$ umask
0002
```
So how does this work? We subtract the umask from 777 and never give execute rights to a new file. So for a file you get 775 (rwxrwxr-x), but because you never set the execute bit this results in 664 or rw-rw-r-- . For folders we also subtract the umask (here 002) from 777, this results in 775 and here we keep the execution-bits. A umask of 000 allows everything, a umask of 777 will make a new file and folder have no permissions. The numbers still work the same (4 for read, 2 for write, 1 for execute) but this time you are using them to **mask** certain permission bits, or put more simply: deny certain permissions on new files and folders.

You can set (=change) the umask by using the same umask command.

```bash
student@linux-ess:~/course$ umask 000       # 777-000=777 and the x is never applied to new files
student@linux-ess:~/course$ touch newfile1
student@linux-ess:~/course$ ls -l newfile1
-rw-rw-rw- 1 student student 0 okt 15 16:23 newfile1
student@linux-ess:~/course$ umask 027 #if you want to mask multiple bits, add them together  (777-027=750)
student@linux-ess:~/course$ touch newfile2
student@linux-ess:~/course$ ls -l newfile2
-rw-r----- 1 student student 0 okt 15 16:24 newfile2
student@linux-ess:~/course$ umask 077 
student@linux-ess:~/course$ mkdir newfolder1
student@linux-ess:~/course$ ls -ld newfolder1
drwx------ 2 student student 4096 okt 15 16:25 newfolder1
```
?> <i class="fa-solid fa-circle-info"></i> Setting the umask using the command changes the umask for your current terminal session. Exiting the terminal will reset it to the default value. To make it permanent add `umask <your umask>` to your user's `.profile` file in your home directory.


One last thing to be aware of: If you look at the following example, you'll see that files created by the root user have a different umask set.

```bash
student@linux-ess:~/course$ touch file
student@linux-ess:~/course$ sudo touch file2
student@linux-ess:~/course$ ls -l
-rw-rw-r-- 1 student student 0 okt 15 16:44 file
-rw-r--r-- 1 root    root    0 okt 15 16:44 file2
```
This is explained by looking at the system-wide umask setting, found in the `/etc/login.defs` file.

```bash
student@linux-ess:~/course$ nano /etc/login.defs
UMASK           022 #line 151
...
USERGROUPS_ENAB yes #line 230
```
To change the setting system-wide you can change the value for umask there. The default umask specified is the one the root user uses (no write for anybody but the owner). The reason files created by regular users get an extra w for the group, is the option on line 230. This option specifies that for any non-root user that has the same user-id as group-id (so the primary group is unchanged) the group umask-bits gets changed to the user umask-bits, explaining the 002 umask seen earlier.


?> <i class="fa-solid fa-circle-info"></i> You can also use the letter notation with umask:
```bash
student@linux-ess:~$ umask
0002
student@linux-ess:~$ umask -S
u=rwx,g=rwx,o=rx
student@linux-ess:~$ touch file3
student@linux-ess:~$ ls -l file3
-rw-rw-r-- 1 student student 0 Nov 11 14:01 file3
student@linux-ess:~$ umask u=rwx,g=rx,o=
student@linux-ess:~$ umask
0027
student@linux-ess:~$ umask -S
u=rwx,g=rx,o=
student@linux-ess:~$ touch file4
student@linux-ess:~$ ls -l file4
-rw-r----- 1 student student 0 Nov 11 14:03 file4
```

  

## Working together in a team (setgid)

If we want to be able to work together it is key that certain users are able to change each others files in a shared folder. The solution to give these users the same primary group is a security issue because this also changes the rights on their homefolders:

```bash
student@linux-ess:~$ sudo groupadd it 
student@linux-ess:~$ sudo useradd -m -g it -s /bin/bash liam
student@linux-ess:~$ sudo passwd liam
student@linux-ess:~$ sudo useradd -m -g it -s /bin/bash jacob
student@linux-ess:~$ sudo passwd jacob
student@linux-ess:~$ ls -ld /home/liam  /home/jacob
drwxr-x--- 2 jacob it 4096 Nov 26 15:39 /home/jacob
drwxr-x--- 2 liam  it 4096 Nov 26 15:32 /home/liam
student@linux-ess:~$ sudo ls -l /home/jacob/.profile
-rw-r--r-- 1 jacob it 807 Jan  6  2022 /home/jacob/.profile
student@linux-ess:~$ su - liam
Password:
liam@linux-ess:~$ head -3 /home/jacob/.profile
# ~/.profile: executed by the command interpreter for login shells.
# This file is not read by bash(1), if ~/.bash_profile or ~/.bash_login
# exists.  
liam@linux-ess:~$ exit
```

?> As you can see the user Liam can view the files from the homefolder of the user Jacob and this isn't what we want.

First of all we will give both users their own primary group:
```bash
student@linux-ess:~$ sudo groupadd liam
student@linux-ess:~$ sudo groupadd jacob
student@linux-ess:~$ sudo usermod -g liam liam
student@linux-ess:~$ sudo usermod -g jacob jacob
student@linux-ess:~$ ls -ld /home/liam  /home/jacob
drwxr-x--- 2 jacob jacob 4096 Nov 26 15:39 /home/jacob
drwxr-x--- 2 liam  liam  4096 Nov 26 15:32 /home/liam
student@linux-ess:~$ sudo ls -l /home/jacob/.profile
-rw-r--r-- 1 jacob jacob 807 Jan  6  2022 /home/jacob/.profile
```

?> Note that changing the primary group of a user also changes the groupowner of every file in his homefolder.

We will create a group for the two users to give them rights on a shared folder that we will create in the next step. We'll also add the users to this new group:
```bash
student@linux-ess:~$ sudo groupadd ict
student@linux-ess:~$ sudo usermod -aG ict liam
student@linux-ess:~$ sudo usermod -aG ict jacob
student@linux-ess:~$ grep ict /etc/group
ict:x:1005:liam,jacob
```

We will make the directory that will be shared between the two users, and we will give it the necessary permissions:
```bash
student@linux-ess:~$ sudo mkdir -p /shares/ict
student@linux-ess:~$ ls -ld /shares/ict
drwxr-xr-x 2 root root 4096 Nov 26 15:58 /shares/ict
student@linux-ess:~$ sudo chgrp ict /shares/ict
student@linux-ess:~$ ls -ld /shares/ict
drwxr-xr-x 2 root ict 4096 Nov 26 15:58 /shares/ict
student@linux-ess:~$ sudo chmod g+w /shares/ict
student@linux-ess:~$ ls -ld /shares/ict
drwxrwxr-x 2 root ict 4096 Nov 26 15:58 /shares/ict
```

?> As you can see members of the group ict have the permission to enter the shared folder ict and to create/delete files and folders within that folder

But there's a problem when the users create a file within the share:
```bash
student@linux-ess:~$ su - jacob
Password:
jacob@linux-ess:~$ cd /shares/ict/
jacob@linux-ess:/shares/ict$ touch testfile
jacob@linux-ess:/shares/ict$ mkdir testdir
jacob@linux-ess:/shares/ict$ ls -l
total 4
drwxrwxr-x 2 jacob jacob 4096 Nov 26 16:12 testdir
-rw-rw-r-- 1 jacob jacob    0 Nov 26 16:11 testfile
jacob@linux-ess:/shares/ict$ exit
logout
student@linux-ess:~$ su - liam
Password:
liam@linux-ess:~$ cd /shares/ict/
liam@linux-ess:/shares/ict$ ls
testdir  testfile
liam@linux-ess:/shares/ict$ echo hallo >> testfile
-bash: testfile: Permission denied
liam@linux-ess:/shares/ict$ ls -ld testdir
drwxrwxr-x 2 jacob jacob 4096 Nov 27 20:44 testdir
liam@linux-ess:/shares/ict$ cd testdir
liam@linux-ess:/shares/ict/testdir$ touch testfile2
touch: cannot touch 'testfile2': Permission denied
liam@linux-ess:/shares/ict$ exit
```

?> As you can see they cannot work together on the same files or in the same directories

A solution is the use of the special bit, named setgid.
We can give it to the shared folder ict with the command chmod g+s (to remove we would use g-s):
```bash
student@linux-ess:~$ ls -ld /shares/ict/
drwxrwxr-x 3 root ict 4096 Nov 26 16:12 /shares/ict/
student@linux-ess:~$ sudo chmod g+s /shares/ict
student@linux-ess:~$ ls -ld /shares/ict/
drwxrwsr-x 3 root ict 4096 Nov 26 16:12 /shares/ict/
```

?> As you can see in the permissions of the groupowner it now ends with a letter _s_. A lowercase _s_ means that there is an _x_ underneath, an uppercase _S_ means that there is no _x_ underneath.

The special bit setgid means that files and folders that will be created in this folder will get the same groupowner as this folder itself:
```bash
student@linux-ess:~$ ls -l /shares/ict/ 
total 4
drwxrwxr-x 2 jacob jacob 4096 Nov 26 16:12 testdir
-rw-rw-r-- 1 jacob jacob    0 Nov 26 16:11 testfile
student@linux-ess:~$ su - jacob
Password:
jacob@linux-ess:~$ cd /shares/ict/
jacob@linux-ess:/shares/ict$ echo "This is Jacob's text" > testfile2
jacob@linux-ess:/shares/ict$ mkdir testdir2
jacob@linux-ess:/shares/ict$ ls -l
total 12
drwxrwxr-x 2 jacob jacob 4096 Nov 26 16:12 testdir
drwxrwsr-x 2 jacob ict   4096 Nov 26 16:26 testdir2
-rw-rw-r-- 1 jacob jacob    0 Nov 26 16:11 testfile
-rw-rw-r-- 1 jacob ict     21 Nov 26 16:26 testfile2
jacob@linux-ess:/shares/ict$ exit
logout
student@linux-ess:~$ su - liam
Password:
liam@linux-ess:~$ cd /shares/ict/
liam@linux-ess:/shares/ict$ echo "This is Liam's text" >> testfile2
liam@linux-ess:/shares/ict$ cat testfile2
This is Jacob's text
This is Liam's text
liam@linux-ess:/shares/ict$ exit
```

?> As you can see the groupowner of the new folder and file is ict and that's why both users can now work together with eachother's files.

?> Also notice that the subdirectory which has been created also gets the setgid-bit set!

## The sticky bit

The setgid bit solves the main problem of making files in a shared folder created by one user accessible to other users in the same non-primary group. However this opens up another problem: Every user with access to the share can now delete or rename the files of other users in this folder. In some cases, like a shared project people are working on, this is fine. But in cases you don't want to allow this, another special permission bit is used: the **sticky bit**. Setting this bit on a folder will disallow any user (except the user root) from renaming or removing files or subfolders he does not own inside that folder.

This principle is also used in the system's `/tmp` folder, disallowing users to remove another user's temporary files.

```bash
student@linux-ess:~$ ls -ld /tmp/
drwxrwxrwt 24 root root 4096 nov 27 13:50 /tmp/
```
?> Notice the t that replaced the x in the 'other' set of permissions when the sticky bit is set.

Just like with other permission bits you use **chmod** to add or remove the sticky bit.

```bash
student@linux-ess:~$ su - liam
Password: 
liam@linux-ess:~$ cd /shares/ict/
liam@linux-ess:/shares/ict$ ls -l
total 8
-rw-rw-r-- 1 jacob jacob    0 nov 27 14:59 testdir
drwxrwsr-x 2 jacob ict   4096 nov 27 15:03 testdir2
-rw-rw-r-- 1 jacob jacob    0 nov 27 14:59 testfile
-rw-rw-r-- 1 jacob ict      4 nov 27 15:03 testfile2
liam@linux-ess:/shares/ict$ rm testfile2 	#Liam can remove Jacob's file.
liam@linux-ess:/shares/ict$ ls -l
total 4
-rw-rw-r-- 1 jacob jacob    0 nov 27 14:59 testdir
drwxrwsr-x 2 jacob ict   4096 nov 27 15:03 testdir2
-rw-rw-r-- 1 jacob jacob    0 nov 27 14:59 testfile
liam@linux-ess:/shares/ict$ exit
logout
student@linux-ess:~$ sudo chmod o+t /shares/ict/         # or sudo chmod +t /shares/ict/
student@linux-ess:~$ ls -ld /shares/ict/
drwxrwsr-t 3 root ict 4096 nov 27 15:05 /shares/ict/
student@linux-ess:~$ su - liam
Password: 
liam@linux-ess:~$ cd /shares/ict
liam@linux-ess:/shares/ict$ rm -rf testdir2/  #Liam can no longer delete Jacob's files or folders
rm: cannot remove 'testdir2/': Operation not permitted	
liam@linux-ess:/shares/ict$ exit
logout
student@linux-ess:~$ sudo chmod o-t /shares/ict/         # or sudo chmod -t /shares/ict/
student@linux-ess:~$ ls -ld /shares/ict/
drwxrwsr-x 3 root ict 4096 nov 27 15:05 /shares/ict/
```

Within the special permissions field, the sticky bit is the rightmost bit, with a value of one. You can use this if you want to completely rewrite the permissions of a folder using octal notation. Just add a one before the standard mode.

```bash
student@linux-ess:~$ cd /shares/
student@linux-ess:/shares$ sudo mkdir ict2
student@linux-ess:/shares$ sudo chown :ict ict2/         # or sudo chgrp ict ict2/
student@linux-ess:/shares$ ls -ld ict2/
drwxr-xr-x 2 root ict 4096 nov 27 15:16 ict2/
student@linux-ess:/shares$ sudo chmod 1775 ict2/
student@linux-ess:/shares$ ls -ld ict2/
drwxrwxr-t 2 root ict 4096 nov 27 15:16 ict2/
```

It's also possible to combine the special bits. In the example below we will combine the sticky bit with the setgid bit, the second bit in the triplet with a value of two. To become the final value you just add both values together (setgid+sticky=2+1=3) and put it in front of the octal permissions (eg.3750) to become a four-digit-mode.

```bash
student@linux-ess:/shares$ sudo mkdir ict3
student@linux-ess:/shares$ sudo chown :ict ict3         # or sudo chgrp ict ict3/
student@linux-ess:/shares$ ls -ld ict3
drwxr-xr-x 5 root ict 4096 nov 27 15:20 ict3
student@linux-ess:/shares$ sudo chmod o-rx ict3
student@linux-ess:/shares$ ls -ld ict3
drwxr-x--- 5 root ict 4096 nov 27 15:20 ict3
student@linux-ess:/shares$ sudo chmod 3770 ict3
student@linux-ess:/shares$ ls -ld ict3
drwxrws--T 2 root ict 4096 nov 27 15:20 ict3 #both setgid and sticky bit are set, when the x for other is not set it displays a capital T
```

To unset the sticky bit use a zero. A three-digit mode will also remove the sticky bit. Notice that the setgid bit is kept. To remove all special permissions add another zero in front (00xxx)!

```bash
student@linux-ess:/shares$ ls -ld ict3/
drwxrws--T 2 root ict 4096 nov 27 15:20 ict3/
student@linux-ess:/shares$ sudo chmod 0777 ict3/        # or chmod 777
student@linux-ess:/shares$ ls -ld ict3/
drwxrwsrwx 2 root ict 4096 nov 27 15:20 ict3/
student@linux-ess:/shares$ sudo chmod 00775 ict3/
student@linux-ess:/shares$ ls -ld ict3/
drwxrwxr-x 2 root ict 4096 nov 27 15:20 ict3/
```

If you want the users of the group ict to work together on each others files and at the same time you want that they can't remove each other's files, you have to set the kernel parameter fs.protected_regular=1.
```bash
student@linux-ess:~$ ls -ld /shares/ict/
drwxrwsr-t 3 root ict 4096 nov 27 15:05 /shares/ict/
student@linux-ess:~$ su - liam
Password: 
liam@linux-ess:~$ cd /shares/ict/
liam@linux-ess:/shares/ict$ ls -l
total 8
-rw-rw-r-- 1 jacob jacob    0 nov 27 14:59 testdir
drwxrwsr-x 2 jacob ict   4096 nov 27 15:03 testdir2
-rw-rw-r-- 1 jacob jacob    0 nov 27 14:59 testfile
-rw-rw-r-- 1 jacob ict      4 nov 27 15:03 testfile2
liam@linux-ess:/shares/ict$ echo text from liam > testfile2 	#Liam cannot change Jacob's files.
-bash: testfile2 Permission denied
liam@linux-ess:/shares/ict$ exit
student@linux-ess:~$ sudo sysctl -a | grep regular
fs.protected_regular = 2
student@linux-ess:~$ sudo sysctl fs.protected_regular=1
fs.protected_regular = 1
student@linux-ess:~$ su - liam
Password: 
liam@linux-ess:~$ cd /shares/ict/
liam@linux-ess:/shares/ict$ echo text from liam > testfile2 	#Liam can change Jacob's files.
liam@linux-ess:~$ cat testfile2
text from liam
```

?> If we want to keep the kernel parameter in the future we have to change this parameter in the file _/usr/lib/sysctl.d/99-protect-links.conf



## Running a binary as the fileowner (setuid)


As you may have noticed there is a third bit we haven't talked about. setuid, the leftmost bit in the field. This allows executable files to run with the permissions of the owner of the file, not the one executing it. This is used by the _passwd_ command to allow users to change their own password for example, as a normal user has no access to the /etc/shadow-file. Setting the setuid bit can have serious security risks, and is almost always a very bad idea.  

In the following example we will show why a normal user (with no privileges) is allowed to change his password in the shadow file which is only accessible for the root user.

```bash
student@linux-ess:~$ ls -l /etc/shadow
-rw-r----- 1 root shadow 2456 Nov 28  2022 /etc/shadow
student@linux-ess:~$ ls -l /bin/passwd
-rwsr-xr-x 1 root root 59976 Nov 24  2022 /bin/passwd
student@linux-ess:~$ stat -c '%a %n' /bin/passwd
4755 /bin/passwd 
```

## Special bits overview

| Permission   | Effect on files                                                               | Effect on directories                                      | 
| ------------ | ----------------------------------------------------------------------------- | ------------------ |
| u+s (etuid)  | The file will execute as the owner of the file, not as the user who ran it    | No effect          |
| g+s (setgid) | The file will execute as the group that owns the file                         | Files that are created in the directory will get the same groupowner as the directory |
| o+t (sticky) | No effect                                                                     | Users with write access to the directory can only remove file they own, they cannot remove or force save someone elses files |

## Access control lists
The ACL feature was created to give users the ability to selectively share files and folders with other users and groups. 
Before ACL’s can be implemented we need to install the package:
```bash
student@linux-ess:~$ sudo apt install acl
```
When installed, it needs to be turned on when the filesystem is mounted. In our Ubuntu installation ACL’s are loaded by default. To add ACL’s to a file or folder, use the `setfacl` command. ACL’s can be viewed with the `getfacl` command.  

?> To add ACL’s you need to be the owner of the file or folder, if you are added by an ACL you will not be able to modify the ACL’s yourself.   

?> ACL permissions have precedence over the regular file permissions. The only exception is for the userowner. When the filepermissions of the userowner are less than the ACLs for this user, then these ACLs will not be effective  (so _r--..._    and ACL    _u : student : rw_   will result in only read rights) 

?> All ACL permissions are cumulative, this means if we are in 2 groups that are added to a file with ACL’s. One with r-- rights and one with rwx rights, we will have rwx rights.   

With the `setfacl` command, we’ll be able to modify (-m) or delete (-x) ACL’s. 

```bash
student@linux-ess:~$ touch memo
student@linux-ess:~$ ls -l memo
-rw-rw-r-- 1 student student 0 Nov 11 14:15 memo
student@linux-ess:~$ getfacl memo
# file: memo
# owner: student
# group: student
user::rw-
group::rw-
other::r--

student@linux-ess:~$ setfacl -m u:teacher:rw memo
student@linux-ess:~$ setfacl -m g:it:rw memo
student@linux-ess:~$ ls -l memo
-rw-rw-r--+ 1 student student 0 Nov 11 14:15 memo
```
?> <i class="fa-solid fa-circle-info"></i> Note that we can also see that ACL’s are applied by a __+__ in the output of the `ls -l` command

With `getfacl` we can check the existing ACL’s on a file or folder. 
```bash
student@linux-ess:~$ getfacl memo
# file: memo
# owner: student
# group: student
user::rw-
user:teacher:rw-
group::rw-
group:it:rw-
mask::rw-
other::r--

```
?> <i class="fa-solid fa-circle-info"></i> For teacher to be able to access the student's file memo in it's homefolder we need to edit some permissions. A possible solution would be: `setfacl -m u:teacher:rx /home/student`. Now, teacher can enter and look in the homefolder of student.   


?> <i class="fa-solid fa-circle-info"></i> In the previous example, we also see a mask option, this option decides the maximum permission and also has precedence over the regular file permissions except for the user owner. We can also add this parameter as follows:
```bash
student@linux-ess:~$ setfacl -m m:r memo 
student@linux-ess:~$ getfacl memo 
# file: memo
# owner: student
# group: student
user::rw-
user:teacher:rw-                #effective:r--
group::rw-                      #effective:r--  
group:it:rw-                    #effective:r--
mask::r--
other::r--

student@linux-ess:~$ ls -l memo
-rw-r--r--+ 1 student student 0 Nov 11 14:15 memo
```
?> <i class="fa-solid fa-circle-info"></i> The mask is reflected by the group permissions you'll see with the command _ls -l_. 

If we want to remove an ACL entry from the file we can use the -x option:
```bash
student@linux-ess:~$ setfacl -x g:it memo
student@linux-ess:~$ getfacl memo 
# file: memo
# owner: student
# group: student
user::rw-
user:teacher:rw-                
group::rw-
mask::rw-
other::r--  

student@linux-ess:~$ ls -l memo
-rw-rw-r--+ 1 student student 0 Nov 11 14:15 memo
```

?> <i class="fa-solid fa-circle-info"></i> Note that the mask of the file _memo_ has automatically changed _rw-_. This is because we changed ACLs and the mask has to make sure that all user-ACLs and group-ACLs can be applied (user : teacher : rw-).


If we want to remove all ACL entries from the file we can use the -b option:
```bash
student@linux-ess:~$ setfacl -b memo
student@linux-ess:~$ getfacl memo 
# file: memo
# owner: student
# group: student
user::rw-
group::rw-
other::r--

student@linux-ess:~$ ls -l memo
-rw-rw-r-- 1 student student 0 Nov 11 14:15 memo
```

We can also add default ACL’s by adding the d: parameter or adding the -d option. The default part makes sure new subfiles and subfolders get the same ACL’s as the specified directory. Note that the user or group need to have the permissions to create the file or folder itself! 

```bash
student@linux-ess:~$ mkdir memos
student@linux-ess:~$ ls -ld memos
drwxrwxr-x 2 student student 4096 Nov 11 14:48 memos
student@linux-ess:~$ getfacl memos
# file: memos
# owner: student
# group: student
user::rwx
group::rwx
other::r-x
student@linux-ess:~$ setfacl -m g:it:rwx memos         # we need to add the group to the folder directly as well, otherwise the group wont be able to enter this folder.
student@linux-ess:~$ setfacl -m d:g:it:rwx memos       # or setfacl -d -m g:it:rwx memos
student@linux-ess:~$ getfacl memos
# file: memos
# owner: student
# group: student
user::rwx
group::rwx
group:it:rwx
other::r-x                 
default:user::rwx
default:group::rwx
default:group:it:rwx
default:mask::rwx
default:other::r-x

student@linux-ess:~$ mkdir memos/January
student@linux-ess:~$ getfacl memos/January/
# file: memos/January/
# owner: student
# group: student
user::rwx
group::rwx
group:it:rwx
mask::rwx
other::r-x
default:user::rwx
default:group::rwx
default:group:it:rwx
default:mask::rwx
default:other::r-x

student@linux-ess:~$ touch memos/January/24
student@linux-ess:~$ getfacl memos/January/24
# file: memos/January/24
# owner: student
# group: student
user::rw-
group::rwx                      #effective:rw-
group:it:rwx                    #effective:rw-
mask::rw-
other::r--

```
