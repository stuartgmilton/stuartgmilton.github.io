---
layout: default
title: Initial Creation
parent: Virtual Machine - VMWare
nav_order: 3
---

# Initial creation of the VM
{: .no_toc }

Instructions:
 1. Download the latest RHEL 7 DVD ISO from [https://developers.redhat.com/products/rhel/download](https://developers.redhat.com/products/rhel/download)
 2. Open VMware Workstation and create a new Virtual Machine (VM) by pressing Ctrl + N.
 3. Select Custom (advanced) and click Next.
 4. Accept the default Hardware Compatability and click Next.
 5. Select 'I will install the Operating System later' and click Next.
 6. Select 'Linux' and then 'RHEL 7 64bit' and click Next.
 7. Give the VM a sensible name and choose where to store it then click Next.
 8. Accept the default Processor Configuration and click Next.
 9. Accept the default Memory Configuration and click Next.
 10. Select 'Use NAT' and click Next.
 11. Accept the default I/O Controller Type and click Next.
 12. Accept the default Disk Type and click Next.
 13. Create a new virtual disk and click Next.  10GB should suffice, click Next.
 14. Accept the default file name and click Next.
 15. Click Finish.
 16. Click 'Edit virtual machine settings'. Click 'Add...'. Select 'Hard Disk' and click Next.
 17. Accept the default Disk Type and click Next.
 18. Create a new virtual disk and click Next.  10GB should suffice, click Next.
 20. Accept the default file name and click Finish.
 21. Select the CD/DVD, then select 'Use ISO image file', then select the ISO downloaded earlier. Click OK.
 22. The VM can now be powered on.
 23. You will probably have to click within the window to gain control, then use the cursor keys to select Install and hit Enter.
 24. Choose your desired language settings and click Continue.
 25. Select Installation Destination, and then ensure there is a tick on both disks. Select 'I will configure partitioning', then click Done.
 26. Click 'click here to create them automatically'
 rhel-root
 modify
 only select sdaa - then call it SystemVG  Save
 
 / filesystem to ext4
 change name to rootVG
 
 select swap
 change name to swapVG
 
 DONE
 
 
 
 
 
 15. Begin the installation in the background by clicking 'Begin Installation'
 16. You can now set the root users password by clicking on it.  Enter the password twice and click Done.
 17. As we do not want to be using the root used by default, we will create another administrator account for our use. Click 'User Creation'.  Enter a Full name and User name.  I suggest 'ansible' for both.  Ensure the 'Make this user administrator' checkbox is checked.  Enter the password twice and then click on Done.
 18. Wait for the installation to complete, and then click 'Finish configuration'
 19. Click the Reboot button, and wait for the VM to restart.
 20. Login to the VM using the non-root account.
 21. To connect the VM to your host, we now need to make a change to the VMs network card.
```
     sudo vi /etc/sysconfig/network-scripts/ifcfg-enp0s3
```
 22. Edit the ONBOOT line to equal 'set ONBOOT=yes'.  Save the file.
 23. Or sed -i '/ONBOOT/s/no/yes'/ /etc/sysconfig/network-scripts/ifcfg-enp0s3
 24. Restart the VM using 'reboot'

[Next Topic](./port_forwarding.md){: .btn .btn-primary .fs-2 .mb-2 .mb-md-0 .mr-2 }

 ---
