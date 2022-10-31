
# Using SSH, Redirection, and Permissions in Linux

In this lab, we'll go over I/O redirection, file permissions, and using the  `ssh`  tool. These are skills that will serve you well in your career as a Linux sysadmin. Once complete, you’ll have a solid understanding of how to use these tools.


## Objectives


### Enable SSH to Connect Without a Password from the `dev` User on `server1` to the `dev` User on `server2`

We need to use SSH keys to satisfy this requirement, so generate them with this:

`[dev@server1]$ ssh-keygen`

Then run:

`[dev@server1]$ ssh-copy-id <server2 IP>`

### Copy All tar Files from `/home/dev/` on `server1` to `/home/dev/` on `server2`, Extract Them, and Redirect Output to `/home/dev/tar-output.log`

We need to use a method of copying files over a network.  `scp`  is the best tool, like this:

`[dev@server1]$ scp *.gz <server2 IP>:~/`

Then connect to  `server2`  using  `ssh`:

`[dev@server1]$ ssh <server2_IP>`

Then we can extract the files:

`[dev@server2]$ tar -xvf deploy_content.tar.gz >> tar-output.log`

`[dev@server2]$ tar -xvf deploy_script.tar.gz >> tar-output.log`

Make sure to use  `>>`, so that the output is appended rather than overwritten.

### Set the Umask So That New Files Are Only Readable and Writeable by the Owner

The task is asking to make new files with the following permission:  `0600`.

So we can do subtraction to figure out what our umask should be.

`0666`  <-- Default

`0600`  <-- Desired

`----`

`0066`  <-- What we need to set

So we run:

`[dev@server2]$ umask 0066`

### Verify the `/home/dev/deploy.sh` Script Is Executable and Run It

First, we check permissions on  `deploy.sh`:

`[dev@server2]$ ls -l deploy.sh`

There's no execute bit. Let's add one:

`[dev@server2]$ chmod +x deploy.sh`

And then run it:

`[dev@server2]$ ./deploy.sh`

## Additional Resources

We need to set up a new server for a developer to use. He needs to be able to connect with  `ssh`  from  `server1`  to  `server2`  as the  `dev`  user, without having to enter a password password.

Once that's set up there are some tar files on  `server1`  that need to be copied over and extracted. To enable the developer to verify that it was done correctly, we should have all the output from the extraction go to  `/home/dev/tar-output.log`.

We need to make sure that new files have the correct permissions (readable and writeable by only the user) by setting the umask correctly.

Once complete we should verify permissions on the very important  `/home/dev/deploy.sh`  script and run it.

Log in to one of the servers (which will then be referred to as  `server1`  throughout the rest of the lab) using the credentials provided:

`ssh dev@<server1_PUBLIC_IP>`

The password for the  `dev`  user is the same as for  `cloud_user`.

## Solution

Please wait an extra minute before loogging into the instances to make sure they are finished being set up. Then log in to one of the servers (which will then be referred to as  `server1`  throughout the rest of the lab guide) using the credentials provided:

`ssh dev@<server1_PUBLIC_IP>`

The password for  `dev`  is the same as the one for  `cloud_user`.

### Enable SSH to Connect Without a Password from the  `dev`  User on  `server1`  to the  `dev`  User on  `server2`

1.  Generate an SSH key:
    
    `[dev@server1]$ ssh-keygen`
    
2.  Press  **Enter**  three times to accept the defaults.
    
3.  Then copy it over to the  _private_  IP of the other server:
    
    `[dev@server1]$ ssh-copy-id <server2_PRIVATE_IP>`
    
4.  Now if we try to log into  `server2`  without a password, it should work. Try it:
    
    `[dev@server1]$ ssh <server2_PRIVATE_IP>`
    
5.  Log out to get back to  `server1`:
    
    `[dev@server2]$ logout`
    

### Copy All  `tar`  Files from  `/home/dev/`  on  `server1`  to  `/home/dev/`  on  `server2`

1.  Copy the files:
    
    `[dev@server1]$ scp *.gz <server2_PRIVATE_IP>:~/`
    
2.  Connect to  `server2`  again:
    
    `[dev@server1]$ ssh <server2_PRIVATE_IP>`
    
3.  Make sure they're there:
    
    `[dev@server2]$ ll`
    
    It should show the two files.
    

### Extract the Files, Making Sure the Output is Redirected

1.  Extract the files:
    
    `[dev@server2]$ tar -xvf deploy_content.tar.gz >> tar-output.log`
    
    `[dev@server2]$ tar -xvf deploy_script.tar.gz >> tar-output.log`
    
2.  Take a look at what's in the directory now:
    
    `ll`
    
    We'll see the new files and their permissions.
    

### Set the Umask So New Files Are Only Readable and Writeable by the Owner

1.  We need to make new files with  `0600`  (`-rw-------`) permissions. Since the default is  `0666`, and we want it to be  `0600`, run the following:
    
    `[dev@server2]$ umask 0066`
    

### Verify the  `/home/dev/deploy.sh`  Script Is Executable and Run It

1.  Check permissions on  `deploy.sh`:
    
    `[dev@server2]$ ls -l deploy.sh`
    
2.  Make the script executable:
    
    `[dev@server2]$ chmod +x deploy.sh`
    
3.  Run it:
    
    `[dev@server2]$ ./deploy.sh`
    

## Conclusion

Congratulations on successfully completing this hands-on lab!
