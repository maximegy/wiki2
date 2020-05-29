---
title: Communications sur un réseau
description: Notions de base et vocabulaire
published: true
date: 2020-05-29T22:13:14.227Z
tags: 
---

# Eléments de communication
## Principaux éléments de communication
Une communication commence avec l'envoi d'un message (des informations) d'un individu ou un périphérique à un autre.
On échange par de nombreuses méthodes de communication différentes mais elles ont toutes en commun:
- Une <span style="color:red">source</span> du message, l'expéditeur.
  > Les sources d'un message sont les personnes ou les périphériques électroniques qui doivent envoyer un message à d'autres individus ou périphériques.
- Une <span style="color:red">destination</span>, le destinataire.
  > La destination reçoit le message et l'interprète.
- Un <span style="color:red">canal</span>.
  > Il est constitué du support qui fournit la voie par laquelle le message peut se déplacer depuis la source vers la destination.

> Imaginons que nous souhaitons communiquer par des mots, des images et des sons. Chacun de ces messages peut-être envoyé à travers un réseau en étant au préalable converti en chiffres binaires, ou <span style="color:red">bits</span>. Ces bits sont ensuites codés pour former un signal qui peut être transmis via le support approprié. Dans un réseau informatique, le support est généralement un type de transmission par câble ou sans fil.

## Communication des messages
En théorie, une communication unique, comme une vidéo ou un mail, pourraient être transmis à travers un réseau depuis une source vers une destination sous la forme d'un flux continu et volumineux de bits.
Si des messages étaient réellement transmis de cette manière, alors aucun autre périphérique ne serait en mesure d'envoyer ou de recevoir des messages sur ce même réseau pendant le transfert de ces données. Ces flux de données volumineux entraîneraient des retards conséquents.

Il existe donc une meilleure approche qui consiste à diviser les données en parties de tailles moins importante et plus facilement gérables pour les envoyer sur le réseau. Cette division du flux de données en parties plus petites est appelée <span style="color:red">segmentation</span>. Cette dernière présente deux avantages:
1. Par l'envoi de parties individuelles de plus petite taille depuis une source vers une destination, de nombreuses conversations différentes peuvent s'entremêler sur le réseau. Le processus qui sert à entremêler les parties des différentes conversations entre elles sur le réseau est appelé <span style="color:red">multiplexage</span>.
2. La segmentation peut augmenter la fiabilité des communications réseau. Les différentes parties de chaque message n'ont pas besoin de parcourir le même chemin sur le réseau depuis la source jusqu'à la destination. Si un chemin particulier devient encombré en raison du trafic de données ou qu'il connaît une défaillance, les parties individuelles du message peuvent toujours être adressées à la destination via d'autres chemins. Si une partie du message ne parvient pas à sa destination, seules les parties manquantes seront transmises à nouveau.

L'inconvénient que présente l'utilisation de la segmentation et du multiplexage pour la transmission des messages à travers un résau réside dans le niveau de complexité ajouté au processus.
> Imaginons que nous devions une lettre de 100 pages mais que chaque enveloppe ne peut contenir qu'une seule page. Le processus d'écrire de l'adresse, de mise sous enveloppe, d'envoi, de réception et d'ouverture de la totalité des 100 enveloppes prendrait beaucoup de temps à l'expéditeur et au destinataire.

## Composants du réseau
Le chemin emprunté par un message depuis une source vers une destination peut être aussi simple sue le connexion entre deux ordinateurs ou aussi complexe qu'un réseau parcourant de globe terrestre.
Cette <span style="color:red">infrastructure réseau</span> constitue la <span style="color:red">plateforme réseau</span>. Elle fournit le canal stable et fiable à travers lequel nos communications peuvent s'établir.

Les <span style="color:red">périphériques</span> et les <span style="color:red">supports</span> représentent les éléments physiques ou le matériel du réseau. Le matériel correspond souvent aux composants visibles de la plateforme réseau, tel qu'un ordinateur portable, un ordinateur de bureau, un commutateur ou le câblage qui sert à relier les périphériques. Parfois, certains composants ne sont pas visibles. Dans le cas d'un support sans fil, les messages sont transmis à travers l'aur, à l'aide d'une fréquence radio ou d'ondes infrarouges invisibles.

