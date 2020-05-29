---
title: 5 Adressage IPv4
description: 
published: true
date: 2020-05-29T22:19:01.929Z
tags: 
---

# Adresses IPv4 et classes d'adresses
Chaque ordinateur connectéà un réseau est identifié par un numéro unique. Ce N° est appelé **adresse IP**. Jusqu'à la version 4 du protocole IP, elle est codée sur 32 bits, ce qui fait donc 4 octets.
On peut donc théoriquement attribuer simultanément $$4 294 967 296$$ (soit $$2^32$$) d'adresses. En pratique, un certain nombre ne sont pas utilisables.

Une adresse IP est notée comme une suite de 4 octets, codés en décimal, séparés par des points.
Par exemple 192.168.1.41 est une adresse IP utilisant la notation décimale pointée.
Le codage décimal de chacun des 4 octets est basé sur le principe suivant:
Dans un octet (8 bits), chaque bit a un poids (importance) particulier.

| $$2^7$$ | $$2^6$$ | $$2^5$$ | $$2^4$$ | $$2^3$$ | $$2^2$$ | $$2^1$$ | $$2^0$$ | Total      |
| ------- | ------- | ------- | ------- | ------- | ------- | ------- | ------- | ---------- |
| 128     | 64      | 32      | 16      | 8       | 4       | 2       | 1       | de 0 à 255 |

Le bit le plus à droite est dit "bit de poids faible","LSB" et peut prendre la valeur 0 ou $$2^0 = 1$$, celui le plus à gauche est dit "bit de poids fort","MSB" et peut prendre la valeur 0 ou $$2^7 = 128$$.

