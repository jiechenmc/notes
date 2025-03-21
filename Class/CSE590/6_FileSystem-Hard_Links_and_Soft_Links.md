---
layout: post
title: Hard Links and Soft Links
tags:
  - linux
  - filesystem
---
# Symlinks

Soft or symbolic links are indirect pointers to other files/directories/other Symlinks/etc. They are sometimes called "delayed name resolution" files, because at creation time, what the symlink points to is not checked at all. Symlinks can point to path components, anything.

Symlinks can cause a cycle and the OS has to ensure that no such loops exist.

## Aside

- OS are complex and hard to develop/debug
- OS designers like to use simple data structures and algorithms
- Fancier ones are harder to debug and has a bigger memory footprint
- Data Structures: lists, tables, and very few trees (R/B trees, B trees)

## Detecting Loops

- When the OS resolve a single path name (open)
- The OS starts a counter: how many times traversed
- Each time the lookup cross another symlink, counter++
- If counter > max number: stop with ELOOP error
- Usually max ~ 10-20, some OS will let you configure

Above will catch even small cycles (a->b, b-a), but will also prevent non-cyclic sequence of Symlinks.

Symlinks have their own inode object and inode# on disk. They can be thought of as a "regular" file whose content may eventually be translated as if it were a path name. 

To read the content of a symlink, use `readlink()`.

`lstat()` to get stat info about Symlinks because `stat()` follow Symlinks.

## MS-DOS

Older filesystems like MS-DOS used a long linked list of LBAs, reserving some bytes at the end of a LBA to point to the next time. This was fragile and any problems in the disk can "cut off" a file.

Modern OSs (BSD FFS -- Fast File System) use direct blocks, 1st indirect blocks, and 2nd indirect blocks, to point to LBAs that themselves are pointers to data or other LBA pointers.  This is much more efficient to seek and append: O(log n).  It also allows files to grow a lot.

Smaller Files are stored directly in the inode.
- more efficient, don't need to allocate an LBA
- faster: file content is right there inside the inode

How can you distinguish those files?
- reserve 1 bit for a flag to distinguish "embedded" content vs. not
- can assume that if file size is < X, then it's embedded, else stored in
  external LBAs
# Hard Links

A "hard" link is another name for the same inode.  Note that a symlink has a
different (new) inode.

A hard link is a directory entry with a diff name, that points to an existing inode. They point to the same inode no matter where they move to in the filesystem.