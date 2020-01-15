---
layout: default
title: Internet Connection
parent: Virtual Machine - VMWare
nav_order: 6
---

# Connect the VM to the Internet

As our machines are situated behind a corporate proxy server, we need to configure the VM to be able communicate via this proxy.  To do this, we will install CNTLM, a popular authentication proxy.

Instructions:
1. Ensure you are connected to the dirty internet, and not behind the corporate proxy.
2. Login to your VM.
3. Run the following command to install some helpful tools.

> sudo yum install vim wget git tree epel-release nc -y

4. To install CNTLM, run the following.

> sudo yum -y install cntlm

5. We now need to create our authentication values for the CNTLM config.  Run the following command, swapping out the placeholders with your own info.  You will be asked to enter your domain password.

> cntlm -H -u [USERNAME] -d [DOMAIN]

6. Copy the PassLM, PassNT & PassNTLMv2 lines.
7. Open the CNTLM configuration file - '/etc/cntlm.conf' and paste the values underneath the 'Password' line.
8. Comment out the Password line.
9. Update your Username and Domain.
10. Comment the two Proxy lines, and add in your corporate proxy on a new line.
11. Update the NoProxy line to look like so - 'NoProxy        *'.  Save and close the file.
12. To enable the CNTLM service, run the following commands.

> sudo systemctl enable cntlm
> sudo systemctl restart cntlm

13. Test the CNTLM is working by executing the following command.  CNTLM is working if the HTTP return code is 200.

> curl -Is https://www.bbc.co.uk

14. Create a file to hold the Proxy info - 'sudo vim /etc/profile.d/proxy.sh'.  Paste in the following lines;

> export http_proxy=http://localhost:3128
> export https_proxy=http://localhost:3128
> export ftp_proxy=http://localhost:3128

16. Ensure the environment variables are live by executing the file - '. /etc/profile.d/proxy.sh'.
17. To ensure YUM works via the new proxy, update the /etc/yum.conf file to add a line in the [main] section like so;

> proxy=http://127.0.0.1:3128

18. You can now reconnect to URA/ww930.

[Next Topic](./cntlm_proxy.md){: .btn .btn-primary .fs-2 .mb-2 .mb-md-0 .mr-2 }
