---
title: 3 Architecture Oracle
description: 
published: true
date: 2020-05-29T22:38:14.587Z
tags: 
---

# Introduction
Un serveur Oracle Database est composé de deux éléments distincts :
* L’instance (qui se compose d’une structure de mémoire partagée et d’un ensemble de processus).
* La base de données (qui se compose d’un ensemble de fichiers physique qui contiennent notamment les données).
Comme comparaison, on peut imaginer qu’une INSTANCE correspond à WORD et que la BASE DE DONNEES correspond à un DOCUMENT WORD.
Dans une architecture client/serveur, il y a également des processus utilisateurs correspondant à l’application utilisée (logiciel, progiciel, sqlplus, …) par l’utilisateur pour se connecter à la base de données.

## L'instance
Une instance est composée :
* D’une zone de mémoire partagée appelée SGA (System Global Area).
* D’un ensemble de processus d’arrière-plan (background process) ayant chacun un rôle bien précis.
* D’un ensemble de processus serveurs (server process) chargés de traiter les requêtes des utilisateurs.
Chaque instance est définie par un nom, il faut définir la variable d’environnement ORACLE_SID pour déterminer sur quelle instance l’on souhaite travailler.

## La base de données
Une base de données est composée :
* D’un ou plusieurs fichiers de données, c’est dans ces fichiers que les données proprement dites sont stockées (tablespace.dbf).
* D’au moins un fichier de contrôle qui contient des informations de contrôle sur la base de données (control.ctl).
* D’au minimum deux groupes de fichiers de journalisation qui enregistrent toutes les modifications apportées à la base (redo.log).
Les fichiers de journalisation peuvent être archivés ; ces fichiers archivés ne font, à proprement parler, pas partie de la base de données.
Chaque base de données porte un nom défini lors de sa création ; ce nom est renseigné par le paramètre d’initialisation DB_NAME.

# L'instance
Une base de données est composée :
* D’un ou plusieurs fichiers de données, c’est dans ces fichiers que les données proprement dites sont stockées (tablespace.dbf).
* D’au moins un fichier de contrôle qui contient des informations de contrôle sur la base de données (control.ctl).
* D’au minimum deux groupes de fichiers de journalisation qui enregistrent toutes les modifications apportées à la base (redo.log).
Les fichiers de journalisation peuvent être archivés ; ces fichiers archivés ne font, à proprement parler, pas partie de la base de données.
Chaque base de données porte un nom défini lors de sa création ; ce nom est renseigné par le paramètre d’initialisation DB_NAME.

## La SGA
La SGA est une zone mémoire qui est utilisée par la base de données pour partager les informations entre les différents processus Oracle.

### La zone mémoire : Shaed Pool
La Shared Pool ou zone de mémoire partagée est utilisée pour partager les informations sur les objets de la base de données ainsi que sur les droits et privilèges accordés aux utilisateurs.
Cette zone mémoire se découpe en 2 blocs :
* La Library Cache
* Le Dictionnary Cache

#### La zone mémoire : Library Cache
La Library Cache est une zone mémoire qui va stocker les informations sur les ordres SQL exécutés récemment dans une zone SQL Cache qui contiendra le texte de l'ordre SQL, la version compilée de l'ordre SQL et son plan d'exécution.
Cette zone mémoire sera utilisée lorsqu'une requête sera exécutée plusieurs fois, car Oracle n'aura plus alors à recréer la version compilée de la requête ainsi que son plan d'exécution car ceux-ci seront disponibles en mémoire.

#### La zone mémoire : Dictonnary Cache
Le Dictionnary Cache est une zone mémoire qui va contenir les définitions des objets de la base de données qui ont été utilisés récemment.
On entend par "définition" la structure, les composants, les privilèges liés à cet objet.
Cette zone mémoire permettra au serveur Oracle de ne pas devoir aller chercher ces informations sur le disque à chaque exécution d'une requête SQL.

### La zone mémoire : Database Buffer Cache
Cette zone mémoire sert à stocker les blocs de données utilisés récemment. Ce qui signifie que lorsque vous allez lancer une première fois la requête Oracle, cette dernière va se charger de rapatrier les données à partir du disque dur.
Lors des exécutions suivantes les blocs de données seront récupérés à partir de cette zone mémoire, entrainant ainsi un gain de temps.
Cette zone fonctionne selon le principe dit du bloc ancien. C'est à dire que l'on peut représenter cette zone mémoire comme étant un tableau dont l'entrée serait en haut à gauche et la sortie en bas à droite. Quand un bloc est appelé pour la première fois, il se situe donc en haut à gauche. S’il n'est pas rappelé ou réutilisé il est alors déplacé lentement vers la sortie. Cependant s’il est à nouveau utilisé il sera automatiquement ramené vers l'entrée de la zone mémoire.

