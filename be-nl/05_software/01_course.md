# Software en pakketten 
In Windows hebben we verschillende opties om software te installeren. We gebruiken meestal installatieprogramma's die we vinden op schijven en websites of zelfs de Windows-app store waar we software kunnen vinden in een online catalogus.  

Herinner je je die nieuwste gehypte videogame die je vooraf hebt besteld en die een totale ramp bleek te zijn? Wanneer je dat spel installeert, kan het je zeggen/vragen dat je de nieuwste versie van DirectX of Visual C ++ Redistributable moet installeren? Dit zijn andere stukjes software die nodig zijn om de eerste toepassing of game uit te voeren. We noemen deze stukjes software _dependencies/afhankelijkheden_. Meestal installeert het oorspronkelijke installatieprogramma deze voor ons, maar soms moeten we deze dependencies zelf handmatig vinden en installeren. 

Het installeren van software op Linux-systemen is niet altijd eenvoudig geweest. Vroeger moesten we zelf broncode downloaden en applicaties compileren, deze in de juiste mappen plaatsen en ervoor zorgen dat we alle benodigde dependencies hadden om de applicatie uit te voeren. We kunnen dit proces tegenwoordig nog tegenkomen, maar meestal gaan we software installeren met behulp van _package managers/pakketbeheerders_. Dit zijn tools die door een database zoeken om de applicatie te vinden die we willen installeren. Als er een toepassing wordt gevonden die overeenkomt met de opgegeven naam, wordt de toepassing en alle vereiste dependencies geïnstalleerd. Als we een toepassing verwijderen, worden ook alle dependencies verwijderd die niet langer nodig zijn. Een ander voordeel is dat de pakketbeheerder ook updates van al onze applicaties en dependencies beheert. 

## Software installeren, verwijderen en bijwerken (apt) 
Bij het installeren van softwarepakketten in Ubuntu gebruiken we vaak het commando `apt` (advanced package system). De manpage geeft ons alle informatie die we nodig hebben om het commando te gebruiken: 
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

Zoals hierboven beschreven is `apt` (of zijn voorganger `apt-get`) een pakketbeheerder. We kunnen deze tool gebruiken om pakketten (lees: software) op onze Linux-machine te installeren. Merk op dat `apt` de specifieke pakketbeheerder voor Ubuntu is. Er zijn verschillende alternatieven beschikbaar zoals `dpkg`, `pacman`, `rpm`, `yum`, `dnf`, ... die vooraf geïnstalleerd met een specifieke Linux-distributie kunnen worden geleverd. 

### Opslagplaatsen 
Belangrijk om op te merken over `apt` is dat het databases van beschikbare pakketten gebruikt. Deze databases, genaamd repositories, dienen eerst gedownload naar de computer. Dit doen we door het onderstaand commando uit te voeren: 
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
?> <i class="fa-solid fa-circle-info"></i> Merk op dat we het commando `sudo` hebben gebruikt. Dit is nodig omdat `apt` een systeembreed commando is die van invloed is op het hele systeem (software installeren/verwijderen/bijwerken). Daarom kunnen we het niet uitvoeren als een gebruiker met standaardmachtigingen. 

We kunnen zien dat dit commando een heleboel lijsten download. Deze lijsten worden _repositories_ genoemd (lijsten met welbepaalde verzamelingen van pakketten). Wanneer we later software installeren, wordt de database op basis van deze repositories gebruikt om te controleren of het pakket dat we willen installeren beschikbaar is. 

De lijst van repositories die `apt` gebruikt is te vinden in het bestand `/etc/apt/sources.list`. We kunnen handmatig meer repositories aan dit bestand toevoegen of het commando `add-apt-repository` gebruiken, maar we zullen hier voorlopig niet op ingaan. 

