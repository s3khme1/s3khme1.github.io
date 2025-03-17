---
title: "CC & CNI Classifier"
date : 2024-05-26 04:56:00 +0008
categories : Programation
tag : [NSI]
---

**Projet Final**

_Compte rendu écrit au fur et à mesure du développement du projet._

Le projet a commencé par une analyse approfondie de la distance de Levenshtein comme recommandé par mon supérieur hiérarchique.

Malheureusement même en ayant compris comment fonctionnait cette distance, je me suis rendu compte que cette méthode ne serait pas adaptée à ce projet car il serait difficile de créer un modèle type de NIR, CC ou autres séries de chiffres quelconque. De nombreux calculs seraient nécessaires sans vraiment l’être. La distance de LEV serait d’autant plus handicapante si je souhaite faire progresser le projet afin de créer une autocomplétion des numéros n’étant pas complets. Dernièrement, un problème se posera si je dois expliquer la distance de LEV à mes camarades de classe qui sont sûrement pour la majorité fâchés avec les mathématiques. Ayant une meilleure compréhension des réseaux neuronaux et du deep/machine learning dûe à une quête personnelle du savoir, j’ai donc décidé d’utiliser le module tenserflow (contre recommandation de ma hiérarchie).

Cette approche me permet de rendre la tâche moins longue ce qui n'empêche pas de garder un niveau de difficulté élevé. En outre, afin de développer un peu plus, je choisi de coder moi même la génération de NIR et CC afin d’avoir un échantillon nécessaire pour valider le fonctionnement de mon réseau neuronal, mais également de l'entraîner. Avec la manière dont mon réseau sera programmé il sera assez simple si ce n’est vraiment easy peasy de lui apprendre de nouvelles séries de valeurs numériques.

Comme mentionné précédemment, je souhaite faire évoluer le projet en proposant une méthode d’autocomplétion des séries de chiffres. Ce projet s’inspire de la reconnaissance d’animaux par IA. Je me suis basé sur des travaux d’autres personnes qui consistaient à reconnaître différents animaux en fonction de différentes photos. L’avantage du projet duquel je m’inspire, est qu’il est plus que similaire au mien. Prenons comme exemple un chat, qu’il soit photographié d’en haut ou d’en bas, il s’agit d’un chat. De même pour les numéros CC ou NIR. La forme peut différer \[2760774865895 37] / \[1284074865901 48]. Tous les deux sont des numéros de sécurité sociale or il ne prennent pas la même forme. Voici un problème auquel ne faisait pas face la distance de Levenshtein. Je peux donc adapter le raisonnement pour la détection d’animaux au raisonnement pour la détection de séries de chiffres. Certes un projet utilise des images et surement un modèle de réseau de neurones différent mais l’idée reste la même.

Pour l’évolution du projet avec la complétion de SDC (série de chiffre) je pense m’inspirer de quelque chose que nous utilisons au quotidien et que j’utilise actuellement en écrivant ce texte : l’autocomplétion de mots, et dans ce cas plus précisément la correction de mots mal écrits.

Voilà tout pour le cheminement de ce projet. Lançons nous !




**Génération de NIR  :** 

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXdnylGXchwIzSqoMDr7WGzQPqUZJmdrwFDHjebTKAR1SowP9WHfDDYW04SatmgEu5p7wFJfn-i1CM_UdpQAPl1Xknoc1BsT5ZvtZmFlNuPMtk3k1Tz-fN8L2ecls3p1cHizeRQi7BQ026SE2KyghAluAgkY-9f53cUL9zOYpm9n4mJgRoiU?key=vp8mLtB2MzOoxGU8IWZGLA)

(image donnée par l’état) <https://www.service-public.fr/particuliers/vosdroits/F33078>    

J’ai désormais ma référence pour commencer à développer.

Souhaitant des numéros afin de pouvoir entraîner mon réseau de neurones, tous ceux que je générerait seront l’oeuvre du hasard. J’ai fait un faux départ en voulant générer ces numéros sous formes de listes (chose difficile et inutile). Je vais donc générer séparément chacune des différentes parties pour ensuite les .join() même si cela va nécessiter de les mettre en string puis en int().




**Année de naissance, mois  etc…**

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXe-AQH0rnk4WVoak48j3wsU874A2bP2VloPYv4GwhaTGhqjg6hvIR092Axu_XZtO9EfLSip39PijpYjtjjpQ1sYk8yjd_vTH19AengXxXg-nahFIZCriqAIVGDtfscN5wfIRJwJz7Frmjjy4sAScSXjbXvX4EMnOeYL5cO1wfMG060yFxKYBg?key=vp8mLtB2MzOoxGU8IWZGLA)




**Code commune**

La première difficulté qui m’est apparue était de trouver si 999 était le nombre maximum qu’un numéro de commune de l’INSEE pouvait avoir. Or ce n’était pas le cas. J’ai donc téléchargé le fichier de toutes les communes selon l’INSEE : <https://www.insee.fr/fr/information/7766585>

J’ai ensuite cherché sur internet quel département contenait le plus de communes. Il s'agit du Nord Pas de Calais, le 62. J’ai donc scroller dans le fichier de toutes les communes jusqu'à trouver le 62 puis jusqu'à trouver cette ligne : 

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXe0ze6QWVfZZKs5NLSYzERB6sqTIqRdmg-bY3FYbDVIAKhAnmGKehG7Z2kZHxpezHbyKP-QOCJO0NQagU8nMurv3npHnU5ePHgESEddJ-ADJ2T5e3WobELEg73sp3aJkZwGdsoxz8oszJKm2L3tL131-Eav6M1WAnAxxIuC0LbdGy8rzbVIWw?key=vp8mLtB2MzOoxGU8IWZGLA)