Les <span style="color:red">services</span> et les <span style="color:red">processus</span> constituent les programmes de communication, appelés logiciels, qui sont exécutés sur les périphériques réseau.
* Un service réseau fournit des informations en réponse à une demande. Les services incluent de nombreuses applications réseau courantes et les services d'hébergement Web.
* Les processus fournissent les fonctionnalités qui dirigent et déplacent les messages à travers le réseau. Les processus nous semblent moins évidents, mais ils sont essentiels au fonctionnement des réseaux.

## Périphériques finaux
Les péripériques réseau auxquels les personnes sont le plus habituées sont appelés <span style="color:red">périphériques finaux</span>. Ces périphériques forment l'interface entre le réseau humain et le réseau de communication sous-jacent. Certains de ces périphériques finaux sont les suivants:
* Ordinateurs (stations de travail, portables, serveurs, ...),
* Imprimantes réseaux,
* Téléphones IP,
* Caméras de surveillance,
* Périphériques portables mobiles (lecteurs de code barres, smartphone, ...),
* ...

Dans le cas d'un réseau, les périphériques finaux sont appelés <span style="color:red">hôtes</span>. Un hôte constitue soit la source, soit la destination d'un message transmis à travers le réseau. Pour qu'il soit possible de faire une distinction entre les hôtes, chaque hôte sur un réseau est identifié par une <span style="color:red">adresse</span>. Lorsqu'un hôte démarre une communication, il utilise l'adresse de l'hôte de destination pour indiquer où le message doit être envoyé.

Dans les réseaux actuels, un hôte peut jouer le rôle de <span style="color:red">client</span>, de <span style="color:red">serveur</span> ou les deux. Le logiciel installé sur l'hôte détermine son rôle sur le réseau:
* Les <span style="color:red">serveurs</span> sont des hôtes équipés de logiciels leur permettant de fournir des informations et des services, commes les emails, des pages web, à d'autres hôtes sur le réseau.
* Les <span style="color:red">clients</span> sont des hôtes équipés d'un logiciel qui leur permet de demander des informations auprès du serveur et de les traiter et/ou les afficher.

## Périphériques intermédiaires
En plus des périphériques finaux, les réseaux dépendent de <span style="color:red">périphériques intermédiaires</span> pour fournir une connectivité et travailler en arrière-plan, afin de garantir le flux des données à travers le réseau. Ces périphériques connectent les hôtes individuels au réseau et peuvent connecter plusieurs réseaux individuels afin de former un <span style="color:red">interréseau</span>. Ces périphériques réseau intermédiaires peuvent être:
* Périphériques d'accès réseau (concentrateurs, commutateurs et point d'accès sans fil),
* Périphériques interréseaux (routeurs),
* Serveurs et modems de communication,
* Périphérique de sécurité.

La gestion des données lors de leur passage à travers le réseau constitue également l'un des rôles des périphériques intermédiaires. Ces périphériques utilisent l'adresse d'hôte de destination, avec les informations concernant les interconnexions réseau, de manière à déterminer le chemin que doivent emprunter les messages à travers le réseau.
Les processus qui s'exécutent sur les périphériques du réseau intermédiaire remplissent les fonctions suivantes:
- régénérer et retransmettre des signaux de données,
- gérer des informations indiquant les chemins qui existent à travers le réseau et l'interréseau,
- indiquer aux autres périphériques les erreurs et les échecs de communication,
- diriger des données vers d'autres chemins en cas d'échec de liaison,
- classifier et diriger des messages en fonction des priorités QoS,
- autoriser ou refuser le flux de données, selon des paramètres de sécurité.

## Supports réseau
La communication à travers un réseau s'effectue sur un support. Ce support fournit le canal via lequel le message se déplace de la source à la destination.

