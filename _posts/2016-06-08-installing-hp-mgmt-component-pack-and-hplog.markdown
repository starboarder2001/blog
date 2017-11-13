---
layout: post
title:  "Installing HP Management Component Pack and the hplog utility on RedHat/CentOS"
date:   2016-06-08 10:13:53 -0700
categories: jekyll update
---

Create The Yum Repo File
===

```
vi /etc/yum.repos.d/mcp.repo
[mcp]
name=Management Component Pack
baseurl=http://downloads.linux.hpe.com/repo/mcp/centos/$releasever/$basearch/current
enabled=1
gpgcheck=0
```

Clear The Yum Cache
===

```
yum clean all
```

Install hp-health, hplog is part of this package
===

```
# yum install hp-health
```

To View power
===

```
hplog -p
```

To View thermals
===

```
hplog -t
```

To View fan speeds
===

```
hplog -f
```

To View All the Logs
===

```
hplog -v
```