Je sais donc désormais que je dois générer de 1 à 909. Ce léger détail a toute son importance, que ce soit pour l'exactitude de la reconnaissance par la suite, ou tout simplement pour ne pas générer des SDC inutiles.

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXcAEIR5J07ww5cQZeirDs3ivFIsdcNvbXl9pfy6tel2EWrD6rW6wda2kk_fMUdTF8U-PPW7oq1yDbzvpdCqERcQtRKZBnWfbgngvfC_8Wt3h1OWo3-_mrAo2gTapazdQov59n6YiIfgKfpMeEhBM83pIrrexMTGhp6ni87ARm1lsGyglwDvyQ?key=vp8mLtB2MzOoxGU8IWZGLA)

**Ordre de naissance**

Ne pouvant savoir comment limiter l'ordre de naissance je me retrouver obligé de générer des valeurs jusqu'à 999 (je me demande si on ne tuerais pas le 1000ème bébé qui naît au même endroit et à la même période pour ne jamais dépasser les 999)

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXfGgdxk9ZQfNIISuiDOyt2U9b1HKfnGDU9ixHqtOwo3wncItSKSoSTQ6a4PHlAQBvhrdWIegFADCBKsG8BIUmVwbTi8tA5_CuXmmkr6zmGmWBcYweLnq65R-WAsW6hR0xRZXWlfW-dvth-Dr_A-8ICSwQShSfr-zy5u5RsgQvUDn6CyXeki?key=vp8mLtB2MzOoxGU8IWZGLA)




**Problème de génération**

Je suis ici confronté à un autre problème. En générant des chiffres de 1 à 10, ils se créent sous la forme 1,2,3 etc… je dois donc transformer en 01,02,03. J’ai donc fait le choix de créer une boucle qui va checker une liste avec toutes les variables. En fonction de quelle est la variable et du chiffre qui est généré, je rajoute un zéro ou deux zéro : 

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXeq0DLR61E9zIBlwMEx9b2rh0tx014SbA4_jDDFKQHGPoaWrUfGitNOMmTn51p-bmWxKxoi137ewWZVMztwhn1HcvqYxbU4zvsRaeQfL-QluS33-xI5d6xRhq2mqJ_7KhpYjQvEoZipxJ833XaBGaPzWSL9RDCs7nq2UiQWeywJM8P73lKNLg?key=vp8mLtB2MzOoxGU8IWZGLA)





**Problème ajout de la clé de contrôle**

Le problème qui se pose pour l’instant est que je me retrouve dans l’incapacité de trouver comment faire ma clé de contrôle car quand j’essaye la méthode que l’on me donne, c’est à dire celle ci dessous…

_Clé NIR = 97 - ( ( Valeur numérique du NIR ) modulo 97 )_

…je ne sais pas pourquoi le résultat n’est jamais celui attendu. Le problème est sûrement que pour savoir si mon algo marche, j’essaye de tester des numéros qui n’existent pas forcément, tel que celui de l’image de NIR tout en haut. Et quand la clé de contrôle est fausse, j’en conclut que mon algo ne marche pas. J’attend donc de rentrer chez moi pour essayer de vrais numéros de carte vitale.

En attendant, continuons en partant du principe que j’ai raison.

**Ajout de la clé de contrôle**

 

Pour ajouter la clé de contrôle, rien de plus simple. J’y ajoute le résultat de mon calcul à la fin : 

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXfGOVh-rWHkoD40fHtnFFCj8EGKw3A0Y1J8CQm8wG8ILDc8gKTPviMrvUfIo_jHmGzh2ct3qj4tHNlZXbMD4IwXrxHwllc7IsRkYYEUGdntolnUVvWjhONa5DAn-DKin1QuLWE8PjEwPzomxz3yIOE538ABQqkRqp9tupdtl_OWR2PqgXVG?key=vp8mLtB2MzOoxGU8IWZGLA)

Le problème d’algorithme était en fait une feinte car quand le même procédé a été appliqué à une plus grand quantité de suite de chiffres, alors les résultats devenaient tout de suite plus cohérent (avant les clés de contrôle tournaient autours des 90 minimum)

 




**Création du fichier training**

Nous allons désormais manipuler les documents afin d’inscrire toutes les NIR dans un fichier CSV et avoir mon fichier de référence pour entraîner mon RN.

Je vais créer le fichier CSV de façon à ce qu’il y ait une catégorie “num” qui correspondra à mes SDC. L’autre catégorie sera simplement “type” et elle servira a mettre une étiquette et dire que toute mes NIR sont des NIR afin que l’IA comprennent le principe et la forme qu’ont globalement les NIR.

Cette étape a sûrement été la plus simple. Pour faire tout cela, j’ai seulement eu besoins d’importer le module csv :

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXcURRRvqMF0B4tzt4dAIm4ZQHxJVGyaNp7K0GXE8yZH5yGTPghwpGXOEkYFbmD8HI2wNDVXyvOt8DI4DyWK_NCgxX95UeyEP7C8qPq1CPbfeDu3ORaa-l5ADa4rx4_Ua8agYW6gmAktsQuM35bnPKrgASoQ1Ddm_1k6kSOPDiZMSKRLhVkm1Q?key=vp8mLtB2MzOoxGU8IWZGLA)

