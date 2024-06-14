# Lab <!-- {docsify-ignore} -->
### Intro

In this course we follow Linus. Linus is a first year computer science student at the PXL university college. His hobbies are making music, going out and gaming.

He recently purchased Minecraft, a very popular sandbox game. He has spent hours in his own offline world and considers himself a Minecraft master. His friends also want to play the game and they often share stories about their adventures and builds. 

All of them have been watching Twitch where they noticed that streamers often play together in a shared world. Intrigued by the idea of a shared world, Linus finds himself searching for options to host one of those worlds himself. He reads online that he will need a *minecraft server*. This is a computer (server) that hosts the world and to which all the players can connect to using the internet.

This is *exactly* what Linus is looking for. After doing some research he finds out that setting up such a server is not an easy task. He reads about all kinds of concepts such as Linux, Unix, chmod, apt, ... that he never heard of before. As determined as Linus is, he will not rest before setting up a minecraft server called *LinusCraft* so he can play with his friends.

![linuscraft](../images/linuxcraft.png)

This is where our story begins. In this course we will follow Linus in a set of labs where we will use and learn new concepts with the goal of setting up and maintaining a minecraft server.  Before setting up this minecraft-server, he wants to advertise it via an own  webserver and website.

For the labs in this course we will use [Minetest](https://www.minetest.net/). This is an _open source_ project that looks alot like the real minecraft. The benefit of using Minetest is that it is free to play and support different operating systems out of the box.



### Course invitation email

Linus wants to use the Cloud to host his server. He will use Amazon Web Services.



To complete the labs, we first need to set up our AWS account.  The school gives you free access to AWS Cloud via the AWS Academy.

Normally you have received a *Course Invitation email* from *AWS Academy*.



![img](../images/01/AD_4nXcRfcpDy2ZTcDhBhQ2oX2Q7ZapfmFsv0onCUMkW0eACapSoFvg_nFXX8xjdCvLyNQalVcX3f_joW9boef7_pnJWcnYkpcvqfFl7zv-nYUTFFl_iEDLKKDIbhlPVBwVWO_VSB0S40LQxZoLx42zbzb87bKGn.png)

Click on *Get Started*.



![img](../images/01/AD_4nXeuHR6yChCyHrQWiIL4NPLhizGpnaXASUs0jARE1WZ7LrwROrPE8kNcWrHbLxIzWmgTTfqANU71cPm4TpfwHracl3_ala6S-VBPUKefg1Xv6Gf4Ge4pGKApeDaZDJPZVXQEBX0Ir9PRTp3ulBUElqRJ6JKI.png)

A Web browser opens with the option to register for the *Course*.

Click on *Create My Account*.



![img](../images/01/AD_4nXcxurlqwmJAVZwWIZ-_uNbxTtJmCyfBUjjLYqrDwr26E9fXrt8xbTDNaUFz9UE7uD_wPU1eZU9IEr_NS7nBD9MUy9IMtaykpgnqaraSCKHz3GSt3PaM34RZfnVaTslFCIr_mMhlAiSG_EzTvaS48RY7SwU.png)

Create a secure password and choose *Brussels* as the Time Zone. Check *I agree … Policy* and click *Register*.



![img](../images/01/AD_4nXfEtTnEnQ9bkqX9CEzmRbxiYgEIduZrwDD5HCsLPBjYRy0TjyaYUZNtRJlAwUb2kzQlVBau6fgK99AkGZMkjA-Z3fF3Obufpw8sbzJGxiGZR6qJZ6C_FSgwEblZJwH1tC3VGvyIjKqwR0zIiu50a8Bjn9ES.png)

Now you enter the *Course*.



### Change nickname and color of the Course

![img](../images/01/AD_4nXd2rbMHEk1uAf0JY-wzPQbx-8bwgKugk3Aonjam3nDb51G1-RPNAya1QgtzUSdnH7htSSgy2et899JRGLIBnBt7macrAmgnb3kyEzVTrVXn-Zqu8fAxhebVQjaCvUtt6sNuTcg74ZUWgFBb495nwQmHvBsL.png)

Click on *Dashboard* and then on the Course's *Hamburger Menu* to adjust the *Nickname* and *color*.



### **Opening a certain Course**

Can be done either via the *Dashboard*, or via *Courses*.



![img](../images/01/AD_4nXeBG6g0nvCDyIg2B1XvkTuZlsGZPX0u5MYeY4c0B3USeRGaPba5giP4JGc7lTdjA1-UAixAbtzuj0QRNvCkQNVA9DePRUmIaC9N9r1-esVru9G5t_9ePzEZdc8r5P53Ph4JXk-P6MoatIx_Z6ZCoruiyVVU.png)

Via the *Dashboard*.



![img](../images/01/AD_4nXdLTLPseelr0j1jb6WFT9c0FDtJ0gixTnrn_dKNDT62bYi9n1iHKxdmINenrtH6PAAOV3ovAekhYi7rT2UQby-BYCXRi5TRk4MI76UHcVAcTQlwqbiqt4Utfh1WOD5bgFFdXx74zC_bYLO3a98GIGDlLr8.png)

Via *Courses*.



![img](../images/01/AD_4nXcnK-lxpeD8xzWxWmvAscmwN1CFxPv4O8wW077HnWwp72QqYdZbP12ihzOvCPpf7res6SgWu78_xz1bEh3AMtWrCuvJ-4WtERmBfy5LINNnmAtU28c9lDHKxD-tl77yG8Upx47MTQedSC9O0ty3KXZZdJ8t.png)

Via *Courses* and then *All courses*.



### **Logging in as a Student on Canvas in the future**

If you want to log in to the course again in the future, surf to 

https://awsacademy.instructure.com/ 

This links to [https://www.awsacademy.com/LMS_Login](https://www.awsacademy.com/vforcesite/LMS_Login)

![img](../images/01/AD_4nXfzZlC-79qLNx2unD0hO9c51EJPCCZScX_tHXuG0ykBkqOiQNS3q3dk0xnwfwDqHoE4_DaW2-ldp-Wvg251EjKjkRmOflFkqIADPXoemnXynPXkRp6UAr9R2nLhO-ikA86Sb19JZ6I5iPsTjrTa4bzTQ5q8.png)

Click on *Student Login*.



![img](../images/01/AD_4nXc7iQDjZQ5vka8yKxPEuLFtQVQGoLfTu5sJesaqDkwuKTOYFF5Opq7vjLZCHm4SWLciBFs1-sw_PA530m2ME0vajwB5dLshxztJ0OyUHb00swRZuMCkK1XB-rK9nl_GwWFj-2DcJziuqI56CghpSkGeu8Vt.png)

Enter your *PXL email address* as login and your *password*.

Check *Stay signed in* and click *Sign in*.



![img](../images/01/AD_4nXcVqFTAuRyGcJsPv1Is6Y8hUiDVfUH6wLdFGmRdputIy7-Nn8H_pYAkxb0dcGYybn4SCrQ7OnnybcC1oyFFxi2JYck3XBXKWywa6hCvI3EkmLiJwyjPjixVh9VCSF1pb4lTGo7GST_DDq5ydo9BOU9Q8yYB.png)

You are now logged in.



### **Starting the Lab (via Vocareum)**

Attention!  Every time you want to use AWS Cloud in your course, you will have to go to *Courses,* then *Modules* and finally *Learner Lab*.

![img](../images/01/AD_4nXeCYhesCBYO1OmKraAXbs7nCbbR7-EDrW8tNIs6wRfrA3EuB2gETmg0v3zxVFzcIZ0Kl4dVLqs4mhBBkXpfF1ORBmq2UiYgvtehtO5g8kFDVHV1TxlKdmUOejhojsq4DFMUv7CssJioSLWsr2E82uPho7Rp.png)

Get in the right Class.



![img](../images/01/AD_4nXfm-q6_pEl52LoI2qlBo3FDLciFfrJoLNjh2Nw9ojMnlSZNOtpkn2xS9EtzRqHkTSZGjztjHvkA2gUuelumjskGqNCbUsF-TT5d89cSGjKh-zOLcbILUPWPme13-2OqfO_SfbjTsqRnud947V8ott_Ys99_.png)

In the Class, click on *Modules* and then on *Learner Lab*.



![img](../images/01/AD_4nXfZG68uqym-XcXobZg0wBMQ8u6ie_c_xQZVmMoggVDeV9M5EaCfBWqi8FT1-T8FJPl-bjV1rFIOEpm_PmSbo9QNNVfg4UXBtZLXWco6yAD5uVwbzHrxMWGgVwl0Lk2do2-RNdWcVpmlM7it0GmH88WFox6f.png)

The first time you must approve the License Agreement. *Scroll* down and **don't** click *Next*.



![img](../images/01/AD_4nXfWLjr3pgsVAvOcPIOh_w5Km1Iz-QHjnrqShBNBD93o-zxIzR6oTXNdCay2Z-CvGU3oJloSGyvnDD-KuXd1_6XdMxgBpvbjZVq6heIA68luayd0HFqkRqXji6EqKAhtf0wjmJGPNrPDMc9p-iNx8VFih5Fu.png)

Click *I Agree* and **not** *Next*.



![img](../images/01/AD_4nXfNvJh3t_2rcuOkJfThPjD4057r8bhIXAUsCIOmQ-_EPqqNN0var9CLEEGZJDf0_uaQO21rVnJJlDw3_A9EbfN7RG0F-t6GhS_cSm9-Qx0Uj68BAa-2jW9CwtES0Yx6QWeFlki1smEgrqEFVYZkMUXCnfs.png)

Click on *Start Lab* and **not** on *Next*.



The *Lab* is being started. This will take several minutes. As soon as the lab is fully started, we see a green dot behind *AWS* 

There is now also a clock running behind AWS. This indicates how long the servers will be *up and running*. It starts counting down from four hours remaining. You can always click Start Lab again to reset the timer to four hours.

After four hours the servers will be shut down, but can simply be restarted at a later time by clicking *Start Lab* again.

We also see how much of our $100 ($50 in the future) has already been spent. This may have a delay of about 8 hours.

Attention! Once you have used up the entire money, you will no longer be able to do anything on the Cloud Platform.



![img](../images/01/AD_4nXflRHJeDcQGXxOY7SP_zQNfz9rT_tPwcVoZXWTvV93uqN3gGV9mzVRUekJBK6mLRpfEQHyO5I8WWxKFAm9aCx7D-EsWoMOFAhmn6bGgDBoPsaF67_0rGhNxQAiZH6lfg9bnVTrDT_cP3KDrz1ZP-Vz8WCN7.png)

Click on *AWS* to go to the *AWS Cloud Platform*.

If a new tab is not opened, it is blocked by your web browser. You must then allow this for this website. Below is an example with the Firefox web browser.

![img](../images/01/AD_4nXd4D31ZEsKRHhh0PseGeIAgwihSq8FplWAnf5jMIEtrSRzIfq5zfCcYwR8Jh8oolNkANxN9yLXz7xwofwuU7yuitrlPRnAJLqIkZav6VP_PeaSYlV8FSKj0Qwq-HfBlM6iKeJTBm2rJluGw6KoxjNJ1cMrG.png)



![img](../images/01/AD_4nXdGJcQMK_vjoMB5XZJ6RqMeyk8GZu35HIvyvEMlvNn2DSEHKyJM6bQLQ4OAt1Uxv-NdtRIU8n9N-p9XUqLXWnKOvmxrUJUghq8gWjSTP2kGpCrttYPMzFp55702rAfsNWpakImQjcYZaXGH8L-218C69hKP.png)

Click on *Accept all cookies* and on *Next*.



![img](../images/01/AD_4nXfD-qwvrpKXDVRF_gmCa2X5udUNKSArDmHo1MFMuATQAkgeXwCgGuBVkWcykFHewOPHfsDhXtxhfSxS486cw9J-fzt0WskKtW0hZ9srjANDlya5oNjU5ispqDUn1tD-hHyRQGO_XpjHug0ldZRYeqr-mD0G.png)

We are ready to start working.



![img](../images/01/AD_4nXeFwCTVGXI1oiP2zBlxhtNmoxJezfHmRxYGm7944MyiKk9DzTJ4DgAMgprocyQRWvi8x8wp6fD3mWZye-m23mrYeH7UI0UK3dUf22HlqxuYcAafS9fkluKIHJeAJv35i2cP8aEfokMF_wIztA13C_YeRpjE.png)

We will use some of these *MenuItems* in this course.



# **Vocareum AWS Details**

![img](../images/01/AD_4nXdyHKwucY4XqTKhiKHmpRH22Fn3lNwQ8msHw93Mu7QaEZeSwIhQKSfKSS54-df52IJDDNfdZQD5L2Lz0CeUSJexro0BUoHHoPzDOWPodIqzY85B9PN4fs4V_EE5O54s8722bLnHUC7deeAhjUuRSt95oP-J.png)

The gray box with Interface is a terminal window and can be used, for example, to fire AWS CLI commands or Python code (via an AWS SDK). Or connect to your Instances (=Servers) with SSH.

At the top we also find some useful buttons. Below an overview

![img](../images/01/AD_4nXf2CygDEDQoTPg_cQL23CqKygTcbfQfPMKnpAuQ4_QQLQY3W5YVSFgHhcZxvPDnOC9xqoh1A9vk7--h4lDLrk2QUWkJ6iaSllPeAKbGpwjxMIk8enVpsJ2DJlxSyhrhCSW_FmQU3w6m7_mbPQvp_MQUGik.png)![img](../images/01/AD_4nXf2CygDEDQoTPg_cQL23CqKygTcbfQfPMKnpAuQ4_QQLQY3W5YVSFgHhcZxvPDnOC9xqoh1A9vk7--h4lDLrk2QUWkJ6iaSllPeAKbGpwjxMIk8enVpsJ2DJlxSyhrhCSW_FmQU3w6m7_mbPQvp_MQUGik.png)



**AWS** : By clicking on this text we navigate to AWS Management 
		Console. It is through this interface that we create a Cloud Infrastructure 
		can start setting up. Tip! If there is no new tab 
 		open, click on the text at the top of the window to get *Popups* 
 		to allow

**Used $0 till $100** : How much budget you have already used. Attention! This just keeps changing 
 		updated every 8 to 12 hours

**03:39** : Remaining time until the Cloud infrastructure is brought down. You 
		can then click on *Start Lab* again to restart the infrastructure.
 		Tip! You can click *Start Lab* again at any time to restart the timer 
 		to be brought back to four hours

**Start Lab** : To (re)start the Cloud Infrastructure. Some services 
 		will have to be restarted manually

**End Lab** : To bring down the Cloud Infrastructure. You can do these afterwards 
		restart with *Start Lab*

**AWS Details** : Shows how long the Cloud infrastructure has now and in total 
 		turned. Also provides the opportunity to use your personal SSH keys
 		view/download

**Readme** : Contains links to pages explaining how the *AWS Cloud Platform*

**Reset**: Everything on AWS under your account (= linked to this course) will be reset 
 		reset. In other words, everything you've ever done ends 
		 AWS removed from this account. You don't get any money spent 
 		budget back.

**⤱ <maximize>** : To maximize the Vocareum window. To undo this press the *Esc* key
