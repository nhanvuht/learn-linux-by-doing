
# Working with Links in Linux

## Introduction

Understanding how soft and hard links work within Linux is an important skill for a system administrator. A review of the  `ln`  man page might be in order before embarking on this hands-on lab to know how to make a symbolic and hard link for files.

## Additional Resources

Make sure to review the man page for the  `ln`  command to know how to make a symbolic and hard link for files.

You have been asked by your development team to help them structure their filesystem with links to various files. They would like the following items created on the system for their use:

-   Create a symbolic link,  `/etc/redhat-release`, to a new link file in the  `cloud_user`'s home directory called  `release`.
-   View the inodes to verify each file was created correctly.
-   Create a directory called  `docs`  in the  `cloud_user`'s home directory and copy the  `/etc/services`  files here.
-   Link this new  `docs/services`  file to a file called  `services`  in the  `cloud_user`'s home directory.
-   Display the inodes to verify they are the same.
-   Attempt to create a hard link from  `docs/services`  to  `/opt/services`  and note whether the link recognizes each location is on a different filesystem.
-   Create a symbolic link from  `/etc/redhat-release`  to  `/opt/release`  and view the inodes to see if symbolic links can be created across those same filesystems.

## Objectives


### Create a Symbolic (soft) Link

Using the  `ln`  command, create a symbolic link from the file  `/etc/redhat-release`  to a new link file named  `release`  in the  `cloud_user`'s home directory. Using the  `ls`  command, verify that the link is valid. Use the  `cat`  command on the  `/home/cloud_user/release`  file to verify its contents.

Can be completed with:

`ln -s /etc/redhat-release release`

`ls -l`

`cat /etc/redhat-release`

### Check the Inode Numbers for the Link

Using the  `ls`  command, first look at the inode number for the  `/home/cloud_user/release`  link and then check the inode number for  `/etc/redhat-release`. They should be different, as the symbolic link is just a new file system entry that references the original file.

Viewing the inodes can be done via:

`ls -i release`

`ls -i /etc/redhat-release`

### Create a Hard Link

Create a directory called  `docs`  in your home directory. Copy the  `/etc/services`  file into this new  `docs`  directory. Using the  `ln`  command again, create a hard link from  `/home/cloud_user/docs/services`  to a link file named  `/home/cloud_user/services`. Use the  `ls`  command to verify the link's inode number, and the inode number for the original  `/etc/services`  file.

The commands to accomplish this task are:

`mkdir docs`

`cp /etc/services docs/`

`ln docs/services services`

`ls -l`

`ls -i services`

`ls -i docs/services`

### Attempt to Create a Hard Link Across File Systems

Using the  `ln`  command, attempt to make a hard link from  `/home/cloud_user/docs/services`  to  `/opt/services`  (you will have write permissions to this location). Why does this not work?

To see the behavior of this task, try the following:

`lsblk`

`ln docs/services /opt/services`

Attempt to Create a Symbolic Link Across File Systems

Once more using the  `ln`  command, attempt to create a soft link from  `/etc/redhat-release`  to  `/opt/release`. Why does this work, but creating a hard link fails? Turn the system over for grading when complete.

### Creating the soft link should succeed, even across filesystems, like so:

`sudo ln -s /etc/redhat-release /opt/release`

`ls -i /etc/redhat-release`

`ls -i /opt/release`


## Solution

Log in to the lab server using the credentials provided:

`ssh cloud_user@<PUBLIC_IP_ADDRESS>`

### Create a Symbolic (Soft) Link

1.  Create a symbolic (or soft) link from the  `/etc/redhat-release`  file to a new link file named  `release`  in the  `cloud_user`'s home directory:
    
    `ln -s /etc/redhat-release release`
    
2.  Verify the link is valid :
    
    `ls -l`
    
3.  See if you can read the file's contents:
    
    `cat release`
    
4.  See if you can read the link's contents:
    
    `cat /etc/redhat-release`
    
    They should be the same.
    

#### Check the Inode Numbers for the Link

1.  Look at the inode number of  `/home/cloud_user/release`:
    
    `ls -i release`
    
2.  Check the inode number for  `/etc/redhat-release`:
    
    `ls -i /etc/redhat-release`
    
    They should be different, as the symbolic link is just a new filesystem entry that references the original file.
    

### Create a Hard Link

1.  Create a directory called  `docs`  :
    
    `mkdir docs`
    
2.  Copy  `/etc/services`  into the  `docs`  directory:
    
    `cp /etc/services docs/`
    
3.  Create a hard link from the  `/home/cloud_user/docs/services`  file to a new link location named  `/home/cloud_user/services`:
    
    `ln docs/services services`
    
4.  Verify the link's inode number as well as the inode number for the original  `/etc/services`:
    
    `ls -l`
    
    This should verify for us that this is a hard link, not a soft link. It won't have an arrow pointing to the actual file it's linked to, like a soft link does. Just to verify, check these two with  `cat`  and make sure they're the same:
    
5.  View the contents of the inodes:
    
    `ls -i services`
    
    `ls -i docs/services`
    
    You should see they the same inode number, meaning they're essentially the same file.
    

### Attempt to Create a Hard Link Across Filesystems

1.  View the individual block devices:
    
    `lsblk`
    
    You should see something similar to the following:
    
    `NAME MAJ:MIN RM SIZE RO TYPE MOUNTPOINT xvda 202:0 0 10G 0 disk ├─xvda1 202:1 0 1M 0 part └─xvda2 202:2 0 10G 0 part / xvdb 202:16 0 2G 0 disk └─xvdb1 202:17 0 2G 0 part /opt`
    
    You can see here  `/`  and  `/opt`  are on 2 separate partitions. Because each partition has its own set of inodes, hard links across partitions don't work. Soft links should, though.
    
2.  Try to make a hard link from  `/home/cloud_user/docs/services`  to  `/opt/services`:
    
    `ln /home/cloud_user/docs/services /opt/services`
    
    You should get a  `failed to create hard link`  error .
    

### Attempt to Create a Soft Link Across Filesystems

1.  Try to make the same sort of cross-partition link, using the  `-s`  flag to make it a soft link:
    
    `sudo ln -s /etc/redhat-release /opt/release`
    
    There shouldn't be any output, meaning it was successful.
    
2.  View the contents of the inodes again:
    
3.  View the inode numbers of  `/etc/redhat-release`  and  `/opt/release`:
    
    `ls -i /etc/redhat-release`
    
    `ls -i /opt/release`
    
    You should see they have different inodes, but the linking will work.
    

## Conclusion

Congratulations on successfully completing this hands-on lab!