J’ai également dû créer un fichier csv qui pourrait accueillir ces NIR : 

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXdl6MF9ouWizZKximxQ7rHlVnxuWQ5tTQ85Fcc9B_rQEkaHLfdy_JF38Y1U9Ejz8zy6c5gTIqqETxB2ucwjhLh2zA1Dr56d9GyGZk00ziypRmlrYBCLWuH0HzoI8rZqwMYyYFGSpLsYklRIK2KqApaULmrgFRS0KeqZJ1sAN-wmwpc6vFzCmw?key=vp8mLtB2MzOoxGU8IWZGLA)




Il ne me restait plus qu'à ouvrir ce fichier en mode écriture, créer les catégories et les écrires dedans :

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXeAsNBkUUjRrseyJuEGt1tYNcwEUTdQ9b58y9XfsutoiCSS4U3ZakIN4YlYshIAjisVS_9c5YfIFzHRu_2-ZdDb-oUa8sNwtrwPeADCo3tovWjl1jmBZP6qZzEkyesr8px-jgZby5gJIgGmKl22Gs9KYVQEif8cAv6WZwWzI4-u3-Mx4qdG-A?key=vp8mLtB2MzOoxGU8IWZGLA)

Ensuite, à chaque fois que je génère une NIR, elle apparaîtra dans ce fichier  :

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXdoFbCM3XzrzFwP1d-_Io2ByuBJAdC5qFGREhF66TmnE-eM7xqrphO4oBPdNLcn3rSwWp3_6tW6iDxN4_AdM6NtWodbc_CbZ8dxOZx94vsX3fPjgQu6i0wkBs7DbnZbU0c2AAO6gKPt4eN-FQ9WyH4dwmtnbU7Y6BA47JNxt87ldEJRSKXv?key=vp8mLtB2MzOoxGU8IWZGLA)

On voit ici que tout fonctionne bien au niveau de la génération : 

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXeYO3MSlX45eatjc8tzvXs9z2rsPjEEw5MFKS0Zhy13m6T8Jr8mjyzDV89oZ5T8tkA-ZfH2ZNvAkI-XibDuJu0iszzf0FQUYMF3iuTCnQ9RSHGvPjpqSlQtpGHrRzq-A7iAq6AQkd6tZ5wIit500fTwOceAnJS28jso7sMisAHax8-lDCwiZg?key=vp8mLtB2MzOoxGU8IWZGLA)

Voilà tout pour notre génération de NIR, passons à la génération de CC.



**Génération de CC  :** 

Il faut savoir que ce générateur de CC créera uniquement des numéros d’American express. Pourquoi donc ? C’est très simple. Je n’ai pas le choix que de me concentrer sur un seul type de carte bancaire à générer car il serait trop long de faire autrement. De plus, les numéros d’American express ne contiennent que 15 chiffres contrairement aux cartes VISA ou MASTERCARD qui en contiennent en majorité 16. Etant donné que les numéro de NIR sont aussi composés de 15 digit le processus sera donc facilité pour la suite. Les réseaux neuronaux portent une grande importance à la scale des donnés utilisée par exemple lors d’une analyse d’images d’animaux. Il est plus que préférable que toutes les images fassent la même taille en pixel. Par exemple du 200x200.

Nous allons, lors de la génération, s’aider de cette image.

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXdBEJWiojiDEjk9W6UUBluelEJHg3GSdpvkGSR7FcX4Omi7b5MPkcDKzmmkjvE4VdhV3uJkGpCBzWu5_jkwnDeVEcKK6Z65RXNwMLXsMHag6Dff2RBkRk8J7nGgm-kE4bkV8w3FDJbr5Kjd8wSkm468ptdMAmMWLQZTjcrKUJEClUxD2Djf?key=vp8mLtB2MzOoxGU8IWZGLA)

“<https://www.stevemorse.org/ssn/List_of_Bank_Identification_Numbers.html>”

Dans le cas précis des American Express, le préfix du réseau bancaire est de 3 car il s’agit de la catégorie _travel and entertainment_. Le chiffre d’après est toujours 4 ou 7. Avec ce que je sais, je peux donc commencer à créer mes numéros.

**Numéro début**

Le début de la génération est assez simple (et pareil pour le reste).

On fait une liste avec les deux seules possibilitées qui existent et on choisi au hasard par quoi commence la carte :

  

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXf9x6qXyRVfnrbzKn-t1J6yH_ui1u22XjnudOqFYxsz1gk156hsmllUdDr7bMkhr-KC_8nRROOriMJRXtvbchJWkpGIgGkRGlwDd39sGG06l9SV77cMtH4K6N-RtaJw7M2iEne2LSyVyb80onYqC49TGPUS1476ILcxcEDmo3v0PwFGj3z3FQ?key=vp8mLtB2MzOoxGU8IWZGLA)

**Numéro émetteur**

Après de nombreuses recherches je n’ai pas pu trouver comment étaient faits -ou dans quelle limite étaient faits- les numéros émetteurs. Je sais à quoi ils correspondent mais cela ne m’aide pas vraiment. Je décide donc de générer tout au hasard, quitte à perdre des perf.

On va donc ensuite générer les 4 chiffres suivants :

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXewrSgolyyMw26ttj93QF1AfB1QFP-5EH9SadGSB2Z4ZsSV2i3PxsXq2I4whnBDtOB8cUhf6RiaJuccrmsbzVLqoOBT6pGPDC0spEw2w2-w1VTkKJUQCwjAMqWbe14J1oM1XTKlmwgaplviC3C2XyzdBhDXcKEczkT0OtdlZB4LRYtoaAoOBA?key=vp8mLtB2MzOoxGU8IWZGLA)

 

