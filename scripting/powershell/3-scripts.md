---
title: 3 PowerShell - Scripts
description: 
published: true
date: 2020-05-29T22:27:30.457Z
tags: 
---

# Scripts
## Commentaires
Laisser des commentaires dans un script va vous permettre ainsi qu'aux différents utilisateurs du script de mieux comprendre ce que le script fait. Un commentaire peut être une ligne commençant par un dièze (#) ou un bloc sur plusieurs lignes commençant et finissant par des dièzes et des chevrons :

```powershell
# simple commentaire
<# commentaire
sur plusieurs
lignes #>
```


---

## Write

`Write-Host` : sert à présenter de la donnée lisible sous forme de texte.
Utilie pour suivre le déroulement d'un script et présenter des menus
`Write-Output` : set à envoyer des objets dans le 'pipeline' Ce qui veut dire que le prochain objet dans le shell/script sera lisible.
`Write-Verbose` : Permet d'afficher ou non le texte associé avec l'argument -Verbose

---

## Variables
| Types     | Description                                             |
| --------- | ------------------------------------------------------- |
| array     | liste de valeurs                                        |
| bool      | valeur booléenne (Vrai ou Faux)                         |
| byte      | nombre en 8 bits                                        |
| char      | suite de charactère en 16bits                           |
| decimal   | nombre pouvant comprendre un point en 128 bits          |
| single    | nombre pouvant comprendre un point en 32 bits           |
| double    | nombre pouvant comprendre un point en 64 bits           |
| hashtable | Stocker des objets sous forme de clé-valeur (key-value) |
| int       | entier sur 32 bits                                      |
| long      | entier sur 64 bits                                      |
| string    | chaine de caractère Unicode (2 milliards de caractères) |
| xml       | objet XML                                               |



-----
## Les blocs conditionnels
### Les comparateurs

Les comparateurs permettent de specifier les conditions de comparaison des valeurs et de déterminer les valeurs qui correspondent aux modèles spécifiés.
| Type                                                              | Opérateur                                                                  | Description                                                          |
| ----------------------------------------------------------------- | -------------------------------------------------------------------------- | -------------------------------------------------------------------- |
| Egalité                                                           | `-eq`                                                                      | égal à                                                               |
| `-ne`                                                             | n'est pas égal à                                                           |
| `-gt`                                                             | plus grand que                                                             |
| `-ge`                                                             | plus grand ou égal                                                         |
| `-lt`                                                             | plus petit que                                                             |
| `-le`                                                             | plus petit ou égal                                                         |
| `-c`                                                              | placé devant l'opérateur, active la sensibilité à la casse ex : `-ceq`     |
| `-i`                                                              | placé devant l'opérateur, explicite l'insensibilité à la casse ex : `-ieq` |
| Correspondance                                                    | `-like`                                                                    | Retourne Vrai si la chaine est semblable au motif                    |
| `notlike`                                                         | Retourne Vrai si la chaine n'est pas semblable au motif                    |
| `match`                                                           | Retourne vrai si la chaine correspond à l'expression régulière             |
| `notmatch`                                                        | Retourne vrai si la chaine ne correspond pas à l'expression régulière      |
| `$match`contient la chaîne correspondant à l'expression régulière |
| Contenant                                                         | `-contains`                                                                | Retourne vrai quand le motif de référence est contenu dans  le motif |
| `-notcontains`                                                    | Retourne vrai quand le motif de référence n'est pas contenu dans  le motif |
| `-in`                                                             | Retourne vrai quand la valeur testée est contenue dans le motif            |
| `-notin`                                                          | Retourne vrai quand la valeur testée n'est pas contenue dans le motif      |
| Type                                                              | `-is`                                                                      | Retourne vrai si les deux objets sont de même type                   |
| `-isnot`                                                          | Retourne vrai si les objets ne sont pas de même type                       |


### if then else elsif

### switch
Case = switch > conditions, aiguillage indexé


### Les boucles
Il y a plusieurs types de boucles en Powershell. Plusieurs peuvent servir le même but, mais il y a souvent une plus adaptée qu'une autre par cas.
#### La boucle ForEach
Cette boucle permet de parcourir un tableau ou une collection composée de 0 à n éléments sans se préocuper du nombre.

```powershell
ForEach ($element in $listeelement) {
Faire quelque chose
}
```

L'élément peut être une dénomination de votre choix.
$element vaut l'item de la liste d'element traité au niveau de la boucle:
| liste | tour de boucle | valeur de `$element` |
| ----- | -------------- | -------------------- |
| toto  | 1              | toto                 |
| tata  | 2              | tata                 |
| titi  | 3              | titi                 |
Liste element vient d'une source, par exemple récupérée lrs d'une autre commande.
Exemple:

