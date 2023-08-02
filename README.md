# Luganodes_Assignment

Task - 4

## Documentation

1. Install Oracle VirtualBox and ISO file for Linux Destro. I'm be using Ubuntu version 21.10.
1. Configure a VM in VirtualBox. Refer - [**Configuring a Virtual Machine**](#vm-configuration-steps)
1. Configure the distro inside the VM. Refer - [**Configuring Ubunutu on VM**](#ubuntu-configuration-steps)
1. Once having a successful running VM, we are ready to configure the [**Firewalld using Nftables**.](#configuring-firewalld)

## Configuring Firewall

1. First, we need to install all the necessary packages. Go to **_[Required Packages](#required-packages)_**
1. Go to root access through the command: `sudo su -` and enter your password. It is a good practice to update all the repos to avoid build failures. To update run: `apt update`
1. Now, to install firewalld, inside your terminal run: `apt install firewalld`
1. After successfull installation, run the command: `systemctl status firewalld`. This would give a breif about the status of the firewalld.
1. To start the firewalld, type in the command: `systemctl start firewalld`
1. Next, we have to enable the firewalld by the command: `systemctl enable firewalld`
1. To know the version of firewalld, type: `firewall-cmd --version`
1. Next step is to get information about the available zones, type in the command: `firewall-cmd --list-all-zones`. This would list out all the available zones. It would also show the different services available for different types of zones.
1. In the available zones look out for the zone which is active. It should be public, since this is the default zone.
1. To get config informatin about any particular zone, type in the command: `firewall-cmd --zone={name} --list-all`
1. To chance the zones, we first need the exact name of the inteface card to move it from one zone to another. To get that information and change zone, put in: `firewall-cmd --zone={name} --change-interface = eno`. This would give the interface cards available. If one one card is available it will automatically change the zone. Incase there is a list, run the command: `firewall-cmd --zone={name} --change-interface = {name_of_interface_card}`
1. For further commands and their usage refer to the [Firewall-cmd documentation.](#https://firewalld.org/documentation/man-pages/firewall-cmd.html)

### Custom-Made Zones

1. To create a custom made zone, we have to run the command: `firewall-cmd --permanent --new-zone=zone-name`
1. Reload the firewall.
1. Finally make the new zone persistent, using the command: `firewall-cmd --runtime-to-permanent`

## Firewall Services

1. To get all the available firewall-services, the command is: `firewall-cmd --get-services`
1. To add a particular service into the firewall, we use the command: `firewall-cmd --add-service={name}`. Then reload the firewall: `firewall-cmd --reload`

## Nftables

- There are two ways of making the NFTtables either by making use of text file with a .nft extension, where we could write the code and pass it using a single terminal command or by typing each command in terminal.
- To get the list of all the existing tables we can make use of the command: `sudo nft list tables/ruleset/chains`
- Example for creating a nftable: `sudo nft add table inet HomeFirewall`
- Example for creating a base chain: `sudo nft add chain inet HomeFirewall INPUT \{type filter hook input priority 0\; policy accept\;\}`. This is a policy that would create the chain.
- Example for creating a base chain: `sudo nft add chain inet HomeFirewall XYZ`
- To specify certain rules in the chain, look at the following example: `sudo nft add rule inet HomeFirewall INPUT icmp type echo-request reject`. This rule would deny any ping requests send to the computer.
- To get the handle of the rule created, which would be used for deletion of the rule, type the following command: `sudo nft list table inet {table_name} -a`
- To delete the rule: `sudo nft delete rule inet {table_name} {chain_name} handle {number}`

## VM Configuration Steps

1. Open Oracle Virtual Box console and on top, click _New_ to initalize a new VM.
1. Enter the Name of VM (of your wish) and specify the folder for creation of VM. Select the ISO image of the distro, which could be browsed from your local files. VirtualBox automatically detects the type and version of the OS from the ISO file. However, incase it doesn't, we can always explicitly do it.
1. Click Next. Incase the ISO file contains an unattended guest os, we have to configure user for the OS. Add a username and password of your wish, which would further become the credentials for logging into the OS.
1. Then we specify the amount of CPU's and RAM that has to be allocate to the VM.
1. Next, we specify the disk type and the storage we want to allocate to the VM.
1. Click Next, check all the configurations once again and then proceed to click _Finish_. This would create a folder for VM inside your local machine with the allocated disk memory. It would now appear on the left hand side of Oracle VirtualBox.
1. Finally, select the newly created VM and click _Start_.

## Ubuntu Configuration Steps

1. Upon the launch of the VM, the VM would itself install the guest OS and perform all the necessary actions (being unattended).
1. Keep clicking on Next and I recommened to not change any default setting unless you have a good reason to do so.
1. It would lead you to the login page where you should see your Username, which was specified on the time of [configuration of VM](#vm-configuration-steps).
1. Click on your profile and enter your password, which was also specified during the time of [configuration of VM](#vm-configuration-steps).

## Required Packages

Here is the list of packages that is first required to be installed -

**Table of Contents:**

1. [Net-tools](#net-tools)
1. [Wireshark](#wireshark)

### Net-Tools

This package is a repository of base networking utilities for Linux. Further, refer to [Net-Tools Documentation.](#https://packages.ubuntu.com/search?keywords=net-tools)

Net-Tools: `sudo apt-instal net-tools`

Enter the user password and hit enter.

### Wireshark

This is an open-source network protocol analyser that helps us to anaylze packets and network during communication between different networks. We can run commands to get specific type of packets from the captured pool to get meaninful insights. To get the list of commands, refer to [Wireshark Documentaion](#https://www.wireshark.org/docs/wsug_html_chunked/ChCustCommandLine.html)

Wireshark: `sudo add-apt-repository ppa:wireshark-dev/stable`

Enter the user password and hit enter.
