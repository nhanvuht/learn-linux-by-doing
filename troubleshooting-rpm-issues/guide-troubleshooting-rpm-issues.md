
# Troubleshooting RPM Issues


## Introduction

In this exercise, you will need to install  `telnet`  and install Apache.
## Objectives

### Install telnet.

First, let's become  `root`:

`sudo -i`

Install the  `telnet`  package:

`yum install -y telnet`

Verify the integrity of the RPM database:

`cd /var/lib/rpm/`

`/usr/lib/rpm/rpmdb_verify Packages`

Move  `Packages`  to  `Packages.bad`  and create a new RPM database from  `Packages.bad`:

`mv Packages Packages.bad`

`/usr/lib/rpm/rpmdb_dump Packages.bad | /usr/lib/rpm/rpmdb_load Packages`

Verify the integrity of the new RPM database:

`/usr/lib/rpm/rpmdb_verify Packages`

Query installed packages for errors:

`rpm -qa > /dev/null`

Rebuild the RPM database:

`rpm -vv --rebuilddb`

Install  `telnet`:

`yum install -y telnet`

### Install Apache.

Install Apache:

`yum install -y httpd`

Edit  `/etc/yum.conf`  to remove the exclusion for  `httpd`:

`vim /etc/yum.conf`

Now, try to install Apache:

`yum install -y httpd`




## Solution

Start by logging in to the lab server using the credentials provided on the hands-on lab page:

`ssh cloud_user@PUBLIC_IP_ADDRESS`

Become the root user:

`sudo -i`

### Install  `telnet`

1.  Install the  `telnet`  package:
    
    `yum install -y telnet`
    
2.  Verify the integrity of the RPM database:
    
    `cd /var/lib/rpm/`
    
    `/usr/lib/rpm/rpmdb_verify Packages`
    
3.  Move  `Packages`  to  `Packages.bad`  and create a new RPM database from  `Packages.bad`:
    
    `mv Packages Packages.bad`
    
    `/usr/lib/rpm/rpmdb_dump Packages.bad | /usr/lib/rpm/rpmdb_load Packages`
    
4.  Verify the integrity of the new RPM database:
    
    `/usr/lib/rpm/rpmdb_verify Packages`
    
5.  Query installed packages for errors:
    
    `rpm -qa > /dev/null`
    
6.  Rebuild the RPM database:
    
    `rpm -vv --rebuilddb`
    
7.  Install  `telnet`:
    
    `yum install -y telnet`
    

### Update Apache

1.  Attempt to install Apache:
    
    `yum install -y httpd`
    
2.  Edit  `/etc/yum.conf`:
    
    `vim /etc/yum.conf`
    
3.  Remove the exclusion for  `httpd`:
    
    `exclude=httpd`
    
4.  Save and close the file:
    
    `:wq`
    
5.  Install Apache:
    
    `yum install -y httpd`
    

## Conclusion

Congratulations, you've completed this hands-on lab!