J’ai essayé de générer la liste de base en mettant le random.sample en string mais ça ne fonctionne pas. Je suis donc contraint de créer une seconde liste. 




**Numéro client**

De la même façon, je ne sais pas comment est fait le numéro client. Je n’ai pas trouvé… (bon je n’ai pas cherché outre mesure mais ça m'a saoulé c’est pas mon projet à la base).

Je fais donc pareil mais en générant 8 chiffres au lieu de 4 (comme vous pouvez le voir sur le screen, sauf que j’en génère 8 car les amex sont faites de 15 et non 16 chiffres) 

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXdUO8L4QfuBgFe0wy-9LxIaIgsRi897u3te1ubNFjGSapdpd02Imd_2wCwjD5UZYQ1Bf33PEKVf_zHEDV4aoO3Fedy4EStc50NSAabnztR22IXHEVNdxxAX6Oct6tSrYvC22CxC0ELAxD5RI-1-JKKloEimTFyFAV0cvmm_YxE9yYZf9uuSLA?key=vp8mLtB2MzOoxGU8IWZGLA)





**![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXeo_G3ztHtPlaYZVNJ6putouKzgex7butQi-j-hHF8Jr6ApEaisTsCNr-G0_6KqwmmalMFEJqboeUYMtZRoIyesRvoz-1oGvXwK_6HhB5IGifhuGi41Q2OSesic-v4wzh9Az3S57xvU_x7S_oiTJUkcizJpFDJn9p0sl3h1o-q4HTjEdDjr?key=vp8mLtB2MzOoxGU8IWZGLA)**

**Algorithme de Luhn**

Je ne vous explique pas en détail comment fonctionne l’algo de Luhn mais il sert à déterminer si un numéro de CC est valide ou non. Il donne la clé de contrôle en fonction des 14 digit précédents. Je vais donc le développer sous forme de fonction afin de pouvoir l’utiliser quand je veux au cas où. Le principe est plutôt simple donc de même pour le code.

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXdBELdM4mtkZEkMGZCNXIdG675MkMG_RbU4TzPqIv_FyR0s2mVH0vRG6R8sO7Ycm68NXDXGAN3e2PdsmZb89otTXZCVsMg0oskU3iuEF73JnM_nZMJLQkYm_vxuoRiPDlmpEZrn3T-Rn0ka3Lrc_NtU8GbBUG5dvp2DCv5HEjsTpe7WsDROIg?key=vp8mLtB2MzOoxGU8IWZGLA)

**Clé de contrôle**

L’algorithme de Luhn est utilisé pour créer la clé de contrôle des cartes de crédit, dont l’Amex. Il n’y a qu’un seul chiffre à la clé de contrôle. Ce chiffre de clé de contrôle est calculé tel que : 

 ![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXevzGeLjPMf6F4_AUorGNTj5Kp5z6Q8tgoRsv_an0FALCN2qtjDDyIGfabGZrRuXPr-i1mdfVhIOfSsbOUoe1asDxFxCiihYMb5a_7qADwplVs4TFttNjccRbHrURIYY1ZJ_qkcUzU9z8aTfGw2U2OvrBCrg0XCb3XKre_l5URERcLC1DMY9Q?key=vp8mLtB2MzOoxGU8IWZGLA)




**Inscription dans le fichier CSV**

Pour inscrire ces numéros dans le fichier CSV je fais exactement pareil que pour les NIR.

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXctKdghjRHZuE5a_dShQ15sAfigSxQOfQFAkYixrxbTY927Ew9_uOZzOzxymqLyplANiZBEGQ7C8l8SlZ1JjP1omECXIQ2wzwQ4KLCV9xt068UyuNshKPR9dfH1xn5SfcJoHhXxMuPg4pK2toa7xPbelpxxc3-3IirCDDSpATW5hA6UT2zUwQ?key=vp8mLtB2MzOoxGU8IWZGLA)

**Partie 1, la fin d’une histoire …**

Voilà tout, en ce qui concerne la première partie de mon projet. Il ne s’agissait après tout que d’un prérequis pour mon projet final : distinguer ces deux types de numéros. Pour cela, comme expliqué précédemment, je vais utiliser TenserFlow. Alors sans perdre de temps, lançons nous !



**Création de l’IA** 

Pour commencer, je tiens à dire que dans ce compte-rendu, je n’expliquerais pas le fonctionnement d’un réseau neuronal car ça serait trop long et surtout vous savez déjà comment tout cela fonctionne. Je ne m’attarderai que sur les parties précises de mon code (celles dont vous pourriez par mégarde croire que j’ai copié-collé sur internet) afin de vous prouver l’implication et la dévotion totale de mon propre esprit dans ce projet. 

Malgré une utilisation de VScode abondante pour la suite de ce projet, je vais utiliser Jupyter Notebook afin de faciliter la visualisation des données.

Tout d’abord configurons un peu notre environnement de travail.

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXdW41AUhGIKOAEPyE_Zdm6Bt-mWX8VI_QIk_NOqxpEzWMUEvmG-K28spTMBvVCoyrdXZZJJ5ujZy-32tLPhSw7rBqjtNFOSKH95DfGkZK-9BUwupbXRTkT8FqmMatc_q0_UXdvmhna4Jmrwq1DiHoASBaWPB6HMkSZddMdxOIBq30OA4mnX?key=vp8mLtB2MzOoxGU8IWZGLA)

