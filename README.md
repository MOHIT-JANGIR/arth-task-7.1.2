
# Increase or Decrease the Size of Static Partition in Linux

![image](https://user-images.githubusercontent.com/61896468/98809641-df23b480-2443-11eb-965b-a561f4f346f2.png)

## In this blog, I am going to discuss how to resize the static partition in Linux with the help of the resize2fs command. The basic prerequisite for this task is Linux partition.

# Linux Partition:

## A hard disk can be divided into several partitions. Each partition functions as if it were a separate hard disk. There are several reasons why we create the partition:

### multiple operating systems on the same disk.

### different file systems on different partitions.

### more efficient disk space management.

### different security settings on different partitions.

### easier backup procedure.

# Task Description:

## In this task, we have to increase or decrease the size of static partition Linux. In Linux, the primary partition that we crease don’t allow to increase or decrease the partition size if we do we have to change the format it again but the issues are that if we format the partition again then we will not be able to access the data that we had stored. So we have to find some way through which we can increase or decrease the size of the static partition by formatting it again.

# Step 1: Add one Hard Disk to the VM

## In the first step add one hard disk to the VM, we can see the hard disk with the fdisk command.

# fdisk -l

![Screenshot 2020-11-11 16 37 27](https://user-images.githubusercontent.com/61896468/98809743-1a25e800-2444-11eb-965b-57bbed11f348.png)

## Here we can see that one new hard disk with the name /dev/xvdf of 5GiB is added.

# Step 2: Create one Primary partition of 2GiB

## In this step, we will create one primary partition of 2GiB with the help of fdisk command.

# fdisk /dev/xvdf

![Screenshot 2020-11-11 16 40 24](https://user-images.githubusercontent.com/61896468/98809745-1b571500-2444-11eb-8f94-5a66d4ca89ac.png)

## Now we can check the partition is a created or not.

![Screenshot 2020-11-11 16 40 58](https://user-images.githubusercontent.com/61896468/98809752-1c884200-2444-11eb-81d6-6ab3e0a23bf3.png)

## Here we can see that one partition of size /dev/xvdf1 with the size of 5GiB.

# Step 3: Format the partition and mount it with some directory

## In this step, we will format the partition with the ext4 file system, and then we will mount with /data directory.

# mkfs.ext4 /dev/xvdf1

# mount /dev/xvdf1 /data

![Screenshot 2020-11-11 16 43 35](https://user-images.githubusercontent.com/61896468/98809755-1db96f00-2444-11eb-959b-826064e809dc.png)

## We can verify that the partition is mounted with /data folder or not with df command.

# df -h

![Screenshot 2020-11-11 16 44 05](https://user-images.githubusercontent.com/61896468/98809757-1eea9c00-2444-11eb-91da-be9f5751e7b6.png)

# Step 4: Put some data in the directory

## In this step, we will put some data in the directory so that we can check if the data get lost or not after resizing the partition.
![Screenshot 2020-11-11 16 45 13](https://user-images.githubusercontent.com/61896468/98809762-201bc900-2444-11eb-951f-e00d8816a97b.png)

# Step 5: Unmount the partition from the /data folder.

## In this step, we will unmount the partition because we have to resize the partition size and the static partition doesn’t allow us to resize the partition on-line.

## To unmount the partition we can use the umount command.

# umount /dev/xvdf1

![Screenshot 2020-11-11 16 46 07](https://user-images.githubusercontent.com/61896468/98809765-214cf600-2444-11eb-9750-ade9784f4e58.png)

## Here the partition /dev/xvdf1 has been mounted from the /data directory.

![Screenshot 2020-11-11 16 46 24](https://user-images.githubusercontent.com/61896468/98809775-25791380-2444-11eb-994a-520f7a1d39d1.png)

## We can check that there is no data in the /data directory.

# Step 6: Create the existing partition

## We will first delete the partition having size 2 GIB

![Screenshot 2020-11-11 16 47 53](https://user-images.githubusercontent.com/61896468/98809779-26aa4080-2444-11eb-8430-871ac0e7a48b.png)


# Step 7: Create that partition again with the changed size
![Screenshot 2020-11-11 16 48 36](https://user-images.githubusercontent.com/61896468/98809790-2a3dc780-2444-11eb-8be9-0c6899ce5611.png)
## As we have to resize the partition so in this step we will create the partition again but the starting sector will be the same as the previous partition.

## In my case the previous partition was started from the 2048 sector so again I will create the partition from that sector only and this time I am going to increase the size from 2GiB to 4GiB.



## We can check the partition is created or not by listing the partition.

![Screenshot 2020-11-11 16 49 35](https://user-images.githubusercontent.com/61896468/98809791-2ad65e00-2444-11eb-8149-edbe8c23a319.png)

## We can clearly see that one partation /dev/xvdf1 of size 4GiB is created.

# Step 8: Verify partition consistency with the e2fsck command

## In this step, we will verify the partition consistency by running the e2fsck command.

# e2fsck -f /dev/xvdf1

![Screenshot 2020-11-11 16 50 05](https://user-images.githubusercontent.com/61896468/98809795-2c078b00-2444-11eb-81ff-c97aa64381cb.png)

# Here it is showing that there is some mismatch in the file system configuration and current partition size. To fix this issue we have to use the resize2fs command.

# resize2fs /dev/xvdf1

![Screenshot 2020-11-11 16 50 28](https://user-images.githubusercontent.com/61896468/98809802-2dd14e80-2444-11eb-8ff3-5404bc50bb98.png)

## Now the file system block size is the same as for partition configuration. Let’s mount the resized volume and check if our data is still there or not.

# Step 9: Mount the resize volume and check the data

![Screenshot 2020-11-11 16 51 04](https://user-images.githubusercontent.com/61896468/98809807-2f027b80-2444-11eb-970c-c073754ba239.png)

## Here we have mounted the volume with the /data directory.

![Screenshot 2020-11-11 16 51 35](https://user-images.githubusercontent.com/61896468/98809809-3033a880-2444-11eb-9602-6613b6727730.png)

## We can clearly see that our data is still there in the directory.

# Thank You !!
