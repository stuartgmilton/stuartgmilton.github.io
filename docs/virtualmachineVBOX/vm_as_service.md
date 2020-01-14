---
layout: default
title: Start VM as a service
parent: Virtual Machine - VirtualBox
nav_order: 6
---

# Run your VM as a Windows Service

This is an optional section - You only need to complete this section if you would like the VM to startup (headless) automatically when your windows machines starts.

Instructions:
 1. On your host machine, open the following url - [https://github.com/onlyfang/VBoxVmService/releases/](https://github.com/onlyfang/VBoxVmService/releases/) and download the latest version of the tool.
 2. Run the executable.
 3. When prompted, accept the license, and click Next.
 4. Select the directory you would like the tool installed, and click Next.
 5. Accept the default Start Menu Folder, and click Next.
 6. Complete the installation by clicking Install followed by Finish.
 7. Open the VBoxVmService.ini file - it is located in the tools installation directory.
 8. For now remove the [VM1] section.
 9. Change the VmName in the [VM0] section, to be that of your VM.  This name can be seen in VirtualBox, but in this example it should be 'AnsibleControlNode'.
 10. Change the ShutdownMethod in the [VM0] section to be 'acpipowerbutton'.
 11. Under the [Settings] section, add the following two lines.  They can be removed once the service is installed.  Save the file when finished.
```
RunAsUser=.\USERNAME
UserPassword=PASSWORD
```
 12. Open a command prompt (as administrator) in the installation directory.  Run 'VmServiceControl.exe -i'.
 13. You may get an error saying the service already exists.  If so run these commands;
``` 
VmServiceControl.exe -u
VmServiceControl.exe -i
```
 14. It is now a decent idea to restart your windows laptop.  It will take a few minutes after the laptop boots until your VM boots in the background.  Test this by connecting directly via Putty, rather than opening VirtualBox.
 
[Next Topic](./internet_connection.md){: .btn .btn-primary .fs-2 .mb-2 .mb-md-0 .mr-2 }
