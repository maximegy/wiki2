---
title: Apprehender les Bases de Données
description: 
published: true
date: 2020-05-29T22:35:36.129Z
tags: 
---

# Définition
La Base de Données (BDD), DataBase en anglais (DB), est un lot d'informations stocké dans un dispositif informatique. 
Les technologies existantes permettent d'organiser et de structurer la base de données de manière à pouvoir facilement manipuler le contenu et stocker efficacement de très grandes quantités d'informations.

# Système de gestion de base de données
Le Système de Gestion de Bases de Données, SGBD ou DBMS en anglais, est un logiciel qui sert à la **manipulation** de bases de données.
LA BDD étant statique, un système est nécessaire pour la gérer.
Il sert à effectuer des opérations ordinaires telles que *consulter*, *modifier*, *construire*, *organiser*, *transformer*, *copier*, *sauvegarder* ou *restorer* des bases de données.
La majorité des SGBB du marché manipule des Bases De Données relationnelles.

# SGBD en entreprise
Une entreprise doit conserver un volume élevé d’informations : noms, adresses, salaires, fournisseurs, clients, numéros de téléphone, demandes, incidents, affaires, quantités, prix, bilan financier, …
Ces informations se retrouvent dans différents systèmes de traitement :
* ERP,
* Système de gestion des stocks,
* Système de facturation,
* Système de préparation de paie,
* Programme de gestion de personnel,
* Gestion du patrimoine immobilier,
* …
La gestion peut devenir complexe, c’est là que les SGBD interviennent !


Utilisateurs>
Concepteurs analystes>
                            Principaux acteurs
Développeurs>
Administrateurs DBA>

# Base de données relationnelle
Dans une base de données relationnelle, les données sont enregistrées dans des tableaux à deux dimensions appelés tables. La manipulation de ces données se fait selon la théorie mathématique des relations (créé par Edgar Frank Codd en 1970).
Le modèle relationnel est une manière de modéliser les relations existantes entre plusieurs informations, et de les ordonner entre elles.
Selon le modèle relationnel, il peut y avoir plusieurs relations connectées implicitement par les valeurs qu'elles contiennent. Dans une base de données relationnelle, chaque enregistrement d'une table contient un groupe d'informations relatives à un sujet et les différents sujets sont connexes. Les liens existant entre les informations sont stockés dans les champs des enregistrements sous forme de **clé primaire** et **clé étrangère**.
La majorité des SGBD actuels est basé sur le modèle relationnelle (SGBDR).

# Principaux SGBDR

| SGDBR      | Description                                                                                                                                                                                                                                                                                                                                            |
|------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Access     | Produit commercial de Microsoft intégré à la suite office. Il est facilement gérable et est destiné à des BDD de petites tailles.                                                                                                                                                                                                                      |
| SQL Server | Produit commercial de Microsoft. La version "express" est gratuite. L'installation est initialement destinée à un environnement Windows mais il existe une portabilité vers Linux depuis la version 2016. Il est destiné à des BDD de moyenne et grande taille.                                                                                        |
| SQLite     | Solution Open Source, c'est une système de BDD embarqué, simple et limité. Il est notamment intégré a firefox, skype, android…                                                                                                                                                                                                                         |
| MySQL      | Anciennement SUN, maintenant Oracle. Commercial pour le support, la version "community" est gratuite. Très populaire notamment pour les serveurs WEB (LAMP). Il intègre désormais du clustering et de nouvelles consoles d'administration.                                                                                                             |
| MariaDB    | C'est un Fork de MySQL 5.1 (après le rachat de SUN par Oracle) par la fondation MariaDB. Il est soutenu notamment par Red Hat.                                                                                                                                                                                                                         |
| PostgreSQL | Développé par la communauté eponyme, il est opensource, a une très bonne réputation et est très performant. Idéal pour commencer.                                                                                                                                                                                                                      |
| Oracle     | Oracle Database, édité par Oracle Corporation est un logiciel commercial, la version "XE" est gratuite mais est déconseillée car top jeune, buggé, et moyen niveau sécurité. Les performances d'Oracle Databases sont excellentes, ses fonctionnalités aussi. Il est adapté aux Grosses et très grosses BDD. Par contre c'est un produit très couteux. |