Les réseaux modernes utilisent principalement trois types de supports pour interconnecter des périphériques et fournir le chemin par lequel des données peuvent être transmises. Ces supports sont les suivants:
* Fils métailliques dans des câbles,
* Câbles en fibres optiques (Fibres de verre ou optiques de plastiques),
* Transmission sans fil.

Le codage du signal qui doit se produire afin de transmettre le message diffère selon le type de support. Sur des <span style="color:red">fils métalliques</span>, les données sont coddées en <span style="color:red">impulsions électriques</span> qui correspondent à des modèles spécifiques. Les transmissions par <span style="color:red">fibre optique</span> s'effectuent via des <span style="color:red">impulsion de lumière</span>, dans des plages de lumières infrarouges ou visibles. Dans les <span style="color:red">transmissions sans fil</span>, des modèles d'<span style="color:red">ondes electromagnétiques</span> illustrent les différentes valeurs de bit.

Les différents types de supports réseau possèdent divers avantages et fonctionnalités. Tous les supports rréeau ne possèdent pas les mêmes caractéristiques et ne conviennent pas pour les mêmes objectifs.
Les critères de choix d'un support réseau sont:
* La distance sur laquelle les supports peuvent transporter correctement un signal,
* L'environnement dans lequel les supports doivent être installés,
* La quantité de données et le débit de la transmission,
* Le coût des supports et de l'installation.

# Réseaux locaux, métropolitain, étendus et interréseaux
Les infrastructures réseau peuvent considérablement varier selon:
- la taille de la zone couverte,
- le nombre d'utilisateurs connectés,
- le nombre et les types de services disponibles.
Le type de réseau local (local, métropolitain, étendu) dépendra donc de ces différents critères.

## Réseaux locaux
Un réseau individuel s'étend généralement sur une zone géographique unique et fournit des services et des applications aux personnes au sein d'une structure organisationnelle commune, telle qu'une entreprise, un campus, une région ou une maison.
Ce tpe de réseau est appelé <span style="color:red">réseau local</span>: 
> **LAN** : <span style="color:red">L</span>ocal <span style="color:red">A</span>rea <span style="color:red">N</span>etwork
> **RLE** : <span style="color:red">R</span>éseau <span style="color:red">L</span>ocal d'<span style="color:red">E</span>ntreprise

En règle général, un réseau local est <span style="color:red">*administré par une organisation unique*</span>. Le contrôle administratif qui gère les stratégies de sécurité et de contrôle d'accès s'applique au niveau du réseau.

## Réseaux métropolitains
Certaines organisations (un campus, une ville) doivent gérer des sites distants les uns des autres de quelques kilomètres. Ces différents sites regroupent un ensemble d'ordinateurs et fournissent deifférents services.
Ce type de réseau est appelé <span style="color:red">réseau métropolitain</span>: **MAN** : <span style="color:red">M</span>etropolitan <span style="color:red">A</span>rea <span style="color:red">N</span>etwork

Ces réseaux utilisent généralement des fibres optiques pour relier les différents sites. Certaines technologies  utilisées dans ce but sont l'ATM ou le FDDI. Ces anciennes technollogies sont en passe d'être remplacées par le Gigabit Ethernet utilisé dans de nombreux MAN, comme dans les LAN.
Comme pour les réseaux locaux, les réseaux métropolitains sont <span style="color:red">*administrés par une organisation unique*</span>.

## Réseaux étendus
Lorsqu'une entreprise ou une organisation dispose d'emplacements (sites) séparés par d'importantes distances géographiques, il peut être nécessaire d'utiliser un fournisseur de services de télécommunications pour interconnecter les réseaux locaux à ces différents emplacements. Les fournisseurs de services de télécommunications utilisent d'importants réseaux régionaux pouvant parcourir de longues distances.

Les organisation individuelles utilisent généralement des connexions via un réseau de fournisseurs de services de télécommunications. Ces réseaux qui connectent des réseaux locaux à des emplacements géographiquement séparés sont appelés <span style="color:red">réseaux étendus</span>:
> **WAN** : <span style="color:red">W</span>ide <span style="color:red">A</span>rea <span style="color:red">N</span>etwork.

