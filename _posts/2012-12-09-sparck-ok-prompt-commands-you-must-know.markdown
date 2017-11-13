---
layout: post
title:  "Sun/Oracle SPARC ok prompt commands you must know"
date:   2012-12-09 10:13:53 -0700
categories: okprompt ok sparc solaris
---

Ok, maybe your not an expert in forth, but if you work on Sparc systems long enough your going to have to work from the ok prompt.

Here are the essentials commands you must know.

Boot the system normally

```
ok> boot
```

Boot the system and allow for discovery of new devices (reconfiguration boot)

```
ok> boot -r
```

Boot into Single-User Mode

```
ok> boot -s
```

Boot into a ROM, useful if your system isn't bootable

```
ok> boot -F failsafe
```

Boot a global-cluster (suncluster) node into single user non-cluster mode.

```
ok> boot -sx
```

List your network adapters, you can then do boot net - install [device path] to boot from the network using the specified interface

```
ok> show-nets
```

Useful for determining boot devices and general server components

```
ok> show-devs
```

devalias lists the device aliases where nvalias is used to set them permanently

```
ok> devalias
ok> nvalias diskname /pathdodevice
```

Used to set environment variables used for the openboot firmware.

```
ok> printenv
ok> setenv
```

(from the OS shell you can use #eeprom auto-boot?=true, for example to set boot environment variables) 

shutdown, reboot, etc

```
ok> power-off
ok> reset-all
```
