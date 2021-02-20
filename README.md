# Articles-Library

## Contents

[![alt text](https://img.shields.io/badge/Ref%201.0-Complete%20Procedure%20of%20system%20startup-yellow)](https://github.com/NashoNightmare/Article-Library#ref-10----complete-procedure-of-system-startup)

## Ref 1.0  - Complete Procedure of System Startup

How a unix boot works is that first the firmware/bios/EFI/whatever with a hardcoded instruction finds a special physical place on the drive called the master boot record which is then executed. The master boot record is then either the complete bootloader or in more advanced newer bootloaders brings the bootloader online. The bootloader then executes the kernel, and with "executes" I mean in the traditional sense, it replaces itself with the kernel and stops running. The kernel is called with specific parameters, the most important of these are the **root filesystem** and the path of the **init** executable thereon.

After the the kernel is finished loading it needs a place to start the userland, enter the **init process**, the first process the kernel loads (always assigned process identifier 1, 0 is never assigned. Sometimes people use pid0 to refer to the kernel), the kernel expects this process to keep running indefinitely and if it halts then the kernel quits too. What the init process does is its own business, a fun fact that is often overlooked in terms of security is that pretty much anything can be your init process. You can set /bin/sh as your init in which case your system will not normally be put online, networking and all that crap is off and you simply start a root shell with decent functionality as you load your system.

Now, traditionally, the init process has been responsible for indeed starting all the services but this is not a given. In sysvinit and systemd this still happens, or at least, what starts the services is part of the overall system as one whole. But for intance OpenRC is a service manager, but not an init. Openrc needs an init (a pid1) underneath it, it can't function as a pid1. It starts the services but something, typically sysvinit but not always needs to start it. Running it as init will not work properly for openrc. The init in unix is not just meant to start the system, it's also the final process that ends. OpenRC just ends after it has initialized all services so using it as init would result in a non-clean shutdown afterwards.

### 1.1 System-V init
System V (SysV) is a mature and popular init scheme on Unix-like operating systems, it is the parent of all processes on a Unix/Linux system. SysV is the first commercial Unix operating system designed.

Almost all Linux distributions first used SysV init scheme except Gentoo which has a custom init and Slackware using BSD-style init scheme.

As years have passed by, due to some imperfections, several SysV init replacements have been developed in quests to create more efficient and perfect init systems for Linux.

Although these alternatives seek to improve SysV and probably offer new features, they are still compatible with original SysV init scripts.

### 1.2 SystemD
SystemD is a relatively new init scheme on the Linux platform. Introduced in Fedora 15, its is an assortment of tools for easy system management. The main purpose is to initialize, manage and keep track of all system processes in the boot process and while the system is running.

Systemd init is comprehensively distinct from other traditional Unix init systems, in the way it practically approaches system and services management. It is also compatible with SysV and LBS init scripts.

It has some of the following eminent features:

- Clean, straightforward and efficient design.
- Concurrent and parallel processing at bootup.
- Better APIv.
- Enables removal of optional processes.
- Supports event logging using **journald**
- Supports job cheduling using systemd calendar timers.
- Storage of logs in binary files.
- Preservation of systemd state for future reference.
- Better integration with GNOME plus many more.

More info:

- [Systemd Overview](https://fedoraproject.org/wiki/Systemd)
- [Story Behind: Why 'init' needed to be replaced with systemd in linux](https://www.tecmint.com/systemd-replaces-init-in-linux/)

### 1.3 Upstart
Upstart is an event-based init system developed by makers of Ubuntu as a replacement for SysV init system. It starts different system tasks and processes, inspects them while the system is running and stops them during system shut down.

It is a hybrid init system which uses both SysV startup scripts and also Systemd scripts, some of the notable features of Upstart init system include:

- Originally developed for Ubuntu Linux but can run on all other distributions
- Event-based starting and stopping of tasks and services
- Events are generated during starting and stopping tasks and services
- Events can be sent by other system processes
- Communication with init process through D-Bus
- Users can start and stop their own processes
- Re-spawning of services that die abruptly and many more

More info :

- [Upstart Homepage](http://upstart.ubuntu.com/index.html)

### 1.4 OpenRC
OpenRC is a dependency-based init scheme for Unix-like operating systems, it is compatible with SysV init. As much as it brings some improvements to Sys V, you must keep in mind that OpenRC is not an absolute replacement for /sbin/init file.

It offers some illustrious features and these include:

- It can run on other many Linix distros including Gentoo and alaso on BSD
- Supports hardware initiated init scripts
- Supports a single config file
- No per- service configurations supported
- Runs as a daemon
- Parallel services startup and many more

More info :

- [Open RC Homepage](https://wiki.gentoo.org/wiki/OpenRC)

### 1.5 RunIt
runit is also a cross-platform init system that can run on GNU/Linux, Solaris, BSD and Mac OS X and it is an alternative for SysV init, that offers service supervision.

It comes with some benefits and remarkable components not found in SysV init and possibly other init systems in Linux and these include:

- Service suprevision, where each service is associated with a service directory
- Clean process state, It guarantees each process a  clean state
= It has a reliable logging facility
- Fasy system bootup and shutdown
- It is also portable
- Packaging friendly
- Small code size and many more

More info :

- [RunIT Homepage](http://smarden.org/runit/)