### La zone mémoire : Redo Log Buffer
Cette zone mémoire sert exclusivement à enregistrer toutes les modifications apportées sur les données de la base.
C’est une zone mémoire de type circulaire, le fait que cette zone mémoire soit de type circulaire et séquentielle, signifie que les informations de toutes les transactions sont enregistrées en même temps.

## Les processus d'arrière plan
### SMON
Le processus SMON (ou System Monitor) est un processus qui va servir à corriger les plantages de l'instance et à vérifier la synchronisation des données.
Si l'instance plante, c'est SMON qui va se charger de rejouer le contenu des REDO LOG FILE afin de pouvoir rejouer les transactions et de resynchroniser les données dans les fichiers de données.
SMON sert aussi à nettoyer les segments temporaires après leur utilisation. Il sert aussi à défragmenter les fichiers de données, tablespaces et autres.

### PMON
Le processus PMON (ou Process Monitor) va être surtout dédié aux processus des utilisateurs.
Il va servir à annuler les transactions d'une session (lors d'un plantage de la session par exemple), mais aussi servir à relâcher tous les verrous posés par la session, et à relâcher toutes les ressources détenues par la session.

### DBWn
Le processus DBWn (ou Database Writer) va être dédié à l'écriture du Database Buffer Cache dans les fichiers de données de la base de données.
Ce processus est aussi là pour vérifier en permanence le nombre de blocs libres dans le Database Buffer Cache afin de laisser assez de place disponible pour l'écriture des données dans le buffer.

### LGWR
Le processus LGWR (ou Log Writer) est le processus qui va écrire les informations contenues dans le REDO LOG Buffer dans les fichiers REDOLOG FILE lors des évenements suivants :
* Quand une transaction est terminée avec un COMMIT.
* Quand le REDO LOG Buffer est au 1/3 plein (peut dépendre de vos propres paramètres).
* Quand il y a plus de 1Mo d'informations de log contenues dans le buffer.
* Avant que DBWn n'écrive le contenu du Database Buffer Cache dans les fichiers du disque dur.

