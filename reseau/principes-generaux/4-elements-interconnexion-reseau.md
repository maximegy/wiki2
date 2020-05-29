---
title: 4 Elements d'Interconnexion des réseaux
description: 
published: true
date: 2020-05-29T22:17:33.973Z
tags: 
---

# Vue d'ensemble
Les LAN (Local Area Network N°2) couvrant une région géographique relativement peu étendue. Ils relient des stations de travail, des périphériques, des terminaux et d'autres unités à l'intérieur d'un bâtiment ou d'autres zones géographiques limitées.

# Les éléments de base d'un LAN
## La topologie d'un réseau
La *topologie* définit la structure du réseau. La définition de la topologie comprend en réalité deux parties:
* la **topologie physique** qui représente la disposition effective des câbles, le média,
* la **topologie logique** qui précise la façon dont les hôtes accèdent au média, la méthode d'accès.

Les topologies physiques couramment utilisées dans la figure ci-dessous:

IMAGE


* Topologie en bus: tous les hôtes sont directement connectés à un seul segment (longueur de câble),
* Topologie en anneau: chaque hôte est connecté à son voisin. Le dernier hôte se connecte au premier. Cette topologie crée un anneau physique de Câble,
* Topologie en étoile: tous les câbles sont raccordés à un point central (commutateur ou un concentrateur),
* Topologie maillée: utilisée lorsqu'il ne faut absolument pas qu'il y ait de rupture de communication. Chaque hôte possède ses propres connexions à tous les autres hôtes (réseau Internet).

> La topologie logique d'un réseau est la méthode qu'utilisent les hôtes pour communiquer par le média. Les deux types de topologie les plus courants sont **le passage de jeton et le broadcast**.

Avec la **méthode du passage du jeton**, l'accès au réseau est contrôlé en passant un jeton électronique de manière séquentielle à chaque hôte. Lorsqu'un hôte reçoit le jeton, cela signifie qu'il peut transmettre des données sur le réseau pendant un certain temps. Passé ce délai, le jeton passe automatiquement à l'hôte suivant.
De cette manière, aucun hôte ne peut monopoliser le réseau qui est alors accessible à tous. Si l'hôte n'a pas de données à transmettre, il passe le jeton à l'hôte suivant et le processus est répété.
Ainsi la technologie <span style="color:red">Token ring</span> d'IBM fonctionne selon la méthode du passage du jeton.

Le **broadcast** (**diffusion**) signifie simplement que chaque hôte envoie ses données à tous les autres hôtes sur le média du réseau. Les stations n'ont pas à respecter un certain ordre pour utiliser le réseau; il s'agit d'une méthode de type "premier arrivé, premier servi". La méthode la plus courant est <span style="color:red">CSMA/CD</span>.
> CSMA/CD signifie <span style="color:red">Carrier Sense Multiple Access with Collision Detection</span> (Accès multiple par écoute de porteuse et détection de collision). C'est un protocole qui gère le partage de l'accès physique au réseau Ethernet selon la norme IEEE 802.3.

### Fonctionnement du protocole CMSA/CD
* CMSA (accès au support par écoute de la porteuse):
  Cette méthode permet à une station d'écouter le support physique de liaison (câble ou fibre) pour déterminer si une autre station transmet une trame de données (niveau déterminé de tension électrique ou de lumière). Si tel n'est pas le cas (donc s'il n'y a pas eu de signal), elle suppose qu'elle peut émettre.
* CD (détection de collision)
  L'accès multiple implique que plusieurs stations peuvent émettre au même moment ce qui provoque une **collision** (donc une perte de donénes). Comme les stations détectent aussi les collisions (niveau du signal différent) elles savent qu'elles doivent réémettre après avoir attendu pendant un délai aléatoire.

  Ce type de protocole est dit "probabiliste", c'est à dire qu'il n'est pas possible de déterminer avec certitude le délai d'envoi d'un message. Rappelons que dans un réseau Ethernet les stations se partagent le même média de communication, qu'il n'y a pas de jeton ni de priorité d'émission.

