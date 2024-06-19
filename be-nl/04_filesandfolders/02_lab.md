# Lab <!-- {docsify-ignore} --> 


touch file .ToDo

nano .ToDo  --> ssh keys backuppen  &  extern ip in file in homefolder



find locate van ssh-key

file commando om te zien wat voor file dit is

cat om te bekijken

cp om te backuppen naar map met spaties in de naam

rename van backup mapje om spatie eruit te halen

Nog een hoofdmapje en backup mapje hiernaar verplaatsen



rm .ToDo







Dit nog in vorig lab

======================================================================================================================

whoami

```bash
ubuntu@linux-ess:~$ whoami
ubuntu
```



groups

```bash
ubuntu@linux-ess:~$ groups
ubuntu adm cdrom sudo dip lxd
```





pwd

```bash
ubuntu@linux-ess:~$ pwd
/home/ubuntu
```



ls

```bash
ubuntu@linux-ess:~$ ls
ubuntu@linux-ess:~$ 
```



ls -a

```bash
ubuntu@linux-ess:~$ ls -a
.   .bash_history  .bashrc  .config   .local    .ssh
..  .bash_logout   .cache   .lesshst  .profile  .sudo_as_admin_successful
```



lscpu

```bash
ubuntu@linux-ess:~$ lscpu
Architecture:             x86_64
  CPU op-mode(s):         32-bit, 64-bit
  Address sizes:          46 bits physical, 48 bits virtual
  Byte Order:             Little Endian
CPU(s):                   2
  On-line CPU(s) list:    0,1
Vendor ID:                GenuineIntel
  Model name:             Intel(R) Xeon(R) CPU E5-2676 v3 @ 2.40GHz
    CPU family:           6
    Model:                63
    Thread(s) per core:   1
    Core(s) per socket:   2
    Socket(s):            1
```



free -h

```bash
ubuntu@linux-ess:~$ free -h
               total        used        free      shared  buff/cache   available
Mem:           3.8Gi       438Mi       3.2Gi       880Ki       447Mi       3.4Gi
Swap:             0B          0B          0B
```



df -h

```bash
ubuntu@linux-ess:~$ df -h
Filesystem      Size  Used Avail Use% Mounted on
/dev/root       6.8G  2.2G  4.6G  33% /
tmpfs           2.0G     0  2.0G   0% /dev/shm
tmpfs           783M  864K  782M   1% /run
tmpfs           5.0M     0  5.0M   0% /run/lock
/dev/xvda16     881M  133M  687M  17% /boot
/dev/xvda15     105M  6.1M   99M   6% /boot/efi
tmpfs           392M   12K  392M   1% /run/user/1000
```



lsblk -e7

```bash
ubuntu@linux-ess:~$ lsblk -e7
NAME     MAJ:MIN RM  SIZE RO TYPE MOUNTPOINTS
xvda     202:0    0    8G  0 disk
├─xvda1  202:1    0    7G  0 part /
├─xvda14 202:14   0    4M  0 part
├─xvda15 202:15   0  106M  0 part /boot/efi
└─xvda16 259:0    0  913M  0 part /boot
```

ip a

```bash
ubuntu@linux-ess:~$ ip a
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1000
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 scope host lo
       valid_lft forever preferred_lft forever
    inet6 ::1/128 scope host noprefixroute
       valid_lft forever preferred_lft forever
2: enX0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 9001 qdisc mq state UP group default qlen 1000
    link/ether 06:75:d5:9f:d8:b3 brd ff:ff:ff:ff:ff:ff
    inet 172.31.63.234/20 metric 100 brd 172.31.63.255 scope global dynamic enX0
       valid_lft 2866sec preferred_lft 2866sec
    inet6 fe80::475:d5ff:fe9f:d8b3/64 scope link
       valid_lft forever preferred_lft forever
```

curl checkip.amazonaws.com

```bash
ubuntu@linux-ess:~$ curl checkip.amazonaws.com
54.87.203.25
```



systemctl status ssh --no-pager

