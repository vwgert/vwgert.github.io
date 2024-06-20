# Assignment on installation

## Task 1 - Download Ubuntu Desktop

Linux also has a desktop version. Download [Ubuntu Desktop](https://ubuntu.com/download/desktop).

![DownloadUbuntuDesktop](../images/02/GetUbuntuDesktop_Download_Ubuntu.png)

## Task 2 - Install Ubuntu Desktop

Install [Ubuntu Desktop](https://ubuntu.com/download/desktop) in a new virtual machine and explore the interface.

### Create the new VM

To create a new virtual machine (VM) in VMWare you go to the menu `file`>`New virtual machine`. The wizard to create a new VM will appear.

![VMware File New Vm](../images/02/VMware_File_New_VM.png)

In the first screen we select the option `Typical`:

![VMware Install Typical](../images/02/VMware_Typical.png)

Next we choose to `install the operating system later`:

![VMware Install Operating System Later](../images/02/VMware_Operating_System_Later.png)

Next we choose the operating system `Linux`. In the version dropdown we select `Ubuntu 64 bit`. This is the Linux distribution that we will use during this course.

![VMware Ubuntu 64bit](../images/02/VMware_Ubuntu_64bit.png)

In the next screen we give the virtual machine a name. You can also specify a different folder to store the virtual machine on your computer.

?> <i class="fa fa-exclamation-circle" style="font-size:48px;color:red"></i> Let op dat je de bestanden van de VM niet opslaat in een map die gesynced wordt met de cloud (OneDrive, Dropbox, Google Drive)?. Je VM zal crashen en je zal alles in de VM kwijt zijn!

![VMware Name The VM](../images/02/LAB_VMware_Name_The_VM.png)

In the next screen we configure the virtual harddisk size for the VM. We will create a disk that has 30GB of storage. Keep in mind that the disk space will be allocated while saving files (max 30GB):

![VMware Disk Size](../images/02/LAB_VMware_Disk_Size.png)

We have to click on `Customize Hardware` to configure the virtual machine a little more:

![VMware Customize Hardware](../images/02/LAB_VMware_Customize_Hardware.png)

We still have to link the Ubuntu-server ISO file to the virtual CD-rom drive. We do this by selecting `New CD/DVD` and browsing to the downloaded `iso` file:

![VMware Select ISO](../images/02/LAB_VMware_Select_ISO.png)

Click on `Finish` and the virtual machine will be created.

![VMware Finish](../images/02/LAB_VMware_Finish.png)

All that's left to set is the UEFI bios. Click on `Edit virtual machine settings`.

![VMware-afwerking](../images/02/LAB_VMware_UEFI_1.png)

Go to the tab `Options`, click on `Advanced` and select the option `UEFI`. Note that you'll also find the setting `Side channel mitigations` here if you should see a warning when you start this Virtual Machine later on.

![VMware-afwerking](../images/02/LAB_VMware_UEFI_2.png)

You can now boot the VM by clicking the green arrow icon. This will boot the virtual machine and run the installation process.

![VMware Finish](../images/02/LAB_VMware_Start_VM.png)

### Installation Ubuntu Desktop

?> <i class="fa-solid fa-circle-info"></i> Does booting the VM result in the error `This host supports Intel VT-x, but Intel VT-x is diabled`? You will have to activate the VT-X option in the BIOS of your laptop. More information can be found in [this article](https://www.qtithow.com/2020/12/fix-error-this-host-supports-Intel-VT-x.html).

When booting the VM for the first time we need to press `enter` or wait 30 seconds:

![Ubuntu_Desktop_First_Grub](../images/02/LAB_Ubuntu_Desktop_First_Grub.png)

We have to wait a few seconds for the boot to finish:

![Ubuntu_Desktop_First_Boot_Screen](../images/02/LAB_Ubuntu_Desktop_First_Boot_Screen.png)

In the next few steps there will be an installation process that we need to go through.

We choose the language:

![Ubuntu_Desktop_Try_Or_Install](../images/02/LAB_Ubuntu_Desktop_Install_Steps_01.png)

We don't specify anything for Accessibility:

![Ubuntu_Desktop_Keyboard_AZERTY](../images/02/LAB_Ubuntu_Desktop_Install_Steps_02.png)

We choose the correct keyboard layout. For `azerty` we select `Belgian`:

?> <i class="fa-solid fa-circle-info"></i> If you have a QWERTY keyboard you have to stick with `English (US)`:


![Ubuntu_Desktop_Normal_Install](../images/02/LAB_Ubuntu_Desktop_Install_Steps_03.png)

We have to choose the wired connection because we are using virtualisation:

![Ubuntu_Desktop_Erase_Disk](../images/02/LAB_Ubuntu_Desktop_Install_Steps_04.png)

We make the choice to Install:

![Ubuntu_Desktop_Erase_Disk](../images/02/LAB_Ubuntu_Desktop_Install_Steps_05.png)

We choose to do the installation interactively:

![Ubuntu_Desktop_Erase_Disk](../images/02/LAB_Ubuntu_Desktop_Install_Steps_06.png)

We choose to have only the default selection of apps installed:

![Ubuntu_Desktop_Erase_Disk](../images/02/LAB_Ubuntu_Desktop_Install_Steps_07.png)

We choose to have third-party software installed for drivers and multimedia formats:

![Ubuntu_Desktop_Erase_Disk](../images/02/LAB_Ubuntu_Desktop_Install_Steps_08.png)

We choose to erase the disk and install Ubuntu Desktop on it:

?> <i class="fa-solid fa-circle-info"></i> Mind that you erase the Virtual Disk of your VM, but it's a clean disk on which we are installing. `The hard disk of your computer/laptop will not be erased!`

![Ubuntu_Desktop_Erase_Disk](../images/02/LAB_Ubuntu_Desktop_Install_Steps_08b.png)

We specify the username and password, and the computername:

![Ubuntu_Desktop_Write_Changes_To_Disk](../images/02/LAB_Ubuntu_Desktop_Install_Steps_09.png)

For the TimeZone we pinpoint Brussels on the map or write it in the textbox:

![Ubuntu_Desktop_TimeZone_Brussels](../images/02/LAB_Ubuntu_Desktop_Install_Steps_11.png)

Click on Install to continue:

![Ubuntu_Desktop_Username_and_Computername](../images/02/LAB_Ubuntu_Desktop_Install_Steps_12.png)

Now we have to wait untill the installation has finished:

![Ubuntu_Desktop_Installaton_Runs](../images/02/LAB_Ubuntu_Desktop_Install_Steps_13.png)

Once the installation is finished we have to click on `Restart Now` to reboot the VM:

![Ubuntu_Desktop_Reboot_After_Install](../images/02/LAB_Ubuntu_Desktop_Install_Steps_14.png)

When we see the screen where they ask to push the 'enter'-key, we first go into the settings of the Virtual Machine :

![Ubuntu_Server_VM_Settings](../images/02/Ubuntu_Server_VM_Settings.png)

There we uncheck that the CD/DVD has to be connected at boot time (otherwise the installation will load again each time we boot)

![Ubuntu_Server_Disable_CDROM](../images/02/Ubuntu_Server_Disable_CDROM.png)

And then we push the 'enter'-key to finilize the installation with rebooting the Virtual Machine

![Ubuntu_Desktop_Enter_to_Restart](../images/02/LAB_Ubuntu_Desktop_Install_Steps_15.png)

## Task 3 - Login for the first time

The very first time we log\`in we have to go through some configuration screens:

![Ubuntu_Desktop_First_Login_Click_Student](../images/02/LAB_Ubuntu_Desktop_First_Login_Click_Student.png)

![Ubuntu_Desktop_First_Login_Enter_Password](../images/02/LAB_Ubuntu_Desktop_First_Login_Enter_Password.png)

![Ubuntu_Desktop_First_Login_Online_Accounts](../images/02/LAB_Ubuntu_Desktop_First_Login_SetupProfile_01.png)

![Ubuntu_Desktop_First_Login_Online_Accounts](../images/02/LAB_Ubuntu_Desktop_First_Login_SetupProfile_02.png)

![Ubuntu_Desktop_First_Login_LivePatch](../images/02/LAB_Ubuntu_Desktop_First_Login_SetupProfile_03.png)

![Ubuntu_Desktop_First_Login_Help_Improve](../images/02/LAB_Ubuntu_Desktop_First_Login_SetupProfile_04.png)

Now we are ready to explore Ubuntu Desktop:

![Ubuntu_Desktop_First_Login_Privacy](../images/02/LAB_Ubuntu_Desktop_First_Login_SetupProfile_05.png)

## Task 4 - Take a snapshot of the VM

Before doing anything else, it's good practice to take a snapshot. If, at a later time, our Ubuntu Desktop breaks, we can allways return to this snapshot.
Being able to roll back to this point is a time saver, because otherwise we have to reinstall the Linux system again from scratch.

When there are some updates waiting it is always nice to do these first.

![Ubuntu_Desktop_First_Login_Software_Updater](../images/02/LAB_Ubuntu_Desktop_First_Login_Software_Updater.png)

`Take a snapshot of the Ubuntu Desktop VM, named "Clean Install"` as follows:

*First shutdown the VM...*

![Ubuntu_Desktop_Snapshot_Poweroff](../images/02/LAB_Ubuntu_Desktop_Snapshot_Poweroff.png)

![Ubuntu_Desktop_Snapshot_Poweroff_Confirm](../images/02/LAB_Ubuntu_Desktop_Snapshot_Poweroff_Confirm.png)

*VM/Snapshot/Take Snapshot...*

![Ubuntu_Desktop_Snapshot_Take_Snapshot](../images/02/LAB_Ubuntu_Desktop_Snapshot_Take_Snapshot.png)

![Ubuntu_Desktop_Snapshot_Take_Snapshot_Name](../images/02/LAB_Ubuntu_Desktop_Snapshot_Take_Snapshot_Name.png)

?> <i class="fa-solid fa-circle-info"></i> At a later time you can always go back to this savepoint in time with:

*VM/Snapshot/Revert to Snapshot...*

![Ubuntu_Desktop_Snapshot_Revert_To_Snapshot](../images/02/LAB_Ubuntu_Desktop_Snapshot_Revert_To_Snapshot.png)





## Task 5 - Explore the Desktop Environment

In the Ubuntu desktop machine, try to execute the following subtasks:

* Change the wallpaper
* Create a new text file with the tool "Text Editor" (=gedit) and try to save it in your documents folder
* Check with the file explorer (Files) if the file exists
* Delete the file and empty the trash
* Pin (=Favorite) the Terminal -application to the Dock (=launcher)
* Surf with Firefox to the school website
* Install the Chromium webbrowser, start the app, pin it to the Dock and place it above the Firefox icon
* Surf with Chromium to your school webmail portal
* Install wps-office and test the apps
* Install Spotify and test the app
* Install Visual Studio Code and test the app
* Install Gimp and take a look at the app