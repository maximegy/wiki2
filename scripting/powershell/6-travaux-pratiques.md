---
title: 6 Travaux Pratiques
description: 
published: true
date: 2020-05-29T22:31:35.342Z
tags: 
---

# TP 1 - les CMDlets
Premier script:
Créez un script permettant :
| Tâche                                                                                                                                                                                                             | Bon ordre                                                                                                                                                                                                        | Commande                                                                                                                                                                                                     |
| ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| Exporter les process en cours sur votre machine sur un fichier texte, en triant par celui consommant le plus de ressources au choix. Si vous le souhaitez, n'affichez que des informations que vous jugez utiles. | laisser le choix à l'utilisateur de où est créé le fichier                                                                                                                                                       | `$dossier = Read-Host "Veuillez renseigner le dossier"`<br/> `$fichier = Read-Host "Nom du fichier"` <br/> `$chemin = "$dossier\$fichier"` <br/> `Write-Host "L'export sera fait dans le fichier : $chemin"` |
| Ouvrir ce fichier texte après sa création                                                                                                                                                                         | vérifier que le dossier où le fichier est créé existe et si non, le créer                                                                                                                                        | `if (!(Test-Path -Path $dossier)) {New-Item -ItemType "directory" -Path $dossier}`                                                                                                                           |
| de le fermer automatiquement après 30 secondes                                                                                                                                                                    | Exporter les process en cours sur votre machine sur un fichier texte, en triant par celui consommant le plus de ressources au choix. Si vous le souhaitez, n'affichez que des informations que vous jugez utiles | `Get-Process | Select-Object Name,CPU | Sort-Object CPU -Descending | Out-File -FilePath $chemin`                                                                                                            |
| de supprimer ce fichier nouvellement créé                                                                                                                                                                         | Ouvrir ce fichier texte après sa création                                                                                                                                                                        | `notepad.exe $chemin`                                                                                                                                                                                        |
| de vérifier que le dossier où le fichier est créé existe et si non, le créer                                                                                                                                      | de le fermer automatiquement après 30 secondes                                                                                                                                                                   | `Start-Sleep -Seconds 10 & Get-Process *notepad* | Stop-Process`                                                                                                                                             |
| Bonus, laisser le choix à l'utilisateur de où est créé le fichier                                                                                                                                                 | de supprimer ce fichier nouvellement créé                                                                                                                                                                        | `Remove-Item $chemin`                                                                                                                                                                                        |

# TP 2 - les fonctions
Affinez votre fonction afin qu'elle remonte les informations suivantes:
- la version de Windows en cours sur votre machine
- Tous les disques disponibles ainsi que l'espace disponible sur chaque disque
- Le disque sur lequel est installé Windows et son chemin d'installation
- Le langage du système
Prenez soin de formater les résultats.


```powershell
function Get-OSInfo {
    $OS = Get-WmiObject -Class Win32_OperatingSystem
    $Culture = Get-Culture
    $Drive = Get-PSDrive -PSProvider 'FileSystem'
    Write-Host "version : $($OS.Version)"
    Write-Host "Language : $($Culture.DisplayName)"
    Write-Host "Disque Install : $($OS.SystemDrive)"
    Write-Host "Disques Disponibles : $($Drive.Name): $($Drive.Free/1gb)"
    }
Get-OSInfo
```


# TP 3 - Personnalisation du Shell
| Personnalisation de Base                                                                                          | Personnalisation avancée                                                                                                                                                                                                                                                                                                                                                                                  |
| ----------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| ![Personnalisation Powershell](/uploads/powershell/personnalisation-powershell.png "Personnalisation Powershell") | Le fichier de profil individuel est stocké dans la variable `$profile.CurrentUserAllHosts` <br/> Le fichier de profil global `$profile.AllUsersAllHosts` <br/> Les fichiers de profils sont chargés au lancement d'un shell, ils permettent de customiser les environnements utilisateurs et système. <br/> La function function Prompt { } permet de modifier les informations retournées par le prompt. |

Personnaliser son shell pour que chaque ligne retourne l'heure, l'emplacement actuel, l'utilisateur actuel...
Faire en sorte que le message d'accueil du shell teste votre,connexion vers google.com avec un message en fonction du succès ou de l'échec
Changer la couleur de la police du message du shell uniquement

```powershell
function prompt { 
    $date=$(Get-Date)
    $location=$(Get-Location)
    $user=$env:USERNAME
    Write-Host "$date $location $user" -NoNewline -ForegroundColor Green
    return ">"}
if (Test-Connection google.fr -Count 1) {Write-Host "Connection Google.fr OK"} else {Write-Host "Connection Google.fr NOK"}
```

# TP 4 - Calculatrice

Créer une calculatrice:
elle doit gérer les 4 opérations de base,
Elle doit retourner une erreur si les valeurs renseignées par l'utilisateur ne sont pas valides,
Gestion des décimales
Afficher des couleurs différentes pour un nombre de chiffres d'entiers différents devant la virgule (1 => Bleu, 2 => Rouge, 3 => Noir, etc)
Intégrer des debug et des verboses, qui commentent les actions entreprises par le script au fur et à mesure
elle ne doit pas se fermer tant que l'utilisateur ne l'a pas demandé

# TP 5 - Modules
Récupérer le fichier "Joli_Texte.txt"
- Identifiez les fonctions du script et expiquez les
- Importez ce script en tant que modue et faites le fonctionner uniquement par des commandes
- Faites fonctionner ce script avec un autre script. Faites appel à une boucle dans ce dernier.
- Enlevez le module.


```powershell
# Renommer le fichier
Rename-Item -Path C:\... -NewName joli_texte.psm1
Move-item
Copy-item
# Déplacer
Move-Item; Copy-Item; Get-content | out-file 
# Créer dossier 
New-item -Path *path* -Type Directory
# Importer
New-ModuleManifest -Path *Path\module.psd1* -NestedModules *Path\module.psm1*
Get-Module-List-Available
Import-Module *NomDuModule*
```

utilisation : 

```powershell
Write-Pretty "texte" "type"
Write-Pretty -PrettyText "texte" -texttype "type"
Commande | Write-Pretty -textype "type"
```



# TP 6 - Help documentation
En vous appuyant sur les déductions faites sur le script "Joli_Texte". Constituez l'aide.
Voici les éléments a faire apparaitre:
- Que font les Rando; Error; Warning et Info,
- Quels sont les paramètres et comment s'en sert-on
- Des exemples d'usages

Les paramètres qui devraient remonter..
- `Get-Help`
- `Get-Help -detailed`
- `Get-Help Write-Pretty -Parameter prettyText & textType`
- `Get-Hep Write-Pretty -Examples`