
# Create New sudo Users

## Introduction

In this hands-on lab, we'll create new users that will be granted varying degrees of  `sudo`  access.

## Objectives

### Create two new users.

1.  Create two new users on the system, and assign the  `avance`  user to the  `wheel`  supplemental group:

`sudo useradd -m gfreeman sudo useradd -G wheel -m avance`

1.  Set the password for both accounts to  `LASudo321`:

`sudo passwd gfreeman sudo passwd avance`

### Verify the `/etc/sudoers` file and test access.

1.  Using the  `visudo`  command, verify that the  `/etc/sudoers`  file will allow the  `wheel`  group access to run all commands with  `sudo`. There should not be a comment (`#`) on this line of the file:

`%wheel ALL=(ALL) ALL`

1.  From the  `cloud_user`  login, use the  `su`  (substitute user) command to switch to the  `avance`  account, and use the dash (`-`) to utilize a login shell:

`sudo su - avance`

1.  As the  `avance`  user, attempt to read the  `/etc/shadow`  file at the console:

`cat /etc/shadow`

1.  As a regular user,  `avance`  does not have sufficient privileges to do so. Rerun the command with the  `sudo`  command:

`sudo cat /etc/shadow`

1.  After you have verified that  `avance`  can read the  `/etc/shadow`  file, log out of that account:

`exit`

### Set up the web administrator.

Now we need to configure  `gfreeman`'s account to have the ability to restart or reload the web server when needed. Since he will be the webmaster, he needs  `sudo`  permissions to restart the service.

1.  First, create a new  `sudoers`  file in the  `/etc/sudoers.d`  directory that will contain a standalone entry for webmasters. Use the  `-f`  option with the  `visudo`  command to create this new file:

`sudo visudo -f /etc/sudoers.d/web_admin`

1.  Enter in the following at the top of the file. This will create an alias command group that we can apply to any user or group that we add to this file. This group of commands will contain the necessary commands for restarting or reloading the web server:

`Cmnd_Alias WEB = /bin/systemctl restart httpd.service, /bin/systemctl reload httpd.service`

1.  Add another line in the file for  `gfreeman`  to be able to use the  `sudo`  command in conjunction with any commands listed in the WEB alias:

`gfreeman ALL=WEB`

1.  Save and close the file.
    
2.  Next, log into the  `gfreeman`  account:
    

`sudo su - gfreeman`

1.  Attempt to restart the web service:

`sudo systemctl restart httpd.service`

1.  Now  `gfreeman`  can restart the web server. As the  `gfreeman`  user, try to read the new  `web_admin sudoers`  file with the  `sudo`  command:

`sudo cat /etc/sudoers.d/web_admin`

Since the  `cat`  command is not listed in the command alias group for WEB,  `gfreeman`  cannot use  `sudo`  to read this file.

## Solution

Open a terminal session, and log in via SSH using the credentials provided on the lab page.

### Create Two New Users

1.  Create a  `gfreeman`  user on the system:
    
    `sudo useradd -m gfreeman`
    
2.  Create an  `avance`  user, and assign it to the  `wheel`  supplemental group:
    
    `sudo useradd -G wheel -m avance`
    
3.  Set the password for both accounts to  `LASudo321`:
    
    `sudo passwd gfreeman sudo passwd avance`
    

### Verify the  `/etc/sudoers`  File and Test Access

1.  Verify that the  `/etc/sudoers`  file will allow the  `wheel`  group access to run all commands with  `sudo`:
    
    `sudo visudo`
    
2.  Note that there should not be a comment (`#`) on this line of the file:
    
    `%wheel ALL=(ALL) ALL`
    
3.  Switch to the  `avance`  account, and use the dash (`-`) to utilize a login shell:
    
    `sudo su - avance`
    
4.  Attempt to read the  `/etc/shadow`  file at the console:
    
    `cat /etc/shadow`
    
5.  Rerun the command with the  `sudo`  command:
    
    `sudo cat /etc/shadow`
    
6.  After you have verified  `avance`  can read the  `/etc/shadow`  file, log out of that account:
    
    `exit`
    

### Set Up the Web Administrator

1.  Create a new  `sudoers`  file in the  `/etc/sudoers.d`  directory that will contain a standalone entry for webmasters:
    
    `sudo visudo -f /etc/sudoers.d/web_admin`
    
2.  Enter in the following at the top of the file:
    
    `Cmnd_Alias WEB = /bin/systemctl restart httpd.service, /bin/systemctl reload httpd.service`
    
3.  Add another line in the file for  `gfreeman`  to be able to use the  `sudo`  command in conjunction with any commands listed in the  `WEB`  alias:
    
    `gfreeman ALL=WEB`
    
4.  Save and close the file with  `:wq!`.
    
5.  Next, log in to the  `gfreeman`  account:
    
    `sudo su - gfreeman`
    
6.  Attempt to restart the web service:
    
    `sudo systemctl restart httpd.service`
    
7.  Try to read the new  `web_admin sudoers`  file:
    
    `sudo cat /etc/sudoers.d/web_admin`
    
    Since the  `cat`  command is not listed in the command alias group for  `WEB`,  `gfreeman`  cannot use  `sudo`  to read this file.
    

## Conclusion

Congratulations on completing this hands-on lab!
