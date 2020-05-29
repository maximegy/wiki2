---
title: 2 Oracle
description: 
published: true
date: 2020-05-29T22:37:00.677Z
tags: 
---

# Définition
Base de données : (BDD ou DB en anglais) C’est un lot d'informations stockées dans un dispositif informatique. Les technologies existantes permettent d'organiser et de structurer la base de données de manière à pouvoir facilement manipuler le contenu et stocker efficacement de très grandes quantités d'informations.
* Base de données relationnelle : C’est un stock d'informations décomposées et organisées dans des matrices (tableaux à deux dimensions) appelées tables.
* Système de gestion de base de données : (SGBD ou DBMS en anglais) C’est un ensemble de logiciels qui sert à la manipulation des bases de données. Il sert à effectuer des opérations ordinaires telles que consulter, modifier, construire, organiser, transformer, copier, sauvegarder ou restaurer des bases de données. La majorité des SGBD du marché manipulent des bases de données relationnelles.
* Système de gestion de base de données relationnelle : (SGBDR ou RDBMS Relational DataBase Management System en anglais). C’est un ensemble de logiciels qui sert à la manipulation des bases de données relationnelles.

# Les différents types de BDDR
Les différents types de bases de données sont :
* Transactionnelle (OLTP : OnLine Transaction Processing) : Elle se caractérise par une forte activité de mise à jour (INSERT/UPDATE), un nombre plus ou moins important d’utilisateurs, une exigence de temps de réponse court.
* Décisionnelle (DSS : Decision Support Systems) : Elle se caractérise par une forte activité d’interrogation (SELECT) généralement sur de gros volumes de données, une mise à jour périodique avec de gros traitements, une exigence de temps de réponse relativement court.
* Mixte : Elle est à la transactionnelle et décisionnelle, le poids respectif de chaque activité étant variable.


# Histoire MDR
Oracle Database est un Système de Gestion de Bases de Données Relationnel (SGDBR) édité par la société du même nom (Oracle Corporation - http://www.oracle.com), leader mondial des bases de données.
En 1977, Oracle Corporation a été créée par Lawrence Ellison, Bob Miner, et Ed Oates. Elle s'appelle alors Relational Software Incorporated (RSI) et commercialise un Système de gestion de bases de données relationnelles nommé Oracle.
En 1979, RSI introduit son produit Oracle V2 comme base de données relationnelle. La version 2 ne supportait pas les transactions mais implémentait les fonctionnalités SQL basiques de requête et jointure. Il n'y a jamais eu de version 1, pour des raisons de marketing, la première version a été la version 2.
En 1983, RSI devient Oracle Corporation pour être plus représentative de son produit phare. La version 3 d'Oracle, entièrement réécrite en langage de programmation C, est publiée. Celle-ci supportait les transactions grâce aux fonctionnalités de commit et rollback. C'est aussi à partir de cette version que la plate-forme Unix est supportée.
En 1984, la première version d'Oracle (Oracle 4) est commercialisée sur les machines IBM.
En 1985, Oracle 5 permet une utilisation client-serveur.
En 1986, Oracle a été porté sur la plateforme 8086.
En 1988, Oracle 6 supporte le PL/SQL et les sauvegardes à chaud (lorsque la base de données est ouverte).
En 1992, Oracle 7 supporte les contraintes d'intégrité, les procédures stockées et les déclencheurs (triggers).
En 1995, Oracle sort sur plates-formes Windows.
En 1997, Oracle 8 introduit le développement orienté objet. Oracle depuis la version 8.0.5 est disponible sous Linux.
En 2001, Oracle 9i ajoute 400 nouvelles fonctionnalités et permet de lire et d'écrire des documents XML.
En 2003, Oracle 10g est publiée. Le g signifie « grid » ; un des atouts marketing de la 10g est en effet qu'elle supporte le « grid computing » (infrastructure virtuelle constituée d'un ensemble de ressources informatiques potentiellement partagées, distribuées, hétérogènes, délocalisées et autonomes).
En 2005, une version complètement gratuite est publiée, « Oracle Database 10g Express Edition » (Oracle XE).
En 2007, Oracle 11gR1 est publié.
En 2009, Oracle 11gR2 est publié. Oracle rachète Sun Microsystems pour 7.4milliards dollars.
En 2013, Oracle 12cR1 est publié. Le « c » signifie « cloud » ; un des atouts marketing de la 12c est qu’elle à été pensé pour le « cloud ».
En 2015, Changement des tarifs, suppression des éditions standard et standard one au profit d’une nouvelle édition, la standard two.
Lawrence Ellison, comparé à Iron Man, il a financé le film, c'est un fou furieux, il fait de la voile, du F1, il apparait dans le film.

# Tarifs
Deux modes de licences:
Soit pour utilisateurs nommés, soit pour processeurs
différence entre nommés ou simultannés: 10 licences simultannés > 10 personnnes en meme temps, nommés: 200 utilisateurs, 200 licences.
a partir  du 51e user c'est mieux de prendre licence processeur.

1. Licence en mode "Named User Plus"

| Edition oracle       | Prix public licence/user | Prix maintenance Oracle /user/an | Nb mini licences |
| :------------------- | :----------------------: | :------------------------------: | :--------------: |
| Standard Edition Two |          304 €           |             66,85 €              |        10        |
| entreprise           |          825 €           |             181,45 €             |        25        |

