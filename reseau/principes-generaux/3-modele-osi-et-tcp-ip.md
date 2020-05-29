---
title: 3 Modèle OSI et TCP/IP
description: Présentation et Terminologie
published: true
date: 2020-05-29T22:16:25.619Z
tags: 
---

# Besoins et utilisation d'un modèle par couche
Précédemment, nous avons parlé de **protocoles** et **suites de protocoles**. Dans ces suites, ou piles, chaque protocole à un rôle précis. Le résultat produit par un protocole sert ensuite à un autre protocole et ainsi de suite.
Pour visualiser l'interaction entre ces différents protocoles, un modèle en **couches** est généralement utilisé. Un modèle en couches illustre le fonctionnement des protocoles dans chaque couche, ainsi que l'<span style="color:green">interaction avec les couches supérieures et inférieures</span>.

> **Pourquoi un modèle réseau en couches ?**
> Un modèle de réseau en couche peut servir à visualiser comment les paquets de données circulent à partir des programmes d'application (documents, messagerie, chat, etc.), en passant par un média réseau (câble, Wifi, etc.) jusqu'à un autre programme d'application se trouvant sur un autre ordinateur en réseau.

L'utilisation d'un modèle en couches présente certains avantages pour décrire des protocoles et des opérations sur un réseau. L'utilisation d'un modèle en couches:
* Aide à la conception d'un protocole. Un protocole fonctionnant à une couche spécifique doit disposer d'informations clairement définies et il doit également tenir compte des couches supérieures et inférieures,
* Il encourage la concurrence, car les produits de différents fournisseurs peuvent fonctionner ensemble,
* Il permet d'éviter que des changements technologiques ou fonctionnels dans une couche ne se répercutent sur d'autres couches, supérieures ou inférieures,
* Fournit un langage commun pour décrire des fonctions et des fonctionnalités réseau.

# Modèle de protocole et modèle de référence
Il existe deux types de modèles de réseau de base :les modèles de protocole et les modèles de référence.

Un modèle de protocole fournit un modèle qui correspond étroitement à la structure d'une suite de protocoles particulière et existante. L'ensemble hiérarchique des protocoles associés dans une suite représente généralement toutes les fonctionnalités requises à l'interface entre le réseau humain et le réseau de données.

Le **modèle TCP/IP** est un *modèle de protocole*, car il décrit les fonctions qui interviennent à chaque couche de protocoles au sein de la suite TCP/IP.

Un modèle de référence fournit une référence commune pour maintenir la cohérence dans tous les types de protocoles et de services réseau. Un modèle de référence n'est pas destiné à être une spécificationd'implémentation, ni à fournir un niveau de détail suffisant pour définir précisément les services de l'architecture réseau. Le principal objectif d'un modèle de référence est d'assurer une compréhension plus claire des fonctions et des processus impliqués.

Le **modèle OSI** (Open System Interconnection) constitue le *modèle de référence* interréseau le plus connu. Il est utilisé pour la conception de réseaux de données, des spécifications d'opérations et la résolution de problèmes.

Bien que les modèles TCP/IP et OSI soient les principaux modèles utlisés lorsqu'il s'agit de fonctionnalités réseau, les concepteurs de protocoles, de services ou de périphériques réseau peuvent créer leurs propres modèlespour représenter leurs produits. Enfin, les concepteurs doivent communiquer avec l'industrie en associant leurs produits ou leurs services aux modèles OSI ou TCP/IP ou aux deux.

# Le modèle de protocole TCP/IP
Le premier modèle de protocole en couches pour les communications interréseau fut créé au début des <span style="color:red">années 70</span> et est appelé modèle Internet. Il définit 4 catégories de fonctions qui doivent s'exécuter pour que les communications réussissent. L'architecture et la suite de protocoles TCP/IP suit la structure de ce modèle. Pour cette raison, le modèle Internet est généralement appelé "**modèle TCP/IP**".

La plupart des modèles de protocole décrivent une pile de protocoles spécifiques au fournisseur. Cependant, puisque le modèle TCP/IP est une **norme ouverte**, aucune entreprise ne contrôle la définition du modèle. Les définitions de la norme et des protocoles TCP/IP sont traités dans un forum public et définies dans un ensemble de documents disponibles au public. Ces documents sont appelés **documents RFC** (Request For Comments). Ils contiennent les spécifications formelles des protocoles ainsi que des ressources ui décrivent l'utilisation des protocoles.

