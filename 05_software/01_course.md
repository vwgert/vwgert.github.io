# Software and packages

In Windows we have several options to install software. We usually use installers that we find on discs and websites or even the Windows app store where we can find software in an online catalog. 

Remember that latest hyped video game that you preordered and turned out to be a total bust? When installing that game it might prompt you saying/asking that you need to install the lastest version of DirectX or Visual C++ Redistributable? These are other pieces of software that are needed to run the initial application or game. We call these pieces of software **dependencies**. Most of the times the original installer installs these for us but sometimes we have to manually find and install these dependencies ourselves.

Installing software on Linux systems hasn't always been easy. Back in the days we had to download source code and compile applications ourselves, put them in the right folders and make sure we have all the needed dependencies to run the application.  We might come across this process in the present day, but most of the time we are gonna install software using _**package managers**_. These are tools that run through a database to find the application that we want to install. If it finds an application matching the specified name it will install the application as well as all the required dependencies. If we remove an application it will also remove all dependencies that are no longer required. Another benefit is that the package manager will also manage updates of all our applications and dependencies.

## installing, removing and updating software (apt)

When installing software packages in Ubuntu we often use the `apt` (advanced package system) command. The manpage gives us all the info we need to use the command:
```bash
student@linux-ess:~$ man apt
APT(8)                                                   APT                                                   APT(8)

NAME
       apt - command-line interface

SYNOPSIS
       apt [-h] [-o=config_string] [-c=config_file] [-t=target_release] [-a=architecture] {list | search | show |
           update | install pkg [{=pkg_version_number | /target_release}]...  | remove pkg...  | upgrade |
           full-upgrade | edit-sources | {-v | --version} | {-h | --help}}

DESCRIPTION
       apt provides a high-level commandline interface for the package management system. It is intended as an end
       user interface and enables some options better suited for interactive usage by default compared to more
       specialized APT tools like apt-get(8) and apt-cache(8).
```

