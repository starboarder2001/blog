---
layout: post
title:  "ZFS primer, creating zpools and ZFS datasets"
date:   2012-12-29 10:13:53 -0700
categories: jekyll update
---

ZFS is a filesystem developed by Sun which has made its way to a variety of platforms.  Solaris and FreeBSD is where you will primarily find ZFS being used.  If you are familiar with using a Volume manager such as lvm, svm, or veritas then ZFS will be a natural transistion.  ZFS is much easier to administer than these tools.

Command basics
===

You can do everything with ZFS with only two commands: zfs and zpool.  The zpool command is used anytime you are doing things with disks where the zfs command is used anytime you are working with datasets (for now think partitions, but virtual partitions).

A zpool  is a filesystem on a collection of disks

To create a pool with a single disk (/dev/dsk/c0t0d0 could also be a file):
===

```
zpool create myzpool /dev/dsk/c0t0d0
```

To create a pool striped across multiple disk (Raid-0), no redundancy, but very fast reads/writes.

```
zpool create myzpool c0t0d0 c0t0d1
```

To create a pool using Raid-1, 50% of the total space is usable, very fast reads/writes, but is inefficient in space utilization.

```
zpool create myzpool mirror c0d0 c0d1
```

To create a pool using Raid-Z, single parity and 80% of the space is usable, its more space efficient, fast reads, but has slower write speed than the other options.

```
zpool create myzpool raidz /dev/dsk/c0t0d0 /dev/dsk/c0t0d1 /dev/dsk/c0t0d2 ...
```

A dataset is a logical collection under a pool, like a separate filesystem under the main pool.

To create a dataset under the pool:

```
zfs create myzpool/mydataset1
```

You can create datasets under datasets:

```
zfs create myzpool/mydataset1/mydataset2
```

Do a man zfs to see all the options available to set at the zfs dataset level.

Maintenance, where is fsck:
You no longer need fsck with ZFS.  ZFS hashes every file and if it detects any inconsistencies all you need to do is resilver the pool.

Some commands to get you started:

```
zpool list
zpool status
zfs list
```