|  N°   |    Couche    | Description                                                                                                                                                       |
| :---: | :----------: | :---------------------------------------------------------------------------------------------------------------------------------------------------------------- |
|   4   | Application  | La couche 4 regroupe tous les aspects liés aux applications. Les question de représentation et de codage des données, le contrôle du dialogue avec l'utilisateur. |
|   3   |  Transport   | La couche 3 prend en charge la communication entre différents périphériques à travers divers réseaux.                                                             |
|   2   |   Internet   | La couche 2 Détermine le meilleur chemin que les données doivent emprunter sur les divers réseaux.                                                                |
|   1   | Accès réseau | La couche 1 contrôle les périphériques matériels (carte réseau) et les supports (câble, fibre optique, etc.) qui constituent le réseau.                           |

[image TCP/IP ]
|              Acronyme               | Nom                            |
| :---------------------------------: | :----------------------------- |
| <span style="color:red">FTP</span>  | File Transfert Protocol        |
| <span style="color:red">HTTP</span> | HyperText Transfert Protocol   |
| <span style="color:red">SMTP</span> | Simple Mail Transfert Protocol |
| <span style="color:red">DNS</span>  | Domain Name System             |
| <span style="color:red">TFTP</span> | Trivial File Transfer Protocol |


# Le modèle de référence OSI
##Organisation et utilisation du modèle OSI
Le *modèle de référence **<span style="color:red">OSI</span>***, pour **<span style="color:red">Open System Interconnexion</span>**, interconnexion de systèmes ouverts, a été créé en **<span style="color:red">1984</span>** comme une *<span style="color:red">architecture descriptive</span>*. Ce modèle offre un ensemble de normes assurant une compatibilité et une interopérabilité entre les divers types de technologies réseau produites par les entreprises.

Le modèle de référence OSI est le principal modèle des communications réseau. C'est un *outil* pour *décrire* l'envoi et la réception de données sur un réseau. Ce modèle permet de décomposer les fonctions réseau et de voir comment elles sont exécutées au niveau de chaque couche.

Dans le modèle OSI, le problème des communications est divisé en sept problèmes plus petits et plus faciles à gérer. Chacun des sept petits problèmes est représenté par une couce particulière du modèle.
Les principaux avantages apportés par le modèle OSI sont:
- Il réduit la complexité (éléments plus petits et plus simples),
- Il facilité la conception modulaire,
- Il uniformise les interfaces réseaux,
- Il assure l'interopérabilité de la technologie,
- Il facilite et accélère l'évolution (les changements apportés à une couche n'affectent pas les autres couches).

