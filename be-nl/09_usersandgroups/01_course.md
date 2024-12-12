# Gebruikers en groepen 

Zoals met elk besturingssysteem zullen we met verschillende gebruikers op het systeem werken. We gebruiken momenteel de gebruiker 'student'. We kunnen dit bevestigen door het commando `whoami` uit te voeren. Andere commando's die we kunnen uitvoeren zijn `who` of `w`. Deze laten ons alle gebruikers zien die zijn ingelogd op het systeem (let op dat beide commando's een andere uitvoer hebben!). 

## Gebruikersbeheer 
### /etc/passwd 
Zoals we eerder hebben gezien, wordt alle systeemconfiguratie gedaan met behulp van configuratiebestanden. Hetzelfde geldt voor gebruikersbeheer. De gebruikersconfiguratie wordt opgeslagen in het bestand `/etc/passwd`. Het bevat een lijst met gebruikersaccounts samen met enkele metagegevens gescheiden door dubbele punten: 
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
Het eerste account in dit bestand is het `root` account: 
```bash
student@linux-ess:~$ head -1 /etc/passwd
root:x:0:0:root:/root:/bin/bash
```

We kunnen meer informatie zien dan alleen gebruikersnamen. Deze regels bevatten de gebruikersidentificatie (`1000` voor `student`), de locatie van de home folder, de standaardshell, ...  

?> <i class="fa-solid fa-circle-info"></i> Meer informatie over dit bestand, de opmaak en de inhoud vind je door het commando `man 5 passwd` uit te voeren. 

### Gebruikers toevoegen (useradd) 
Om gebruikers toe te voegen kunnen we eenvoudig het commando `useradd` gebruiken. Het is belangrijk op te merken dat we dit commando moeten uitvoeren met `sudo`-rechten. Dit komt omdat het een systeemopdracht is die het hele systeem beïnvloedt. Om een nieuwe gebruiker met de gebruikersnaam `teacher` toe te voegen, kunnen we het volgende commando uitvoeren: 
```bash
student@linux-ess:~$ sudo useradd -m -d /home/teacher -c "Teacher Account" teacher
[sudo] password for student:
student@linux-ess:~$ tail -3 /etc/passwd
student:x:1000:1000:student:/home/student:/bin/bash
lxd:x:999:100::/var/snap/lxd/common/lxd:/bin/false
teacher:x:1001:1001:Teacher Account:/home/teacher:/bin/sh
```

De `-d` neemt een argument op en gebruikt dit argument als een pad naar waar de homefolder moet worden gemaakt. De optie `-m` (`create home`) zorgt ervoor dat de homefolder daadwerkelijk met de juiste machtigingen wordt aangemaakt. Ten slotte stelt de optie `-c` (`comment`) extra metadata in voor de gebruiker.  

?> <i class="fa-solid fa-circle-info"></i> Houd er rekening mee dat de optie -d optioneel is en als deze niet is opgegeven, standaard een map is met dezelfde naam als de gebruikersnaam in de map /home. 

?> <i class="fa-solid fa-circle-info"></i> We kunnen gebruikers verwijderen door het commando `userdel -r teacher` uit te voeren. De optie `-r` verwijdert ook de homefolder van die gebruiker. 

Zoals te zien is in de map `/home` of in het bestand `/etc/passwd` is de nieuwe gebruiker aangemaakt: 
```bash
student@linux-ess:~$ tail -1 /etc/passwd
teacher:x:1001:1001:Teacher Account:/home/teacher:/bin/sh
student@linux-ess:~$ ls -l /home
total 8
drwxr-x--- 5 student student 4096 Nov  4 16:04 student
drwxr-x--- 2 teacher teacher 4096 Nov  7 20:28 teacher
```

Elke gebruiker heeft een userid (het derde veld in `/etc/passwd`). Om de userid van een gebruiker te bekijken kun je het commando `id` gebruiken: 
```bash
student@linux-ess:~$ id teacher
uid=1001(teacher) gid=1001(teacher) groups=1001(teacher)
```

#### Standaardwaarden 
Het commando `useradd` gebruikt nogal wat standaardwaarden. We kunnen deze standaardwaarden controleren door het volgende commando uit te voeren: 
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
Deze instellingen worden bewaard in het bestand `/etc/default/useradd` en kunnen op elk moment worden gewijzigd door het bestand te wijzigen of `useradd -D [optie]` te gebruiken. 

?> <i class="fa-solid fa-circle-info"></i> Merk op dat de standaardwaarde voor de shell `/bin/sh` is. Het is een goede gewoonte om dit te wijzigen in `/bin/bash` zodat elke nieuwe gebruiker die in de toekomst wordt aangemaakt de `bourne again shell` als standaard krijgt (bijv. sudo useradd -D --shell /bin/bash). 

