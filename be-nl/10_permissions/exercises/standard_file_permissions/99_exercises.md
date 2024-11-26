# Oefeningen op Standard file permissions

## Oefening 1
voer het volgende commando uit: <br />
```bash
ls /root
```


## Oefening 2
Deze uitvoer wordt getoond omdat de directory /root eigendom is van de gebruiker `root` en omdat de beveiliging zo is ingesteld dat niemand behalve de `root` (en misschien gebruikers die lid zijn van de groep `root`) toegang heeft. Je kunt dit zien met het commando ls -ld /root 
Laten we nu zeggen dat jij de systeembeheerder bent en dat je toegang nodig hebt tot de mappen van de groep `root`. In dit geval moeten we onze gebruiker toevoegen aan de groep `root`. <br /> 

Welk commando kan worden gebruikt om dit te bereiken? 


## Oefening 3
Wat is er gewijzigd in het bestand /etc/group? 


## Oefening 4
Kan je het ls commando in de directory /root gebruiken? JA / NEE 


## Oefening 5
Zo niet, los dit probleem dan op 


## Oefening 6
Verander je umask in 0037. Maak een nieuwe file en folder en check de rechten.


## Oefening 7
Test op je systeem of het volgende correct is: <br /> 
'Als iemand schrijfrechten heeft in een map, worden deze schrijfrechten ook automatisch toegekend aan alle bestanden in deze map, wat betekent dat deze persoon al deze bestanden kan wijzigen?' 


## Oefening 8
Kopieer het bestand .bashrc van de homefolder van de gebruiker root naar /tmp 


## Oefening 9
Wijzig de groupowner van het bestand /tmp/.bashrc naar de groep users


## Oefening 10
Wijzig de userowner van het bestand /tmp/.bashrc naar jouw gebruiker 


## Oefening 11
Wijzig de machtigingen van het bestand /tmp/.bashrc naar: <br /> 
- De gebruikerseigenaar:    lezen, bewerken en uitvoeren 
- De groepseigenaar:        alleen-lezen 
- Anderen:                  Niets 


## Oefening 12
Wat is de opdracht die ervoor zorgt dat alle nieuw gemaakte bestanden de volgende machtiging krijgen: <br /> 
rw-r----- 


## Oefening 13
Kopieer de thuismap van iemand anders (niet die van root) met alle inhoud naar de map /tmp. Controleer de ownerships en de permissions van de gekopieerde bestanden. <br /> 
Wat valt je op? 


## Oefening 14
Kopieer de homefolder van iemand anders (niet die van root) met alle inhoud naar de map /tmp, zorg ervoor dat alle permissions en ownerships behouden blijven. Controleer de ownerships en de permissions van de gekopieerde bestanden. <br /> 
Wat valt je op? 
