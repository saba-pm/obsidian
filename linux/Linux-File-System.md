We have these  in the root directory:
- bin
	 /bin. The /bin directory, which stands for “binary” **includes basic binaries that are required for the system's basic function**. These binaries are available to all users and are required for the system to function properly. In other words, /bin contains the basic commands that users utilize on a daily basis.
- Boot
	Every Linux system has a boot directory, with all the needed files for the boot process. This directory is mounted directly on the root file system and is called **/boot**. Out of all of these files, there are four that stand out: The Configuration file
- etc
	The /etc directory **contains system configuration information**. Several files and subdirectories have been added, removed, or changed. File system commands, such as mount*, have been moved to subdirectories of the /usr/lib/fs directory.
- Dev
	this directory related to devices. On Linux, we have two types, one of them is block device and another one is character device.
	All hardware connect to the server and kernel can recognize them define in these directories.  The /dev directory contains device files (also sometimes known as device special files and device nodes) that provide access to peripheral devices such as hard disks, to resources on peripheral devices such as disk partitions, and pseudo devices such as a random number generator.
- Home
 - lib
	 The /lib directory **contains those shared library images needed to boot the system and run the commands in the root file system**, ie. by binaries in /bin and /sbin .
 - Mnt
	 The /mnt directory exists on all Linux systems, and it is **intended specifically for use as a mount point for temporary media like floppy disks or CDROMs**. It may be empty, or it may contain subdirectories for mounting individual devices.
- Root
- sbin (system binary)
      some commands are built in, and they are existed in the kernel like ls, CD, blkid they are in bin directory, but some commands are added they are in sbin.
	 /sbin. Unlike the /bin directory, the /sbin directory **contains binary executable   and command line tools that are preserved for the root user**. These are privileged commands used for system administration tasks. Examples of such commands include fdisk, route, reboot, mkfs, init, and fsck to mention a few.
- Tmp 
 - usr
	 As your link already said, `/usr` is a place for _system-wide_, _read-only_ files. So all your installed software goes there. Information about user. 
- 

** The default path for execute command is in **bin** o **sbin**.
