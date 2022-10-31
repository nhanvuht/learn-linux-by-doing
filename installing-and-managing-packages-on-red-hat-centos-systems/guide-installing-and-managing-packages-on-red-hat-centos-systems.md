
# Installing and Managing Packages on Red Hat/CentOS Systems

## Scenario

Your development team is working on their new web-based API. During testing, they decided to use a terminal based web browser to perform tests on a separate system (that way, they don't have to leave their terminal window). They found a terminal browser they like, but it has to run a specific version that is a bit different from the repository version. They managed to download the appropriate package for their system and architecture, but are unable to install it. Performing the package installation indicates that there are several missing dependencies. They have asked you to resolve the issue and have provided your credentials and connection information to their client testing system. You will need to install the 'elinks' package in the /home/cloud_user/Downloads directory successfully. You can resolve the unmet dependencies however you choose, but the version that has already been downloaded is the version that will need to be installed. Once you verify the application is installed and running properly, you can turn the system back over for their use.

## Objectives


###  Elinks Application Install and Available

An elinks rpm file is already downloaded, but can't be installed because of missing dependencies.

In order to install the package successfully, you will need to deal with the dependencies. You can use the package manager to do that for you via:

`sudo yum install /home/cloud_user/Downloads/elinks-0.12-0.37.pre6.el7.0.1.x86_64.rpm`

Optionally, adding  `-y`  to the command (`sudo yum -y install...`) will skip prompting for the dependencies, and will just complete the install as though you'd said "yes" to everything.

If you are able to install the application and dependencies successfully, the learning activity can be considered successfully completed.

__Note:__: The  _exact_  version in your activity may be different; this version was current as of the time this activity was created.

### Elinks Package RPM Exists

You've been asked to install a package called  _elinks_  using the  `/home/cloud_user/Downloads/elinks-0.12-0.37.pre6.el7.0.1.x86_64.rpm`  file, and this package must be present in order to do so.

Verify that the application is installed. You can check by doing either:

`which elinks`

Which will return the /usr/bin/elinks path, or simply run the command to view the console browser application itself

`elinks`

You can exit once you acknowledge the dialog by pressing the 'ESC' key.

## Additional Resources

Your development team is working on their new web-based API. During testing, they decided to use a terminal based web browser to perform tests on a separate system. This way, they won't have to leave their terminal window. They found a terminal browser they like, but it the version they need to run is a bit different from the version in the official repository.

They managed to download the appropriate package for their system and architecture, but are unable to install it because of several missing dependencies. They have asked you to resolve the issue, and have provided you with credentials and connection information to their client testing system.

You will need to successfully install the elinks using the .rpm file that the development team downloaded. You can resolve the unmet dependencies however you choose, but the version that has already been downloaded is the version that you need to install. Once you verify the application is installed and running properly, you can turn the system back over for their use.

## Solution
1.  Log in to the cloud server using the credentials provided in the hands-on lab page.
    
2.  Attempt to install the RPM to determine what dependencies are required:
    

`cd Downloads sudo rpm -i elinks-0.12-0.37.pre6.el7.0.1.x86_64.rpm`

We'll get some dependency errors (version numbers may vary):

`error: Failed dependencies: libmozjs185.so.1.0()(64bit) is needed by elinks-0.12-0.37.pre6.el7.0.1.x86_64 libnss_compat_ossl.so.0()(64bit) is needed by elinks-0.12-0.37.pre6.el7.0.1.x86_64`

1.  Use the package manager to determine which packages provide the dependencies:

`sudo yum provides libmozjs185*`

The output shows that the  `js`  package provides  `libmozjs185`.

1.  Install the packages that provide those dependencies:

`sudo yum install js`

1.  All of our dependencies were not resolved with that one package installation. Attempt to install the RPM again. If any other dependencies are needed, repeat steps 3 and 4 (substituting  `libmozjs185`  with whatever dependency is still missing) to resolve that issue:

`sudo rpm -i elinks-0.12-0.37.pre6.el7.0.1.x86_64.rpm`

1.  Once the RPM is installed successfully, run  `elinks`  to ensure the application is working properly:
    
    -   Run the application:
    
    `elinks`
    
    -   Attempt to open a website by providing a URL:
        -   _[http://www.amazon.com](http://www.amazon.com/)_
2.  If the dependency issues have been resolved and the application is working properly, you have completed this hands-on lab. Great job!
