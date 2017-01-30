Short Remedial Course
=====================

Even though this book primarily targets administrators and
“power-users”, we wouldn't like to exclude motivated beginners. This
appendix will therefore be a crash-course describing the fundamental
concepts involved in handling a Unix computer.

Shell and Basic Commands {#sect.shell-and-basic-commands}
========================

In the Unix world, every administrator has to use the command line
sooner or later; for example, when the system fails to start properly
and only provides a command-line rescue mode. Being able to handle such
an interface, therefore, is a basic survival skill for these
circumstances.

A command-line environment can be run from the graphical desktop, by an
application known as a “terminal”. In GNOME, you can start it from the
“Activities” overview (that you get when you move the mouse in the
top-left corner of the screen) by typing the first letters of the
application name. In KDE, you will find it in the [K &gt; Applications
&gt; System]{.menuchoice} menu.

This section only gives a quick peek at the commands. They all have many
options not described here, so please refer to the abundant
documentation in their respective manual pages.

Browsing the Directory Tree and Managing Files
----------------------------------------------

Once a session is open, the `pwd` command (which stands for *print
working directory*) displays the current location in the filesystem. The
current directory is changed with the `cd
      directory` command (`cd` is for *change directory*). The parent
directory is always called `..` (two dots), whereas the current
directory is also known as `.` (one dot). The `ls` command allows
*listing* the contents of a directory. If no parameters are given, it
operates on the current directory.

    $ pwd
    /home/rhertzog
    $ cd Desktop
    $ pwd
    /home/rhertzog/Desktop
    $ cd .
    $ pwd
    /home/rhertzog/Desktop
    $ cd ..
    $ pwd
    /home/rhertzog
    $ ls
    Desktop    Downloads  Pictures  Templates
    Documents  Music      Public    Videos
          

A new directory can be created with `mkdir
      directory`, and an existing (empty) directory can be removed with
`rmdir
      directory`. The `mv` command allows *moving* and/or renaming files
and directories; *removing* a file is achieved with `rm
      file`.

    $ mkdir test
    $ ls
    Desktop    Downloads  Pictures  Templates  Videos
    Documents  Music      Public    test
    $ mv test new
    $ ls
    Desktop    Downloads  new       Public     Videos
    Documents  Music      Pictures  Templates
    $ rmdir new
    $ ls
    Desktop    Downloads  Pictures  Templates  Videos
    Documents  Music      Public
          

Displaying and Modifying Text Files
-----------------------------------

The `cat file` command (intended to *concatenate* files to the standard
output device) reads a file and displays its contents on the terminal.
If the file is too big to fit on a screen, use a pager such as `less`
(or `more`) to display it page by page.

The `editor` command starts a text editor (such as `vi` or `nano`) and
allows creating, modifying and reading text files. The simplest files
can sometimes be created directly from the command interpreter thanks to
redirection: `echo "text"
      >file` creates a file named file with “text” as its contents.
Adding a line at the end of this file is possible too, with a command
such as `echo "moretext"
      >>file`. Note the `>>` in this example.

Searching for Files and within Files
------------------------------------

The `find directory
      criteria` command looks for files in the hierarchy under directory
according to several criteria. The most commonly used criterion is
`-name name`: that allows looking for a file by its name.

The `grep expression
      files` command searches the contents of the files and extracts the
lines matching the regular expression (see sidebar
[???](#sidebar.regexp)). Adding the `-r` option enables a recursive
search on all files contained in the directory passed as a parameter.
This allows looking for a file when only a part of the contents are
known.

Managing Processes
------------------

The `ps aux` command lists the processes currently running and helps
identifying them by showing their *pid* (process id). Once the *pid* of
a process is known, the `kill
      -signal
      pid` command allows sending it a signal (if the process belongs to
the current user). Several signals exist; most commonly used are `TERM`
(a request to terminate gracefully) and `KILL` (a forced kill).

The command interpreter can also run programs in the background if the
command is followed by a “&”. By using the ampersand, the user resumes
control of the shell immediately even though the command is still
running (hidden from the user; as a background process). The `jobs`
command lists the processes running in the background; running `fg
      %job-number` (for *foreground*) restores a job to the foreground.
When a command is running in the foreground (either because it was
started normally, or brought back to the foreground with `fg`), the
[Control+Z]{.keycombo} key combination pauses the process and resumes
control of the command-line. The process can then be restarted in the
background with `bg
      %job-number` (for *background*).

System Information: Memory, Disk Space, Identity
------------------------------------------------

The `free` command displays information on memory; `df` (*disk free*)
reports on the available disk space on each of the disks mounted in the
filesystem. Its `-h` option (for *human readable*) converts the sizes
into a more legible unit (usually mebibytes or gibibytes). In a similar
fashion, the `free` command supports the `-m` and `-g` options, and
displays its data either in mebibytes or in gibibytes, respectively.

    $ free
                 total       used       free     shared    buffers     cached
    Mem:       1028420    1009624      18796          0      47404     391804
    -/+ buffers/cache:     570416     458004
    Swap:      2771172     404588    2366584
    $ df
    Filesystem           1K-blocks      Used Available Use% Mounted on
    /dev/sda2              9614084   4737916   4387796  52% /
    tmpfs                   514208         0    514208   0% /lib/init/rw
    udev                     10240       100     10140   1% /dev
    tmpfs                   514208    269136    245072  53% /dev/shm
    /dev/sda5             44552904  36315896   7784380  83% /home

The `id` command displays the identity of the user running the session,
along with the list of groups they belong to. Since access to some files
or devices may be limited to group members, checking available group
membership may be useful.

    $ id
    uid=1000(rhertzog) gid=1000(rhertzog) groups=1000(rhertzog),24(cdrom),25(floppy),27(sudo),29(audio),30(dip),44(video),46(plugdev),108(netdev),109(bluetooth),115(scanner)
          

Organization of the Filesystem Hierarchy {#sect.filesystem-hierarchy}
========================================

Filesystem Hierarchy
The Root Directory
------------------

A Debian system is organized along the *Filesystem Hierarchy Standard*
(FHS). This standard defines the purpose of each directory. For
instance, the top-level directories are described as follows:

-   `/bin/`: basic programs;

-   `/boot/`: Linux kernel and other files required for its early boot
    process;

-   `/dev/`: device files;

-   `/etc/`: configuration files;

-   `/home/`: user's personal files;

-   `/lib/`: basic libraries;

-   `/media/*`: mount points for removable devices (CD-ROM, USB keys and
    so on);

-   `/mnt/`: temporary mount point;

-   `/opt/`: extra applications provided by third parties;

-   `/root/`: administrator's (root's) personal files;

-   `/run/`: volatile runtime data that does not persist across reboots
    (not yet included in the FHS);

-   `/sbin/`: system programs;

-   `/srv/`: data used by servers hosted on this system;

-   `/tmp/`: temporary files; this directory is often emptied at boot;

-   `/usr/`: applications; this directory is further subdivided into
    `bin`, `sbin`, `lib` (according to the same logic as in the root
    directory). Furthermore, `/usr/share/` contains
    architecture-independent data. `/usr/local/` is meant to be used by
    the administrator for installing applications manually without
    overwriting files handled by the packaging system (`dpkg`).

-   `/var/`: variable data handled by daemons. This includes log files,
    queues, spools, caches and so on.

-   `/proc/` and `/sys/` are specific to the Linux kernel (and not part
    of the FHS). They are used by the kernel for exporting data to user
    space (see [section\_title](#sect.userspace-presentation) and
    [section\_title](#sect.user-space) for explanations about this
    concept).

The User's Home Directory
-------------------------

The contents of a user's home directory is not standardized, but there
are still a few noteworthy conventions. One is that a user's home
directory is often referred to by a tilde (“\~”). That is useful to know
because command interpreters automatically replace a tilde with the
correct directory (usually `/home/user/`).

Traditionally, application configuration files are often stored directly
under the user's home directory, but their names usually start with a
dot (for instance, the `mutt` email client stores its configuration in
`~/.muttrc`). Note that filenames that start with a dot are hidden by
default; and `ls` only lists them when the `-a` option is used, and
graphical file managers need to be told to display hidden files.

Some programs also use multiple configuration files organized in one
directory (for instance, `~/.ssh/`). Some applications (such as the
Iceweasel web browser) also use their directory to store a cache of
downloaded data. This means that those directories can end up using a
lot of disk space.

These configuration files stored directly in a user's home directory,
often collectively referred to as *dotfiles*, have long proliferated to
the point that these directories can be quite cluttered with them.
Fortunately, an effort led collectively under the FreeDesktop.org
umbrella has resulted in the “XDG Base Directory Specification”, a
convention that aims at cleaning up these files and directory. This
specification states that configuration files should be stored under
`~/.config`, cache files under `~/.cache`, and application data files
under `~/.local` (or subdirectories thereof). This convention is slowly
gaining traction, and several applications (especially graphical ones)
have started following it.

Graphical desktops usually display the contents of the `~/Desktop/`
directory (or whatever the appropriate translation is for systems not
configured in English) on the desktop (ie, what is visible on screen
once all applications are closed or iconized).

Finally, the email system sometimes stores incoming emails into a
`~/Mail/` directory.

Inner Workings of a Computer: the Different Layers Involved {#sect.computer-layers}
===========================================================

A computer is often considered as something rather abstract, and the
externally visible interface is much simpler than its internal
complexity. Such complexity comes in part from the number of pieces
involved. However, these pieces can be viewed in layers, where a layer
only interacts with those immediately above or below.

An end-user can get by without knowing these details… as long as
everything works. When confronting a problem such as, “The internet
doesn't work!”, the first thing to do is to identify in which layer the
problem originates. Is the network card (hardware) working? Is it
recognized by the computer? Does the Linux kernel see it? Are the
network parameters properly configured? All these questions isolate an
appropriate layer and focus on a potential source of the problem.

The Deepest Layer: the Hardware {#sect.hardware}
-------------------------------

IDE
SCSI
Serial ATA
Parallel ATA
ATA
IEEE 1394
Firewire
USB
Let us start with a basic reminder that a computer is, first and
foremost, a set of hardware elements. There is generally a main board
(known as the *motherboard*), with one (or more) processor(s), some RAM,
device controllers, and extension slots for option boards (for other
device controllers). Most noteworthy among these controllers are IDE
(Parallel ATA), SCSI and Serial ATA, for connecting to storage devices
such as hard disks. Other controllers include USB, which is able to host
a great variety of devices (ranging from webcams to thermometers, from
keyboards to home automation systems) and IEEE 1394 (Firewire). These
controllers often allow connecting several devices so the complete
subsystem handled by a controller is therefore usually known as a “bus”.
Option boards include graphics cards (into which monitor screens will be
plugged), sound cards, network interface cards, and so on. Some main
boards are pre-built with these features, and don't need option boards.

Checking that a piece of hardware works can be tricky. On the other
hand, proving that it doesn't work is sometimes quite simple.

A hard disk drive is made of spinning platters and moving magnetic
heads. When a hard disk is powered up, the platter motor makes a
characteristic whir. It also dissipates energy as heat. Consequently, a
hard disk drive that stays cold and silent when powered up is broken.

Network cards often include LEDs displaying the state of the link. If a
cable is plugged in and leads to a working network hub or switch, at
least one LED will be on. If no LED lights up, either the card itself,
the network device, or the cable between them, is faulty. The next step
is therefore testing each component individually.

Some option boards — especially 3D video cards — include cooling
devices, such as heat sinks and/or fans. If the fan does not spin even
though the card is powered up, a plausible explanation is the card
overheated. This also applies to the main processor(s) located on the
main board.

The Starter: the BIOS or UEFI {#sect.bios}
-----------------------------

BIOS
UEFI
Master Boot Record (MBR)
Hardware, on its own, is unable to perform useful tasks without a
corresponding piece of software driving it. Controlling and interacting
with the hardware is the purpose of the operating system and
applications. These, in turn, require functional hardware to run.

This symbiosis between hardware and software does not happen on its own.
When the computer is first powered up, some initial setup is required.
This role is assumed by the BIOS or UEFI, a piece of software embedded
into the main board that runs automatically upon power-up. Its primary
task is searching for software it can hand over control to. Usually, in
the BIOS case, this involves looking for the first hard disk with a boot
sector (also known as the *master boot record* or MBR), loading that
boot sector, and running it. From then on, the BIOS is usually not
involved (until the next boot). In the case of UEFI, the process
involves scanning disks to find a dedicated EFI partition containing
further EFI applications to execute.

Setup
The BIOS/UEFI also contains a piece of software called Setup, designed
to allow configuring aspects of the computer. In particular, it allows
choosing which boot device is preferred (for instance, the floppy disk
or CD-ROM drive), setting the system clock, and so on. Starting Setup
usually involves pressing a key very soon after the computer is powered
on. This key is often Del or Esc, sometimes F2 or F10. Most of the time,
the choice is flashed on screen while booting.

The boot sector (or the EFI partition), in turn, contains another piece
of software, called the bootloader, whose purpose is to find and run an
operating system. Since this bootloader is not embedded in the main
board but loaded from disk, it can be smarter than the BIOS, which
explains why the BIOS does not load the operating system by itself. For
instance, the bootloader (often GRUB on Linux systems) can list the
available operating systems and ask the user to choose one. Usually, a
time-out and default choice is provided. Sometimes the user can also
choose to add parameters to pass to the kernel, and so on. Eventually, a
kernel is found, loaded into memory, and executed.

UEFI
Secure Boot
UEFI is a relatively recent development. Most new computers will support
UEFI booting, but usually they also support BIOS booting alongside for
backwards compatibility with operating systems that are not ready to
exploit UEFI.

This new system gets rid of some of the limitations of BIOS booting:
with the usage of a dedicated partition, the bootloaders no longer need
special tricks to fit in a tiny *master boot record* and then discover
the kernel to boot. Even better, with a suitably built Linux kernel,
UEFI can directly boot the kernel without any intermediary bootloader.
UEFI is also the basic foundation used to deliver *Secure Boot*, a
technology ensuring that you run only software validated by your
operating system vendor.

The BIOS/UEFI is also in charge of detecting and initializing a number
of devices. Obviously, this includes the IDE/SATA devices (usually hard
disk(s) and CD/DVD-ROM drives), but also PCI devices. Detected devices
are often listed on screen during the boot process. If this list goes by
too fast, use the Pause key to freeze it for long enough to read.
Installed PCI devices that don't appear are a bad omen. At worst, the
device is faulty. At best, it is merely incompatible with the current
version of the BIOS or main board. PCI specifications evolve, and old
main boards are not guaranteed to handle newer PCI devices.

The Kernel {#sect.kernel}
----------

Both the BIOS/UEFI and the bootloader only run for a few seconds each;
now we are getting to the first piece of software that runs for a longer
time, the operating system kernel. This kernel assumes the role of a
conductor in an orchestra, and ensures coordination between hardware and
software. This role involves several tasks including: driving hardware,
managing processes, users and permissions, the filesystem, and so on.
The kernel provides a common base to all other programs on the system.

The User Space {#sect.userspace-presentation}
--------------

Although everything that happens outside of the kernel can be lumped
together under “user space”, we can still separate it into software
layers. However, their interactions are more complex than before, and
the classifications may not be as simple. An application commonly uses
libraries, which in turn involve the kernel, but the communications can
also involve other programs, or even many libraries calling each other.

Some Tasks Handled by the Kernel {#sect.kernel-role-and-tasks}
================================

Driving the Hardware {#sect.hardware-drivers}
--------------------

The kernel is, first and foremost, tasked with controlling the hardware
parts, detecting them, switching them on when the computer is powered
on, and so on. It also makes them available to higher-level software
with a simplified programming interface, so applications can take
advantage of devices without having to worry about details such as which
extension slot the option board is plugged into. The programming
interface also provides an abstraction layer; this allows
video-conferencing software, for example, to use a webcam independently
of its make and model. The software can just use the *Video for Linux*
(V4L) interface, and the kernel translates the function calls of this
interface into the actual hardware commands needed by the specific
webcam in use.

`lspci` `lsusb` `lsdev` `lspcmcia` The kernel exports many details about
detected hardware through the `/proc/` and `/sys/` virtual filesystems.
Several tools summarize those details. Among them, `lspci` (in the
*pciutils* package) lists PCI devices, `lsusb` (in the *usbutils*
package) lists USB devices, and `lspcmcia` (in the *pcmciautils*
package) lists PCMCIA cards. These tools are very useful for identifying
the exact model of a device. This identification also allows more
precise searches on the web, which in turn, lead to more relevant
documents.

    $ lspci
    [...]
    00:02.1 Display controller: Intel Corporation Mobile 915GM/GMS/910GML Express Graphics Controller (rev 03)
    00:1c.0 PCI bridge: Intel Corporation 82801FB/FBM/FR/FW/FRW (ICH6 Family) PCI Express Port 1 (rev 03)
    00:1d.0 USB Controller: Intel Corporation 82801FB/FBM/FR/FW/FRW (ICH6 Family) USB UHCI #1 (rev 03)
    [...]
    01:00.0 Ethernet controller: Broadcom Corporation NetXtreme BCM5751 Gigabit Ethernet PCI Express (rev 01)
    02:03.0 Network controller: Intel Corporation PRO/Wireless 2200BG Network Connection (rev 05)
    $ lsusb
    Bus 005 Device 004: ID 413c:a005 Dell Computer Corp.
    Bus 005 Device 008: ID 413c:9001 Dell Computer Corp.
    Bus 005 Device 007: ID 045e:00dd Microsoft Corp.
    Bus 005 Device 006: ID 046d:c03d Logitech, Inc.
    [...]
    Bus 002 Device 004: ID 413c:8103 Dell Computer Corp. Wireless 350 Bluetooth

These programs have a `-v` option, that lists much more detailed (but
usually not necessary) information. Finally, the `lsdev` command (in the
*procinfo* package) lists communication resources used by devices.

Applications often access devices by way of special files created within
`/dev/` (see sidebar [???](#sidebar.special-files)). These are special
files that represent disk drives (for instance, `/dev/hda` and
`/dev/sdc`), partitions (`/dev/hda1` or `/dev/sdc3`), mice
(`/dev/input/mouse0`), keyboards (`/dev/input/event0`), soundcards
(`/dev/snd/*`), serial ports (`/dev/ttyS*`), and so on.

Filesystems {#sect.filesystems}
-----------

filesystem
system, filesystem
Filesystems are one of the most prominent aspects of the kernel. Unix
systems merge all the file stores into a single hierarchy, which allows
users (and applications) to access data simply by knowing its location
within that hierarchy.

The starting point of this hierarchical tree is called the root, `/`.
This directory can contain named subdirectories. For instance, the
`home` subdirectory of `/` is called `/home/`. This subdirectory can, in
turn, contain other subdirectories, and so on. Each directory can also
contain files, where the actual data will be stored. Thus, the
`/home/rmas/Desktop/hello.txt` name refers to a file named `hello.txt`
stored in the `Desktop` subdirectory of the `rmas` subdirectory of the
`home` directory present in the root. The kernel translates between this
naming system and the actual, physical storage on a disk.

Unlike other systems, there is only one such hierarchy, and it can
integrate data from several disks. One of these disks is used as the
root, and the others are “mounted” on directories in the hierarchy (the
Unix command is called `mount`); these other disks are then available
under these “mount points”. This allows storing users' home directories
(traditionally stored within `/home/`) on a second hard disk, which will
contain the `rhertzog` and `rmas` directories. Once the disk is mounted
on `/home/`, these directories become accessible at their usual
locations, and paths such as `/home/rmas/Desktop/hello.txt` keep
working.

mkfs
There are many filesystem formats, corresponding to many ways of
physically storing data on disks. The most widely known are *ext2*,
*ext3* and *ext4*, but others exist. For instance, *vfat* is the system
that was historically used by DOS and Windows operating systems, which
allows using hard disks under Debian as well as under Windows. In any
case, a filesystem must be prepared on a disk before it can be mounted
and this operation is known as “formatting”. Commands such as
`mkfs.ext3` (where `mkfs` stands for *MaKe FileSystem*) handle
formatting. These commands require, as a parameter, a device file
representing the partition to be formatted (for instance, `/dev/sda1`).
This operation is destructive and should only be run once, except if one
deliberately wishes to wipe a filesystem and start afresh.

There are also network filesystems, such as NFS, where data is not
stored on a local disk. Instead, data is transmitted through the network
to a server that stores and retrieves them on demand. The filesystem
abstraction shields users from having to care: files remain accessible
in their usual hierarchical way.

Shared Functions {#sect.shared-functions}
----------------

Since a number of the same functions are used by all software, it makes
sense to centralize them in the kernel. For instance, shared filesystem
handling allows any application to simply open a file by name, without
needing to worry where the file is stored physically. The file can be
stored in several different slices on a hard disk, or split across
several hard disks, or even stored on a remote file server. Shared
communication functions are used by applications to exchange data
independently of the way the data is transported. For instance,
transport could be over any combination of local or wireless networks,
or over a telephone landline.

Managing Processes {#sect.process-management}
------------------

pid
A process is a running instance of a program. This requires memory to
store both the program itself and its operating data. The kernel is in
charge of creating and tracking them. When a program runs, the kernel
first sets aside some memory, then loads the executable code from the
filesystem into it, and then starts the code running. It keeps
information about this process, the most visible of which is an
identification number known as *pid* (*process identifier*).

Unix-like kernels (including Linux), like most other modern operating
systems, are capable of “multi-tasking”. In other words, they allow
running many processes “at the same time”. There is actually only one
running process at any one time, but the kernel cuts time into small
slices and runs each process in turn. Since these time slices are very
short (in the millisecond range), they create the illusion of processes
running in parallel, although they are actually only active during some
time intervals and idle the rest of the time. The kernel's job is to
adjust its scheduling mechanisms to keep that illusion, while maximizing
the global system performance. If the time slices are too long, the
application may not appear as responsive as desired. Too short, and the
system loses time switching tasks too frequently. These decisions can be
tweaked with process priorities. High-priority processes will run for
longer and with more frequent time slices than low-priority processes.

The limitation described above of only one process being able to run at
a time, doesn't always apply. The actual restriction is that there can
only be one running process *per processor core* at a time.
Multi-processor, multi-core or “hyper-threaded” systems allow several
processes to run in parallel. The same time-slicing system is still
used, though, so as to handle cases where there are more active
processes than available processor cores. This is far from unusual: a
basic system, even a mostly idle one, almost always has tens of running
processes.

Of course, the kernel allows running several independent instances of
the same program. But each can only access its own time slices and
memory. Their data thus remain independent.

Rights Management {#sect.permissions}
-----------------

Unix-like systems are also multi-user. They provide a rights management
system that supports separate users and groups; it also allows control
over actions based on permissions. The kernel manages data for each
process, allowing it to control permissions. Most of the time, a process
is identified by the user who started it. That process is only permitted
to take those actions available to its owner. For instance, trying to
open a file requires the kernel to check the process identity against
access permissions (for more details on this particular example, see
[???](#sect.rights-management)).

The User Space {#sect.user-space}
==============

user space
kernel space
“User space” refers to the runtime environment of normal (as opposed to
kernel) processes. This does not necessarily mean these processes are
actually started by users because a standard system normally has several
“daemon” (or background) processes running before the user even opens a
session. Daemon processes are also considered user-space processes.

Process {#sect.process-basics}
-------

init
When the kernel gets past its initialization phase, it starts the very
first process, `init`. Process \#1 alone is very rarely useful by
itself, and Unix-like systems run with many additional processes.

fork
First of all, a process can clone itself (this is known as a *fork*).
The kernel allocates a new (but identical) process memory space, and
another process to use it. At this time, the only difference between
these two processes is their *pid*. The new process is usually called a
child process, and the original process whose *pid* doesn't change, is
called the parent process.

Sometimes, the child process continues to lead its own life
independently from its parent, with its own data copied from the parent
process. In many cases, though, this child process executes another
program. With a few exceptions, its memory is simply replaced by that of
the new program, and execution of this new program begins. This is the
mechanism used by the init process (with process number 1) to start
additional services and execute the whole startup sequence. At some
point, one process among `init`'s offspring starts a graphical interface
for users to log in to (the actual sequence of events is described in
more details in [???](#sect.system-boot)).

When a process finishes the task for which it was started, it
terminates. The kernel then recovers the memory assigned to this
process, and stops giving it slices of running time. The parent process
is told about its child process being terminated, which allows a process
to wait for the completion of a task it delegated to a child process.
This behavior is plainly visible in command-line interpreters (known as
*shells*). When a command is typed into a shell, the prompt only comes
back when the execution of the command is over. Most shells allow for
running the command in the background, it is a simple matter of adding
an `&` to the end of the command. The prompt is displayed again right
away, which can lead to problems if the command needs to display data of
its own.

Daemons {#sect.daemons}
-------

daemon
daemon
A “daemon” is a process started automatically by the boot sequence. It
keeps running (in the background) to perform maintenance tasks or
provide services to other processes. This “background task” is actually
arbitrary, and does not match anything particular from the system's
point of view. They are simply processes, quite similar to other
processes, which run in turn when their time slice comes. The
distinction is only in the human language: a process that runs with no
interaction with a user (in particular, without any graphical interface)
is said to be running “in the background” or “as a daemon”.

Although *daemon* term shares its Greek etymology with *demon*, the
former does not imply diabolical evil, instead, it should be understood
as a kind of helper spirit. This distinction is subtle enough in
English; it is even worse in other languages where the same word is used
for both meanings.

Several such daemons are described in detail in [???](#unix-services).

Inter-Process Communications {#sect.ipc}
----------------------------

IPC
Inter-Process Communications
An isolated process, whether a daemon or an interactive application, is
rarely useful on its own, which is why there are several methods
allowing separate processes to communicate together, either to exchange
data or to control one another. The generic term referring to this is
*inter-process communication*, or IPC for short.

The simplest IPC system is to use files. The process that wishes to send
data writes it into a file (with a name known in advance), while the
recipient only has to open the file and read its contents.

pipe
In the case where you do not wish to store data on disk, you can use a
*pipe*, which is simply an object with two ends; bytes written in one
end are readable at the other. If the ends are controlled by separate
processes, this leads to a simple and convenient inter-process
communication channel. Pipes can be classified into two categories:
named pipes, and anonymous pipes. A named pipe is represented by an
entry on the filesystem (although the transmitted data is not stored
there), so both processes can open it independently if the location of
the named pipe is known beforehand. In cases where the communicating
processes are related (for instance, a parent and its child process),
the parent process can also create an anonymous pipe before forking, and
the child inherits it. Both processes will then be able to exchange data
through the pipe without needing the filesystem.

Let's describe in some detail what happens when a complex command (a
*pipeline*) is run from a shell. We assume we have a `bash` process (the
standard user shell on Debian), with *pid* 4374; into this shell, we
type the command: `ls | sort` .

The shell first interprets the command typed in. In our case, it
understands there are two programs (`ls` and `sort`), with a data stream
flowing from one to the other (denoted by the `|` character, known as
*pipe*). `bash` first creates an unnamed pipe (which initially exists
only within the `bash` process itself).

Then the shell clones itself; this leads to a new `bash` process, with
*pid* \#4521 (*pids* are abstract numbers, and generally have no
particular meaning). Process \#4521 inherits the pipe, which means it is
able to write in its “input” side; `bash` redirects its standard output
stream to this pipe's input. Then it executes (and replaces itself with)
the `ls` program, which lists the contents of the current directory.
Since `ls` writes on its standard output, and this output has previously
been redirected, the results are effectively sent into the pipe.

A similar operation happens for the second command: `bash` clones itself
again, leading to a new `bash` process with pid \#4522. Since it is also
a child process of \#4374, it also inherits the pipe; `bash` then
connects its standard input to the pipe output, then executes (and
replaces itself with) the `sort` command, which sorts its input and
displays the results.

All the pieces of the puzzle are now set up: `ls` reads the current
directory and writes the list of files into the pipe; `sort` reads this
list, sorts it alphabetically, and displays the results. Processes
numbers \#4521 and \#4522 then terminate, and \#4374 (which was waiting
for them during the operation), resumes control and displays the prompt
to allow the user to type in a new command.

Not all inter-process communications are used to move data around,
though. In many situations, the only information that needs to be
transmitted are control messages such as “pause execution” or “resume
execution”. Unix (and Linux) provides a mechanism known as *signals*,
through which a process can simply send a specific signal (chosen from a
predefined list of signals) to another process. The only requirement is
to know the *pid* of the target.

For more complex communications, there are also mechanisms allowing a
process to open access, or share, part of its allocated memory to other
processes. Memory now shared between them can be used to move data
between the processes.

Finally, network connections can also help processes communicate; these
processes can even be running on different computers, possibly thousands
of kilometers apart.

It is quite standard for a typical Unix-like system to make use of all
these mechanisms to various degrees.

Libraries {#sect.libraries}
---------

library (of functions)
Function libraries play a crucial role in a Unix-like operating system.
They are not proper programs, since they cannot be executed on their
own, but collections of code fragments that can be used by standard
programs. Among the common libraries, you can find:

-   the standard C library (*glibc*), which contains basic functions
    such as ones to open files or network connections, and others
    facilitating interactions with the kernel;

-   graphical toolkits, such as Gtk+ and Qt, allowing many programs to
    reuse the graphical objects they provide;

-   the *libpng* library, that allows loading, interpreting and saving
    images in the PNG format.

Thanks to those libraries, applications can reuse existing code.
Application development is simplified since many applications can reuse
the same functions. With libraries often developed by different persons,
the global development of the system is closer to Unix's historical
philosophy.

One of the fundamental concepts that underlies the Unix family of
operating systems is that each tool should only do one thing, and do it
well; applications can then reuse these tools to build more advanced
logic on top. This philosophy can be seen in many incarnations. Shell
scripts may be the best example: they assemble complex sequences of very
simple tools (such as `grep`, `wc`, `sort`, `uniq` and so on). Another
implementation of this philosophy can be seen in code libraries: the
*libpng* library allows reading and writing PNG images, with different
options and in different ways, but it does only that; no question of
including functions that display or edit images.

Moreover, these libraries are often referred to as “shared libraries”,
since the kernel is able to only load them into memory once, even if
several processes use the same library at the same time. This allows
saving memory, when compared with the opposite (hypothetical) situation
where the code for a library would be loaded as many times as there are
processes using it.
