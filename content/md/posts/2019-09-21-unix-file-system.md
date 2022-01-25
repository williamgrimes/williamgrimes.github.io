{:title "The Unix Filesystem"
 :layout :post
 :toc true
 :tags  ["unix" "filesystem"]}

The Unix operating system is a multitasking, multiuser operating system that started life under the initiative of Ken Thompson in the late 1960s at AT&T Bell Labs in New Jersey, United States. Researchers at Bell Labs are also credited with developing radio astronomy, the transistor, the laser, the photovoltaic cell, the charge-coupled device (CCD), information theory, and the programming languages B, C, C++, S, SNOBOL, AWK, AMP [[^1]]. Unix has become widely used in many computing systems, including desktop computers, servers, laptops, and mobile devices.

Linux is a UNIX-like clone that was developed independently starting in 1991 by Linus Torvalds and team. The Linux kernel was designed in such a way so that it acts like Unix but from a different code base. This Linux kernel is generally packaged within Linux distributions to form a complete operating system. Unix and Unix-like systems form the backbone of many modern software services due to their robustness, portability, and flexibility. They also have extensive software libraries and features like a hierarchical file system and unified directory structure.

A filesystem is a data structure and a method that an operating system uses to logically store and organise large volumes of data. These data are stored on disk as a continuous stream of bytes, but the operating system accesses these data as discrete files, where a file is an abstract term that refers to a chunk of data that can be thought of as a discrete unit, and accessed by its file name.

The expression "everything is a file" describes the philosophy within Unix systems that each entity within the architecture behaves as a file. Or more accurately, a file descriptor which is abstracted over the virtual file system layer in the kernel [[^2]]. A file descriptor is an identifier to an open file, that so long as the file is open operations can be performed on.

On disk an inode is the physical manifestation of the file-system. This is an index onto a table by which the data can be accessed and contains metadata information for example about the file's permission bits, the creation/modification/access timestamps, the actual file type, and size of the file [[^3]].

# File Systems
---
There is an important distinction between the _filesystem_ and the layer of abstraction in Unix called the _Virtual File System (VFS)_. A VFS is part of the linux kernel that provides a unified abstraction layer used by file systems and user applications. The VFS presents multiple local or network file systems in a common accessible format. Whilst the underlying filesystem describes how the data are arranged on the media, some common filesystems are [[^4]]:

 - **File Allocation Table (FAT)**: is a Windows file system originally developed for floppy disk drives in 1977. Before Windows 2000 FAT filesystems were the default on Windows operating systems. It has some limitations for example: FAT partitions cannot extend beyond 2TB, and FAT partitions need to be defragmented often to maintain reasonable performance.
 - **Extended File Allocation Table (exFAT)**: is a Microsoft file system that is compatible with Windows and Mac (not Unix). exFAT partitions can extend up to large disk sizes of 512 TB, and exFAT partitions should be defragmented often.
 - **New Technology File System (NTFS)**: is a file system that is commonly used with modern Windows systems since Windows XP. Files stored on NTFS partitions can be as large as the partition, and partitions require occasional defragmentation. NTFS partitions can be read from and written to by Windows and Linux systems and, can only be read from by Mac OS X systems (by default).
 - **Hierarchical File System Plus (HFS+)**: is a file system developed by Apple for Mac OS X. Files stored on HFS+ partitions can be as large as the partition. Windows users can read HFS+ but not write. Drivers are available that allow Linux users to read and writer to HFS+ volumes.
 - **Extended Filesystem (ext)**: is a filesystem developed in 1992 for linux systems with the VFS. Ext2 is the oldest iteration of ext and lacks important features like journalling, meaning that in case of power loss whilst writing drive, data may be lost. Ext3 adds features for robustness at the cost of some speed, and ext4 is more modern and faster. The ext4 filesystem is the default on most Linux distributions now.

On top of these file systems that determine how data is accessed on disk the Unix Filesystem Hierarchy Standard (FHS) is a reference describing the conventions used for the layout of a UNIX system. This was first released in 1994 and is now on version is 3.0 released on 3 June 2015.

# Unix File Types
---
The Portable Operating System Interface (POSIX) is a family of standards specified by the Institute of Electrical and Electronics Engineers (IEEE) Computer Society. The objective of these POSIX standards is to increase compatibility between operating systems. This is done through a common standardised application programming interface (API), standard command line shells and utility interfaces.

The `ls` command is an example of a command specified by POSIX that lists files in the current working directory and can specify more information about files with `-l` the long format argument. For example:

