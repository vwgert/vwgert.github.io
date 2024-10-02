# Lab <!-- {docsify-ignore} -->

 

### **Uitzetten van de systembell in de Ubuntu instance**

Indien je het vrij vervelend vindt om steeds de systembell te horen bij een tab-completion, dan kan je deze uitzetten:

- via de file */etc/inputrc*

OF

- via het verwijderen van de pcspkr -kernelmodule

***sudo nano /etc/inputrc***

![img](../images/05/AD_4nXeZpL1XR2jQF9fMJUmBWtbQeJC2SpwNVmOCga_oSciOUCFcf7zftSTPjz29KgLmU5l_3OBj0tpNJJX4xqibmTUtaYKYqO8xnBR-sZB1BcAvuZq_hz1pAm-f0d5IqYK5K2ZlYMtsAZCO15q32AVL5-Z-r1-U.png)

Haal de regel *set bell-style none* uit commentaar door het hekje vooraan weg te halen.

De ssh-sessie verlaten en opnieuw aanmelden over ssh om het resultaat te bekomen.

Als dat niet werkt, dan kan je het proberen met het verwijderen van de pc-speaker-kernelmodule (als deze geïmplementeerd is) met

***sudo rmmod pcspkr***



### **De webserver installeren** 

We installeren de nginx-webserver. Maar eerst updaten we alle geïnstalleerde pakketten naar hun laatste versie.



​	***sudo apt update*** 

​	- dit zorgt er voor dat de computer de laatste versies van alle pakketten kent

![img](../images/05/AD_4nXffuw5rrfCzwTQrTOOKR8mpAeBiwvbMUo59GttyvPVwu2xqvQTwA-Jpp21X15v0hvwBv-xbCQ2KBso9teViK0moZZ80z218Xwq__9h3XJs_HWrpskv5iBMRouLhXdft6biPeUT-l1tjoy4fkQdD8wtW3n4.png)

​	

***sudo apt -y upgrade***

​	- dit upgrade alle pakketten naar hun laatste versie![img](../images/05/AD_4nXdGNtqaOrbp_wIyLD6aJ3n1FOb3OFEoQ0LUFWAoR70YJznoe2dkXWFmz06BejlOfm3FuKwusqtU1Sxwi6QW6zzS9wHQ9gBwSgX11BPYJw67vJ1f6Eqlr-72ERTdYHd82ZMSOikTUlvjKApS3RXuRasioMY1.png)

![img](../images/05/AD_4nXfcJNEVEMX-vtiFq-b_CW7opmtyQHalgoKRDUzFL3Hz6AJW8gZ2SKtKcXf6QxOJ762LdE8eLsTuNKzONxCqTWOjFsYu12Mwu5Wn5rTFunpwKgo4OIRKE0jy-TzGW1DCLX_EtOf5HuEPDrwx7Ioe4uc37vY.png)





Herstart de Webserver-Instance met 
**sudo reboot**

![img](../images/05/AD_4nXewrU_Ii3JCeJSkbrnfDb7uLWZBZcG4tIcfkhCaqyLEOMTUhtieuRWvkTVMJFjbDXkMlKSZSeP6f6t61n252jMZe56wTRtoyWEZV7NvlhHHT9kskhcyVcUDkBIHwJMZg2-m1X6DbDXlT1fFEZQhbKY-HMYI.png)



Nu installeren we de webserver met
***sudo apt -y install nginx***

​	- dit installeert de nginx-webserver

![img](../images/05/AD_4nXdeOYx_ssXxMG1yDdzycWxZ_Vai2BvCy2kkzPiWeTJrUkDXRp17kOd5UNaW7X2wXv72CaD0OB2cOfHAFGH2B_Yt3akmI4-hWZVf3gjugnsTq50MXxCW2AD9k7UEngG-XYR0ddyN4YMVFR2qYCkXPvmvsTbn.png)



​	We controleren of 

- nginx draait
- er wordt geluisterd op  poort 80

![img](../images/05/AD_4nXdUOi0U51gEFUDLKkpcheqsIQUc58HoLjSjgyrHTQuXIWSM71s94iXoaqZ3neZSsmsvPA09yLEtAwij8UZSmGDOEJ6FfIYZDRlEovB0XO7kdxfkdQep8CW30ZSDwrcxLvs5YSeuAyxwg4Psso9r7dOsRTE.png)

![img](../images/05/AD_4nXeYwxhsO51zFFUA9NV1wZM_AZWxB873_1DRBJzWn1Y-G6c-GxityjTPDfYRAEqVTC2S8xd5oO3dfgH35vTL1J9DCThkuTVyypCG2NJJ2Cemi_vbhG40PpiQ0gmcvJgAmHFlir_ja1fNTH4FlOOt6xpU8VgC.png)