# Architecture client / serveur
Le client est un ordinateur qui fournit une interface entre l'usager et l'application informatique.
1. Accepte les demandes de l'utilisateur,
2. Effectue une requête au serveur,
3. Affiche le résultat à l'écran.

Le serveur est un ordinateur connecté à un réseau qui fournit des services à d'autres ordinateurs (clients).
1. Reçoit les requêtes des ordinateurs clients,
2. Exécute les requêtes,
3. Retourne le résultat aux clients.

# Architecture 3 tier
Poste client > serveur Wab > Serveur BDD

# Définition: BDDR
C'est un stock d'informations décomposées et organisées dans des tableaux à deux dimensions appelés tables.

Qu'est ce qu'une table:
Elle a un nom,
Elle est composées de colonnes et de lignes.

# Présentation SQL
SQL: Structured Query Langage
Le SQL se subdivise en différents langages permettant soit la définition des éléments d'une base de données: 
- la **manipulation des données**,
- la **gestion des droits d'accès** aux données et des transactions,
- l'**extraction des données**.
C'est un lagage de type déclaratif, c'est à dire que l'on spécifie les propriétés des données que l'on souhaite manipuler logiquement.

## SQL SELECT 
L’utilisation la plus courante en SQL consiste à lire des données issues de la base de données.
Cela s’effectue grâce à la commande SELECT, qui retourne les enregistrements d’une table.
Syntaxe :
```sql
SELECT lacolone1>,lacolone2>
FROM latable
WHERE {condition};
```

Exemple: Afficher le prénom et le nom de la table "employees" dont le salaire est supérieur à 10000:
```sql
SELECT first_name, last_name FROM employees WHERE salary > 10000;
```

## INSERT
L'insertion de données dans une table s'effectue à l'aide de la commande INSERT INTO

Syntaxe :
```sql
INSERT INTO latable (lacolone1, lacolone2)
VALUES (lavaleur1, lavaleur2)
```

Exemple
```sql
INSERT INTO employees (id, first_name, last_name, hire_date, job_id, salary)
VALUES (300, 'Florian', 'DAUBORD', sysdate, 'IT_DBA', '420000');
```

## UPDATE
La commande UPDATE permet d’effectuer des modifications sur des lignes existantes.
Très souvent cette commande est utilisée avec WHERE pour spécifier sur quelles lignes doivent porter la ou les modifications.

Syntaxe :
```sql
UPDATE latable
SET lacolone1 = lavaleur1, lacolone2 = lavaleur2, …
WHERE {condition} ;
```

Exemple :
```sql
UPDATE employees SET salary = 1000000 WHERE id = 300;
```

## DELETE
La commande DELETE en SQL permet de supprimer des lignes dans une table.
Très souvent cette commande est utilisée avec WHERE pour spécifier quelles lignes doivent être supprimées.

Syntaxe :
```sql
DELETE FROM latable
WHERE {condition};
```

Exemple :
```sql
DELETE FROM employees WHERE id = 300;
```

# Intégrité et transaction
Plusieurs utilisateurs doivent pouvoir accéder aux données et les modifier sans qu'il en résulte de dégâts causés par des manipulations qui s'enchevêtrent. C'est ce que l'on appelle le respect de l'intégrité des données.
Les transactions sont la clef même de toute problématique d'accès concurrent.
Une transaction est un ensemble cohérent de modifications faites sur les données. Une transaction est soit entièrement annulée (ROLLBACK), soit entièrement validée (COMMIT).
Tant qu'il n'y a pas eu COMMIT, seul l'utilisateur courant voit ses mises à jour.
