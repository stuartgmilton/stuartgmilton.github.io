---
layout: default
title: Admin User
parent: Ansible
nav_order: 4
---

# Create a non-root admin account

As Ansible is an automation tool, it would defeat the purpose if you had to enter a password after every command, thus we will allow your non-root user to run commands as the root user without entering a password.

Instructions:
 1. Login to your VM as your non-root user.
 2. Edit the Sudoers file by running the following command;

>  sudo visudo -f /etc/sudoers

 3. Comment the following line - '%wheel ALL=(ALL)  ALL'
 4. Uncomment the following line - '#%wheel ALL=(ALL)  NOPASSWD: ALL'
 5. Save and close the file.
 6. Test that you can sudo to root without a password, by entering 'sudo -i'
 7. Type exit to log out as the root user.