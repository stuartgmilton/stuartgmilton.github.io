---
layout: default
title: Oracle
nav_order: 5
has_children: true
permalink: /docs/oracle
---

# Oracle

clone https://github.com/oracle/docker-images

Download Oracle binaries from
https://www.oracle.com/technetwork/database/enterprise-edition/downloads/index.html
make sure you use the linux link: Linux x86-64 and download to put them into the dockerfiles/<version> folder. The needed file is named linuxx64__database.zip. You also have to make sure to have internet connectivity for yum. Note that you must not uncompress the binaries. The script will handle that for you and fail if you uncompress them manually!

If you wget on the vm, authorization will be a problem, so in your browser, select the binary to download, log in and start the download.  Pause the download.  Go to your browsers downloads and copy the link. Finally, on the vm, wget and paste the link.  The downloaded file needs to be in its dockerfile folder in the cloned directory, if 18.3 was downloaded, then put the zip in OracleDatabase/SingleInstance/dockerfiles/18.3.0/
Remove the auth part from the zip file.
cd to where the buildDockerImage.sh is.

sudo ./buildDockerImage.sh -v 18.3.0 -e
Checking if required packages are present and valid...
{:toc}