### **De webserver lokaal testen** 

We testen lokaal of de webserver werkt. Omdat we op een Linux Server zitten en geen GUI hebben, moeten we dit dus doen met een Text-based-browser

- installeer lynx 

![img](../images/05/AD_4nXeYN69F8nQlwGjF1e5HTg78Yq-mW3j7AnwyJ3hgArQo2RbCLApj0X1MqzTtaak3HaROboXDGZBRgmvVC99xa6W242S0lV6vNa8xwK-ob3P_WNXzxutqjAurGRKfhNxEZSy6HF8E5vE8JVXvqztnzUh1S1LU.png)

- en surf naar 127.0.0.1

![img](../images/05/AD_4nXcRwx6itzeFKQ38bpTkjgV2FtZDgU3fL-w_Ss24PYuLI0lIkPYeWDX2nGLNj9SWczys6kigq9JHo2BW5WeRgrgXdDJrDFnGcybd_MrbO-g0Yv-stV9Cnr3RmsgoOLGkIIRqXTLcYiu4kl0zhLeKxGogKF1I.png)

- of surf naar localhost

![img](../images/05/AD_4nXcDsUMYMFXx9saoD1_Pr5TNLu45723zxG-5DoKblwLZj6mLyH-9ddlVIKW4NeOljpz9VbzzLXTV-oRlhG0veeGK1gKh3NSEoGOiRr44tqqlceXQczq6K6fDPFsMdpAlk-3tbGe0rLSjf8zUEco3UI3ol3P1.png)

Je zou op onderstaande pagina moeten uitkomen. De webbrowser verlaten doe je met *Q*

![img](../images/05/AD_4nXfSo75rpMprepMs3phlFWfpWDxj9vMGfOGkTrq7jc-Y8teWpA2lUsV3v869Mp0IiRgBJVLAi6bZIVkg51hlH8R9ciBp3T9rwhxg979j87wHHngC38b_mQavq7GX-TqQHna2V0X3LjR_XC_yDBiChozePHJm.png)



### **De webserver vanop de laptop testen en Firewall aanpassen**

Surf vanop je laptop naar het publieke IP van de website over **http** (voor het testen van poort 80)

![img](../images/05/AD_4nXd2tqvpoexDAHMhTS1U72lIJC3n0VJP6iAaJrUMDmIZLlyiSC_XMAjW10aaFNQroAh3aw6lKJT2ACsuM3aDD_D7IXn0tgmj1Q85CSeAIqAnw0xWtcv5615DGQKJLYwvcDnHgKB0Q9GZg792HTP5BJntpP7z.png)



De website blijft een heel aantal minuten gewoon hangen bij het laden

![img](../images/05/AD_4nXf85uQOui-9oeRUFoSKUjbDDD3g4ZPIDtNrEoLEA3bTMZSsWosHwaUNQoXoIiKcdXr_VWPoKWFTABZ7itNuQPfME78z577IQK7kHK_32I8Qo2po-h1wXgCYptE88RHycPIknQJYDKUfE70HbQBvCkrjtdr8.png)



Na een hele tijd krijgen we *The connection was reset*.  ![img](../images/05/AD_4nXdldFE0L2e1QyItb0UlK4jJvUH9LBSaxU5qqrNCNQjBAv63CwI1dBdE1XG9xaIUB9fESdhISLYH5QWp_HdgFDJKwVixgL2IIO251CzYS6vhDjKERLLBg0vr5wQEVp1nnKKSxwYthi0MIzHhKVKpVDoPlqWG.png)

Het blijkt dus nog niet te werken!



Omdat dit niet werkt zoeken we uit of er http-traffic aankomt op de Webserver

- ***sudo tcpdump -i enX0 port 80***            (als enX0 de naam is van jouw NIC, wat je kan zien met het commando *ip a*. De naam had ook iets kunnen zijn als eth0 of enp0s3 of ens33 of ...)
- We surfen over http van de laptop naar het extern IP-adres van de Webserver (of refreshen)
- We kijken wat er toekomt en vertrekt van pakketjes op de Webserver

![img](../images/05/AD_4nXdog3DLneu6wPmcj68yoqOrwuc3xMa6elaLCHD4ZwkK6MLuPum78pRQr3qmeuwf1SN7_h6VX6nyIG50-nHaftgnJ3gsncQqDW08GJaqhNaXK-kbMxPWAYIBl9CP3fV3dTLOxdsep203Cl69_jw27m4GB3w.png)

