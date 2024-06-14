# Lab <!-- {docsify-ignore} -->
### Intro

In deze cursus volgen we Linus. Linus is eerstejaars informaticastudent aan de hogeschool PXL. Zijn hobby's zijn muziek maken, uitgaan en gamen. 

Hij kocht onlangs Minecraft, een zeer populaire sandbox-game. Hij heeft uren doorgebracht in zijn eigen offline wereld en beschouwt zichzelf als een Minecraft-meester. Zijn vrienden willen het spel ook spelen en ze delen vaak verhalen over hun avonturen en bouwwerken.  

Ze hebben allemaal naar Twitch gekeken, waar ze merkten dat streamers vaak samen spelen in een gedeelde wereld. Geïntrigeerd door het idee van een gedeelde wereld, zoekt Linus naar opties om zelf een van die werelden te hosten. Hij leest online dat hij een *minecraft server* nodig heeft. Dit is een computer die de wereld host en naar waar alle spelers kunnen verbinden met behulp van het internet. 

Dit is *precies* wat Linus zoekt. Na wat onderzoek komt hij erachter dat het opzetten van zo'n server geen gemakkelijke taak is. Hij leest over allerlei concepten zoals Linux, Unix, chmod, apt, ... waar hij nog nooit van gehoord had. Hoe vastberaden Linus ook is, hij zal niet rusten voordat hij een minecraft-server genaamd *LinusCraft* heeft opgezet, zodat hij met zijn vrienden kan spelen. 

![Linuscraft](../images/linuxcraft.png) 

Hier begint ons verhaal. In deze cursus volgen we Linus in een reeks labs waar we nieuwe concepten zullen gebruiken en leren met als doel het opzetten en onderhouden van een minecraft-server.  Vooraleer hij deze minecraft-server opzet, wil hij ook de nodige reclame maken via een eigen webserver en website.