### CKPT
Ce processus va servir à mettre à jour les en-têtes des fichiers de données, et mettre à jour les fichiers CONTROL FILE afin de spécifier que l'action de CHECKPOINT s'est bien déroulée (par exemple lors d'un changement de groupe de REDO LOG FILES).
Le CHECKPOINT est un évènement qui se déclenche lors :
* D'un changement de groupe de REDO LOG FILE.
* D'un arrêt normal de la base de données (c'est à dire sans l'option ABORT).
* D'une demande explicite de l'administrateur.
* D'une limite définie par les paramètres d'initialisation.

### ARCn
Ce processus va avoir pour seule fonction de copier un fichier REDO LOG FILE à un autre emplacement.
Cette copie se déclenchera automatiquement en mode ARCHIVELOG (en mode NOARCHIVELOG le processus n'existe pas) lors du changement de groupe de REDO LOG FILE.

## Les processus serveurs
Lors d’une connexion utilisateur à la base de données, deux processus permettent à un utilisateur d'interagir avec l'instance et finalement avec la base de données : le processus utilisateur et le processus serveur.
Chaque fois qu'un utilisateur exécute une application telle qu’une application de gestion de ressources humaines, de gestion financière ou tout simplement une commande SQL, la machine client lance au préalable, un processus utilisateur pour établir une connexion de l'utilisateur à l'instance Oracle.

### Le processus d'écoute (Listener)
Le processus d’écoute Oracle listener est le principal composant Oracle coté serveur qui permet d'établir la connexion entre les ordinateurs clients et une base de données Oracle. Le listener peut être considéré comme une grande oreille qui écoute les demandes de connexion aux services Oracle.
Théoriquement, une machine serveur peut héberger plusieurs bases de données Oracle et un listener et un seul pour permettre la connexion d’un client à l’instance Oracle de son choix. Le nom de l’instance est soumis par le client lors du processus de connexion (étape 1).
Deux cas sont possibles :
1. Un processus d’écoute (Listener) peut servir plusieurs bases de données configurées sur une même machine serveur,
2. Plusieurs listeners peuvent être configurés sur une même machine (à des fins de basculement ou d'équilibre de charge pour supporter des charges importantes de demandes de connexion).

Dans une configuration de serveur dédié, le Listener lance pour chaque client un nouveau processus serveur et lui cède le contrôle de la session du client. Chaque connexion client est servie par son propre processus serveur.
Le schéma ci-dessus correspond à une configuration serveur dédié et pour une application client/serveur.
Le processus de connexion passe par les étapes suivantes :
1. Le client contacte le listener Oracle en choisissant l’instance à laquelle il souhaite se connecter (demande d’un nom de service).
2. Le listener démarre un processus dédié appelé processus serveur
3. Le listener envoie un accusé de réception au client avec l'adresse du processus serveur dédié
4. Le client établit une connexion avec le processus serveur dédié
5. Le processus serveur se connecte à l'instance Oracle pour le compte du processus utilisateur (création d’une session utilisateur)
C’est le processus serveur qui se connecte à l'instance Oracle pour servir le processus utilisateur durant toute la session du client.
Le processus utilisateur n'entre pas directement en interaction avec le serveur Oracle. C'est plutôt, le processus serveur qui interagit

### PGA
Une structure de mémoire supplémentaire appelée PGA (Programme Global Area) est créée pour chaque utilisateur connecté.
La PGA stocke des informations de contrôle spécifiques à la session de l’utilisateur, chaque processus serveur dispose de sa propre mémoire PGA privée qui lui est exclusivement réservée.
Lorsque le processus utilisateur se déconnecte (fin de session), le processus serveur associé prend fin et la mémoire PGA est libérée.

# La Base De Données
Comme vu précédemment une base de données est composée :
* D’un ou plusieurs fichiers de données, c’est dans ces fichiers que les données proprement dites sont stockées (tablespace.dbf).
* D’au moins un fichier de contrôle qui contient des informations de contrôle sur la base de données (control.ctl).
* D’au minimum deux groupes de fichiers de journalisation qui enregistrent toutes les modifications apportées à la base (redo.log).

## Fichiers de données
Les fichiers de données sont actualisés par les données insérées dans la base de données. Le tablespace est la structure logique des fichiers de données.
Un tablespace est un espace logique qui contient les objets stockés dans la base de données comme les tables, les index ou les données nécessaires à Oracle (dictionnaire de données).
Un tablespace est composé d'au moins un fichier de données qui est physiquement présent sur le serveur à l'endroit stipulé lors de sa création.
En termes de taille ce sont bien entendu les fichiers les plus importants.
Lors de la création d’une base de données (sous Oracle 10g), on retrouve habituellement les tablespaces suivants (les tablespaces SYSTEM et SYSAUX sont obligatoires) :
· SYSTEM : tablespace qui contient le dictionnaire de données.
· SYSAUX : tablespace auxiliaire du tablespace SYSTEM.
· TEMP : tablespace spécifique aux opérations de tri pour lequel la PGA ne serait pas suffisamment grande.
· UNDO : tablespace réservé exclusivement à l'annulation de requêtes SQL.
· USERS : tablespace par défaut pour tout nouvel utilisateur.

## Fichiers de contrôle
Un fichier de contrôle (control.ctl) est un fichier binaire, il contient des informations sur la structure physique de la base. Il est créé pendant la création d’une base de données et est modifié en permanence.
Ce fichier doit être toujours disponible car il est consulté et modifié fréquemment par le serveur Oracle. Il est indispensable pour la restauration d’une base de données.
Le fichier de contrôle contient notamment les informations suivantes :
· Informations sur la base
· Historique des fichiers de journalisation archivés
· Informations sur les tablespaces et les fichiers de données
· Date et heure de création de la base
· Le nom de la base
· Le mode d'archivage actuel
· Les numéros de séquence (de chaque journal)
· Informations sur les blocs corrompus
· L'ID de la base
On peut utiliser un seul fichier de contrôle mais Oracle en préconise au minimum deux sur des disques différents. Perdre tous les fichiers de contrôle rend difficile la restauration d’une base de données.

## Fichiers de journalisation
Oracle utilise les fichiers de journalisation pour être sûr que toute modification effectuée par un utilisateur ne sera pas perdue s'il y a défaillance du système.
Les fichiers de journalisation (redo.log) sont essentiels pour les processus de restauration.
Quand une instance s'arrête anormalement, il se peut que certaines informations dans les fichiers redo ne soient pas encore écrites dans les fichiers de données.
Oracle dispose les journaux redo en groupes. Chaque groupe a au moins un fichier redo. On doit avoir au minimum deux groupes distincts de fichiers redo, chacun contient au minimum un seul membre. Car, si l'on n'a qu'un seul fichier redo, Oracle ecrasera ce fichier redo et on perdra toutes les transactions.