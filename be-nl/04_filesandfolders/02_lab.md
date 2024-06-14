# Lab <!-- {docsify-ignore} --> 
In het vorige hoofdstuk installeerde Linus een pakket genaamd `minetest` maar hij is in de war over waar dit pakket zich bevindt! In dit lab zullen we ontdekken hoe we mappen kunnen bekijken en navigeren en hoe we enkele basisopdrachten kunnen gebruiken om met bestanden te werken. Met deze kennis kunnen we misschien het `minetest`-pakket lokaliseren en de server daadwerkelijk starten. 

## Inhoud van mappen weergeven 

Voordat hij iets anders doet, wil Linus echt weten hoe hij de inhoud van mappen kan weergeven. Hij kwam er al achter dat hij een prompt gebruikt die opdrachten uitvoert in een specifieke map, zoals te zien is in de vorige hoofdstukken. Met behulp van het commando `apropos directory` komt hij erachter dat er allerlei commando's beschikbaar zijn om met mappen te werken. Het eerste commando dat Linus bekijkt is het `pwd` commando: 

```bash
student@linux-ess:~$ apropos directory
...
ls (1)               - list directory contents
...
pwd (1) - print name of current/working directory
...
```

Na het uitvoeren van dit commando ziet Linus inderdaad de werkmap waarin hij zich bevindt: 

```bash
student@linux-ess:~$ pwd
/home/student
```

Met behulp van de manpages leert hij over het `ls` commando dat de inhoud van een map moet tonen: 

```bash
student@linux-ess:~$ ls
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