|  N°   |                      Couche                       | Description                                                                                                                                                                                                                                                                                                                                                   | Rôle                                                                                                                                        |
| :---: | :-----------------------------------------------: | :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | :------------------------------------------------------------------------------------------------------------------------------------------ |
| **7** |    <span style="color:red">Application</span>     | La couche application est la couche OSI la plus proche de l'utilisateur. Elle fournit des services réseau aux applications de l'utilisateur.<br /> Par exemple, les navigateurs                                                                                                                                                                               | **Services réseaux fournis aux applications**<br />Courrier électronique<br />Transfert de fichier                                          |
| **6** |    <span style="color:red">Présentation</span>    | La couche présentation s'assure que les informations envoyées par la couche application d'un système dont lisibles par la couche application d'un autre système en utilisant un format commun.<br />Par exemple, format de données - Code ASCII)                                                                                                              | **Représentation des données**<br />Format et structure des données<br />Cryptage, compression                                              |
| **5** |      <span style="color:red">Session</span>       | La couche session ouvre, gère et ferme les sessions entre deux syqtèmes hôtes en communication. Elle synchronise également le dialogue entre les couches de présentation des deux hôtes et gère l'échange des données<br />Par exemple, dialogues et conversations                                                                                            | **Communication entre les hôtes**<br />Etablissement, gestion et fermeture des sessions entre les applications                              |
| **4** |     <span style="color:red">Transport</span>      | La couche transport segmente (découpe) les données envoyées par l'emetteur et les rassemble en flux de données sur le récepteur.<br />Les problèmes liés à la fiabilité du transport entre deux systèmes hôtes relèvent de la couche transport.<br />Qualité de service et fiabilité                                                                          | **Connexions de bout en bout**<br />Fiabilité du transport<br />Détection des erreurs et reprise<br />Contrôle des flux.                    |
| **3** |       <span style="color:red">Réseau</span>       | La couche réseau assure la connectivité et la sélection du chein entre deux systèmes hôtes pouvant être situés sur des réseaux géographiquement éloignés.<br />Pour cela, on associe à chaque machine une **adresse logique**, plus connue sous le terme "**Adresse IP**".<br />Selection du chemin, routage et adressage IP.                                 | **Adressage et sélection du meilleur chemin**<br />Connectivité et sélection du chemin entre deux systèmes distants<br />Domaine de partage |
| **2** | <span style="color:red">Liaison de données</span> | La couche liaison de données assure un transit fiable des données sur une liaison physique. Ainsi, la couche liaison de données s'occupe de l'**adressage physique (adresse MAC)**, de la topologie du réseau, de l'accès au réseau, de la notification des erreurs, de la livraison ordonnée des trames et du contrôle de flux.<br />Trames et adresses MAC. | **Accès au média<br />Transfert fiable des données<br />Adressage physique, topologie réseau, notification des erreurs                      |
| **1** |      <span style="color:red">Physique</span>      | La couche Physique définit les spécifications électriques, mécaniques, procédurales et fonctionnelles permettant d'activer, de maintenir et de désactiver la liaison physique entre les systèmes d'extrémité.<br />Signaux et médias.                                                                                                                         | **Transmission binaire**<br />Câbles, connecteurs<br />tensions électriques, débits<br />distance maximale                                  |

# Encapsulation des données
Si un ordinateur (hôte A) veut envoyer des données à un autre ordinateur (hôte B), lorsque ces données d'application descendent la pile de protocoles en vue de leur transmission sur le support réseau, différents protocoles ajoutent des informations à chaque niveau. Il s'agit du processus d'**<span style="color:red">encapsulation</span>**.
Pour comprendre comment se produit l'encapsulation, examinons la manière dont les données traversent les couches. La présentation et le flux des données échangées subissent des changements au fur et à mesure que les réseaux fournissent leurs services aux utilisateurs.
Les réseaux doivent effectuer les cinq étapes de conversion ci-dessous afin d'encapsuler les données:
1. **Construction des données**
   Lorsqu'un utilisateur envoie un message électronique, les caractères alphanumériques qu'il contient sont convertis en données pouvant circuler sur le réseau. Avec ajout de cryptage et/ou de compression.
2. **Préparation des données pour le transport de bout en bout**
   Les données sont préparées pour le transport interréseau. En utilisant des <span style="color:red">*segments*</span>, des petites quantités de données, la fonction de transport s'assure que les systèmes hôtes situés à chaque extrémité du système de messagerie peuvent communiquer de façon fiable.
3. **Ajoute de l'adresse réseau à l'en-tête**
   Les données sont organisées en <span style="color:red">*paquets*</span>, ou <span style="color:red">*datagrammes*</span>, contenant un en-tête réseau constitué des adresses logiques ou <span style="color:blue">*adresses IP d'origine et de destination*</span>. Ces adresses aident les uunités réseau interédiaires à acheminer les paquets dans le réseau suivant un chemin déterminé.
4. **Ajout de l'adresse locale à l'en-tête de laison**
   Chaque unité réseau doit placer le paquet dans une <span style="color:red">*trame*</span>. La trame permet d'établir la connexionavec la prochaine unité réseau directement connectée dans la liaison. Pour cela, il faut identifier les machines sources et destination par leurs <span style="color:red">*adresses MAC*</span>.
5. **Conversion en bits pour la transmission**
   La trame doit être convertie en une série de bits (1 ou 0) pour la transmission sur le média (câbles). Une fonction de synchronisation permet aux unités de distinguer ces bits lorsqu'ils circulent sur le média. Tout au long du trajet suivi dans l'inter réseau physique, le média peut varier.


   [image OSI ]

