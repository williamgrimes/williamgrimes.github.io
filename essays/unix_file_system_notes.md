---
layout: essay
type: essay
title: Notes on Unix file system 
date: 2019-09-21
labels:
  - Unix
  - guide
  - notes
---

<em>Notes on Unix file system</em>

## Unix File System
#### / = root
- every single file and directory starts from the root directory
- only root user has write privilege under this directory
- please note that `/root` is root user’s home directory, which is not same as `/`
#### /bin = binary executables
- contains binary executables
- common linux commands you need to use in single-user modes are located here
- commands used by all the users of the system are located here
- for example: `ps`, `ls`, `ping`, `grep`, `cp`
#### /sbin = system binaries
- just like `/bin`, `/sbin` also contains binary executables
- linux commands for sys admin and sys maintenance
- for example: `iptables`, `reboot`, `fdisk`, `ifconfig`, `swapon`
#### /etc = configuration files
- contains configuration files required by all programs
- this also contains startup and shutdown shell scripts used to start/stop individual programs
- for example: `/etc/resolv.conf`, `/etc/logrotate.conf`
#### /dev = device files
- contains device files
- these include terminal devices, usb, or any device attached to the system
- for example: `/dev/tty1`, `/dev/usbmon0`
#### /proc = process information
- contains information about system process
- this is a pseudo filesystem contains information about running process. for example: `/proc/{pid}` directory contains information about the process with that particular `pid`
- this is a virtual filesystem with text information about system resources. for example: `/proc/uptime`
#### /var - variable files
- var stands for variable files
- content of the files that are expected to grow can be found under this directory
- this includes — system log files (/var/log); packages and database files (/var/lib); emails (/var/mail); print queues (/var/spool); lock files (/var/lock); temp files needed across reboots (/var/tmp);
#### /tmp = temporary files
- directory that contains temporary files created by system and users
- files under this directory are deleted when system is rebooted
#### /usr – user programs
- contains binaries, libraries, documentation, and source-code for second level programs
- `/usr/bin` contains binary files for user programs. if you can’t find a user binary under `gc/bin`gc, look under `gc/usr/bin`. for example: at, `awk`, `cc`, `less`, `scp`
- `/usr/sbin` contains binary files for system administrators. if you can’t find a system binary under `/sbin`, look under `/usr/sbin`. for example: `atd`, `cron`, `sshd`, `useradd`, `userdel`
- `/usr/lib` contains libraries for `/usr/bin` and `/usr/sbin`
- `/usr/local` contains users programs that you install from source. for example, when you install apache from source, it goes under `/usr/local/apache2`
#### /home – home directories
- home directories for all users to store their personal files
- for example: `/home/john`
#### /boot – boot loader files
- contains boot loader related files
- kernel `initrd`, `vmlinux`, `grub` files are located under `/boot`
- for example: `initrd.img-2.6.32-24-generic`, `vmlinuz-2.6.32-24-generic`
#### /lib – system libraries
- contains library files that supports the binaries located under `/bin` and `/sbin`
- library filenames are either `ld*` or `lib*.so.*`
- for example: `ld-2.11.1.so`, `libncurses.so.5.7`
#### /opt – optional add-on applications
- opt stands for optional
- contains add-on applications from individual vendors
- add-on applications should be installed under either `/opt/` or `/opt/ sub-directory`
#### /mnt – mount directory
- temporary mount directory where sysadmins can mount filesystems
#### /media – removable media devices
- temporary mount directory for removable devices
- for examples, `/media/cdrom` for cd-rom; `/media/floppy` for floppy drives; `/media/cdrecorder` for cd writer
#### /srv – service data
- srv stands for service
- contains server specific services related data
- for example, `/srv/cvs` contains cvs related data
