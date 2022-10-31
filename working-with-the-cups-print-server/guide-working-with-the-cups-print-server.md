# Working with the CUPS Print Server

## Scenario
A Linux system administrator should have a basic understanding of the CUPS print server. Even though computers were supposed to usher in the "paperless society," printing is still an important function of many businesses for record-keeping and government compliance. In this hands-on lab, we will practice with a newly installed print server that will send jobs to PDF files. We will use the `lpd` (line print daemon) toolset provided by a CUPS installation.

## Objectives
Install a PDF printer.
Print a test page.
Modify the printer and work with the print queue.

## Additional Resources
You just started a new job where you will be managing a print server for a small company. This company uses a centralized print server that will send all jobs to PDF files that they can email to their various business contacts and accounting services. You will configure a PDF printer on this server and send test jobs through the print queue to practice with the line print daemon commands from a terminal.


=====Solution=====
# Working with the CUPS Print Server

## Introduction

A Linux system administrator should have a basic understanding of the CUPS print server. Even though computers were supposed to usher in the "paperless society," printing is still an important function of many businesses for record-keeping and government compliance. In this hands-on lab, we will practice with a newly installed print server that will send jobs to PDF files. We will use the  `lpd`  (line print daemon) toolset provided by a CUPS installation.

## Install a PDF Printer

1.  Open your terminal application.
2.  Check to see which printers are installed.

`lpstat -s`

1.  Check to see what types of printer connections are available.

`sudo lpinfo -v`

1.  Install a PDF printer to use with CUPS.

`sudo lpadmin -p CUPS-PDF -v cups-pdf:/`

1.  Determine which driver files we can use with our printer by querying the CUPS database for files that contain "PDF".

`lpinfo --make-and-model "PDF" -m`

1.  Use  `CUPS-PDF.ppd`  as the driver file.

`sudo lpadmin -p CUPS-PDF -m "CUPS-PDF.ppd"`

1.  Run the  `lpstat`  command again.

`lpstat -s`

1.  Check the status of the printer we just installed.

`lpc status`

1.  Enable the printer to accept jobs, and set it up as the default printer.

`sudo lpadmin -d CUPS-PDF -E sudo cupsenable CUPS-PDF sudo cupsaccept CUPS-PDF`

1.  Run the  `lpc status`  command again.

`lpc status`

1.  The printer should now be ready.

## Print a Test Page

1.  Print a copy of the  `/etc/passwd`  file to a PDF file in our home directory.

`lpr /etc/passwd`

1.  Verify that there is a copy of the  `/etc/passwd`  file in the home directory.

`ls`

## Modify the Printer and Work with the Print Queue

1.  Configure the printer so that it will not accept any new jobs.

`sudo cupsreject CUPS-PDF`

1.  Verify the status of the printer.

`lpc status`

1.  Attempt to print the  `/etc/group`  file to the printer.

`lpr /etc/group`

1.  You should receive a message that says the printer is not currently accepting jobs.
2.  Reconfigure the printer to once again accept incoming jobs.

`sudo cupsaccept CUPS-PDF`

1.  Check the status of the printer.

`lpc status`

1.  Configure the printer so that it accepts jobs to its queue but will not print them.

`sudo cupsdisable CUPS-PDF`

1.  Check the status of the printer.

`lpc status`

1.  Attempt to print the  `/etc/group`  file again.

`lpr /etc/group`

1.  List the contents of the  `/home`  directory.

`ls`

1.  Check the printer's queue.

`lpq`

1.  Remove the job from the printer's queue (remember to substitute the job ID from your command's output).

`lprm <JOB_ID>`

1.  Verify that the job was successfully removed from the printer's queue.

`lpq`

1.  Re-enable the printer's ability to print new jobs.

`sudo cupsenable CUPS-PDF`

1.  Verify that the CUPS-PDF printer is once again ready to accept new jobs.

`lpq`

## Conclusion

Congratulations, you've successfully completed this hands-on lab!
