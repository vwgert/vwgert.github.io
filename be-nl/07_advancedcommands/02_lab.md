# Lab <!-- {docsify-ignore} -->
Linus kan het commando om het publiek IP adres te achterhalen niet onthouden. Daarom maakt hij er een alias voor aan. 

```bash
ubuntu@linux-ess:~$ curl checkip.amazonaws.com
54.87.203.25
ubuntu@linux-ess:~$ alias getip="curl checkip.amazonaws.com"
ubuntu@linux-ess:~$ getip
54.87.203.25
```



Tevens wil hij een ICE(In Case of Emergency) aanmaken die de webserver onmiddellijk down brengt.

```bash
ubuntu@linux-ess:~$ alias ice="systemctl stop nginx; systemctl status nginx --no-pager"
ubuntu@linux-ess:~$ sudo ice
○ nginx.service - A high performance web server and a reverse proxy server
     Loaded: loaded (/usr/lib/systemd/system/nginx.service; enabled; preset: enabled)
     Active: inactive (dead) since Fri 2024-06-21 11:04:58 UTC; 10ms ago
   Duration: 9.704s
       Docs: man:nginx(8)
    Process: 1158 ExecStartPre=/usr/sbin/nginx -t -q -g daemon on; master_process on; (code=exited, status=0/SUCCESS)
    Process: 1160 ExecStart=/usr/sbin/nginx -g daemon on; master_process on; (code=exited, status=0/SUCCESS)
    Process: 1169 ExecStop=/sbin/start-stop-daemon --quiet --stop --retry QUIT/5 --pidfile /run/nginx.pid (code=exited, status=0/SUCCESS)
   Main PID: 1161 (code=exited, status=0/SUCCESS)
        CPU: 21ms

Jun 21 11:04:48 linux-ess systemd[1]: Starting nginx.service - A high performance web server and a reverse prox…erver...
Jun 21 11:04:48 linux-ess systemd[1]: Started nginx.service - A high performance web server and a reverse proxy server.
Jun 21 11:04:58 linux-ess systemd[1]: Stopping nginx.service - A high performance web server and a reverse prox…erver...
Jun 21 11:04:58 linux-ess systemd[1]: nginx.service: Deactivated successfully.
Jun 21 11:04:58 linux-ess systemd[1]: Stopped nginx.service - A high performance web server and a reverse proxy server.
Hint: Some lines were ellipsized, use -l to show in full.
```



Na controle van juiste uitvoer dient hij de aliases toe te voegen aan een (nieuw) bestand genaamd .bash_aliases in zijn homefolder. Dit bestand wordt uitgevoerd telkens er een nieuwe shell wordt gestart, zoals bijvoorbeeld bij het inloggen op de server. Maak het bestand aan met *nano*.

```
ubuntu@linux-ess:~$ cat .bash_aliases
alias getip="curl checkip.amazonaws.com"
alias ice="sudo systemctl stop nginx; systemctl status nginx --no-pager"
```



Linus wil ook een overzicht krijgen van wie allemaal zijn website bezoekt. Hiervoor heeft hij de access file nodig van nginx. Deze file zal normaal gezien geconfigureerd staan in de config file van nginx.

```bash
ubuntu@linux-ess:~$ locate nginx.conf
/etc/nginx/nginx.conf
ubuntu@linux-ess:~$ cat /etc/nginx/nginx.conf
user www-data;
worker_processes auto;
pid /run/nginx.pid;
error_log /var/log/nginx/error.log;
include /etc/nginx/modules-enabled/*.conf;
...
        ##
        # Logging Settings
        ##

        access_log /var/log/nginx/access.log;
...
ubuntu@linux-ess:~$ cat /var/log/nginx/access.log
193.190.253.145 - - [21/Jun/2024:11:30:36 +0000] "GET / HTTP/1.1" 200 2039 "-" "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/126.0.0.0 Safari/537.36"
193.190.253.145 - - [21/Jun/2024:11:30:36 +0000] "GET /style.css HTTP/1.1" 304 0 "http://54.87.203.25/" "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/126.0.0.0 Safari/537.36"
193.190.253.145 - - [21/Jun/2024:11:30:36 +0000] "GET /header.png HTTP/1.1" 304 0 "http://54.87.203.25/style.css" "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/126.0.0.0 Safari/537.36"
193.190.253.145 - - [21/Jun/2024:11:30:36 +0000] "GET /favicon.ico HTTP/1.1" 404 196 "http://54.87.203.25/" "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/126.0.0.0 Safari/537.36"
...
```



