# Oefeningen op File globbing

## Oefening 1 
Maak een nieuwe map met de naam FileGlobEx met de bestanden script.sh, scrupt.sh en scrApt.sh. Gebruik het commando touch om de bestanden te maken.  

## Oefening 2 
Probeer het volgende commando: ls scr[a-z]pt.* 
- Zorg ervoor dat dit commando hoofdlettergevoelig is en test 
- Zorg ervoor dat dit commando niet hoofdlettergevoelig is en test  

?> <i class="fa-solid fa-circle-info"></i> Momenteel is het ingesteld om automatisch niet hoofdlettergevoelig te gebruiken. 

## Oefening 3 
Maak de volgende bestanden met slechts één commando: script.sd, script.dh, script2.dh, script.ds, script2.ds, script2.dd, script3.ss en script3.ds 

## Oefening 4 
Zoek in de map naar alle bestanden die eindigen op .sh of .sd of .dh of .ds of .ss of .dd  
Probeer dit één keer op te lossen met vierkante haken en één keer zonder 

## Oefening 5 
Zoek in de map naar alle bestanden die beginnen met scr, dan één willekeurig teken, gevolgd door pt. Na pt kan er een niet-gespecificeerd aantal tekens zijn, maar het bestand moet eindigen met een h of een s 

## Oefening 6 
Zorg ervoor dat het commando ls /b* niet de inhoud van de gevonden mappen weergeeft, maar de mappen zelf. Zoek in de manpage naar een oplossing 

## Oefening 7 
Toon alle bestanden en mappen die eindigen op ".conf" in de map "/etc" 

## Oefening 8 
Toon alle bestanden en mappen die eindigen op ".d" gevonden in de map "/etc", toon de inhoud van deze mappen niet

## Oefening 9 
Toon alle bestanden en mappen uit de map "/etc" die "sh" ergens in hun naam hebben  

## Oefening 10 
Toon alle bestanden en mappen uit de map "/etc" met slechts 10 tekens in hun naam, toon de inhoud van de gevonden mappen niet.  

## Oefening 11 
Zoek in de map "/etc" naar een bestand met "os" in de naam gevolgd door "release" ergens. Toon de inhoud van dit bestand. 

## Oefening 12 
Voer het volgende commando uit en leg het resultaat uit:  
```bash 
ls -d /usr/share/bash-completion/completions/resolv*conf 
``` 

## Oefening 13 
Zoek naar alle bestanden die beginnen met twee cijfers uit de map "/etc/grub.d" 

## Oefening 14 
Toon een lijst van alle bestanden die niet beginnen met een nummer uit de map "/etc/grub.d" 

## Oefening 15 
Extra: Probeer alle voorbeelden van bestand globbing van het leerboek opnieuw. Oefening baart kunst ;-) 
