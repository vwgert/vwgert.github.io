# Oefeningen op automatisatie

## Oefening 1
Maak een map met de naam _bin_ in je thuismap.     
  

## Oefening 2
Log uit en log weer in. Zorg ervoor dat de map _bin_ is toegevoegd aan de variabele PATH. Weet je ook waarom de map aan de variabele PATH is toegevoegd? (Hint: .profile) 

```bash
student@linux-ess:~$ echo $PATH
/home/student/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/games:/usr/local/games:/snap/bin
```
  
  
## Oefening 3
Maak een script, genaamd _show.sh_, dat vraagt om een pad naar een map. Probeer de gebruikersnaam bij de vraag te betrekken (zie het voorbeeld). Gebruik het commando `env` om te zoeken naar de juiste systeemvariabele om te gebruiken.  
Toon een lijst met alle bestanden in de gegeven map.  
Maak het script uitvoerbaar en controleer of het werkt.  

Voorbeeld: 
```bash
student@linux-ess:~/bin$ show.sh
Beste student, geef aub een map op:
/etc/ssl
certs  openssl.cnf  private
```
  
  
## Oefening 4
Wijzig het vorige script. Zoek in de manpage van echo hoe je de cursor achter de vraag kunt houden: Geef de dir op: _ 

Voorbeeld: 
```bash
student@linux-ess:~/bin$ show.sh
Beste student, geef aub een map op: /etc/ssl
certs  openssl.cnf  private
```
  
  
## Oefening 5
Wijzig het vorige script. Vang drie parameters op in het script en voeg deze toe aan het commando `ls` in het script. 
Test het script met de parameters `-l`, `-a` en `-h` 

Voorbeeld: 
```bash
student@linux-ess:~/bin$ show.sh -l -a -h
Beste student, geef aub een map op: /etc/ssl
total 44K
drwxr-xr-x  4 root root 4.0K Nov  4 14:19 .
drwxr-xr-x 97 root root 4.0K Nov 12 13:41 ..
drwxr-xr-x  2 root root  16K Aug  9 11:58 certs
-rw-r--r--  1 root root  13K Jul  4 11:20 openssl.cnf
drwx------  2 root root 4.0K Jul  4 11:20 private
```

Probeer ook het script te starten met slechts 1 parameter (-l) of een samentrekking (-lah) 
  
  
## Oefening 6
Probeer het script uit te voeren terwijl je je in een andere map bevindt dan de bin-map. Werkt het door alleen de naam op te geven (geen pad)?  
Maak een nieuwe map in je thuismap, genaamd _myscripts_. 
Verplaats het script _show.sh_ naar de map _myscripts_. 
Probeer het script uit te voeren terwijl je je in een andere map bevindt dan de map myscripts. Werkt het door alleen de naam op te geven (geen pad)? 
Los dit op door het pad toe te voegen aan de juiste variabele. Zorg er ook voor dat dit pad in de toekomst gekend is. Om dit te testen moet je uitloggen en opnieuw inloggen. 
Gebruik ook het commando `which` om te controleren of het werkt. 
  
  
## Oefening 7
Wijzig het vorige script. Druk eerst de huidige datum af in de notatie zoals in het voorbeeld. Zoek in de manpage van `date` om het juiste formaat te vinden. 

Voorbeeld:  
```bash
student@linux-ess:~/myscripts$ show.sh
Saturday, 12 November 2022
Dear student, please specify the dir: /
bin   dev  home  lib32  libx32      media  opt   root  sbin  srv       sys  usr
boot  etc  lib   lib64  lost+found  mnt    proc  run   snap  swap.img  tmp  var
```
   
   
## Oefening 8
Maak een taak die je eenmaal in ongeveer vijf minuten uitvoert. De taak moet een overzicht van alle ingelogde gebruikers in het bestand _/tmp/userlist_ plaatsen. 
Naast de huidige ssh-verbinding met de server, log ook in op de server zelf. 
Bekijk na 5 minuten het bestand _/tmp/userlist_. 

Voorbeeld:
```bash  
student@linux-ess:~/myscripts$ cat /tmp/userlist
 17:10:15 up 14:42,  2 users,  load average: 0.20, 0.16, 0.10
USER     TTY      FROM             LOGIN@   IDLE   JCPU   PCPU WHAT
student  tty1     -                17:08    2:13   0.11s  0.05s -bash
student  pts/0    192.168.75.1     15:04    7.00s  0.25s  0.02s w
``` 
    
   
## Oefening 9
Maak een persoonlijke cronjob die de tekst _Herstart om_ opslaat en vervolgens de _datum_ en _tijd_ in het bestand _~/rebootlog_. 
Doorzoek de manpage van het crontab-bestand, meer bepaald de sectie _File Format_. Zoek naar de tekst _reboot_.  
      
  
## Oefening 10 
Maak een Cronjob die elke zondag om 23:59 uur een back-up maakt van alle homefolders (reguliere gebruikers en root) naar de map _/backups_. Plaats de back-up in een tarball met de naam homefolders.tar.gz. 
Maak het script en plaats het in _/scripts_.  
Maak de cronjob. 

PS: Om de cronjob te testen verander je de tijd en dag-van-de-week naar binnen precies 1 minuut. Wacht een minuut en controleer of de tarball bestaat.