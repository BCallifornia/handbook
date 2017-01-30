Derivative Distributions
========================

derivative distribution distribution, derivative Many Linux
distributions are derivatives of Debian and reuse Debian's package
management tools. They all have their own interesting properties, and it
is possible one of them will fulfill your needs better than Debian
itself.

Census and Cooperation {#sect.derivative-census}
======================

The Debian project fully acknowledges the importance of derivative
distributions and actively supports collaboration between all involved
parties. This usually involves merging back the improvements initially
developed by derivative distributions so that everyone can benefit and
long-term maintenance work is reduced.

This explains why derivative distributions are invited to become
involved in discussions on the `debian-derivatives@lists.debian.org`
mailing-list, and to participate in the derivative census. This census
aims at collecting information on work happening in a derivative so that
official Debian maintainers can better track the state of their package
in Debian variants.
[](https://wiki.debian.org/DerivativesFrontDesk)[](https://wiki.debian.org/Derivatives/Census)

Let us now briefly describe the most interesting and popular derivative
distributions.

Ubuntu {#sect.ubuntu}
======

Ubuntu
Ubuntu made quite a splash when it came on the Free Software scene, and
for good reason: Canonical Ltd., the company that created this
distribution, started by hiring thirty-odd Debian developers and
publicly stating the far-reaching objective of providing a distribution
for the general public with a new release twice a year. They also
committed to maintaining each version for a year and a half.

These objectives necessarily involve a reduction in scope; Ubuntu
focuses on a smaller number of packages than Debian, and relies
primarily on the GNOME desktop (although an official Ubuntu derivative,
called “Kubuntu”, relies on KDE). Everything is internationalized and
made available in a great many languages.

Kubuntu
So far, Ubuntu has managed to keep this release rhythm. They also
publish *Long Term Support* (LTS) releases, with a 5-year maintenance
promise. As of April 2015, the current LTS version is version 14.04,
nicknamed Utopic Unicorn. The last non-LTS version is version 15.04,
nicknamed Vivid Vervet. Version numbers describe the release date:
15.04, for example, was released in April 2015.

main
restricted
universe
multiverse
Canonical has adjusted multiple times the rules governing the length of
the period during which a given release is maintained. Canonical, as a
company, promises to provide security updates to all the software
available in the `main` and `restricted` sections of the Ubuntu archive,
for 5 years for LTS releases and for 9 months for non-LTS releases.
Everything else (available in the `universe` and `multiverse`) is
maintained on a best-effort basis by volunteers of the MOTU team
(*Masters Of The Universe*). Be prepared to handle security support
yourself if you rely on packages of the latter sections.

Ubuntu has reached a wide audience in the general public. Millions of
users were impressed by its ease of installation, and the work that went
into making the desktop simpler to use.

Ubuntu and Debian used to have a tense relationship; Debian developers
who had placed great hopes in Ubuntu contributing directly to Debian
were disappointed by the difference between the Canonical marketing,
which implied Ubuntu were good citizens in the Free Software world, and
the actual practice where they simply made public the changes they
applied to Debian packages. Things have been getting better over the
years, and Ubuntu has now made it general practice to forward patches to
the most appropriate place (although this only applies to external
software they package and not to the Ubuntu-specific software such as
Mir or Unity). [](http://www.ubuntu.com/)

Linux Mint {#sect.linux-mint}
==========

Linux Mint
Linux Mint is a (partly) community-maintained distribution, supported by
donations and advertisements. Their flagship product is based on Ubuntu,
but they also provide a “Linux Mint Debian Edition” variant that evolves
continuously (as it is based on Debian Testing). In both cases, the
initial installation involves booting a LiveDVD.

The distribution aims at simplifying access to advanced technologies,
and provides specific graphical user interfaces on top of the usual
software. For instance, Linux Mint relies on Cinnamon instead of GNOME
by default (but it also includes MATE as well as KDE and Xfce);
similarly, the package management interface, although based on APT,
provides a specific interface with an evaluation of the risk from each
package update.

Linux Mint includes a large amount of proprietary software to improve
the experience of users who might need those. For example: Adobe Flash
and multimedia codecs. [](http://www.linuxmint.com/)

Knoppix {#sect.knoppix}
=======

LiveCD
Knoppix
bootable CD-ROM
CD-ROM
bootable
The Knoppix distribution barely needs an introduction. It was the first
popular distribution to provide a *LiveCD*; in other words, a bootable
CD-ROM that runs a turn-key Linux system with no requirement for a
hard-disk — any system already installed on the machine will be left
untouched. Automatic detection of available devices allows this
distribution to work in most hardware configurations. The CD-ROM
includes almost 2 GB of (compressed) software, and the DVD-ROM version
has even more.

Combining this CD-ROM to a USB stick allows carrying your files with
you, and to work on any computer without leaving a trace — remember that
the distribution doesn't use the hard-disk at all. Knoppix uses LXDE (a
lightweight graphical desktop) by default, but the DVD version also
includes GNOME and KDE. Many other distributions provide other
combinations of desktops and software. This is, in part, made possible
thanks to the *live-build* Debian package that makes it relatively easy
to create a LiveCD. [](http://live.debian.net/)

live-build
Note that Knoppix also provides an installer: you can first try the
distribution as a LiveCD, then install it on a hard-disk to get better
performance. [](http://www.knopper.net/knoppix/index-en.html)

Aptosid and Siduction {#sect.aptosid}
=====================

Sidux
Aptosid
Siduction
These community-based distributions track the changes in Debian *Sid*
(*Unstable*) — hence their name. The modifications are limited in scope:
the goal is to provide the most recent software and to update drivers
for the most recent hardware, while still allowing users to switch back
to the official Debian distribution at any time. Aptosid was previously
known as Sidux, and Siduction is a more recent fork of Aptosid.
[](http://aptosid.com) [](http://siduction.org)

Grml {#sect.grml}
====

Grml
Grml is a LiveCD with many tools for system administrators, dealing with
installation, deployment, and system rescue. The LiveCD is provided in
two flavors, `full` and `small`, both available for 32-bit and 64-bit
PCs. Obviously, the two flavors differ by the amount of software
included and by the resulting size. [](https://grml.org)

Tails {#sect.tails}
=====

Tails
Tails (The Amnesic Incognito Live System) aims at providing a live
system that preserves anonymity and privacy. It takes great care in not
leaving any trace on the computer it runs on, and uses the Tor network
to connect to the Internet in the most anonymous way possible.
[](https://tails.boum.org)

Kali Linux {#sect.kali}
==========

Kali
penetration testing
forensics
Kali Linux is a Debian-based distribution specialising in penetration
testing (“pentesting” for short). It provides software that helps
auditing the security of an existing network or computer while it is
live, and analyze it after an attack (which is known as “computer
forensics”). [](https://kali.org)

Devuan {#sect.devuan}
======

Devuan
Devuan is a relatively new fork of Debian: it started in 2014 as a
reaction to the decision made by Debian to switch to `systemd` as the
default init system. A group of users attached to `sysv` and opposing
(real or perceived) drawbacks to `systemd` started Devuan with the
objective of maintaining a `systemd`-less system. As of March 2015, they
haven't published any real release: it remains to be seen if the project
will succeed and find its niche, or if the systemd opponents will learn
to accept it. [](https://devuan.org)

Tanglu {#sect.tanglu}
======

Tanglu
Tanglu is another Debian derivative; this one is based on a mix of
Debian *Testing* and *Unstable*, with patches to some packages. Its goal
is to provide a modern desktop-friendly distribution based on fresh
software, without the release constraints of Debian.
[](http://tanglu.org)

DoudouLinux {#sect.doudoulinux}
===========

DoudouLinux
DoudouLinux targets young children (starting from 2 years old). To
achieve this goal, it provides an heavily customized graphical interface
(based on LXDE) and comes with many games and educative applications.
Internet access is filtered to prevent children from visiting
problematic websites. Advertisements are blocked. The goal is that
parents should be free to let their children use their computer once
booted into DoudouLinux. And children should love using DoudouLinux,
just like they enjoy their gaming console.
[](http://www.doudoulinux.org)

Raspbian {#sect.raspbian}
========

Raspbian
Raspberry Pi
Raspbian is a rebuild of Debian optimised for the popular (and
inexpensive) Raspberry Pi family of single-board computers. The hardware
for that platform is more powerful than what the Debian *armel*
architecture can take advantage of, but lacks some features that would
be required for *armhf*; so Raspbian is a kind of intermediary, rebuilt
specifically for that hardware and including patches targeting this
computer only. [](https://raspbian.org)

And Many More {#sect.other-derivatives}
=============

Distrowatch
The Distrowatch website references a huge number of Linux distributions,
many of which are based on Debian. Browsing this site is a great way to
get a sense of the diversity in the Free Software world.
[](http://distrowatch.com)

The search form can help track down a distribution based on its
ancestry. In March 2015, selecting Debian led to 131 active
distributions! [](http://distrowatch.com/search.php)