Voilà, tout est bon. Lançons nous ! 



![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXe68ODHxskcLNzTvfncJEB58fOE9ZagR2xR5Y9TNmwGbD_8VfhLhxhLw3syWwD0jAESdGls65naZK8EYyj90Vu4y79Izu0pq_g89EAznjQIWeFjMDImX68PtIf7s93AsY-LOfBwIIJqvs9z0SOYNM7u3wwUlG0RZjn1N4ZNF1MBaSPuYHFU?key=vp8mLtB2MzOoxGU8IWZGLA)

**Traitement du fichier CSV**

Lors de ce projet, je vais me servir de mon fichier csv créé avec les tools précédents. 

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXdqq7l0PyplZVBgsaHCRPG394ay6S2X33xHlJQ7RL3Lxc2vnYycU9xJmOxSAM1K65Ae7u8JKMsl3W88xBQDIUrfvPe5gDZScMtIljMWvEK-UscQfD2lY1WgDKT0Kt5ezxwIv_F7Sv6hRpFjYRmzAFCflnUv3pc06MLfDwNBlpYEN2A6fHxrWA?key=vp8mLtB2MzOoxGU8IWZGLA)![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXfs4b0EE81KfSvBg9fiGD5GQzzJVrOUfwF3QlTpDkMXxUvHaxVEsgSqh7KJqo7qql_qPP1PRECSdOcHo63NX_pDy_Xj9JS16-cMUVGc1_jEZ6hmGIgBf0_lIhzHQ7RivXLuol6hcIbDFcLdU6WS1die5EgSREl_kc730aVQY1BagxZM4pw1cA?key=vp8mLtB2MzOoxGU8IWZGLA)

Malheureusement, les modèles de deep learning ne sont pas text friendly. Il m’est donc nécessaire de transformer mes catégories “nir” et "cc". Il est donc évident que cela va se transformer en 1 et 2 (et dans la même logique, si je dois analyser d’autres types de suite de chiffres, ils deviendront 3,4,5 et …).

Pour faire cela, nous allons utiliser la fonction _replace_ qui est incluse dans la librairie pandas.

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXeUBtBsVRS19KViJVcDYPnl-3j1FmoQcz6rKjWSqwrlDDT-lQkmyplJptnot7rirnceuqD0QOaPOXYICexIX_Xnn3tQO82-WsKu-hbHB0vzrLalMw5OdPyP5aMhnx1NDHtjldp-g_bzdWpahmStXWqBq4myyfoL0VsfglUb86vkfc7UAz3UhQ?key=vp8mLtB2MzOoxGU8IWZGLA)

Comme on le voit tout fonctionne parfaitement pour le moment.

**Problème potentiel**

Peut être que je devrai réduire la quantité de séries de chiffres car j’ai l’impression qu’en ayant 100k de chaque, mon modèle va surement être “overtrain” et je vais finir par avoir une prédiction de mes résultats très inexacte. On verra bien plus tard, tout ça se résoudra très rapidement.

**Constat gênant:**

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXe48Zpor4h82RWcUCFGZM91R_58QKMYxlrij2ns9-4JspiwzpdA2HYapZaNfc9pZMmUMsq9sv-u542VuufY4zUWT6CL9cBPL4r3DqZKE1zeYGnbvs6cn9k2Qgih8aXfXdSNKTPHa75fyaIFsg0NXWmTeumqb9OL-kbqZl9e1dAQsLa2zVDGrg?key=vp8mLtB2MzOoxGU8IWZGLA)




Comme on peut l’observer, les résultats sont plus que mauvais. Je me demande donc comment cela se fait. Les raisons peuvent être si nombreuses que je vais péter mon crâne. J’ai déjà essayé de jouer avec les fonctions d’activation en utilisant _relu_ mais l’accuracy reste la même. Je crains que le problème vienne du fait que je n’ai qu’un seul neurone en entrée en hiden layer. Mais je me demande donc comment je peux diviser mes séries de chiffres afin d’avoir plus de colonnes, car le diviser en 15 colonnes (par exemple : une colonne, un chiffre) serais plutôt stupide, je pense. Donc peut être qu’une division en deux pourrait être une option. A savoir que même en changeant l’epochs, les stats ne s'améliorent pas au fur et à mesure du temps. De plus, je viens tout juste de réduire mon échantillon de 200k à 20k séries de chiffres, mais ça ne fonctionne pas mieux. Je décide finalement de diviser mes séries de chiffres de la manière suivante : 1er chiffre, 7 chiffres suivants, 7 chiffres suivant. Je vais ensuite voir le résultat que cela donne, mais je dois d'abord modifier le programme que j’ai fait pour les NIR et CC.

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXd4maea1FaNbaObXlPCfLO1lNXIcnf8rbvwLltdPpXDwdVPEFklUaipfp296OGnU-9Ufsd4HCrI533VScGQme94TY4JAIV30EaBg0Ljr1ng5Boy-SQSsk3SqQINUWc4RQv_S_preSozGEPmlPul6vxz2LLpeGDoGt-i8jYg5eV87f8H3pt3gg?key=vp8mLtB2MzOoxGU8IWZGLA)

Une seule ligne suffit à tout régler (à peu près). Le résultat est bon :  

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXcVeJiQAVjuvPi7AEWo9h0K3xB9TCx0jC0gh8xRxCCUF7j7TRMXKjGWfnwGGhnb4OlZpmkQoJYxPGgJ7FztBBeu4Ge0CXEMZq0Tdb8K7_vMXTmC95kKpzzbZXc9oiO4wXLOBhfPkO3J7m8tomPaEgqNLEBbojIu4NqrBn9XJwclr12bk9my?key=vp8mLtB2MzOoxGU8IWZGLA)

 


