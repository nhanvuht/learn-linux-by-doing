
# Scheduling a Systemd Service Job With Timer Units

During the time that our development team has spent working on the new Web-based API for our organization, there have been several instances of mistaken keystrokes or processes that have necessitated the restoration of the site directory from backup.

We have been asked to run periodic backups of the website directory and, given that the development environment does not have access to the backup network, we have decided to write a custom service that will do so.

Previously we wrote systemd unit files to back up the site and have been provided a file called  _web-backup.sh_  in our  _/root_  directory. Using that file and the associated  _web-backup.service_, we will create a systemd timer unit file that will control the schedule of our service.

After we have all three components ready, we'll stage the files in their appropriate locations and start the service for our team and turn it back over for their use.

## Objectives

### Create a Service Timer Unit File
Follow the scenario to create the appropriate timer unit file.

### Putting Files Where They Belong
Copy the service and timer files and the shell script into the correct locations.

### Run the Custom Service
Once the backup service has been created successfully from the scenario, make sure it is running so the backup will happen as scheduled.

## Before We Begin

We need to be the root user to complete our goals. Sign into root using the  `sudo`  command:

`[user@$host ~]$ sudo su -`

When prompted, enter the provided lab credentials to finish logging in.

## Orientation

Part of this job is already done. In a previous lab, we wrote the systemd unit file,  _web-backup.service_  in the  _/root_  directory, which we will use alongside the  _web-backup.sh_  file that the Dev team gave us. To use it, we need to make sure we are in  _/root_  and that the file is there.

First, check where we currently are in the filesystem using  `pwd`:

`[root@$host ~]# pwd /root`

We are in  _/root_. Good, now use  `ls`  to list out our resources and make sure everything we need is there:

`[root@$host ~]# ls web-backup.sh web-backup.service`

## Create a Timer Unit File

With our items sourced, we are ready to create the timer unit file. To do so, use the  `vi`  command along with  `web-backup.timer`:

`[root@$host ~]# vi web-backup.timer`

Fill out the information as follows:

`[Unit] Description=Fire off the backup [Timer] OnCalendar=*-*-* 23:00:00 Persistent=true Unit=web-backup.service [Install] WantedBy=multi-user.target`

Note that 23:00:00 can be set to anything. We're just picking 11:00 PM here as an example.

When the file is correct, remember to write and quit properly from  `vi`  using the  `Esc`  key,  `:`  (the colon), then  `w`, then  `q`.

## Putting Files Where They Belong

With everything ready, we now need to make sure our files are in the correct locations. The shell script needs to be copied into  `/usr/local/sbin`  with the  `cp`  command:

`[root@$host ~]# cp web-backup.sh /usr/local/sbin/`

Then, using the  `cp`  command again, copy both the service and timer files into  `/etc/systemd/`:

`[root@$host ~]# cp web-backup.{service,timer} /etc/systemd/system/`

## Tell  `systemd`  to Run The Files

With our files in place, we need to reload the systemd daemon so that it can calculate the service dependencies:

`[root@$host ~]# systemctl daemon-reload`

Now enable the services to run at boot:

`[root@$host ~]# systemctl enable web-backup.service [root@$host ~]# systemctl enable web-backup.timer`

Set the permissions for the file to be executable.

`[root@$host ~]# chmod +x /usr/local/sbin/web-backup.sh`

Once the symlinks are created, go ahead and start the services manually:

`[root@$host ~]# systemctl start web-backup.timer web-backup.service`

Then check on the statuses of both the timer and the service:

`[root@$host ~]# systemctl status web-backup.timer [root@$host ~]# systemctl status web-backup.service`

They both show as running, meaning this server is ready to go back to the Dev team.

## Conclusion

In a previous scenario, we prepared a custom service that would run a backup script. Here, we actually put the service to use. It will start the process of backing the Dev team's site up at the specified time, just like they wanted. Congratulations! This will really make life easier for the Dev team moving forward.
