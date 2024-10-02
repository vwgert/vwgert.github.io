# Lab <!-- {docsify-ignore} --> 




In een vorig hoofdstuk hebben we een cloud instance (=server) aangemaakt en hebben we ook een ssh-key aangemaakt en gekoppeld aan deze instance. Daardoor lukt het ons om met dit keypair in te loggen onder de gebruiker ubuntu (=standaard gebruiker van de AWS-Ubuntu-image). Linus is nu wel benieuwd waar de public ssh key zich dan wel bevindt op de server. 

## Zoeken van de public ssh key 

Voordat hij iets kan vinden, wil Linus weten hoe hij het beste de mappen kan doorzoeken. Met behulp van het commando ***apropos find*** komt hij erachter dat er meerdere commando's beschikbaar zijn om in een mappenstructuur te zoeken. Zo vindt hij de commando's  *find* en *locate*.

```bash
ubuntu@aws-linux-ess:~$ apropos find
...
find (1)             - search for files in a directory hierarchy
...
locate (1)           - find files by name, quickly
...
```

Hij zoekt uit hoe hij het commando *locate* kan gebruiken: 

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

Het zoeken naar bestanden of mappen met het woord key in de naam levert volgend resultaat: 

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

De laatste zichtbare lijn toont hierboven hoe ergens in zijn homefolder een bestand staat genaam *authorized_keys*.



Tevens zoekt Linus uit hoe hij het *find* commando had kunnen gebruiken:

```bash
ubuntu@aws-linux-ess:~$ man find
```



Het zoeken, met *find*, naar bestanden of mappen met het woord key in de naam levert volgend resultaat:  

```bash
ubuntu@aws-linux-ess:~$ find -name "*key*"
./.ssh/authorized_keys
```


Merk op dat de uitvoer van het commando begint met *./*. Dit duidt erop dat *.ssh* zicht bevindt in de huidige map. Dat de map *.ssh* begint met een punt (.) duidt er op dat deze map verborgen is. Het commando ls zal deze map dus niet tonen. We zullen het commando *ls -a* moeten gebruiken, zodanig dat de verborgen bestanden en mappen ook zichtbaar zijn.  

```bash
ubuntu@aws-linux-ess:~$ ls -a
.   .bash_history  .bashrc  .config   .local    .ssh
..  .bash_logout   .cache   .lesshst  .profile  .sudo_as_admin_successful
```

 

Met het commando *file* kan Linus achterhalen welk type file *.ssh* is.

```bash
ubuntu@aws-linux-ess:~$ file .ssh
.ssh: directory
```



Hij verplaatst zich in de map, bekijkt de inhoud en achterhaald welk type file *authorized_keys* is.

```
ubuntu@aws-linux-ess:~$ cd .ssh
ubuntu@aws-linux-ess:~/.ssh$ ls
authorized_keys
ubuntu@aws-linux-ess:~/.ssh$ file authorized_keys
authorized_keys: OpenSSH ED25519 public key
```

Dit is dus de public key die behoort bij de private key die op zijn laptop is gedownload vanuit AWS.



De inhoud bekijken van de file kan met ***cat authorized_keys***

```bash
ubuntu@aws-linux-ess:~/.ssh$ cat authorized_keys
ssh-ed25519 AAAAC3NzaC1lZDI1NTE5AAAAIGg8jhO/tYNeKuHodLUbgnmUn1mUJiRofPkWWWf17Mnp gert-key
```



## Backuppen van de public ssh key 

Voor de zekerheid wil Linus de *authorized_keys* file backuppen in dezelfde map. Hij doet dit door het bestand te kopiëren. Hij dient quotes te gebruiken omdat hij een spatie in de naam wilt.

```bash
ubuntu@aws-linux-ess:~/.ssh$ cp authorized_keys "authorized_keys backup"
ubuntu@aws-linux-ess:~/.ssh$ ls
 authorized_keys  'authorized_keys backup'
```



Bij nader inzien maakt de spatie het misschien onnodig moeilijker. Hij hernoemt het bestand om er geen spatie meer in te hebben.

```bash
ubuntu@aws-linux-ess:~/.ssh$ mv "authorized_keys backup" authorized_keys.backup
ubuntu@aws-linux-ess:~/.ssh$ ls
authorized_keys  authorized_keys.backup
```



Overzichtelijker zou misschien zijn indien alle backups samen staan in een mapje *backups* rechtstreeks in zijn homefolder. Dit kan als volgt:

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



## Opslaan van Publiek IP 

Het IP adres van de server zou in principe steeds hetzelfde moeten blijven. Om dit eventueel op een later tijdstip te checken wil Linus het huidige IP adres in een bestandje zetten.

Eerst achterhaald hij het huidige publieke IP adres. Hij kent het commando niet meer, maar weet dat het iets was met *curl*. Hij zoekt in de historiek van zijn shell commando's door de toetsencombinatie ***CTRL+r***. 

```bash
ubuntu@aws-linux-ess:~$     (CTRL+r)
(reverse-i-search)`curl': curl checkip.amazonaws.com
ubuntu@aws-linux-ess:~$ curl checkip.amazonaws.com
54.87.203.25
```



Dit IP adres kan hij in een bestandje plaatsen genaamd *PublicIP* met het commando ***nano PublicIP***.  De editor (nano) afsluiten kan met de toetsencombinaties ***CTRL+s*** (=save) gevolgd door ***CTRL+x*** (=exit).

```bash
ubuntu@aws-linux-ess:~$ nano PublicIP
...
ubuntu@aws-linux-ess:~$ cat PublicIP
54.87.203.25
```

