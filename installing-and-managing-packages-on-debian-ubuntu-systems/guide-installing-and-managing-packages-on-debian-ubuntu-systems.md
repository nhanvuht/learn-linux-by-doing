
# Installing and Managing Packages on Debian/Ubuntu Systems

## Scenario

You have been provided the credentials and connection information for a new Ubuntu 16.04 LTS system that your development team will be using to do some basic web server testing as an alternative to the CentOS 7 systems they are developing their API on. They will be doing most of the configuration, however, they have asked you to provision the server to serve basic web pages. Fortunately, you know that Ubuntu starts services for you (when appropriate) when you install packages. You have been asked to install the Apache web server on the system you have been given access to using the default package management system. Before you turn the system over, make sure the 'wget' package is installed. Once it is installed, use it to download the default web page from the Apache server you just installed and redirect that output to a file called _'local_index.result'_ in your user's home directory. Once that is successfully captured, you can turn the system back over to your developers.

## Introduction

Installation and removal of packages is a core skill for anyone managing Linux distributions. During this activity, the student will work with the package manager and installation utility  `apt`  to manage packages on Ubuntu/Debian Linux distributions.

You've been provisioned with an Ubuntu 16.04 LTS server and will need to install the Apache web server and  `wget`  on it. Log in to the system using the credentials provided on the hands-on lab page.

## Objectives
### Install the Apache Web Server Package

You've been provisioned with an Ubuntu 16.04 LTS server and will need to install the Apache web server and Wget on it using the standard package manager:

`sudo apt install apache2 wget`

**Note:**  Ubuntu/Debian systems will usually start a service automatically, once its package is installed. You may need to update the package manager.

`sudo apt update`

### IVerify the Server is Running and Capture the Result

Using the  _wget_  package, capture the output of a request to the local Apache server's default site in a file in the home directory called  `local_index.response`.

You can verify the service is running with:

`sudo systemctl status apache2`

And capture the output via the command:

`wget --output-document=local_index.response http://localhost`

## Install the Apache Web Server Package

> **Note**: Ubuntu/Debian systems will usually start a service automatically, once its package is installed. You may need to update the package manager.

First, let's update our package information:

`sudo apt update`

Now we can install the packages:

`sudo apt install apache2 wget`

## Verify the Server is Running and Capture the Result

The Apache web server should be running, but let's check:

`curl http://localhost`

If that's working, we use the  `wget`  package to capture the output of an http request. We'll point the output to a file in our home directory called  `local_index.response`:

`wget --output-document=local_index.response http://localhost`

## Conclusion

Congratulations, you have successfully completed this hands-on lab!
