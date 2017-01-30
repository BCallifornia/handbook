Foreword
========

Linux has been garnering strength for a number of years now, and its
growing popularity drives more and more users to make the jump. The
first step on that path is to pick a distribution. This is an important
decision, because each distribution has its own peculiarities, and
future migration costs can be avoided if the right choice is made from
the start.

Linux
kernel
Linux
distribution
distribution
Linux distribution
Strictly speaking, Linux is only a kernel, the core piece of software
which sits between the hardware and the applications.

A “Linux distribution” is a full operating system; it usually includes
the Linux kernel, an installer program, and most importantly
applications and other software required to turn a computer into a tool
that is actually useful.

Debian GNU/Linux is a “generic” Linux distribution that fits most users.
The purpose of this book is to show its many aspects so that you can
make an informed decision when choosing.

Why This Book? {#sect.why-this-book}
==============

distribution
commercial distribution
Most Linux distributions are backed by a for-profit company that
develops them and sells them under some kind of commercial scheme.
Examples include *Ubuntu*, mainly developed by *Canonical Ltd.*; *Red
Hat Enterprise Linux*, by *Red Hat*; and *Suse Linux*, maintained and
made commercially available by *Novell*.

At the other end of the spectrum lie the likes of Debian and the Apache
Software Foundation (which hosts the development for the Apache web
server). Debian is above all a project in the Free Software world,
implemented by volunteers working together through the Internet. While
some of them do work on Debian as part of their paid job in various
companies, the project as a whole is not attached to any company in
particular, nor does any one company have a greater say in the project's
affairs than what purely volunteer contributors have.

Linux has gathered a fair amount of media coverage over the years; it
mostly benefits the distributions supported by a real marketing
department — in other words, company-backed distributions (Ubuntu,
Red Hat, SUSE, and so on). But Debian is far from being a marginal
distribution; multiple studies have shown over the years that it is
widely used both on servers and on desktops. This is particularly true
among webservers where Debian is the leading Linux distribution.
[](http://www.heise.de/open/artikel/Eingesetzte-Produkte-224518.html)
[](http://w3techs.com/blog/entry/debian_ubuntu_extend_the_dominance_in_the_linux_web_server_market_at_the_expense_of_red_hat_centos)

The purpose of this book is to help you discover this distribution. We
hope to share the experience that we have gathered since we joined the
project as developers and contributors in 1998 (Raphaël) and 2000
(Roland). With any luck, our enthusiasm will be communicative, and maybe
you will join us sometime…

The first edition of this book (in 2004) served to fill a gaping hole:
it was the first French-language book that focused exclusively on
Debian. At that time, many other books were written on the topic both
for French-speaking and English-speaking readers. Unfortunately almost
none of them got updated, and over the years the situation slipped back
to one where there were very few good books on Debian. We hope that this
book, which has started a new life with its translation into English
(and several translations from English into various other languages),
will fill this gap and help many users.

Who Is this Book For? {#sect.who-is-this-book-for}
=====================

We tried to make this book useful for many categories of readers. First,
systems administrators (both beginners and experienced) will find
explanations about the installation and deployment of Debian on many
computers. They will also get a glimpse of most of the services
available on Debian, along with matching configuration instructions and
a description of the specifics coming from the distribution.
Understanding the mechanisms involved in Debian's development will
enable them to deal with unforeseen problems, knowing that they can
always find help within the community.

Users of another Linux distribution, or of another Unix variant, will
discover the specifics of Debian, and should become operational very
quickly while benefiting fully from the unique advantages of this
distribution.

Finally, readers who already have some knowledge of Debian and want to
know more about the community behind it should see their expectations
fulfilled. This book should make them much closer to joining us as
contributors.

General Approach {#sect.selected-approach}
================

All of the generic documentation you can find about GNU/Linux also
applies to Debian, since Debian includes most common free software.
However, the distribution brings many enhancements, which is why we
chose to primarily describe the “Debian way” of doing things.

It is interesting to follow the Debian recommendations, but it is even
better to understand their rationale. Therefore, we won't restrict
ourselves to practical explanations only; we will also describe the
project's workings, so as to provide you with comprehensive and
consistent knowledge.

Book Structure {#sect.book-structure}
==============

This book has its origins in French publisher Eyrolles' “Administrator's
Handbook” collection, and keeps the same approach of revolving around a
case study providing both support and illustration for all topics being
addressed.

This book has its own website, which hosts whatever elements that can
make it more useful. In particular, it includes an online version of the
book with clickable links, and possible errata. Feel free to browse it
and to leave us some feedback. We will be happy to read your comments or
support messages. Send them by email to <hertzog@debian.org> (Raphaël)
and <lolando@debian.org> (Roland). [](http://debian-handbook.info/)

**Chapter 1** focuses on a non-technical presentation of the Debian
project and describes its goals and organization. These aspects are
important because they define a general framework that other chapters
will complete with more concrete information.

**Chapters 2 and 3** provide a broad outline of the case study. At this
point, novice readers can take the time to read **appendix B**, where
they will find a short remedial course explaining a number of basic
computing notions, as well as concepts inherent to any Unix system.

To get on with our real subject matter, we will quite naturally start
with the installation process (**chapter 4**); **chapters 5 and 6** will
unveil basic tools that any Debian administrator will use, such as those
of the **APT** family, which is largely responsible for the
distribution's excellent reputation. These chapters are in no way
restricted to professionals, since everyone is their own administrator
at home.

**Chapter 7** will be an important parenthesis; it describes workflows
to efficiently use documentation and to quickly gain an understanding of
problems in order to solve them.

The next chapters will be a more detailed tour of the system, starting
with basic infrastructure and services (**chapters 8 to 10**) and going
progressively up the stack to reach the user applications in **chapter
13**. **Chapter 12** deals with more advanced subjects that will most
directly concern administrators of large sets of computers (including
servers), while **chapter 14** is a brief introduction to the wider
subject of computer security and gives a few keys to avoid most
problems.

**Chapter 15** is for administrators who want to go further and create
their own Debian packages.

package
Debian package
package
binary package
package
source package
source
package
A Debian package is an archive containing all the files required to
install a piece of software. It is generally a file with a `.deb`
extension, and it can be handled with the `dpkg` command. Also called a
*binary package*, it contains files that can be directly used (such as
programs or documentation). On the other hand, a *source package*
contains the source code for the software and the instructions required
for building the binary package.

The present version is already the seventh edition of the book (we
include the first four that were only available in French). This edition
covers version 8 of Debian, code-named *Jessie*. Among the changes,
Debian now sports two new architectures — *arm64* for 64-bit ARM
processors, and *ppc64el* for little-endian 64-bit PowerPC processors
(designed by IBM and licensed to various manufacturers via the OpenPOWER
foundation). On the opposite side, some architectures have been dropped
(*sparc*, *ia64*) due to lack of volunteers to keep up with development
(which itself can be explained by the fact that associated hardware is
getting old and less interesting to work on). Some architectures are
still available (in the *Unstable* distribution) but did not get their
*ready for release* stamp: *hurd-i386*, *kfreebsd-i386*,
*kfreebsd-amd64*. All included packages have obviously been updated,
including the GNOME desktop, which is now in its version 3.14. More
interestingly, there are two new alternative desktops that are
available: [Cinnamon](http://cinnamon.linuxmint.com/) (fork of GNOME's
Shell created by and for Linux Mint) and
[MATE](http://mate-desktop.org/) (continuation of the GNOME 2.x
desktop).

We have added some notes and remarks in sidebars. They have a variety of
roles: they can draw attention to a difficult point, complete a notion
of the case study, define some terms, or serve as reminders. Here is a
list of the most common of these sidebars:

-   BACK TO BASICS: a reminder of some information that is supposed to
    be known;

-   VOCABULARY: defines a technical term, sometimes Debian specific;

-   COMMUNITY: highlights important persons or roles within the project;

-   POLICY: a rule or recommendation from the Debian Policy. This
    document is essential within the project, and describes how to
    package software. The parts of the policy highlighted in this book
    bring direct benefits to users (for example, knowing that the policy
    standardizes the location of documentation and examples makes it
    easy to find them even in a new package).

-   TOOL: presents a relevant tool or service;

-   IN PRACTICE: theory and practice do not always match; these sidebars
    contain advice resulting from our experience. They can also give
    detailed and concrete examples;

-   other more or less frequent sidebars are rather explicit: CULTURE,
    TIP, CAUTION, GOING FURTHER, SECURITY, and so on.

Acknowledgments {#sect.acknowledgments}
===============

A Bit of History
----------------

In 2003, Nat Makarévitch contacted Raphaël because he wanted to publish
a book on Debian in the *Cahier de l'Admin* (Admin's Handbook)
collection that he was managing for Eyrolles, a leading French editor of
technical books. Raphaël immediately accepted to write it. The first
edition came out on 14th October 2004 and was a huge success — it was
sold out barely four months later.

Since then, we have released 6 other editions of the French book, one
for each subsequent Debian release. Roland, who started working on the
book as a proofreader, gradually became its co-author.

While we were obviously satisfied with the book's success, we always
hoped that Eyrolles would convince an international editor to translate
it into English. We had received numerous comments explaining how the
book helped people to get started with Debian, and we were keen to have
the book benefit more people in the same way.

Alas, no English-speaking editor that we contacted was willing to take
the risk of translating and publishing the book. Not put off by this
small setback, we negotiated with our French editor Eyrolles and got
back the necessary rights to translate the book into English and publish
it ourselves. Thanks to a successful crowdfunding campaign, we worked on
the translation between December 2011 and May 2012. The “Debian
Administrator's Handbook” was born and it was published under a
free-software license!

While this was an important milestone, we already knew that the story
would be not be over for us until we could contribute the French book as
an official translation of the English book. This was not possible at
that time because the French book was still distributed commercially
under a non-free license by Eyrolles.

In 2013, the release of Debian 7 gave us a good opportunity to discuss a
new contract with Eyrolles. We convinced them that a license more in
line with the Debian values would contribute to the book's success. That
wasn't an easy deal to make, and we agreed to setup another crowdfunding
campaign to cover some of the costs and reduce the risks involved. The
operation was again a huge success and in July 2013, we added a French
translation to the Debian Administrator's Handbook.

The Birth of the English Book
-----------------------------

We are back in 2011 and we just got the required rights to make an
English translation of our French book. We are looking into ways to make
this happen.

Translating a book of 450 pages is a considerable effort that requires
several months of work. Self-employed people like us had to ensure a
minimum income to mobilize the time necessary to complete the project.
So we set up a crowdfunding campaign on Ulule and asked people to pledge
money towards the project. [](http://www.ulule.com/debian-handbook/)

The campaign had two goals: raising €15,000 for the translation and
completing a €25,000 liberation fund to get the resulting book published
under a free license — that is, a license that fully follows the Debian
Free Software Guidelines.

When the Ulule campaign ended, the first goal had been achieved with
€24,345 raised. The liberation fund was not complete however, with only
€14,935 raised. As initially announced, the liberation campaign
continued independently from Ulule on the book's official website.

While we were busy translating the book, donations towards the
liberation continued to flow in… And in April 2012, the liberation fund
was completed. You can thus benefit from this book under the terms of a
free license.

We would like to thank everybody who contributed to these fundraising
campaigns, either by pledging some money or by passing the word around.
We couldn't have done it without you.

### Supportive Companies and Organizations

We had the pleasure of getting significant contributions from many free
software-friendly companies and organizations. Thank you to [Code
Lutin](http://www.codelutin.com), [École Ouverte
Francophone](http://eof.eu.org), [Evolix](http://www.evolix.fr),
[Fantini Bakery](http://www.fantinibakery.com), [FSF
France](http://fsffrance.org), [Offensive
Security](http://www.offensive-security.com) (the company behind [Kali
Linux](http://www.kali.org)), [Opensides](http://www.opensides.be),
[Proxmox Server Solutions Gmbh](http://www.proxmox.com), SSIELL (Société
Solidaire d'Informatique En Logiciels Libres), and
[Syminet](http://www.syminet.com).

We would also like to thank [OMG! Ubuntu](http://www.omgubuntu.co.uk)
and [April](http://www.april.org) for their help in promoting the
operation.

### Individual Supporters

With over 650 supporters in the initial fundraising, and several hundred
more in the continued liberation campaign, it is thanks to people like
you that this project has been possible. Thank you!

We want to address our special thanks to those who contributed at least
€35 (sometimes much more!) to the liberation fund. We are glad that
there are so many people who share our values about freedom and yet
recognize that we deserved a compensation for the work that we have put
into this project.

So thank you Alain Coron, Alain Thabaud, Alan Milnes, Alastair
Sherringham, Alban Dumerain, Alessio Spadaro, Alex King, Alexandre
Dupas, Ambrose Andrews, Andre Klärner, Andreas Olsson, Andrej Ricnik,
Andrew Alderwick, Anselm Lingnau, Antoine Emerit, Armin F. Gnosa, Avétis
Kazarian, Bdale Garbee, Benoit Barthelet, Bernard Zijlstra, Carles
Guadall Blancafort, Carlos Horowicz — Planisys S.A., Charles Brisset,
Charlie Orford, Chris Sykes, Christian Bayle, Christian Leutloff,
Christian Maier, Christian Perrier, Christophe Drevet, Christophe
Schockaert (R3vLibre), Christopher Allan Webber, Colin Ameigh, Damien
Dubédat, Dan Pettersson, Dave Lozier, David Bercot, David James, David
Schmitt, David Tran Quang Ty, Elizabeth Young, Fabian Rodriguez, Ferenc
Kiraly, Frédéric Perrenot — Intelligence Service 001, Fumihito Yoshida,
Gian-Maria Daffré, Gilles Meier, Giorgio Cittadini, Héctor Orón
Martínez, Henry, Herbert Kaminski, Hideki Yamane, Hoffmann Information
Services GmbH, Holger Burkhardt, Horia Ardelean, Ivo Ugrina, Jan
Dittberner, Jim Salter, Johannes Obermüller, Jonas Bofjäll, Jordi
Fernandez Moledo, Jorg Willekens, Joshua, Kastrolis Imanta, Keisuke
Nakao, Kévin Audebrand, Korbinian Preisler, Kristian Tizzard, Laurent
Bruguière, Laurent Hamel, Leurent Sylvain, Loïc Revest, Luca Scarabello,
Lukas Bai, Marc Singer, Marcelo Nicolas Manso, Marilyne et Thomas, Mark
Janssen — Sig-I/O Automatisering, Mark Sheppard, Mark Symonds, Mathias
Bocquet, Matteo Fulgheri, Michael Schaffner, Michele Baldessari, Mike
Chaberski, Mike Linksvayer, Minh Ha Duong, Moreau Frédéric, Morphium,
Nathael Pajani, Nathan Paul Simons, Nicholas Davidson, Nicola
Chiapolini, Ole-Morten, Olivier Mondoloni, Paolo Innocenti, Pascal Cuoq,
Patrick Camelin, Per Carlson, Philip Bolting, Philippe Gauthier,
Philippe Teuwen, PJ King, Praveen Arimbrathodiyil (j4v4m4n), Ralf
Zimmermann, Ray McCarthy, Rich, Rikard Westman, Robert Kosch, Sander
Scheepens, Sébastien Picard, Stappers, Stavros Giannouris, Steve-David
Marguet, T. Gerigk, Tanguy Ortolo, Thomas Hochstein, Thomas Müller,
Thomas Pierson, Tigran Zakoyan, Tobias Gruetzmacher, Tournier Simon,
Trans-IP Internet Services, Viktor Ekmark, Vincent Demeester, Vincent
van Adrighem, Volker Schlecht, Werner Kuballa, Xavier Neys, and Yazid
Cassam Sulliman.

The Liberation of the French Book
---------------------------------

After the publication of the English book under a free software licence,
we were in a weird situation with a free book which is a translation of
a non-free book (since it was still distributed commercially under a
non-free license by Eyrolles).

We knew that fixing this would require us to convince Eyrolles that a
free license would contribute to the book's success. The opportunity
came to us in 2013 when we had to discuss a new contract to update the
book for Debian 7. Since freeing a book often has a significant impact
on its sales, as a compromise, we agreed to setup a crowdfunding
campaign to offset some of the risks involved and to contribute to the
publication costs of a new edition. The campaign was again hosted on
Ulule: [](http://www.ulule.com/liberation-cahier-admin-debian/)

The target was at €15,000 in 30 days. It took us less than a week to
reach it, and at the end we got a whopping €25,518 from 721 supporters.

We had significant contributions from free software-friendly companies
and organizations. Let us thank the [LinuxFr.org](http://linuxfr.org)
website, [Korben](http://korben.info),
[Addventure](http://www.addventure.fr),
[Eco-Cystèmes](http://www.eco-cystemes.com/), [ELOL
SARL](http://elol.fr), and [Linuvers](http://www.linuvers.com). Many
thanks to LinuxFr and Korben, they considerably helped to spread the
news.

The operation has been a huge success because hundreds of people share
our values of freedom and put their money to back it up! Thank you for
this.

Special thanks to those who opted to give 25€ more than the value of
their reward. Your faith in this project is highly appreciated. Thank
you Adrien Guionie, Adrien Ollier, Adrien Roger, Agileo Automation,
Alban Duval, Alex Viala, Alexandre Dupas, Alexandre Roman, Alexis
Bienvenüe, Anthony Renoux, Aurélien Beaujean, Baptiste Darthenay, Basile
Deplante, Benjamin Cama, Benjamin Guillaume, Benoit Duchene, Benoît
Sibaud, Bornet, Brett Ellis, Brice Sevat, Bruno Le Goff, Bruno Marmier,
Cédric Briner, Cédric Charlet, Cédrik Bernard, Celia Redondo, Cengiz
Ünlü, Charles Flèche, Christian Bayle, Christophe Antoine, Christophe
Bliard, Christophe Carré, Christophe De Saint Leger, Christophe Perrot,
Christophe Robert, Christophe Schockaert, Damien Escoffier, David
Dellier, David Trolle, Davy Hubert, Decio Valeri, Denis Marcq, Denis
Soriano, Didier Hénaux, Dirk Linnerkamp, Edouard Postel, Eric Coquard,
Eric Lemesre, Eric Parthuisot, Eric Vernichon, Érik Le Blanc, Fabian
Culot, Fabien Givors, Florent Bories, Florent Machen, Florestan
Fournier, Florian Dumas, François Ducrocq, Francois Lepoittevin,
François-Régis Vuillemin, Frédéric Boiteux, Frédéric Guélen, Frédéric
Keigler, Frédéric Lietart, Gabriel Moreau, Gian-Maria Daffré, Grégory
Lèche, Grégory Valentin, Guillaume Boulaton, Guillaume Chevillot,
Guillaume Delvit, Guillaume Michon, Hervé Guimbretiere, Iván Alemán,
Jacques Bompas, Jannine Koch, Jean-Baptiste Roulier, Jean-Christophe
Becquet, Jean-François Bilger, Jean-Michel Grare, Jean-Sébastien Lebacq,
Jérôme Ballot, Jerome Pellois, Johan Roussel, Jonathan Gallon, Joris
Dedieu, Julien Gilles, Julien Groselle, Kevin Messer, Laurent
Espitallier, Laurent Fuentes, Le Goût Du Libre, Ludovic Poux, Marc
Gasnot, Marc Verprat, Marc-Henri Primault, Martin Bourdoiseau, Mathieu
Chapounet, Mathieu Emering, Matthieu Joly, Melvyn Leroy, Michel
Casabona, Michel Kapel, Mickael Tonneau, Mikaël Marcaud, Nicolas
Bertaina, Nicolas Bonnet, Nicolas Dandrimont, Nicolas Dick, Nicolas
Hicher, Nicolas Karolak, Nicolas Schont, Olivier Gosset, Olivier
Langella, Patrick Francelle, Patrick Nomblot, Philippe Gaillard,
Philippe Le Naour, Philippe Martin, Philippe Moniez, Philippe Teuwen,
Pierre Brun, Pierre Gambarotto, Pierre-Dominique Perrier, Quentin Fait,
Raphaël Enrici — Root 42, Rémi Vanicat, Rhydwen Volsik, RyXéo SARL,
Samuel Boulier, Sandrine D'hooge, Sébasiten Piguet, Sébastien Bollingh,
Sébastien Kalt, Sébastien Lardière, Sébastien Poher, Sébastien Prosper,
Sébastien Raison, Simon Folco, Société Téïcée, Stéphane Leibovitsch,
Stéphane Paillet, Steve-David Marguet, Sylvain Desveaux, Tamatoa Davio,
Thibault Taillandier, Thibaut Girka, Thibaut Poullain, Thierry Jaouen,
Thomas Etcheverria, Thomas Vidal, Thomas Vincent, Vincent Avez, Vincent
Merlet, Xavier Alt, Xavier Bensemhoun, Xavier Devlamynck, Xavier
Guillot, Xavier Jacquelin, Xavier Neys, Yannick Britis, Yannick Guérin,
and Yves Martin.

Special Thanks to Contributors
------------------------------

This book would not be what it is without the contributions of several
persons who each played an important role during the translation phase
and beyond. We would like to thank Marilyne Brun, who helped us to
translate the sample chapter and who worked with us to define some
common translation rules. She also revised several chapters which were
desperately in need of supplementary work. Thank you to Anthony Baldwin
(of Baldwin Linguas) who translated several chapters for us.

We benefited from the generous help of proofreaders: Daniel Phillips,
Gerold Rupprecht, Gordon Dey, Jacob Owens, and Tom Syroid. They each
reviewed many chapters. Thank you very much!

Then, once the English version was liberated, of course we got plenty of
feedback and suggestions and fixes from the readers, and even more from
the many teams who undertook to translate this book into other
languages. Thanks!

We would also like to thank the readers of the French book who provided
us some nice quotes to confirm that the book was really worth being
translated: thank you Christian Perrier, David Bercot, Étienne Liétart,
and Gilles Roussi. Stefano Zacchiroli — who was Debian Project Leader
during the crowdfunding campaign — also deserves a big thank you, he
kindly endorsed the project with a quote explaining that free (as in
freedom) books were more than needed.

If you have the pleasure to read these lines in a paperback copy of the
book, then you should join us to thank Benoît Guillon, Jean-Côme
Charpentier, and Sébastien Mengin who worked on the interior book
design. Benoît is the upstream author of
[dblatex](http://dblatex.sourceforge.net) — the tool we used to convert
DocBook into LaTeX (and then PDF). Sébastien is the designer who created
this nice book layout and Jean-Côme is the LaTeX expert who implemented
it as a stylesheet usable with dblatex. Thank you guys for all the hard
work!

Finally, thank you to Thierry Stempfel for the nice pictures introducing
each chapter, and thank you to Doru Patrascu for the beautiful book
cover.

Thanks to Translators
---------------------

Ever since the book has been freed, many volunteers have been busy
translating it to numerous languages, such as Arabic, Brazilian
Portuguese, German, Italian, Spanish, etc. Discover the full list of
translations on the book's website:
[](http://debian-handbook.info/get/#other)

We would like to thank all the translators and translation reviewers.
Your work is highly appreciated because it brings Debian into the hands
of millions of persons who cannot read English.

Personal Acknowledgments from Raphaël
-------------------------------------

First off, I would like to thank Nat Makarévitch, who offered me the
possibility to write this book and who provided strong guidance during
the year it took to get it done. Thank you also to the fine team at
Eyrolles, and Muriel Shan Sei Fan in particular. She has been very
patient with me and I learned a lot with her.

The period of the Ulule campaigns were very demanding for me but I would
like to thank everybody who helped to make them a success, and in
particular the Ulule team who reacted very quickly to my many requests.
Thank you also to everybody who promoted the operations. I don't have
any exhaustive list (and if I had it would probably be too long) but I
would like to thank a few people who were in touch with me: Joey-Elijah
Sneddon and Benjamin Humphrey of OMG! Ubuntu, Florent Zara of
LinuxFr.org, Manu of Korben.info, Frédéric Couchet of April.org, Jake
Edge of Linux Weekly News, Clement Lefebvre of Linux Mint, Ladislav
Bodnar of Distrowatch, Steve Kemp of Debian-Administration.org,
Christian Pfeiffer Jensen of Debian-News.net, Artem Nosulchik of
LinuxScrew.com, Stephan Ramoin of Gandi.net, Matthew Bloch of
Bytemark.co.uk, the team at Divergence FM, Rikki Kite of Linux New
Media, Jono Bacon, the marketing team at Eyrolles, and numerous others
that I have forgotten (sorry about that).

I would like to address a special thanks to Roland Mas, my co-author. We
have been collaborating on this book since the start and he has always
been up to the challenge. And I must say that completing the Debian
Administrator's Handbook has been a lot of work…

Last but not least, thank you to my wife, Sophie. She has been very
supportive of my work on this book and on Debian in general. There have
been too many days (and nights) when I left her alone with our 2 sons to
make some progress on the book. I am grateful for her support and know
how lucky I am to have her.

Personal Acknowledgments from Roland
------------------------------------

Well, Raphaël preempted most of my “external” thank-yous already. I am
still going to emphasize my personal gratitude to the good folks at
Eyrolles, with whom collaboration has always been pleasant and smooth.
Hopefully the results of their excellent advice hasn't been lost in
translation.

I am extremely grateful to Raphaël for taking on the administrative part
of this English edition. From organizing the funding campaign to the
last details of the book layout, producing a translated book is so much
more than just translating and proofreading, and Raphaël did (or
delegated and supervised) it all. So thanks.

Thanks also to all who more or less directly contributed to this book,
by providing clarifications or explanations, or translating advice. They
are too many to mention, but most of them can usually be found on
various \#debian-\* IRC channels.

There is of course some overlap with the previous set of people, but
specific thanks are still in order for the people who actually do
Debian. There wouldn't be much of a book without them, and I am still
amazed at what the Debian project as a whole produces and makes
available to any and all.

More personal thanks go to my friends and my clients, for their
understanding when I was less responsive because I was working on this
book, and also for their constant support, encouragement and egging on.
You know who you are; thanks.

And finally; I am sure they would be surprised by being mentioned here,
but I would like to extend my gratitude to Terry Pratchett, Jasper
Fforde, Tom Holt, William Gibson, Neal Stephenson, and of course the
late Douglas Adams. The countless hours I spent enjoying their books are
directly responsible for my being able to take part in translating one
first and writing new parts later.
