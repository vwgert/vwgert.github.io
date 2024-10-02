# Oefeningen op software 

In deze oefeningen gebruiken we `apt` in plaats van `apt-get` en `apt-cache`, wat oudere commando's zijn 

## Oefening 1 
Werk de lokale apt-cache bij. zo krijgt je de laatste informatie van de repositories  

## Oefening 2 
Upgrade alle pakketten die zijn geïnstalleerd met _apt_ naar de nieuwste beschikbare versie  

## Oefening 3 
Zoek met apt naar een pakket dat iets te maken heeft met 'usage and stats'. Je ziet `btop` als een van de resultaten. Installeer het pakket en voer de app uit  

## Oefening 4 
Zoek met apt naar een pakket dat iets te maken heeft met 'colorful cat''. Je ziet `lolcat` als een van de resultaten. Installeer het pakket en voer de volgende opdrachten uit:  
cd  
cat .bash_history  
lolcat .bash_history 

## Oefening 5 
Installeer met apt het pakket 'neofetch' en voer de app uit  

## Oefening 6 
Zoek met apt naar "the matrix" en zoek in de eerste 5 gepresenteerd packages naar het pakket dat lijkt op de weergave van de matrixfilm en installeer dit. Voer deze app uit 

## Oefening 7 
Verwijder het pakket btop van het systeem. Je zou het niet meer moeten kunnen uitvoeren  

## Oefening 8 
Toon een lijst van alle pakketten die zijn geïnstalleerd met apt. In de lijst ziet je één vermelding voor `caca-utils`. Zo niet, installeer dit pakket en controleer opnieuw. Zoek in de manpage van `apt` hoe je wat info van deze pakketten kunt zien. Je zal zien dat dit pakket verschillende hulpprogramma's bevat. Probeer de laatste twee. Tip: Je kunt op 'enter' drukken om verschillende dingen te zien. Gebruik `ctrl+c` om een hulpprogramma af te sluiten. 

## Oefening 9 
Zoek naar een snap pakket via de omschrijving "resource monitor"  

## Oefening 10 
Installeer de snap `bashtop`  

## Oefening 11 
voer bashtop uit 

## Oefening 12 
We krijgen geen info over de schijven. Dit komt omdat de snap machtigingen nodig heeft om verbonden te zijn met de mount-plug.  
Lees de informatie over de snap `bashtop` om een oplossing te vinden.  
Voer de opdracht uit om het probleem op te lossen  
Voer bashtop opnieuw uit 

## Oefening 13 
Toon een lijst met geïnstalleerde snaps  

## Oefening 14 
Verwijder de snap bashtop  

## Oefening 15 
Toon een lijst met geïnstalleerde snaps  

## Oefening 16 
Toon de geschiedenis van wijzigingen in snap en controleer of de snap verwijderd is

## Oefening 17 
Controleer of de snap 'asciiquarium' bestaat. Lees wat informatie over de snap, installeer deze en voer deze uit  

## Oefening 18 
Zip de _homedirectory_ van de gebruiker student (met alle bestanden en mappen) in een bestand genaamd _/tmp/myhomefolder.zip_.  
Bekijk de inhoud van het zipbestand om het resultaat te controleren.  

## Oefening 19 
Zoek in de manpage van zip om erachter te komen hoe je een bestand uit je zipbestand kunt verwijderen.  
Verwijder het bestand .bash_history uit het zipbestand _/tmp/myhomefolder.zip_  
Controleer de inhoud van het zipbestand.  

## Oefening 20 
Maak een map met de naam _zipdemo_ in de tijdelijke map (_/tmp_).  
Pak het zipbestand _myhomefolder.zip_ uit in de map _/tmp/zipdemo_  
Gebruik `tree` om te controleren of het proces met succes is voltooid. 

## Oefening 21 
Maak een tarball genaamd _/tmp/myhomefolder.tar.gz_ met de bestanden en mappen van de _homedirectory_ van de gebruiker student.  
Bekijk de inhoud van de tarfile om het resultaat te controleren.  
Maak een map met de naam _tardemo_ in de tijdelijke map (_/tmp_).  
Pak de tarball _myhomfolder.tar.gz_ uit in de directory _/tmp/tardemo_  

## Oefening 22 
Extra uitdaging: Probeer het bestand _.bashrc_ uit de tarball te verwijderen (oefening 21)  
Doorzoek de manpage van tar om een oplossing te vinden.  
Controleer de inhoud van de tarball aan het einde van de oefening. 

## Oefening 23 
Probeer google chrome te installeren op je ubuntu Desktop met de command line interface.  
Zoals je kunt zien wanneer je naar een download zoekt, vindt je alleen een .deb pakket om te downloaden. Gebruik dit pakket met dpkg om google chrome te installeren.  

Moeilijker: Probeer dit .deb pakket te downloaden met wget om de volledige installatie in je CLI te voltooien. 

