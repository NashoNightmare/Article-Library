# Articles-Library

## Contents

[![alt text](https://img.shields.io/badge/Ref%201.0-Complete%20Procedure%20of%20system%20startup-yellow)](https://github.com/NashoNightmare/Article-Library#ref-10----complete-procedure-of-system-startup)

## Ref 1.0  - Complete Procedure of System Startup

How a unix boot works is that first the firmware/bios/EFI/whatever with a hardcoded instruction finds a special physical place on the drive called the master boot record which is then executed. The master boot record is then either the complete bootloader or in more advanced newer bootloaders brings the bootloader online. The bootloader then executes the kernel, and with "executes" I mean in the traditional sense, it replaces itself with the kernel and stops running. The kernel is called with specific parameters, the most important of these are the **root filesystem** and the path of the **init** executable thereon.

After the the kernel is finished loading it needs a place to start the userland, enter the **init process**, the first process the kernel loads (always assigned process identifier 1, 0 is never assigned. Sometimes people use pid0 to refer to the kernel), the kernel expects this process to keep running indefinitely and if it halts then the kernel quits too. What the init process does is its own business, a fun fact that is often overlooked in terms of security is that pretty much anything can be your init process. You can set /bin/sh as your init in which case your system will not normally be put online, networking and all that crap is off and you simply start a root shell with decent functionality as you load your system.

Now, traditionally, the init process has been responsible for indeed starting all the services but this is not a given. In sysvinit and systemd this still happens, or at least, what starts the services is part of the overall system as one whole. But for intance OpenRC is a service manager, but not an init. Openrc needs an init (a pid1) underneath it, it can't function as a pid1. It starts the services but something, typically sysvinit but not always needs to start it. Running it as init will not work properly for openrc. The init in unix is not just meant to start the system, it's also the final process that ends. OpenRC just ends after it has initialized all services so using it as init would result in a non-clean shutdown afterwards.