**Nouvelle tentative**

Maintenant que j’ai améliorer cette partie, il est l’heure d’essayer à nouveau.

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXc956EcEDmsXE_oPSQPLkUSrD8UUuNHkfe1gixuqikVKXjxmxkIyLBVeiUy1ogQaINyTEzH_c7s54v9hx-KJlfpN_N2NotIrFadNZr3OecoXqXsMgyv-T1-OXBrtAFp3Ui0OUm4gFH170Nj-HWQHmvG9-XoAV5Q2Z0ALqLu4WtICTHQDinheQ?key=vp8mLtB2MzOoxGU8IWZGLA)

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXcnOL5Qhx9uts8D4kRYLdRfgCRi4wew2MjxXMNWRjsWqKvZY-OyRwXgT4Xcy7C6W8ERen4rOKq8eJtCDhA4hGKWhZhvCj68dZSEriSXHeuhFWeYBOMMaKhk1VgDVYPmkAgS-VFJdZQqlJxWDEXKw-NsfgxjZ7Q7ytvBj-8JxF-0zb5a95cB?key=vp8mLtB2MzOoxGU8IWZGLA)



Pour l'instant tout va bien. Le résultat de ce code sera le moment de vérité, car j’ai malheureusement essayé sans scale les values de 0 à 1. Le résultat parle de lui même :  

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXdaxeCSYkqyAP2WlDlsDdP1vYbRXLTisZNO0h8sRw3H2rq_6nGgT-nAFLeBjKzlnvWncieTluZvHlwKPP_TinvDaqkTnz0cLrB82tPIQadNp0j81AeR7byp5l8X3qhJJZEeflVpee78D2vJc-gaI5GJ5XU4Jn5hpboD8lmeDdqaMoaObPoYOw?key=vp8mLtB2MzOoxGU8IWZGLA)

A peine 55% d’accuracy autrement dit c’est vraiment inutile.



MAIS VOILÀ QUE TOUT D’UN COUP ….. 

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXff60AZE9qGtWaPnokWHOsPjjv6pVIuLQpSK3h5Xqcy0E9YTOBWpaGmBtxbbjOAHianMmlvQVkXBTRX99sVuHdHGwQop9DDYmclOkc_YEsRPtiZcBvpjVPYCwIniRnS1qJP4KrtpaOtKbyeZKsasLXI-ExC7oZdLmagwOW83CTCDBUjOrd3cg?key=vp8mLtB2MzOoxGU8IWZGLA)




![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXeh1ESqQmmYTLREQoHu7zaWlfIttpGmQOB4lXzwQ3xkgqDqsaQSEpEXtwX7fNcIeHlnIEdMymo4hELi-bBkTFpHuips7OKOQD8VTCgRf3xrXBm7ab53kNC74C7Zuqm2j-jz32CZ6wt1Pk1m7IvNMmbIqCstALfrYXb2rTHKprD6wOjNC-jsSQ?key=vp8mLtB2MzOoxGU8IWZGLA) Personne ne peut prétendre avoir une fonction loss qui retourne un résultat si bas que ça.

On observe que de manière plus que concluante le modèle marche à la perfection.


Dans cette section je vais rentabiliser mes dizaines d’heures à écouter des indiens parlant un anglais approximatif afin de m’enseigner le deep learning.



![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXcnOAzS3wfoSrvJ042iLRrLbOQgSifhQxhp27MTTqA31K7wGJ-aBLDtCfBG4rvgUIIFguO8MT4WpptDFh_-UqAOgy7yq_ThixmcwIlXv99LYTTW0efUV9A5xxYFoExgS1qROked5G9RRKm7hR3mao5fnGeVvv3G7JlxzvNOkoZ6Cy_Y1TXayQ?key=vp8mLtB2MzOoxGU8IWZGLA)

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXffv7AdzaPd3YbIAgo5LZ_vv9O9EjSWiVa-_9o_eTwcj0ATwggOZUwkOMrmb0mse95je5Q6A_ijAuKCvbZo_koUoDnToswNZYmAGeiOi5m4rKLMJ3JpEI51zeOvrtuhPhHnJEt3_rOn9au1lYD6vXc3AhXbYnIdO5k338TvDmBg26_83DjjTA?key=vp8mLtB2MzOoxGU8IWZGLA)

Ici, j’importe les modules dont j’aurai besoin (je vais finalement me servir uniquement de pandas).

Je charge également mon fichier CSV et le print afin de voir que tout est bien en ordre.

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXd0e2m_4htmBozjBqzoNJyfYWXs9TBef04GB0NrSl1WDN2cxHupY_Yz9WhEpyZvGdrZRRzeDoQDvwU9AS2MSGv2tqDjVhDemx80FC_yFyZZhhLitpva-qySR3Zz-DT9bNtlg7X0DIwXdHP3x421JGe2fWNnhs8iXdPjJLkqtZBU0YdoSS1z?key=vp8mLtB2MzOoxGU8IWZGLA)

