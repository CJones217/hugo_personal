+++
author = "Collin"
title = "Setting up ClamAV daemon"
description = "Setting up ClamD with SystemD"
date = 2023-08-08
+++

## Goal

The goal of setting up ClamAV as a daemon is to be able to scan with multiple threads. I normally use clamscan but this only uses a single thread so scans are very slow. 

## Setting up Daemons

Install the [clamav](https://archlinux.org/packages/extra/x86_64/clamav/) package (this one is for Arch)

You'll need to make freshclam, the tool that updates the virus signature database, a daemon as well so the signatures to scan for stay up to date.

- ```sudo systemctl start clamav-freshclam.service```
- ```sudo systemctl enable clamav-freshclam.service```

The freshclam config file is in ```/etc/clamav/freshclam.conf```

Now clamav(clamd) needs to be made a daemon.

- ```sudo systemctl start clamav-daemon.service```
- ```sudo systemctl enable clamav-daemon.service```

Logs for the daemon are found in ```/var/log/clamav/clamd.log```

The clamd config file is in ```/etc/clamav/clamd.conf```

By default, clamd will use 10 threads.

## Using clamdscan

clamdscan is basically the same as clamscan except it uses the daemon. This makes it possible to make the scan multithreaded.

```clamdscan --multiscan --fdpass /home/```
The ```multiscan``` option tells clamd to use multiple threads and the ```fdpass``` option tells clamd to scan the file using the clamd user the daemon was started as.

## Monitor scans

when a scan is running, you can use ```clamdtop``` to monitor the progress. It acts like htop but for clamav and will show how many files are being scanned, the queue for files to scan, how many threads are used, and other resources being used by the scan.

## Conclusion

the daemons run on startup of my machine which is great. The scans now finish in 30 minutes using the daemon compared to the single thread scans of clamscan which would take many hours.

## To learn more

[clamav arch wiki](https://wiki.archlinux.org/title/ClamAV)

[clamav docs](https://docs.clamav.net/)
