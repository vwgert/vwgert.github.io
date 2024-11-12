# Lab <!-- {docsify-ignore} -->

Linus has a friend named Dennis who also wants to help with the project.



Linus creates a new user *dennis* for him on the server

```
ubuntu@aws-linux-ess:~$ sudo useradd -m -c "Dennis Ritchie" -s /bin/bash dennis
```



He gives him a temporary first password *pxl*

```
ubuntu@aws-linux-ess:~$ sudo passwd dennis
```



He also gives Dennis sudo rights to restart the nginx server without him having to provide a password

```
ubuntu@aws-linux-ess:~$ which systemctl                           # to find the full path of the command
/usr/bin/systemctl
ubuntu@aws-linux-ess:~$ sudo visudo

Toevoegen onderaan:
dennis ALL=(ALL) NOPASSWD: /usr/bin/systemctl restart nginx

ubuntu@aws-linux-ess:~$ sudo -l -U dennis                         # to test if the sudoers file is ok for Dennis
Matching Defaults entries for dennis on ubserv:
    env_reset, mail_badpass,
    secure_path=/usr/local/sbin\:/usr/local/bin\:/usr/sbin\:/usr/bin\:/sbin\:/bin\:/snap/bin,
    use_pty

User dennis may run the following commands on ubserv:
    (ALL) NOPASSWD: /usr/bin/systemctl restart nginx

ubuntu@aws-linux-ess:~$ su - dennis                               # switch to the user dennis
dennis@aws-linux-ess:~$ sudo systemctl restart nginx              # testing if dennis is allowed to restart the nginx service
dennis@aws-linux-ess:~$ exit

```



He also creates a new ssh keypair for Dennis (because Dennis doesn't have a keypair yet)

```
ubuntu@aws-linux-ess:~$ su - dennis                                      # switch to the user dennis
dennis@aws-linux-ess:~$ ssh-keygen -t ecdsa -C "dennis@aws-linux-ess"    # Enter three times to answer the questions

```



This process created a public and a private key in the  folder .ssh of the user's homefolder. We copy the contents of the public key to a file called *authorized_keys*.  Try to find out what the purpose of the file *authorised_keys* is.

```
dennis@linux-ess:~$ cd .ssh
dennis@linux-ess:~/.ssh$ ls
id_ecdsa   id_ecdsa.pub
dennis@linux-ess:~/.ssh$ cat id_ecdsa.pub >> authorized_keys    
dennis@linux-ess:~/.ssh$ exit

```



Linus downloads Dennis' private key to his laptop so he can email it to him. First he has to put the private key in his own homefolder so he can transfer it via scp to his laptop

```
ubuntu@aws-linux-ess:~$ sudo cp /home/dennis/.ssh/id_ecdsa .
ubuntu@aws-linux-ess:~$ sudo chmod o+r id_ecdsa								   # to give rights for scp via user ubuntu
ubuntu@aws-linux-ess:~$ exit
```



In a new powershell window Linus downloads the key

```
Powershell > scp -i ".ssh/privatekeyfile.pem" ubuntu@ipvandeserver:id_ecdsa .  # to download the key from the server
```



He also tests whether he can log in as Dennis on the server using this public key

```
Powershell > ssh -i ".\id_ecdsa" dennis@ipvandeserver						   # to test the key by logging in as dennis
dennis@aws-linux-ess:~$ exit
Powershell > 
```



Linus can now email this key to Dennis

