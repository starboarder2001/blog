---
layout: post
title:  "Setting the infiniband (IB) node description on Solaris"
date:   2017-12-22 10:13:53 -0700
categories: jekyll update
---

By default the node description for the IB interfaces on Solaris is set to the name of the card.  If you wish to change the node description that matches the server hostname, just run the set_nodedesc.sh command.
===

```
# set_nodedesc.sh
```

You can set the IB node description to whatever you want using the -N option with set_nodedesc.sh.
===

```
# set_nodedesc.sh -N 'something'
```

You can reference the [man page](https://docs.oracle.com/cd/E86824_01/html/E54764/set-nodedesc-sh-1m.html) for the set_nodedesc.sh command to see the full command reference.
