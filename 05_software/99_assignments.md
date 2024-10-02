# Assignment on software

In this assignment we will use `apt` instead of `apt-get` and `apt-cache` which are older commands

## Task 1
Update the local apt cache. This will get the latest info from the repositories  

## Task 2
Upgrade all packages installed with _apt_ to the latest available version  

## Task 3
Search with apt for a package that has something to do with 'usage and stats'. You will see `btop` as one of the results. Install the package and run the app  

## Task 4
Search with apt for a package that has something to do with 'colorful cat'. You will see `lolcat` as one of the results. Install the package and run the following commands:  
cd  
cat .bash_history  
lolcat .bash_history  

## Task 5
Install with apt the package 'neofetch' and run the app  

## Task 6
Search with apt for "the matrix" and search within the first 5 presented packages and install the package which resembles the display of the matrix movie. Run the app  

## Task 7
Remove the package btop from the system. You shouldn't be able to run it anymore  

## Task 8
List all the packages that are installed with apt. In the list you will see one entry for `caca-utils`. If not, install this package and check again. Search in the manpage of 'apt' how you can see some info of this packages. You will see that this package holds several utilities. Try the last two. Tip: You can push 'enter' to try and see different things. Use `ctrl+c` to quit a utility.  

## Task 9
Search for a snap package via the description "resource monitor"    

## Task 10
Install the snap `bashtop`  

## Task 11
Run bashtop    

## Task 12
We don't get any info about the disks. This is because the snap needs permissions to be connected with the mount-plug.  
Read the information about the snap `bashtop` to find a solution.  
Run the command to solve the problem    
Run bashtop again  

## Task 13
Show a list of installed snaps  

## Task 14
Remove the snap bashtop  

## Task 15
Show a list of installed snaps to check if the snap is removed  

## Task 16
Show the history of changes in snap  

## Task 17
Check if the snap 'asciiquarium' exists. Read some info about the snap, install it and run it  
    
## Task 18
Zip the _homedirectory_ of the user student (with all files and folders) into a file called _/tmp/myhomefolder.zip_.  
View the contents of the zipfile to check the result.  

## Task 19
Search the manpage of zip to find out how you can delete a file from your zipfile.  
Delete the file .bash_history from the zipfile _/tmp/myhomefolder.zip_  
Check the contents of the zipfile.  

## Task 20
Make a directory called _zipdemo_ in the temporary folder (_/tmp_).  
Unzip the zipfile _myhomefolder.zip_ in the directory _/tmp/zipdemo_ 
Use `tree` to check if the process completed successfully.

## Task 21
Make a tarball called _/tmp/myhomefolder.tar.gz_ with the files and folders of the _homedirectory_ of the user student.  
View the contents of the tarfile to check the result.  
Make a directory called _tardemo_ in the temporary folder (_/tmp_).  
Extract the tarball _myhomfolder.tar.gz_ in the directory _/tmp/tardemo_  

## Task 22
Extra Challenge: Try to remove the file _.bashrc_ from the tarball (task 21)  
Search the manpage of tar to find a solution.  
Check the contents of the tarball at the end of the exercise.   

## Task 23
Try and install google chrome on your ubuntu Desktop with the command line interface.  
As you can see when you search for a download, you'll only find a .deb package to download. Use this package with dpkg to install google chrome.   

More difficult: Try to download this .deb package with wget to accomplish the full installation in your CLI.

