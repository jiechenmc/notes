---
layout: post
title: Block Based Organization
tags:
  - linux
  - filesystem
---

The filesystem has to decide how to layer the information on LBAs 0...N

- That initialization step is format

What does mkfs do?

- Where do we place inodes?
- How many inodes can we preallocate?
- Where would data blocks go?
- How do I know what blocks/inodes are used or free?

You have to decide how many Inodes vs data/dir blocks you need
How many bitmaps needed for each type of data
Where is the start/end/len of each type of data
-> Store all these sizes/offsets in a special superblocks

Each superblock has a "magic number" that identifies the filesystem

`mount()` checks for the "magic number" and will refuse to mount if it does not match what is going to be mounted.

## Example 1

Suppose I want to create a new file and write some data to it.

1. Get an unused inode
2. Get an unused data block
3. Mask allocation bitmaps for inodes and for data blocks
4. Update the superblock count of used/unused data/inodes
5. Create a named entry in some directory, write <name, inode> tuple

What if power goes out?

- Bitmaps say data is allocated but the actual data blocks are not used
- Data blocks are used but bitmap is not updated
- Dirent points to an inode, but that inode is not initalized
- Inodes created but points to data blocks that aren't initialized or used
- A lot of dangling pointers or "orphans"
