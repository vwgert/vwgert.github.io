# Lab <!-- {docsify-ignore} -->

Er is geen lab voor dit hoofdstuk. 

TODO: User toevoegen die ook met sudo de webserver kan herstarten enz…



Linus heeft een vriend, genaamd Dennis,  die ook wil meehelpen met het project. 



Linus maakt een nieuwe gebruiker *dennis* aan voor hem op de server

```
ubuntu@aws-linux-ess:~$ sudo useradd -m -c "Dennis Ritchie" -s /bin/bash dennis
```



Hij geeft hem een tijdelijk eerste wachtwoord *pxl*

```
ubuntu@aws-linux-ess:~$ sudo passwd dennis
```



Hij geeft Dennis ook sudo rechten om de nginx-server te herstarten zonder dat hij een paswoord dient op te geven

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



Tevens maakt hij een nieuw ssh -keypair voor Dennis

```
ubuntu@aws-linux-ess:~$ su - dennis                                      # switchen naar de user dennis
dennis@aws-linux-ess:~$ ssh-keygen -t ecdsa -C "dennis@aws-linux-ess"    # driemaal enter om te antwoorden op de vragen

```



Dit heeft een public en een private key aangemaakt in folder .ssh van de homefolder van de gebruiker. We kopiëren de inhoud van de public key naar een file genaamd *authorized_keys* en veranderen de rechten van deze file naar 600 (zie later voor meer uitleg)

```
dennis@linux-ess:~$ cd .ssh
dennis@linux-ess:~/.ssh$ ls
id_ecdsa   id_ecdsa.pub
dennis@linux-ess:~/.ssh$ cat id_ecdsa.pub >> authorized_keys    
dennis@linux-ess:~/.ssh$ chmod 600 authorized_keys                      # dit eventueel terug weg
dennis@linux-ess:~/.ssh$ exit

```



Hij download de private key van Dennis naar zijn laptop zodanig dat hij deze kan doormailen. Eerst moet hij de private key wel even in zijn eigen homefolder zetten om deze te kunnen overbrengen via scp

```
ubuntu@aws-linux-ess:~$ sudo cp /home/dennis/.ssh/id_ecdsa .
ubuntu@aws-linux-ess:~$ sudo chmod o+r id_ecdsa								   # om rechten te geven voor scp via user ubuntu
ubuntu@aws-linux-ess:~$ exit
Powershell > scp -i ".ssh/privatekeyfile.pem" ubuntu@ipvandeserver:id_ecdsa .  # om de key te downloaden van de server
Powershell > ssh -i ".\id_ecdsa" dennis@ipvandeserver						   # om de key te testen met het inloggen als dennis
```





```
ubuntu@aws-linux-ess:~$ 
```



```

```