A l’aide d’un dictionnaire, je remplace toutes mes valeurs NIR et CC par des chiffres car les IA n’aiment pas les string. Cela me donne un résultat binaire (ça ne sera pas le cas à la seconde ou j'intégrerai d’autres types de séries de chiffres un autre jour).

Je print pour voir si tout fonctionne, et c’est le cas.

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXeM8vtTVjc4_GPNUKr18p5omCtCqmNGqVCmvka01C3E8MzJklhq1FuIxYiiPSpYbmzl03mHfVuppxOJcFekacjIsfgNGN1ea1RfZFzhgLf_O6MdcNvpACoYvU2KmwhScai5QfvF2d8QAwkFTfCagkxQFT_n9spgBYWVYECRjDwHcw8khMhnuA?key=vp8mLtB2MzOoxGU8IWZGLA)

Comme déjà dit dans le compte-rendu, la scale des éléments est importante en deep learning je dois donc faire un travail de traitement des données afin de m’assurer du bon déroulement des choses. J’utilise ici le module sklearn et une fonction qui lui est pré-intégrée, qui va me permettre de réduire les nombre de 7 chiffres en chiffres de 0 à 1 de manière efficace et sans altérer l’output de mon réseau neuronal.

Je transforme les colonnes que je veux adapter sans oublier de ne pas impacter la colonne type (ça n’aurait pas changé grand chose mais on ne sait jamais)

Encore une fois je print et je check que tout fonctionne.




![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXcBIVlP3G750VKzvkC9pVbpKuIuzVo-89JCgAEvBFwZc7ECxV9lRbz7rIViqBeLzBwb_5Vvn-YLU_74U3JLGViwewi5JNoxgmQbOKgOltKWhq315rAzmtHUVDXgpaNxN2XogLdPkupVIQGRwHXWLKMCoCBcrBSNT25SJG5azHB6scSNvj5cnA?key=vp8mLtB2MzOoxGU8IWZGLA)

Les choses un peu plus sérieuses commencent. Ici je crée deux variables qui correspondent a mes colonnes (x) et l’output qui est censé avoir (y). Je vais ensuite, grâce au module sklearn, transformer ces simples variables en entrainement pour mon ia avec x/y\_train, mais aussi en lui permettant de confirmer si tout ce qu’elle fait est bon avec x/y\_test.




J’ai décidé d’allouer 80% des ressources à l'entraînement et 20% au test.

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXegXNeAfGPyWDB-kTvve4bq_dDUnnEx29zOmhRz9l8riKm0mRZ_0OQaCj7jLvZdhcnYGepeMku9iV2SbGhSPSrJkbVZ56Arp31OcxabfrwSiyMVn3tuIKar1bnd6l1tYgn_LJjaKfvMimNrxI7RRvxMzRiCVVuUDooCKey_IswgX7S8U_Wk?key=vp8mLtB2MzOoxGU8IWZGLA)

Ici on voit que tout est fonctionnel.

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXdColH4-dy64-WMQzV0pk8AkfGJxV7onaj2x2hBSdXz-fd0Do1yP--9zJMdpFDpQIj_JuOGEqFixJBTM3BmlqP3_3co5Tkcldkx6IYiEEc6u0FaFoFBJVi0n-l63kwXSWAbUUNzhxHTc6dyccHIikLDlMByuP0ou3eh9qMCQNbilFCXCkD7BA?key=vp8mLtB2MzOoxGU8IWZGLA)

Là aussi tout va bien.

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXcXgkX523Skah10wRIDPCqU01N_spcsy_ZMoFZ4R5vJlfTFUY8vdqhS3WsVm3iT6ZbLSEmEOK7p0woYn9QWvDFbBYSbOH0s3pi5CYayt-KvWZKTyNyUFAbl7IhVnH_FT6Fwa3I2tUfynB1OCbOU4BlKEDa5tGVHn55zgxR6VYQHbA3hwZCsXA?key=vp8mLtB2MzOoxGU8IWZGLA)

Voila tout ce qu’il y’a de plus simple, complexe et concret à la fois.

Dans ce code je commence par importer tensorflow  ainsi que keras.

Keras sert à créer des réseaux neuronaux.

Je crée donc mon modèle avec une couche d’input qui correspond tout simplement à mes 3 colonnes, au même moment une couche cachée est créée. J’utilise comme fonction d’activation la fonction _relu_ car elle ne demande pas trop de performances comparé à d'autres et elle est également la plus adaptée dans cette situation.

Un seul neurone est nécessaire pour l’output et la fonction d’activation utilisée est sigmoïde, car dans ce cas précis, le résultat attendu est binaire (la fonction d’activation pourrait par exemple ici être modifiée si d’autres séries de chiffres sont ajoutées au programme).

Je compile ensuite ce réseau de neurones. L’optimizer utilisé ici est _adam_ car il s’agit de l’optimizer le plus utilisé et le plus basique je n’ai pas besoin de faire un autre choix pour mon programme. Loss prend cette valeur car mon output est binaire.

Je finis par lancer mon RN avec mes fichiers de training créer plus tôt. J’ai set epochs à 100 mais comme on le voit ici : ![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXcnqSNtzTpshNdNsvm7Po0UXveRXo4IRFR-MhiIFBafYEt6Ni-pjrL3tH4TeriVhpAR-SkwklKHpCYIEz-1utVAx8gSNbOCc7-SE1M_hSbfbiCqRpUluA-cUM31O9RKtFG1A8rgjX0oByC-vkCxX-xh0gs6NXZIAY085T4SQKhHfA-R8k7mJA?key=vp8mLtB2MzOoxGU8IWZGLA)

5 tours du dataset auraient suffit car la détection n’est pas très compliquée dans ce cas précis.

—------------------------------------------------------------------------------------------------------------------