#### /etc/skel 
Standaard worden homefolders aangemaakt als een submap van de map `/home`. Deze mappen worden niet uit het niets gemaakt. De inhoud van de map `/etc/skel` wordt gekopieerd binnen elke nieuw aangemaakte homefolder. Dit betekent dat als we inhoud in deze `skel`map wijzigen, deze daadwerkelijk wordt gekopieerd naar elke nieuwe gebruiker die in de toekomst zal worden gemaakt: 
```bash
student@linux-ess:~$ ls -a /etc/skel
.  ..  .bash_logout  .bashrc  .profile
student@linux-ess:~$ sudo ls -a /home/teacher/
.  ..  .bash_logout  .bashrc  .profile
```

#### Standaard profielbestanden 
__.bashrc__: uitgevoerd telkens wanneer een nieuwe shell (bash) wordt gestart 

__.bash\_logout__: wist het scherm wanneer de gebruiker uitlogt 

__.profile__: uitgevoerd wanneer de gebruiker inlogt 

### Gebruikers bewerken (usermod & userdel) 
Om de accountconfiguratie van een gebruiker te bewerken, kunnen we het commando `usermod` gebruiken. Dit commando heeft verschillende opties die we kunnen gebruiken om specifieke instellingen te bewerken. Om bijvoorbeeld het commentaarveld van een gebruiker te bewerken, kunnen we het volgende commando uitvoeren: 
```bash
student@linux-ess:~$ grep student /etc/passwd
student:x:1000:1000:student:/home/student:/bin/bash
student@linux-ess:~$ sudo usermod -c "Student Account" student
student@linux-ess:~$ grep student /etc/passwd
student:x:1000:1000:Student Account:/home/student:/bin/bash
```

Om de standaard shell voor een specifieke gebruiker te bewerken, kunnen we het volgende doen: 
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

?> Bekijk de manpage van `usermod` voor alle mogelijke opties. 

?> Als we een gebruiker willen maken waarop niet kan worden ingelogd, kunnen we zijn shell wijzigen naar `/bin/false` of `/sbin/nologin`. Het verschil tussen deze twee is dat `/sbin/nologin` een beleefd bericht geeft dat je niet kunt inloggen op dit account voordat het afsluit. De optie `/bin/false` sluit direct af zonder iets te zeggen. 

#### Gebruikerswachtwoorden instellen 
Als we ons eigen wachtwoord willen wijzigen, kunnen we het commando `passwd` gebruiken (zonder sudo!): 

```bash
student@linux-ess:~$ passwd
Changing password for student.
Current password:
New password:
Retype new password:
passwd: password updated successfully
```
?> <i class="fa-solid fa-circle-info"></i> Houd er rekening mee dat je wachtwoord lang en moeilijk genoeg moet zijn, anders wordt het nieuwe wachtwoord niet geaccepteerd. 

?> <i class="fa-solid fa-circle-info"></i> Merk op dat als we `sudo passwd` gebruiken, we het wachtwoord van de root gebruiker wijzigen en niet ons eigen wachtwoord! 

Zoals te zien is in de vorige commando's hebben we een nieuwe gebruiker aangemaakt met de gebruikersnaam `teacher` maar we hebben deze nooit een wachtwoord gegeven. Om dit te doen kunnen we het `passwd` commando uitvoeren met `sudo` rechten en met een gebruikersnaam als argument. Dit dwingt het instellen van een nieuw wachtwoord voor die specifieke gebruiker: 
```bash
student@linux-ess:~$ sudo passwd teacher
New password:
Retype new password:
passwd: password updated successfully
```

Het wachtwoord wordt om veiligheidsredenen opgeslagen in het bestand `/etc/shadow`. Gewone gebruikers kunnen de inhoud van dit bestand niet bekijken: 
```bash
student@linux-ess:~$ tail -1 /etc/shadow
tail: cannot open '/etc/shadow' for reading: Permission denied
student@linux-ess:~$ sudo tail -1 /etc/shadow
teacher:$y$j9T$Vtf.U//c4/N/CB8LzHfnl0$5iCgijrpqXfaA3v18w/nAL2rl8BmiBYX5rn5rf.j6B7:19171:0:99999:7:::
```
Zoals te zien is in het bovenstaande voorbeeld, wordt het wachtwoord niet weergegeven in leesbare tekst. Dit komt omdat Linux-systemen hashing-algoritmes gebruiken om de wachtwoorden te versleutelen. Het algoritm dat hier wordt gebruikt, wordt _sha512_ genoemd. 

## Veranderen van gebruiker (su) 
Je kan een gebruiker uitloggen met `logout` of `exit`. Natuurlijk kun je na het uitloggen weer inloggen als een andere gebruiker. Met het commando su (substitute user) kan je tijdelijk als een andere gebruiker werken: 
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

Merk op dat root kan worden wie hij wil zonder dat hij het wachtwoord van die gebruiker hoeft te kennen: 
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

Merk op dat om root te worden (zonder zijn wachtwoord te kennen) we ook het commando `sudo su` kunnen gebruiken: 
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

Je moet voorzichtig zijn met commando's die je als `root`-gebruiker uitvoert. Deze gebruiker kan machtigingen hebben voor alle bestanden, mappen en services op ons systeem. Dit betekent dat het uitvoeren van commando's als `root` een enorme impact kan hebben wanneer ze worden misbruikt. 