```bash
ubuntu@linux-ess:~$ systemctl status ssh --no-pager
● ssh.service - OpenBSD Secure Shell server
     Loaded: loaded (/usr/lib/systemd/system/ssh.service; disabled; preset: enabled)
    Drop-In: /usr/lib/systemd/system/ssh.service.d
             └─ec2-instance-connect.conf
     Active: active (running) since Wed 2024-06-19 06:34:04 UTC; 56min ago
TriggeredBy: ● ssh.socket
       Docs: man:sshd(8)
             man:sshd_config(5)
   Main PID: 899 (sshd)
      Tasks: 1 (limit: 4676)
     Memory: 4.1M (peak: 4.6M)
        CPU: 45ms
     CGroup: /system.slice/ssh.service
             └─899 "sshd: /usr/sbin/sshd -D -o AuthorizedKeysCommand /usr/share/ec2-instance-connect/eic_run_authorized…

Jun 19 06:34:04 linux-ess systemd[1]: Starting ssh.service - OpenBSD Secure Shell server...
Jun 19 06:34:04 linux-ess sshd[899]: Server listening on :: port 22.
Jun 19 06:34:04 linux-ess systemd[1]: Started ssh.service - OpenBSD Secure Shell server.
Jun 19 06:34:05 linux-ess sshd[900]: Accepted publickey for ubuntu from 84.195.122.178 port 57085 ssh2: ED25519…LE3PFz3E
Jun 19 06:34:05 linux-ess sshd[900]: pam_unix(sshd:session): session opened for user ubuntu(uid=1000) by ubuntu(uid=0)
Hint: Some lines were ellipsized, use -l to show in full.
```



ss -ltn

```bash
ubuntu@linux-ess:~$ ss -ltn
State         Recv-Q        Send-Q               Local Address:Port               Peer Address:Port       Process
LISTEN        0             4096                    127.0.0.54:53                      0.0.0.0:*
LISTEN        0             4096                 127.0.0.53%lo:53                      0.0.0.0:*
LISTEN        0             4096                             *:22                            *:*
```



=========================================================================================================================







In een vorig hoofdstuk hebben we een instance (=server) aangemaakt en hebben we ook een ssh-key aangemaakt en gekoppeld aan deze instance. Daardoor lukt het ons om met dit keypair in te loggen onder de gebruiker ubuntu (=standaard gebruiker van de AWS-Ubuntu-image). Linus is nu wel benieuwd waar de public ssh key zich dan wel bevindt op de server. 

## Zoeken van de public ssh key 

Voordat hij iets kan vinden, wil Linus echt weten hoe hij de mappen kan doorzoeken. Hij kwam er al achter dat hij een prompt gebruikt die opdrachten uitvoert in een specifieke map, zoals te zien is in de vorige hoofdstukken. Met behulp van het commando `apropos directory` komt hij erachter dat er allerlei commando's beschikbaar zijn om met mappen te werken. Het eerste commando dat Linus bekijkt is het `pwd` commando: 

```bash
ubuntu@ip-172-31-63-234:~$ apropos find
...
find (1)             - search for files in a directory hierarchy
...
locate (1)           - find files by name, quickly
...
```

Hij zoekt uit hoe hij het commando locate kan gebruiken: 