**Cahier des charges pas nécessaire car déjà inclu dans le postambule de mon compte rendu :** 

Je dois juste savoir qui est qui en résumé. L’objectif est de détecter de quel type de série de chiffres il s’agit. (à savoir que l’idée est vouée à évoluer car j’aurais pu sinon tout simplement faire un : 

if ftDigit == 1 or ftDigit == 2:

print(“numéro NIR ouaisss !!!”

else:

print(“bingooooo numéro de cc”)

—--------------(trop long de relire tout le projet donc surement des erreurs)---------------------!

Durée de réalisation : 1 semaine

Difficultées rencontrées : Comprendre de A à Z le machine et deep learning (malgré cela j’ai toujours l’impression de manquer un truc et de ne pas m’y connaitre même si c’est surement normal vu que c’est très vaste )

Note globale :         `⭐⭐⭐⭐`


# Code ancien donc surement pas très beau a voir : 



```py
import random,time,csv

#lancer le chrono pour savoir je met combien de temps a faire tourner le programme
tps1 = time.time()
quantity = 10000#int(input("Combien de CC et NIR souhaitez vous générer > ")) 


#création de l'algo de Luhn
def algoLuhn(number):
    #balayer les chiffres faire une nouvelle liste en int reversed
    number = number[::-1]
    number = [int(x) for x in number]
    #balayer dans la totalité de 2 en 2 comme le veux l'algo de base
    for i in range (1, len(number),2):
        #x2 les nombres impairs
        number[i] *= 2
        #si superieur a 9 on fait modulo 10 + 1 ce qui reviens a faire par ex 18 > 9 donc 1+8 = 9 (vous avez compris l'idée)
        if number[i] > 9:
            number[i] = number[i]%10+1
    #on additione le tout et on le return pour pouvoir calculer la clé
    full  = sum(number)
    return full


#création de la fonction pour générer des NIR 
def genNIR():
    #sexxxeeeeeee ;)
    sex = random.randint(1,2)
    #année de naissance
    bornYear = random.randint(0,99)
    #mos de naissance
    bornMonth = random.randint(1,12)
    #département de naissance
    bornDep = random.randint(1,99)
    #code commune INSEE
    commDep = random.randint(1,909)
    #ordre de naissance
    bornOrder = random.randint(1,999)
    #création d'une liste qu'on va parcourir pour pouvoir faire en sorte que l'affichage soit tel que 01 ou 001 au lieu de 1
    list  = [bornYear,bornMonth,bornDep,commDep,bornOrder]
    listCent = [commDep,bornOrder]
    total = str(sex)
    #code qui parle de lui même 
    for cat in list: 
        if cat < 100 and cat > 9 and cat in listCent:
            cat = str(cat)
            cat = "0" + cat
        elif cat < 10 and cat in listCent:
            cat = str(cat)
            cat = "00" + cat
        elif cat < 10 and cat not in listCent:
            cat = str(cat)
            cat = "0"+cat
        else:
            cat = str(cat)
        #création de la variable total (tout est en string)
        total += cat
    #mise en int de la variable pour pouvoir calculer la clé
    total = int(total)
    #création de la clé
    controlKey = (97-(total%97))
    #même système que pour ce qui précède
    if controlKey < 10:
        controlKey = str(controlKey)
        controlKey = "0" + controlKey 
    else:
        controlKey = str(controlKey)
    #le remmetre en string afin de pouvoir avoir mon truc en entier
    total = str(total)
    total = total+controlKey
    #au cas ou une clé est mal générer pour je ne sais quel raison
    if len(total) != 15:
        return genNIR()
    #on return pour pouvoir l'écrire dans le fichier texte
    writer.writerow([total[0],total[1:8],total[8:],"nir"])


#création de la fonction pour générer des CC
def genCC():    
    #faire en sorte que la carte commence par 34 ou 37 comme toute les american express 
    bankStart = [34,37]
    bankRef = random.choice(bankStart)
    bankRef = str(bankRef)
    #je crée la suite des caractère (l'éméteur) avec le module random et je transform la list de int en list de str et en une seul variable
    issuerInt = random.sample(range(1,9),4)
    #un peu de list comprehension
    issuer = [str(issuer) for issuer in issuerInt]
    #on whipin tout
    issuer= "".join(issuer)

    #comme on dit en bon francais 'tout pareil' (bon on est pas totalement stupide on change la quantité de chiffre générer pour en avoir 8)
    userInt = random.sample(range(1,9),8)
    user = [str(user) for user in userInt]
    user = "".join(user)

    #on met tout ensemble ni plus ni moins
    total = bankRef + issuer + user + "0"
    #on créer la clé de mon numéro d'Amex si c'est deja bon alors c'est cool et sinon on fait la clé
    if algoLuhn(total) % 10 == 0:
        True
    else:
        key = 10 - algoLuhn(total) % 10
        key = str(key)
        total = bankRef + issuer + user + key
    #pour pouvoir l'écrire dans le fichier
    writer.writerow([total[0],total[1:8],total[8:],"cc"])

#on ouvre le fichier csv avec les catégories qu'on veut créer             
with open('numType.csv', 'w', newline='') as file:
    writer = csv.writer(file)     
    field = ["ftDigit","sevOne","sevTwo","type"]
    writer.writerow(field)
    #en fonction de la quanité de numéro que l'utilisateur veut on inscrit les numéros dans le fichier csv 
    for i in range(quantity):
        genCC()
        genNIR()

#afficher le temps que le programme met
tps2 = time.time()
print(tps2-tps1)
```