
# Increase or Decrease the Size of Static Partition in Linux

In this blog, I am going to discuss how to resize the static partition in Linux with the help of the resize2fs command. The basic prerequisite for this task is Linux partition.

Linux Partition:

A hard disk can be divided into several partitions. Each partition functions as if it were a separate hard disk. There are several reasons why we create the partition:

multiple operating systems on the same disk.

different file systems on different partitions.

more efficient disk space management.

different security settings on different partitions.

easier backup procedure.

Task Description:

In this task, we have to increase or decrease the size of static partition Linux. In Linux, the primary partition that we crease don’t allow to increase or decrease the partition size if we do we have to change the format it again but the issues are that if we format the partition again then we will not be able to access the data that we had stored. So we have to find some way through which we can increase or decrease the size of the static partition by formatting it again.

Step 1: Add one Hard Disk to the VM

In the first step add one hard disk to the VM, we can see the hard disk with the fdisk command.

fdisk -l

Image for post

Here we can see that one new hard disk with the name /dev/sdb of 50GiB is added.

Step 2: Create one Primary partition of 30GiB

In this step, we will create one primary partition of 30GiB with the help of fdisk command.

fdisk /dev/sdb

Image for post

Image for post

Now we can check the partition is a crate or not.

Image for post

Here we can see that one partition of size /dev/sdb1 with the size of 30GiB.

Step 3: Format the partition and mount it with some directory

In this step, we will format the partition with the ext4 file system, and then we will mount with /data directory.

mkfs.ext4 /dev/sdb1

mount /dev/sdb1 /data

Image for post

We can verify that the partition is mounted with /data folder or not with df command.

df -h

Image for post

Step 4: Put some data in the directory

In this step, we will put some data in the directory so that we can check if the data get lost or not after resizing the partition.

Image for post

Step 5: Unmount the partition from the /data folder.

In this step, we will unmount the partition because we have to resize the partition size and the static partition doesn’t allow us to resize the partition on-line.

To unmount the partition we can use the umount command.

umount /dev/sdb1

Image for post

Here the partition /dev/sdb1 has been mounted from the /data directory.

Image for post

We can check that there is no data in the /data directory.

Step 6: Create the existing partition

In this step first, we will create the partition /dev/sdb1 so that we can change the size of the partition.

Image for post

Image for post

Step 7: Create that partition again with the changed size

As we have to resize the partition so in this step we will create the partition again but the starting sector will be the same as the previous partition.

In my case the previous partition was started from the 2048 sector so again I will create the partition from that sector only and this time I am going to increase the size from 30GiB to 40GiB.

Image for post

Image for post

We can check the partition is create or not by listing the partition command.

Image for post

We can clearly see that one partation /dev/sdb1 of size 40GiB is created.

Step 8: Verify partition consistency with the e2fsck command

In this step, we will verify the partition consistency by running the e2fsck command.

e2fsck -f /dev/sdb1

Image for post

Here it is showing that there is some mismatch in the file system configuration and current partition size. To fix this issue we have to use the resize2fs command.

resize2fs /dev/sdb1

Image for post

Now the file system block size is the same as for partition configuration. Let’s mount the resized volume and check if our data is still there or not.

Step 9: Mount the resize volume and check the data

Image for post

Here we have mounted the volume with the /data directory.

Image for post

We can clearly see that our data is still there in the directory.

Thank You !!
