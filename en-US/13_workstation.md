Workstation
===========

Now that server deployments are done, the administrators can focus on
installing the individual workstations and creating a typical
configuration.

Configuring the X11 Server {#sect.x11-server-configuration}
==========================

XFree86
X.org
X11
interface
graphical
The initial configuration for the graphical interface can be awkward at
times; very recent video cards often don't work perfectly with the X.org
version shipped in the Debian stable version.

A brief reminder: X.org is the software component that allows graphical
applications to display windows on screen. It includes a driver that
makes efficient use of the video card. The features offered to the
graphical applications are exported through a standard interface, *X11*
(*Jessie* contains version *X11R7.7*).

X11 is the graphical system most widely used on Unix-like systems (also
available for Windows and Mac OS). Strictly speaking, the term “X11”
only refers to a protocol specification, but it is also used to refer to
the implementation in practice.

X11 had a rough start, but the 1990s saw XFree86 emerge as the reference
implementation because it was free software, portable, and maintained by
a collaborative community. However, the rate of evolution slowed down
near the end when the software only gained new drivers. That situation,
along with a very controversial license change, led to the X.org fork in
2004. This is now the reference implementation, and Debian *Jessie* uses
X.org version 7.7.

Current versions of X.org are able to autodetect the available hardware:
this applies to the video card and the monitor, as well as keyboards and
mice; in fact, it is so convenient that the package no longer even
creates a `/etc/X11/xorg.conf` configuration file. This is all made
possible by features provided by the Linux kernel (in particular for
keyboards and mice), by having each driver list the video cards it
supports, and by using the DDC protocol to fetch monitor
characteristics.

resolution
The keyboard configuration is currently set up in
`/etc/default/keyboard`. This file is used both to configure the text
console and the graphical interface, and it is handled by the
*keyboard-configuration* package. Details on configuring the keyboard
layout are available in [???](#sect.keyboard-config).

The *xserver-xorg-core* package provides a generic X server, as used by
the 7.x versions of X.org. This server is modular and uses a set of
independent drivers to handle the many different kinds of video cards.
Installing *xserver-xorg* ensures that both the server and at least one
video driver are installed.

server
X
xserver-xorg
Note that if the detected video card is not handled by any of the
available drivers, X.org tries using the VESA and fbdev drivers. VESA is
a generic driver that should work everywhere, but with limited
capabilities (fewer available resolutions, no hardware acceleration for
games and visual effects for the desktop, and so on) while fbdev works
on top of the kernel's framebuffer device. The X server writes its
messages to the `/var/log/Xorg.0.log` log file, which is where one would
look to know what driver is currently in use. For example, the following
snippet matches what the `intel` driver outputs when it is loaded:

    (==) Matched intel as autoconfigured driver 0
    (==) Matched modesetting as autoconfigured driver 1
    (==) Matched vesa as autoconfigured driver 2
    (==) Matched fbdev as autoconfigured driver 3
    (==) Assigned the driver to the xf86ConfigLayout
    (II) LoadModule: "intel"
    (II) Loading /usr/lib/xorg/modules/drivers/intel_drv.so

VESA
video card
Some video card makers (most notably nVidia) refuse to publish the
hardware specifications that would be required to implement good free
drivers. They do, however, provide proprietary drivers that allow using
their hardware. This policy is nefarious, because even when the provided
driver exists, it is usually not as polished as it should be; more
importantly, it does not necessarily follow the X.org updates, which may
prevent the latest available driver from loading correctly (or at all).
We cannot condone this behavior, and we recommend you avoid these makers
and favor more cooperative manufacturers.

If you still end up with such a card, you will find the required
packages in the *non-free* section: *nvidia-glx* for nVidia cards, and
*fglrx-driver* for some ATI cards. Both cases require matching kernel
modules. Building these modules can be automated by installing the
packages *nvidia-kernel-dkms* (for nVidia), or *fglrx-modules-dkms* (for
ATI).

The “nouveau” project aims to develop a free software driver for nVidia
cards. As of *Jessie*, its feature set does not match the proprietary
driver. In the developers' defense, we should mention that the required
information can only be gathered by reverse engineering, which makes
things difficult. The free driver for ATI video cards, called “radeon”,
is much better in that regard although it often requires non-free
firmware.

ATI
nVidia
Customizing the Graphical Interface {#sect.customizing-graphical-interface}
===================================

Choosing a Display Manager
--------------------------

manager
display
gdm
kdm
xdm
The graphical interface only provides display space. Running the X
server by itself only leads to an empty screen, which is why most
installations use a *display manager* to display a user authentication
screen and start the graphical desktop once the user has authenticated.
The three most popular display managers in current use are *gdm3*
(*GNOME Display Manager*), *kdm* (*KDE Display Manager*) and *lightdm*
(*Light Display Manager*). Since the Falcot Corp administrators have
opted to use the GNOME desktop environment, they logically picked `gdm3`
as a display manager too. The `/etc/gdm3/daemon.conf` configuration file
has many options (the list can be found in the
`/usr/share/gdm/gdm.schemas` schema file) to control its behaviour while
`/etc/gdm3/greeter.dconf-defaults` contains settings for the greeter
“session” (more than just a login window, it is a limited desktop with
power management and accessibility related tools). Note that some of the
most useful settings for end-users can be tweaked with GNOME's control
center.

Choosing a Window Manager
-------------------------

Since each graphical desktop provides its own window manager, which
window manager you choose is usually influenced by which desktop you
have selected. GNOME uses the `mutter` window manager, KDE uses `kwin`,
and Xfce (which we present later) has `xfwm`. The Unix philosophy always
allows using one's window manager of choice, but following the
recommendations allows an administrator to best take advantage of the
integration efforts led by each project.

metacity
mutter
kwin
manager
window
window manager
The window manager displays the “decorations” around the windows
belonging to the currently running applications, which includes frames
and the title bar. It also allows reducing, restoring, maximizing, and
hiding windows. Most window managers also provide a menu that pops up
when the desktop is clicked in a specific way. This menu provides the
means to close the window manager session, start new applications, and
in some cases, change to another window manager (if installed).

Older computers may, however, have a hard time running heavyweight
graphical desktop environments. In these cases, a lighter configuration
should be used. “Light” (or small footprint) window managers include
WindowMaker (in the *wmaker* package), Afterstep, fvwm, icewm, blackbox,
fluxbox, or openbox. In these cases, the system should be configured so
that the appropriate window manager gets precedence; the standard way is
to change the `x-window-manager` alternative with the command
`update-alternatives --config x-window-manager`.

WindowMaker
Afterstep
Blackbox
Icewm
Fluxbox
Openbox
x-window-manager
alternative
choice
update-alternatives
The Debian policy lists a number of standardized commands able to
perform a particular action. For example, the `x-window-manager` command
invokes a window manager. But Debian does not assign this command to a
fixed window manager. The administrator can choose which manager it
should invoke.

For each window manager, the relevant package therefore registers the
appropriate command as a possible choice for `x-window-manager` along
with an associated priority. Barring explicit configuration by the
administrator, this priority allows picking the best installed window
manager when the generic command is run.

Both the registration of commands and the explicit configuration involve
the `update-alternatives` script. Choosing where a symbolic command
points at is a simple matter of running `update-alternatives --config
    symbolic-command`. The `update-alternatives` script creates (and
maintains) symbolic links in the `/etc/alternatives/` directory, which
in turn references the location of the executable. As time passes,
packages are installed or removed, and/or the administrator makes
explicit changes to the configuration. When a package providing an
alternative is removed, the alternative automatically goes to the next
best choice among the remaining possible commands.

Not all symbolic commands are explicitly listed by the Debian policy;
some Debian package maintainers deliberately chose to use this mechanism
in less straightforward cases where it still brings interesting
flexibility (examples include `x-www-browser`, `www-browser`, `cc`,
`c++`, `awk`, and so on).

x-www-browser
www-browser
cc
c++
awk
Menu Management
---------------

menu
update-menus
Modern desktop environments and many window managers provide menus
listing the available applications for the user. In order to keep menus
up-to-date in relation to the actual set of available applications, each
package usually provides a `.desktop` file in `/usr/share/applications`.
The format of those files has been standardized by FreeDesktop.org:
[](http://standards.freedesktop.org/desktop-entry-spec/latest/)

The applications menus can be further customized by administrators
through system-wide configuration files as described by the “Desktop
Menu Specification”. End-users can also customize the menus with
graphical tools such as *kmenuedit* (in KDE), *alacarte* (in GNOME) or
*menulibre*. [](http://standards.freedesktop.org/menu-spec/latest/)

Historically — way before the FreeDesktop.org standards emerged — Debian
had invented its own menu system where each package provided a generic
description of the desired menu entries in `/usr/share/menu/`. This tool
is still available in Debian (in the *menu* package) but it is only
marginally useful since package maintainers are encouraged to rely on
`.desktop` files instead.

Graphical Desktops {#sect.graphical-desktops}
==================

The free graphical desktop field is dominated by two large software
collections: GNOME and KDE. Both of them are very popular. This is
rather a rare instance in the free software world; the Apache web
server, for instance, has very few peers.

graphical desktop
GNOME
KDE
GTK+
Qt
This diversity is rooted in history. KDE was the first graphical desktop
project, but it chose the Qt graphical toolkit and that choice wasn't
acceptable for a large number of developers. Qt was not free software at
the time, and GNOME was started based on the GTK+ toolkit. Qt has since
become free software, but the projects still evolved in parallel.

GNOME and KDE still work together: under the FreeDesktop.org umbrella,
the projects collaborated in defining standards for interoperability
across applications.

FreeDesktop.org
Choosing “the best” graphical desktop is a sensitive topic which we
prefer to steer clear of. We will merely describe the many possibilities
and give a few pointers for further thoughts. The best choice will be
the one you make after some experimentation.

GNOME {#sect.gnome-desktop}
-----

Debian *Jessie* includes GNOME version 3.14, which can be installed by a
simple `apt-get install gnome` (it can also be installed by selecting
the “Debian desktop environment” task).

gnome
GNOME is noteworthy for its efforts in usability and accessibility.
Design professionals have been involved in writing its standards and
recommendations, which has helped developers to create satisfying
graphical user interfaces. The project also gets encouragement from the
big players of computing, such as Intel, IBM, Oracle, Novell, and of
course, various Linux distributions. Finally, many programming languages
can be used in developing applications interfacing to GNOME.

![The GNOME desktop](images/gnome.png){width="70%"}

For administrators, GNOME seems to be better prepared for massive
deployments. Application configuration is handled through the GSettings
interface and stores its data in the DConf database. The configuration
settings can thus be queried and edited with the `gsettings`, and
`dconf` command-line tools, or by the `dconf-editor` graphical user
interfaces. The administrator can therefore change users' configuration
with a simple script. The GNOME website provides information to guide
administrators who manage GNOME workstations:
[](https://help.gnome.org/admin/)

gsettings
dconf
KDE
---

Debian *Jessie* includes version 4.14 of KDE, which can be installed
with `apt-get install kde-standard`.

KDE has had a rapid evolution based on a very hands-on approach. Its
authors quickly got very good results, which allowed them to grow a
large user-base. These factors contributed to the overall project
quality. KDE is a mature desktop environment with a wide range of
applications.

![The KDE desktop](images/kde.png){width="70%"}

Since the Qt 4.0 release, the last remaining license problem with KDE
has been solved. This version was released under the GPL both for Linux
and Windows (the Windows version was previously released under a
non-free license). Note that KDE applications must be developed using
the C++ language.

Xfce and Others
---------------

Xfce is a simple and lightweight graphical desktop, which is a perfect
match for computers with limited resources. It can be installed with
`apt-get install xfce4`. Like GNOME, Xfce is based on the GTK+ toolkit,
and several components are common across both desktops.

Xfce
Unlike GNOME and KDE, Xfce does not aim to become a vast project. Beyond
the basic components of a modern desktop (file manager, window manager,
session manager, a panel for application launchers and so on), it only
provides a few specific applications: a terminal, a calendar (Orage), an
image viewer, a CD/DVD burning tool, a media player (Parole), sound
volume control and a text editor (mousepad).

![The Xfce desktop](images/xfce.png){width="70%"}

Another desktop environment provided in *Jessie* is LXDE, which focuses
on the “lightweight” aspect. It can be installed with the *lxde*
meta-package.

LXDE
Email {#sect.main-desktop-tools}
=====

email
software
Evolution
---------

Evolution
Installing the *popularity-contest* package enables participation in an
automated survey that informs the Debian project about the most popular
packages. A script is run weekly by `cron` which sends (by HTTP or
email) an anonymized list of the installed packages and the latest
access date for the files they contain. This allows the Debian
maintainers to know which packages are most frequently installed, and of
these, how frequently they are actually used.

popularity-contest
popularity of packages
package
popularity
This information is a great help to the Debian project. It is used to
determine which packages should go on the first installation disks. The
installation data is also an important factor used to decide whether to
remove a package with very few users from the distribution. We heartily
recommend installing the *popularity-contest* package, and participating
in the survey.

The collected data are made public every day.
[](http://popcon.debian.org/)

These statistics can also help users to choose between two packages that
seem otherwise equivalent. Choosing the more popular package is probably
a safer choice.

Evolution is the GNOME email client and can be installed with
`apt-get install evolution`. Evolution is more than a simple email
client: it also provides a calendar, an address book, a task list, and a
memo (free-form note) application. Its email component includes a
powerful message indexing system, and allows for the creation of virtual
folders based on search queries on all archived messages. In other
words, all messages are stored the same way but displayed in a
folder-based organization, each folder containing messages that match a
set of filtering criteria.

![The Evolution email software](images/evolution.png){width="70%"}

An extension to Evolution allows integration with a Microsoft Exchange
email system; the required package is *evolution-ews*.

evolution-ews
KMail
-----

KMail
The KDE email software can be installed with `apt-get
      install kmail`. KMail only handles email, but it belongs to a
software suite called KDE-PIM (for *Personal Information Manager*) that
includes features such as address books, a calendar component, and so
on. KMail has all the features one would expect from an excellent email
client.

![The KMail email software](images/kmail.png){width="70%"}

Thunderbird and Icedove
-----------------------

The *icedove* package provides the Debian version of Thunderbird, the
email client from the Mozilla software suite. For legal reasons detailed
in the sidebar [sidebar\_title](#sidebar.firefox-iceweasel), Debian
*Jessie* contains Icedove, and not Thunderbird, but the only real
differences between them are their names and icons.

Various localization sets are available in *icedove-l10n-*/* packages;
the *enigmail* extension handles message encrypting and signing, but it
is not available in all languages.

![The Icedove email software](images/icedove.png){width="70%"}

Thunderbird, Mozilla
Mozilla
Thunderbird
Web Browsers {#sect.web-browsers}
============

Web browser
browser, Web
Epiphany, the web browser in the GNOME suite, uses the WebKit display
engine developed by Apple for its Safari browser. The relevant package
is *epiphany-browser*.

WebKit
Epiphany
Konqueror, available in the *konqueror* package, is the KDE file
manager, which also functions as a web browser. It uses the KDE-specific
KHTML rendering engine; KHTML is an excellent engine, as witnessed by
the fact that Apple's WebKit is based on KHTML. Konqueror

Users not satisfied by either of the above can use Iceweasel. This
browser, available in the *iceweasel* package, uses the Mozilla
project's Gecko renderer, with a thin and extensible interface on top.
Gecko MozillaFirefox Firefox, Mozilla

![The Iceweasel web browser](images/iceweasel.png){width="70%"}

Iceweasel
Icedove
Many users will no doubt be surprised by the absence of Mozilla Firefox
in the Debian *Jessie* menus. No need to panic: the *iceweasel* package
contains Iceweasel, which is basically Firefox under another name.

The rationale behind this renaming is a result of the usage rules
imposed by the Mozilla Foundation on the Firefox registered trademark:
any software named Firefox must use the official Firefox logo and icons.
However, since these elements are not released under a free license,
Debian cannot distribute them in its *main* section. Rather than moving
the whole browser to *non-free*, the package maintainer chose to use a
different name.

The `firefox` command still exists in the *iceweasel* package, but only
for compatibility with tools that would try to use it.

For similar reasons, the Thunderbird email client was renamed to Icedove
in a similar fashion.

Mozilla
Firefox
Firefox, Mozilla
Netscape Navigator was the standard browser when the web started
reaching the masses, but lost ground when Microsoft bundled Internet
Explorer with Windows and signed contracts with computer manufacturers
which forbade them from pre-installing Netscape Navigator. Faced with
this failure, Netscape (the company) decided to “free” its source code,
by releasing it under a free license, to give it a second life. This was
the beginning of the Mozilla project. After many years of development,
the results are more than satisfying: the Mozilla project brought forth
an HTML rendering engine (called Gecko) that is among the most
standard-compliant. This rendering engine is in particular used by the
Mozilla Firefox browser, which is one of the most successful browsers,
with a fast-growing user base.

Mozilla
Netscape
Last but not least, Debian also contains the *Chromium* web browser
(available in the *chromium-browser* package). This browser is developed
by Google at such a fast pace that maintaining a single version of it
across the whole lifespan of Debian *Jessie* is unlikely to be possible.
Its clear purpose is to make web services more attractive, both by
optimizing the browser for performance and by increasing the user's
security. The free code that powers Chromium is also used by its
proprietary version called Google Chrome.

Development {#sect.development}
===========

Tools for GTK+ on GNOME
-----------------------

Anjuta (in the *anjuta* package) is a development environment optimized
for creating GTK+ applications for GNOME. Glade (in the *glade* package)
is an application designed to create GTK+ graphical interfaces for GNOME
and save them in an XML file. These XML files can then be loaded by the
*libglade* shared library, which can dynamically recreate the saved
interfaces; such a feature can be interesting, for instance for plugins
that require dialogs.

Anjuta
Glade
The scope of Anjuta is to combine, in a modular way, all the features
one would expect from an integrated development environment.

Tools for Qt on KDE
-------------------

The equivalent applications for KDE are KDevelop (in the *kdevelop*
package) for the development environment, and Qt Designer (in the
*qttools5-dev-tools* package) for the design of graphical interfaces for
Qt applications on KDE.

KDevelop
Qt
Designer
Collaborative Work {#sect.collaborative-work}
==================

Collaborative Work
Working in Groups: *groupware*
------------------------------

groupware
Groupware tools tend to be relatively complex to maintain because they
aggregate multiple tools and have requirements that are not always easy
to reconcile in the context of an integrated distribution. Thus there is
a long list of groupware packages that were once available in Debian but
have been dropped for lack of maintainers or incompatibility with other
(newer) software in Debian. This has been the case with PHPGroupware,
eGroupware, and Kolab. [](http://www.phpgroupware.org/)
[](http://www.egroupware.org/) [](http://www.kolab.org/)

PHPGroupware
eGroupware
Kolab
All is not lost though. Many of the features traditionally provided by
“groupware” software are increasingly integrated into “standard”
software. This is reducing the requirement for specific, specialized
groupware software. On the other hand, this usually requires a specific
server. Citadel (in the *citadel-suite* package) and Sogo (in the *sogo*
package) are alternatives that are available in Debian *Jessie*.

Collaborative Work With FusionForge
-----------------------------------

FusionForge
FusionForge is a collaborative development tool with some ancestry in
SourceForge, a hosting service for free software projects. It takes the
same overall approach based on the standard development model for free
software. The software itself has kept evolving after the SourceForge
code went proprietary. Its initial authors, VA Software, decided not to
release any more free versions. The same happened again when the first
fork (GForge) followed the same path. Since various people and
organizations have participated in development, the current FusionForge
also includes features targeting a more traditional approach to
development, as well as projects not purely concerned with software
development.

SourceForge
FusionForge can be seen as an amalgamation of several tools dedicated to
manage, track and coordinate projects. These tools can be roughly
classified into three families:

-   *communication*: web forums, mailing-list manager, and announcement
    system allowing a project to publish news

-   *tracking*: tools to track project progress and schedule tasks, to
    track bugs, feature requests, or any other kind of “ticket”, and to
    run surveys

-   *sharing*: documentation manager to provide a single central point
    for documents related to a project, generic file release manager,
    dedicated website for each project.

Since FusionForge largely targets development projects, it also
integrates many tools such as CVS, Subversion, Git, Bazaar, Darcs,
Mercurial and Arch for source control management (also called
“configuration management” or “version control”). These programs keep a
history of all the revisions of all tracked files (often source code
files), with all the changes they go through, and they can merge
modifications when several developers work simultaneously on the same
part of a project.

Most of these tools can be accessed or even managed through a web
interface, with a fine-grained permission system, and email
notifications for some events.

Office Suites {#sect.office-suites}
=============

office suite
suite, office
Office software has long been seen as lacking in the free software
world. Users require replacements for Microsoft tools such as Word and
Excel, but these are so complex that replacements were hard to develop.
The situation changed when Sun released the StarOffice code under a free
license as OpenOffice, a project which later gave birth to Libre Office,
which is available on Debian. The KDE project also has its own office
suite, called Calligra Suite (previously KOffice), and GNOME, while
never offering a comprehensive office suite, provides AbiWord as a word
processor and Gnumeric as a spreadsheet. The various projects each have
their strengths. For instance, the Gnumeric spreadsheet is better than
OpenOffice.org/Libre Office in some domains, notably the precision of
its calculations. On the word processing front, the Libre Office suite
still leads the way.

OpenOffice.org
StarOffice
Libre Office
GNOME Office
Calligra Suite
Gnumeric
Another important feature for users is the ability to import Microsoft
Office documents. Even though all office suites have this feature, only
the ones in OpenOffice.org and Libre Office are functional enough for
daily use.

OpenOffice.org contributors set up a foundation (*The Document
Foundation*) to foster the project's development. The idea had been
discussed for some time, but the actual trigger was Oracle's acquisition
of Sun. The new ownership made the future of OpenOffice under Oracle
uncertain. Since Oracle declined to join the foundation, the developers
had to give up on the OpenOffice.org name. This office suite is now
known as *Libre Office*, and is available in Debian.

After a period of relative stagnation on OpenOffice.org, Oracle donated
the code and associated rights to the Apache Software Foundation, and
OpenOffice is now an Apache project. This project is not currently
available in Debian.

Word, Microsoft
Excel, Microsoft
Microsoft
Word
Microsoft
Excel
Libre Office and Calligra Suite are available in the *libreoffice* and
*calligra* Debian packages, respectively. Although the *gnome-office*
package was previously used to install a collection of office tools such
as AbiWord and Gnumeric, this package is no longer part of Debian, with
the individual packages now standing on their own.

Language-specific packs for Libre Office are distributed in separate
packages, most notably *libreoffice-l10n-\** and *libreoffice-help-\**.
Some features such as spelling dictionaries, hyphenation patterns and
thesauri are in separate packages, such as *myspell-\**, *hunspell-\**,
*hyphen-\** and *mythes-\**.

Emulating Windows: Wine {#sect.windows-emulation}
=======================

Emulating Windows
Windows, emulation
In spite of all the previously mentioned efforts, there are still a
number of tools without a Linux equivalent, or for which the original
version is absolutely required. This is where Windows emulation systems
come in handy. The most well-known among them is Wine.
[](https://www.winehq.org/)

*CrossOver*, produced by CodeWeavers, is a set of enhancements to Wine
that broadens the available set of emulated features to a point at which
Microsoft Office becomes fully usable. Some of the enhancements are
periodically merged into Wine. [](http://www.codeweavers.com/products/)

CrossOver
CodeWeavers
However, one should keep in mind that it is only a solution among
others, and the problem can also be tackled with a virtual machine or
VNC; both of these solutions are detailed in the sidebars
[sidebar\_title](#sidebar.virtual-machines) and
[sidebar\_title](#sidebar.wts-or-vnc).

Let us start with a reminder: emulation allows executing a program
(developed for a target system) on a different host system. The
emulation software uses the host system, where the application runs, to
imitate the required features of the target system.

Wine
Now let's install the required packages (*ttf-mscorefonts-installer* is
in the contrib section):

    # apt-get install wine ttf-mscorefonts-installer

winecfg
On a 64 bit (amd64) system, if your Windows applications are 32 bit
applications, then you will have to enable multi-arch to be able to
install wine32 from the i386 architecture (see [???](#sect.multi-arch)).

The user then needs to run `winecfg` and configure which (Debian)
locations are mapped to which (Windows) drives. `winecfg` has some sane
defaults and can autodetect some more drives; note that even if you have
a dual-boot system, you should not point the `C:` drive at where the
Windows partition is mounted in Debian, as Wine is likely to overwrite
some of the data on that partition, making Windows unusable. Other
settings can be kept to their default values. To run Windows programs,
you will first need to install them by running their (Windows) installer
under Wine, with a command such as `wine
    .../setup.exe`; once the program is installed, you can run it with
`wine
    .../program.exe`. The exact location of the `program.exe` file
depends on where the `C:` drive is mapped; in many cases, however,
simply running `wine
    program` will work, since the program is usually installed in a
location where Wine will look for it by itself.

In some cases, `winecfg` (which is just a wrapper) might fail. As a
work-around, it is possible to try to run the underlying command
manually: `wine64
          /usr/lib/x86_64-linux-gnu/wine/wine/winecfg.exe.so` or `wine32
          /usr/lib/i386-linux-gnu/wine/wine/winecfg.exe.so`.

Note that you should not rely on Wine (or similar solutions) without
actually testing the particular software: only a real-use test will
determine conclusively whether emulation is fully functional.

An alternative to emulating Microsoft's operating system is to actually
run it in a virtual machine that emulates a full hardware machine. This
allows running any operating system. [???](#advanced-administration)
describes several virtualization systems, most notably Xen and KVM (but
also QEMU, VMWare and Bochs).

Yet another possibility is to remotely run the legacy Windows
applications on a central server with *Windows Terminal Server* and
access the application from Linux machines using *rdesktop*. This is a
Linux client for the RDP protocol (*Remote Desktop Protocol*) that
*Windows NT/2000 Terminal Server* uses to display desktops on remote
machines.

RDP
Remote Desktop Protocol
Windows Terminal Server
The VNC software provides similar features, with the added benefit of
also working with many operating systems. Linux VNC clients and servers
are described in [???](#sect.remote-login).

Real-Time Communications software {#sect.rtc-clients}
=================================

Debian provides a wide range of Real-Time Communications (RTC) client
software. The setup of RTC servers is discussed in
[???](#sect.rtc-services). In SIP terminology, a client application or
device is also referred to as a user agent.

User agent (SIP)
SIP
user agent
Each client application varies in functionality. Some applications are
more convenient for intensive chat users while other applications are
more stable for webcam users. It may be necessary to test several
applications to identify those which are most satisfactory. A user may
finally decide that they need more than one application, for example, an
XMPP application for messaging with customers and an IRC application for
collaboration with some online communities.

To maximize the ability of users to communicate with the wider world, it
is recommended to configure both SIP and XMPP clients or a single client
that supports both protocols.

SIP
XMPP
The default GNOME desktop includes the Empathy communications client.
Empathy can support both SIP and XMPP. It supports instant messaging
(IM), voice and video. The KDE desktop provides KDE Telepathy, a
communications client based on the same underlying Telepathy APIs used
by the GNOME Empathy client.

Empathy
Telepathy
Popular alternatives to Empathy/Telepathy include Ekiga, Jitsi,
Linphone, Psi and Ring (formerly known as SFLphone).

Ekiga
Jitsi
Linphone
Psi
Ring (soft-phone)
SFLphone
Some of these applications can also interact with mobile users using
apps such as Lumicall on Android. [](http://lumicall.org)

Lumicall
The *Real-Time Communications Quick Start Guide* has a chapter dedicated
to client software.
[](http://rtcquickstart.org/guide/multi/useragents.html)

Some RTC clients have significant problems sending voice and video
through firewalls and NAT networks. Users may receive ghost calls (their
phone rings but they don't hear the other person) or they may not be
able to call at all.

The ICE and TURN protocols were developed to resolve these issues.
Operating a TURN server with public IP addresses in each site and using
client software that supports both ICE and TURN gives the best user
experience.

If the client software is only intended for instant messaging, there is
no requirement for ICE or TURN support.

Debian Developers operate a community SIP service at
[rtc.debian.org](https://rtc.debian.org). The community maintains a wiki
with documentation about setting up many of the client applications
packaged in Debian. The wiki articles and screenshots are a useful
resource for anybody setting up a similar service on their own domain.
[](https://wiki.debian.org/UnifiedCommunications/DebianDevelopers/UserGuide)

IRC can also be considered, in addition to SIP and XMPP. IRC is more
oriented around the concept of channels, the name of which starts with a
hash sign `#`. Each channel is usually targeted at a specific topic and
any number of people can join a channel to discuss it (but users can
still have one-to-one private conversations if needed). The IRC protocol
is older, and does not allow end-to-end encryption of the messages; it
is still possible to encrypt the communications between the users and
the server by tunneling the IRC protocol inside SSL.

IRC
Internet Relay Chat
IRC clients are a bit more complex, and they usually provide many
features that are of limited use in a corporate environment. For
instance, channel “operators” are users endowed with the ability to kick
other users from a channel, or even ban them permanently, when the
normal discussion is disrupted.

Since the IRC protocol is very old, many clients are available to cater
for many user groups; examples include XChat and Smuxi (graphical
clients based on GTK+), Irssi (text mode), Erc (integrated to Emacs),
and so on.

Ekiga (formerly GnomeMeeting) is a prominent application for Linux video
conferencing. It is both stable and functional, and is very easily used
on a local network; setting up the service on a global network is much
more complex when the firewalls involved lack explicit support for the
H323 and/or SIP teleconferencing protocols with all their quirks.

video conference
H323
If only one Ekiga client is to run behind the firewall, the
configuration is rather straightforward, and only involves forwarding a
few ports to the dedicated host: TCP port 1720 (listening for incoming
connections), TCP port 5060 (for SIP), TCP ports 30000 to 30010 (for
control of open connections) and UDP ports 5000 to 5100 (for audio and
video data transmission and registration to an H323 proxy).

GnomeMeeting
Ekiga
When several Ekiga clients are to run behind the firewall, complexity
increases notably. An H323 proxy (for instance the *gnugk* package) must
be set up, and its configuration is far from simple.

gnugk
