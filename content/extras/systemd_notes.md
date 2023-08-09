+++
author = "Collin"
title = "Notes for SystemD"
date = 2023-08-08
description = "List of random notes for interacting with SystemD so I can look back when I forget"
+++

- start service, this will stop once machine restarts

```systemctl start [NAME_OF_SERVICE]```

- enable service, this will run even after restart

```systemctl enable [NAME_OF_SERVICE]```

- view status of serivce, works when it is enabled, disabled, running, or stopped

``` systemctl status [NAME_OF_SERVICE]```

- list all services that are enabled

```systemctl list unit-files | grep enabled```

- list all services that are running

```systemctl | grep running```
