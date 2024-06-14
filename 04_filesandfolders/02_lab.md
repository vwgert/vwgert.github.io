# Lab <!-- {docsify-ignore} -->
In the previous chapter Linus installed a package called `minetest` but he is confused as to where this package is located! In this lab we will find out how we can view and navigate through folders and how we can use some basic commands to work with files. With this knowledge we might be able to actually locate the `minetest` package and actually run the server.

## Listing directory contents

Before doing anything else, Linus really wants to find out how he can list contents of folders. He already figured out that he is using a prompt that runs commands in a specific directory as seen in the previous chapters. Using the `apropos directory` command he finds out that there are all kinds of commands available to work with directories. The first command that Linus checks out is the `pwd` command:

```bash
student@linux-ess:~$ apropos directory
...
ls (1)               - list directory contents
...
pwd (1) - print name of current/working directory
...
```

After running this command, Linus indeed sees the working directory that he is in:

```bash
student@linux-ess:~$ pwd
/home/student
```

Using the manpages he learns about the `ls` command which should list the contents of a directory:

```bash
student@linux-ess:~$ ls
```

We don't see any output. This is because, by default, our homefolder (`/home/student`) appears to be empty. There might be some hidden files that are not shown. Using the  `man ls` command he tries to look for an _option_ that allows him to view hidden files:

```bash
student@linux-ess:~$ man ls
```

To view hidden files (files that start with a `.` sign), he uses the option `-a` as follows:
```bash
student@linux-ess:~$ ls -a
.   .bash_history  .bashrc      .ssh
..  .bash_logout   .profile     .sudo_as_admin_successful
student@linux-ess:~$
```
Note that the output of the `ls -a` command may be different on your system. The main goal is that we get a list of hidden files (files starting with `.`). Linus wants to check if these files (or folders) actually contain contents. To do this he uses the `man ls` command to search for options to view file sizes:
```bash
student@linux-ess:~$ ls -alh
total 52K
drwxr-xr-x 6 dries dries 4.0K Aug 25 08:02 .
drwxr-xr-x 3 root  root  4.0K Oct  5  2021 ..
-rw------- 1 dries dries 5.5K Jun  2 10:06 .bash_history
-rw-r--r-- 1 dries dries  220 Oct  5  2021 .bash_logout
-rw-r--r-- 1 dries dries 3.7K May 31 14:59 .bashrc
-rw-r--r-- 1 dries dries  807 Oct  5  2021 .profile
drwx------ 2 dries dries 4.0K Mar 10 09:15 .ssh
-rw-r--r-- 1 dries dries    0 Oct  6  2021 .sudo_as_admin_successful
```

To find out the file size of the file he combines the options `-a`, `-l` and `-h`.  Now Linus knows that the file  `.bashrc` for example is 3,5Kb in size and was last changed on 31 May at 14:59.

## Create a folder structure 
Linus wants a clean folder structure for his _LinusCraft_ project. In his homefolder he would like to create a folder with the name `linuscraft`. To do this he found the `mkdir` command using the manpages.

```bash
student@linux-ess:~$ mkdir linuscraft
```

After creating the `linuscraft` folder he wants to create a folder `playerinfo` inside that folder. To do this he can use one of the 2 options below:

1. By using the `cd` command:
```bash
student@linux-ess:~$ cd linuscraft
student@linux-ess:~/linuscraft$ mkdir playerinfo
```

2. By using the mkdir command directly from his homefolder (`/home/student`) using a relative path:
```bash
student@linux-essentials:~$ mkdir linuscraft/playerinfo
```

He checks if the folder is created correctly by navigating to that folder using an absolute path:
```bash
student@linux-ess:~/linuscraft$ cd /home/student/linuscraft/playerinfo
student@linux-ess:~/linuscraft/playerinfo$ pwd
/home/student/linuscraft/playerinfo
```

?> Exercise: Can you navigate to the playerinfo folder using a relative path starting from your homefolder?


He would also like a folder `administration` inside the `linuscraft` folder. While using the folder `playerinfo` as the working directory (`cd /home/student/linuscraft/playerinfo`), he creates this folder using a relative path:

```bash
student@linux-ess:~/linuscraft/playerinfo$ mkdir ../administration
```

To finish up he creates the folders named `backups`, `secrets` and `serverfiles` inside the `linuscraft` folder using an absolute path:

```bash
student@linux-ess:~/linuscraft$ mkdir /home/student/linuscraft/backups /home/student/linuscraft/secrets /home/student/linuscraft/serverfiles
```
Notice how we can use multiple arguments with the `mkdir` command to create multiple folders with just one command.

Linus decides to navigate back to his homefolder by using the `cd` command without any arguments. Afterwards he checks the contents of his created folder `linuscraft`: 

```bash
student@linux-ess:~/linuscraft$ cd
student@linux-ess:~$ ls -lh linuscraft
total 12K
drwxr-xr-x 2 student student 4.0K May  4 21:45 administration
drwxr-xr-x 2 student student 4.0K May  4 21:48 backups
drwxr-xr-x 2 student student 4.0K May  4 21:44 playerinfo
drwxr-xr-x 2 student student 4.0K May  4 21:48 secrets
drwxr-xr-x 2 student student 4.0K May  4 21:48 serverfiles
```

## Create files 
Linus would like to create a file, named `todo.txt` to list any outstanding tasks. He creates this file in the folder `linuscraft` using the `touch` command:

```bash
student@linux-ess:~$ touch linuscraft/todo.txt
```

This command creates an empty file. We will find out how to insert data into the file in the next chapter's lab.

Next up he creates some additional files with the following command:

```bash
student@linux-ess:~$  touch linuscraft/contact.txt linuscraft/backuplog.txt linus.txt
```
Notice how we can provide multiple arguments to the touch command to create multiple files using just one command.

He wants to create a hidden file in the secrets folder to store private information as well using an absolute path:

```bash
student@linux-ess:~$ touch /home/student/linuscraft/secrets/.private
```
He checks if all files have been created succesfully using the following set of commands:
```bash
student@linux-ess:~$ ls ~
linus.txt  linuscraft
student@linux-ess:~$ ls linuscraft/
administration  backuplog.txt  backups  contact.txt  playerinfo  secrets  serverfiles  todo.txt
student@linux-ess:~$ ls -a /home/student/linuscraft/secrets/
.  ..  .private
```

## Finetune the file and folder structure 

There are some problems with the files and folders that we just created. The `linus.txt` file for instance is created in the homefolder of the user `student`. We have to move this file to the `playerinfo` folder:

```bash
student@linux-ess:~$ mv linus.txt linuscraft/playerinfo/
```

There are 3 `txt` files present in the `linuscraft` folder. Linus learnt that in Linux files do do not need file extentions so he wants to remove them using only one command. To achieve this goal, he uses the `rename` command:

```bash
student@linux-ess:~$ cd linuscraft
student@linux-ess:~/linuscraft$ ls
administration  backuplog.txt  backups  contact.txt  playerinfo  secrets  todo.txt
student@linux-ess:~/linuscraft$ rename 's/\.txt//' *.txt
student@linux-ess:~/linuscraft$ ls
administration  backuplog  backups  contact  playerinfo  secrets  todo
```

The `secrets` folder and its contents are no longer needed so Linus decides to delete it while having `~/linuscraft` as his working directory (`cd ~/linuscraft`):

```bash
student@linux-ess:~/linuscraft$ rm -rf secrets
```

In the next chapter's lab we will learn how we can add file contents to the files we just created.
