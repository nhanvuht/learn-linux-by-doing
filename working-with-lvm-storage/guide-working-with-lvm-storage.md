# Working with LVM Storage

## Scenario
We've been tasked with creating a large logical volume out of the two disks attached to this server. The volume group name should be  `RHCSA`. The Logical Volume name should be  `pinehead`  and should be 3 GB in size.

Make sure that the resulting logical volume is formatted as XFS, and persistently mounted at  `/mnt/lvol`.

After that is complete, we should grow the logical volume and the filesystem by 200 MB.

## Introduction

In this lab we’re going to go over LVM managent tool. These are skills that will serve you well in your career as a Linux sysadmin. Once complete, you’ll have a solid understanding of how to use these tools.

## Objectives
Create Physical Devices

Create a Volume Group

Create a Logical Volume

Format the LV as XFS and Mount It Persistently at `/mnt/lvol`

Grow the Mount Point by 200 MB

## Additional Resources

Use the credentials and server IP to log in to our lab server. Run  `sudo -i`  to become  `root`  once you've logged in.

We've been tasked with creating a large logical volume out of the two disks attached to this server. The Volume Group name should be  `RHCSA`. The Logical Volume name should be  `pinehead`  and should be 3 GB in size.

Make sure that the resulting logical volume is formatted as XFS and persistently mounted at  `/mnt/lvol`.

After that is complete, we should grow the logical volume and the filesystem by 200 MB.

## Solution
### Get Logged in

Use the credentials and server IP in the hands-on lab overview page to log in to our lab server. Once we're in, we can get moving. Since we'll need to be  `root`  for the all of the commands, we'll run a quick  `sudo -i`  as soon as we're in. Once that's done, we can get moving.

### Create a Physical Device

To see the names of our disks, we need to run  `fdisk -l`. Then we run  `pvcreate /dev/xvdg /dev/xvdf`  to create the physical devices. To check how it went, we can do a quick  `pvs`  or  `pvdisplay`, and we'll see that they've been created.

### Create a Volume Group

All we need to do is run  `vgcreate RHCSA /dev/xvdg /dev/xvdf`.  `RHCSA`  is going to be the name of our volume group, and those physical devices we created in the last step is where this volume group will go.

### Create a Logical Volume

Now we can create the our logical volume using the  `lvcreate`  command:

`[root@host]# lvcreate -n pinehead -L 3G RHCSA`

-   `-n`  denotes the name of the LV
-   `-L`  denotes the size of the LV
-   `RHCSA`  is the name of the Volume Group we're creating this LV in

### Format the LV as XFS and Mount It Persistently at  `/mnt/lvol`

Now we can format the disk like any other device. To format it as XFS, we'll run:

`[root@host]# mkfs.xfs /dev/mapper/RHCSA-pinehead`

We've got to create a mount point:

`mkdir /mnt/lvol`

Before we can get it mounting persistently (after reboots), we need the UUID. Run  `blkid`  to get it, then copy it. We'll need it in a second.

Edit  `/etc/fstab`  (with whichever text editor you prefer) and create a new line that looks like this:

`UUID="&ltTHE_UUID_WE_COPIED>" /mnt/lvol xfs defaults 0 0`

Now, to mount everything listed in  `fstab`  (including this new mount we just created), let's run  `mount -a`.

### Grow the Mount Point by 200 MB

To grow an LV, we can run:

`[root@host]# lvextend -L+200M /dev/RHCSA/pinehead`

We can let the LVM tools automatically resize the filesystem as well by passing the  `-r`  or  `--resizefs`  flags.

Optionally, we could have run a  `growfs`  command to resize the filesystem:

`[root@host]# xfs_growfs /mnt/lvol`

## Conclusion

We did it. We created a logical volume, got it to mount persistently, and  _then_  made it a little bigger. These are exactly the things we set out to do. Congratulations!
