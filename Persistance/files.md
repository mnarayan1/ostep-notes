## File

How to manage persistent data.

File: linear array of bytes with a low-level name (inode number)

Creating a file involves
1. Creating an inode that tracks size, where its blocks are located on disk, etc
2. Linking a human readable name to inode, and putting that link into directory

Directory: also has an i-number. Contains list of user-readable names mapped to i-node numbers.

API
- open()
    - returns a file descriptor (integer)
    - FDs are managed by OS on a per-process basis
- read() and write()
    - self-explanatory, return number of bytes read/written
- lseek()
    - non-sequential reads and writes (include offset)

Sharing
- Each process will have a unique FD, but child shares FDs from parent
- dup() redirects a program's stdout to a different file descriptor
- mmap() => creates correspondence between file offset and virtual address in calling process (can be used for IPC)

Metadata
- stat() and fstat() syscalls

Linking
- When you link(), you create another way to refer to the same file
    - Same inode number, different name
- When you unlink(), you track relevant information about the file
    - You only "delete" a file once the reference count in the inode has reached zero
- symlink allows you to link to a file in another disk partition or link to a directory
    - is a file itself, holds the pathname of the linked file as data