### Software zoeken (apt search) 
Stel je voor dat we een bestand hebben gedownload dat eindigt om `.zip`. Dan kunnen we op zoek gaan naar een programma dat hiermee overweg kan. We kunnen het onderstaande commando uitvoeren gebruik makend van regular expressions in de zoekterm: 
```bash
student@linux-ess:~$ apt search "\.zip file"       # \.  om aan te duiden dat hier letterlijk naar een punt moet gezocht worden
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
Als laatste in de lijst zien we een pakket dat .zip files kan archiveren. De procedure om dit te vinden was:
* Het doorzoekt alle repositories die we gedownload hebben van het Internet (/etc/apt/sources.list) om een pakket te vinden dat voldoet aan onze zoekterm. 
* Er worden pakketten gevonden, zoals het `zip`-pakket en `unzip`-pakket. 

?> <i class="fa-solid fa-circle-info"></i> Merk op dat je best eerst een `apt update` uitvoert om de laatste versie van de repositories te downloaden, want er wordt in deze gedownloade repositories gezocht naar de pakketten. Een verouderde repository bevat een pakket misschien nog niet, of download een verouderde versie van een pakket. 


### Software installeren (apt install) 
Stel je voor dat we het `zip`-pakket willen installeren. We kunnen eenvoudig het onderstaande commando uitvoeren: 
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
Als we de uitvoer van het commando analyseren, zien we een paar dingen gebeuren: 
* Het leest de repositories om het `zip`-pakket te vinden. Nadat dit is gebeurd, bouwt het een afhankelijkheidsboom om te zien welke afhankelijkheden het `zip`-pakket nodig heeft. 
* Het wijst erop dat het een extra pakket met de naam `unzip` zal installeren. Dit is een afhankelijkheid van het `zip` commando. 
* Het geeft aan welke nieuwe pakketten zullen worden geïnstalleerd en of er pakketten zullen worden bijgewerkt. 
* Het vraagt om een bevestiging of we zeker weten dat we door willen gaan. Na deze bevestiging zal het alle pakketten installeren / bijwerken die in de bovenstaande uitvoer worden genoemd. 

?> <i class="fa-solid fa-circle-info"></i> Je merkt misschien dat je zowel het commando `apt` als `apt-get` kunt gebruiken. Beide commando's lijken erg op elkaar (met kleine verschillen, maar daar gaan we nu niet op in). 

Na het uitvoeren van het bovenstaande commando, kunnen we met succes het commando `zip` gebruiken: 
```bash
student@linux-ess:~$ zip
Copyright (c) 1990-2008 Info-ZIP - Type 'zip "-L"' for software license.
Zip 3.0 (July 5th 2008). Usage:
zip [-options] [-b path] [-t mmddyyyy] [-n suffixes] [zipfile list] [-xi list]
  The default action is to add or replace zipfile entries from list, which
  can include the special name - to compress standard input.
  If zipfile and list are omitted, zip compresses stdin to stdout.
```
?> <i class="fa-solid fa-circle-info"></i> Je vraagt je misschien af waar het uitvoerbare bestand van `zip` zich bevindt en hoe de shell weet hoe dat exacte uitvoerbare bestand moet worden uitgevoerd. We kunnen dit controleren door het commando `which zip` uit te voeren. Dit zal ons vertellen dat, wanneer we het `zip`-commando uitvoeren, het eigenlijk het `zip` binaire bestand (=executable) op `/usr/bin/zip` zal uitvoeren. `/usr/bin` is een van de mappen waarin binaire bestanden (=uitvoerbare bestanden) worden opgeslagen. Je zou dit kunnen vergelijken met de map `c:\program files` in Windows-systemen. Linux heeft meerdere plaatsen waar binaire bestanden worden opgeslagen. Deze zijn vaak gebundeld in de variabele `$PATH` die we in een later hoofdstuk zullen leren gebruiken.  

Stel je voor dat we een typefout hebben gemaakt in ons commando en proberen een pakket te installeren dat niet bestaat: 
 ```bash
