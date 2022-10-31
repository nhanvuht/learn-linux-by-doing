
# Host Security with TCP Wrappers and Systemd Sockets

## Introduction

A Linux system administrator is responsible for keeping their servers secure. There are a multitude of tools and software packages available to keep a networked Linux system safe from malicious intruders. In this hands-on lab, we will learn how to move away from always-on services to those that use systemd socket units. Socket units only provide access to a network service when an incoming connection requests it. To further enchance the security of the service, we will apply TCP wrappers to allow incoming connections to a specified service.

## Objectives


###  Configure `sshd` to use sockets.

You will be using an active SSH connection to the server when you log in.

1.  Verify that the  `sshd.socket`  unit is not active:

`systemctl status sshd.socket`

The output should show that it is not active.

1.  We will need to set up an  `at`  job that will stop the  `sshd.service`  unit and start the  `sshd.socket`  for us. Run the following commands in this sequence:

`sudo at now + 3 minutes at> systemctl stop sshd.service at> systemctl start sshd.socket at> <EOT>`

The  <EOT>  is from the key combination  **Ctrl+D**. After three minutes, the  `sshd.service`  will stop, and the  `sshd.socket`  unit will take over for your connection, so your remote shell should not disconnect. If it does, SSH back into the learning activity again.

1.  After the time has expired on the  `at`  job, verify that the  `sshd.socket`  unit is active and running:

`systemctl status sshd.socket`

Now any new secure shell connections that come into the system will utilize an on-demand socket. This way, the server does not have to keep a running secure shell running.

1.  Enable the socket for SSH and disable the service for SSH:

`sudo systemctl enable sshd.socket sudo systemctl disable sshd.service`

###  Set up TCP wrappers to only allow SSH.

1.  First, verify that the  `sshd`  server has been compiled to use TCP wrappers:

`ldd /usr/sbin/sshd | grep libwrap`

You should see that the  `sshd`  binary is capable of being used with TCP wrappers.

1.  Edit the  `/etc/hosts.allow`  file, and add the following:

`sshd2 sshd : ALL`

This will permit incoming SSH connections from any network.

1.  Now set up a default deny rule for TCP wrappers to deny any other incoming connections. Edit the  `/etc/hosts.deny`  file and add the following:

`ALL : ALL`

Exit out of the SSH session and attempt to reconnect. Provided that the commands have been entered as described, you will be granted access back into the system.

## Additional Resources

Secure your system using the TCP Wrappers using the Systemd Socket Units. Check that the  `sshd.socket`  unit is not running and then create an  `at`  job that will stop the SSH service and then start the  `sshd.socket`  service. After three minutes, verify that the  `sshd.socket`  unit is running.

Enable the socket unit while disabling the SSHD service so that this change is permanent. Using TCP Wrappers, configure the service so that it allows specific connections to use SSH. Edit the appropriate file to allow SSH incoming from any network.

Be sure to  `DENY`  any other connections from any other systems to any other services. Verify you can then reconnect to the SSH server as expected.

## Connecting to the Lab

1.  Open your terminal application, and run the following command. (Remember to replace  `<PUBLIC_IP>`  with the public IP you were provided on the lab instructions page.)

`ssh cloud_user@&lt;PUBLIC_IP&gt;`

1.  Enter your password at the prompt.

## Configure  `sshd`  to use Sockets

1.  Verify that the  `sshd.socket`  unit is not active.

`systemctl status sshd.socket`

1.  Set up an  `at`  job that stops the  `sshd.service`  unit and starts  `sshd.socket`.

`sudo at now + 3 minutes`

1.  Enter your password at the prompt.
2.  Add the following:

`at> systemctl stop sshd.service at> systemctl start sshd.socket`

1.  Press  **Ctrl + D**  to end the  `at`  job configuration.
2.  Verify that the  `sshd.socket`  unit is active and running.

`systemctl status sshd.socket`

1.  Enable the socket for SSH and disable the service for SSH.

`sudo systemctl enable sshd.socket sudo systemctl disable sshd.service`

## Set Up TCP Wrappers to Only Allow SSH

1.  Verify that the  `sshd`  server has been compiled to use TCP wrappers.

`ldd /usr/sbin/sshd | grep libwrap`

1.  Edit the  `/etc/hosts.allow`  file.

`sudo vim /etc/hosts.allow`

1.  Add the following line to the file:

`sshd2 sshd : ALL`

1.  Edit the  `/etc/hosts.deny`  file.

`sudo vim /etc/hosts.deny`

1.  Add the following line to the file:

`ALL : ALL`

1.  Exit the SSH session.

`exit`

1.  Reconnect to the secure shell session.

`ssh cloud_user@&lt;PUBLIC_IP&gt;`

1.  Enter your password at the prompt.

## Conclusion

Congratulations, you've successfully completed this hands-on lab!