Indien je het bestand nginx.conf niet vindt met *locate*, dan moet je eerst de locate-database updaten met *updatedb*.



We zien dat er nog niet zo heel veel bezoekers zijn geweest. Als je toch veel regels ziet, dan zijn dat waarschijnlijk requests naar onbestaande pagina's en scripts door anderen die aan het rondneuzen zijn voor vulnerabilities (=kwetsbaarheden in de veiligheid). Je website staat dan ook publiek voor de hele wereld. Dus er zijn altijd bezoekers met kwaad opzet.



We gaan deze access file gaan uitbreiden met data via een script. Zodat het lijkt alsof we reeds veel meer bezoekers hebben gehad. Gebruik ook dit script op jouw server. Maak een nieuwe file, genaamd script, met de editor *nano*.

```bash
ubuntu@linux-ess:~$ cat script   # Plaats onderstaande tekst in de file
#!/bin/bash

# IP-adressen per land (voorbeeld)
IPS_US=("8.0.2.1" "8.250.2.2" "8.154.72.23")
IPS_UK=("31.24.100.1" "31.29.198.22" "31.31.59.3")
IPS_AU=("101.160.0.1" "101.165.12.4" "101.190.113.33")

# Tijdstempel functie
timestamp() {
  date "+%d/%b/%Y:%H:%M:%S %z"
}

# URLs die bezocht worden
URLS=("/index.html" "/about.html" "/contact.html")

# HTTP status codes
STATUS_CODES=("200" "404" "500")

# User agents
USER_AGENTS=(
  "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/91.0.4472.124 Safari/537.36"
  "Mozilla/5.0 (iPhone; CPU iPhone OS 14_6 like Mac OS X) AppleWebKit/605.1.15 (KHTML, like Gecko) Version/14.0 Mobile/15E148 Safari/604.1"
  "Mozilla/5.0 (compatible; Googlebot/2.1; +http://www.google.com/bot.html)"
)

# Referrer URLs
REFERRERS=(
  "http://google.com"
  "http://bing.com"
  "http://yahoo.com"
)

# Functie om een willekeurig IP-adres uit een lijst te kiezen
random_ip() {
  local ips=("$@")
  echo "${ips[$RANDOM % ${#ips[@]}]}"
}

# Genereren van logregels
for i in {1..100}; do
  # Willekeurig land kiezen
  case $((RANDOM % 3)) in
    0) IP=$(random_ip "${IPS_US[@]}") ;;
    1) IP=$(random_ip "${IPS_UK[@]}") ;;
    2) IP=$(random_ip "${IPS_AU[@]}") ;;
  esac

  URL=${URLS[$RANDOM % ${#URLS[@]}]}
  STATUS=${STATUS_CODES[$RANDOM % ${#STATUS_CODES[@]}]}
  SIZE=$((RANDOM % 5000 + 500))
  USER_AGENT=${USER_AGENTS[$RANDOM % ${#USER_AGENTS[@]}]}
  REFERRER=${REFERRERS[$RANDOM % ${#REFERRERS[@]}]}

  LOG_ENTRY="$IP - - [$(timestamp)] \"GET $URL HTTP/1.1\" $STATUS $SIZE \"$REFERRER\" \"$USER_AGENT\""
  echo $LOG_ENTRY
done
```



Van zodra het script uitvoerbaar is kunnen we de output bekijken.

