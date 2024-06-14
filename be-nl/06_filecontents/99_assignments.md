# Oefeningen op bestandsinhoud 

## Oefening 1 
Ontdek waarom je `less` zou moeten gebruiken in plaats van `more` 

## Oefening 2 
Toon de eerste regel van het bestand /proc/meminfo om erachter te komen hoeveel geheugen je aan je Ubuntu Virtual-machine hebt gegeven. 

## Oefening 3 
Toon de laatste regel van het bestand passwd in de map etc van de hoofdmap 

## Oefening 4 
Toon de eerste 4 tekens (=bytes) van het bestand /etc/passwd. Doorzoek de manpage van head om erachter te komen hoe dit moet. Je zou de naam van een bepaalde gebruiker moeten zien. Wie is deze gebruiker? 

## Oefening 5 
Gebruik cat om de volgende tekst in een nieuw bestand "mytextfile" in je homefolder te plaatsen:  
Dit is mijn tekst  
verdeeld over meerdere lijnen  
ingevoegd door cat. 

## Oefening 6 
Gebruik het commando `echo` drie keer om de volgende tekst in een nieuw bestand "myechotextfile" in je homefolder te plaatsen:  
Dit is mijn tekst  
verdeeld over meerdere lijnen  
ingevoegd door echo. 

Moeilijker: Het is ook mogelijk om dit te doen met slechts één `echo` commando. Maar je zal moeten zoeken naar de juiste optie om te ontsnappen aan karakters in de manpage van 'echo' 

## Oefening 7 
Gebruik cat om het bestand .bashrc in je homefolder te kopiëren naar een nieuw bestand met de naam .bashrc.backup 

## Oefening 8 
Wanneer je een nieuwe gebruiker toevoegt, wordt een nieuwe regel toegevoegd aan het bestand /etc/passwd. Toon de inhoud van dit bestand, maar in de volgorde van nieuwste gebruiker naar oudste gebruiker (andersom dan normaal)  

## Oefening 9 
Gebruik het commando tail om het bestand /var/log/auth.log open te houden, zodat je alle nieuwe logboekvermeldingen ziet verschijnen wanneer ze zich voordoen. (Je kan een paar keer op enter drukken om de nieuwe komende regels te scheiden) Start in een nieuw Powershell-venster een nieuwe ssh-sessie en meld je aan. Log vervolgens opnieuw uit. Wat zag je in de logboeken? 

## Oefening 10 
Open het configuratiebestand van ssh, `/etc/ssh/sshd_config`, met het _less_ commando en probeer met de zoekfunctie om te zoeken naar X11. Dit is iets dat we later zullen gebruiken om schermen via SSH te openen. 

## Oefening 11 
Gebruik nano om de tekst te bewerken in het bestand "myechotextfile" dat je eerder in je homefolder hebt gemaakt:  
Dit is mijn tekst, bewerkt,  
nog steeds verdeeld over meerdere lijnen  
Ingevoegd door Echo en bewerkt door Nano.  

## Oefening 12 
Gebruik cat met de eindmarkering "LinuxIsFun" om de tekst te overschrijven in het bestand "myechotextfile" dat je eerder in je homefolder hebt gemaakt:  
Deze tekst is veel interessanter.  
Ik gebruik nog steeds meerdere lijnen d'oh,  
gewoon omdat het kan.  

## Oefening 13 
Druk de volledige inhoud van de eerder gemaakte bestanden "mytextfile" en "myechotextfile" af met slechts één commando. 

## Oefening 14 
Haal de laatste 10 aangemaakte gebruikers op en zet ze in het bestand "nieuwsteUsers" met slechts één commando. 

## Oefening 15 
a. Open een nieuw bestand, genaamd _Linus Torvalds_ met `nano`. Kopieer de volgende tekst naar de nano-editor. 