Bien que l'organisation gère l'ensemble des stratégies et de l'administration des réseaux locaux aux deux extrémités de la connexion, les stratégies au sein du réseau du fournisseur de services de communications sont gérées par lui-même.
Les réseaux étendus utilisent des périphériques réseau spécialement conçus pour effectuer les interconnexions entre les réseaux locaux : les <span style="color:red">routeurs</span>.

## Interréseau
La plupart d'entre nous devons communiquer avec une ressource sur un autre réseau, en dehors de notre organisation locale. Parmi les exmples de ce type de communication, citons:
* l'envoi d'un courriel à un ami se trouvant dans un autre pays,
* l'accès à des informations ou à des produits sur un site Web,
* l'obtention d'un fichier à partir de l'ordinateur d'un voisin,
* la messagerie instantanéee avec une connaissance qui se trouve dans une autre ville,
* le suivi des résultats sportifs de son équipe favorite sur un téléphone portable.

Pour répondre à ces besoins humains en matière de communication il faut interconnecter une multitude de réseaux. L'interréseau public le plus connu et dont l'utilisation est la plus répandue est *Internet*.
Garantir une communication efficace à travers cette infrastructure diverse implique l'application de technologies et de protocoles cohérents et communément reconnus, ainsi que la coopération entre de nombrex organismes.

Le terme <span style="color:red">intranet</span> est souvent utilisé pour faire référence à un réseau LAN privé qui appartient à une entreprise ou une administration et auquel peuvent accéder uniquement ses membres, ses employés ou des tierces personnes autorisées. Un intranet est un réseau LAN sur lequel on utilise les mêmes technologies que sur Internet.

## Représentations du réseau et symboles utilisés
Afin de pouvoir visualiser l'organisation et le fonctionnement d'un réseau, il est indispensable de recourir à des représentations et des graphiques visuels.
Comme pour tout langage, celui propre au réseau utilise un ensemble commun de symboles pour représenter les différents périphériques finaux, réseaux et supports.
Les principaux symboles utilisés en réseau sont:

<center>

|                                               Icône                                               |       Description       |                                                   Icône                                                    |        Description         |
| :-----------------------------------------------------------------------------------------------: | :---------------------: | :--------------------------------------------------------------------------------------------------------: | :------------------------: |
|              ![Routeur](/uploads/communication-sur-un-reseau/routeur.png "Routeur")               |         Routeur         |             ![Commutateur](/uploads/communication-sur-un-reseau/commutateur.png "Commutateur")             |        Commutateur         |
| ![Routeur Sans Fil](/uploads/communication-sur-un-reseau/routeur-sans-fil.png "Routeur Sans Fil") |      Routeur Wi-Fi      |                 ![Pare Feu](/uploads/communication-sur-un-reseau/pare-feu.png "Pare Feu")                  |          Pare-feu          |
|          ![Ordinateur](/uploads/communication-sur-un-reseau/ordinateur.png "Ordinateur")          |  Ordinateur de bureau   | ![Ordinateur Portable](/uploads/communication-sur-un-reseau/ordinateur-portable.png "Ordinateur Portable") |    Ordinateur Portable     |
|              ![Serveur](/uploads/communication-sur-un-reseau/serveur.png "Serveur")               |         Serveur         |                 ![Sans Fil](/uploads/communication-sur-un-reseau/sans-fil.png "Sans Fil")                  | Support de réseau sans fil |
|       ![Reseau Local](/uploads/communication-sur-un-reseau/reseau-local.png "Reseau Local")       | Support de réseau local |                    ![Etendu](/uploads/communication-sur-un-reseau/etendu.png "Etendu")                     |  Support de réseau étendu  |

</center>

