---
title: "Cyber Ninja CTF walkthrought OSINT, qualification"
date : 2025-02-07 04:56:00 +0008
categories : Walkthrought
description : "[EN] OSINT challenges walkthrought Cyber Ninja CTF qualification, Oteria School"
tag : [cyberninja,ctf,osint]
---
![Desktop View](/assets/img/post/oteriaLogo.png)

## K1 : PRINCESS SPARKLE

**Statement**

Security teams apprehended a suspicious individual loitering in the vicinity of the
space center, at times when no one should be there. A preliminary
of his devices revealed a disturbing fact: while his phone and other
other devices are completely devoid of any trace of activity or communication
communication, his laptop contains an intriguing browsing history.
browsing history. During the first hours of his interrogation, under pressure, he
mentioned having recently communicated with his superior, a certain Mr. Hubert,
but without providing any further details.
Your mission: Based on the clues found in his browsing history,
find out how he came into contact with this mysterious superior.

![image](/assets/img/post/k1Site.png)

**Solution**

Looking at the image, a rather suspicious site appears: Fabulous dog 
![image](/assets/img/post/k1Dog.png)
We go on the site then we can find the flag.

**Flag : {fabulous-dogs-paradise.com}**

## K2 : H4ck3r

**Statement**

We need to gather more information about the people behind this
this organization. Find the pseudonym of the person to contact in the event of a
problems.

**Solution**

By analyzing the source code of the page, and in particular that of the contact form
we notice a comment: **<!-- Contact github.com/Sh4d0wD4sch if needed --<**

![image](/assets/img/post/k2Site.png)

**Flag : {Sh4d0wD4sch}**

## K3 : Algorithmes Lyriques

During questioning, the individual mentioned an application with a space-related name, which he would use to communicate with his superiors.
that he would use to communicate with his superiors.
Explore this lead and identify the political figure who could be linked to this
mysterious group.

We now have a github username : Sh4d0wD4sch

Let's take a look at this github account.

![image](/assets/img/post/k3Git.png)

As we can see there is a repo on it.

