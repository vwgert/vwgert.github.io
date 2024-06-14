# Assignments on command line
# Oefeningen op de command line

Voer de eerste oefeningen uit terwijl je de cli op de Ubuntu Server gebruikt (geen ssh).  

## Oefening 1 
Maak gebruik van het commando `man` om erachter te komen wat het commando `man -f` doet en met welk ander commando het vervangen kan worden. 

## Oefening 2 
Maak gebruik van het commando `man` om erachter te komen wat de optie is voor het commando `shutdown` om de machine opnieuw op te starten in plaats van uit te schakelen. 

## Oefening 3 
Gebruik het commando `apropos` en/of het commando `man -k` om het juiste commando te vinden om: 
- je VM te herstarten (__reboot__)
- je wachtwoord of het wachtwoord van een andere gebruiker te wijzigen (__password__ / __user__)
- de inhoud van een folder te tonen (__contents__)
- het terminalscherm leeg te maken (__clear__)
- te zien wie er ingelogd is --> probeer alle commando's (__logged in__/__on__)
- te zien hoeveel vrij geheugen de server heeft --> zoek in de manpage van dit commando hoe je de uitvoer kan tonen in human readable formaat (__memory__)
- te zien hoeveel vrije schuifruimte je hebt (__disk space__) 

## Oefening 4 
Gebruik de manpage van `ls` om erachter te komen hoe je ook de verborgen bestanden zou kunnen zien. Toon de verborgen bestanden van je homefolder. 

## Oefening 5  
Probeer alleen de korte beschrijving van het commando `ls` te tonen. 

## Oefening 6  
Probeer erachter te komen waar het commando `reboot` en zijn manpage op je schijf zijn opgeslagen. 

## Oefening 7 
Maak verbinding met je server via SSH en blijf verbonden voor de oefeningen. Het voordeel is dat je nu met je muis door je schermen kunt scrollen. 

## Oefening 8  
Voer het commando `cd` uit. Voer het commando uit om ook de verborgen bestanden in deze map weer te geven. Voer vervolgens het commando `cat .bashrc` uit. Dit bestand bevat een script dat wordt uitgevoerd elke keer je een nieuwe shell opent (bijv. Terminalvenster). We zullen het in een latere les nog uitleggen. Voer het commando uit om het scherm leeg te maken. 

## Oefening 9  
Gebruik de pijltjestoetsen om naar het commando `cat .bashrc` te gaan en gebruik de pijltjestoetsen opnieuw om het te veranderen naar `cat .bash_history`. Druk op enter om het commando uit te voeren. Dit bestand bevat je geschiedenis. Het ontvangt je geschiedenis van opdrachten wanneer je een shell sluit (terminalvenster sluiten, uitloggen, ...). Je ziet de laatste opdrachten die je in deze shell hebt getypt niet. 

## Oefening 10 
Voer het commando uit om je server onmiddellijk af te sluiten. Start je server opnieuw op via VMware Workstation. 
Maak verbinding met je server via SSH en blijf verbonden voor de oefeningen. Als het niet werkt, moet je het IP-adres van de server controleren (van VMware Workstation). 
Probeer de geschiedenis te gebruiken om het commando `cat .bash_history` opnieuw uit te voeren. Je zal nu zien dat de opdrachten van de sessie zijn toegevoegd voordat je opnieuw opstartte. Telkens wanneer je een nieuwe shell start, worden de opdrachten uit dit bestand gekopieerd naar het geheugen van de shell, zodat we de geschiedenis kunnen gebruiken. 

## Oefening 11 
Voer het commando `echo Dit is het echo-commando met een spatie ervoor`. Let op de spatie aan het begin van de regel, vóór het echocommando. 
Voer het commando `echo Dit is het echo-commando zonder een spatie ervoor` uit. Merk op dat er hier geen spatie is voor het echocommando. 
Typ history om je geschiedenis te controleren. 
Je zal merken dat opdrachten die met een spatie zijn begonnen, niet in de geschiedenis worden bewaard. 
Voer het commando `ls -a` uit. 
Voer hetzelfde commando `ls -a` opnieuw uit. 
Typ history om je geschiedenis te controleren. 
Je zal merken dat het herhalen van dezelfde opdracht achter elkaar alleen het eerste voorval in de geschiedenis zal behouden. 

## Oefening 12 
Voer het commando `apt install sl` uit. Je zult merken dat er meer privileges nodig zijn. We moeten deze opdracht opnieuw uitvoeren met rootrechten. Voer het commando `sudo !!` uit om het laatste commando opnieuw uit te voeren met sudo voorop. `sl` is een commando om mensen die `ls` verkeerd typen te foppen. Typ `sl` en druk op `enter`. 

## Oefening 13 
Druk de toetscombinatie `CTRL-R` in en typ `shu` om te zoeken naar het laatst gebruikte shutdown commando. Gebruik de pijl naar rechts om de regel te bewerken en wijzig de opdracht in `sudo shutdown -r now` en druk op enter om je server opnieuw op te starten. Je kan het opstartproces volgen in VMware Workstation. Maak verbinding met je server via SSH en blijf verbonden voor de oefeningen. Als het niet werkt, moet je het IP-adres van de server controleren (van VMware Workstation). 

## Oefening 14 
Druk de toetscombinatie `CTRL-R` in en typ `shu` om te zoeken naar het laatst gebruikte shutdown commando. We zien het commando `sudo shutdown -r now`. We willen de server __niet__ opnieuw opstarten. Dus drukken we nogmaals de toetsencombinatie `CTRL-R` in om naar een ouder commando te gaan dat `shu` in de naam heeft. Blijf de toetsencombinatie herhalen totdat je het commando `sudo shutdown now` ziet en druk op enter. 

## Oefening 15 
Probeer verbinding te maken van de Ubuntu Desktop naar de Ubuntu Server via ssh.  

## Oefening 16 
Installeer `Windows Terminal` op je Windows-laptop via de `Microsoft Store`. Probeer verbinding te maken vanaf de Windows Terminal met de Ubuntu Server via ssh.  