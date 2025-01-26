+++
author = "Collin"
title = "Notes for udiskctl"
date = 2025-01-26
description = "List of random notes for interacting with udiskctl so I can look back when I forget"
+++

- Use udiskctl to mount a drive with permissions of the user (no longer need sudo to access mounted files).

```udisksctl mount -b /dev/sdc1```

- unmount drive.

```umount /dev/sdc1```

- unmount drive using udisksctl.

```udisksctl unmount -b /dev/sdc1```

- if needed, set permissions of files on drive to current user for read write execute.

```sudo chmod ug+rwx /run/media/user/media_dir```

- view info of drives.

```udisksctl status```

- show more detailed info of drive.

```udisksctl info --block-device /dev/sdc1```

```-b``` and ```--block-device``` are the same thing.

- monitor storage events of drives. It will open a window with live events happening.

```udisksctl monitor```


If you want to learn more, check out [this site](https://commandmasters.com/commands/udisksctl-linux/) it helped a ton.
