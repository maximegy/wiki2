---
title: 8 PowerShell : Administration AD
description: 
published: true
date: 2020-05-29T22:33:40.420Z
tags: 
---

```Powershell
New-ADOrganizationalUnit -Name Maxime_VINCENT -Path "OU=TP,DC=testrisr,DC=cesi"
$password = ConvertTo-SecureString -String "P@ssw0rd" -AsPlainText -Force
New-ADUser -Name maxime.vincent -Path "OU=Maxime_VINCENT,OU=TP,DC=testrisr,DC=cesi" -AccountPassword $password -enabled $true
Add-ADGroupMember -Identity risradm -Members maxime.vincent
```



```Powershell
$valeur = ('Comptabilite').Substring(0,6)
New-ADGroup "MV_$valeur" -GroupScope Global -Path "OU=Maxime_VINCENT,OU=TP,DC=testrisr,DC=cesi"
$table = "Admin","Editor","Reader"
foreach($elem in $table) {
    $group = "MV_"+"$valeur"+"_"+"$elem"
    New-ADGroup -Name "$group" -GroupScope Global -Path "OU=Maxime_VINCENT,OU=TP,DC=testrisr,DC=cesi"
    Add-ADGroupMember -Identity "MV_$valeur" -Members "$group"
}
```



```Powershell
$password = ConvertTo-SecureString -String "pwd123!!" -AsPlainText -Force

ForEach ($nom_source in "Comptabilité","Ressources-Humaines","Moyens-Generaux")
    {
    New-ADGroup -Name "MV_$nom_source" -GroupScope Global -Path "OU=Maxime_VINCENT,OU=TP,DC=testrisr,DC=cesi"
    $nom_court="MV_$($nom_source.Substring(0,6))"
    $i=1
    ForEach ($nom_extension in "Editor","Admin","Reader")
        {
        New-ADGroup -Name $nom_court"_"$nom_extension  -GroupScope Global -Path "OU=Maxime_VINCENT,OU=TP,DC=testrisr,DC=cesi"
        Add-ADGroupMember -Members $nom_court"_"$nom_extension -Identity "LG_$nom_source"
        New-ADUser "$($nom_court).user0$($i)" -AccountPassword $password -ChangePasswordAtLogon $false -Enabled $true -Path "OU=Maxime_VINCENT,OU=TP,DC=testrisr,DC=cesi"
	    Add-ADGroupMember -Members "$($nom_court).user0$($i)" -Identity "$($nom_court)_$($nom_extension)"
        $i++
        }
    }
```

UNPACKED

# SQL
```Powershell
$dbinstance = "ADRLA\SQLEXPRESSRISR"
$dbrisr = "RISRDB"
Invoke-Sqlcmd -Query "
    CREATE TABLE Maxime_VINCENT (
        Nom varchar(255),
        Serv varchar(255),
        DateArrivee varchar(255),
        Pays varchar(255),
        Ville varchar(255),
        Numero varchar(255),
        Matricule varchar(255)
    )
" -Database $dbrisr -ServerInstance $dbinstance
```

```Powershell
$country = "France"
$city = "Toulouse"
$service = "Infrastructure" Invoke-Sqlcmd -Database $dbrisr -ServerInstance $dbinstance -Query "
    INSERT INTO [dbo].[Maxime_VINCENT]
    ([Nom],[Serv],[DateArrivee],[Pays],[Ville],[Numero],[Matricule])
    VALUES
        ('MV_user1',`'$service`','15/03/2019',`'$country`',`'$city`','0611111111','RISR17XMV01'),
        ('MV_user2',`'$service`','15/03/2019',`'$country`',`'$city`','0622222222','RISR17XMV02'),
        ('MV_user3',`'$service`','15/03/2019',`'$country`',`'$city`','0633333333','RISR17XMV03'),
        ('MV_user4',`'$service`','15/03/2019',`'$country`',`'$city`','0644444444','RISR17XMV04'),
        ('MV_user5',`'$service`','15/03/2019',`'$country`',`'$city`','0655555555','RISR17XMV05')
"
Invoke-Sqlcmd -Database $dbrisr -ServerInstance $dbinstance -Query "SELECT * FROM [dbo].[Maxime_VINCENT]"
```

```Powershell
Invoke-Sqlcmd -Database $dbrisr -ServerInstance $dbinstance -Query "CREATE TABLE Maxime_VINCENT_GROUPS (Nom varchar(255),Descript varchar(255))" 

Invoke-Sqlcmd -Database $dbrisr -ServerInstance $dbinstance -Query "INSERT INTO [dbo].[Maxime_VINCENT_GROUPS] ([Nom],[Descript]) VALUES ('MV_Group1','RISR17XMV01-Group'),('MV_Group2','RISR17XMV02-Group')"


$groupesel=Invoke-Sqlcmd -Database $dbrisr -ServerInstance $dbinstance -Query "SELECT * FROM [dbo].[Maxime_VINCENT_GROUPS]"
$groupesel
Foreach ($resultgrp in $groupesel)
    {
    New-ADGroup -Name $($resultgrp.Nom) -Description $($resultgrp.Descript) -GroupScope Global -Path "OU=Maxime_VINCENT,OU=TP,DC=testrisr,DC=CESI"
    }
```

```Powershell
$Groups = Get-ADGroup -filter { Members -notlike "*" } -SearchBase "OU=Maxime_VINCENT,OU=TP,DC=testrisr,DC=cesi" | Select-Object Name, GroupCategory, DistinguishedName
ForEach ($Item in $Groups){
    Remove-ADGroup -Identity $Item.DistinguishedName -Confirm:$false
    Write-Output "$($Item.Name) - Deleted"
}
```