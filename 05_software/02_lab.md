# Lab <!-- {docsify-ignore} -->

### **Disabling the systembell in the Ubuntu instance**

If you find it quite annoying to always hear the system bell during a tab completion, you can turn it off:

- via the file */etc/inputrc*

OR

- via removing the pcspkr kernel module

***sudo nano /etc/inputrc***

![img](../images/05/AD_4nXeZpL1XR2jQF9fMJUmBWtbQeJC2SpwNVmOCga_oSciOUCFcf7zftSTPjz29KgLmU5l_3OBj0tpNJJX4xqibmTUtaYKYqO8xnBR-sZB1BcAvuZq_hz1pAm-f0d5IqYK5K2ZlYMtsAZCO15q32AVL5-Z-r1-U.png)

Uncomment the line *set bell-style none* by removing the hash sign at the front.

Leave the ssh session and log in again over ssh to get the result.

If that doesn't work, you can try removing the PC speaker kernel module (if it is implemented) with

***sudo rmmod pcspkr***



### **Installing the web server** 

We install the nginx web server. But first we upgrade all the packages to their latest version.

***sudo apt update*** 

this ensures that the computer knows the latest versions of all packages

![img](../images/05//AD_4nXffuw5rrfCzwTQrTOOKR8mpAeBiwvbMUo59GttyvPVwu2xqvQTwA-Jpp21X15v0hvwBv-xbCQ2KBso9teViK0moZZ80z218Xwq__9h3XJs_HWrpskv5iBMRouLhXdft6biPeUT-l1tjoy4fkQdD8wtW3n4.png)



***sudo apt -y upgrade***

 		- updates all packages to their latest version![img](../images/05/AD_4nXdGNtqaOrbp_wIyLD6aJ3n1FOb3OFEoQ0LUFWAoR70YJznoe2dkXWFmz06BejlOfm3FuKwusqtU1Sxwi6QW6zzS9wHQ9gBwSgX11BPYJw67vJ1f6Eqlr-72ERTdYHd82ZMSOikTUlvjKApS3RXuRasioMY1.png)

![img](../images/05/AD_4nXfcJNEVEMX-vtiFq-b_CW7opmtyQHalgoKRDUzFL3Hz6AJW8gZ2SKtKcXf6QxOJ762LdE8eLsTuNKzONxCqTWOjFsYu12Mwu5Wn5rTFunpwKgo4OIRKE0jy-TzGW1DCLX_EtOf5HuEPDrwx7Ioe4uc37vY.png)





Restart the Webserver-Instance with

 ***sudo reboot***

![img](../images/05/AD_4nXewrU_Ii3JCeJSkbrnfDb7uLWZBZcG4tIcfkhCaqyLEOMTUhtieuRWvkTVMJFjbDXkMlKSZSeP6f6t61n252jMZe56wTRtoyWEZV7NvlhHHT9kskhcyVcUDkBIHwJMZg2-m1X6DbDXlT1fFEZQhbKY-HMYI.png)



Now we install the webserver with

**sudo apt -y install nginx**

   - this installs the nginx-webserver

![img](../images/05/AD_4nXdeOYx_ssXxMG1yDdzycWxZ_Vai2BvCy2kkzPiWeTJrUkDXRp17kOd5UNaW7X2wXv72CaD0OB2cOfHAFGH2B_Yt3akmI4-hWZVf3gjugnsTq50MXxCW2AD9k7UEngG-XYR0ddyN4YMVFR2qYCkXPvmvsTbn.png)



We check whether 

- nginx is running
- listening is done on port 80

![img](../images/05/AD_4nXdUOi0U51gEFUDLKkpcheqsIQUc58HoLjSjgyrHTQuXIWSM71s94iXoaqZ3neZSsmsvPA09yLEtAwij8UZSmGDOEJ6FfIYZDRlEovB0XO7kdxfkdQep8CW30ZSDwrcxLvs5YSeuAyxwg4Psso9r7dOsRTE.png)

![img](../images/05/AD_4nXeYwxhsO51zFFUA9NV1wZM_AZWxB873_1DRBJzWn1Y-G6c-GxityjTPDfYRAEqVTC2S8xd5oO3dfgH35vTL1J9DCThkuTVyypCG2NJJ2Cemi_vbhG40PpiQ0gmcvJgAmHFlir_ja1fNTH4FlOOt6xpU8VgC.png)



- ### **Test the web server locally** 

  We test locally whether the web server works. Because we are on a Linux Server and do not have a GUI, we have to do this with a Text-based browser

  - install lynx

![img](../images/05/AD_4nXeYN69F8nQlwGjF1e5HTg78Yq-mW3j7AnwyJ3hgArQo2RbCLApj0X1MqzTtaak3HaROboXDGZBRgmvVC99xa6W242S0lV6vNa8xwK-ob3P_WNXzxutqjAurGRKfhNxEZSy6HF8E5vE8JVXvqztnzUh1S1LU.png)

- and surf to
- 127.0.0.1

![img](../images/05/AD_4nXcRwx6itzeFKQ38bpTkjgV2FtZDgU3fL-w_Ss24PYuLI0lIkPYeWDX2nGLNj9SWczys6kigq9JHo2BW5WeRgrgXdDJrDFnGcybd_MrbO-g0Yv-stV9Cnr3RmsgoOLGkIIRqXTLcYiu4kl0zhLeKxGogKF1I.png)

- localhost

![img](../images/05/AD_4nXcDsUMYMFXx9saoD1_Pr5TNLu45723zxG-5DoKblwLZj6mLyH-9ddlVIKW4NeOljpz9VbzzLXTV-oRlhG0veeGK1gKh3NSEoGOiRr44tqqlceXQczq6K6fDPFsMdpAlk-3tbGe0rLSjf8zUEco3UI3ol3P1.png)

You should arrive at the page below. You can leave the web browser with *Q*

![img](../images/05/AD_4nXfSo75rpMprepMs3phlFWfpWDxj9vMGfOGkTrq7jc-Y8teWpA2lUsV3v869Mp0IiRgBJVLAi6bZIVkg51hlH8R9ciBp3T9rwhxg979j87wHHngC38b_mQavq7GX-TqQHna2V0X3LjR_XC_yDBiChozePHJm.png)



### **Test the web server from the laptop and adjust the firewall**

Surf from your laptop to the public IP of the website via **http** (for testing port 80)

![img](../images/05/AD_4nXd2tqvpoexDAHMhTS1U72lIJC3n0VJP6iAaJrUMDmIZLlyiSC_XMAjW10aaFNQroAh3aw6lKJT2ACsuM3aDD_D7IXn0tgmj1Q85CSeAIqAnw0xWtcv5615DGQKJLYwvcDnHgKB0Q9GZg792HTP5BJntpP7z.png)



The website hangs for several minutes while loading

![img](../images/05/AD_4nXf85uQOui-9oeRUFoSKUjbDDD3g4ZPIDtNrEoLEA3bTMZSsWosHwaUNQoXoIiKcdXr_VWPoKWFTABZ7itNuQPfME78z577IQK7kHK_32I8Qo2po-h1wXgCYptE88RHycPIknQJYDKUfE70HbQBvCkrjtdr8.png)



After a long time we get *The connection was reset*.  ![img](../images/05/AD_4nXdldFE0L2e1QyItb0UlK4jJvUH9LBSaxU5qqrNCNQjBAv63CwI1dBdE1XG9xaIUB9fESdhISLYH5QWp_HdgFDJKwVixgL2IIO251CzYS6vhDjKERLLBg0vr5wQEVp1nnKKSxwYthi0MIzHhKVKpVDoPlqWG.png)

- So it doesn't seem to work yet!

  

  Because this does not work, we check whether there is http traffic arriving on the Web server

  - ***sudo tcpdump -i enX0 port 80*** (if enX0 is the name of your NIC, which you see with the command *ip a*. The name could also be somthing like eth0 or enp0s3 or ens33 or ...)
  - We surf over http from the laptop to the external IP address of the Web server (or refresh)
  - We look at what arrives and leaves packets on the Web server

![img](../images/05/AD_4nXdog3DLneu6wPmcj68yoqOrwuc3xMa6elaLCHD4ZwkK6MLuPum78pRQr3qmeuwf1SN7_h6VX6nyIG50-nHaftgnJ3gsncQqDW08GJaqhNaXK-kbMxPWAYIBl9CP3fV3dTLOxdsep203Cl69_jw27m4GB3w.png)

We see that not a single package arrives. So no external traffic enters the web server. The traffic is already filtered out somewhere beforehand.

Stop the sniffing with *CTRL-C*

![img](../images/05/AD_4nXfUH9KCv0LUL-4MrJvc-4baJyfsR_5klhuWusMlrLJFHdSSTkGkGKP9HMbAq3naBIj8tXcAZVDGKOVcXc2VloeAfQJlyWlKGtZy-BS_b0ZhOJWFukZN9V0Izt_hlUCfC24BkAGKBcL1mtJ-5X9REaHu8L8d.png)

PS: You may still see some packets that come from an APIPA address (=169.254.0.0/16), but not from an external IP

![img](../images/05/AD_4nXfFtVH73fwHMcBLPXCKV8z6VbmWa2wC8EFZdmfDvxv6v7tpxPK4f9PM89wuY9YePEkUNYu6bO6FVXaOYgwEQiLF1RgWi-zQA7j2g3yL7t8YNo4jkhvDdyB95Tf9Z385S4hb6DE5R5uxSTFsg-cdjyTg1_Im.png)

Surfing does not work because the traffic is filtered at AWS level and more specifically via the Security Group. So we have to solve this.



### **Add a new inbound rule in the Security Group that allows incoming traffic to port 80.**

Click on the *Security Group* to change te configuration![img](../images/05/AD_4nXfajb5p1DJuextkhIyQjVkPr6-pYjuf7zZXDMxqHQPMxkl86nyjMR-tWwXXazdvSH3gYjRRNkt03dI4fEKD32HABQ9L6lt6ifvJ0qlHhAwP6Wa6ULABqeOWjw_BB64a2xQxpSAQGQ3dxOwJM-PUNLsa4bg.png)



Click on *Edit inbound rules*![img](../images/05/AD_4nXeCqyqSnnHrg4edeJnBXRW2lBDOkbAs_k0wFcma3FVtI7kS0Gt-rTTIfVKbCKMR6rlgqyziFpn5OTXLN0GA4n_qGUyEGQunmIKPTlqWi8Jatdpk-46rs6Vo2HZYwCtSte--tgOCWnm0WW_PUu94Jym0D8vl.png)



Click on *Add rule* and add a rule that allows incoming HTTP traffic over IPv4 from anywhere![img](../images/05/AD_4nXcLguEadlaOzr4hZRxQTUTWKt9LUE2RHDNovFIKMN1tOiKmoHqAPOocsL0b2nvP_5-0ANMxJVIJmzQex7LRjopIAr-dUl-Gd5kzmQZ6UddkWxC1qLzOcUf86ArHzyDBf8ajPZ5tBCD_PTdq5bRuxfRbGp4k.png)



The addition was successful![img](../images/05/AD_4nXfPiAA-HRGSvo6jyz7EQtibgU1cq_vQ2NUfCUWb-EO8aJxUgqPTGCh-znPOhPTis6OcDmevLtQhbgKA9w-XRW39TXwuaV-nZQX-RoqxWAqPZmGSB3Hq2ExKlpGEnC6gLpB2rrHAva8QLhVATaKzsUJ-p8s.png)



We are going to test again whether surfing works

We start with sniffing first…

- *sudo tcpdump -i eth0 port 80* (if eth0 is the name of your NIC)
- We surf again from the laptop to the external IP address of the Web server via http (or Refresh)
- We look at what arrives and leaves packages

![img](../images/05/AD_4nXdZm4lGoI4c02OmNrJMtfZ9Y67A_S-JaCRG9UrXUvzS-miQ5MsWGwDFJV7htErw6-z-4V-89mGbJTeQNQJzjiZCopNxn9EaR_F5Cgr-gHDNZgBcORI50pBcSJFRFI140Df7xdDQh-Pbo8H2vsz-rMJKCysP.png)



We now see that packets arrive from an external address and depart back to that external address.![img](../images/05/AD_4nXddqPxKYDwjlVYi-GciVtN6XQ5dX9z-lMIdzRc8nYTYYY9ySy6pYtnmTxnDR5ry-UPPR8sW7YUwZHrDMzdphRkrJdz9Bw9PwjuZQ3BDAHPS0MhguVX1fNxfbKT0v8POAEcCSnY_r__I3W4GLxHgcadLYRBg.png)

The website works!
