---
layout: post
title:  "Solaris 10 shutdown, reboot, init, and halt command differences"
date:   2011-09-16 10:13:53 -0700
categories: solaris shutdown reboot init halt
---

In summary, init and shutdown commands cleanly shutdown the system by running the shutdown rc scripts.

The advantage of shutdown is that you can set a shutdown delay and warning message.

halt and reboot are not as clean, no shutdown rc scripts are run so applications will not be brought down clean, I generally do not use these commands unless its a last resort.

```
init (runs the shutdown scripts in /etc/rc*)
init 0 (shutdown (on sparc it takes it to the ok prompt)
init s (single user mode)
init 5 (shutdown)
init 6 (reboot)
```

```
shutdown (runs the shutdown scripts in /etc/rc*, prints message warning users)
shutdown -y -g 0
shutdown -y -i 0 (shutdown to ok prompt)
shutdown -y -i S (single user mode)
shutdown -y -i 5 (shutdown)
shutdown -y -i 6 (reboot)
```

```
halt (ungraceful shutdown, use sync;sync;halt)
halt
```

```
reboot (ungraceful reboot. Always run sync;sync;reboot. The prefered method is using init.)
reboot (reboot) 
reboot -- -r  (reconfiguration reboot)
reboot -- -s (reboot into single usermode)
```