student@linux-ess:~$ sudo apt install zap
Reading package lists... Done
Building dependency tree
Reading state information... Done
E: Unable to locate package zap
 ```
De uitvoer geeft aan dat het het pakket `zap` niet kan vinden. Dit betekent dat het al zijn repositories heeft gecontroleerd op een pakket met de naam `zap`, maar het kon niet worden gevonden. Als het pakket bestaat, moeten we de repository met het pakket toevoegen en `sudo apt update` uitvoeren. 

### Software verwijderen (apt remove) 
Om software te verwijderen, kunnen we eenvoudig het onderstaande commando gebruiken: 
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
Merk op hoe het niet automatisch de afhankelijkheden verwijdert waar we het eerder over hadden. Dit komt omdat er mogelijk andere pakketten zijn die deze afhankelijkheid vereisen. We kunnen het commando `sudo apt autoremove` gebruiken om ongebruikte afhankelijkheden te verwijderen. 

We hebben ook een wat agressiever commando om pakketten te verwijderen: `sudo apt purge <pakketnaam>`. Het verschil tussen `remove` en `purge` is dat bij het gebruik van `purge` ook alle configuratiebestanden worden verwijderd die aan die toepassing zijn gekoppeld. Bij gebruik van `remove` blijven die configuratiebestanden op het systeem staan. 

?> <i class="fa-solid fa-circle-info"></i> Om een overzicht te krijgen van alle mogelijke softwarepakketten kunnen we gebruik maken van `apt list`. Om een lijst van geïnstalleerde softwarepakketten te krijgen, kunnen we `apt list --installed` gebruiken. Waarschuwing: deze lijst kan erg lang zijn! 

### Software bijwerken (apt upgrade) 
Voor het updaten van onze software hebben we een aantal opties. Om te beginnen kunnen we bepaalde pakketten individueel updaten door simpelweg het commando `sudo apt install <pakketnaam>` te gebruiken. Wanneer je deze opdracht gebruikt met een pakket dat al is geïnstalleerd, wordt geprobeerd het bij te werken naar de nieuwste versie. 

?> Houd er rekening mee dat voordat je software bijwerkt of zelfs installeert, je misschien je database wilt bijwerken door `sudo apt update` uit te voeren, zodat je zeker weet dat we de nieuwste en juiste repositories gebruiken. *Dit kan in het begin ook verwarrend zijn omdat het commando `update` pakketten niet echt bijwerkt!* 

Wanneer we alle pakketten op ons systeem willen updaten, kunnen we het commando `sudo apt upgrade` gebruiken. Hiermee worden alle geïnstalleerde pakketten bijgewerkt. 

## gzip en tar 

### gzip 

Als we een bestand comprimeren, behouden we de inhoud, maar wordt de bestandsgrootte kleiner. We kunnen een bestand comprimeren met gzip. 

```bash
student@ubuntu-server:~$ cd
student@ubuntu-server:~$ cp /var/lib/apt/lists/be.archive.ubuntu.com_ubuntu_dists_jammy_universe_binary-amd64_Packages .
student@ubuntu-server:~$ ls -lh be.archive*
-rw-r--r-- 1 student student 62M Oct 10 19:40 be.archive.ubuntu.com_ubuntu_dists_jammy_universe_binary-amd64_Packages
student@ubuntu-server:~$ gzip be.archive.ubuntu.com_ubuntu_dists_jammy_universe_binary-amd64_Packages
student@ubuntu-server:~$ ls -lh be.archive*
-rw-r--r-- 1 student student 17M Oct 10 19:40 be.archive.ubuntu.com_ubuntu_dists_jammy_universe_binary-amd64_Packages.gz
```

Het bestand heeft de extensie gz en is nu een stuk kleiner, maar je kunt de inhoud niet zien. Het originele bestand is verdwenen en we hebben nu alleen het gecomprimeerde bestand. 

### gunzip 

Als we het bestand willen decomprimeren, kunnen we gunzip gebruiken. 
```bash
student@ubuntu-server:~$ ls -lh be.archive*
-rw-r--r-- 1 student student 17M Oct 10 19:40 be.archive.ubuntu.com_ubuntu_dists_jammy_universe_binary-amd64_Packages.gz
student@ubuntu-server:~$ gunzip be.archive.ubuntu.com_ubuntu_dists_jammy_universe_binary-amd64_Packages.gz
student@ubuntu-server:~$ ls -lh be.archive*
-rw-r--r-- 1 student student 62M Oct 10 19:40 be.archive.ubuntu.com_ubuntu_dists_jammy_universe_binary-amd64_Packages
```

Het bestand heeft zijn oorspronkelijke grootte teruggekregen en de inhoud kan opnieuw worden bekeken/bewerkt. Het gezipte bestand is weer weg en we hebben alleen het originele bestand nog. 

### tar 

Als we meerdere bestanden en mappen in één bestand willen samenvoegen, kunnen we tar gebruiken. We gebruiken de optie -c om de tarfile te maken. 
```bash
student@ubuntu-server:~$ tree
.
├── Downloads
│   ├── logo.png
│   └── Steam
│       └── games
│           └── pacman
├── emptyfile
student@ubuntu-server:~$ tar -cf Downloads.tar Downloads     # creëer tar
student@ubuntu-server:~$ tar -tf Downloads.tar               # bekijk de inhoud van de tar
Downloads/
Downloads/logo.png
Downloads/Steam/
Downloads/Steam/games/
Downloads/Steam/games/pacman
```

### tarball

We kunnen de tar ook ineens zippen als we hem aanmaken.

```bash
student@ubuntu-server:~$ tree
.
├── Downloads
│   ├── logo.png
│   └── Steam
│       └── games
│           └── pacman
├── emptyfile
student@ubuntu-server:~$ tar -czf Downloads.tar.gz  Downloads             # creëer tarball 
student@ubuntu-server:~$ tar -tzf Downloads.tar.gz                        # bekijk de inhoud van de tarball
Downloads/
Downloads/logo.png
Downloads/Steam/
Downloads/Steam/games/
Downloads/Steam/games/pacman
```

### pak een tar uit

We kunnen een tarfile (.tar) of tarball (.tar.gz) uitpakken. 

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
student@ubuntu-server:~$ tar -xzf Downloads.tar.gz  -C backup      # gezipte tarball
student@ubuntu-server:~$ tar -xf Downloads.tar -C /tmp             # tarbestand
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

### Pakketten installeren via een tarball 

Soms kan je een `tar` of `tar.gz` bestand tegenkomen voor het installeren van sommige software. Een `tar.gz` bestand wordt ook wel een `tarball` genoemd. Het is een gecomprimeerd bestand met allerlei soorten bestanden en mappen. Je kunt deze vergelijken met `zip` of `rar` bestanden. We moeten de bestanden / mappen in dit bestand uitpakken voordat we ze kunnen gebruiken. Hiervoor kunnen we het commando `tar` gebruiken. De opties die we gebruiken, variëren afhankelijk van het bestand. Willen we een `tar`-bestand of een `tar.gz`-bestand uitpakken: 
```bash
student@linux-ess:~/tarexample$ ls
app.tar.gz  docs.tar
student@linux-ess:~/tarexample$ tar -xf docs.tar
student@linux-ess:~/tarexample$ mkdir app
student@linux-ess:~/tarexample$ tar -xzf app.tar.gz -C ./app
student@linux-ess:~/tarexample$ ls
app  app.tar.gz  docs  docs.tar
```
De opties die we gebruiken zijn te vinden in de manpage, maar hieronder vind je een kleine samenvatting van de belangrijkste:  
* `-x`: Staat voor extract, hiermee wordt alle inhoud van het bestand uitgepakt. 
* `-f`: Staat voor file. Dit gebruikt het argument na de opties als het pad van het archief dat we willen uitpakken. 
* `-z`: Dit zorgt ervoor dat we het bestand uitvoeren via `gzip`, een andere archieftool. De extensie `tar.gz` geeft aan dat het via `gzip` wordt verwerkt. 
* `-C`: Hiermee wordt de map gewijzigd voordat deze wordt uitgepakt naar het pad dat als argument wordt opgegeven. Dit betekent dat de inhoud in deze map wordt uitgepakt. 
* `-t`: Geeft alleen de inhoud van het archief weer op het scherm. Het zal niets uitpakken. 

## dpkg
`dpkg` was de eerste pakketbeheerder voor Debian gebaseerde systemen. Waar Ubuntu tegenwoordig `apt` als standaard pakketbeheerder gebruikt, kunnen wij ook `dpkg` gebruiken. `dpkg` was de voorloper van `apt-get` en `apt`. `dpkg` maakt geen gebruik van repositories, dus we moeten het installatiebestand hebben voordat we het commando gebruiken. Het downloadt ook niet automatisch afhankelijkheden. Daarom noemden ze het vroeger *de dependancy hell* We kunnen `dpkg` gebruiken om `.deb`-bestanden te installeren / verwijderen / ... . In het onderstaande voorbeeld wordt het pakket `yourpackage` geïnstalleerd: 
```bash
student@linux-ess:~$ sudo dpkg -i yourpackage.deb
```

`dpkg` kan ook worden gebruikt om bepaalde pakketten te (her)configureren. We kunnen dit bijvoorbeeld gebruiken om de toetsenbordindeling op onze server te wijzigen door het volgende uit te voeren: 
```bash
student@linux-ess:~$ sudo dpkg-reconfigure keyboard-configuration
```


## snap
Een van de relatief nieuwe spelers is snap. Een snap is een bundel van software die we willen installeren met al zijn afhankelijkheden opgeslagen in één bestand en uitgevoerd in zijn eigen bubbel. Dit betekent dat twee snaps elkaar niet kunnen verstoren. Dit maakt het bijvoorbeeld mogelijk om twee verschillende versies van dezelfde software tegelijkertijd te installeren en samen uit te voeren. Snaps hebben hun eigen bestandssysteem, maar kunnen ook werken met bestanden op je systeem. Je kunt snaps vinden in de snap store op een Desktop of met `snap search` op een server. Snaps worden steeds meer gebruikt omdat ze distro-onafhankelijk zijn. Als je de snap-daemon op de distro kunt installeren, kan je alle snaps uitvoeren.  

De commando's voor het werken met snap zijn bijna vergelijkbaar met apt. Wij beschikken over: 
snap search  
snap list (geïnstalleerd apps)  
snap list --all (toont alle geïnstalleerde versies)  
snap revert <snapname> --revision <revnumber> (Teruggaan naar een eerdere versie van de snap )  
snap info   
snap install  
snap remove   
snap refresh (upgraden van de snaps, gebeurt elke dag automatisch)     
snap changes (geschiedenis van wijzigingen)  
snap version  

snap update bestaat niet. De snap daemon controleert 4 keer per dag op updates. 

Je kunt installeren vanuit verschillende kanalen (zoals stable, beta,...) maar de standaard is stabiel en dat houden we zo. 
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

?> Om te navigeren en in te zoomen gebruik je de *pijltjes* en *a* en *z* 


## zip vs gzip
`gzip` comprimeert slechts één bestand en wordt daarom gebruikt met `tar` dat meerdere bestanden in één bestand brengt.  
`zip` wordt gebruikt wanneer je in één stap een aantal bestanden in één bestand wilt comprimeren. 

```bash
student@linux-ess:~$ ls -a
.   ..   .bash_history   .bash_logout   .bashrc   .profile   .ssh
student@linux-ess:~$ zip myzipfile.zip .bashrc .profile
  adding: .bashrc (deflated 54%)
  adding: .profile (deflated 51%)