```bash
student@linux-ess:~$ man locate
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

Dit levert volgend resultaat: 

```bash
ubuntu@ip-172-31-63-234:~$ locate key
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
```

We zien geen output. Dit komt omdat onze thuismap (`/home/student`) standaard leeg lijkt te zijn. Er zijn mogelijks enkele verborgen bestanden die niet worden weergegeven. Met behulp van het `man ls` commando probeert hij te zoeken naar een _optie_ waarmee hij verborgen bestanden kan bekijken: 

```bash
student@linux-ess:~$ man ls
```

Om verborgen bestanden (bestanden die beginnen met een `.` teken) te bekijken, gebruikt hij de optie `-a` als volgt: 
```bash
student@linux-ess:~$ ls -a
.   .bash_history  .bashrc      .ssh
..  .bash_logout   .profile     .sudo_as_admin_successful
student@linux-ess:~$
```
Merk op dat de uitvoer van het commando `ls -a` op jouw systeem anders kan zijn. Het belangrijkste doel is dat we een lijst met verborgen bestanden krijgen (bestanden die beginnen met `.`). Linus wil controleren of deze bestanden (of mappen) daadwerkelijk inhoud bevatten. Om dit te doen, gebruikt hij het commando `man ls` om te zoeken naar opties om bestandsgroottes te bekijken: 
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

Om de bestandsgrootte van het bestand te achterhalen combineert hij de opties `-a`, `-l` en `-h`. Nu weet Linus dat het bestand `.bashrc` bijvoorbeeld 3,5Kb groot is en voor het laatst is gewijzigd op 31 mei om 14:59. 







naar .ssh mapje en file key(s) en keys  catten   en backuppen







## Maak een mappenstructuur  

Linus wil een schone mappenstructuur voor zijn _LinusCraft_-project. In zijn homefolder wil hij graag een map aanmaken met de naam `linuscraft`. Om dit te doen vond hij het `mkdir` commando met behulp van de manpages. 

```bash
student@linux-ess:~$ mkdir linuscraft
```

Na het aanmaken van de map `linuscraft` wil hij een map `playerinfo` in deze map aanmaken. Om dit te doen kan hij een van de 2 onderstaande opties gebruiken: 

1. Door het commando `cd` te gebruiken: 
```bash
student@linux-ess:~$ cd linuscraft
student@linux-ess:~/linuscraft$ mkdir playerinfo
```

2. Door het mkdir commando direct vanuit zijn homefolder (`/home/student`) te gebruiken met behulp van een relatief pad: 
```bash
student@linux-essentials:~$ mkdir linuscraft/playerinfo
```

Hij controleert of de map correct is gemaakt door naar die map te navigeren met behulp van een absoluut pad: 
```bash
student@linux-ess:~/linuscraft$ cd /home/student/linuscraft/playerinfo
student@linux-ess:~/linuscraft/playerinfo$ pwd
/home/student/linuscraft/playerinfo
```

?> Oefening: Kun je naar de map playerinfo navigeren met behulp van een relatief pad dat begint vanuit je homefolder? 

Ook wil hij graag een map `administration` in de map `linuscraft`. Terwijl hij de map `playerinfo` als werkmap gebruikt (`cd /home/student/linuscraft/playerinfo`), maakt hij deze map aan met behulp van een relatief pad: 
```bash
student@linux-ess:~/linuscraft/playerinfo$ mkdir ../administration
```

Om af te sluiten maakt hij de mappen met de naam `backups`, `secrets` en `serverfiles` in de map `linuscraft` met behulp van een absoluut pad: 
```bash
student@linux-ess:~/linuscraft$ mkdir /home/student/linuscraft/backups /home/student/linuscraft/secrets /home/student/linuscraft/serverfiles
```
Merk op hoe we meerdere argumenten kunnen gebruiken met het commando `mkdir` om meerdere mappen te maken met slechts één commando. 

Linus besluit terug te navigeren naar zijn homefolder door het commando `cd` zonder argumenten te gebruiken. Daarna controleert hij de inhoud van zijn aangemaakte map `linuscraft`: 
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

## Bestanden maken  
Linus wil graag een bestand maken, genaamd `todo.txt` om eventuele openstaande taken op te sommen. Hij maakt dit bestand aan in de map `linuscraft` met behulp van het `touch` commando: 

```bash
student@linux-ess:~$ touch linuscraft/todo.txt
```

Met deze opdracht wordt een leeg bestand gemaakt. We zullen ontdekken hoe we gegevens in het bestand kunnen invoegen in het lab van het volgende hoofdstuk. 

Vervolgens maakt hij enkele extra bestanden met het volgende commando: 

```bash
student@linux-ess:~$  touch linuscraft/contact.txt linuscraft/backuplog.txt linus.txt
```
Merk op hoe we meerdere argumenten kunnen geven aan het touch commando om meerdere bestanden te maken met slechts één commando. 

Hij wil een verborgen bestand in de map secrets maken om ook privé-informatie op te slaan met behulp van een absoluut pad: 

```bash
student@linux-ess:~$ touch /home/student/linuscraft/secrets/.private
```
Hij controleert of alle bestanden met succes zijn gemaakt met behulp van de volgende reeks commando's: 
```bash
student@linux-ess:~$ ls ~
linus.txt  linuscraft
student@linux-ess:~$ ls linuscraft/
administration  backuplog.txt  backups  contact.txt  playerinfo  secrets  serverfiles  todo.txt
student@linux-ess:~$ ls -a /home/student/linuscraft/secrets/
.  ..  .private
```

## Verfijn de bestands- en mapstructuur  

Er zijn enkele problemen met de bestanden en mappen die we zojuist hebben gemaakt. Het `linus.txt` bestand wordt bijvoorbeeld aangemaakt in de homefolder van de gebruiker `student`. We moeten dit bestand verplaatsen naar de map `playerinfo`: 

```bash
student@linux-ess:~$ mv linus.txt linuscraft/playerinfo/
```

Er zijn 3 `txt` bestanden aanwezig in de map `linuscraft`. Linus leerde dat in Linux bestanden geen bestandsuitbreidingen nodig hebben, dus hij wil ze verwijderen met slechts één commando. Om dit doel te bereiken, gebruikt hij het commando `rename`: 

```bash
student@linux-ess:~$ cd linuscraft
student@linux-ess:~/linuscraft$ ls
administration  backuplog.txt  backups  contact.txt  playerinfo  secrets  todo.txt
student@linux-ess:~/linuscraft$ rename 's/\.txt//' *.txt
student@linux-ess:~/linuscraft$ ls
administration  backuplog  backups  contact  playerinfo  secrets  todo
```

De map `secrets` en de inhoud ervan zijn niet langer nodig, dus Linus besluit deze te verwijderen terwijl hij `~/linuscraft` als werkmap heeft (`cd ~/linuscraft`): 

```bash
student@linux-ess:~/linuscraft$ rm -rf secrets
```

In het lab van het volgende hoofdstuk zullen we leren hoe we bestandsinhoud kunnen toevoegen aan de bestanden die we zojuist hebben gemaakt.