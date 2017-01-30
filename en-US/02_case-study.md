Presenting the Case Study {#case-study}
=========================

In the context of this book, you are the system administrator of a
growing small business. The time has come for you to redefine the
information systems master plan for the coming year in collaboration
with your directors. You choose to progressively migrate to Debian, both
for practical and economical reasons. Let's see in more detail what's in
store for you…

We have envisioned this case study to approach all modern information
system services currently used in a medium sized company. After reading
this book, you will have all of the elements necessary to install Debian
on your servers and fly on your own wings. You will also learn how to
efficiently find information in the event of difficulties.

Fast Growing IT Needs {#sect.fast-growing-it-needs}
=====================

Falcot Corp is a manufacturer of high quality audio equipment. The
company is growing strongly, and has two facilities, one in
Saint-Étienne, and another in Montpellier. The former has around 150
employees; it hosts a factory for the manufacturing of speakers, a
design lab, and all administrative office. The Montpellier site is
smaller, with only about 50 workers, and produces amplifiers.

The Falcot Corp company used as an example here is completely fictional.
Any resemblance to an existing company is purely coincidental. Likewise,
some example data throughout this book may be fictional.

The computer system has had difficulty keeping up with the company's
growth, so they are now determined to completely redefine it to meet
various goals established by management:

-   modern, easily scalable infrastructure;

-   reducing cost of software licenses thanks to use of Open Source
    software;

-   installation of an e-commerce website, possibly B2B (business to
    business, i.e. linking of information systems between different
    companies, such as a supplier and its clients);

-   significant improvement in security to better protect trade secrets
    related to new products.

The entire information system will be overhauled with these goals in
mind.

Master Plan {#sect.master-plan}
===========

master plan
migration
With your collaboration, IT management has conducted a slightly more
extensive study, identifying some constraints and defining a plan for
migration to the chosen Open Source system, Debian.

A significant constraint identified is that the accounting department
uses specific software, which only runs on Microsoft Windows. The
laboratory, for its part, uses computer aided design software that runs
on OS X.

![Overview of the Falcot Corp
network](images/case-study.png){width="75%"}

The switch to Debian will be gradual; a small business, with limited
means, cannot reasonably change everything overnight. For starters, the
IT staff must be trained in Debian administration. The servers will then
be converted, starting with the network infrastructure (routers,
firewalls, etc.) followed by the user services (file sharing, Web, SMTP,
etc.). Then the office computers will be gradually migrated to Debian,
for each department to be trained (internally) during the deployment of
the new system.

Why a GNU/Linux Distribution? {#sect.why-gnu-linux}
=============================

GNU/Linux
Linux
Linux, as you already know, is only a kernel. The expressions, “Linux
distribution” and “Linux system” are, thus, incorrect: they are, in
reality, distributions or systems *based on* Linux. These expressions
fail to mention the software that always completes this kernel, among
which are the programs developed by the GNU Project. Dr. Richard
Stallman, founder of this project, insists that the expression
“GNU/Linux” be systematically used, in order to better recognize the
important contributions made by the GNU Project and the principles of
freedom upon which they are founded.

Debian has chosen to follow this recommendation, and, thus, name its
distributions accordingly (thus, the latest stable release is Debian
GNU/Linux 8).

Several factors have dictated this choice. The system administrator, who
was familiar with this distribution, ensured it was listed among the
candidates for the computer system overhaul. Difficult economic
conditions and ferocious competition have limited the budget for this
operation, despite its critical importance for the future of the
company. This is why Open Source solutions were swiftly chosen: several
recent studies indicate they are less expensive than proprietary
solutions while providing equal or better quality of service so long as
qualified personnel are available to run them.

TCO
Total Cost of Ownership
The Total Cost of Ownership is the total of all money expended for the
possession or acquisition of an item, in this case referring to the
operating system. This price includes any possible license fee, costs
for training personnel to work with the new software, replacement of
machines that are too slow, additional repairs, etc. Everything arising
directly from the initial choice is taken into account.

This TCO, which varies according to the criteria chosen in the
assessment thereof, is rarely significant when taken in isolation.
However, it is very interesting to compare TCOs for different options if
they are calculated according to the same rules. This assessment table
is, thus, of paramount importance, and it is easy to manipulate it in
order to draw a predefined conclusion. Thus, the TCO for a single
machine doesn't make sense, since the cost of an administrator is also
reflected in the total number of machines they manage, a number which
obviously depends on the operating system and tools proposed.

Among free operating systems, the IT department looked at the free BSD
systems (OpenBSD, FreeBSD, and NetBSD), GNU Hurd, and Linux
distributions. GNU Hurd, which has not yet released a stable version,
was immediately rejected. The choice is simpler between BSD and Linux.
The former have many merits, especially on servers. Pragmatism, however,
led to choosing a Linux system, since its installed base and popularity
are both very significant and have many positive consequences. One of
these consequences is that it is easier to find qualified personnel to
administer Linux machines than technicians experienced with BSD.
Furthermore, Linux adapts to newer hardware faster than BSD (although
they are often neck and neck in this race). Finally, Linux distributions
are often more adapted to user-friendly graphical user interfaces,
indispensable for beginners during migration of all office machines to a
new system.

kFreeBSD
FreeBSD
BSD
Since Debian *Squeeze*, it is possible to use Debian with a FreeBSD
kernel on 32 and 64 bit computers; this is what the `kfreebsd-i386` and
`kfreebsd-amd64` architectures mean. While these architectures are not
“official release architectures”, about 90 % of the software packaged by
Debian is available for them.

These architectures may be an appropriate choice for Falcot Corp
administrators, especially for a firewall (the kernel supports three
different firewalls: IPF, IPFW, PF) or for a NAS (network attached
storage system, for which the ZFS filesystem has been tested and
approved).

Why the Debian Distribution? {#sect.why-debian}
============================

Once the Linux family has been selected, a more specific option must be
chosen. Again, there are plenty of criteria to consider. The chosen
distribution must be able to operate for several years, since the
migration from one to another would entail additional costs (although
less than if the migration were between two totally different operating
systems, such as Windows or OS X).

Sustainability is, thus, essential, and it must guarantee regular
updates and security patches over several years. The timing of updates
is also significant, since, with so many machines to manage, Falcot Corp
can not handle this complex operation too frequently. The IT department,
therefore, insists on running the latest stable version of the
distribution, benefiting from the best technical assistance, and
guaranteed security patches. In effect, security updates are generally
only guaranteed for a limited duration on older versions of a
distribution.

Finally, for reasons of homogeneity and ease of administration, the same
distribution must run on all the servers (some of which are Sparc
machines, currently running Solaris) and office computers.

Commercial and Community Driven Distributions
---------------------------------------------

There are two main categories of Linux distributions: commercial and
community driven. The former, developed by companies, are sold with
commercial support services. The latter are developed according to the
same open development model as the free software of which they are
comprised.

A commercial distribution will have, thus, a tendency to release new
versions more frequently, in order to better market updates and
associated services. Their future is directly connected to the
commercial success of their company, and many have already disappeared
(Caldera Linux, StormLinux, etc.).

A community distribution doesn't follow any schedule but its own. Like
the Linux kernel, new versions are released when they are stable, never
before. Its survival is guaranteed, as long as it has enough individual
developers or third party companies to support it.

distribution
community Linux distribution
distribution
commercial Linux distribution
A comparison of various Linux distributions led to the choice of Debian
for various reasons:

-   It is a community distribution, with development ensured
    independently from any commercial constraints; its objectives are,
    thus, essentially of a technical nature, which seem to favor the
    overall quality of the product.

-   Of all community distributions, it is the most significant from many
    perspectives: in number of contributors, number of software packages
    available, and years of continuous existence. The size of its
    community is an incontestable witness to its continuity.

-   Statistically, new versions are released every 18 to 24 months, and
    they are supported for 5 years, a schedule which is agreeable to
    administrators.

-   A survey of several French service companies specialized in free
    software has shown that all of them provide technical assistance for
    Debian; it is also, for many of them, their chosen distribution,
    internally. This diversity of potential providers is a major asset
    for Falcot Corp's independence.

-   Finally, Debian is available on a multitude of architectures,
    including ppc64el for OpenPOWER processors; it will, thus, be
    possible to install it on Falcot Corp's latest IBM servers.

The Debian Long Term Support (LTS) project started in 2014 and aims to
provide 5 years of security support to all stable Debian releases. As
LTS is of primary importance to organizations with large deployments,
the project tries to pool resources from Debian-using companies.
[](https://wiki.debian.org/LTS)

Falcot Corp is not big enough to let one member of its IT staff
contribute to the LTS project, so the company opted to subscribe to
Freexian's Debian LTS contract and provides financial support. Thanks to
this, the Falcot administrators know that the packages they use will be
handled in priority and they have a direct contact with the LTS team in
case of problems. [](https://wiki.debian.org/LTS/Funding)
[](http://www.freexian.com/services/debian-lts.html)

Once Debian has been chosen, the matter of which version to use must be
decided. Let us see why the administrators have picked Debian Jessie.

Why Debian Jessie? {#sect.why-debian-stable}
==================

Every Debian release starts its life as a continuously changing
distribution, also known as “*Testing*”. But at the time we write those
lines, Debian Jessie is the latest “*Stable*” version of Debian.

The choice of Debian Jessie is well justified based on the fact that any
administrator concerned about the quality of their servers will
naturally gravitate towards the stable version of Debian. Even if the
previous stable release might still be supported for a while, Falcot
administrators aren't considering it because its support period will not
last long enough and because the latest version brings new interesting
features that they care about.
