# Lab <!-- {docsify-ignore} -->

In the following chapters Linus will install a Webserver and Minetest Server. Before he can do that, he will need to have a Linux System up and running. In this lab he will create a Linux Cloud Instance on  Amazon Web Services (AWS). With this infrastructure set up he will be able to install, configure and maintain his Webserver and Minecraft Server at a later time.

### Creating the SSH keypair  

Before we can install the instance we need to create an SSH keypair so we will be able to connect (=login) to the instance af creation.

On *AWS*, go to *EC2*.

![AWSCreateSSH](../images/01/02_lab/AWSCreateSSH_0_Compute.png)



Go to *key pairs* and create a new one.

![AWSCreateSSH](../images/01/02_lab/AWSCreateSSH_1_KeyPairs.png)



![AWSCreateSSH](../images/01/02_lab/AWSCreateSSH_2_CreateKeyPair.png)

The private key wil automatically be downloaded by your browser to the *Downloads* folder.

![AWSCreateSSH](../images/01/02_lab/AWSCreateSSH_3_KeyPairCreated.png)

Move this key to the folder .*ssh* under your account *"C:\Users\\<your loginname>"*. Create this folder if it doesn't exit.

![AWSCreateSSH](../images/01/02_lab/AWSCreateSSH_4_KeyPairCut.png)

![AWSCreateSSH](../images/01/02_lab/AWSCreateSSH_5_KeyPairPaste.png)



### Creating the Cloud instance 

The Web server and Minecraft Server run in a Linux Server Environment. More specifically, an Ubuntu Server.

On *AWS*, go to *EC2*.

![AWSCreateInstance](../images/01/02_lab/AWSCreateInstance_0_Compute.png)

Make sure you are in the *"N. Virginia"* Region and click *Launch instance*.

![AWSCreateInstance](../images/01/02_lab/AWSCreateInstance_1_LaunchInstance.png)

Fill in the correct details.

![AWSCreateInstance](../images/01/02_lab/AWSCreateInstance_2_InstanceSettings_1.png)

![AWSCreateInstance](../images/01/02_lab/AWSCreateInstance_2_InstanceSettings_2.png)

You will receive a message that the instance was successfully created.

![AWSCreateInstance](../images/01/02_lab/AWSCreateInstance_3_SuccesFullInitiated.png)

After a while, the Pending status also changes to Running to indicate that the server has also started successfully.

![AWSCreateInstance](../images/01/02_lab/AWSCreateInstance_4_RunningState.png)



### Giving the instance a static IP address (Elastic IP)

Everytime we restart the instance it wil get another IP address (and DNS name). 

![AWSCreateInstance](../images/01/02_lab/AWSElasticIP_0_IPChange.png)



We use this IP address (or DNS name) to connect to the server. Het is dus veel makkelijker indien de server hetzelfde IP adres (en DNS naam) zou houden in de toekomst.

To prevent changing the IP address, we will have to give the instance an Elastic (=static) IP.

On *AWS*, go to *EC2*.

![AWSCreateInstance](../images/01/02_lab/AWSElasticIP_1_Compute.png)



Click on *Elastic IPs* and then *Allocate Elastic IP address*.

![AWSCreateInstance](../images/01/02_lab/AWSElasticIP_2_AllocateElasticIP.png)



We create a new Elastic IP by clicking *Allocate*.

![AWSCreateInstance](../images/01/02_lab/AWSElasticIP_3_CreateElasticIP.png)

  

Click on *Actions* and then on *Associate Elastic IP address*.

![AWSCreateInstance](../images/01/02_lab/AWSElasticIP_4_AssociateElasticIP.png)



Select the *Instance* to which this Elastic IP address should be linked and click on *Associate*.

![AWSCreateInstance](../images/01/02_lab/AWSElasticIP_5_Associate.png)



The Elastic IP address has been successfully linked to our server instance.

![AWSCreateInstance](../images/01/02_lab/AWSElasticIP_6_Success.png)



We see that this has been successful when we look at the Instance again. If we now stop the instance and restart it afterwards, the IP address and associated DNS name will remain the same.

![AWSCreateInstance](../images/01/02_lab/AWSElasticIP_7_Success_2.png)



### Connecting to the Cloud instance

To work on the server instance, it is best to start a connection from our laptop via SSH. To request the data required for this, we do the following.

Click *Instances*. Then select the server instance and click *Connect*.

![AWSCreateInstance](../images/01/02_lab/AWSConnectInstance_0_Connect.png)





AWS suggests an SSH command with a certain key. 
But please note, our key on the laptop may be named differently if you followed different steps while creating the SSH keypair or if you already had a keypair.

![AWSCreateInstance](../images/01/02_lab/AWSConnectInstance_1_CopyCommand.png)





We start a Powershell or Windows Terminal and paste the command, but change the name of our key should this be necessary.

You can paste into a Powershell window by clicking the right mouse button.

![AWSCreateInstance](../images/01/02_lab/AWSConnectInstance_2_Connect_Logout.png)

As you can see in the previous screenshot, we are now logged in to the server. If you wish to leave the connection you can give the command *exit* or *logout*.





As an exercise, restart an ssh session with the instance and change the *name* of the server to *linux-ess* with the command:

***sudo hostnamectl set-hostname linux-ess***



![image-20240618102237878](../images/03/image-20240618102237878.png)

The name change will be visible in the prompt the next time you make an ssh connection.
