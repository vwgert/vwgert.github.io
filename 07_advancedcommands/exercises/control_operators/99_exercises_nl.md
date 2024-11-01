# Oefeningen op Besturingsoperators

## Oefening 1 
Als je in het verleden aliassen hebt gemaakt voor de commando's rm, cp en mv, moet je ze verwijderen. Je kan ze vinden in de bestanden ~/.bashrc of ~/.bash_aliases. Verwijder deze regels uit die bestanden en start een nieuwe shell door een nieuw terminalvenster te openen, ssh-sessie, opnieuw in te loggen of 'bash' te typen. 

## Oefening 2 
Maak een commando die tijdens het verwijderen van het bestand "test": 
- de foutmeldingen onderdrukt door ze naar het zwarte gat te sturen (device `null`) 
- de tekst "Met succes verwijderd!" toont wanneer het bestand met succes is verwijderd 
- de tekst "Kon het bestand niet verwijderen!" geeft wanneer de bestanden niet konden worden verwijderd 

## Oefening 3 
Stel je voor dat je een back-up moet maken van alle homefolders naar de map /backup. Nadat de back-up is gekopieerd, moet de pc worden afgesloten. Helaas moet je gaan. Hoe kun je dit doen zodat je nu kunt vertrekken. Probeer dit eens.  

?> <i class="fa-solid fa-circle-info"></i> Een goede back-up houdt ook de tijdstempels en eigenaars van het bestand in tact!  

## Oefening 4 
Maak een map bron en een map bestemming in je homefolder. Maak ook een tekstbestand met de naam "belangrijk.txt" in de map bron. Je moet dit bestand naar de map bestemming kopiëren. Als de kopie is geslaagd, kan je de map bron verwijderen met de opdracht rm -rf. Hoe kun je dit doen met slechts één opdrachtregel? Probeer dit eens.. 

## Oefening 5 
Wat is de uitvoer van: (Probeer te antwoorden zonder het eerst in de terminal te typen)  
```bash 
echo Hello#world 
```

## Oefening 6 
Wat is de uitvoer van: (Probeer te antwoorden zonder het eerst in de terminal te typen) 
```bash 
echo Hello #world 
```

## Oefening 7 
Wat is de uitvoer van: (Probeer te antwoorden zonder het eerst in de terminal te typen) 
```bash 
echo \\\\\??\#\"\ \\ #\\
```

## Oefening 8 
Wijzig de foutuitvoer van de opdracht ls in: "Ik kan dit bestand of deze map niet vinden, sorry". De werking van het commando moet hetzelfde blijven. 