# Processus d'envoi et de réception
Lors de l'envoi de messages sur un réseau, la pile de protocoles sur un hôte fonctionne de haut en bas. Dans l'exemple du serveur Web vu précédemment, nous pouvons utiliser le modèle TCP/IP pour illuster le processus d'envoi d'une page Web HTML à un client.
Dans la **couche transport**, les données de la couche application sont divisées en *segments* TCP. La couche étiquette, appelée *en-tête*,qui contient des informations pour désigner le processus (**n° de port**) s'exécutant sur l'ordinateur de destination qui doit recevir le message. Il contient également les informations (chaque segment est numéroté) pour permettre au processus de destination de réassembler les données selon leur format d'origine.
Le segment est ensuite envoyé à la couche Internet, ou est implémenté le protocole IP.

Dans cette **couche Internet**, la totalité du segment TCP est à son tour encapsulé dans un *paquet* IP, qui ajoute une autre étiquette, appelée en-tête IP. L'*en-tête* IP contient des <span style="color:red">*adresses IP* d'hôtes sources et de destination</span>, ainsi que des informations nécessaires à la livraison du paquet à son processus de destination correspondant.

Le paquet IP est ensuite envoyé à la **couche d'accès réseau**, où im est encapsulé dans une *trame* qui contient une en-tête et une queue de trame. Chaque en-tête de trame contient une <span style="color:red">*adresse physique* source et de destination</span>.
L'adresse physique identifie de manière unique les périphériques sur le réseau local. L'en-queue contient des informations de vérification d'erreur.
Enfin, les *bits* sont codés et envoyés sur le support Ethernet par la carte réseau du serveur.

Le processus de réception est inversé sur l'hôte de destination. Les données sont décapsulées au fur et à mesure qu'elles se déplacent vers la partie supérieure de la pie et l'application d'utilisateur final.

# Comparaison du modèle OSI et du modèle TCP/IP
Même si le modèle de référence OSI est universellement reconnu, historiquement et techniquement, la norme ouvert d'Internet est <span style="color:red">le protocole TCP/IP</span>.

Le *modèle de référence* TCP/IP et la *pile de protocoles* TCP/IP rendent possible l'échange de données entre deux ordinateurs partout dans le monde. Le modèle TCP/IP présente une importance historique semblable aux normes qui ont permis l'essor des industries du téléphone, de l'electricité, du chemin de fer, de la télévision et de la vidéo.

[ Image a faire ]

En comparant le modèle OSI au modèle TCP/IP, vous remarquerez des similitudes et des différences:

**Similitudes**
    - Tous deux comportent des couches,
    - Tous deux comportent une couche application, bien que chacune fournisse des services très differents,
    - Tous deux comportent des couches réseau et transport comparables,
    - Tous deux supposent l'utilisation de la technologie de commutation de paquets,
    - Les professionnels des réseaux doivent connaître les deux modèles.

**Différences**
    - TCP/IP intègre la couche présentation et la couche session dans sa couche application,
    - TCP/IP regroupe les couches physiques et liaison de données du modèle OSI au sein d'une seule couche.
    - TCP/IP semble plus simple car il comporte moins de couche,
    - Les protocolesTCP/IP constituent la norme sur laquelle s'est développé Internet. Aussi, le modèle TCP/IP a bâti la réputation de ses protocoles. En revanche, les réseaux ne sont généralement pas architecturés autour du protocole OSI, bien que le modèle OSI puisse être utilisé comme guide.

Bien que les protocoles TCP/IP constituent les normes sur lesquelles repose Internet, le modèle OSI a été choisi pour les raisons suivantes:
- Il s'agit d'une norme universelle, générique et indépendant.
- Ce modèle comporte davantage de détails, ce qui le rend plus utile pour l'enseignement et l'étude,
- Cette richesse de détails peut également s'avérer fort utile au moment du dépannage.

L'opinion de nombreux professionnels des réseaux diffère quant au modèle à utiliser. Vous devez vous familiariser avec les deux modèles. Vous utiliserez le modèle OSI comme microscoper pour l'analyse des réseaux, mais vous utiliserez également les protocoles TCP/IP tout au long du programme d'études.
Souvenez-vous qu'il existe une différence entre un modèle, les couches, interfaces et spécifications de protocole, et un protocole réel utilisé dans les réseaux.

Ainsi on utilise le **modèle OSI** et les **protocoles TCP/IP**
