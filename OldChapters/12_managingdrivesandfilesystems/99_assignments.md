# Assignments CH11


To start these assignments, add a virtual drive of 1GB or use a USB flash drive of at least 1 GB.

## Task 1
Determine the device name of the drive you want to use.

## Task 2
Run a command to list the partition table of the virtual drive or the USB flash drive.

## Task 3
Delete all the partitions on your USB flash drive (or show how you would do this, if using a virtual drive). Save the changes, and make sure the changes were made both on the disk’s partition table and in the Linux kernel.

## Task 4
Add three partitions to the drive: 100MB Linux partition, 200MB swap partition, and 500MB LVM partition. Save the changes.

## Task 5
Put an ext4 filesystem on the Linux partition.

## Task 6
Create a mount point called /mnt/mypart, and mount the new Linux partition on it.

## Task 7
Enable the swap partition, and turn it on so additional swap space is immmediately available.

## Task 8
Create a volume group called abc from the LVM partition, create a 200MB logical volume from that group called data, add an ext4 partition, and then temporarily mount the logical volume on a new directory named /mnt/test. Check that it was successfully mounted.

## Task 9
Grow the logical volume from 200MB to 300MB.

## Task 10
Do what you need to do to safely remove the USB flash drive from the computer: unmount the Linux partition, turn off the swap partition, unmount the logical volume, and delete the volume group from the USB flash drive. 
