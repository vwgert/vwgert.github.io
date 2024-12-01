# Lab <!-- {docsify-ignore} -->

Linus wants the script that shows from which countries people are surfing to the website to be automatically updated every 5 minutes

```bash
ubuntu@linux-ess:~$ crontab -e


*/5 *  * * *  for file in $(ls -r /var/log/nginx/access.*[!z]); cat $file >> $HOME/fullaccess.log; done
*/5 *  * * *  $HOME/scriptomuittelezen fullaccess.log | sudo tee  /var/www/html/monitor.html
```

