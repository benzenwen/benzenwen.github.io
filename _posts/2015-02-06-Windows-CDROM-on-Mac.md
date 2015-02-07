---
layout: post
title:  "Windows CD-ROMs on a Mac"
date:   2015-02-06
categories: howto sysadmin
tags: mac apple osx commands
comments: True
---

I recently had need of an circa 2000 Windows CD-ROM.  It was a
language learning CD-ROM, and I wanted to run it in a VirtualBox VM
running Windows XP.

My main machine is a MacBook Air.  I don't have an external optical
drive, so I also wanted a readable image.  I have another Mac with an
optical drive to do the initial read.

_To mount the drive_

~~~~
> mkdir /Volumes/foo
> mount_cd9660 -er /dev/disk1s1 /Volumes/foo
~~~~


_To make a image of it that's readable in a Windows VM_

~~~~
> hdiutil makehybrid -o /tmp/foo.iso /Volumes/foo
~~~~

Note, don't use Disk Utility.

The resulting file can be mounted and read by the XP machine.  
