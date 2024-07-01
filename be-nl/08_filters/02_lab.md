# Lab <!-- {docsify-ignore} -->

Er is geen lab voor dit hoofdstuk. 



TODO: Output redirecten naar html pagina in website om te kunnen zien via webbrowser



Linus wil een paar statistieken trekken uit de access-file.

Eerst zal hij de verschillende access-files samenvoegen  (niet de gezipte) in een full-access file.

```bash
for file in $(ls -r /var/log/nginx/access.*[!z]); do echo "adding $file ($(wc -l $file | cut -d' ' -f1))"; cat $file >> ~/fullaccess.log; done
```



Hij controleert dan ook of het aantal regels klopt bij de full-access file:

```bash
wc -l ~/fullaccess.log
```



Hij telt het aantal unieke IP adressen van de bezoekers.

```bash
cut -d' ' -f1 fullaccess.log | sort -n | uniq -c
```



Als Linus ook wil weten van welke geolocatie zijn bezoekers afkomstig zijn, dan kan dat met de package, genaamd geoiplookup.

```bash
sudo apt-get install geoip-bin
```



```bash
cut -d' ' -f1 fullaccess.log | sort -n | uniq -c | while read line; do IP=$(echo $line | cut -d' ' -f2); COUNT=$(echo $line | cut -d' ' -f1 | xargs);echo "$IP $COUNT $(geoiplookup $IP)"; done
```



Om een verkort overzicht te krijgen van bezoeken per land kan heeft hij onderstaand script geschreven. Probeer dit te begrijpen. Kopieer het naar de server en voer uit.

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



### Uitleg:

1. **Controle van het logbestand:** Het script controleert of een logbestand als argument is meegegeven en of dit bestand bestaat.
2. **Lezen van het logbestand:** Een `while`-loop leest elke regel van het logbestand.
3. **Extractie van IP-adres:** Met `cut` wordt het eerste veld (het IP-adres) uit de logregel gehaald.
4. **GeoIP Lookup:** Het script voert `geoiplookup` uit voor elk IP-adres en haalt het land eruit met behulp van `cut`.
5. **Tellen van bezoekers per land:** Het script houdt het aantal bezoekers per land bij in een associatieve array.
6. **Weergave van resultaat:** Het resultaat wordt afgedrukt met een overzicht van het aantal bezoekers per land, geordend op aantal bezoeken.





Linus wil ook een overzicht van wanneer en van welk IP adres er verzoeken zijn gebeurd naar webpagina's die niet bestonden (HTML status 404):

```
grep " 404 " fullaccess.log | cut -d '"' -f1 | sed "s/- -/-/" | sort -n
```



Op dezelfde manier wil hij ook een overzicht van de onbeschikbare pagina's die gevraagd werden:

```
grep " 404 " fullaccess.log | cut -d '"' -f2 | cut -d' ' -f2 | sort | uniq -c | sort -nr
```

