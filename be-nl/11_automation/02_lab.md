# Lab <!-- {docsify-ignore} -->

Linus wil het script dat toont uit welke landen er gesurfd wordt naar de website om de 5 minuten automatisch laten updated

```bash
ubuntu@linux-ess:~$ crontab -e


*/5 *  * * *  for file in $(ls -r /var/log/nginx/access.*[!z]); cat $file >> $HOME/fullaccess.log; done
*/5 *  * * *  $HOME/scriptomuittelezen fullaccess.log | sudo tee  /var/www/html/monitor.html
```

