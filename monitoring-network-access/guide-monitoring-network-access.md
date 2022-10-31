# Monitoring Network Access

## Scenario
During the development of a new Web-based API our team is working on, they have discovered that they are receiving intermittent network disconnects from clients, even when they are local to the network of the server itself. We have been provided credentials and access information for two CentOS 7 systems in their environment. They have asked for us to install tools that they can use to monitor network traffic between the two system



## Objectives

Install Client Utilities

Create the Traffic Log File

## Additional Resources
During the development of a new Web-based API our team is working on, they have discovered that they are receiving intermittent network disconnects from clients, even when they are local to the network of the server itself.

We have been provided credentials and access information for two CentOS 7 systems in their environment. They have asked for us to install tools that they can use to monitor network traffic between the two systems.

We'll have to install the tools we need and create traffic on port  **2525**  from  `server2`  to  `server1`. We want to get  _all_  network traffic sent to  `/home/cloud_user/traffic_log.txt`

## Introduction
Understanding networking concepts is a more advanced concept for most system administrators, but it is essential to being successful. In this activity, the we will use the netcat (`nc`) utility to generate network traffic between two servers and view that traffic's appearance in a tool called `iptraf-ng`.


## Solution
### Logging In

Use the credentials in the hands-on lab overview page to log into the provided servers. It will be easier to have a terminal or two open for each server at the same time. We're going to be  `root`  right off, so as soon as we get logged in we'll want to run a quick  `sudo su`  in each one.

### Install Client Utilities

We've got to install the two packages that the team will use to generate and monitor traffic. Let's use YUM to get it done:

`[root@server1]# yum install iptraf-ng nc`

Repeat this on the other server:

`[root@server2]# yum install iptraf-ng nc`

### Create the Traffic Log File

On the first server, let's run  `iptraf-ng`  and go under  `Configure...`  In the menu, don't forget this isn't a menu we control with a mouse -- it's all keyboard. Make sure  `Logging`  is toggled to  `On`. Set the log file path to:  `/home/cloud_user/traffic_log.txt`. Then go into  **IP traffic monitor**. In the next menu, select  **eth0**. Once we press  **Enter**  the logging will start.

#### Listen for Traffic

Let's open a second terminal into  `server1`  and run  `sudo su`  right off. Once we're there, we're going to start netcat listening on post  **2525**  with this:

`[root@server1]# nc -l 2525`

#### Send Some Traffic

Now, let's start talking. Back in the  `server2`  window we've got open, send netcat traffic to  `server1`  with this (where  `x.x.x.x`  is the internal IP of  `server1`  that we'll see on the hands-on lab overview page):

`[root@server2]# nc x.x.x.x 2525`

We'll just land at a blinking cursor below the prompt, but we can type a message there and press  **Enter**. Once we do, it will show up back in the window we're listening in on  `server1`. A bunch of messages sent from  `server2`  would look like this:

`[root@server2]# nc x.x.x.x 2525 test test testing This is a test`

On  `server1`, they would look like this when they arrive:

`[root@server1]# nc -l 2525 test test testing This is a test`

That should be enough traffic for what we're doing. On  `server2`, press  **Ctrl + C**  to kill the  `nc`  command we've got running and flip back over to the terminal we were running  `iptraf-ng`  in. Press  **x**  to stop the monitoring and get out, then choose  **Exit**  from the main menu.

#### Examine the Log

On  `server1`, if we run  `ls /home/cloud_user`  we should see  `traffic_log.txt`  listed in the output. Read that to see if it was capturing what we need:

`[root@server1]# less /home/cloud_user/traffic_log.txt`

We should see some log entries showing traffic going from  `server2`  to  `server1`  on port  **2525**.

## Conclusion

We did it. We've got all of the tools in place. There's a tool listening for traffic, and one logging it. We've done our job, and our development team can take things from here. Congratulations!