student@linux-ess:~$ ls -l
total 2440
-rw-rw-r-- 1 student student    2440 Oct 14 15:00 myzipfile.zip
student@linux-ess:~$ unzip -l myzipfile.zip     # alleen de bestanden weergeven 
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
Dus waarom gebruiken we `tar` en `gzip` als we in plaats daarvan `zip` kunnen gebruiken? Dit komt omdat `tar` ook de eigenaars en de rechten op elk bestand behoudt. We zullen de twee vergelijken met een voorbeeld (als je de eigenaars in het voorbeeld niet echt begrijpt, houd er dan rekening mee dat het in een latere les zal worden uitgelegd): 
```bash
student@linux-ess:~$ ls -lh .bashrc
-rw-r--r-- 1 student student 3.7K Jan  6  2022 .bashrc        # let op de eigenaar student
student@linux-ess:~$ zip zipdemo.zip .bashrc
  adding: .bashrc (deflated 54%)
student@linux-ess:~$ tar -czf tardemo.tgz .bashrc
student@ulinux-ess:~$ ls -lh zipdemo.zip tardemo.tgz
-rw-rw-r-- 1 student student 1.9K Oct 14 15:21 tardemo.tgz
-rw-rw-r-- 1 student student 1.9K Oct 14 15:19 zipdemo.zip 
student@ulinux-ess:~$ cp zipdemo.zip tardemo.tgz /tmp
student@ulinux-ess:~$ cd /tmp
student@ulinux-ess:/tmp$ sudo unzip zipdemo.zip              # sudo -> doe als root gebruiker -> gewoon om de rechten te demonstreren
student@ulinux-ess:/tmp$ ls -lh .bashrc
-rw-r--r-- 1 root root 3.7K Jan  6  2022 .bashrc             # root is de eigenaar omdat hij de bestanden heeft gemaakt met het uitpakken van het zipbestand 
student@ulinux-ess:/tmp$ sudo rm .bashrc
student@ulinux-ess:/tmp$ sudo tar -xzf tardemo.tgz            # sudo -> doe als root gebruiker -> gewoon om de rechten te demonstreren
student@ulinux-ess:/tmp$ ls -lh .bashrc
-rw-r--r-- 1 student student 3.7K Jan  6  2022 .bashrc       # student is nog steeds de eigenaar, ook al zijn de bestanden gemaakt door root (sudo) terwijl we uitpakken 
```