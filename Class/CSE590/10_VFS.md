---
layout: post
title: Untitled
tags:
  - linux
  - filesystem
---
# Symlinks

`int (*readlink) (struct dentry *, char __user *,int);`

The `__user` subtype tells the kernel that the address is in the userspace and not the kernel space.

# Negative dentry

A negative dentry has two benefits.

1. If we find a dentry w/o an inode (i.e., dentry with RC=0 but
dentry->"NULL inode"), for example dentry->d_inode==NULL, then we KNOW that
the on-disk file does NOT exist.  And we can immediately return ENOENT w/o
spending any I/O cycles.

2. A negative dentry could become a positive dentry in the future.  That is,
its RC will go from 0 to 1.  That can happen if the previously non-existent
(or deleted file), is now re-created.