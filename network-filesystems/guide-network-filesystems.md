# Monitoring Network Access

## Scenario
Implementing network fileshares, Linux servers, and clients is a key skill for any experienced system administrator. In this activity, we will be working to set up both a Linux Samba fileshare and an NFS fileshare that can then be used by a remote client to store files on. Once you complete this activity, you will understand how to configure network filesystems



## Objectives
Set Up a Samba Share

Set Up the NFS Share

## Additional Resources
We need to set two servers up so that they can share files over both NFS and SMB.

The shares need to be writable on both ends, and we can't use  `no_root_squash`  on the NFS server.

## Set Up the Samba Server

1.  Log in to the Samba server using the credentials provided:
    
    `ssh cloud_user@<SAMBA_SERVER_PUBLIC_IP_ADDRESS>`
    
2.  Become  `root`:
    
    `[cloud_user@samba-server]$ sudo -i`
    
3.  Create the  `/smb`  path:
    
    `[root@samba-server]# mkdir /smb`
    
4.  Make sure the client can write to the path:
    
    `[root@samba-server]# chmod 777 /smb`
    
5.  Install the Samba packages:
    
    `[root@samba-server]# yum install samba -y`
    
6.  Open  `/etc/samba/smb.conf`:
    
    `[root@samba-server]# vim /etc/samba/smb.conf`
    
7.  Add the following section at the bottom:
    
    `[share] browsable = yes path = /smb writable = yes`
    
8.  Save and exit the file by pressing  **Escape**  followed by  `:wq`.
    
9.  Check that our changes saved correctly:
    
    `[root@samba-server]# testparm`
    

### Samba Share User

1.  Create the user on the server:
    
    `[root@samba-server]# useradd shareuser`
    
2.  Give it a password:
    
    `[root@samba-server]# smbpasswd -a shareuser`
    
    Enter and confirm a password you'll easily remember (e.g.,  `123456`), as we'll need to reenter it later.
    

### Start It Up

1.  Start the Samba daemon:
    
    `[root@samba-server]# systemctl start smb`
    

## Set Up the Samba Client

1.  Open up a new terminal.
    
2.  Log in to the NFS server:
    
    `ssh cloud_user@<NFS_SERVER_PUBLIC_IP_ADDRESS>`
    
3.  Become  `root`:
    
    `[cloud_user@nfs-server]$ sudo -i`
    
4.  Install software:
    
    `[root@nfs-server]# yum install cifs-utils -y`
    

### Make a Mount Point

1.  Create a place for mounting the share:
    
    `[root@nfs-server]# mkdir /mnt/smb`
    

### The Mount

1.  In the Samba server terminal, get its IP address:
    
    `[root@samba-server]# ip a s`
    
2.  Copy the private  `inet`  address on  `eth0`, and paste it into a text file, as we'll need it next.
    
3.  In the NFS terminal, run the following command, replacing  `<SERVER_IP>`  with the IP you just copied and  `<SMBPASSWD_PASS>`  with the password you created earlier:
    
    `[root@nfs-server]# mount -t cifs //<SERVER_IP>/share /mnt/smb -o username=shareuser,password=<SMBPASSWD_PASS>`
    
4.  Make sure you see it listed when you run:
    
    `[root@nfs-server]# mount`
    
5.  Change directory:
    
    `[root@nfs-server]# cd /mnt/smb`
    
6.  Create a file:
    
    `[root@nfs-server smb]# touch file`
    
7.  List the contents:
    
    `[root@nfs-server smb]# ls`
    
    We should see the new file called  `file`.
    

## Set Up the NFS Share

1.  Install software:
    
    `[root@nfs-server smb]# yum install nfs-utils -y`
    
2.  Create the directory that will be shared out:
    
    `[root@nfs-server smb]# mkdir /nfs`
    
3.  Open  `/etc/exports`:
    
    `[root@nfs-server smb]# vim /etc/exports`
    
4.  Add the following line:
    
    `/nfs *(rw)`
    
5.  Save and exit the file by pressing  **Escape**  followed by  `:wq`.
    
6.  Edit permissions, to make sure it's going to be writable, on the shared directory:
    
    `[root@nfs-server smb]# chmod 777 /nfs`
    
7.  Implement what we've configured in  `/etc/exports`:
    
    `[root@nfs-server smb]# exportfs -a`
    
8.  Start the required services:
    
    `[root@nfs-server smb]# systemctl start {rpcbind,nfs-server,rpc-statd,nfs-idmapd}`
    
9.  Verify it:
    
    `[root@nfs-server smb]# showmount -e localhost`
    
10.  Run the following to get the NFS server's IP:
    
    `[root@nfs-server smb]# ip a s`
    
11.  Copy the  `inet`  address on  `eth0`  and paste it into a text file, as we'll need it shortly.
    

## Set Up the NFS Client

1.  In the Samba server terminal, install software:
    
    `[root@samba-server]# yum install nfs-utils -y`
    
2.  Create a mount point:
    
    `[root@samba-server]# mkdir /mnt/nfs`
    
3.  Check to see what's being shared out on the NFS server, replacing  `<NFS_SERVER_IP>`  with the IP you copied earlier:
    
    `[root@samba-server]# showmount -e <NFS_SERVER_IP>`
    
4.  To be able to mount NFS shares, we need start a daemon:
    
    `[root@samba-server]# systemctl start rpcbind`
    

## Mount the NFS Share

1.  Mount it, replacing  `<NFS_SERVER_IP>`  with the IP you copied earlier:
    
    `[root@samba-server]# mount -t nfs <NFS_SERVER_IP>:/nfs /mnt/nfs`
    
2.  Make sure you see it listed after running:
    
    `[root@samba-server]# mount`
    
3.  Change directory:
    
    `[root@samba-server]# cd /mnt/nfs`
    
4.  Create a file:
    
    `[root@samba-server nfs]# touch file`
    
5.  List the contents:
    
    `[root@samba-server nfs]# ls`
    
    We should see the new file, called  `file`.
    

## Conclusion

We did it. There are two servers set up that share files back and forth. One is using Samba to share, and the other is using NFS. Congratulations!