Voor de labs in deze cursus gebruiken we [Minetest](https://www.minetest.net/). Dit is een _open source_ project dat veel lijkt op het echte minecraft. Het voordeel van het gebruik van Minetest is dat het gratis is om te spelen en verschillende besturingssystemen ondersteund.



### Cursus-uitnodigings-mail

Linus wil gebruik maken van de Cloud om zijn server te hosten. Hij zal gebruik maken van Amazon Web Services.



Om de labs af te werken dienen we eerst ons account voor AWS in orde te brengen.  Via de school krijg je gratis toegang tot AWS Cloud via de AWS Academy.

Normaal gezien heb je een *Course Invitation mail* ontvangen van *AWS Academy*.

![img](../images/01/AD_4nXcRfcpDy2ZTcDhBhQ2oX2Q7ZapfmFsv0onCUMkW0eACapSoFvg_nFXX8xjdCvLyNQalVcX3f_joW9boef7_pnJWcnYkpcvqfFl7zv-nYUTFFl_iEDLKKDIbhlPVBwVWO_VSB0S40LQxZoLx42zbzb87bKGn.png)

Klik op *Get Started*.



![img](../images/01/AD_4nXeuHR6yChCyHrQWiIL4NPLhizGpnaXASUs0jARE1WZ7LrwROrPE8kNcWrHbLxIzWmgTTfqANU71cPm4TpfwHracl3_ala6S-VBPUKefg1Xv6Gf4Ge4pGKApeDaZDJPZVXQEBX0Ir9PRTp3ulBUElqRJ6JKI.png)

Er opent een Webbrowser met de mogelijkheid om in te schrijven voor de *Cursus*.

Klik op *Create My Account*.



![img](../images/01/AD_4nXcxurlqwmJAVZwWIZ-_uNbxTtJmCyfBUjjLYqrDwr26E9fXrt8xbTDNaUFz9UE7uD_wPU1eZU9IEr_NS7nBD9MUy9IMtaykpgnqaraSCKHz3GSt3PaM34RZfnVaTslFCIr_mMhlAiSG_EzTvaS48RY7SwU.png)

Maak een veilig wachtwoord en kies als Time Zone *Brussels*. Vink *I agree … Policy*  aan en klik op *Register*.



![img](../images/01/AD_4nXfEtTnEnQ9bkqX9CEzmRbxiYgEIduZrwDD5HCsLPBjYRy0TjyaYUZNtRJlAwUb2kzQlVBau6fgK99AkGZMkjA-Z3fF3Obufpw8sbzJGxiGZR6qJZ6C_FSgwEblZJwH1tC3VGvyIjKqwR0zIiu50a8Bjn9ES.png)

Nu kom je terecht in de *Cursus*.



### Bijnaam en kleur wijzigen van de Cursus

![img](../images/01/AD_4nXd2rbMHEk1uAf0JY-wzPQbx-8bwgKugk3Aonjam3nDb51G1-RPNAya1QgtzUSdnH7htSSgy2et899JRGLIBnBt7macrAmgnb3kyEzVTrVXn-Zqu8fAxhebVQjaCvUtt6sNuTcg74ZUWgFBb495nwQmHvBsL.png)

Klik op *Dashboard* en vervolgens op het *Hamburgermenu* van de Cursus om de *Bijnaam* en de *kleur* aan te passen.



### **Openen van een bepaalde Cursus**

Kan ofwel via het *Dashboard*, ofwel via *Cursussen*.

![img](../images/01/AD_4nXeBG6g0nvCDyIg2B1XvkTuZlsGZPX0u5MYeY4c0B3USeRGaPba5giP4JGc7lTdjA1-UAixAbtzuj0QRNvCkQNVA9DePRUmIaC9N9r1-esVru9G5t_9ePzEZdc8r5P53Ph4JXk-P6MoatIx_Z6ZCoruiyVVU.png)

Via het *Dashboard*.



![img](../images/01/AD_4nXdLTLPseelr0j1jb6WFT9c0FDtJ0gixTnrn_dKNDT62bYi9n1iHKxdmINenrtH6PAAOV3ovAekhYi7rT2UQby-BYCXRi5TRk4MI76UHcVAcTQlwqbiqt4Utfh1WOD5bgFFdXx74zC_bYLO3a98GIGDlLr8.png)

Via *Cursussen*.



![img](../images/01/AD_4nXcnK-lxpeD8xzWxWmvAscmwN1CFxPv4O8wW077HnWwp72QqYdZbP12ihzOvCPpf7res6SgWu78_xz1bEh3AMtWrCuvJ-4WtERmBfy5LINNnmAtU28c9lDHKxD-tl77yG8Upx47MTQedSC9O0ty3KXZZdJ8t.png)

Via *Cursussen* en vervolgens *Alle cursussen*.



### **Inloggen als Student op Canvas**

Als je in de toekomst opnieuw wilt inloggen op de cursus surf je naar 

https://awsacademy.instructure.com/ 

Dit linkt door naar [https://www.awsacademy.com/LMS_Login](https://www.awsacademy.com/vforcesite/LMS_Login) 

![img](../images/01/AD_4nXfzZlC-79qLNx2unD0hO9c51EJPCCZScX_tHXuG0ykBkqOiQNS3q3dk0xnwfwDqHoE4_DaW2-ldp-Wvg251EjKjkRmOflFkqIADPXoemnXynPXkRp6UAr9R2nLhO-ikA86Sb19JZ6I5iPsTjrTa4bzTQ5q8.png)

Klik op *Student Login*.



![img](../images/01/AD_4nXc7iQDjZQ5vka8yKxPEuLFtQVQGoLfTu5sJesaqDkwuKTOYFF5Opq7vjLZCHm4SWLciBFs1-sw_PA530m2ME0vajwB5dLshxztJ0OyUHb00swRZuMCkK1XB-rK9nl_GwWFj-2DcJziuqI56CghpSkGeu8Vt.png)

Geef je *PXL email adres* als login en je *wachtwoord*.

Vink *Aangemeld blijven* aan en klik op *Aanmelden*.



![img](../images/01/AD_4nXcVqFTAuRyGcJsPv1Is6Y8hUiDVfUH6wLdFGmRdputIy7-Nn8H_pYAkxb0dcGYybn4SCrQ7OnnybcC1oyFFxi2JYck3XBXKWywa6hCvI3EkmLiJwyjPjixVh9VCSF1pb4lTGo7GST_DDq5ydo9BOU9Q8yYB.png)

Je bent nu ingelogd.



### **Starten van het Lab (via Vocareum)**

Opgelet!  Je zal telkens je gebruik wilt maken van AWS Cloud in je cursus moeten gaan en vervolgens op *Courses,* dan *Modules* en als laatste *Learner Lab* moeten klikken.

![img](../images/01/AD_4nXeCYhesCBYO1OmKraAXbs7nCbbR7-EDrW8tNIs6wRfrA3EuB2gETmg0v3zxVFzcIZ0Kl4dVLqs4mhBBkXpfF1ORBmq2UiYgvtehtO5g8kFDVHV1TxlKdmUOejhojsq4DFMUv7CssJioSLWsr2E82uPho7Rp.png)

Ga in de juiste Class.



![img](../images/01/AD_4nXfm-q6_pEl52LoI2qlBo3FDLciFfrJoLNjh2Nw9ojMnlSZNOtpkn2xS9EtzRqHkTSZGjztjHvkA2gUuelumjskGqNCbUsF-TT5d89cSGjKh-zOLcbILUPWPme13-2OqfO_SfbjTsqRnud947V8ott_Ys99_.png)

Klik in de Class op *Modules* en vervolgens op *Learner Lab*.



![img](../images/01/AD_4nXfZG68uqym-XcXobZg0wBMQ8u6ie_c_xQZVmMoggVDeV9M5EaCfBWqi8FT1-T8FJPl-bjV1rFIOEpm_PmSbo9QNNVfg4UXBtZLXWco6yAD5uVwbzHrxMWGgVwl0Lk2do2-RNdWcVpmlM7it0GmH88WFox6f.png)

De eerste keer moet je de License Agreement goedkeuren. *Scroll* naar onder en klik **niet** op *Next*.



![img](../images/01/AD_4nXfWLjr3pgsVAvOcPIOh_w5Km1Iz-QHjnrqShBNBD93o-zxIzR6oTXNdCay2Z-CvGU3oJloSGyvnDD-KuXd1_6XdMxgBpvbjZVq6heIA68luayd0HFqkRqXji6EqKAhtf0wjmJGPNrPDMc9p-iNx8VFih5Fu.png)

Klik op *I Agree* en **niet** op *Next*.



![img](../images/01/AD_4nXfNvJh3t_2rcuOkJfThPjD4057r8bhIXAUsCIOmQ-_EPqqNN0var9CLEEGZJDf0_uaQO21rVnJJlDw3_A9EbfN7RG0F-t6GhS_cSm9-Qx0Uj68BAa-2jW9CwtES0Yx6QWeFlki1smEgrqEFVYZkMUXCnfs.png)

Klik op *Start Lab* en **niet** op *Next*.



Het *Lab* wordt gestart. Dit duurt wel enkele minuten. Van zodra het lab volledig is opgestart zien we een groen bolletje achter *AWS* 

Er loopt nu ook een klok achter AWS. Deze geeft aan hoelang de servers nog *up and running* zullen zijn. Het begint af te tellen vanaf vier uur resterend. Je kan altijd opnieuw op Start Lab klikken om de timer opnieuw op vier uur te zetten.

Na vier uur worden de servers afgesloten, maar kunnen op een later tijdstip gewoon opnieuw worden opgestart door opnieuw op *Start Lab* te klikken.

Tevens zien we hoeveel er reeds van onze $100 ($50 in de toekomst) is gespendeerd. Dit kan wel een vertraging hebben van een 8-tal uur.

Opgelet! Van zodra als je het volledige $geld hebt opgebruikt zal je niets meer kunnen doen op het Cloudplatform.

![img](../images/01/AD_4nXflRHJeDcQGXxOY7SP_zQNfz9rT_tPwcVoZXWTvV93uqN3gGV9mzVRUekJBK6mLRpfEQHyO5I8WWxKFAm9aCx7D-EsWoMOFAhmn6bGgDBoPsaF67_0rGhNxQAiZH6lfg9bnVTrDT_cP3KDrz1ZP-Vz8WCN7.png)

Klik op *AWS* om naar het *AWS Cloudplatform* te gaan.

Indien er geen nieuw tabblad wordt geopend, wordt dit geblokkeerd door je webbrowser. Je dient dit dan toe te laten voor deze website. Hieronder een voorbeeld met de Firefox-webbrowser.

![img](../images/01/AD_4nXd4D31ZEsKRHhh0PseGeIAgwihSq8FplWAnf5jMIEtrSRzIfq5zfCcYwR8Jh8oolNkANxN9yLXz7xwofwuU7yuitrlPRnAJLqIkZav6VP_PeaSYlV8FSKj0Qwq-HfBlM6iKeJTBm2rJluGw6KoxjNJ1cMrG.png)



![img](../images/01/AD_4nXdGJcQMK_vjoMB5XZJ6RqMeyk8GZu35HIvyvEMlvNn2DSEHKyJM6bQLQ4OAt1Uxv-NdtRIU8n9N-p9XUqLXWnKOvmxrUJUghq8gWjSTP2kGpCrttYPMzFp55702rAfsNWpakImQjcYZaXGH8L-218C69hKP.png)

Klik op *Accept all cookies* en op *Next*.



![img](../images/01/AD_4nXfD-qwvrpKXDVRF_gmCa2X5udUNKSArDmHo1MFMuATQAkgeXwCgGuBVkWcykFHewOPHfsDhXtxhfSxS486cw9J-fzt0WskKtW0hZ9srjANDlya5oNjU5ispqDUn1tD-hHyRQGO_XpjHug0ldZRYeqr-mD0G.png)

We zijn klaar om te beginnen werken.



![img](../images/01/AD_4nXeFwCTVGXI1oiP2zBlxhtNmoxJezfHmRxYGm7944MyiKk9DzTJ4DgAMgprocyQRWvi8x8wp6fD3mWZye-m23mrYeH7UI0UK3dUf22HlqxuYcAafS9fkluKIHJeAJv35i2cP8aEfokMF_wIztA13C_YeRpjE.png)

Een aantal van deze *MenuItems* zullen we in deze cursus gaan gebruiken.



# **Vocareum AWS Details**

![img](../images/01/AD_4nXdyHKwucY4XqTKhiKHmpRH22Fn3lNwQ8msHw93Mu7QaEZeSwIhQKSfKSS54-df52IJDDNfdZQD5L2Lz0CeUSJexro0BUoHHoPzDOWPodIqzY85B9PN4fs4V_EE5O54s8722bLnHUC7deeAhjUuRSt95oP-J.png)

De grijze kader met Interface is een terminal venster en kan gebruikt worden om bijvoorbeeld AWS CLI commando's of python code (via een AWS SDK) af te vuren. Of met SSH te verbinden naar je Instances (=Servers)

Bovenaan vinden we ook nog wat nuttige knoppen. Hieronder een overzicht

![img](../images/01/AD_4nXf2CygDEDQoTPg_cQL23CqKygTcbfQfPMKnpAuQ4_QQLQY3W5YVSFgHhcZxvPDnOC9xqoh1A9vk7--h4lDLrk2QUWkJ6iaSllPeAKbGpwjxMIk8enVpsJ2DJlxSyhrhCSW_FmQU3w6m7_mbPQvp_MQUGik.png)![img](https://lh7-us.googleusercontent.com/docsz/AD_4nXf2CygDEDQoTPg_cQL23CqKygTcbfQfPMKnpAuQ4_QQLQY3W5YVSFgHhcZxvPDnOC9xqoh1A9vk7--h4lDLrk2QUWkJ6iaSllPeAKbGpwjxMIk8enVpsJ2DJlxSyhrhCSW_FmQU3w6m7_mbPQvp_MQUGik?key=1I7ADgn2TLyya6bv3dP9wg)



**AWS** 			: Door op deze tekst te klikken navigeren we naar de AWS Management 
			 	  Console. Het is via deze interface dat we een Cloud Infrastructuur 
			 	  kunnen gaan opzetten. Tip! Indien er geen nieuw tabblad wordt 
 			 	  geopend dien je bovenaan het venster te klikken op de tekst om *Popups* 
 			 	  toe te laten

**Used $0 of $100**	: Hoeveel budget je reeds hebt opgebruikt. Opgelet! Dit wordt maar om 
 			 	  de 8 à 12 uur geupdated

**03:39**			: Resterende tijd totdat de Cloud-infrastructuur wordt down gebracht. Je 
			 	  kan nadien opnieuw op *Start Lab* klikken om de infra weer op te starten.
 			 	  Tip! Je kan op ieder moment opnieuw op *Start Lab* klikken om de timer 
 			 	  opnieuw op vier uur te brengen

**Start Lab**		: Om de Cloud Infrastructuur (opnieuw) op te starten. Sommige services 
 			 	  zullen wel handmatig opnieuw moeten worden opgestart

**End Lab**		: Om de Cloud Infrastructuur down te brengen. Je kan deze nadien 
			 	  opnieuw opstarten met *Start Lab*

**AWS Details**		: Toont hoelang de Cloud infrastructuur nu en in het totaal heeft 
 			 	  gedraaid. Geeft ook de gelegenheid om je persoonlijke SSH keys te
 			 	  bekijken/downloaden

**Readme** 		: Bevat linken naar paginas met uitleg over de werking van het *AWS Cloud Platform*

**Reset**			: Alles op AWS onder je account (=gekoppeld aan deze course) wordt 
 			 	  gereset. Met andere woorden wordt alles wat je ooit gedaan hebt op 
			 	   AWS onder dit account verwijderd. Je krijgt wel geen gespendeerd 
 			 	  budget terug.

**⤱ <maximize>**	: Om het Vocareum venster te maximaliseren. Om dit ongedaan te maken
			 	  druk je op de *Esc* toets

