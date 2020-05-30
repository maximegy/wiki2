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