``` shell
$ ls -l /user/home
drwxr-xr-x 1 root root 0 Jan 1 1970 home
```
The fields here separated by a space are given as [[^5]]:
1. The **mode-string** `drwxr-xr-x` describes the file type and permissions. In this case `d` for directory. The following 9 characters `rwxr-xr-x` specify the file permissions, read, write, and execute, for user(root), group and others respectively. In this example the user has read-write-execute permission, the group has read-execute permissions, and other users have read-execute permissions. If all three permissions were given to user(root), group and others, the format looks like `rwxrwxrwx`.
2. The **number of links** specifies the number of hard links for that file. In this example, `1` indicates there is only one link to this directory.
3. The **file owner** specifies the owner of the file. In this example, this file is owned by `root`.
4. The **file group** specifies the group that the file belongs to. In this example, this file belongs to `root` group.
5. The **file size** in bytes. In this example, the file size is `0` since it is  a directory.
6. The **last modified date** specifies the date and time of the last modification of the file, in this example the start of Unix time `Jan 1 1970`.
7. The **file name** is the last field in this example, the directory is called `home`.

Unix systems have seven standard file types, as defined by the Portable Operating System Interface (POSIX):
 - regular,
 - directory,
 - symbolic link,
 - FIFO special,
 - block special,
 - character special,
 - and socket.

### Regular file
Regular files show up in `ls -l` with a hyphen `-` in the mode field.

```shell
$ ls -l /etc/passwd
-rw-r--r-- ... /etc/passwd
```

### Directory
The most common special file is the directory, which is indicated by a `d`.

```shell
$ ls -l /
drw-r--r-- ... /
```

### Symbolic link
A symbolic link is a reference to another file, this special file referenced by `l` stores a textual representation of the referenced file's path .

```shell
lrwxrwxrwx ... linkfile -> /home/user/linkedfile
```

### FIFO (named pipe)
Pipes connect the output of one process to the input of another, and are a strong feature of linux for inter-process communication. This is fine if both processes exist in the same parent process space, started by the same user. However there are circumstances when the processes must be executed under different user names and permissions. In this case named pipes are special files that can exist anywhere in the file system. They can be created with the command `mkfifo`, and are marked with a `p`

```shell
prw-rw---- ... pipefile
```

### Socket
A socket is a special file used for inter-process communication, which enables communication between two processes. In addition to sending data, processes can send file descriptors across a Unix domain socket connection. Sockets allow for bidirectional information flow unlike pipes, which are unidirectional. A socket file is marked with an `s`.

```shell
srwxrwxrwx /tmp/.X11-unix/X0
```

### Device file (block, character)
The great exception is network devices, which do not turn up in the file system but are handled separately. Device files are used to apply access rights to the devices and to direct operations on the files as block devices `b` or character `c` devices.

```shell
crw------- ... /dev/null
brw-rw---- ... /dev/sda
```

# Unix Virtual File System Hierarchy
---
In Unix files are arranged within a hierarchical tree with the highest level directory the root (`/`) of the filesystem as the location from which all other files descend.  so that it can more easily be retrieved.

Conventions exist for grouping certain files together, such as programs, system configuration files, and users' home directories. To view documentation for this look at the manual page for the hierarchy: `man hier`. This is a general overview of common locations of files in Unix and their uses [[^6]]:

<pre style='line-height:1;'>
/
├── bin
│   ├── bash
│   ├── cat
│   ├── chmod
│   ├── ср
│   ├── date
│   ├── echo
│   ├── grep
│   ├── gunzip
│   ├── gzip
│   ├── hostnam
│   ├── kill
│   ├── less
│   ├── ln
│   ├── ls
│   ├── mkdir
│   ├── more
│   ├── mount
│   ├── my
│   ├── nano
│   ├── open
│   ├── ping
│   ├── ps
│   ├── pwd
│   ├── rm
│   ├── sh
│   ├── su
│   ├── tar
│   ├── touch
│   ├── umount
│   ├── uname
│   └── ...
├── boot
│   ├── grub
│   ├── initrd.img
│   ├── lost+found
│   ├── vmlinuz
│   └── ...
├── dev
│   ├── null
│   ├── tty1
│   ├── usb
│   └── ...
├── etc
│   ├── ...
│   ├── crontab
│   ├── cups
│   ├── fonts
│   ├── fstab
│   ├── host.conf
│   ├── hostname
│   ├── hosts
│   ├── hosts.allow
│   ├── hosts.deny
│   ├── init
│   ├── issue
│   ├── machine-id
│   ├── mtab
│   ├── nanorc
│   ├── networks
│   ├── passwd
│   ├── profile
│   ├── protocols
│   ├── resolv.conf
│   ├── security
│   ├── shells
│   ├── timezone
│   └── ...
├── home
│   └── username
├── mnt
├── opt
├── proc
├── root
├── sbin
├── usr
│   ├── bin
│   ├── include
│   ├── lib
│   ├── local
│   └── share
└── var
    ├── cache
    ├── lib
    ├── lock
    ├── log
    ├── opt
    ├── spool
    └── tmp