La valeur de l'octet est donc la **somme des poids de chaque bit à "1"** et elle peut varier de 0 à 255.
Une adresse IP se divise en deux parties (en prenant l'adresse complète 192.168.1.41):
- d'une partie qui indique le numéro de réseau, ici 192.168.1,
- d'une autre partie qui indique le numéro de l'hôte (ou de la machine) sur ce réseau, ici 41.

Depuis 1998, c'est l'ICANN (*Internet Corporation for Assigned Names and Numbers*, remplaçant l'IANA, *Internet Assigned Numbers Agencey) qui est chargée d'attribuer des adresses **IP publiques**, c'est à dire les adresses IP des ordinateurs directement connectés sur le réseau public Internet. L'ICANN délègue une partie de la gestion des adresses à d'autres organismes appelés RIR (Regional Internet Registries).
L'affectation des **adresses Privées** est à la charge des administrateurs réseaux de l'entreprise.

L'objectif de l'adressage IP est de pouvoir identifier des réseaux mais aussi les machines appartenant à ces réseaux. Pour cela, on a défini différentes combinaisons des 32 bits. Il s'agit des classes d'adressage. Elles sont au nombre de 5: A, B, C, D et E.

Chaque classe d'adresses (A,B et C) possède une plage d'adresse réservée aux réseaux locaux privés (RFC 1918). Toute organisation peut donc utiliser ces adresses pour ses propres besoins.
> Ces adresses privées ne sont pas routées (ou routables) sur Internet.

C'est à dire que les routeurs qui gèrent l'acheminement des trames ne savent pas traiter les adresses privées ce qui est normal puisque deux ou plusieurs organisations peuvent utiliser les mêmes adresses privées. Un routeur ne peut donc savoir à qui correspond une adresse privée.

| Classe | Adresses IPv4 sur 32 bits                                                                                                                                                                       | Description                                                                                                                                                                                                                          |
| ------ | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| A      | De <span style="color:red">0</span>0000000 . 00000000 . 00000000 . 00000001<br />A <span style="color:red">0</span>1111111 . 11111111 . 11111111 . 11111110<br />De 0.0.0.1 à 126.255.255.254   | 1 bit Id_classe<br />7 bits Id_réseau<br />24 bits Id_machine<br />126 ($$2^7$$) adresses réseau<br />16 777 214 ($$2^24 - 2$$) adresses machines<br />réseaux locaux: 10.0.0.0 à 10.255.255.255                                     |
| B      | De <span style="color:red">10</span>000000 . 00000000 . 00000000 . 00000001<br />A <span style="color:red">10</span>111111 . 11111111 . 11111111 . 11111110<br />De 128.0.0.1 à 191.255.255.254 | 2 bits Id_classe<br />14 bits Id_réseau<br />16 bits Id_machine<br />16 384 ($$2^14$$) adresses réseau<br />65 534 ($$2^16 - 2$$) adresses machines<br />réseaux locaux: 172.16.0.0 à 172.31.255.255                                 |
| C      | De <span style="color:red">110</span>00000 . 00000000 . 00000000 . 00000001<br />A <span style="color:red">110</span>11111 . 11111111 . 11111111 . 11111110<br />De 192.0.0.1 à 223.255.255.254 | 3 bits Id_classe<br />21 bits Id_réseau<br />8 bits Id_machine<br />2 097 152 ($$2^21$$) adresses réseau<br />254 ($$2^8 - 2$$) adresses machines<br />réseaux locaux: 192.168.0.0 à 192.168.255.255                                 |
| D      | De 224.0.0.0 à 239.255.255.255                                                                                                                                                                  | 4 bits Id_classe<br />28 bits Id_réseau<br />De 224.0.0.0 à 239.255.255.255<br />Adresses réservées<br />Adresses **MULTICAST** (adressage simultané de plusieurs machines utilisant une zone spéciale de l'en-tête d'un paquet IP). |
| E      | De 240.0.0.0 à 255.255.255.255                                                                                                                                                                  | 4 bits Id_classe<br />28 bits Id_réseau<br />De 240.0.0.0 à 255.255.255.255<br />Adresses **INUTILISEES**                                                                                                                            |


# Adresses particulières
Une adresse IP est donc constituée d'un *Id_réseau* et *Id_machine*, le tout sur 32 bits (Ex **192.168.1.41).
Lorsqu'on annule la partie Id_machine, c'est à dire lorsqu'on remplace les bits réservés aux machines du réseau *par des zéros* (exemple: 192.168.1.<span style="color:red">0</span>), on obtient ce que l'on appelle l'<span style="color:red">**adresse réseau**</span>.

Lorsqu'on remplace les bits réservés aux machines *par des 1* (par exemple 192.168.1.255), on obtient ce que l'on appelle l'<span style="color:red">**adresse de diffusion** ou de **broadcast**</span>.
Il s'agit d'une adresse spécifique, permettant d'envoyer un message à toutes les machines situées sur le réseau spécifié par *Id_réseau*.

Ces 2 adresses (que des "0" ou que des "1" pour a partie *Id_machine*) ne peuvent pas être attribuées à un hôte du réseau.
Enfin l'adresse <span style="color:red">**127.0.0.1**</span> est appelée <span style="color:red">adresse de rebouclage</span> (<span style="color:red">loopback</span>) car elle désigne la <span style="color:red">machine locale</span> (<span style="color:red">LocalHost</span>).

Le processus <span style="color:red">**APIPA**</span> (<span style="color:red">A</span>utomatic <span style="color:red">P</span>rivate <span style="color:red">I</span>nternet <span style="color:red">P</span>rotocol <span style="color:red">A</span>ddressing) ou *IPv4LL* permet à un système d'exploitation de s'attribuer automatiquement une adresse IP, lorsque le serveur **DHCP** est hors service.
APIPA utilise la plage d'adresses IP *169.254.0.0/16* (qu'on peut également noter 169.254.0.0/255.255.0.0), c'est à dire la plage dont les adresses vont de *169.254.0.0 à 169.254.255.255*.
Dans certaines situations, il est préférable de désactiver APIPA afin d'empêcher l'attribution automatique d'une adresse IP par le système. Ceci pour éviter de penser qu'un serveur DHCP est bien actif.

# Masque de sous réseau
## Utilisation des classes standards
La lecture d'une adresse IP ne permet pas de faire la distincion entre la partie *Id_réseau* et la partie *id_machine*. Le seul moyen pour cela est d'utiliser le masque de sous réseau. Ce dernier utilise la même notation qu'une adresse IP (décimale pointée). Si l'on convertit les décimales en binaire, on obtient alors une suite de "1" et de "0".
Les bits du masque de sous réseau qui sont à 1 identifient la partie id_réseau de l'adresse IP et ceux qui sont à 0 identifient la partie id_machine.

Si l'on n'utilise pas de sous réseaux, les masques de sous réseau des classes d'adresses A, B et C sont respectivement:
- 255.0.0.0
- 255.255.0.0
- 255.255.255.0
  Où les "255" correspondent aux octets id_réseau, les "0" correspondent aux octets Id_machine.

Exemples:
* Adresse IP de classe B: 172.16.10.20 => masque de sous réseau 255.255.0.0
  Adresse IP en décimal :   172         16          10          20
  Masque en décimal     :   255         255         0           0
            en binaire  :   1111 1111   1111 1111   0000 0000   0000 0000
  L'adresse du réseau est **172.16.0.0**,
  L'identifiant de la machine dans le réseau ci-dessous est **10.20**

  Dans ce cas simple, on arrive facilement à déterminer l'adresse du réseau. On devrait faire la même chose mais de façon plus rigoureuse, comme le fait une carte réseau. Pour cela, il faut faire un *ET Logique* entre l'adresse IP et le masque en ayant au préalable convertit l'adresse IP et le masque en binaire.

  | IP 172.16.10.20    | 1010 1100 | 0001 0000 | 0000 1010 | 0001 0100 |
  | ------------------ | :-------: | :-------: | :-------: | :-------: |
  | Masque 255.255.0.0 | 1111 1111 | 1111 1111 | 0000 0000 | 0000 0000 |
  | ET logique         | 1010 1100 | 0001 0000 | 0000 0000 | 0000 0000 |
  | Adresse            |    172    |    16     |     0     |     0     |

* Adresse IP de classe C: 192.168.14.22 => masque de sous réseau 255.255.255.0
  Adresse IP en décimal :   192         168         14          22
  Masque en décimal     :   255         255         255         0
            en binaire  :   1111 1111   1111 1111   1111 1111   0000 0000
  L'adresse du réseau est **192.168.14.0**,
  L'identifiant de la machine dans le réseau ci-dessous est **22**.

  | IP 192.168.14.22   | 1100 0000 | 1010 1000 | 0000 1110 | 0001 0110 |
  | ------------------ | :-------: | :-------: | :-------: | :-------: |
  | Masque 255.255.0.0 | 1111 1111 | 1111 1111 | 1111 1111 | 0000 0000 |
  | ET logique         | 1100 0000 | 1010 1000 | 0000 1110 | 0000 0000 |
  | Adresse            |    192    |    168    |    14     |     0     |

## Mise en oeuvre de sous réseaux
Comme on l'a vu précédemment, l'utilisation des classes d'adresses est devenue inapproprié avec la généralisation d'Internet. Par exemple, une adresse de classe A (16 777 214 hôtes possibles dans un réseau) n'est jamais utilisée en pratique. L'idée de découper un réseau en sous réseaux de tailles plus petites et surtout adaptés aux besoins les plus courant est donc apparue.

Pour mettre en oeuvre des sous réseaux, il faut utiliser un certain nombre de bits initialement prévus pour l'id_machine et les affecter à l'identification des sous réseaux.
Cela a donc pour effet de __modifier le masque de sous réseau__ dans lequel un ou plusieurs "0" vont être remplacés par des "1" en fonction du nombre de sous réseaux que l'on veut mettre en place.

<span style="color:red">Attention!</span> L'identification des hôtes doit respecter la règle suivante:
> Si **n** représente le nombre de bits utilisés pour l'identification des hôtes, toutes les combinaisons de ces **n** bits sont possibles sauf deux:
> * L'une où tous les **n** bits sont à 1: il s'agit de l'adresse de diffusion,
> * L'autre où tous les *n* bits sont à 0: il s'agit de l'adresse de réseau.
> Par conséquent, le nombre de possibilités offertes pour **n** bits est de $$2^n -2$$.
Par contre, pour l'identification des sous réseaux toutes les combinaisons sont autorisées. Ainsi, si **x** représente le nombre de bits affectés aux sous réseaux, le nombre de possibilités sera de <span style="color:red">$$2^x$$</span>.

### Exemple
Dans un réseau de classe B, 16 bits sont normalement utilisés pour l'identification des machines (65 534 hôtes possibles). Ces possibilités n'étant jamais utilisées, on peut alors choisir d'utiliser:
* 8 bits pour réaliser des sous réseaux et 8 bits pour les adresses machines
  |  2 bits   |  14 bits  |   16 bits   |  =>   |  2 bits   |  14 bits  |     8 bits     |         8 bits         |
  | :-------: | :-------: | :---------: | :---: | :-------: | :-------: | :------------: | :--------------------: |
  | Id_classe | Id_réseau | Id_machines |  =>   | Id_classe | Id_réseau | SR bits 9 à 16 | Id_machines bits 1 à 8 |
  Le masque de sous réseau d'une classe B (sans sous réseau) est 255.255.0.0 (0.0 => 2 octects pour Id_machines).
  Ici on souhaite utiliser 8 bits pour les adresses machines (bit 1 à 8) et 8 bits pour les sous réseaux (bit 9 à 16). Dans ces conditions, les bits 1 à 8 du masque restent à "0" et les bits 9 à 16 passent à "1".

  Le nouveau masque de sous réseau devient: 1111 1111 . 1111 1111 . <span style="color:red">1111 1111</span> . 0000 0000 soit la valeur décimale 255.255.255.0 au lieu de 255.255.0.0.
  Ce masque permettra donc d'obtenir:
  * $$2^8 = 256$$ sous réseaux,
  * $$2^8 - 2 = 254$$ machines (hôtes par sous réseaux).

# Moyens mis en oeuvre pour palier aux limites d'IPv4
L'essor fulgurant d'Internet a engendré une très forte demande d'adresse IP. La répartition des adresses en classes est alors devenue mal adaptée à cette forte demande. Il a donc fallu faire face à une pénurie d'adresse IPv4.
Le nombre d'adresses publiques IPv4 est arrivé officiellement àà saturation le 3 février 2011.
Pour remédier à cela, plusieurs techniques ont été élaborées afin d'utiliser au mieux toutes les adresses disponibles.

## Réduction du nombre d'adresses IP utilisées
### NAT
Le manque d'adresses IPv4 (RFC 791 de 1981) a été dans un premier temps contourné grâce à l'utilisation de la technique de traduction d'adresses (NAT : Network Address Translation).
Avant l'apparition de la NAT, toutes les machines qui souhaitaient se connecter à Internet devaient avoir, chacune, une adresse IP publique.

IMAGE

Avec la NAT, c'est l'équipement qui est raccordé à Internet (routeur) qui détient une adresse publique. Tous les hôtes internes utilisent des adresses privées (qui ne sont pas routées sur Internet). Pour accéder à Internet, ils utilisent tous l'adresse publique du routeur. La fonction NAT installée sur le routeur permet alors de faire la correspondance entre les adresses privées internes et l'adresse publique qui permet d'accéder à Internet.

IMAGE


Cette technique a donc permis d'économiser un grans nombre d'adresses publiques.

### DHCP
L'autre technique qui a permis de mieux gérer les adresses est le DHCP (Dynamic Host Configuration Protocol).
Ce protocole permet d'attribuer automatiquement une configuration IP à un hôte. Ainsi, on utilise des adresses uniquement lorsqu'on en a besoin.

De cette façon, une même adresse peut être affectée à un hôte pendant une durée très courte (une journée) puis réaffectée à d'autres hôtes les jours suivants.

## Les classes d'adresses deviennent obsolètes avec l'apparition du système CIDR
En 1992, la RFC 1338 propose d'abolir la notion de classe qui n'était plus adaptée à la taille d'Internet.
Le <span style="color:red">*Classless Inter-Domain Routing*</span> est mis au point en 1993 (RFC1518) afin de diminuer la taille des tables de routage des routeurs. Ce but est atteint en agrégreant (regroupant) plusieurs entrées de cette table en une seule.
La distinction entre les adresses de classe A, B ou C a été ainsi rendue obsolète, de sorte que la totalité de l'espace d'adressage unicast puisse être gérée comme une collection unique de sous-réseaux indépendamment de la notion de classe. Le masque de sous-réseau ne peut plus être déduit de l'adresse IP elle-même.
Le masque de sous réseau est donné sous la forme "**/x** où **x** représente le nombre de bits identifiant le réseau.

### Exemple
Une entreprise a obtenu l'adresse IP *150.10.4.0/22*. Cette entreprise dispose de 3 agences réparties en France et souhaite créer un sous réseau pour chaque agence en ayant le maximum d'adresses IP disponibles.
> <span style="color:red">Important</span>: Pour créer des sous réseaux, le principe est toujours le même : on utilise des bits initialement prévus pour l'identification des hôtes. Celà implique donc une __modification du masque de sous réseau__ !

/22 signifie que l'on a un masque de 22 bits, soit en binaire 1111 1111 1111 1111 1111 1100 0000 0000.
Pour créer des sous réseaux, il faut utiliser des bits initialement prévus pour l'identification des hôtes (ici 10 bits)
Il faut donc déterminer le nombre de bits (que nous noterons *x*) qui permet d'avoir au moins 3 sous réseaux.
> Trouver *x* tel que $$2^x >= 3$$ : $$2^1 = 2$$, $$2^2 = 4$$. Il faut donc 2 bits pour obtenir les 3 sous réseaux.

Le masque des sous réseaux sera alors **/(22+2)** = <span style="color:red">**/24**</span>,
    soit en binaire 1111 1111 1111 1111 1111 11<span style="color:red">11</span> 0000 0000. Il reste alors 8 bits pour identifier les hôtes. 8 bits => $$2^8 -2 = 256 -2 = 254$$ hôtes par sous réseau soit 1016 hôtes au total.

Il faut maintenant définir les adresses de chaque sous réseau.
Adresse IP entreprise   150.10.4.0      1001 0110 0000 1010 0000 0100 0000 0000
Masque                  /22             1111 1111 1111 1111 1111 11<span style="color:red">00 0000 0000</span>

Puisqu'on veut créer des sous réseaux, il faut utiliser le __*nouveau masque /24*__
Adresse IP entreprise   150.10.4.0      1001 0110 0000 1010 0000 0100 0000 0000
Masque                  /24             1111 1111 1111 1111 1111 11<span style="color:red">**11** 0000 0000</span>

Pour obtenir les adresses IP des sous réseaux, il faut déterminer toutes les combinaisons possibles que peuvent prendre les 2 bits réservés aux sous réseaux et les intégrer dans l'adresse IP d'origine:
Puisqu'on a 2 bits, les différentes combinaisons de ces 2 bits sont 0 0; 0 1; 1 0 et 1 1.

Ce qui donne les adresses IP de sous réseau en binaire suivantes:
* Sous réseau 1: 1001 0110 0000 1010 0000 01<span style="color:red">00</span> 0000 0000,
* Sous réseau 2: 1001 0110 0000 1010 0000 01<span style="color:red">01</span> 0000 0000,
* Sous réseau 3: 1001 0110 0000 1010 0000 01<span style="color:red">10</span> 0000 0000,
* Sous réseau 4: 1001 0110 0000 1010 0000 01<span style="color:red">11</span> 0000 0000.

On obtient alors les adresses IP de sous réseau en décimal pointé suivantes:
* Sous réseau 1: 150.10.4.0 (octet 0000 01<span style="color:red">00</span> = <span style="color:red">4</span>)
* Sous réseau 2: 150.10.5.0 (octet 0000 01<span style="color:red">01</span> = <span style="color:red">5</span>)
* Sous réseau 3: 150.10.6.0 (octet 0000 01<span style="color:red">10</span> = <span style="color:red">6</span>)
* Sous réseau 4: 150.10.7.0 (octet 0000 01<span style="color:red">11</span> = <span style="color:red">7</span>)

Attention !
> Le réseau de l'entreprise ainsi que le réseau 1 ont pour adresse 150.10.4.0. Ces deux adresses sont techniquement différentes car elles n'ont pas le même masque (/22 et /24).

Le système CIDR permet de créer des sous réseaux pouvant tous accueillir le même nombre d'hôtes. Dans l'exemple précédent, nous avons vu que l'on pouvait créer 4 sous réseaux pouvant accueillir chacun 254 hôtes. Dans la réalité, les besoins des différents sous réseaux sont rarement identiques. Au contraire, certains sous réseaux ont des besoins en hôtes beaucoup plus importants que d'autres.

L'idéal serait donc de pouvoir adapter la taille des sous réseaux en fonction du nombre d'hôtes utilisés. Cela permettrait de ne pas réserver inutilement des adresses IP. C'est ce que permet de faire la technique VLSM.

## La technique VLSM
La technique <span style="color:red">**VLSM**</span> (<span style="color:red">***Variable-Length Subnet Mask***, *masque de longueur variable*) permet le découpage de l'espace d'adressage en blocs de tailles variables, permettant une utilisation plus efficace de l'espace d'adressage.

## Nouveau protocole d'adressage IPv6
Les spécifications du nouveau protocole IPv6 sont apparues en décembre 1995 (RFC 1883).
Une adresse IPv6 est longue de 128 bits, soit 16 octets, contre 32 bits (4 octets) pour le protocole IPv4.

### Notation d'une adresse IPv6
La notation décimale pointée employée pour les adresses IPv4 est abandonnées au profit d'une écriture hexadecimale dans laquelle 8 groupes de 2 octets (soit 16 bits par groupe) sont séparés par le signe "**:**".
Par exemple **2001:0db8:0000:0000:0000:85a3:ac1f:8001**.

Dans cette notation il est permis d'omettre les *zéros non significatifs* situés à gauche de chaque groupe de 4 chiffres hexadécimaux.
Par exemple **2001:0db8<span style="color:red">:0:0:0:</span>85a3:ac1f:8001**.

De plus, une suite de un ou plusieurs groupes consécutifs valant zéro peut être omise (seulement ***une seule fois***). Ainsi, l'adresse va être encore raccourcie en retirant la suite "0:0:0".
Par exemple **2001:0db8<span style="color:red">::</span>85a3:ac1f:8001**.

### Catégories d'adresses et préfixes associés
Une adresse IPv6 se compose de deux parties:
* Les 64 premiers bits de l'adresse IPv6 (<span style="color:red">**préfixe**</span>) servent généralement à l'adresse de sous réseau.
* Les 64 bits suivants identifient l'hôte à l'intérieur du sous réseau: ce découpage joue un rôle un peu similaire aux masques de sous réseau IPv4.

IMAGE

IPv6 prévoit différentes catégories d'adresses prédéfinies telles que les **adresses globales point à point (unicast)**, les **adresses locales uniques** (préfixe fc00::/7), les **adresses de lien local** (*link-local*, préfixe fe80::/10) et les **adresses de multidiffusion** (*multicast*, préfixe ff00::/8).

Enfin, les adresses IPv4 peuvent être écrites en utilisant la représentation de l'adresse en notation décimale pointée précédée d'un double deux-points, comme par exemple : "**::ffff:172.31.254.46**" ou la représentation normale d'une adresse IPv6 "**::ffff:ac1f:fe2e**".
