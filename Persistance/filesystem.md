## Very Simple Filesystem

Disk is split into uniformly sized blocks

Components
- Most of filesystem is **data region**
- Store metadata about file in **inode** => store indoes in the inode table (more inodes means more files)
- Use 2 **bitmaps** to keep track of free inodes and free data blocks
- **superblock** contains information about file system (how many inodes/data blocks), where inode begins, where data begins, file system type

Inode
- Identified by an i-number (low-level name)
- Can directly calculate location of inode based on its i-number (i-number * size of inode)
-  Metadata stored
    - permissions (mode)
    - uid (owner)
    - size
    - time, ctime (created), mtime (modified)
    - gid (group)
    - link_count
    - blocks allocated
- Indirection allows for larger files => point to a block that contains more pointers, each of which points to user data

Free space management
- Search bitmap for inode for the file. Similar process for data block.

Reading a file
- Begin traversal at root directory, then look of it to find pointers to data blocks, which contain contents of the root directory
    - Recursively traverse the pathname until the desired inode is found

Writing a file to disk
- Similar to read
- If necessary, decide which block to allocate to the file and update bitmasks/inode accordingly

Caching/Buffering
- Fixed-sized cache to hold popular blocks
- Dynamic partitioning integrates virtual memory pages and file system pages into a unified page cache