</pre>

# Unix Important Directories
---
Directories have specific purposes and generally hold the same types of files, the following are directories that exist on most major versions of Unix:

- `/` = root
  - every single file and directory starts from the root directory
  - only root user has write privilege under this directory
  - please note that `/root` is root user’s home directory, which is not same as `/`

- `/bin` = binary executables
  - contains binary executables
  - common linux commands you need to use in single-user modes are located here
  - commands used by all the users of the system are located here
  - for example: `ps`, `ls`, `ping`, `grep`, `cp`

- `/sbin` = system binaries
  - just like `/bin`, `/sbin` also contains binary executables
  - linux commands for sys admin and sys maintenance
  - for example: `iptables`, `reboot`, `fdisk`, `ifconfig`, `swapon`

- `/etc` = configuration files
  - contains configuration files required by all programs
  - this also contains startup and shutdown shell scripts used to start/stop individual programs
  - for example: `/etc/resolv.conf`, `/etc/logrotate.conf`

- `/dev` = device files
    - contains device files
    - these include terminal devices, usb, or any device attached to the system
    - for example: `/dev/tty1`, `/dev/usbmon0`

- `/proc` = process information
  - contains information about system process
  - this is a pseudo filesystem contains information about running process. for example: `/proc/{pid}` directory contains information about the process with that particular `pid`
  - this is a virtual filesystem with text information about system resources. for example: `/proc/uptime`

- `/var` - variable files
  - var stands for variable files
  - content of the files that are expected to grow can be found under this directory
  - this includes — system log files (`/var/log`); packages and database files (`/var/lib`); emails (`/var/mail`); print queues (`/var/spool`); lock files (`/var/lock`); temp files needed across reboots (`/var/tmp`);

- `/tmp` = temporary files
  - directory that contains temporary files created by system and users
  - files under this directory are deleted when system is rebooted

- `/usr` – user programs
    - contains binaries, libraries, documentation, and source-code for second level programs
    - `/usr/bin` contains binary files for user programs. if you can’t find a user binary under `gc/bin`gc, look under `gc/usr/bin`. for example: at, `awk`, `cc`, `less`, `scp`
    - `/usr/sbin` contains binary files for system administrators. if you can’t find a system binary under `/sbin`, look under `/usr/sbin`. for example: `atd`, `cron`, `sshd`, `useradd`, `userdel`
    - `/usr/lib` contains libraries for `/usr/bin` and `/usr/sbin`
    - `/usr/local` contains users programs that you install from source. for example, when you install apache from source, it goes under `/usr/local/apache2`

- `/home` – home directories
  - home directories for all users to store their personal files
  - for example: `/home/john`

- `/boot` – boot loader files
  - contains boot loader related files
  - kernel `initrd`, `vmlinux`, `grub` files are located under `/boot`
  - for example: `initrd.img-2.6.32-24-generic`, `vmlinuz-2.6.32-24-generic`

- `/lib` – system libraries
  - contains library files that supports the binaries located under `/bin` and `/sbin`
  - library filenames are either `ld*` or `lib*.so.*`
  - for example: `ld-2.11.1.so`, `libncurses.so.5.7`

- `/opt` – optional add-on applications
    - opt stands for optional
    - contains add-on applications from individual vendors
    - add-on applications should be installed under either `/opt/` or `/opt/ sub-directory`

- `/mnt` – mount directory
  - temporary mount directory where sysadmins can mount filesystems

- `/media` – removable media devices
  - temporary mount directory for removable devices
  - for examples, `/media/cdrom` for cd-rom; `/media/floppy` for floppy drives; `/media/cdrecorder` for cd writer

- `/srv` – service data
  - srv stands for service
  - contains server specific services related data
  - for example, `/srv/cvs` contains cvs related data

# Unix Important Files
---
Given below are some of the most useful and often used linux files that it is worth being aware of [[^7]].

## Dotfiles
These are hidden files typically in a users home directory, often they are used for personal configuration settings. These files will not ordinarily be shown by the `ls` command unless given the `-a` flag as in `ls -a` to specify _all_ files.

These are some useful dotfiles which are available with a bash shell, other dotfiles may exist depending on the installed programs. Often these files end with `rc` like `~/.bashrc` and `~/.vimrc` where the `rc` stands for run commands, to be executed on program launch.