As described above `apt` (or it's predecessor `apt-get`) is a package manager. We can use this tool to install packages (read: software) on our Linux machine. Note that `apt` is the specific package manager for Ubuntu. There are several alternatives available such as `pacman`, `rpm`, `yum`, `dnf`, ... which might come pre-installed with a specific linux distribution.

### Repositories
An important thing to note about `apt` is that it uses a database of available packages. We can update this list of packages by running the command below:
```bash
student@linux-ess:~/globbing$ sudo apt update
[sudo] password for student:
Get:1 http://security.ubuntu.com/ubuntu focal-security InRelease [114 kB]
Hit:2 http://archive.ubuntu.com/ubuntu focal InRelease
Get:3 http://archive.ubuntu.com/ubuntu focal-updates InRelease [114 kB]
Get:4 http://security.ubuntu.com/ubuntu focal-security/main amd64 Packages [1490 kB]
Get:5 http://security.ubuntu.com/ubuntu focal-security/main Translation-en [257 kB]
Get:6 http://security.ubuntu.com/ubuntu focal-security/main amd64 c-n-f Metadata [10.4 kB]
Get:7 http://security.ubuntu.com/ubuntu focal-security/restricted amd64 Packages [948 kB]
Get:8 http://security.ubuntu.com/ubuntu focal-security/restricted Translation-en [135 kB]
Get:9 http://security.ubuntu.com/ubuntu focal-security/restricted amd64 c-n-f Metadata [520 B]
Get:10 http://security.ubuntu.com/ubuntu focal-security/universe amd64 Packages [705 kB]
Get:11 http://security.ubuntu.com/ubuntu focal-security/universe Translation-en [126 kB]
Get:12 http://security.ubuntu.com/ubuntu focal-security/universe amd64 c-n-f Metadata [14.5 kB]
...
Get:28 http://archive.ubuntu.com/ubuntu focal-updates/multiverse amd64 c-n-f Metadata [596 B]
Get:29 http://archive.ubuntu.com/ubuntu focal-backports/main amd64 Packages [44.5 kB]
Get:30 http://archive.ubuntu.com/ubuntu focal-backports/main Translation-en [10.9 kB]
Get:31 http://archive.ubuntu.com/ubuntu focal-backports/main amd64 c-n-f Metadata [980 B]
Get:32 http://archive.ubuntu.com/ubuntu focal-backports/universe amd64 Packages [23.8 kB]
Get:33 http://archive.ubuntu.com/ubuntu focal-backports/universe Translation-en [15.9 kB]
Get:34 http://archive.ubuntu.com/ubuntu focal-backports/universe amd64 c-n-f Metadata [860 B]
Fetched 8672 kB in 2s (3651 kB/s)
```
?> <i class="fa-solid fa-circle-info"></i> Note that we used the `sudo` command. This is needed because `apt` is a system wide command that impacts the entire system (installing/removing/updating software). Therefore we cannot run it as a user with default permissions.

We can see that this command gets data from a bunch of lists. These lists are called _**repositories**_ (lists with a collection of packages for certain purposes). When we install software later, it will use the database based on these repositories to check if the package that we want to install is available and which is the latest version.



The list of repositories that `apt` uses can be found in the file `/etc/apt/sources.list` or `/etc/apt/sources.list.d/...`  . We can manually add more repositories to this file or use the command `add-apt-repository` but we will not go into this for now.



Below is the contents of the file */etc/apt/sources.list.d/ubuntu.sources*

```
Types: deb
URIs: http://be.archive.ubuntu.com/ubuntu/
Suites: noble noble-updates noble-backports
Components: main restricted universe multiverse
Signed-By: /usr/share/keyrings/ubuntu-archive-keyring.gpg

Types: deb
URIs: http://security.ubuntu.com/ubuntu/
Suites: noble-security
Components: main restricted universe multiverse
Signed-By: /usr/share/keyrings/ubuntu-archive-keyring.gpg
```



Below you can see the repositories that are cached (=downloaded) on the server after *sudo apt update*

```
student@ubserv:~$ ls /var/lib/apt/lists/
auxfiles                                                                                     be.archive.ubuntu.com_ubuntu_dists_noble-updates_main_i18n_Translation-en
be.archive.ubuntu.com_ubuntu_dists_noble-backports_InRelease                                 be.archive.ubuntu.com_ubuntu_dists_noble-updates_multiverse_binary-amd64_Packages
be.archive.ubuntu.com_ubuntu_dists_noble-backports_main_cnf_Commands-amd64                   be.archive.ubuntu.com_ubuntu_dists_noble-updates_multiverse_cnf_Commands-amd64
be.archive.ubuntu.com_ubuntu_dists_noble-backports_main_dep11_Components-amd64.yml.gz        be.archive.ubuntu.com_ubuntu_dists_noble-updates_multiverse_dep11_Components-amd64.yml.gz
be.archive.ubuntu.com_ubuntu_dists_noble-backports_multiverse_cnf_Commands-amd64             be.archive.ubuntu.com_ubuntu_dists_noble-updates_multiverse_i18n_Translation-en
be.archive.ubuntu.com_ubuntu_dists_noble-backports_multiverse_dep11_Components-amd64.yml.gz  be.archive.ubuntu.com_ubuntu_dists_noble-updates_restricted_binary-amd64_Packages
be.archive.ubuntu.com_ubuntu_dists_noble-backports_restricted_cnf_Commands-amd64             be.archive.ubuntu.com_ubuntu_dists_noble-updates_restricted_cnf_Commands-amd64
be.archive.ubuntu.com_ubuntu_dists_noble-backports_restricted_dep11_Components-amd64.yml.gz  be.archive.ubuntu.com_ubuntu_dists_noble-updates_restricted_dep11_Components-amd64.yml.gz
be.archive.ubuntu.com_ubuntu_dists_noble-backports_universe_binary-amd64_Packages            be.archive.ubuntu.com_ubuntu_dists_noble-updates_restricted_i18n_Translation-en
be.archive.ubuntu.com_ubuntu_dists_noble-backports_universe_cnf_Commands-amd64               be.archive.ubuntu.com_ubuntu_dists_noble-updates_universe_binary-amd64_Packages
be.archive.ubuntu.com_ubuntu_dists_noble-backports_universe_dep11_Components-amd64.yml.gz    be.archive.ubuntu.com_ubuntu_dists_noble-updates_universe_cnf_Commands-amd64
be.archive.ubuntu.com_ubuntu_dists_noble-backports_universe_i18n_Translation-en              be.archive.ubuntu.com_ubuntu_dists_noble-updates_universe_dep11_Components-amd64.yml.gz
be.archive.ubuntu.com_ubuntu_dists_noble_InRelease                                           be.archive.ubuntu.com_ubuntu_dists_noble-updates_universe_i18n_Translation-en
be.archive.ubuntu.com_ubuntu_dists_noble_main_binary-amd64_Packages                          
lock
be.archive.ubuntu.com_ubuntu_dists_noble_main_cnf_Commands-amd64                             
partial
be.archive.ubuntu.com_ubuntu_dists_noble_main_dep11_Components-amd64.yml.gz                  security.ubuntu.com_ubuntu_dists_noble-security_InRelease
be.archive.ubuntu.com_ubuntu_dists_noble_main_i18n_Translation-en                            security.ubuntu.com_ubuntu_dists_noble-security_main_binary-amd64_Packages
be.archive.ubuntu.com_ubuntu_dists_noble_multiverse_binary-amd64_Packages                    security.ubuntu.com_ubuntu_dists_noble-security_main_cnf_Commands-amd64
be.archive.ubuntu.com_ubuntu_dists_noble_multiverse_cnf_Commands-amd64                       security.ubuntu.com_ubuntu_dists_noble-security_main_dep11_Components-amd64.yml.gz
be.archive.ubuntu.com_ubuntu_dists_noble_multiverse_dep11_Components-amd64.yml.gz            security.ubuntu.com_ubuntu_dists_noble-security_main_i18n_Translation-en
be.archive.ubuntu.com_ubuntu_dists_noble_multiverse_i18n_Translation-en                      security.ubuntu.com_ubuntu_dists_noble-security_multiverse_binary-amd64_Packages
be.archive.ubuntu.com_ubuntu_dists_noble_restricted_binary-amd64_Packages                    security.ubuntu.com_ubuntu_dists_noble-security_multiverse_cnf_Commands-amd64
be.archive.ubuntu.com_ubuntu_dists_noble_restricted_cnf_Commands-amd64                       security.ubuntu.com_ubuntu_dists_noble-security_multiverse_dep11_Components-amd64.yml.gz
be.archive.ubuntu.com_ubuntu_dists_noble_restricted_i18n_Translation-en                      security.ubuntu.com_ubuntu_dists_noble-security_multiverse_i18n_Translation-en
be.archive.ubuntu.com_ubuntu_dists_noble_universe_binary-amd64_Packages                      security.ubuntu.com_ubuntu_dists_noble-security_restricted_binary-amd64_Packages
be.archive.ubuntu.com_ubuntu_dists_noble_universe_cnf_Commands-amd64                         security.ubuntu.com_ubuntu_dists_noble-security_restricted_cnf_Commands-amd64
be.archive.ubuntu.com_ubuntu_dists_noble_universe_dep11_Components-amd64.yml.gz              security.ubuntu.com_ubuntu_dists_noble-security_restricted_dep11_Components-amd64.yml.gz
be.archive.ubuntu.com_ubuntu_dists_noble_universe_i18n_Translation-en                        security.ubuntu.com_ubuntu_dists_noble-security_restricted_i18n_Translation-en
be.archive.ubuntu.com_ubuntu_dists_noble-updates_InRelease                                   security.ubuntu.com_ubuntu_dists_noble-security_universe_binary-amd64_Packages
be.archive.ubuntu.com_ubuntu_dists_noble-updates_main_binary-amd64_Packages                  security.ubuntu.com_ubuntu_dists_noble-security_universe_cnf_Commands-amd64
be.archive.ubuntu.com_ubuntu_dists_noble-updates_main_cnf_Commands-amd64                     security.ubuntu.com_ubuntu_dists_noble-security_universe_dep11_Components-amd64.yml.gz
be.archive.ubuntu.com_ubuntu_dists_noble-updates_main_dep11_Components-amd64.yml.gz          security.ubuntu.com_ubuntu_dists_noble-security_universe_i18n_Translation-en
```



Below is the data for the package "zip", found in one of the above files.

```
Package: zip
Architecture: amd64
Version: 3.0-13build1
Multi-Arch: foreign
Priority: optional
Section: utils
Origin: Ubuntu
Maintainer: Ubuntu Developers <ubuntu-devel-discuss@lists.ubuntu.com>
Original-Maintainer: Santiago Vila <sanvila@debian.org>
Bugs: https://bugs.launchpad.net/ubuntu/+filebug
Installed-Size: 536
Depends: libbz2-1.0, libc6 (>= 2.34)
Recommends: unzip
Filename: pool/main/z/zip/zip_3.0-13build1_amd64.deb
Size: 175418
MD5sum: 31b4161417c3ba2f6c02c17d4775543c
SHA1: 6b19302c15eab7c8fd7a6fcc3fab3664c74c878b
SHA256: 5c1a2dfb052f50e7031037aa2e267839804d2254c4d282040fdfe826ffba1e38
SHA512: 6e18366ade8761f3a86c53a3ccaa40d6e5959886266138a4c638b10783444c1f26cda774b4753b7c7721e8666c42c74c0e2b06e45f82e94e7132037979c6efa3
Homepage: https://infozip.sourceforge.net/Zip.html
Description: Archiver for .zip files
Task: ubuntu-desktop-minimal, ubuntu-desktop, ubuntu-desktop-raspi, kubuntu-desktop, xubuntu-minimal, xubuntu-desktop, lubuntu-desktop, ubuntustudio-desktop-core, ubuntustudio-desktop, ubuntukylin-desktop, ubuntukylin-desktop-minimal, ubuntu-mate-core, ubuntu-mate-desktop, ubuntu-budgie-desktop-minimal, ubuntu-budgie-desktop, ubuntu-budgie-desktop-raspi, ubuntu-unity-desktop, edubuntu-desktop-gnome-minimal, edubuntu-desktop-gnome-raspi, ubuntucinnamon-desktop-minimal, ubuntucinnamon-desktop-raspi
Description-md5: 581928d34d669e63c353cd694bd040b0
```



You can see the information shown above with the command *apt show zip*



### Finding software (apt search) 
Imagine that we downloaded a file that ends with `.zip` and we have to find a program that can deal with this kind of file. We could use the following command, making use of a regular expression in the search term: 
```bash
student@linux-ess:~$ apt search "\.zip file"       # \.  to make clear that we are searching for a dot
Sorting... Done
Full Text Search... Done
goldendict/jammy 1.5.0~rc2+git20210630+ds-2 amd64
  feature-rich dictionary lookup program

node-jszip/jammy 3.7.1+dfsg-1 all
  Create, read and edit .zip files with Javascript

node-jszip-utils/jammy 0.1.0+dfsg-1 all
  collection of cross-browser utilities to go along with JSZip

unicode-cldr-core/jammy 32.0.1-1.1 all
  Common data from Unicode CLDR (core)

unzip/jammy-updates,jammy-security 6.0-26ubuntu3.1 amd64
  De-archiver for .zip files

zip/jammy 3.0-12build2 amd64
  Archiver for .zip files

student@linux-ess:~$
```
The last entry in the list shows us a package that can archive .zip files. The procedure to find it was as follows: 

* It searches all repositories that we have downloaded from the Internet (/etc/apt/sources.list) to find a package that meets the search term. 
* Packages are found, like the `zip`-package or `unzip`-package. 

?> <i class="fa-solid fa-circle-info"></i> Mind that it's best practice to do an `apt update` to download the latest versions of the repositories, right before you search for a package. This way you will find all available packages and latest version of every package.

### Installing software (apt install)
Imagine we would like to install the `zip` package. We could simply run the command below:
```bash
student@linux-ess:~$ sudo apt install zip
Reading package lists... Done
Building dependency tree... Done
Reading state information... Done
The following additional packages will be installed:
  unzip
The following NEW packages will be installed:
  unzip zip
0 upgraded, 2 newly installed, 0 to remove and 175 not upgraded.
Need to get 336 kB of archives.
After this operation, 1231 kB of additional disk space will be used.
Do you want to continue? [Y/n] y
Get:1 http://archive.ubuntu.com/ubuntu jammy/main amd64 unzip amd64 6.0-25ubuntu1 [169 kB]
Get:2 http://archive.ubuntu.com/ubuntu jammy/main amd64 zip amd64 3.0-11build1 [167 kB]
Fetched 336 kB in 1s (444 kB/s)
Selecting previously unselected package unzip.
(Reading database ... 32259 files and directories currently installed.)
Preparing to unpack .../unzip_6.0-25ubuntu1_amd64.deb ...
Unpacking unzip (6.0-25ubuntu1) ...
Selecting previously unselected package zip.
Preparing to unpack .../zip_3.0-11build1_amd64.deb ...
Unpacking zip (3.0-11build1) ...
Setting up unzip (6.0-25ubuntu1) ...
Setting up zip (3.0-11build1) ...
Processing triggers for man-db (2.9.1-1) ...
```
If we analyse the output of the command we can see a couple of things happening:

* It reads the package list to find the `zip` package. After this is done it builds a dependency tree to see what dependencies the `zip` package needs.
* It points out that it will install an additional package called `unzip`. This is a dependency of the `zip` command.
* It points out what new packages will be installed and if any packages will be updated.
* It asks for a confirmation if we are sure we want to continue. After this confirmation it will install / update all the packages mentioned in the output above.

?> <i class="fa-solid fa-circle-info"></i> You might notice that you can use both the `apt` and `apt-get` command.  Both commands are very similar (with minor differences, but we won't get into that now).

After running the command above, we can succesfully use the `zip` command:
```bash
student@linux-ess:~$ zip
Copyright (c) 1990-2008 Info-ZIP - Type 'zip "-L"' for software license.
Zip 3.0 (July 5th 2008). Usage:
zip [-options] [-b path] [-t mmddyyyy] [-n suffixes] [zipfile list] [-xi list]
  The default action is to add or replace zipfile entries from list, which
  can include the special name - to compress standard input.
  If zipfile and list are omitted, zip compresses stdin to stdout.
```
?> <i class="fa-solid fa-circle-info"></i> You might wonder where the `zip` executable is located and how the shell knows how to run that exact executable. We can check this by running the `which zip` command. This will tell us that, when we run the `zip` command it will actually run the `zip` binary (=executable) located at `/usr/bin/zip`. `/usr/bin` is one of the folders where binaries (=executable files) are stored. You could compare this to the folder `c:\program files` in Windows systems. Linux has multiple places where binaries are stored. These are often bundled in the `$PATH` variable which we will learn to use in a later chapter. 

Imagine we made a typo in our command and try to install a package that doesn't exist:
```bash
student@linux-ess:~$ sudo apt install zap
Reading package lists... Done
Building dependency tree
Reading state information... Done
E: Unable to locate package zap
```
The output indicates that it cannot locate the package `zap`. This means that it checked all its repositories for a package with the name `zap` but it could not be found. If the package does exists we would have to add the repository containing the package and run `sudo apt update`.

### Removing software (apt remove)
To remove software we can simply use the command below:

```bash
student@linux-ess:~$ sudo apt remove zip
Reading package lists... Done
Building dependency tree... Done
Reading state information... Done
The following package was automatically installed and is no longer required:
  unzip
Use 'sudo apt autoremove' to remove it.
The following packages will be REMOVED:
  zip
0 upgraded, 0 newly installed, 1 to remove and 175 not upgraded.
After this operation, 638 kB disk space will be freed.
Do you want to continue? [Y/n] y
(Reading database ... 32291 files and directories currently installed.)
Removing zip (3.0-11build1) ...
Processing triggers for man-db (2.9.1-1) ...
```
 Notice how it doesn't automatically remove the dependencies we talked about earlier. This is because there might be other packages that require this dependency. We can use the `sudo apt autoremove` command to remove unused dependencies.

 We also have a somewhat more agressive command to remove packages: `sudo apt purge <packagename>`. The difference between `remove` and `purge` is that when using `purge` it will remove any config files linked to that application as well. When using `remove` those config files will stay on the system.

?> <i class="fa-solid fa-circle-info"></i> To get a list of all possible software packages we can use `apt list`. To get a list of installed software packages we can use `apt list --installed`. Warning: this list can be very very long!

### Updating software (apt upgrade)
For updating our software we have a couple of options. To start of we can individually update certain packages by simply using the `sudo apt install <packagename>` command. When you use this command with a package that has already been installed, it will try to update it to the latest version.

?> Mind that before updating or even installing software you might want to update your database by running `sudo apt update` so you are certain we use the latest and correct repositories. *This might also be confusing at first because the `update` command doesn't actually update packages!*

When we want to update all the packages on our system we can use the `sudo apt upgrade` command. This will update all the installed packages.

## gzip and tar

### gzip

If we compress a file, we keep the content, but the filesize will become smaller.  We can compress a file with gzip.

```bash
student@ubuntu-server:~$ cd
student@ubuntu-server:~$ cp /var/lib/apt/lists/be.archive.ubuntu.com_ubuntu_dists_jammy_universe_binary-amd64_Packages .
student@ubuntu-server:~$ ls -lh be.archive*
-rw-r--r-- 1 student student 62M Oct 10 19:40 be.archive.ubuntu.com_ubuntu_dists_jammy_universe_binary-amd64_Packages
student@ubuntu-server:~$ gzip be.archive.ubuntu.com_ubuntu_dists_jammy_universe_binary-amd64_Packages
student@ubuntu-server:~$ ls -lh be.archive*
-rw-r--r-- 1 student student 17M Oct 10 19:40 be.archive.ubuntu.com_ubuntu_dists_jammy_universe_binary-amd64_Packages.gz
```

The file has an extension of gz and  is a lot smaller now, but you cannot see its contents. The original file is gone and we only have the compressed file now.


### gunzip

If we want to decompress the file we can use gunzip.
```bash
student@ubuntu-server:~$ ls -lh be.archive*
-rw-r--r-- 1 student student 17M Oct 10 19:40 be.archive.ubuntu.com_ubuntu_dists_jammy_universe_binary-amd64_Packages.gz
student@ubuntu-server:~$ gunzip be.archive.ubuntu.com_ubuntu_dists_jammy_universe_binary-amd64_Packages.gz
student@ubuntu-server:~$ ls -lh be.archive*
-rw-r--r-- 1 student student 62M Oct 10 19:40 be.archive.ubuntu.com_ubuntu_dists_jammy_universe_binary-amd64_Packages
```

The file regained its original size and the content can be viewed/edited again. The zipped file is gone again and we only have the original file.


### tar

If we want to put multiple files and folders together in one file, we can use tar. We use the option -c to create the tarfile.

```bash
student@ubuntu-server:~$ tree
.
├── Downloads
│   ├── logo.png
│   └── Steam
│       └── games
│           └── pacman
├── emptyfile
student@ubuntu-server:~$ tar -cf Downloads.tar Downloads # create tar
student@ubuntu-server:~$ tar -tf Downloads.tar # view contents of tar
Downloads/
Downloads/logo.png
Downloads/Steam/
Downloads/Steam/games/
Downloads/Steam/games/pacman
```

### tarball

We can also zip the tar file when we create it.

```bash
student@ubuntu-server:~$ tree
.
├── Downloads
│   ├── logo.png
│   └── Steam
│       └── games
│           └── pacman
├── emptyfile
student@ubuntu-server:~$ tar -czf Downloads.tar.gz  Downloads # create tarball 
student@ubuntu-server:~$ tar -tzf Downloads.tar.gz # view contents of tarball
Downloads/
Downloads/logo.png
Downloads/Steam/
Downloads/Steam/games/
Downloads/Steam/games/pacman
```


### Extract a tar

We can extract a tarfile (.tar) or tarball (.tar.gz).

```bash
student@ubuntu-server:~$ tree
.
├── Downloads
│   ├── logo.png
│   └── Steam
│       └── games
│           └── pacman
├── Downloads.tar
├── Downloads.tar.gz
├── emptyfile

student@ubuntu-server:~$ mkdir backup
student@ubuntu-server:~$ tar -xzf Downloads.tar.gz  -C backup      # zipped tarball
student@ubuntu-server:~$ tar -xf Downloads.tar -C /tmp             # tarfile
student@ubuntu-server:~$ tree
.
├── backup
│   └── Downloads
│       ├── logo.png
│       └── Steam
│           └── games
│               └── pacman

...

student@ubuntu-server:~$ tree /tmp/Downloads/
/tmp/Downloads/
├── logo.png
└── Steam
    └── games
        └── pacman

2 directories, 2 files

```

![tar](../images/05/tar.png)   

### Installing packages via a tarball

Sometimes you might encounter a `tar` or `tar.gz` file for installing some software. A  `tar.gz` file is also known as a `tarball`. it's a compressed file containing all kinds of files & folders. You can compare these to `zip` or `rar` files. We need to extract the files/folders inside this file before we can use them. To do so we can use the `tar` command. The options we use will vary depending on the case. Do we want to extract a `tar` file or a `tar.gz`file:
```bash
student@linux-ess:~/tarexample$ ls
app.tar.gz  docs.tar
student@linux-ess:~/tarexample$ tar -xf docs.tar
student@linux-ess:~/tarexample$ mkdir app
student@linux-ess:~/tarexample$ tar -xzf app.tar.gz -C ./app
student@linux-ess:~/tarexample$ ls
app  app.tar.gz  docs  docs.tar
```
The options we use can be found in the manpage, but below you can find a small summary of the most important ones: 

* `-x`: Stands for extract, this will unpack all the contents of the file.
* `-f`: Stands for file. This uses the argument after the options as the path of the archive we want to extract.
* `-z`: This makes sure we run the file through `gzip`, another archive tool. The extention `tar.gz` hints that it is processed through `gzip`.
* `-C`: This changes the directory before extracting to the path supplied as an argument. This means the contents will be extracted in this folder.
* `-t`: Will only list the contents of the archive to the screen. It will not unpack anything.
  
  
## dpkg

`dpkg` was the first package manager for Debian-based systems. Where Ubuntu nowadays uses `apt` as the default package manager, we can also use `dpkg`. `dpkg` was the predecessor of `apt-get` and `apt`. `dpkg` doesn't make use of repositories, so we have to have the installer file before using the command. It also doesn't download dependencies automatically. That's why they used to call it *the dependancy hell*  We can use `dpkg` to install / remove / ... `.deb` files. The example below installs the package `yourpackage`:
```bash
student@linux-ess:~$ sudo dpkg -i yourpackage.deb
```

`dpkg` can also be used to (re)configure particular packages. We can use this for example to change the keyboard layout on our server by running:
```bash
student@linux-ess:~$ sudo dpkg-reconfigure keyboard-configuration
```


## snap

One of the relative new players is snap. A snap is a bundle of the software we want to install with all of its dependencies stored in one file and executed in its own bubble. This means that two snaps cannot interfere with eachother. This for example makes it possible to install two different versions of the same software at the same time and running them together. Snaps have their own filesystem but can work with files on your systems too. You can find snaps in the snap store on a Desktop or with `snap search` on a server. Snaps are used more and more because they are distro independant. If you can install the snap daemon on the distro it will run all snaps. 

The commands for working with snap are almost similar as apt. We have:  
```bash
snap search  
snap list (installed apps)  
snap list --all (shows all the installed versions)  
snap revert <snapname> --revision <revnumber> (go back to a previous version of the snap)  
snap info   
snap install  
snap remove   
snap refresh (upgrades the snaps, happens every day automatically)     
snap changes (history of changes)  
snap version 
```


snap update does not exist. The snap daemon checks for updates 4 times a day.

You can install from different channels (like stable, beta,...) but the standard is stable and we keep it that way.

```bash
student@linux-ess:~$ snap search mapscii
Name     Version  Publisher  Notes  Summary
mapscii  0.3.1    nhaines    -      The whole world in your console.
student@linux-ess:~$ snap info mapscii
name:      mapscii
summary:   The whole world in your console.
publisher: Nathan Haines (nhaines)
store-url: https://snapcraft.io/mapscii
contact:   https://github.com/nathanhaines/mapscii
license:   MIT
description: |
  A node.js based Vector Tile to Braille and ASCII renderer for
  xterm-compatible terminals.
snap-id: YmktiCRE0Dg3FvsSwXiNFHeygSzRtyIo
channels:
  latest/stable:    0.3.1 2020-08-12 (14) 29MB -
  latest/candidate: ↑
  latest/beta:      ↑
  latest/edge:      0.3.1 2020-08-15 (14) 29MB -
student@linux-ess:~$ sudo snap install mapscii
[sudo] password for student:
mapscii 0.3.1 from Nathan Haines (nhaines) installed
student@linux-ess:~$ mapscii 
```
![mapscii](../images/05/mapscii.png)   

?> To navigate and zoom you can use the *arrow keys* and *a* and *z* 


## zip vs gzip
`gzip` compresses only one file and therefore is used with `tar` which brings multiple files into one file.  
`zip`is used when you want to compress a bunch of files into one file in one step. 

```bash
student@linux-ess:~$ ls -a
.   ..   .bash_history   .bash_logout   .bashrc   .profile   .ssh
student@linux-ess:~$ zip myzipfile.zip .bashrc .profile
  adding: .bashrc (deflated 54%)
  adding: .profile (deflated 51%)
student@linux-ess:~$ ls -l
total 2440
-rw-rw-r-- 1 student student    2440 Oct 14 15:00 myzipfile.zip
student@linux-ess:~$ unzip -l myzipfile.zip     # only list the files 
Archive:  myzipfile.zip
  Length      Date    Time    Name
---------  ---------- -----   ----
     3771  2022-01-06 16:23   .bashrc
      807  2022-01-06 16:23   .profile
---------                     -------
     4578                     2 files
student@linux-ess:~$ rm .bashrc .profile
student@linux-ess:~$ ls -a
.   ..   .bash_history   .bash_logout   .ssh
student@linux-ess:~$ unzip myzipfile.zip
Archive:  myzipfile.zip
  inflating: .bashrc
  inflating: .profile
student@linux-ess:~$ ls -a
.   ..   .bash_history   .bash_logout   .bashrc   .profile   .ssh  
```

So why do we use `tar` and `gzip` if we can use `zip` instead? This is because `tar` will also keep the ownerships and the rights on each file. We will compare the two with an example (if you don't really understand the ownership in the example, mind that it will be explained in a later lesson):  

```bash
student@linux-ess:~$ ls -lh .bashrc
-rw-r--r-- 1 student student 3.7K Jan  6  2022 .bashrc        # mind the owner student
student@linux-ess:~$ zip zipdemo.zip .bashrc
  adding: .bashrc (deflated 54%)
student@linux-ess:~$ tar -czf tardemo.tgz .bashrc
student@ulinux-ess:~$ ls -lh zipdemo.zip tardemo.tgz
-rw-rw-r-- 1 student student 1.9K Oct 14 15:21 tardemo.tgz
-rw-rw-r-- 1 student student 1.9K Oct 14 15:19 zipdemo.zip 
student@ulinux-ess:~$ cp zipdemo.zip tardemo.tgz /tmp
student@ulinux-ess:~$ cd /tmp
student@ulinux-ess:/tmp$ sudo unzip zipdemo.zip              # sudo -> do as root user  -> just to demo the rights
student@ulinux-ess:/tmp$ ls -lh .bashrc
-rw-r--r-- 1 root root 3.7K Jan  6  2022 .bashrc             # root is the owner because he created the files with unzipping the zipfile
student@ulinux-ess:/tmp$ sudo rm .bashrc
student@ulinux-ess:/tmp$ sudo tar -xzf tardemo.tgz            # sudo -> do as root user  -> just to demo the rights
student@ulinux-ess:/tmp$ ls -lh .bashrc
-rw-r--r-- 1 student student 3.7K Jan  6  2022 .bashrc       # student is still the owner even though the files are created by root (sudo) while untarring
```
