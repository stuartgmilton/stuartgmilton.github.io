---
layout: default
title: Port Forwarding
parent: Virtual Machine
nav_order: 3
---

# Port forward from host to VM

 1. Towards the bottom of the VMs window, right click on the network icon (2 monitors), and click 'Network Settings'.  Under Adapter 1, click Advanced and then 'Port Forwarding'.
 2. Add a new record like so, and click OK.

| Name | Protocol | Host IP | Host Port | Guest IP | Guest Port |
|--|--|--|--|--|--|
| SSH | TCP | 127.0.0.1 | 2222 | 10.0.2.15 | 22 |

 5. Click OK.
 6. Open Putty and connect to 127.0.0.1 on port 2222.  You will be asked to accept the VMs key fingerprint - click Yes.
 7. Login to the VM using your non-root account.