```bash
ubuntu@linux-ess:~$ chmod u+x script
ubuntu@linux-ess:~$ ./script
192.0.2.3 - - [21/Jun/2024:11:25:22 +0000] "GET /contact.html HTTP/1.1" 404 3077 "http://yahoo.com" "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/91.0.4472.124 Safari/537.36"
198.51.100.1 - - [21/Jun/2024:11:25:22 +0000] "GET /contact.html HTTP/1.1" 200 2660 "http://bing.com" "Mozilla/5.0 (compatible; Googlebot/2.1; +http://www.google.com/bot.html)"
198.51.100.2 - - [21/Jun/2024:11:25:22 +0000] "GET /about.html HTTP/1.1" 500 5369 "http://google.com" "Mozilla/5.0 (compatible; Googlebot/2.1; +http://www.google.com/bot.html)"
198.51.100.3 - - [21/Jun/2024:11:25:22 +0000] "GET /about.html HTTP/1.1" 200 4020 "http://google.com" "Mozilla/5.0 (compatible; Googlebot/2.1; +http://www.google.com/bot.html)"
203.0.113.1 - - [21/Jun/2024:11:25:22 +0000] "GET /about.html HTTP/1.1" 200 3695 "http://yahoo.com" "Mozilla/5.0 (iPhone; CPU iPhone OS 14_6 like Mac OS X) AppleWebKit/605.1.15 (KHTML, like Gecko) Version/14.0 Mobile/15E148 Safari/604.1"
198.51.100.2 - - [21/Jun/2024:11:25:22 +0000] "GET /about.html HTTP/1.1" 200 3553 "http://yahoo.com" "Mozilla/5.0 (compatible; Googlebot/2.1; +http://www.google.com/bot.html)"
...

```



Vooraleer we deze output toevoegen aan de access file is het een goed idee om een backup van deze file te maken.

```bash
ubuntu@linux-ess:~$ ls -l /var/log/nginx/
total 32
-rw-r----- 1 www-data adm  1101 Jun 21 11:30 access.log
-rw-r----- 1 www-data adm 13926 Jun 20 21:57 access.log.1
-rw-r----- 1 www-data adm  2726 Jun 19 23:59 access.log.2.gz
-rw-r----- 1 www-data adm  1267 Jun 18 11:36 access.log.3.gz
-rw-r----- 1 www-data adm  3619 Jun 14 14:03 access.log.4.gz
-rw-r----- 1 www-data adm     0 Jun 13 06:16 error.log
ubuntu@linux-ess:~$ mkdir backups
ubuntu@linux-ess:~$ cp /var/log/nginx/access* backups/
ubuntu@linux-ess:~$ ls backups
access.log  access.log.1  access.log.2.gz  access.log.3.gz  access.log.4.gz  authorized_keys.backup
```



We voegen de output van het script nu toe aan de access file. Om dit te doen moeten we even switchen naar de gebruiker *root*

```bash
ubuntu@linux-ess:~$ sudo su
root@linux-ess:/home/ubuntu# ./script >> /var/log/nginx/access.log
root@linux-ess:/home/ubuntu# exit
exit
ubuntu@linux-ess:~$
```



Als laatste wil Linus zelf bijhouden wanneer hij inlogt op de server en wat op dat ogenblik het publiek IP adres van de server was. Hij zal dit telkens toevoegen aan het bestand *PublicIP* van in zijn homefolder.

```bash
ubuntu@linux-ess:~$ ls
LinusCraft  LinusCraft.zip  PublicIP  backups  script
ubuntu@linux-ess:~$ cat .profile
# ~/.profile: executed by the command interpreter for login shells.
# This file is not read by bash(1), if ~/.bash_profile or ~/.bash_login
# exists.
# see /usr/share/doc/bash/examples/startup-files for examples.
# the files are located in the bash-doc package.

# the default umask is set in /etc/profile; for setting the umask
# for ssh logins, install and configure the libpam-umask package.
#umask 022

echo "$(date) --- $(curl -s checkip.amazonaws.com)"  >>  ~/PublicIP
...

```



Na het disconnecteren en opnieuw connecteren zien we de toevoeging in de file.

```bash
ubuntu@linux-ess:~$ cat PublicIP
54.87.203.25
Fri Jun 21 14:47:03 UTC 2024 --- 54.87.203.25
```