?> <i class="fa-solid fa-circle-info"></i> Merk op dat als je de min (-) gebruikt met het su commando, dat het profiel van de nieuwe gebruiker ook geladen wordt en je in de homedirectory van die gebruiker wordt gezet. Als je de min (-) niet gebruikt, wordt het profiel van de gebruiker niet geladen. Je wordt nog steeds de nieuwe gebruiker met zijn rechten, maar je blijft in de huidige map omdat zijn profiel niet wordt geladen. 

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

## Groepsmanagement 

### Groepsinfo van een gebruiker bekijken (id, groups) 

Om de groepen te bekijken waarvan een gebruiker lid is, kunnen we de commando's `id` en `groups` gebruiken: 
```bash
student@linux-ess:~$ id student
uid=1000(student) gid=1000(student) groups=1000(student),4(adm),24(cdrom),27(sudo),30(dip),46(plugdev),110(lxd)
student@linux-ess:~$ groups student
student : student adm cdrom sudo dip plugdev lxd
```

### /etc/group 
Het bestand waarin de groepsinformatie van de gebruikers is opgeslagen is `/etc/group`. We kunnen ook wijzigingen aanbrengen in dit bestand in plaats van commando's te gebruiken. 
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

### Groepen toevoegen (groupadd) 
Als er behoefte is aan nieuwe groepen, kunnen we dit doen met het commando `groupadd`: 
```bash
student@linux-ess:~$ sudo groupadd ict
student@linux-ess:~$ tail -3 /etc/group
student:x:1000:
teacher:x:1001:
ict:x:1002:
```

?> We kunnen groepen verwijderen met het commando `groupdel`. 

### Groepen bewerken (groupmod) 
Als we een groep moeten wijzigen, kunnen we `groupmod` gebruiken: 
```bash
student@linux-ess:~$ sudo groupmod -n it ict
student@linux-ess:~$ tail -3 /etc/group
student:x:1000:
teacher:x:1001:
it:x:1002:
```

### Groepslidmaatschappen bewerken (usermod & deluser) 
Als we een gebruiker aan een extra groep willen toevoegen, kunnen we ook het commando `usermod` gebruiken: 
```bash
student@linux-ess:~$ sudo usermod -a -G it teacher
student@linux-ess:~$ id teacher
uid=1001(teacher) gid=1001(teacher) groups=1001(teacher),1002(it)
student@linux-ess:~$ groups teacher
teacher : teacher it
student@linux-ess:~$ grep it /etc/group
it:x:1002:teacher
```

?> <i class="fa-solid fa-circle-exclamation"></i> Als we de optie `-a` (__add__) vergeten, bevindt de gebruiker zich alleen in de opgegeven aanvullende groep en wordt deze verwijderd uit alle groepen waarin hij zich bevond. Dit kan een ernstig probleem zijn als de gebruiker de enige in de sudo-groep was! 

Als we een gebruiker willen verwijderen uit een extra groep hebben we een aantal opties
* specificeer alle aanvullende groepen waarin hij moet blijven en gebruiken de optie -a niet in het usermod commando
* bewerk het groepsbestand `/etc/group` met de hand en verwijder de gebruikersnaam in de gebruikerslijst van de groep
* gebruik het deluser commando (enkel in debian-based distro's):
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

?> <i class="fa-solid fa-circle-info"></i> De primaire groep van een gebruiker wordt opgegeven in `/etc/passwd` en is de standaardgroep die is ingesteld op een nieuw bestand of een nieuwe map die door die gebruiker is gemaakt. 

?> <i class="fa-solid fa-circle-info"></i> Een gebruiker weet een wijziging in het groepslidmaatschap alleen wanneer hij zich aanmeldt. Dus na een wijziging moet een gebruiker opnieuw inloggen om het verschil te merken. 

In het onderstaande voorbeeld zien we dat de `primaire` groep van de gebruiker student is gewijzigd in 'it' en dit wordt weergegeven door de id en grep van het passwd-bestand. Het groups-commando toont echter niet de verandering van groep, ook wanneer we een nieuw bestand maken, wordt de oude primaire groep nog steeds gebruikt. Zoals eerder vermeld, moeten we uitloggen en opnieuw inloggen om de wijzigingen te laten plaatsvinden. Dit is ook te zien in het voorbeeld. 
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
student@linux-ess:~$ 
```

Merk in het bovenstaande voorbeeld op dat toen we de primaire groep wijzigden, alle bestanden van de gebruiker student ook werden bewerkt naar de nieuwe primaire groep van deze gebruiker. Maar omdat we de groepen niet hebben bijgewerkt door uit te loggen en opnieuw in te loggen, wordt onze oude primaire groep gebruikt voor het nieuwe bestand. In het hoofdstuk over rechten leren we hoe je de groepseigenaar kunt wijzigen om deze fout te corrigeren. Als we opnieuw inloggen, zien we dat onze groepen zijn bijgewerkt. 
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
