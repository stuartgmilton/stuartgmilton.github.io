---
layout: default
title: Virtual Machine
nav_order: 2
has_children: true
permalink: /docs/virtualmachine
---

# Create a VM
{: .no_toc }
Pre-requisites:
 - You have the latest VirtualBox 6.x installed
 - You have the appropriate version of the VirtualBox Extensions Pack installed
 - You have Putty or a similar SSH Connection tool installed

Instructions:
 1. Download the latest Centos 7 Minimal ISO from [https://www.centos.org/download/](https://www.centos.org/download/)
 2. Open VirtualBox and create a new Virtual Machine (VM) by clicking the New button.
 3. Give the VM a representative name, such as 'AnsibleControlNode'.  Change the type to 'Linux', and the Version to 'Red Hat (64-bit).  Click Next.
 4. Accept the default 'Memory size' and click Next.
 5. Accept the default 'Hard Disk' and click Next.
 6. Accept the default 'Hard disk file type' and click Next.
 7. Accept the default 'Storage on physical hard disk' and click Next.
 8. Accept the default 'File location and size' and click Create.
 9. Right click on the new VM in VirtualBox.  Select Settings > System > Motherboard.  Change the pointing device to USB Tablet.  Click OK
 10. Right click on the new VM in VirtualBox.  Select Settings > Storage.  Select the empty disk drive under the IDE Controller.  Under Attributes, click the small CD image, then 'Choose Virtual Optical Disk File'.  Locate the CentOs 7 Minimal ISO.  Click Open.  Click OK.
 11. Double click on the new VM in VirtualBox to power it on.
 12. Select Install CentOs 7 using the cursor keys.  Hit Return.  After a short pause, you will be presented with a GUI to guide you through the installaton of CentOs.
 13. Choose your desired language settings and click Continue.
 14. Select Installation Destination, and accept the defaults by clicking Done.
 15. Begin the installation in the background by clicking 'Begin Installation'
 16. You can now set the root users password by clicking on it.  Enter the password twice and click Done.
 17. As we do not want to be using the root used by default, we will create another administrator account for our use. Click 'User Creation'.  Enter a Full name and User name.  I suggest 'ansible' for both.  Ensure the 'Make this user administrator' checkbox is checked.  Enter the password twice and then click on Done.
 18. Wait for the installation to complete, and then click 'Finish configuration'
 19. Click the Reboot button, and wait for the VM to restart.
 20. Login to the VM using the non-root account.
 21. To connect the VM to your host, we now need to make a change to the VMs network card.


    sudo vi /etc/sysconfig/network-scripts/ifcfg-enp0s3
 22. Edit the ONBOOT line to equal 'set ONBOOT=yes'.  Save the file.
 23. Towards the bottom of the VMs window, right click on the network icon (2 monitors), and click 'Network Settings'.  Under Adapter 1, click Advanced and then 'Port Forwarding'.
 24. Add a new record like so, and click OK.

| Name | Protocol | Host IP | Host Port | Guest IP | Guest Port |
|--|--|--|--|--|--|
| SSH | TCP | 127.0.0.1 | 2222 | 10.0.2.15 | 22 |

 25. Click OK again then restart the VM by running the 'reboot' command
 26. Open Putty and connect to 127.0.0.1 on port 2222.  You will be asked to accept the VMs key fingerprint - click Yes.
 27. Login to the VM using your non-root account.

 ---
