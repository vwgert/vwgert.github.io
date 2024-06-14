# Oefeningen op installatie
## Oefening 1 - Download Ubuntu Desktop
Linux heeft ook een desktopversie. Download [Ubuntu Desktop](https://ubuntu.com/download/desktop). 

![DownloadUbuntuDesktop](../images/02/GetUbuntuDesktop_Download_Ubuntu.png)

## Oefening 2 - Installeer Ubuntu Desktop 

Installeer [Ubuntu Desktop](https://ubuntu.com/download/desktop) in een nieuwe virtuele machine en verken de interface. 

### De nieuwe VM maken 
Om een nieuwe virtuele machine (VM) aan te maken in VMWare ga je naar het menu `File`>`New Virtual Machine`. De wizard voor het maken van een nieuwe VM wordt weergegeven. 

![VMware-bestand nieuwe VM](../images/02/VMware_File_New_VM.png) 

In het eerste scherm selecteren we de optie `Typical`: 

![VMware Installatie Standaard](../images/02/VMware_Typical.png) 

Vervolgens kiezen we voor `I will install the operating system later`:

![VMware installeert besturingssysteem later](../images/02/VMware_Operating_System_Later.png) 

Vervolgens kiezen we voor het besturingssysteem `Linux`. In de versie dropdown selecteren we `Ubuntu 64-bit`. Dit is de Linux-distributie die we tijdens de labs zullen gebruiken. 

![VMware Ubuntu 64bit](../images/02/VMware_Ubuntu_64bit.png) 

In het volgende scherm geven we de virtuele machine een naam. Je kunt ook een andere map opgeven om de virtuele machine op je computer op te slaan.  
  
?> <i class="fa fa-exclamation-circle" style="font-size:48px;color:red"></i> Let op dat je de bestanden van de VM niet opslaat in een map die gesynced wordt met de cloud (OneDrive, Dropbox, Google Drive)?. Je VM zal crashen en je zal alles in de VM kwijt zijn!  
  

![VMware noemt de VM](../images/02/LAB_VMware_Name_The_VM.png) 

In het volgende scherm configureren we de grootte van de virtuele harde schijf voor de VM. We zullen een schijf maken met 30 GB opslagruimte. Houd er rekening mee dat de schijfruimte enkel wordt ingenomen door het opslaan van bestanden (dus groeiend tot maximum 30 GB): 

![VMware-schijfgrootte](../images/02/LAB_VMware_Disk_Size.png) 

We moeten op `Customize Hardware` klikken om de virtuele machine verder te configureren: 

![VMware past hardware aan](../images/02/LAB_VMware_Customize_Hardware.png) 

We moeten het ISO-bestand van de Ubuntu-desktop nog koppelen aan het virtuele cd-rom-station. Dit doen we door `New CD/DVD` te selecteren en naar het gedownloade `iso` bestand te bladeren: 

![VMware Selecteer ISO](../images/02/LAB_VMware_Select_ISO.png) 

Klik op `Finish` en de virtuele machine wordt gemaakt. 

![VMware-afwerking](../images/02/LAB_VMware_Finish.png) 

We kunnen nu de UEFI bios nog instellen. Klik hiervoor op `Edit virtual machine settings`. 
  
![VMware-afwerking](../images/02/LAB_VMware_UEFI_1.png) 

Ga naar het tabblad `Options`, klik op `Advanced` en selecteer de optie `UEFI`. Hier vind je ook de instelling omtrent `Side channel mitigations` zou je daar straks een waarschuwing van krijgen tijdens het starten van de Virtuele Machine. 
  
![VMware-afwerking](../images/02/LAB_VMware_UEFI_2.png) 
  
Je kan de VM nu opstarten door op het groene pijltje te klikken. Hiermee wordt de virtuele machine opgestart en wordt het installatieproces uitgevoerd. 

![VMware-afwerking](../images/02/LAB_VMware_Start_VM.png) 

### Installatie Ubuntu Desktop 

?> <i class="fa-solid fa-circle-info"></i> Resulteert het opstarten van de VM in de fout `This host supports Intel VT-x, but Intel VT-x is diabled`? Dan moet je de VT-X-optie activeren in de BIOS van je laptop. Meer informatie is te vinden in [dit artikel](https://www.qtithow.com/2020/12/fix-error-this-host-supports-Intel-VT-x.html). 

Wanneer we de VM voor de eerste keer opstarten, moeten we op `enter` drukken of 30 seconden wachten: 

![Ubuntu_Desktop_First_Grub](../images/02/LAB_Ubuntu_Desktop_First_Grub.png) 

We moeten een paar seconden wachten tot de boot klaar is: 

![Ubuntu_Desktop_First_Boot_Screen](../images/02/LAB_Ubuntu_Desktop_First_Boot_Screen.png) 

In de volgende paar stappen zal er een installatieproces zijn dat we moeten doorlopen.  
We kiezen de taal:

![Ubuntu_Desktop_Try_Or_Install](../images/02/LAB_Ubuntu_Desktop_Install_Steps_01.png)

We specifiëren niets voor Accessibility:

![Ubuntu_Desktop_Keyboard_AZERTY](../images/02/LAB_Ubuntu_Desktop_Install_Steps_02.png)

We kiezen de juiste keyboard layout. Voor `azerty` selecteren we `Belgian`:
?> <i class="fa-solid fa-circle-info"></i> Indien je een QWERTY keyboard hebt, behoudt je best `English (US)`:


![Ubuntu_Desktop_Normal_Install](../images/02/LAB_Ubuntu_Desktop_Install_Steps_03.png)

We moeten kiezen voor wired connection omdat we deze Ubuntu in een virtuele omgeving draaien:

![Ubuntu_Desktop_Erase_Disk](../images/02/LAB_Ubuntu_Desktop_Install_Steps_04.png)

We maken de keuze om te installeren:

![Ubuntu_Desktop_Erase_Disk](../images/02/LAB_Ubuntu_Desktop_Install_Steps_05.png)

We kiezen er voor om de installatie verder manueel af te ronden:

![Ubuntu_Desktop_Erase_Disk](../images/02/LAB_Ubuntu_Desktop_Install_Steps_06.png)

We kiezen er voor om enkel de standaard selectie van applicaties te installeren:

![Ubuntu_Desktop_Erase_Disk](../images/02/LAB_Ubuntu_Desktop_Install_Steps_07.png)

We kiezen er voor om third-party software te installeren voor drivers en multimedia formats:

![Ubuntu_Desktop_Erase_Disk](../images/02/LAB_Ubuntu_Desktop_Install_Steps_08.png)

We kiezen er voor om de disk leeg te maken en Ubuntu Desktop er op te installeren:
?> <i class="fa-solid fa-circle-info"></i> Denk er aan dat je enkel de Virtuele Disk van je VM gaat ledigen en dit is een lege disk op dit moment. `De hard disk van jouw computer/laptop zal dus niet leeg gemaakt worden!`

![Ubuntu_Desktop_Erase_Disk](../images/02/LAB_Ubuntu_Desktop_Install_Steps_08b.png)

We specifiëren de gebruikersnaam en wachtwoord, en de computernaam:

![Ubuntu_Desktop_Write_Changes_To_Disk](../images/02/LAB_Ubuntu_Desktop_Install_Steps_09.png)


Als TimeZone klikken we op de kaart Brussel aan of schrijven we Europe/Brussels in het tekstvak:

![Ubuntu_Desktop_TimeZone_Brussels](../images/02/LAB_Ubuntu_Desktop_Install_Steps_11.png)

Klik op Install om verder te gaan:

![Ubuntu_Desktop_Username_and_Computername](../images/02/LAB_Ubuntu_Desktop_Install_Steps_12.png)

Nu moeten we wachten tot de installatie afgerond is:

![Ubuntu_Desktop_Installaton_Runs](../images/02/LAB_Ubuntu_Desktop_Install_Steps_13.png)

Van zodra de installatie afgerond is klikken we op `Restart Now` om de VM te herstarten:

![Ubuntu_Desktop_Reboot_After_Install](../images/02/LAB_Ubuntu_Desktop_Install_Steps_14.png)

Wanneer we het scherm zien waar ze vragen om de 'enter'-key te drukken, gaan we eerst in de settings van de Virtuele Machine :

![Ubuntu_Server_VM_Settings](../images/02/Ubuntu_Server_VM_Settings.png)

We vinken uit dat de CD/DVD geconnecteerd moet worden tijdens het booten van de VM (anders wordt telkens bij het opstarten van de VM de installatie opnieuw gestart!)

![Ubuntu_Server_Disable_CDROM](../images/02/Ubuntu_Server_Disable_CDROM.png)

Nu kunnen we drukken op de 'enter'-key om de installatie af te ronden door te herstarten (er zal dan gestart worden van de harde schijf waar de installatie op gebeurd is)

![Ubuntu_Desktop_Enter_to_Restart](../images/02/LAB_Ubuntu_Desktop_Install_Steps_15.png)

## Task 3 - Login for the first time

De allereerste keer dat we inloggen moeten we door de configuratieschermen:

![Ubuntu_Desktop_First_Login_Click_Student](../images/02/LAB_Ubuntu_Desktop_First_Login_Click_Student.png)

![Ubuntu_Desktop_First_Login_Enter_Password](../images/02/LAB_Ubuntu_Desktop_First_Login_Enter_Password.png)

![Ubuntu_Desktop_First_Login_Online_Accounts](../images/02/LAB_Ubuntu_Desktop_First_Login_SetupProfile_01.png)

![Ubuntu_Desktop_First_Login_Online_Accounts](../images/02/LAB_Ubuntu_Desktop_First_Login_SetupProfile_02.png)

![Ubuntu_Desktop_First_Login_LivePatch](../images/02/LAB_Ubuntu_Desktop_First_Login_SetupProfile_03.png)

![Ubuntu_Desktop_First_Login_Help_Improve](../images/02/LAB_Ubuntu_Desktop_First_Login_SetupProfile_04.png)


Nu zijn we klaar om Ubuntu Desktop verder te verkennen:

![Ubuntu_Desktop_First_Login_Privacy](../images/02/LAB_Ubuntu_Desktop_First_Login_SetupProfile_05.png)

## Oefening 4 - Maak een momentopname van de VM 

Voordat je iets anders doet, is het een goede gewoonte om een momentopname, oftewel snapshot, te maken. Als op een later tijdstip onze Ubuntu Desktop breekt, kunnen we altijd terugkeren naar deze momentopname. 
Het is een tijdsbesparing om terug te kunnen keren naar dit punt, omdat we anders het Linux-systeem opnieuw moeten installeren. 

Indien er nog updates wachtende zijn, kunnen we die nog eerst even doen.

![Ubuntu_Desktop_First_Login_Software_Updater](../images/02/LAB_Ubuntu_Desktop_First_Login_Software_Updater.png)

`Maak een momentopname van de Ubuntu Desktop VM, genaamd "Clean Install"` als volgt: 

_Sluit eerst de VM af..._

![Ubuntu_Desktop_Snapshot_Poweroff](../images/02/LAB_Ubuntu_Desktop_Snapshot_Poweroff.png)

![Ubuntu_Desktop_Snapshot_Poweroff_Confirm](../images/02/LAB_Ubuntu_Desktop_Snapshot_Poweroff_Confirm.png)


_VM/Snapshot/Take Snapshot..._
 
![Ubuntu_Desktop_Snapshot_Take_Snapshot](../images/02/LAB_Ubuntu_Desktop_Snapshot_Take_Snapshot.png)

![Ubuntu_Desktop_Snapshot_Take_Snapshot_Name](../images/02/LAB_Ubuntu_Desktop_Snapshot_Take_Snapshot_Name.png)


?> <i class="fa-solid fa-circle-info"></i> Op een later tijdstip kun je altijd teruggaan naar deze momentopname in de tijd met: 

_VM/Snapshot/Revert to Snapshot..._

![Ubuntu_Desktop_Snapshot_Revert_To_Snapshot](../images/02/LAB_Ubuntu_Desktop_Snapshot_Revert_To_Snapshot.png)

## Oefening 5 - Verken de desktopomgeving 
Probeer op de Ubuntu-desktopmachine de volgende suboefeningen uit te voeren:  
- Verander de desktopachtergrond
- Maak een nieuw tekstbestand met de tool "Text Editor" (= gedit) en probeer het op te slaan in je documentenmap  
- Controleer met de bestandsverkenner (Files) of het bestand bestaat  
- Verwijder het bestand en leeg de prullenbak  
- Pin (=Favorite) de Terminal-applicatie aan het Dock (=launcher)  
- Surf met Firefox naar de website van de school 
- Installeer de Chromium-webbrowser, start de app, maak deze vast aan het Dock en plaats deze boven het Firefox-pictogram  
- Surf met Chromium naar de school webmail portal 
- Installeer wps-office en test de apps  
- Installeer Spotify en test de app  
- Installeer Visual Studio Code en test de app  
- Installeer Gimp en bekijk de app 
