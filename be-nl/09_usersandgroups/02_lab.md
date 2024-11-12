# Lab <!-- {docsify-ignore} -->

Linus heeft een vriend, genaamd Dennis,  die ook wil meehelpen met het project. 



Linus maakt een nieuwe gebruiker *dennis* aan voor hem op de server

```
ubuntu@aws-linux-ess:~$ sudo useradd -m -c "Dennis Ritchie" -s /bin/bash dennis
```



Hij geeft hem een tijdelijk eerste wachtwoord *pxl*

```
ubuntu@aws-linux-ess:~$ sudo passwd dennis
```



Hij geeft Dennis ook sudo rechten om de nginx-server te herstarten zonder dat deze hiervoor een paswoord dient op te geven

```
ubuntu@aws-linux-ess:~$ which systemctl                                   # om het volledig pad van het commando op te zoeken
/usr/bin/systemctl
ubuntu@aws-linux-ess:~$ sudo visudo

Toevoegen onderaan:
dennis ALL=(ALL) NOPASSWD: /usr/bin/systemctl restart nginx

ubuntu@aws-linux-ess:~$ sudo -l -U dennis                                # om te testen of de sudoers file ok is voor Dennis
Matching Defaults entries for dennis on ubserv:
    env_reset, mail_badpass,
    secure_path=/usr/local/sbin\:/usr/local/bin\:/usr/sbin\:/usr/bin\:/sbin\:/bin\:/snap/bin,
    use_pty

User dennis may run the following commands on ubserv:
    (ALL) NOPASSWD: /usr/bin/systemctl restart nginx

ubuntu@aws-linux-ess:~$ su - dennis                                      # switchen naar de user dennis
dennis@aws-linux-ess:~$ sudo systemctl restart nginx                     # testen of dennis de nginx service mag herstarten
dennis@aws-linux-ess:~$ exit

```



Tevens maakt Linus een nieuw ssh -keypair voor Dennis (want Dennis heeft nog geen keypair)

```
ubuntu@aws-linux-ess:~$ su - dennis                                      # switchen naar de user dennis
dennis@aws-linux-ess:~$ ssh-keygen -t ecdsa -C "dennis@aws-linux-ess"    # driemaal enter om te antwoorden op de vragen

```



Dit proces heeft een public key en een private key aangemaakt in de folder .ssh van de homefolder van de gebruiker Linus. We kopiëren de inhoud van de public key naar een file genaamd *authorized_keys*.  Tracht te achterhalen wat de bedoeling is van de file *authorised_keys*.

```
dennis@linux-ess:~$ cd .ssh
dennis@linux-ess:~/.ssh$ ls
id_ecdsa   id_ecdsa.pub
dennis@linux-ess:~/.ssh$ cat id_ecdsa.pub >> authorized_keys
dennis@linux-ess:~/.ssh$ exit

```



Linus download de private key van Dennis naar zijn laptop zodanig dat hij deze kan doormailen. Eerst moet hij de private key wel even in zijn eigen homefolder zetten om deze te kunnen overbrengen via scp

```
ubuntu@aws-linux-ess:~$ sudo cp /home/dennis/.ssh/id_ecdsa .
ubuntu@aws-linux-ess:~$ sudo chmod o+r id_ecdsa								   # om rechten te geven voor scp via user ubuntu
ubuntu@aws-linux-ess:~$ exit
```



In een nieuw powershell venster download Linus de key

```
Powershell > scp -i ".ssh/privatekeyfile.pem" ubuntu@ipvandeserver:id_ecdsa .  # om de key te downloaden van de server
```



Tevens test hij of hij kan inloggen als dennis op de server met behulp van deze public key

```
Powershell > ssh -i ".\id_ecdsa" dennis@ipvandeserver						   # om de key te testen met het inloggen als dennis
dennis@aws-linux-ess:~$ exit
Powershell > 
```



Linus kan deze key nu doormailen naar Dennis

