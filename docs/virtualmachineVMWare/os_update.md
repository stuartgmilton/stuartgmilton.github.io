---
layout: default
title: OS Update
parent: Virtual Machine - VMWare
nav_order: 5
---

# RedHat Subscription

Instructions:
 1. Login to your VM as your non-root user.
 2. Run the below command, swapping out the placeholders for you RedHat account credentials.
```
sudo subscription-manager register --username XXX --password XXX --auto-attach
```
 3. Once registered, update the system with the below command.
```
sudo yum update -y
``` 
 4. 
```
sudo yum install https://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm -y
```
 5. 
```
sudo yum install vim wget git tree nc -y
```
  
[Next Topic](./internet_connection.md){: .btn .btn-primary .fs-2 .mb-2 .mb-md-0 .mr-2 }
