# Storage Management

## Scenario
In this lab, we’re going to go over managing and formatting partitions. Having a solid understanding of how to use these tools is a fundamental component of a Linux sysadmin career.

## Objectives
Create a 2 GB GPT Partition
Create a 2 GB MBR Partition
Format the GPT Partition with XFS and Mount the Device persistently
Format the MBR Partition with ext4 and Mount the Device.


## Additional Resources

There are two disks advertised to this server. You've been tasked with setting one up with a  `GPT`  partition table and allocating 2GB to a single partition. The other needs to be a  `MBR`  partition with a 2GB partition.

**Note:**  The Block devices have changed for the lab environment. To see the available block devices to use, run:  `lsblk`  The commands in the lab instructions have been updated for the new change.

## Solution

Log in to the server using the credentials provided:

`ssh cloud_user@<PUBLIC_IP_ADDRESS>`

Then, become  `root`:

`sudo -i`

### Create a 2 GB GPT Partition on  `/dev/nvme1n1`

1.  Create the partition:
    
    `gdisk /dev/nvme1n1`
    
2.  Enter  `n`  to create a new partition.
    
3.  Accept the default for the partition number.
    
4.  Accept the default for the starting sector.
    
5.  For the ending sector, enter  `+2G`  to create a 2 GB partition.
    
6.  Accept the default partition type.
    
7.  Enter  `w`  to write the partition information.
    
8.  Enter  `y`  to proceed.
    
9.  Finalize the settings:
    
    `partprobe`
    

### Create a 2 GB MBR Partition on  `/dev/nvme2n1`

1.  Create the partition:
    
    `fdisk /dev/nvme2n1`
    
2.  Enter  `n`  to create a new partition.
    
3.  Accept the default partition type.
    
4.  Accept the default for the partition number.
    
5.  Accept the default for the starting sector.
    
6.  For the ending sector, type  `+2G`  to create a 2 GB partition.
    
7.  Enter  `w`  to write the partition information.
    
8.  Finalize the settings:
    
    `partprobe`
    

### Format the GPT Partition with XFS and Mount the Device on  `/mnt/gptxfs`  Persistently

1.  Format the partition:
    
    `mkfs.xfs /dev/nvme1n1p1`
    

#### Getting It Ready for Mounting

1.  Run the following:
    
    `blkid`
    
2.  Copy the UUID of the partition at  `/dev/nvme1n1p1`.
    
3.  Open the  `/etc/fstab`  file:
    
    `vim /etc/fstab`
    
4.  Add the following, replacing  `<UUID>`  with the UUID you just copied:
    
    `UUID="<UUID>" /mnt/gptxfs xfs defaults 0 0`
    
5.  Save and exit the file by pressing  **Escape**  followed by  `:wq`.
    

#### Create a Mount Point

1.  Create the mount point we specified in  `fstab`:
    
    `mkdir /mnt/gptxfs`
    
2.  Mount everything that's described in  `fstab`:
    
    `mount -a`
    
3.  Check that it's mounted:
    
    `mount`
    
    The partition should be listed in the output.
    

### Format the MBR Partition with ext4 and Mount the Device on  `/mnt/mbrext4`

1.  Format the partition:
    
    `mkfs.ext4 /dev/nvme2n1p1`
    

#### Create a Mount Point

1.  Create the mount point:
    
    `mkdir /mnt/mbrext4`
    
2.  Mount it:
    
    `mount /dev/nvme2n1p1 /mnt/mbrext4`
    
3.  Check that it's mounted:
    
    `mount`
    
    The partition should be listed in the output.
    

## Conclusion

We formatted a couple of partitions exactly as someone wanted them, created mount points for them, and set one up to mount at boot. Congratulations!
