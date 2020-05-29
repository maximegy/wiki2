---
title: 1 PowerShell - Introduction
description: 
published: true
date: 2020-05-29T22:25:04.820Z
tags: 
---

# Algorithmique de Base
Mettre un utilisateur dans un groupe:

![Algorithmique](/uploads/powershell/algorithmique.png "Algorithmique"){.align-center}

Traduction d'une série d'action pour obtenir un résultat en définition systématique.

-----

# Présentation
## Introduction
Powershell est la volonté de Microsoft de fournir une plateforme d'automatisation, de scripting et d'une variété d'autres fonctions afin de concurrencer les shells du marché:
- Fournir une vraie interface robuste d'administration scriptée,
- Offrir une logique dans les commandes "verbe-nom",
- Remplacer l'obsolète "CMD".
PowerShell offre à la fois une console en ligne de commande et un environnement de scripting intégré.
* Pour lancer la console PowerShell, tapez PowerShell.exe dans le menu Démarrer de Windows.  

![Console Powershell](/uploads/powershell/console-powershell.png "Console Powershell"){.align-center}
* Pour lancer PowerShell ISE (Integrated Scripting Environment), tapez powershell_ise.exe dans le menu démarrer. Cet environnement est un bon moyen de travailler sur les scripts car il fournit notamment l'auto completion, la coloration du code et les fonctionnalités d'automatisation et de simplification de développement et test de code.  

![Powershell Ise](/uploads/powershell/powershell-ise.png "Powershell Ise"){.align-center}
* Un autre logiciel peut être pratique pour développer les scripts non seulement PowerShell mais aussi d'autres langages. Ce logiciel développé par Microsoft est disponible gratuitement en installation complète mais aussi sans droits administrateurs dans les dossiers de l'utilisateur. Il prend nativement en charge Git et de nombreuses extensions permettent de le rendre encore plus puissant. Visual Studio Code permet une reconnaissance du langage comme PowerShell_ISE. il propose aussi le débogage, l'autocompletion et l'explication des commandes tapées.  

![Visual Studio Code](/uploads/powershell/visual-studio-code.png "Visual Studio Code"){.align-center}
Les deux derniers logiciels permettent :
- IntelliSense : les commandes s'autocomplètent et montrent les options (extension PowerShell sur VSCode),
- Debbugging de script,
- Comparaison des fichiers récents,
- Mise en évidence des synthaxes.

## Versions
Depuis sa création, PowerShell a évolué jusqu'à devenir un langage puissant et très flexible.
|                | Server 2003 et 2003 R2 | Server 2008 et 2008 R2 | Server 2012 et 2012 R2 | Windows 7 et 8.1 | Windows 8 | Windows 10 |
| -------------- | ---------------------- | ---------------------- | ---------------------- | ---------------- | --------- | ---------- |
| Version 1      | OK                     | NOK                    | NOK                    | NOK              | NOK       | NOK        |
| Version 2      | OK                     | OK                     | OK                     | OK               | OK        | NOK        |
| Version 3      | NOK                    | OK                     | OK                     | OK               | OK        | NOK        |
| Version 4 et + | NOK                    | OK                     | OK                     | OK               | NOK       | OK         |

La version de Powershell est stockée dans la variable système `$host`. Pour obtenir seulement la version : `$host.version`.

## Avant tout
Par défaut et par sécurité la politique de Microsoft est de restreindre l'exécution de scripts. Pour vérifier la politique d'exécution, lancer la commande `Get-Execution Policy` dans une console PowerShell lancée en administrateur.

4 valeurs sont possibles:
* **Restricted** : Aucun script est autorisé. C'est la politique par défaut.
* **AllSigned** : Il est possible d'exécuter les scripts signés par un developper de confiance. Avec cette politique, il est demandé de confirmer le lancement du script.
* **RemoteSigned** : Il est possible de lancer ses propres scripts ou les scripts signés par un développeur de confiance.
* **Unrestricted** : On peut lancer n'importe quel script.

Pour commencer à travailler avec PowerShell, il faut configurer la politique d'exécution de Restricted à RemoteSigned ou Unrestricted par la commande: `Set-ExecutionPolicy RemoteSigned`.

Terminologie:
* **Cmdlets**: Ce sont essentiellement des commandes qui interagissent avec du code .NET sr des fonctions définies par les commandes
* **Scripts**: Les scripts dont des fichiers .ps1 exécutables qui contiennent une série de commandes PowerShell
* **Fonctions**: une fonction est une série de commandes groupées qui, ensemble, permettent de réaliser une certaine tâche.