
# Working with System Service Log Files Using the Journal Control

## Introduction

Troubleshooting is an important part of working with services through systemd. In this hands-on lab, we will learn how to view system service log files using the Journal Control utility. At the end of this hands-on lab, you will know how to use the built-in  `journalctl`  utility to view and troubleshoot system services.

## Objectives

### Check the Web Server Configuration File

The Apache website's default configuration file is missing. Once this task is completed, the service will start as expected.

### Verify That the Web Server Service Is Running

Once the configuration issue is resolved, make sure the appropriate service is running.

## Connecting to the Lab

1.  Open your terminal application, and run the following command. (Remember to replace  `<PUBLIC_IP>`  with the public IP you were provided on the lab instructions page.)

`ssh cloud_user@&lt;PUBLIC_IP&gt;`

1.  Enter your password at the prompt.

## Check the Web Server Configuration File

1.  Change to the root account.

`sudo su -`

1.  Check the status of the web service.

`systemctl status httpd.service`

1.  Attempt to start the web service.

`systemctl start httpd.service`

1.  After the service fails to start, check the journal.

`journalctl -u httpd.service`

1.  Check the directory where the httpd configuration file should be.

`ls /etc/httpd/conf`

1.  Restore the original httpd configuration file.

`mv /etc/httpd/conf/httpd.conf.bkup /etc/httpd/conf/httpd.conf`

1.  Restart the service.

`systemctl restart httpd.service`

## Verify That the Web Server Service Is Running

1.  Check the status of the service.

`systemctl status httpd.service`

1.  Navigate to the local web page.

`elinks http://localhost`

## Conclusion

Congratulations, you've successfully completed this hands-on lab!
