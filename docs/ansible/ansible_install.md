---
layout: default
title: Ansible Installation
parent: Ansible
nav_order: 4
---

# Ansible Installation

Instructions:
1. Run the following command to install Ansible.

> sudo yum install ansible python-boto python-boto3 -y

2. As Ansible works over SSH, we will now create an SSH Key to allow connectivity between VMs.  Run the following commands;

> ssh-keygen -t rsa -b 4096 -f ~/.ssh/id_rsa -q -P ""
>
> cat ~/.ssh/id_rsa.pub >> ~/.ssh/authorized_keys
>
> chmod og-wx ~/.ssh/authorized_keys

Test that Ansible is installed and working correctly by running 'ansible localhost -m ping'.  You should receive output like below;

> [WARNING]: provided hosts list is empty, only localhost is available. Note that the implicit localhost does not match 'all'
> localhost | SUCCESS => {
>     "changed": false,
>     "ping": "pong"
> }

Ansible is installed and working.  You can ignore the warning for now.