```
linus Benedict torvalds, * , is a Finnish-American software engineer who is the creator and, historically, the main developer of the Linux kernel, used by Linux distributions and other operating systems such as Android. 
He also created the distributed version control system Git.

linus torvalds was born in Helsinki, Finland. His parents were campus radicals at the University of Helsinki in the 1960s. 
linus torvalds was born in Helsinki, Finland. His parents were campus radicals at the University of Helsinki in the 1960s. 

Torvalds attended the University of Helsinki from 1988 to 1996, graduating with a master's degree in computer science.
His academic career was interrupted after his first year of study when he joined the Finnish Navy Nyland Brigade in the summer of 1989, selecting the 11-month officer training program to fulfill the mandatory military service of Finland. 

He gained the rank of second lieutenant, with the role of an artillery observer. 

He bought computer science professor Andrew Tanenbaum's book Operating Systems: Design and Implementation, in which Tanenbaum describes MINIX, an educational stripped-down version of Unix. In 1990, Torvalds resumed his university studies, and was exposed to Unix for the first time.His MSc thesis was titled Linux: A Portable Operating System.

His interest in computers began with a Commodore VIC-20 at the age of 11 in 1981. He started programming for it in BASIC, then later by directly accessing the 6502 CPU in machine code (he did not utilize assembly language).
He wrote a Pac-Man clone, Cool Man. 

On 5 January 1991 he purchased an Intel 80386-based clone of IBM PC before receiving his MINIX copy, which in turn enabled him to begin work on Linux.

The first Linux prototypes were publicly released in late 1991. Version 1.0 was released on 14 March 1994.

Torvalds first encountered the GNU Project in 1991 when another Swedish-speaking computer science student, Lars Wirzenius, took him to the University of Technology to listen to free software guru Richard Stallman's speech. Torvalds used _____ GNU General Public License version 2 (GPLv2) for his Linux kernel.

The history of Linux 
Linus was born 28 December 1969 in Finland
```

b. Sla de wijzigingen op en sluit nano af  
c. Open het bestand opnieuw met nano  
d. Zoek naar de tekst "1981" om te weten wat er dat jaar is gebeurd  
e. De tweede alinea bevat twee van dezelfde regels. Gebruik een sneltoets om een van de twee regels te verwijderen  
f. Zoek naar 'linus' en vervang dit door 'Linus'  
g. Selecteer alleen de tekst "born 28 December 1969" van de laatste regel. Knip het en plak het op de eerste regel waar het sterretje staat (\*)  
h. Zoek naar 'torvalds' en vervang dit door 'Torvalds'  
i. Ga naar regel 9, kolom 80. Vervang de punt (.) door een uitroepteken (!)  
j. Ga naar de laatste regel tekst. Knip de hele lijn weg. Maak de knip ongedaan. Voer de knip opnieuw uit.  
k. Gebruik Knippen en plakken om de laatste regel tekst naar de bovenkant van het document te verplaatsen  
l. Zoek in de help binnen nano om erachter te komen hoe je het 'totale aantal regels, woorden en tekens' kunt weergeven.  
m. Gebruik twee keer een sneltoets (ctrl+...) om nano op te slaan en af te sluiten 

## Oefening 16 
Gebruik het commando _head_ om alles in het bestand _/etc/passwd_ af te drukken, zonder het aantal regels in het bestand te kennen. Je zal in de manpage moeten zoeken naar een oplossing. Probeer dit nu met het commando _tail_. 

## Oefening 17 
We kunnen cat gebruiken om de inhoud van meerdere bestanden onder elkaar af te drukken, maar het is moeilijk om erachter te komen welk deel uit welk bestand komt.  
Controleer bijvoorbeeld: 
```bash
student@linux-ess:~$ cat mytextfile myechotextfile
This is my text
spaced over multiple lines
inserted by cat.
This text is way more interesting.
I still use multiple lines d'oh,
just because I can.
```
We hebben in dit hoofdstuk 2 commando's gezien waar we kunnen opgeven om ook de bestandsnaam af te drukken, controleer de manpages van de geziene commando's om erachter te komen welke 2 commando's kunnen worden gebruikt. Probeer ze uit en druk de volledige inhoud van de bestanden af met de bestandsnamen. 

## Optionele Oefening 
Gebruik het commando `vimtutor` om te leren hoe je vim gebruikt. Wat is er zo anders aan deze editor?  