```powershell
$process = Get-Process
$i = 1
ForEach ($proc in $process)
	Write-Host "le process numéro $i est $($process.Name)"
	$i++
}
```


 #### La boucle For
 
 for (valeur de départ;test ou condition;nombre d'itération) {
 FaireQuelquechose
 }
 
 Par exemple

```powershell
 for ($i=1;$i -le 15; $i++ {
	 Write-Host "Ceci est la couleur $i" -ForegroundColor $I
}
```


Les conditions sont au choix pouvant créer une boucle infinie

```powershell
for () { Write-Host "Wheeeeeeeeeeee!"}
```


On privilégiera les boucles For lorsqu'on veut exécuter un même ensemble de code plusieurs fois, pour une raison ou une autre.

#### La boucle While
les boucles While continuent tant qu'une condition est vraie

While (condition)

on peut par exemple ouvrir plusieurs instances d'un programme
```powershell
$notepad = Get-Process Notepad
While ($notepad.Count -le 5) {
	block de condition
}
```

#### La boucle Do
La différence avec la boucle While, l'action se fera systématiquement au moins une fois.
La condition peut être traitée par "until" ou "while", selon l'opération de comparaison et l'évaluation.

```powershell
do {
  $valeur++
  Write-Host $valeur
} until | while ($valeur –ge | –le 10)
```
---

## Blocks d'instruction
Il existe plusieurs blocks {} permettant de traiter des 

---

## Gestion des strings
Un string est un objet powershell qui dispose de ce 'type'.
Par exemple
```powershell
$MyPath = Get-Location
$MyPath | Get-Member
```

A l'instant T, on voit qu `$MyPath`est un objet avec un type:
```Powershell
$MyPath | Get-Member
   TypeName : System.Management.Automation.PathInfo
```

Pour récupérer le sting du chemin, on utilisera donc:
`$MyPath.Path`

Désormais, on constate que le TypeName change
```Powershell
$MyPath.Path | Get-Member
	TypeName : System.String
```

### Manipulation
Il est désormais possible de manipuler le résultat obtenu en tant que string.
`$ourPath = (GetLocation).Path`
#### Method : Substring

Qu'affiche `$ourPath.Substring(0,8)`
-> les 8 premiers caractères
et `$ourPath.Substring(5,5)`
-> les 5 caractères à partir du 5e caractère

#### Method: LastIndexOf
A qoi correspond le résultat de `$ourPath.lastIndexOf('\')`
-> la position du dernier `\`
A quoi correspond alors le résultat de `$ourPath.Substring($ourPath.LastIndexOf('\')+1)`
->ce qui suit le dernier `\`

La commande à suivre permet d'obtenir les noms des dossiers dans le dossier courant:
```Powershell
Get-ChildItem C:\ -Directory | Select-Object -ExpandProperty Name
```

Avec les commandes vues précédemment, on obtient le même résultat:
```Powershell
$var = Get-ChildItem C:\
foreach($element in $var)
{
    if ($element.mode -match "-")
    {
        $element.FullName.Substring($element.FullName.LastIndexOf('\')+1)
    }
}
```

Les strings étendus permettent d'écrire la valeur d'une variable à l'intérieur d'un string aavant qu'il soit exéécuté et affiché. Ces dernières sont entourées de guillements
```Powershell
$test = Ceci est un test
Write-Host "Test : [$test]"
$process = Get-Process
```
Les strings littéraux, intégrés entre simples guillemets `'` permettent d'intégrer tous les caractères de la chaine.


L'opérateur `-F` permet de mettre en forme des strings dans de manières diverses en se vasant sur leurs prédéfinitions:
```Powershell
$user = (Get-ChildItem Env:\USERNAME).value
$date = get-date
"your user is {0}, and the time is [{1:HH}:{1:mm}:{1:ss}]" -f $user,$date
```

Les conversions vers un string se font avec l'appel de la méthode associée (GM)
```Powershell
[int]$number = 10
$number | gm
$numberString = $number.ToString()
$numberString | gm
```

Comme vu précédemment il est également possible de forcer le type de contenu d'une variable
```Powershell
[int]$number
[string]$number
```

Construire un *ScriptBlock*
Il est possible de construire un block de script dont on pourra ensuite faire usage dans d'autres commandes
En premier lieu, il faut déclarer la variable et l'expression
```Powershell
$findprocess = 'chrom'
$expression = [scriptblock]::Create("Get-Process $findProcess | Select-Object ProcessName, CPU, Path | Format-List")
```

Et le lancer:

```Powershell
Start-Job -Name "$findProcess`Process" -ScriptBlock $expression
Receive-Job "$findProcess`Process"
Get-Job "$findProcess`Process" | Remove-Job
```

```$x = 1
while ($x -ne 25)
New-AdUser -Name "risr$x" -AccountPassword $password -ChangePasswordAtLogon $false
Set-1ADUser risr$x 
$x++
}```