### CSMA/CD en pratique
* Si une station veut émettre, elle écoute le réseau (*Listen before talking*) pour savoir s'il y a déjà une autre émission en cours (présence ou non de porteuse). Si oui elle attend, sinon elle émet.
* La station émet pendant un minimum de temps, ceci afin que son émission puisse être détectée par les autres stations et donc d'éviter d'autres émissions simultanées. Cependant elle continue à écouter pendant son émission afin de vérifier que ses données n'ont pas été perturbées (*Listen while talking*).
* Si une collision a lieu, les deux machines interrompent leur communication et attendent un délai aléatoire (déterminé par l'algorithme de *backoff* exponentiel), puis la première ayant passé ce délai peut alors réémettre. Si le nombre de collisions dépasse un certain seuil (généralement 16), on considère qu'il y a une erreur fatale et l'émission s'interrompt avec la condition "**excessive collision**.

> La technologie <span style="color:red">Ethernet</span> fonctionne en Broadcast et utilise le protocole CSMA/CD.

Pour information, le Wi-Fi utilise une méthode similaire: **CSMA/CA**
> <span style="color:red">CSMA/CA</span> signifie Carrier Sense Multiple Access with Collision Avoidance (Accès multiple par écoute de porteuse et <span style="color:red">évitement</span> de collision).
C'est un protocole qui gère le partage de l'accès au réseau WiFi, selon la norme IEEE 802.11.

Les principaux symboles utilisés pour représenter les réseaux sont :



IMAGES


FDDI utilise la fibre optique (en multimode => 2km, et en monomode => 60km).
Il s'agit en fait d'une paire d'anneaux (l'un est dit *primaire*, l'autre, permettant de rattraper les erreurs du premier, est dit *secondaire*). FDDI est un protocole utilisant un anneau à jeton à détection et correction d'erreurs.

## Les unités LAN dans une topologie
Les unités directement connectées à un segment de réseau sont appelées hôtes. Ces hôtes peuvent être des ordinateurs de bureau, des serveurs, des imprimantes ainsi que nombreux autres types d'équipements. Ces unités fournissent les connexions réseau aux utilisateurs grâce auxquelles ils peuvent partager, créer et obtenir des informations.
Les unités hôte n'appartiennent à aucune couche. Elles sont connectées physiquement au média réseau grâce à leur carte réseau et les fonctions des autres couches OSI sont exécutées par des logiciels exploités par l'hôte. Cela signifie que les unités hôte fonctionnent au niveau des sept couches du modèle OSI. Elles se chargent du processus d'encapsulation et de désencapsulation (ou décapsulation) afin de pouvoir envoyer ou recevoir des messages.

## Les médias
La fonction de base des médias consiste à acheminer un flux d'informations dans un réseau.
Les 3 catégories de médias les plus utilisés sont:
* Les cuivres
  Ils permettent la propagation de signaux électriques numériques ou analogiques sur des distances inférieures à 100m. Les deux principaux types sont:
  1. Les Câbles à paires torsadées
   La norme ISO-CEI 11801 définie les types de blindages et les appelations normalisées associées. La dénomination acutelle est: **X X / Y Z Z**

   |             **X X**              |              **Y**               |                 **Z Z**                 |
   | :------------------------------: | :------------------------------: | :-------------------------------------: |
   |         Blindage général         |        Blindage par paire        |              Type de paire              |
   | U : Unshielded : Pas de blindage | U : Unshielded : Pas de blindage |   TP: Twisted Pair : Paires torsadées   |
   |   F : Foiled : Blindage écran    |   F : Foiled : Blindage écran    | TQ: Twisted Quad : Structure en quartes |
   |  S : Shielded : Blindage tresse  |                                  |                                         |
   |       SF : Tresse + écran        |                                  |                                         |

IMAGES

  1. Les Câbles coaxiaux
   Ce sont les câbles de type câble antenne TV. L'emploi de ce type de câble est devenu rare dans un LAN, sauf en environnement industriel pour la bonne protection contre les perturbations électromagnétiques.
* Les fibres optiques
  Elles permettent la propagation de signaux lumineux sur de longues distances: quelques dizaines de Kilomètres sans régénérateur, des milliers de Kilomètres avec régénérateur.
* Les liaisons Hertziennes
  Utilisent la propagation d'ondes électromagnétiques, comme le WiMAX, le WIFI, etc.

Les médias sont considérés commes des composants de <span style="color:red">couche 1</span> du modèle OSI.
On peut construire des réseaux informatiques en utilisant plusieurs types de médias différents. Chaque type de média présente des avantages et des inconvénients.
Les principaux critères de choix sont:
- La longueur maximale,
- Le débit supporté,
- Le coût,
- La facilité d'installation...

## Les répéteurs
L'un des désavantages du câble à paire torsadée non blindée est la longueur. En effet, dans un réseau, la longueur maximale d'un tel câble est de 100 mètres. Pour prolonger un réseau au-delà de cette limite, il faut ajouter une unité appelée *répéteur*.
Le terme répéteur désigne habituellement une unité à un seul port "d'entrée" et à un seul port de "sortie".
> La fonction du répéteur est de régénérer les signaux et de les resynchroniser au niveau du bit pour leur permettre de voyager sur de plus longues distances dans le média.

IMAGE

Les répéteurs sont des unité de couche 1 car ils agissent uniquement au niveau du bit et ne soucient d'aucune autre information.

IMAGE

## Les concentrateurs - ou hubs
Le but du concentrateur est de régénérer et de resynchroniser les signaux réseau. Il fait cela au niveau du bit pour un grand nombre d'hôtes (par exemple 4,8,12,24 ou même 48) en utilisant un processus appelé concentration. Cette définition est très proche du répéteur, c'est pour cela que le concentrateur est souvent appelé *répéteur multiport*.
On utilise un concentrateur pour créer un point de connexion central. Les concentrateurs sont considérés comme des unités de couche 1 parce qu'ils ne font que regénérer le signal et le diffuser par tous leurs ports.
Une autre classification divise les concentrateurs en unités intelligentes et unités non intelligentes. Les concentrateurs intelligents sont dotés de **ports console**, ce qui signifie qu'ils peuvent être programmés pour gérer le trafic réseau. Les concentrateurs non intelligents répètent et régénèrent uniquement le signal.

IMAGE


## Les cartes réseau
En anglais NIC pour Network Interface Card.
En traitant la carte réseau, nous allons maintenant passer à la couche 2, la couche liaison de données, du modèle OSI. Pour ce qui est de son aspect physique, une carte réseau (ou NIC) est une plaquette de circuits imprimés logée dans l'emplacement d'extension d'un bus, sur la carte mère d'un ordinateur ou sur un périphérique. Certains l'appellent aussi *adaptateur réseau*. Sa fonction consiste à adpater l'unité hôte au média du réseau.
Les cartes réseaux sont considérées comme des composants de couche 2 parce que chaque carte réseau porte un nom de code unique, dans le monde, appelé adresse MAC.
Cette adresse est utilisée pour contrôler la communication des données de l'hôte dans le rseau, notamment la gestion des trames. Les trames qui circulent entre deux hôtes contiennent les adresses MAC de l'hôte source et celle de l'hôte de destination.
La carte réseau contrôle l'accès de l'hôte au média. Pour celà on doit y installer un programme appelé **Pilote** ou **Driver** qui permet de faire la liaison entre le système d'exploitation de l'hôte et le type de réseau auquel il est connecté.

IMAGE

## Les ponts
Le rôle du pont est de filtrer le trafic d'un LAN pour le confiner au niveau local, tout en établissant une connectivité avec d'autres parties (segments) du LAN.
> Comment fait le pont pour différencier le trafic local du trafic non local ?
> Il regarde tout simplement l'adresse locale. Comme chaque unité réseau possède une adresse MAC unique, le pont effectue le suivi des adresses MAC se trouvant de chacun de ses côtés et prend des décisions en fonction de cette liste d'adresses. Si l'adresse MAC de destination fait partie de la liste, alors un pont est une unité de couche 2 car il gère le traffic des trames grâce aux MAC.

Le terme pont fait traditionnellement référence à une unité possédant deux ports seulement. On peut cependant rencontrer des ponts ayant 3 ports ou plus. Un pont se définit véritablement par la manière dont le filtrage est réalisé (couche 2 => adresse MAC).

IMAGE

## Les commutateurs - Switch
Le commutateur est une unité de couche 2 tout comme le pont. En fait, un commutateur est également appelé pont multiports tout comme le concentrateur qui est un répéteur multiport. La différence entre le concentrateur et le commutateur est que ce dernier **prend des décisions en fonction des adresses MAC** tandis que le concentrateur ne prend aucune décision. En raison des décisions qu'il prend, le commutateur rend le LAN beaucoup plus efficace:
Il transfère les données en "<span style="color:red">commutant</span>" (dirigeant) celles-ci uniquement au port auquel le destinataire est connecté. Utilisation de tout la <span style="color:red">bande passante disponible</span>. Par contraste, un concentrateur achemine les données à tous les ports, de sorte que tous les hôtes doivent examiner et traiter (accepter ou rejeter) toutes les trames. Dans ce cas, il y a partage de la bande passante.

Le symbole d'un commutateur, comme présenté ci-dessous, contient des flèches qui représentent les chemins distincts que peuvent emprunter les données dans un commutateur, contrairement au concentrateur où toutes les données emprutent tous les chemins.

IMAGE


##Les Routeurs - router
Le routeur travaille au niveau de la couche 3 (couche réseau du modèle OSI). Cela lui permet de prendre des décisions selon des groupes d'adresses réseau (adresses IP). Les routeurs peuvent aussi connecter différentes technologies de couche 2, telles qu'Ethernet, Token Ring et FDDI.
Le rôle du routeur consite à examiner les <span style="color:red">paquets</span> entrants (données de couche 3), à choisir le meilleur chemin pour les transporter sur le réseau et à les commuter ensuite au port du sortie approprié. Sur les grands réseaux, les routeurs sont les équipements de régulation du trafic le plus important.
En raison de leur capacité d'acheminer les paquets en fonction des informations de couche 3, les routeurs sont devenus le **backbone** (**épine dorsale**) d'Internet.

Un routeur peut avoir plusieurs types différents de port d'interface:
* **port série**, qui est une connecion de réseau longue distance (WAN),
* **port console**, pour établir une connexion directe au routeur pour le configurer,
* **port Ethernet**, qui permet de connecter le routeur au réseau local (LAN).

IMAGE

# Les notions de bases sur les flux de donénes dans les LAN
## Rappels sur l'encapsulation
Ce procédé a été décrit au chapitre "Modèle OSI". Chaque couche est en relation avec la couche supérieure et inférieure. La couche N travaille avec la couche N+1 et N-1. L'ensemble des informations que s'échangent deux couches s'appelle: <span style="color:red">**PDU (Protocol Data Unit - Unité de données de protocole)**</span>.
* Les trois couches supérieures (*application*,*présentation* et *session*) préparent les donnés pour la transmission en créant un format commun.
* La couche *transport* divise les données en portions plus petites et le PDU transmis à la couche réseau est le **segment**. La numérotation des segments permet à l'hôte récepteur de replacer les données dans le bon ordre.
* La couche *réseau* encapsule ensuite le segment en ajoutant une adresse réseau d'origine et une adresse destination, habituellement appelée une adresse IP et transmet le PDU nommé **paquet** à la couche 2.
* La couche *liaison de données* poursuit l'encapsulation en ajoutant l'adresse locale (MAC) d'origine et celle de destination du paquet. Elle transmet ensuite le PDU nommé **trame** à la couche Physique qui convertit les données en vits et les envoie sur le média.

## La circulation des paquets dans les unités de couche 1
Certaines unités fonctionnent uniquement au niveau de la couche 1. Le flux des paquets à travers les unités de couche 1 est simple. Les médias physiques sont considérés comme des composants de couche 1.
Si les unités de couche 1 sont passives (par exemple, les connecteurs, les prises, les tableaux de connexions et les médias physiques), les bits traversent simplement avec le moins de distortion (déformation) possible.
Si les unités de couche 1 sont actives (par exemple, les répéteurs ou les concentrateurs qui possèdent une alimentation electrique), les bits sont régénérés et resynchonisés.
Les équipements de couche 1 n'examinent ni les en-têtes, ni les données des paquets encapsulés. Ils ne transmettent que des bits (impulsions électriques ou impulsions lumineuses pour fibre optique par exemple).

## La circulation des paquets dans les unités de couche 2
Il est important de ne pas oublier que les segments sont contenus dans les paquets et que les paquets sont eux-mêmes contenus dans des trames. Les trames circulent ensuite sur le réseau.

Certaines unités appartiennent en fait aux couches 1 et 2 du modèle OSI. Ainsi, les cartes réseau (NIC), les ponts et les commutateurs se basent sur les adresses MAC pour diriger les paquets, c'est pourquoi on les considère comme des équipements de couche 2. L'adresse MAC unique réside sur la carte réseau et est utilisée pour créer la trame.
Ces équipements fournissent également la connectique (prise RJ45) pour le raccordement au réseau. De ce fait, ils appartiennent aussi à la couche physique (couche 1).

Le rôle des ponts et des commutateurs est d'examiner l'adresse MAC de destination des paquets entrants. Le commutateur fonctionne de la façon suivante:
> Le commutateur accepte une trame de données (couche 1), il désencapsule la trame (couche 2) puis il la lit en examinant l'adresse MAC de destination s'il connait l'adresse MAC il réencapsule la trame (couche 2) et achemine la trame (il la commute) vers le port approrié et la transmet (travail de la couche 1). S'il ne connait pas l'adresse MAC, il rejette la trame.

## La circulation des paquets dans les unités de couche 3
Le routeur est le principal équipement de couche réseau traité dans le cadre de ce chapitre. Le routeur fonctionne en réalité au niveau de la couche 1 (bits achemindé sur le média aux interfaces du routeur), au niveau de la couche 2 (trames commutées d'une interface à une autre)) selon les informations du paquet et au niveau de la couche 3 (décisions de routage).
Le flux des paquets à travers les routeurs (c'est à dire la sélection du meilleur chemin et la cimmutation au port ou inteface de sortie approprié) repose sur les adresses réseau de couche 3 (Adresse IP).

Une fois le bon port sélectionné, le routeur encapsule de nouveau le paquet dans une trame pour l'acheminer vers sa prochaine destination. Ce processus se produit à chaque routeur rencontré sur le chemin entre l'hôte source et l'hôte de destination.

# Aspects techniques complémentaires
Les équipements réseaux peuvent proposer des aspects techniques complémentaires.

* Equipements empliables:
  Matériels que l'on peut emplier les uns sur les autres. Ils disposent, entre autres, d'un port permettant de le relier à d'autres équipements. Plusieurs équipements empilés apparaissent comme une seule unité.
  Par exemple: 3 commutateurs de 24 ports empilés ) 1 commutateur de 72 ports.
* Equipements cascadables:
  Equipements qui peuvent être reliés entre eux par un câble et éventuellement situés dans des locaux différents. Ils disposent d'un port appelé UPLINK.
* Equipements rackables:
  Equipements se présentant sous forme d'un châssis que l'on peut insérer dans une baie ou armoire.
* Equipements manageables:
  Equipements qui peuvent être administrés par un logiciel et accessible de l'extérieur, via le réseau et très souvent par l'intermédiaire d'un simple navigateur (interface Web).
* Techniques de commutation:
  * commutation **à la volée** (on the fly) qui consiste à retransmettre la trame reçue vers le port de destination avant même qu'elle soit entièrement lue,
  * commutation **par validation** (buffered ou store and forward) qui consiste à "bufferiser" ou stocker la trame en mémoire puis à la vérifier avant de la retransmettre.
  La première technique est plus rapide mais peut laisser passer des trames non valides. Le seconde bloque les mauvaises trames mais introduit une **latence** (temps de retard) supplémentaire.