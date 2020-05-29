---
title: 2 PowerShell - Bases
description: 
published: true
date: 2020-05-29T22:26:30.269Z
tags: 
---

Documentation officielle : [docs.microsoft.com](https://docs.microsoft.com/en-us/powershell/#pivot=main&panel=getstarted)


-----

# Symboles
| Symbole | Nom                           | Description                                                                                                                                                                                       |
| ------- | ----------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **$**   | Dollar                        | Préfixe le nom d'une variable, `$_` est l'objet en cours.                                                                                                                                         |
| **[]**  | Crochets                      | Encadre un type de variable ou l'indice des éléments d'un tableau. <br/> Exemple: `[int]`, `$var`ou `$tableau[$i]`                                                                                |
| **{}**  | Accolades                     | Encadre un ensemble de code (bloc d'instructions, expressions, filtres, boucles, ...)                                                                                                             |
| **()**  | Parenthèses                   | Groupe de commandes ou d'expressions (évite l'ambiguité des évaluations)                                                                                                                          |
| **\|**  | Pipe                          | Pipeline (enchainement de commandes et/ou de filtres), peut être mis en fin d'une ligne de commande dans un script, la suite sur la ligne suivante                                                |
| **.**   | Point                         | Membre d'une instance d'objet (méthode ou propriété), séparateur décimal (la virgule étant un séparateur de valeur)                                                                               |
| **,**   | Virgule                       | Séparateur de valeur, typiquement pour les éléments d'un tableau                                                                                                                                  |
| **..**  | Point Point                   | Plage de valeurs (exemple 1..10 désigne tous les chiffres de 1 à 10)                                                                                                                              |
| **::**  | Double 2 points               | Membre statique d'une classe .NET                                                                                                                                                                 |
| **%**   | Pourcent                      | Reste de division (Modulo) Ou alias de la commande de boucle ForEach `%{_}`                                                                                                                       |
| **#**   | Dièse                         | Commentaire ou <# bloc de commentaire #>                                                                                                                                                          |
| **\`**  | Anti-quotte <br/> ou Backtick | Caractère d'échappement (évite l'interpretation du caractère qui suit), permet de couper une ligne d'instruction s'il est situé en fin de ligne                                                   |
| **?**   | Point d'interrogation         | Alias de la commande `Where-Object`                                                                                                                                                               |
| **;**   | Point virgule                 | Permet d'écrire plusieurs instructions sur la même ligne (ou de terminer explicitement une ligne d'instruction, et ainsi éviter une erreur d'interprétation lorsque le retour ligne est supprimé) |
| **@**   | Arrobase                      | Tableau de valeurs si suivi de parenthèses `@()` ou table de hachage si suivi d'accolades @{}. Cas particulier pour du texte @' string '@                                                         |
| **&**   | Esperuette                    | Opérateur d'invocation ou d'appel (Execution d'un bloc de script ou d'une commande)                                                                                                               |
| **!**   | Point d'exclamation           | Opérateur logique d'inversion équivalent à "-not"                                                                                                                                                 |
| **"**   | Guillements                   | Encadre typiquement une chaine "non protégée". Les variables $... sont remplacées par leur valeur respective ou rien si vide                                                                      |
| **'**   | Simple quottes                | Encadre strictement une chaine en évitant toute interprétation des caractères qu'elle contient"                                                                                                   |



# Cmdlets
## A propos
Une cmdlet est une commande PowerShell avec une fonction prédéfinie suivant la logique "Action" - "information".
* Il existe des applets de commande système, utilisateur et personnalisé,
* Les résultats des CMDlets en sortie sont des objets ou des tableaux d'objets, il faut voir ça comme un conteneur qui contient des propriétés et ainsi de suite, comme des poupées russes.
	 Les objets les plus simples sont ainsi exploitables :
```powershell
> 'Hello World'.Lenght
11
```

   Et manipulables
```powershell
> 'Hello World'.ToLower()
hello world
> 'Hello World'.ToUpper()
HELLO WORLD
```

* Les Cmdlets sont fournis par Microsoft,
* Les Cmdlets créés sont des Cmdlets-like,		
* Les applets de commande peuvent obtenir des données à analyser ou transférer des données vers une autre applet de commande à l'aide de canaux,
* Les cmdlets sont insensibles à la casse, par exemple `Get-Aduser`, `get-aduser` ou encore `GeT-ADUseR` fonctionnent,
* Dans une chaine, si on veut utiliser plusieurs cmdlets, il faut les séparer par un point-virgule (`;`).

## Format
La structure d'une cmdlet consiste toujours à un **verbe** suivi d'un **nom**. Les verbes les plus connus sont:
- `Get` : pour obtenir quelque-chose,
- `Set` : pour définir quelque-chose,
- `Start` : pour executer quelque-chose,
- `Stop` : pour arrêter quelque-chose,
- `Out` : pour retourner quelque-chose,
- `New` : pour créer quelque-chose.

Commandes les plus importantes :
- "`| gm`" pour "`Get-Member`" permet de récupérer les membres, propriétés, paramètres et méthodes des objets.
- `Get-Verb` permet d'avoir une vue sur l'ensemble des verbes utilisés.
- `Get-Help` permet d'avoir des informations sur les commandes, cmdlets et autres.

"`Get-Command -CommandType Cmdlet | Group-Object Verb | Sort-Object Count -Descendig | Format-Table --Autosize`"
Les Alias (`Get-Alias`) Permettent de créer des raccourcis pour exécuter des commandes communes
`Get-Command`: Permet de découvrir les commandes par exemple toutes les commandes relatives aux processus (`Get-Command -Name "*process*"`)

Appliquons l'utilisation d'une commande sur un exemple pratique:
- `Get-Process` retourne les process
- `Get-Process | Format list` permet d'avoir une liste séparant chaque item.

Un petit mix de toutes les informations pour avoir, par exemple, les process qui consomment le plus de CPU
- `Get-Process | Select-Object Name,CPU | Sort-Object CPU -Descending | Format-Table -Autosize`
- Powershell est également en mesure d'afficher un tableau exporté en utilisant la commande Out-GridView

Les chevrons '`>`' et '`>>`' permettent respectivement d'exporter des résultats dans un fichier.
Par exemple:
```powershell
Get-Process > processes.txt
Start-Process .\processes.txt
```

Rappel d'objet avec le pipe: le pipe permet d'utiliser un objet récupéré dans une commande précédente (`Select-Objet`, `Out-File`...)
Un exemple pratique pour agir sur une machine: `Get-Process notepad | Stop-Process`

( ) > comparaison t paramètres
{ } > Block d'instruction
" " > Litéral
' ' > string pur
\` \` > paramètre d'échappement pour les `' '`

## Paramètres
Chaque CMDlet possède de nombreux paramètres permettant de personnaliser son fonctionnement. PowerShell ISE et Visual Studio Code suggèrent tous les paramètres et leur types après avoir écrit la commande suivi d'un tiret.  

![Parametres](/uploads/powershell/parametres.png "Parametres"){.align-center}

## Pipes
Les pipes ( "|" - barre verticale), renvoient les données d'une cmdlet à une autre.
Par exemple :
`Get-Service | Sort-Object -property Status`
Le résultat de la commande `Get-Service` est redirigé dans la commande `Sort-Object -property Status`. Tous les services sont donc triés par leur statut.
Il est possible d'utiliser plusieurs pipes par exemple:
`Get-Service | WHERE {$_.status -eq "Running"} | SELECT displayname`
La commande liste les services, exclue les services arrêtés et affiche seulement leur nom.
Pour information : `$_` defini l'element  actuellement dans le pipe.



## Alias
On peut aussi créer des alias qui sont des noms de cmdlets raccourcis.
Par exemple, à la place de `Get-Help`, on peut juste entrer `Help`

```powershell
Start-Process notepad
start notepad
```

ou encore

```powershell
Stop-Process -Name notepad
spps -Name notepad
```




-----

## CMDlet-like
Afin d'améliorer les fonctions, il est possible d'ajouter une fonctionnalité Powershell simple à cette dernière [cmdletbinding()]

```powershell
function Invoke-AdvancedFunctionality {
[cmdletbinding()]
param()
	Write-Verbose "Cette fonction est maintenant avancée !"
}
Invoke-AdvancedFunctionality
```



