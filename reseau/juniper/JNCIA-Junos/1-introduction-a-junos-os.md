---
title: Fondamentaux Junos OS
description: 
published: true
date: 2020-05-30T22:31:03.469Z
tags: 
---

#Junos

Les fonctionnalités Junos OS sont compartimentés au sein d'une pultitude de processus.
Chaque processus s'occuper d'une portion des fonctionnalités de l'appareil.
Chaque processus s'execute dans son propre espace mémoire protégé ce qui permet qu'un processus ne peut pas directement interferer avec un autre.
Quand un processus échoue, le systeme entier n'échoue pas nécessairement.
De nouvelles fonctionnalités peuvent donc être ajoutées avec moins de probabilité de casser une fonctionnalité existante.

Junos OS est un système d'exploitation robuste et modulaire, construit sur des systèmes open-source comme FreeBSD et Linux.
C'est un système fiable et sécurisé alimentant l'infrastructure réseau haute performance offerte par Juniper.

IMAGE


Toutes les plateformes sous Junos exécutent le même base de code source empaqueté dans des images adaptées.
Ce principe permet aux configurations de fonctionner sur n'importe quel chassis car les différentes plateformes s'administrent de la même manière.



# User Interface Options: The Junos CLI
## Les interfaces utilisateurs

Junos OS fourni deux interfaces pour administrer, monitorer, configurer et troubleshoot l'équipement.

### Junos CLI
Junos CLI est un une interface en ligne de commande. Un moyen d'accéder au CLI est via le port Série (out-of-band).
Les paramètres du ports console sont prédéfinis et ne sont pas configurables par l'utilisateur.

Sur les systèmes junos virtualisés comme les vSRX et vMX, la console virtuelle fournit la connexion.

Une deuxième méthode pour accéder au CLI est par le réseau (in band) en utilisant des protocoles comme Telnet et SSH. A contrario de la connexion console, ces types de connexions nécessitent pour le protocole d'accès et les ports alloués.

Beaucoup de plateformes qui exécutent Junos OS fournissent un port Ethernet de management dédié. Ce port fournit un accès "Out-od-Band". Par contre le système ne peut pas transférer du traffic sur ce port. Le nom du port peut différer selon les différentes plateformes.

### J-Web
J-Web est une interface utilisateur graphique à travers un site Web qui peut être accessible via HTTP ou HTTPS. Il fourit des assistants de configuration rapides pour simplifier les tâches de configuration les plus courantes.
Pour les configurations les plus complexes, J-Web permet d'éditer directement le fichier de configuration du système.
J-Web est installé et activé par défaut sur la majorité des plateformes exécutant Junos OS.

## Se connecter
Junos OS nécessite un nom d'utilisateur et un mot de passe pour y accéder.

Une fois connectés, les utilisateurs sans droits d'administration sont directement placés sur le CLI.

Quand il est configuré, la CLI affiche le nom d'hôte (hostname) de l'équipement.

Quand le hostname n'est pas configuré, comme dans le cas d'une configuration d'usine, le CLI affiche "amnesiac".

L'utilisateur "root" à un accès complet pour contrôler l'équipement.
Quand on se connecte en tant que root, le système nous place automatiquement sur le shel unix.

Pour démarrer la CLI, il faut taper la commande `cli`.

## Modes CLi

Junos OS fournit deux modes CLI : 
## Operational Mode
Le mode "Opérationnel", on peut utiliser la CLI pour monitorer et dépanner l'équipement. 
Par exemple les commandes `monitor`, `ping`, `show`, `test` et `traceroute` permet d'afficher des informations et tester la connectivité réseau de l'appareil.

le charactère `>` après le hostname identifie le mode opérationnel.

## Configuration Mode
Dans le mode configuraiton, on peut configurer toutes les propriétés de Junos OS comme les interfaces, les protocoles, les accès utilisateurs ou encore les propriétés systèmes et hardware.

Le charactère `#` après le hostname identifie le mode configuration.



## Configuration Mode