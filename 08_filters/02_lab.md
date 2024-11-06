# Lab <!-- {docsify-ignore} -->

Linus wants to pull some statistics from the access file.

First he will merge the different access files (not the zipped ones) into a full-access file.

```bash
for file in $(ls -r /var/log/nginx/access.*[!z]); do echo "adding $file ($(wc -l $file | cut -d' ' -f1))"; cat $file >> ~/fullaccess.log; done
```



It also checks whether the number of lines is correct in the full-access file:

```bash
wc -l ~/fullaccess.log
```



It counts the number of unique IP addresses of visitors.

```bash
cut -d' ' -f1 fullaccess.log | sort -n | uniq -c
```



If Linus also wants to know from which geolocation his visitors come, this can be done with the package called geoiplookup.

```bash
sudo apt-get install geoip-bin
```



```bash
cut -d' ' -f1 fullaccess.log | sort -n | uniq -c | while read line; do IP=$(echo $line | cut -d' ' -f2); COUNT=$(echo $line | cut -d' ' -f1);echo "$IP --- $COUNT --- $(geoiplookup $IP)"; done
```



To get a shortened overview of visits per country, he wrote the script below. Try to understand this. Copy it to the server and run.

```bash
#!/bin/bash

# Controleer of het logbestand als argument is doorgegeven
if [ -z "$1" ]; then
  echo "Gebruik: $0 /pad/naar/nginx-access.log"
  exit 1
fi

LOGFILE=$1

# Controleer of het logbestand bestaat
if [ ! -f "$LOGFILE" ]; then
  echo "Het bestand $LOGFILE bestaat niet."
  exit 1
fi

declare -A COUNTRY_COUNT

# Gebruik een while-loop om door elke regel van het logbestand te lopen
while read -r line; do
  # Haal het IP-adres uit de regel (eerste veld)
  IP=$(echo "$line" | cut -d ' ' -f 1)
  
  # Voer geoiplookup uit voor het IP-adres
  GEOIP_OUTPUT=$(geoiplookup "$IP")
  
  # Haal het land uit de geoiplookup output
  COUNTRY=$(echo "$GEOIP_OUTPUT" | cut -d ':' -f 2 | cut -d ',' -f 1 | xargs)
  
  # Verhoog de teller voor het land
  if [ -n "$COUNTRY" ]; then
    COUNTRY_COUNT["$COUNTRY"]=$((COUNTRY_COUNT["$COUNTRY"] + 1))
  fi
done < "$LOGFILE"

# Print het resultaat
echo "Bezoekers per land:"
for COUNTRY in "${!COUNTRY_COUNT[@]}"; do
  echo "$COUNTRY: ${COUNTRY_COUNT[$COUNTRY]}"
done | sort -t ':' -k 2 -nr

```



```bash
chmod u+x visitors_by_country.sh
```



```bash
./visitors_by_country.sh fullaccess.log
```



### Explanation:

1. **Checking the log file:** The script checks whether a log file has been given as an argument and whether this file exists.
2. **Reading the log file:** A `while` loop reads each line of the log file.
3. **Extraction of IP address:** With `cut` the first field (the IP address) is removed from the log line.
4. **GeoIP Lookup:** The script runs `geoiplookup` for each IP address and extracts the country using `cut`.
5. **Counting visitors per country:** The script keeps track of the number of visitors per country in an associative array.
6. **Display of result:** The result is printed with an overview of the number of visitors per country, organized by number of visits.





Linus also wants to have this overview available via a web page. That's why he redirects the output of the script to an html page:

```bash
ubuntu@linux-ess:~$ ./scriptomuittelezen fullaccess.log > /var/www/html/monitor.html
-bash: /var/www/html/monitor.html: Permission denied
ubuntu@linux-ess:~$ ./scriptomuittelezen fullaccess.log | sudo tee  /var/www/html/monitor.html
Bezoekers per land:
IP Address not found: 100
US: 10
BE: 7
HR: 3
NL: 2
CN: 2
RU: 1
PT: 1
ES: 1
ubuntu@linux-ess:~$ cat !$
cat /var/www/html/monitor.html
Bezoekers per land:
IP Address not found: 100
US: 10
BE: 7
HR: 3
NL: 2
CN: 2
RU: 1
PT: 1
ES: 1
```



To check this, you can surf to the web page https://\<your-server-ip\>//monitor.html

We then see that everything is shown on one line

```html
Bezoekers per land: IP Address not found: 100 US: 10 BE: 7 HR: 3 NL: 2 CN: 2 RU: 1 PT: 1 ES: 1
```



To solve this, we place a number of line breaks \<br /\> in the output (adjustments at the bottom of the script):

```bash
#!/bin/bash

# Controleer of het logbestand als argument is doorgegeven
if [ -z "$1" ]; then
  echo "Gebruik: $0 /pad/naar/nginx-access.log"
  exit 1
fi

LOGFILE=$1

# Controleer of het logbestand bestaat
if [ ! -f "$LOGFILE" ]; then
  echo "Het bestand $LOGFILE bestaat niet."
  exit 1
fi

declare -A COUNTRY_COUNT

# Gebruik een while-loop om door elke regel van het logbestand te lopen
while read -r line; do
  # Haal het IP-adres uit de regel (eerste veld)
  IP=$(echo "$line" | cut -d ' ' -f 1)
  
  # Voer geoiplookup uit voor het IP-adres
  GEOIP_OUTPUT=$(geoiplookup "$IP")
  
  # Haal het land uit de geoiplookup output
  COUNTRY=$(echo "$GEOIP_OUTPUT" | cut -d ':' -f 2 | cut -d ',' -f 1 | xargs)
  
  # Verhoog de teller voor het land
  if [ -n "$COUNTRY" ]; then
    COUNTRY_COUNT["$COUNTRY"]=$((COUNTRY_COUNT["$COUNTRY"] + 1))
  fi
done < "$LOGFILE"

# Print het resultaat
echo "<h1>Bezoekers per land:</h1>"
for COUNTRY in "${!COUNTRY_COUNT[@]}"; do
  echo "$COUNTRY: ${COUNTRY_COUNT[$COUNTRY]} <br />"
done | sort -t ':' -k 2 -nr
```



We redirect the output of the script to the HTML page again:

```bash
ubuntu@linux-ess:~$ ./scriptomuittelezen fullaccess.log | sudo tee  /var/www/html/monitor.html
Bezoekers per land:
IP Address not found: 100
US: 10
BE: 7
HR: 3
NL: 2
CN: 2
RU: 1
PT: 1
ES: 1
ubuntu@linux-ess:~$ cat !$
cat /var/www/html/monitor.html
Bezoekers per land:
IP Address not found: 100
US: 10
BE: 7
HR: 3
NL: 2
CN: 2
RU: 1
PT: 1
ES: 1
```



When we now look at the web page again, we see that the lines are shown one below the other:

```html
Bezoekers per land:
IP Address not found: 100
US: 10
BE: 7
HR: 3
NL: 2
CN: 2
RU: 1
PT: 1
ES: 1
```





Linus also wants an overview of when and from which IP address requests were made to web pages that did not exist (HTML status 404):

```
grep " 404 " fullaccess.log | cut -d '"' -f1 | sed "s/- -/-/" | sort -n
```



Likewise, he also wants an overview of the unavailable pages that were requested:

```
grep " 404 " fullaccess.log | cut -d '"' -f2 | cut -d' ' -f2 | sort | uniq -c | sort -nr
```