En plus de ces représentations, une terminologie spécialisée est étudiée pour étudier la manière dont ces périphériques et supports se connectent entre eux. Les termes importants sont:
* <span style="color:red">Carte réseau</span>: ou adaptateur, fournit la connexion physique au réseau à partir de l'ordinateur ou d'un autre périphérique hôte. Les supports qui relient l'ordinateur au périphérique réseau se branchent directement à la carte réseau.
* <span style="color:red">Port physique</span>: connecteur ou prise sur un périphérique réseau auquel le support est connecté à un hôte ou autre périphérique réseau.
* <span style="color:red">Interface</span>: ports spécialisés sur un périphérique réseau qui se connectent à des réseaux individuels. Puisque les routeurs sont utilisés pour interconnecter des réseaux, les ports sur un routeur sont appelés interfaces réseau.

# Protocoles réseau
## Les règles qui régissent les communications
Toutes les communications sont régies par des <span style="color:red">règles prédéterminées</span> appelées <span style="color:red">protocoles</span>. Dans nos communications personnelles quotidiennes, les règles que nous utilisons pour communiquer à travers un support (un appel téléphonique, par exemple) ne sont pas forcémment identiques au protocole d'utilisation d'un autre support tel que l'envoi d'une lettre.

La réussite d'une communication entre des hôtes sur un réseau requiert l'interaction de nombreux protocoles différents. Un groupe de protocoles associés entre eux et nécessaires pour remplir une fonction de communication est appelé <span style="color:red">suite de protocoles</span>. Ces protocoles sont impémentés dans le logiciel et le matériel installés sur chaque hôte et périphérique réseau.

L'une des meilleures manières pour visualiser la manière dont l'ensemble de ces protocoles interagit sur un hôte spécifique est de l'afficher sous forme de pile.
Une <span style="color:red">pile de protocoles</span> indique la manière dont des protocoles individuels au sein d'une suite sont implémentés sur l'hôte. Les protocoles sont affichés sous forme de hiérarchie en couches.
Le protocole A sert à faire l'interface avec l'utilisateur et fait appel au protocole B pour communiquer.
Les fonctionnalités du protocole B permettent de répondre au service demandé par A et pour cela il fait appel au protocole C qui est en mesure de proposer d'autres fonctionnalités. Idem pour le protocole C et les autres.

Une suite de protocoles réseau doit décrire des exigences et des interactions précises. Les suites de protocoles réseau décrivent des processus tels que:
* Le format ou la structure du message,
* La méthode selon laquelle des périphériques réseau partagent des informations sur des chemins avec d'autres réseaux,
* Comment et à quel moment des messages d'erreur et système sont transférés entre des périphériques,
* La configuration et l'arrêt des sessions de transfert de données.

Certains protocoles peuvent être spécifiques à un fournisseur. il en est le propriétaire. <span style="color:red">Propriétaire</span>, dans ce contexte, signifie qu'une société ou qu'un <span style="color:red">*fournisseur contrôle la définition du protocole* et *la manière dont il fonctionne*</span>. Certains protocoles propriétaires peuvent être utilisés par différentes organisations avec l'autorisation du propriétaire. D'autres peuvent uniquement être implémentés sur du matériel fabriqué par le fournisseur propriétaire.

## Protocoles et normes de l'industrie
Souvent, de nombreux protocoles qui comprennent une suite de protocoles font référence à d'autres protocoles largement utilisés ou normes de l'industrie. Une <span style="color:red">norme</span> est un processus ou un protocole reconnu par l'industrie du réseau et ratifié par une organisation de normes, telle que l'Institute of Electrical and Electronics Engineers (<span style="color:red">IEEE</span>) ou le groupe de travail <span style="color:red">IUTF</span>.

L'utilisation de normes dans le développement et l'implémentation de protocoles garantit que les produits provenant de différents fabricants peuvent fonctionner ensemble (interopérabilité) pour créer des communications efficaces. Si un fabricant spécifique n'adhère pas strictement à un protocole, son équipement ou ses logiciels risquent de ne pas communiquer avec les produits d'autres fabricants.

Dans les communications de données, par exemple, si les extrémités d'une conversation utilisent des protocoles différents pour gérer une communication, en toute probabilité, aucune information ne peut être échangée.

