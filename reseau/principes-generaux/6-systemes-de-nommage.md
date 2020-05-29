---
title: 6 Systemes De Nommage
description: 
published: true
date: 2020-05-29T22:20:49.162Z
tags: 
---

Chaque fois que nous voulons utiliser un service Web (Internet) ou communiquer avec une autre machine, on se sert le plus souvent d'un nom convivial ("__laposte.net__" ou "Serveur Web").
En effet, un nom convivial est pmus facile à retenir. Cependant, les ordinateurs utilisent des adresses numériques pour communiquer sur un réseau. Pour faciliter l'utilisation des ressources réseau, un système de nommage fournit une méthode qui établit la correspondance entre le ***nom convivial d'un ordinateur*** (ou d'un service) et son ***adresse numérique*** (adresse IP).

# Les principes de base de DNS
## Le concept DNS
**DNS** (*D*omain *N*ame *S*ystem, système de nom de domaine) est le système de nom actuellement le plus répandu car parfaitement adapté à Internet.
### Définition
> DNS est un système de noms pour les ordinateurs et les services réseau organisé selon une hiérarchie de domaines.
> Le système DNS est utilisé dans les réseaux TCP/IP (Internet) pour localiser des ordinateurs (trouver leur adresse IP) à partir de noms conviviaux.

### Notion de domaine DNS et exemple
Le système de nom de domaine (DNS) a été initialement défini dans les RFC (*Request for Comments*, *demandes de commentaires*) 1034 et 1035 qui spécifient la façon d'implémenter les logiciels DNS.
L'espace de noms de domaines DNS, illustré dans la figure ci-dessous, repose sur le concept **d'arborescence des domaines nommés*.

IMAGE

Chaque niveau de l'arborescence représente une branche ou une feuille de cet "arbre":
Une **branche** est un niveau dans lequel plusieurs noms sont utilisés pour identifier un ensemble de ressources numériques.
Une **feuille** représente un <span style="color:red">nom unique</span> utilisé une seule fois à ce niveau pour identifier une ressource spécifique, le plus souvent un ordinateur ou un serveur.

Les noms de domaines DNS comportent deux étiquettes (labels) ou plus, chacune indiquant un niveau de l'arborescence. Les points sont utilisés pour séparer les étiquettes.
* <span style="color:green">académie-aix-marseille</span>**.**<span style="color:blue">fr</span> : 2 labels,
* <span style="color:green">mail</span>**.**<span style="color:blue">google</span>**.**<span style="color:red">com</span> : 3 labels.

Termes utilisés pour décrire les noms de domaines DNS par leur fonction dans l'espace de noms:
* La **racine du domaine** : Il s'agit de la cime de l'arborescence, représentant un niveau non nommé.
  Elle est parfois affichée sous la forme de deux guillemets vides (" "), indiquant une valeur nulle.
  Lorsqu'elle est utilisée dans un npm de domaine DNS, elle est indiquée par un point "." à droite pour indiquer que le nom est situé à la racine ou au *niveau supérieur de la hierarchie du domaine*.
  Un nom de domaine DNS désigne un emplacement exact de l'arborescence des noms.
  On parle alors de *nom de domaine complet* - **FQDN** : **F**ully **Q**ualified **D**omain **N**ame.
  Exemple: www.google.com<span style="color:red">**.**</span> <- **Racine du domaine**.
* **Domaine de premier niveau - TLD : Top Level Domain**: Nom de deux ou trois lettres utilisé pour indiquer un pays, une région ou le type d'organisation utilisant un nom.
  Domaines génériques - **g**TLD : **g**eneric TLD: Existant depuis l'origine .com .edu .gov .int .net .org .mil
  Nouveaux gTLD (novembre 2000) : .aero .biz .museum .name .info .coop .pro
  Domaines nationaux - **cc**TLD : **c**ountry **c**ode: correspondant aux codes nationaux définis par la norme ISO 3166 : .fr .us .de .ru ...
* **Domaine de second niveau** : Noms de domaines inscrits au nom d'un individu ou d'une organisation pour une utilisation sur Internet. Ces noms sont toujours associés à un domaine de premier niveau approprié, selon le type d'organisation ou l'emplacement géographique dans lequel un nom est utilisé.
  La demande de nom de domaine se dépose auprès d'un organisme internationnal (l'**Internir**) ou de l'un des sous-organismes appelés "**registrats**", l'Afnic pour la France.
* **Sous-domaine** : Noms supplémentaires pouvant être créés par une organisation et associés au nom de domaine de second niveau inscrit.
  Toute organisation peut développer sa propre arborescence en fonction des services offerts ou de la localisation géographique.
* **Nom d'hôte ou de ressource** : Nom qui représente une feuille (extrémité) de 'arborescence DNS des noms et identifie une ressource particulière. Généralement, l'étiquette la plus à gauche d'un nom de domaine DNS identifie un ordinateur spécifique du réseau.

Avec DNS, un nom de domaine complet (composé de plusieurs niveaux) de *lit de gauche à droite*:
**serveur.service.monentreprise.fr.**
* **serveur**       Nom d'hôte, plus à gauche => feuille ou extremité),
* **service**       Nom de sous domaine dans lequel se trouve l'hôte,
* **monentreprise** Nom de domaine de second niveau constituant la racine du sous-domaine "service"
* **fr**            Nom de domaine de premier niveau (France) constituant la racine du domaine "monentreprise".
* **.**             Qualifie le nom de domaine complet (FQDN)


## La mise en cache
Lorsque les serveurs DNS traitent les requêtes clientes, ils acquièrent de nombreuses informations sur l'espace de noms DNS. Ces informations sont ensuite **mises en cache** par le serveur (c'est à dire **stockées temporairement**). La mise en cache permet d'**accélerer** la résolution DNS pour les requêtes ultérieures portant sur des noms très utilisés, tout en réduisant de manière significative le trafic des requêtes DNS sur le réseau.

## Fonctionnement des requêtes DNS
Lorsqu'un client DNS a besoin de rechercher un nom utilisé dans un programme, il émet une requête. Les requêtes DNS peuvent être résolues de différentes manières.
1. Une requête de nom est formulée au niveau de l'ordinateur client et transmise au solveur (ou résolveur) qui est le client DNS, en vue d'être résolue.
   Le client peut *parfois* répondre localement à une requête en utilisant les informations mises en cache, obtenues en réponse à une requête précédente.
2. 