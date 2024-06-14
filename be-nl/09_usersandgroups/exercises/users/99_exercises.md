# Oefeningen op Gebruikers

## Oefening 1
De definitie van gebruikers wordt bewaard in het bestand /etc/passwd. Dit bestand heeft 1 regel voor elke gebruiker. Elk van deze lijnen is verdeeld in 7 velden, gescheiden door een ":". Geef een beschrijving van elk van deze velden: 

Field 1: ________<br />
Field 2: ________<br />
Field 3: ________<br />
Field 4: ________<br />
Field 5: ________<br />
Field 6: ________<br />
Field 7: ________<br />


## Oefening 2
In de begindagen van Unix bevatte het bestand /etc/passwd niet alleen gebruikersinformatie, het bevatte ook een gecodeerde versie van het wachtwoord. Dit was natuurlijk een zwak punt in de beveiliging van het Unix-systeem, omdat iedereen het /etc/passwd-bestand kan lezen en dus de gecodeerde wachtwoorden kan zien. Voor een hacker zou de volgende stap zijn om een tool te maken om deze wachtwoorden te decoderen, bijvoorbeeld: cracker. Nadat dit probleem was herkend, werd besloten dat de wachtwoorden in een ander bestand moesten worden bewaard. Dit bestand zou alleen toegankelijk zijn voor de root gebruiker, wiens ID wordt gebruikt om de passwd- en inlogprogramma's uit te voeren.  
Wat is de naam van het bestand met de gecodeerde wachtwoorden? 


## Oefening 3
Maak een gebruiker met de volgende kenmerken: 
gebruikersnaam:	    john<br />
gebruikers-ID:      1111<br />
Groep-ID:	        100 (=users)<br />
Beschrijving:	    John Doe<br />
Home-dir:	        /home/john<br />
Shell:		        /bin/bash<br />
  
   
## Oefening 4
Controleer de gewijzigde bestanden: 
Wat is er gewijzigd in het bestand /etc/passwd? 


## Oefening 5
Wat is er veranderd in het bestand /etc/shadow? 
  
?> <i class="fa-solid fa-circle-info"></i> Nadat een gebruiker is aangemaakt, wordt het wachtwoord ingesteld op "!", wat betekent dat deze naam niet kan worden gebruikt om in te loggen. Om dit mogelijk te maken moet je John een wachtwoord geven. Stel het wachtwoord van John in op "Januari". 

  
## Oefening 6
Wat is er gewijzigd in het bestand /etc/group? 


## Oefening 7
Wat is er veranderd in de directory /home? 


## Oefening 8
De gebruiker John is nu aangemaakt op je systeem. Nu zou John informatie over zichzelf moeten kunnen vragen.<br />  
Log in als John en voer de volgende opdracht uit: 
```bash
id
```

## Oefening 9
Verwijder de gebruiker John van je systeem met behulp van de opdracht: userdel –r john<br /> 
Wat is er gewijzigd in het bestand /etc/passwd? 


## Oefening 10
Wat is er veranderd in het bestand /etc/shadow? 


## Oefening 11
Wat is er veranderd in het bestand /etc/group?


## Oefening 12
Bestaat de directory /home/john nog? 


## Oefening 13
Maak een gebruiker Sarah, door alleen de gebruikersnaam op te geven en dat ze een thuismap moet hebben. 


## Oefening 14
Bekijk de bestanden die zijn gewijzigd<br /> 
Wat is er gewijzigd in het bestand /etc/passwd? 


## Oefening 15
Wat is er veranderd in het bestand /etc/shadow? 


## Oefening 16
Wat is er veranderd in het bestand /etc/group?


## Oefening 17
Wat is er veranderd in de directory /home? 


## Oefening 18
Geef de gebruiker Sarah een wachtwoord 


## Oefening 19
Probeer in te loggen als Sarah 


## Oefening 20
Verwijder de gebruiker Sarah, maar behoud haar thuismap 


## Oefening 21
Verwijder de thuismap van Sarah 