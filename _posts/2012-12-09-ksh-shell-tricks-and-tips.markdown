---
layout: post
title:  "ksh trick - For a one liner shell command that exceeds 80 characters"
date:   2012-12-29 10:13:53 -0700
categories: ksh shell scripting
---

Lets say you start out with something simple.


```
$ ls -l
total 0
drwxr-xr-x   4 starboarder2001  staff   136 Aug  7  2011 Books
drwx------   6 starboarder2001  staff   204 Aug 19 22:02 Business
drwxr-xr-x   5 starboarder2001  staff   170 Jul 30  2011 Calibre Library
drwxr-xr-x+  4 starboarder2001  staff   136 Nov 25 10:50 Desktop
drwxr-xr-x+  9 starboarder2001  staff   306 Nov 18 21:24 Documents
drwxr-xr-x+ 12 starboarder2001  staff   408 Dec  9 17:58 Downloads
drwxr-xr-x@ 11 starboarder2001  staff   374 Dec  9 18:00 Google Drive
drwxr-xr-x@ 59 starboarder2001  staff  2006 Nov 13 08:03 Library
drwxr-xr-x+  5 starboarder2001  staff   170 Nov 25 22:09 Movies
drwxr-xr-x+  5 starboarder2001  staff   170 Aug 19 21:50 Music
drwxr-xr-x+ 30 starboarder2001  staff  1020 May 29  2012 Pictures
drwxr-xr-x+  6 starboarder2001  staff   204 Jul 31  2011 Public
drwxr-xr-x+  4 starboarder2001  staff   136 Apr 15  2009 Sites
drwxr-xr-x   8 starboarder2001  staff   272 Nov 25 21:36 mac_projects
```

```
$ IFS="
"
$ for i in `ls -l | awk '{if ($1 ~ /\+$/){print;}}'`; do echo $i; done

drwxr-xr-x+  4 starboarder2001  staff   136 Nov 25 10:50 Desktop
drwxr-xr-x+  9 starboarder2001  staff   306 Nov 18 21:24 Documents
drwxr-xr-x+ 12 starboarder2001  staff   408 Dec  9 17:58 Downloads
drwxr-xr-x+  5 starboarder2001  staff   170 Nov 25 22:09 Movies
drwxr-xr-x+  5 starboarder2001  staff   170 Aug 19 21:50 Music
drwxr-xr-x+ 30 starboarder2001  staff  1020 May 29  2012 Pictures
drwxr-xr-x+  6 starboarder2001  staff   204 Jul 31  2011 Public
drwxr-xr-x+  4 starboarder2001  staff   136 Apr 15  2009 Sites
```

Ok, now you want to fine tune this command, what to do.

```
$ set -o vi on
$ (press and release k, press and release esc, then v)
```

Now the line is open in vi

```
  1 for i in `ls -l | awk '{if ($1 ~ /\+$/){print;}}'`; do echo $i; done
```

Make changes as you like in vi

```
 1 for i in `ls -l | awk '{if ($1 ~ /\+$/){print;}}'|grep -vi do`; do
  2     echo $i
  3 done
```

Now press ZZ or :wq!

```
$ for i in `ls -l | awk '{if ($1 ~ /\+$/){print;}}'`; do echo $i; done
for i in `ls -l | awk '{if ($1 ~ /\+$/){print;}}'|grep -vi do`; do
    echo $i
done
drwxr-xr-x+  4 starboarder2001  staff   136 Nov 25 10:50 Desktop
drwxr-xr-x+  5 starboarder2001  staff   170 Nov 25 22:09 Movies
drwxr-xr-x+  5 starboarder2001  staff   170 Aug 19 21:50 Music
drwxr-xr-x+ 30 starboarder2001  staff  1020 May 29  2012 Pictures
drwxr-xr-x+  6 starboarder2001  staff   204 Jul 31  2011 Public
drwxr-xr-x+  4 starboarder2001  staff   136 Apr 15  2009 Sites
```

Rinse and repeat as needed.  Now you can make those lengthy one liner commands look neat and organized without using a temporary file.
