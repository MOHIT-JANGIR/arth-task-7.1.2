

#  TASK : Increase or Decrease the Size of Static Partition in Linux.


# SOLUTION :
# 1. We add one Hard-disk of 8GB :-
![](https://miro.medium.com/max/875/1*KnVcKueTFA9ehUaBLDc2Mg.png)

# Run cmd "lsblk" to list all block devices.
# `2. We create a partition of 4GB :-`
# Now run cmd "fdisk /dev/sdb" to create partition of 4 GB.
![](https://miro.medium.com/max/875/1*rx113arRIuKwS-06zJWlFw.png)
# 3. Format and Mount :-
## To format we run cmd "mkfs.ext4 /dev/sdb1".
## `To mount run "mount /dev/sdb1 team/"`
![](https://miro.medium.com/max/875/1*dYqHLUwY8Rn9TtwY2BgHjQ.png)
# 4. Write some data :-
![](https://miro.medium.com/max/875/1*APc_h8CUJW3i0fT8D2i0mA.png)

# `5.Unmount partition :-`
##  cmd → umount /dev/sdb1
# 6. Run fsck on the partition to check consistency of partition or file system.
## *cmd → e2fsck -f /dev/sdb1*
![](https://miro.medium.com/max/875/1*z7I02ujpQF7ZyHLbTRtwrg.png)
# Here we start our practical to increase static partition size.
# 7. We delete and create new partition of 7GB :-

# They prompt as “Do you want to remove the signature? [Y]es/[N]o:”
# We give NO as a option otherwise we can lose our data
![](https://miro.medium.com/max/875/1*NtdsX02-h9S8vm79X6iQ_w.png)
# 8. let’s check size of partition :-
![](https://miro.medium.com/max/875/1*Rqg9tfUets-N2vlImMdQCA.png)

# congratulation we successfully increase size of partition from 4G to 7G
# 9. let’s check our data:-
## 1st we mount and see
![](https://miro.medium.com/max/875/1*Su9nT-OvC5v8o81RMEWvfg.png)
