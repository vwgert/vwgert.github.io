## Lab <!-- {docsify-ignore} -->

In de volgende hoofdstukken installeert Linus een Webserver en Minetest Server. Voordat hij dat kan doen, moet hij een Linux-systeem in gebruik hebben. In dit lab zal hij een Linux Cloud Instance aanmaken op Amazon Web Services (AWS). Met deze infrastructuur opgezet zal hij in staat zijn om zijn Webserver en Minecraft Server op een later tijdstip te installeren, configureren en onderhouden. 

### Aanmaken van SSH keypair  

Vooraleer we de instance kunnen aanmaken hebben we een SSH keypair nodig om na creatie veilig te kunnen verbinden (= in te loggen) met deze instance.

Ga op *AWS* naar *EC2*.

![AWSCreateSSH](../images/01/02_lab/AWSCreateSSH_0_Compute.png)

Ga naar *Key Pairs* en maak een nieuwe aan

![AWSCreateSSH](../images/01/02_lab/AWSCreateSSH_1_KeyPairs.png)

![AWSCreateSSH](../images/01/02_lab/AWSCreateSSH_2_CreateKeyPair.png)

De private key zal automatisch gedownload worden door jouw browser naar het *Downloads*-mapje.

![AWSCreateSSH](../images/01/02_lab/AWSCreateSSH_3_KeyPairCreated.png)

Verplaats deze key naar het mapje .ssh onder jouw account *"C:\Users\\<jouw loginnaam>"*. Indien nodig maak je dit mapje zelf aan.

![AWSCreateSSH](../images/01/02_lab/AWSCreateSSH_4_KeyPairCut.png)

![AWSCreateSSH](../images/01/02_lab/AWSCreateSSH_5_KeyPairPaste.png)



### Aanmaken van de Cloud instance 

De Webserver en Minecraft Server draaien in een Linux Server Envrironment. Meer bepaald een Ubuntu Server.   

Ga op *AWS* naar *EC2*.

![AWSCreateInstance](../images/01/02_lab/AWSCreateInstance_0_Compute.png)

Zorg dat je je in de Regio *"N. Virginia"* bevindt en klik op *Launch instance*.

![AWSCreateInstance](../images/01/02_lab/AWSCreateInstance_1_LaunchInstance.png)

Vul de juiste gegevens in.

![AWSCreateInstance](../images/01/02_lab/AWSCreateInstance_2_InstanceSettings_1.png)

![AWSCreateInstance](../images/01/02_lab/AWSCreateInstance_2_InstanceSettings_2.png)

Je krijgt de melding dat de instance succesvol werd aangemaakt.

![AWSCreateInstance](../images/01/02_lab/AWSCreateInstance_3_SuccesFullInitiated.png)

Na een tijdje verandert de status Pending ook naar Running om aan te geven dat de server ook succesvol is  opgestart.

![AWSCreateInstance](../images/01/02_lab/AWSCreateInstance_4_RunningState.png)



### Een vast IP-adres toekennen (Elastic IP)

Iedere keer dat we een instance herstarten zal deze een ander IP adres (en DNS naam) krijgen. 

![AWSCreateInstance](../images/01/02_lab/AWSElasticIP_0_IPChange.png)





We gebruiken dit IP adres (of DNS naam) om te connecteren naar de server. Het is dus veel makkelijker indien de server hetzelfde IP adres (en DNS naam) zou houden in de toekomst. 

Om het veranderen van IP adres te voorkomen, zullen we de instance een Elastic (=static) IP moeten geven.

Ga op *AWS* naar *EC2*.

![AWSCreateInstance](../images/01/02_lab/AWSElasticIP_1_Compute.png)



Klik op *Elastic IPs* en vervolgens op *Allocate Elastic IP address*.

![AWSCreateInstance](../images/01/02_lab/AWSElasticIP_2_AllocateElasticIP.png)



We maken een nieuw Elastic IP aan door op *Allocate* te klikken.

![AWSCreateInstance](../images/01/02_lab/AWSElasticIP_3_CreateElasticIP.png)



Klik op *Actions* en vervolgens op *Associate Elastic IP address*.

![AWSCreateInstance](../images/01/02_lab/AWSElasticIP_4_AssociateElasticIP.png)



Selecteer de *Instance* waar dit Elastic IP adres aan gekoppeld moet worden en klik op *Associate*.

![AWSCreateInstance](../images/01/02_lab/AWSElasticIP_5_Associate.png)



Het Elastic IP adres is succesvol gekoppeld aan onze server instance.

![AWSCreateInstance](../images/01/02_lab/AWSElasticIP_6_Success.png)

We zien dat dit gelukt is als we opnieuw naar de Instance gaan kijken. Wanneer we nu de instance gaan stoppen en nadien opnieuw starten, dan zal het IP adres en bijhorende DNS naam hetzelfde blijven.

![AWSCreateInstance](../images/01/02_lab/AWSElasticIP_7_Success_2.png)







### Connecteren naar de Cloud instance

Om op de server instance te werken gaan we best over SSH een connectie starten vanop onze laptop. Om de gegevens die hiervoor nodig zijn op te vragen doen we het volgende.

Klik *Instances*. Selecteer vervolgens de server-instance en klik op *Connect*.

![AWSCreateInstance](../images/01/02_lab/AWSConnectInstance_0_Connect.png)





AWS stelt een SSH-commando voor met een bepaalde key. 
Maar let op, onze key op de laptop kan anders noemen als je andere stappen hebt gevolgd tijdens het aanmaken van het SSH-keypair of indien je reeds een keypair had.

![AWSCreateInstance](../images/01/02_lab/AWSConnectInstance_1_CopyCommand.png)





We starten een Powershell of Windows Terminal en plakken het commando, maar passen indien nodig de naam van onze key aan.

Plakken kan in een Powershell venster door op de rechtermuisknop te klikken.

![AWSCreateInstance](../images/01/02_lab/AWSConnectInstance_2_Connect_Logout.png)

Zoals je in vorige screenshot kan zien zijn we dan ingelogd op de server. Indien je de connectie wenst te verlaten kan je het commando *exit* of *logout* geven.





Als wijze van oefening start je opnieuw een ssh-sessie met de instance en pas je de *naam* van de server aan naar *linux-ess* met het commando:

***sudo hostnamectl set-hostname linux-ess***



![image-20240618102237878](../images/01/02_lab/image-20240618102237878.png)