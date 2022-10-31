# Testing DNS Resolution

## Scenario
A Linux system administrator is expected to know how to configure a system's DNS settings. Nearly all modern Linux distributions use NetworkManager to handle a host's DNS settings. In this learning activity, we will utilize the `nmcli` utility to configure our DNS resolution.

## Objectives

Review current DNS configuration.

Configure your system to use your network's DNS.

## Additional Resources
You just started a new job where you will be managing a server for a small business. After you take inventory of the equipment, you notice that one of the servers on the local network is not configured to use DNS. After you ask your fellow employees about it, they say that the system in question has never been able to access remote sites for updates. You have determined that the server can not get updates because it can not resolve the hostnames for the update servers to the IP addresses. You sit down to correct this issue, with the help of the  `nmcli`  command-line tool.

DNS Server IP Address:  `10.0.0.2`


## Solution

In this hands-on lab, we will utilize the  `nmcli`  utility to configure our DNS resolution. Please note, the use of  `eth0`  in the video has been replaced with  `ens5`.

### Before We Begin

Open a terminal session, and log in via SSH using the credentials provided on the lab page.

### Review Current DNS Configuration

1.  See if the system can resolve hostnames to IP addresses:
    
    `host www.google.com`
    
    Note that the command times out.
    
2.  Check to see what DNS server entries we have in the  `/etc/resolv.conf`  file:
    
    `cat /etc/resolv.conf`
    
    Note that we do not have any DNS entries listed.
    
3.  Review our network connections:
    
    `nmcli con show`
    
4.  Our default connection name should be  `System ens5`. Review our DNS IP settings:
    
    `nmcli -f ipv4.dns con show "System ens5"`
    
    This system obviously does not have any DNS servers configured for use.
    

### Configure Your System to Use Your Network's DNS

1.  Modify the system's default connection to use the network's DNS server:
    
    `sudo nmcli con mod "System ens5" ipv4.dns "10.0.0.2"`
    
2.  Verify the settings using the  `nmcli`  command and then checking the  `/etc/resolv.conf`  file:
    
    `nmcli -f ipv4.dns con show "System ens5" cat /etc/resolv.conf`
    
3.  We need to reactivate the system's network connection for the change to take effect:
    
    `sudo nmcli con up "System ens5"`
    
4.  Verify our settings once more:
    
    `cat /etc/resolv.conf`
    
5.  Now, attempt to resolve a hostname to an IP address:
    
    `host www.google.com`
    
    Our system should be able to resolve an IP address for the domain name.
    

## Conclusion

Congratulations on completing this hands-on lab!
