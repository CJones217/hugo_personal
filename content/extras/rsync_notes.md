+++
author = "Collin"
title = "Notes for Rsync"
date = 2024-09-23
description = "List of random notes for interacting with rsync so I can look back when I forget"
+++

- Use rsync to copy home directory to mounted backup drive. Ignore cache.

```sudo rsync -aAXv --exclude '/home/collin/.cache/*' /home /mnt/veracrypt5/folder_rsync```

- Use rsync to copy local backup drive to offline drive.

```sudo rsync -aAXv /mnt/veracrypt5 /mnt/veracrypt3/rsync_harddrive```
