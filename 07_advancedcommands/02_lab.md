# Lab <!-- {docsify-ignore} -->

Linus cannot remember the command to retrieve the public IP address. That's why he creates an alias for it.

```bash
ubuntu@linux-ess:~$ curl checkip.amazonaws.com
54.87.203.25
ubuntu@linux-ess:~$ alias getip="curl checkip.amazonaws.com"
ubuntu@linux-ess:~$ getip
54.87.203.25
```



He also wants to create an ICE (In Case of Emergency) that will immediately bring down the web server.

```bash
ubuntu@linux-ess:~$ alias ice="sudo systemctl stop nginx; systemctl status nginx --no-pager"
ubuntu@linux-ess:~$ ice
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



After checking the correct output, he should add the aliases to a (new) file called .bash_aliases in his home folder. This file is executed every time a new shell is started, such as when logging into the server.

```
ubuntu@linux-ess:~$ cat .bash_aliases
alias getip="curl checkip.amazonaws.com"
alias ice="sudo systemctl stop nginx; systemctl status nginx --no-pager"
```



Linus also wants to get an overview of who visits his website. For this he needs the access file from nginx. This file will normally be configured in the nginx config file.

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



We see that there have not been very many visitors yet. If you see a lot of lines, they are probably requests to non-existent pages and scripts by others who are sniffing around for vulnerabilities. Your website is therefore public for the whole world. So there are always visitors with malicious intent.



We are going to expand this access file with data via a script. So that it seems as if we have already had many more visitors. Also use this script on your server. Make a new file, called script, with the editor nano.

```bash
ubuntu@linux-ess:~$ cat script           # put this text in the file...
#!/bin/bash

# IP-adressen per land (voorbeeld)
IPS_US=("192.0.2.1" "192.0.2.2" "192.0.2.3")
IPS_UK=("198.51.100.1" "198.51.100.2" "198.51.100.3")
IPS_AU=("203.0.113.1" "203.0.113.2" "203.0.113.3")

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



Once the script is executable we can view the output.

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



Before we add this output to the access file, it is a good idea to make a backup of this file.

```bash
ubuntu@linux-ess:~$ ls -l /var/log/nginx/
total 32
-rw-r----- 1 www-data adm  1101 Jun 21 11:30 access.log
-rw-r----- 1 www-data adm 13926 Jun 20 21:57 access.log.1
-rw-r----- 1 www-data adm  2726 Jun 19 23:59 access.log.2.gz
-rw-r----- 1 www-data adm  1267 Jun 18 11:36 access.log.3.gz
-rw-r----- 1 www-data adm  3619 Jun 14 14:03 access.log.4.gz
-rw-r----- 1 www-data adm     0 Jun 13 06:16 error.log
ubuntu@linux-ess:~$ cp /var/log/nginx/access* backups/
ubuntu@linux-ess:~$ mkdir backups
ubuntu@linux-ess:~$ ls backups
access.log  access.log.1  access.log.2.gz  access.log.3.gz  access.log.4.gz  authorized_keys.backup
```



We now add the output of the script to the access file.

```bash
ubuntu@linux-ess:~$ sudo su
root@linux-ess:/home/ubuntu# ./script >> /var/log/nginx/access.log
root@linux-ess:/home/ubuntu# exit
exit
ubuntu@linux-ess:~$
```



Finally, Linus himself wants to Log when he logs in to the server and what the public IP address is. He will always add this to the *PublicIP* file in his home folder.

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



After disconnecting and reconnecting over SSH we see the addition in the file.

```bash
ubuntu@linux-ess:~$ cat PublicIP
54.87.203.25
Fri Jun 21 14:47:03 UTC 2024 --- 54.87.203.25
```

