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
The repo is called 'etoiles'
![image](/assets/img/post/k3Clone.png)

There is two files creating and supposly creating an IP adress coming from a poeme.
The poeme is not sorted. We have to look for the right poeme on internet then order it.
Once sorted we can execute the file then we get a IP adress '185.143.103.229'
Looking for this IP as a website we can see the name of a certain 'Hubert de La Tour du Pin'
**Flag : {hubert-de-la-tour-du-pin}**

## K4 : Une histoire de détails
We gotta see where this men was mi-december 2024
Looking this name on google we can easly find an LinkedIn acc.
![image](/assets/img/post/k4LinkedIn.png)

There is a video on this website. 

Too long to explain but let's see the flag.

**Flag : {clermont-ferrand}**


## K5 : Une sacrée histoire

There are two other versions of the element that allowed you to discover the previous flag.
Identify them in the order in which they appear.
Reading articles about these famous medals embedded in the ground of the city of Clermont-Ferrand,
we learn that two other illustrious historical figures from the city are represented: Vercingetorix and Urban II.
The flag is a representation of the city's coat of arms.

**Flag : {vercingetorix_urbain-II}**

## K6 : Opsec failure

As we can see the user Shadow only have one repo. We don't have that much information about it.
Except one, he made a commit. 

![image](/assets/img/post/k6repo.png)

Git reveals a lot of information, and if the GitHub account is not
configured to hide it, it appears in the data associated with the
commit.

By adding .patch at the end of the commit, we obtain details information about him.

![image](/assets/img/post/k6patch.png)

It is the first commit 4833adf79f1a87c45b09a6bf8ed4b0b56d4142fb that allows us to
identify the email address used by Sh4d0wD4sch:
thomas.mercier@spacepin-consulting.com

**Flag : {thomas.mercier@spacepin-consulting.com_4833adf79f1a87c45b09a6bf8ed4b0b56d4142fb}**


## K7 : Un écran de fumée

We are looking for a company linked to the public activities of Hubert de La Tour du Pin and Thomas Mercier.

Upon analyzing the website delatourdupin-depute.fr, both Hubert de La Tour du Pin and Thomas Mercier are mentioned.

We recently obtained the email address:
thomas.mercier@spacepin-consulting.com

Technical analysis of this email domain revealed that spacepin-consulting.com was hosted on the same server as delatourdupin-depute.fr — specifically, the IP address 185.143.103.229.

A tool like https://viewdns.info/ can help us to investigate.

![image](/assets/img/post/k7truc.png)

![image](/assets/img/post/k7truc2.png)

But also to obtain the date on which these two domains were last seen in the same
place, January 27, 2025.

**Flag : {spacepin-consulting-sas_2025-01-27}**

## K8 : OPsec failure II

What name is the employee known by on social media? Find their
date of birth.
There are several avenues we can explore. Given that the most popular social network is
Facebook, let's start our search there.
We will use the password recovery form to check whether
the address thomas.mercier@spacepin-consulting.com is associated with a
Facebook account.
After attempting this search, no account is linked to this email address.

![image](/assets/img/post/k8img1.png)

When searching for the username sh4d0wd4sch, we find a Medium account
(https://medium.com/@sh4d0wd4sch ) with an interesting email address
in the bio: sh4d0wd4sch@fabulous-dogs-paradise.com

![image](/assets/img/post/k8img2.png)

![image](/assets/img/post/k8img3.png)


The latter allows us to identify a username: Thomas Mrcr, as well as a profile photo.
By searching for this name directly on the network, we find his account and can retrieve his date of birth.
The third step is to find the user's email address. To do this, we use the following command:
`wget -l -o file.txt -f /path/to/database.json -h 1000 -r 10000 -r 100000 -r 10

![image](/assets/img/post/k8img4.png)

**Flag : {thomas-mrcr_05/09/1990}**

## OVNI dans le nord : I
The person on the right is convinced that he saw a UFO in northern France.
What is his last name? In what year does he think he saw Martians?
In what city?

![image](/assets/img/post/ovni1.png)

Go to the Gaumont archives website (you can find it by clicking on the logo at the
bottom left). Type “martians” into the search bar and you will find this:
https://gparchives.com/index.php?urlaction=doc&rang=1
The description gives us all the details.

**Flag : {dupuis_1965_rouen}**

## OVNI dans le nord : II

On the day of the incident, Marius Dewilde was reading a weekly magazine. His
wife had already gone upstairs to bed with their 3-year-old son, who was fast asleep
.
Outside, his dog was barking incessantly, which alerted Dewilde and allowed him to
see little men and a flying saucer.
He then alerted the gendarmes, then the police.
What is his dog's name? In which city is the police station where Dewilde
was able to speak to the police?

A simple Google search leads us to some clues.
In particular, this very well-documented blog: https://oncle-
dom.fr/paranormal/ovni/confusions/bolides/quarouble/quarouble.htm
The only catch is the name of the police station, because Dewilde first went
to a gendarmerie (in Blanc Misseron), but it was closed.

**Flag : {onnaing}**

## OVNI dans le nord : III

From the moment Dewilde told his story, numerous theories began to be put forward by people with varying degrees of expertise.
In the 18th issue of a magazine discussing conspiracy theories about classified information, a reader wrote a short article with this photo.
What is this reader's username?

![image](/assets/img/post/ovni3.png)

On trouve le numéro 18 de la revue Top Secret
En parcourant le magazine on trouve la photo et le pseudo
http://seclin.tourisme.free.fr/Magazine_Top_Secret_num_18.pdf

**Flag : {mulder}**

## OVNI dans le nord : III

The most far-fetched theories have been put forward about the UFO that Marius believes he saw.
Some believe that the same UFO crashed on an island after passing over northern France.
Which country does the island belong to where the UFO seen in the photo crashed?
The UFO was spotted by Marius, a 25-year-old man from the town of Saint-Jean-de-Luz in the Basque region of France.

![image](/assets/img/post/ovni4.png)

You have to do some research on the various UFOs that have crashed on islands, and
you find that this one crashed on Starbuck Island, which belongs to Kiribati.

**Flag : {kiribati}**