## Interaction des protocoles
L'interaction entre un serveur Web et un navigateur Web constitue un exemple de l'utilisation d'une suite de protocoles sans des communications réseau. Cette interaction utilise plusieurs protocoles et normes dans le processus d'échange d'informations entre ceux-ci. Les différents protocoles fonctionnent entre eux pour garantir que les messages sont reçus et compris par les deux parties. Voici des exemples de protocoles:
* <span style="color:red">**Protocole d'application**</span>:
  Le protocole de transfert hypertexte HTTP - <span style="color:red">Hyper Text Transfer Protocol</span> régit la manière dont un serveur Web et un client Web interagissent. Le protocole HTTP décrit le contenu et la mise en forme des requêtes et des réponses échangées entre le client et le serveur. Les logiciels du client et du serveur Web implémentent le protocole HTTP dans le cadre de l'application. Le protocole HTTP dépend d'autres protocoles pour gérer le transport des messages entre le client et le serveur.
* <span style="color:red">**Protocole de transport**</span>:
  Le protocole TCP - <span style="color:red">Transmission Control Protocol</span> représente le protocole de transport qui gère les conversations individuelles entre des serveurs Web et des clients Web. Le protocole TCP *divise les messages* HTTP en *parties de plus petite taille*, appelées <span style="color:red">segments</span>, pour les envoyer au client de destination. Ce protocole est également responsable du *contrôle de la taille et du débit d'échange* de messages entre le serveur et le client.
* <span style="color:red">**Protocole interréseau**</span>:
  Le protocole interréseau le plus courant est le protocole IP - <span style="color:red">Internet Protocol</span>. Le protocole IP est responsable de la récupération des segments formatés à partir du protocole TCP, de leur encapsulation en <span style="color:red">paquets</span>, de *l'affectation des adresses* appropriées et de la *sélection du meilleur chemin* vers l'hôte de destination.
* <span style="color:red">**Protocoles d'accès au réseau**</span>:
  Les protocoles d'accès au réseau décrivent deux fonctions principales: la gestion des liaisons de données et la transmission physique des données sur les supports.
  - Les protocoles de gestion de liaison de données prennent les paquets fournis par le protocole IP et les formatent pour les transmettre à travers les supports.
  - Les normes et les protocoles des supports physiques régissent la manière dont les signaux sont envoyés à travers les supports, ainsi que leur interprétation par les clients destinataires. Des émetteurs-récepteurs sur les cartes réseau implémentent les normes appropriées pour les supports en cours d'utilisation.

## Protocoles indépendants de la technologie
Les protocoles réseau décrivent les fonctions qui se produisent au cours de communication réseau. Dans l'exemple d'une conversation face à face, un protocole de communication peut stipuler qu'afin de signaler que la conversation est terminée, l'expéditeur doit demeurer silencieux pendant deux secondes complètes. Cependant, ce protocole ne spécifie pas comment l'expéditeur doit demeurer silencieux pendant ces deux secondes.

En général, les protocoles n'indiquent pas comment remplir une fonction particulière. Ils précisent uniquement quelles fonctions sont requises pour une règle de communication spécifique mais pas comment ces fonctions doivent être exécutées, l'implémentation d'un protocole particulier peut être indépendante de la technologie.

Si nous prenons l'exemple d'un serveur Web, le protocole HTTP ne spécifie pas le langage de programmation utilisé pour créer le navigateur, ni le logiciel de serveur Web qui doit être utilisé pour traiter les pages Web, ni le système d'exploitation sous lequel le logiciel est exécuté, ni les exigences matérielles pour afficher le navigateur. Il ne décrit pas non plus la manière dont le serveur doit détecter les erreurs, même s'il décrit ce que doit effectuer le serveur en cas d'erreur.

Cela signifie qu'un ordinateur et tout autre périphérique (par exemple, des smartphones) peut accéder à une page web stockée sur n'iporte quel type de serveur Web qui utilise n'importe quel système d'exploitation, n'importe où sur Internet.

Pour visualiser l'interaction entre différents protocoles, un <span style="color:red">modèle en couches</span> est généralement utilisé. Un modèle en couches illustre le fonctionnement des protocoles dans chaque couche, ainsi que l'interaction avec les couches supérieures et inférieures.