1. Licence en mode "Processor Licence"

| Edition oracle       | Prix public licence/proc | Prix maintenance Oracle /proc/an | Nb maxi proc |
| :------------------- | :----------------------: | :------------------------------: | :----------: |
| Standard Edition Two |         15 194 €         |            3 342,57 €            |      2       |
| Enterprise           |         41 240 €         |            9 072,69 €            |   illimité   |

1. Personal Edition
Version pour les devs ou pour réaliser des tests sur une app. Prix à partir de 80€ pour une année, 280€ pour 5 ans et 399€ en licence perpétuelle.

4. Express Edition
Version totalement gratuite, il s'agit d'une version 11g, fortement limitée, elle gère actuellement des fichiers de données limitées à 11Go de données et un serveur doté d'un seul processeur et d'un maximum de 1 Go de mémoire RAM.


# Introduction
Un serveur Oracle DB est composé de deux éléments distincts
- L'instance, qui se compose d'une structure de mémoire partagée et d'un ensemble de processus,
- La BSS, qui se compose d'un ensemble de fchiers physique qui contiennent notamment les données.

Dans une architecture client/serveur, il y a également des processus utilisateurs correspondant à 

Principaux process:
- SGA , mémoire occupée sur le serveur,
- Listener, écoute les connexions

## L'instance
Une instance est composée:
- D'une zone de mémoire partagée appelée SGA System Global Area,
- D'un ensemble de processus d'arrière plan ayant chacun unrôle bien précis

### La SGA
- mémoire:
  - la library cache, qui stocke toutes les informations SQL qu'on a tapé, donc la donnée de la requête est mise en cache,
  - Le dictionnary Cache, des tables par oracle pour oracle pour son fonctionnement interne. (exemple la liste d'utilisateurs...).

#### La zone mémoire: Library Cache
La library Cache est une zone mémoire qui va stocker les informations sur les ordres SQL exécutés récemment dans une zone SQL Cache qui contiendra le texte de l'ordre SQL, la version compilée de l'ordre SQL et son plan d'execution
Cette zone mémoire sera utilisée lorsqu'une requête sera exécutée plusieurs fois, car Oracle n'aura plus alors à recréer la version compilée de la requête ainsi que son plan d'exécution (chemin).

## Les processus d'arrière plan:
### SMON
Le processus SMON est un processus qui va servir à corriger les plantages de l'instance et à vérifier la synchronisation des données.
Si l'instance plante, c'est SMON qui va se charger de rejouer le contenu des REDO LOG FILE afin de pouvoir rejouer les transactions et de resynchroniser els données dans les fichiers de données.
SMON sert aussi à nettoyer les segments temporaires après leur utilisation. Il sert aussi à défragmenter les fichiers de données, tablespaces et autres

### PMON
Le processus PMON (process monitor) va être surtout dédié aux processus des utilisateurs. Il va servir à annuler les transactions d'une sessions (lors d'un plantage de la sessions par exemple), mais aussi servir à relâcher tous les verrous posés par la session, et à relâcher toutes les ressources détenues par la session.

### DBWin
Le processus DBWn va être dédié à l'écriture du Database buffer cache dans les fichiers de données de la base de données.
Ce processus est aussi là pour vérifier en permanence le nombre de blocs libres dans le Database Buffer Cahe afin de laisser assez de place disponible pour l'écriture des données dans le buffer.

### LGWR
Le processus LGWR -Log Writer) est le processus qui va écrire les informations contenues dans le REDO LOG Buffer dans les fichiers REDOLOG File lors des évenements suivants:
- Quand une transaction est terminée avec un COMMIT,
- Quand le REDO LOG Buffer est au 1/3 plein
- Quand il n'y a plus de 1Mo d'informations de log contenues dans le Buffer,
- aadzzad

### CKPT
Ce processus va servir à mettre à jour les en-têtes des fichiers de données, et à mettre à jour les fichiers CONTROL FILE afin de spécifier que l'action de CHECKPOINT s'est bien déroulée.
Le cHECKPOINT est un évènement qui se déclanche lors:
- D'un changement de groupe de REDO LOG FILE,
- D'un arrêt nrmal de la BDDD?
- aaaa
- Dune limite définir par les paramètre d'initialisation

### ARCn

blabla




## Processus Serveur
Processus d'écoute par défaut port: 1521.
une fois connecté ne passe plus par le listener
### Processus d'écoute


### PGA
Mémoire avec données propres à l'utilisateur.


## La base de données
Fichiers de donnés, c'est dans ces fichiers que les données proprement dites sont stockées,(tablespace.dbf)
Fichiers de contrôle, qui contient des informations de contrôle sur la BDDD (control.ctl)
Fichiers de journalisation, qui enregistrent toutes les modifications apportées à la base (redo.log)
archivelog, les fichiers de journalisation qui sont archivés, qui permet d'avoir les états des BDD à un temps donné
attention gourmand en espace disque.


### Fichiers de données
Tablespace

### Fichiers de contrôle


###Fichiers de journalisation



# Vidéo

rond processus d'arrière plan