We zien dat er geen enkel pakketje aankomt. Er komt dus geen externe trafiek binnen op de webserver. De trafiek wordt voordien al ergens weggefilterd.

Stop het sniffen met *CTRL-C*

![img](../images/05/AD_4nXfUH9KCv0LUL-4MrJvc-4baJyfsR_5klhuWusMlrLJFHdSSTkGkGKP9HMbAq3naBIj8tXcAZVDGKOVcXc2VloeAfQJlyWlKGtZy-BS_b0ZhOJWFukZN9V0Izt_hlUCfC24BkAGKBcL1mtJ-5X9REaHu8L8d.png)

PS: Het kan zijn dat je toch wat pakketjes ziet die komen van een APIPA adres (=169.254.0.0/16), maar niet van een extern IP 

![img](../images/05/AD_4nXfFtVH73fwHMcBLPXCKV8z6VbmWa2wC8EFZdmfDvxv6v7tpxPK4f9PM89wuY9YePEkUNYu6bO6FVXaOYgwEQiLF1RgWi-zQA7j2g3yL7t8YNo4jkhvDdyB95Tf9Z385S4hb6DE5R5uxSTFsg-cdjyTg1_Im.png)

Het surfen werkt niet omdat de trafiek wordt weggefilterd op AWS-niveau en meer bepaald via de Security Group. Dit moeten we dus oplossen.



### **Toevoegen van een nieuwe inbound rule in de Security Group die inkomende trafiek naar poort 80 toelaat.**



Klik op de *Security Group* om deze aan te passen![img](../images/05/AD_4nXfajb5p1DJuextkhIyQjVkPr6-pYjuf7zZXDMxqHQPMxkl86nyjMR-tWwXXazdvSH3gYjRRNkt03dI4fEKD32HABQ9L6lt6ifvJ0qlHhAwP6Wa6ULABqeOWjw_BB64a2xQxpSAQGQ3dxOwJM-PUNLsa4bg.png)



Klik op *Edit inbound rules*![img](../images/05/AD_4nXeCqyqSnnHrg4edeJnBXRW2lBDOkbAs_k0wFcma3FVtI7kS0Gt-rTTIfVKbCKMR6rlgqyziFpn5OTXLN0GA4n_qGUyEGQunmIKPTlqWi8Jatdpk-46rs6Vo2HZYwCtSte--tgOCWnm0WW_PUu94Jym0D8vl.png)



Klik op *Add rule* en voeg een rule toe die inkomend HTTP verkeer toelaat over IPv4 van overal![img](../images/05/AD_4nXcLguEadlaOzr4hZRxQTUTWKt9LUE2RHDNovFIKMN1tOiKmoHqAPOocsL0b2nvP_5-0ANMxJVIJmzQex7LRjopIAr-dUl-Gd5kzmQZ6UddkWxC1qLzOcUf86ArHzyDBf8ajPZ5tBCD_PTdq5bRuxfRbGp4k.png)



Het toevoegen is gelukt![img](../images/05/AD_4nXfPiAA-HRGSvo6jyz7EQtibgU1cq_vQ2NUfCUWb-EO8aJxUgqPTGCh-znPOhPTis6OcDmevLtQhbgKA9w-XRW39TXwuaV-nZQX-RoqxWAqPZmGSB3Hq2ExKlpGEnC6gLpB2rrHAva8QLhVATaKzsUJ-p8s.png)



We gaan opnieuw testen of het surfen werkt

We beginnen eerst met sniffen…

- sudo tcpdump -i eth0 port 80            (als eth0 de naam is van jouw NIC)
- We surfen opnieuw vanaf de laptop naar het extern IP-adres van de Webserver via http (of Refresh)
- We kijken wat er toekomt en vertrekt van pakketjes![img](../images/05/AD_4nXdZm4lGoI4c02OmNrJMtfZ9Y67A_S-JaCRG9UrXUvzS-miQ5MsWGwDFJV7htErw6-z-4V-89mGbJTeQNQJzjiZCopNxn9EaR_F5Cgr-gHDNZgBcORI50pBcSJFRFI140Df7xdDQh-Pbo8H2vsz-rMJKCysP.png)



We zien dat er nu wel pakketjes aankomen van een extern adres en terug vertrekken naar dat extern adres.![img](../images/05/AD_4nXddqPxKYDwjlVYi-GciVtN6XQ5dX9z-lMIdzRc8nYTYYY9ySy6pYtnmTxnDR5ry-UPPR8sW7YUwZHrDMzdphRkrJdz9Bw9PwjuZQ3BDAHPS0MhguVX1fNxfbKT0v8POAEcCSnY_r__I3W4GLxHgcadLYRBg.png)

De website werkt!
