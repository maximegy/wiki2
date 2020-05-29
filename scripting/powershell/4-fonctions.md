---
title: 4 Fonctions
description: 
published: true
date: 2020-05-29T22:28:29.603Z
tags: 
---

# Header

## Les Fonctions
Rappel: les fonctions sont des successions de commandes regroupées dans le but de réaliser certaines tâches
Reprenons un script blanc et créons une fonction vierge dans le fichier:

```powershell
function Get-OSInfo {
Write-Host "This function will dipslay OS information"
$osInfo = Get-WmiObject -Class Win32_OperatingSystem
Return $osInfo
}
Get-OSInfo
```

### Passer des variables en paramètre de la fonction
La fonction est utilisée par son nom.
Si on veut mettre des variables ou des données en entrée de la fonction il faut dans la fonction déclarer les positions de paramètres ainsi que la variable rattachée:

```powershell
function mafonction {
  param (
        [parameter(position=1)]
        $X,
        [parameter(position=2)]
        $Y,
        [parameter(position=3)]
        $ntry,
        [parameter(position=4)]
        $number
    )
}
```