- `~/.bash_history` - file containing a history of the most recent 500 bash commands.
- `~/.bash_logout` - a script that is run by the bash shell when the user logs out of the system.
- `~/.bash_profile` - an initialisation script to setup variables and aliases upon login. When bash is started as the default login shell, it looks for the `~/.bash_profile` file in the user’s home directory; if not found, it looks for `~/.bash_login`.  If there is no `~/.bash_login` file, it then looks for a `~/.profile file`.
- `~/.bashrc` - an initialisation script executed whenever the bash shell is started in some way other than a login shell.
- `~/.login` - the initialisation script that is run whenever a user login occurs.
- `~/.logout` - the script that is automatically run whenever a user logout occurs.
- `~/.profile` - Put default system-wide environment variables in /etc/profile.
- `~/.vimrc` - an initialisation script for the vim text editor.

## System Files
- `/boot/vmlinuz` - the Linux kernel file, file naming conventions may include release information.
- `/dev/fd0` - device file for the first floppy disk drive on the system.
- `/dev/null` - a dummy device which contains nothing.  It is sometimes useful to send output to this device to make it disappear.
- `/etc/bashrc` - contains global initialisation script for bash shell.
- `/etc/crontab` - a parent shell script to run commands periodically, for example hourly, daily, weekly, and monthly scripts.
- `/etc/fstab` - the file system table contains the description of what disk devices are available at what mount points.
- `/etc/group` - contains information regarding security group definitions.
- `/etc/grub.conf`- the grub boot loader configuration file
- `/etc/hosts` - contains host names and their corresponding IP addresses used for name resolution whenever a DNS server is unavailable
- `/etc/hosts.allow` - contains a list of hosts allowed to access services on this computer.
- `/etc/hosts.deny` - contains a list of hosts forbidden to access services on this computer.
- `/etc/issue` - contains the pre-login message.
- `/etc/mtab` - status information for currently mounted devices and partitions.
- `/etc/passwd` - contains information regarding registered system users, with passwords kept in a shadow file for security.
- `/etc/printcap` - holds printer setup information.
- `/etc/profile` - contains global defaults for the bash shell.
- `/etc/resolv.conf` - a list of domain name servers (DNS) used by the local machine.
- `/proc/cpuinfo` - contains CPU related information.
- `/proc/filesystems` - holds information regarding filesystems that are currently in use.
- `/proc/interrupts` - stores the interrupts that are currently being used.
- `/proc/ioports` - a list of the I/O addresses used by devices connected to the server.
- `/proc/meminfo` - contains memory usage information for both physical memory and swap.
- `/proc/modules` lists currently loaded kernel modules.
- `/proc/mounts` - displays currently mounted file systems.
- `/proc/stat` - contains various statistics about the system, such as the number of page faults since the system was last booted.
- `/proc/swaps` - holds swap file utilisation information.
- `/proc/version` -contains Linux version information.
- `/var/log/lastlog` - stores information about the last boot process.
- `/var/log/messages` - contains messages produced by the syslog daemon during the boot process.
- `/var/log/wtmp` - a binary data file holding login time and duration for each user currently on the system.

# Conclusion
---
The Unix philosophy is documented by Doug McIlroy in the Bell System Technical Journal from 1978:

1. Make each program do one thing well. To do a new job, build afresh rather than complicate old programs by adding new "features".
2. Expect the output of every program to become the input to another, as yet unknown, program. Don't clutter output with extraneous information. Avoid stringently columnar or binary input formats. Don't insist on interactive input.
3. Design and build software, even operating systems, to be tried early, ideally within weeks. Don't hesitate to throw away the clumsy parts and rebuild them.
4. Use tools in preference to unskilled help to lighten a programming task, even if you have to detour to build the tools and expect to throw some of them out after you've finished using them.

This philosophy and early design decisions in Unix have created some of the most successful operating systems still used today. Understanding the basic concepts and ideas of Unix is very useful, and the filesystem is integral to this. Learning your way around Unix systems and understanding the basic hierarchy, file permissions, and locations of important directories and files is an investment well worth making.

# References
[^1]: [Wikipedia: Bell Labs](https://en.wikipedia.org/wiki/Bell_Labs)
[^2]: [StackExchange: Unix - Everything is a file?](https://unix.stackexchange.com/a/225542)
[^3]: [StackOverflow: What is the difference between inode number and file descriptor?](https://stackoverflow.com/a/45633752)
[^4]: [Knowledge Base: File Systems Overview](https://kb.wisc.edu/helpdesk/page.php?id=11300)
[^5]: [Wikipedia: Unix file type](https://en.wikipedia.org/wiki/Unix_file_type)
[^6]: [Wikipedia: Unix filesystem](https://en.wikipedia.org/wiki/Unix_filesystem)
[^7]: [Unixmantra: list-of-important-files](http://www.unixmantra.com/2013/08/list-of-important-files-and-directories-linux.html)
