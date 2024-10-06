# Lab <!-- {docsify-ignore} --> 




In a previous chapter we created a cloud instance (=server) and we also created an ssh key and linked it to this instance. This allows us to log in with this keypair under the user ubuntu (= standard user of the AWS-Ubuntu image). Linus is now curious where the public ssh key is located on the server.

## Searching for the public ssh key 

Before he can find anything, Linus wants to know the best way to search the folders. Using the command ***apropos find*** he discovers that there are several commands available to search in a folder structure. This is how he finds the commands *find* and *locate*.

```bash
ubuntu@aws-linux-ess:~$ apropos find
...
find (1)             - search for files in a directory hierarchy
...
locate (1)           - find files by name, quickly
...
```



?> <i class="fa-solid fa-circle-info"></i> If the commando ***apropos find*** results in the text  *find: nothing appropriate.*  ,you must rebuild the man-database with the command ***sudo mandb*** and try again. If the command doesn't find locate, it's because locate isn't installed yet. First install the package with ***sudo apt install plocate***.  If the package *plocate* can't be found for installation, you firstly have to run the command ***sudo apt update***



He figures out how to use the *locate* command:

```bash
ubuntu@aws-linux-ess:~$ man locate
locate(1)                                      General Commands Manual                                      locate(1)

NAME
       plocate - find files by name, quickly

SYNOPSIS
       plocate [OPTION]...  PATTERN...

DESCRIPTION
       plocate  finds  all  files  on  the  system matching the given pattern (or all of the patterns if multiple are
       given). It does this by means of an index made by updatedb(8) or (less commonly) converted from another  index
       by plocate-build(8).
```



?> <i class="fa-solid fa-circle-info"></i> If the commando ***man locate*** results in the text  *find: nothing appropriate.*  ,you must rebuild the man-database with the command ***sudo mandb*** and try again.



Searching for files or folders with the word key in the name produces the following results:

```bash
ubuntu@aws-linux-ess:~$ locate key
/boot/grub/i386-pc/at_keyboard.mod
/boot/grub/i386-pc/keylayouts.mod
/boot/grub/i386-pc/keystatus.mod
/boot/grub/i386-pc/sendkey.mod
/boot/grub/i386-pc/usb_keyboard.mod
/boot/grub/x86_64-efi/at_keyboard.mod
/boot/grub/x86_64-efi/keylayouts.mod
/boot/grub/x86_64-efi/keystatus.mod
/boot/grub/x86_64-efi/usb_keyboard.mod
/etc/apparmor.d/keybase
/etc/apparmor.d/abstractions/ssl_keys
/etc/apt/keyrings
/etc/apt/trusted.gpg.d/ubuntu-keyring-2012-cdimage.gpg
/etc/apt/trusted.gpg.d/ubuntu-keyring-2018-archive.gpg
/etc/chrony/chrony.keys
/etc/console-setup/cached_setup_keyboard.sh
/etc/default/keyboard
/etc/init.d/keyboard-setup.sh
/etc/rcS.d/S01keyboard-setup.sh
/etc/ssh/ssh_host_ecdsa_key
/etc/ssh/ssh_host_ecdsa_key.pub
/etc/ssh/ssh_host_ed25519_key
/etc/ssh/ssh_host_ed25519_key.pub
/etc/ssh/ssh_host_rsa_key
/etc/ssh/ssh_host_rsa_key.pub
/etc/systemd/system/sshd-keygen@.service.d
/etc/systemd/system/multi-user.target.wants/ec2-instance-connect-harvest-hostkeys.service
/etc/systemd/system/sshd-keygen@.service.d/disable-sshd-keygen-if-cloud-init-active.conf
/etc/systemd/system/sysinit.target.wants/keyboard-setup.service
/etc/systemd/user/sockets.target.wants/keyboxd.socket
/home/ubuntu/.ssh/authorized_keys
...
```

The last visible line above shows how somewhere in his home folder there is a file called *authorized_keys*.



Linus also figures out how he could have used the *find* command:

```bash
ubuntu@aws-linux-ess:~$ man find
```



Searching, with *find*, for files or folders with the word key in the name produces the following results:

```bash
ubuntu@aws-linux-ess:~$ find -name "*key*"
./.ssh/authorized_keys
```



Note that the output of the command starts with *./*. This indicates that *.ssh* is located in the current directory. The fact that the folder *.ssh* starts with a period (.) indicates that this folder is hidden. The ls command will therefore not show this folder. We will have to use the command *ls -a* so that the hidden files and folders are also visible.

```bash
ubuntu@aws-linux-ess:~$ ls -a
.   .bash_history  .bashrc  .config   .local    .ssh
..  .bash_logout   .cache   .lesshst  .profile  .sudo_as_admin_successful
```

 

With the *file* command, Linus can find out what type of file *.ssh* is.

```bash
ubuntu@aws-linux-ess:~$ file .ssh
.ssh: directory
```



He moves around the folder, looks at the contents and determines which type of file *authorized_keys* is.

```
ubuntu@aws-linux-ess:~$ cd .ssh
ubuntu@aws-linux-ess:~/.ssh$ ls
authorized_keys
ubuntu@aws-linux-ess:~/.ssh$ file authorized_keys
authorized_keys: OpenSSH ED25519 public key
```

So this is the public key that belongs to the private key that was downloaded onto his laptop from AWS.



You can view the contents of the file with ***cat authorized_keys***

```bash
ubuntu@aws-linux-ess:~/.ssh$ cat authorized_keys
ssh-ed25519 AAAAC3NzaC1lZDI1NTE5AAAAIGg8jhO/tYNeKuHodLUbgnmUn1mUJiRofPkWWWf17Mnp gert-key
```



## Backup the public ssh key 

To be on the safe side, Linus wants to backup the *authorized_keys* file in the same folder. He does this by copying the file. He needs to use quotes because he wants a space in the name.

```bash
ubuntu@aws-linux-ess:~/.ssh$ cp authorized_keys "authorized_keys backup"
ubuntu@aws-linux-ess:~/.ssh$ ls
 authorized_keys  'authorized_keys backup'
```



On second thought, perhaps the space makes it unnecessarily more difficult. He renames the file to no longer have any spaces in it.

```bash
ubuntu@aws-linux-ess:~/.ssh$ mv "authorized_keys backup" authorized_keys.backup
ubuntu@aws-linux-ess:~/.ssh$ ls
authorized_keys  authorized_keys.backup
```



It would perhaps be clearer if all backups were stored together in a folder *backups* directly in the home folder. This can be done as follows:

```bash
ubuntu@aws-linux-ess:~/.ssh$ cd
ubuntu@aws-linux-ess:~$ mkdir backups
ubuntu@aws-linux-ess:~$ mv .ssh/authorized_keys.backup backups/
ubuntu@aws-linux-ess:~$ ls .ssh
authorized_keys
ubuntu@aws-linux-ess:~$ ls backups/
authorized_keys.backup
ubuntu@aws-linux-ess:~$ tree .ssh backups
.ssh
└── authorized_keys
backups
└── authorized_keys.backup

2 directories, 2 files
```



## Storing Public IP 

In principle, the IP address of the server should always remain the same. To check this at a later time, Linus wants to put the current IP address in a file.

First he finds out the current public IP address. He no longer knows the command to do this, but knows that it was something with *curl* and that he has executed this command before. He therefore searches the history of his shell commands with the key combination ***CTRL+r***.

```bash
ubuntu@aws-linux-ess:~$     (CTRL+r)
(reverse-i-search)`curl': curl checkip.amazonaws.com
ubuntu@aws-linux-ess:~$ curl checkip.amazonaws.com
54.87.203.25
```



He can place this IP address in a file called *PublicIP* with the command ***nano PublicIP***.  You can close the editor (nano) with the key combinations ***CTRL+s*** (=save) followed by ***CTRL+x*** (=exit).

```bash
ubuntu@aws-linux-ess:~$ nano PublicIP
...  <typ the IP address> ... CTRL+s ...  CTRL+x
ubuntu@aws-linux-ess:~$ cat PublicIP
54.87.203.25
```

