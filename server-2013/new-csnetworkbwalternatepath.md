---
title: New-CsNetworkBWAlternatePath
TOCTitle: New-CsNetworkBWAlternatePath
ms:assetid: 9017378e-4583-42bc-9572-aa8e9571cfe3
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Gg398732(v=OCS.15)
ms:contentKeyID: 49298056
ms.date: 05/20/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsNetworkBWAlternatePath

 

_**Dernière rubrique modifiée :** 2015-03-09_

Crée de nouveaux paramètres permettant de définir si un média peut emprunter d’autres chemins via Internet pour les connexions à bande passante restreinte. Cette applet de commande est une nouveauté de Lync Server 2010.

## Syntaxe

    New-CsNetworkBWAlternatePath -AlternatePath <$true | $false> -BWPolicyModality <Audio | Video>

## Exemples

## EXEMPLE 1

Cet exemple crée un autre chemin de bande passante réseau et affecte les paramètres à une région nouvellement créée. La première ligne de cet exemple appelle l’applet de commande **New-CsNetworkBWAlternatePath** afin de créer un autre chemin. Les autres chemins n’ont que deux propriétés : BWPolicyModality, qui doit être définie sur audio ou vidéo (audio dans cet exemple) et AlternatePath, qui doit être définie sur True ou False (True dans cet exemple). Nous affectons le résultat de cette applet de commande, faisant référence à l’objet de l’autre chemin qui vient d’être créé, à la variable $a.

À la ligne 2 de cet exemple, nous utilisons cet autre chemin nouvellement créé pour la création d’une nouvelle région de réseau. Pour ce faire, nous appelons l’applet de commande **New-CsNetworkRegion**, qui transmet une identité NorthAmerica. Nous affectons une valeur au paramètre CentralSite obligatoire (dans cet exemple, le nom du site central de cette région est Redmond-NA-MLS), puis nous spécifions le paramètre BWAlternatePaths, pour lui transmettre la variable ($a) contenant l’objet de l’autre chemin que nous venons de créer.

    $a = New-CsNetworkBWAlternatePath -BWPolicyModality "audio" -AlternatePath $true
    New-CsNetworkRegion -Identity NorthAmerica -CentralSite Redmond-NA-MLS -BWAlternatePaths $a

## Description détaillée

Il existe deux modalités possibles au sein d’une configuration de contrôle d’admission des appels (Call Admission Control ou CAC) dans Lync Server : audio et vidéo. Des restrictions de bande passante peuvent être définies pour chacune de ces modalités. Quand les restrictions de bande passante empêchent d’effectuer un appel, il est possible de choisir un autre chemin via Internet pour établir l’appel. Cette applet de commande permet de créer les paramètres définissant si un appel peut emprunter un autre chemin via Internet en fonction de la modalité. Les paramètres s’appliquent par région au sein de la configuration de contrôle d’admission des appels.

Cette applet de commande n’enregistre pas immédiatement les paramètres nouvellement créés, mais les créé dans la mémoire. Pour appliquer ces paramètres à une région au sein du réseau, vous devez affecter le résultat de l’applet de commande à une variable, puis utiliser cette variable comme valeur du paramètre BWAlternatePaths de l’applet de commande **New-CsNetworkRegion** ou l’applet de commande **Set-CsNetworkRegion**. Notez que vous pouvez appliquer ces paramètres directement en utilisant les paramètres AudioAlternatePath et VideoAlternatePath des applets de commande **New-CsNetworkRegion** et**Set-CsNetworkRegion** sans devoir appeler l’applet de commande **New-CsNetworkBWAlternatePath** pour créer un nouvel objet.

Personnes autorisées à exécuter cette applet de commande : Par défaut, les membres des groupes qui suivent sont autorisés à exécuter localement l’applet de commande **New-CsNetworkBWAlternatePath** : RTCUniversalServerAdmins. Pour retourner une liste de tous les rôles RBAC (Contrôle d’accès basé sur un rôle) auxquels cette applet de commande a été affectée (y compris les rôles RBAC personnalisés créés par vos soins), exécutez la commande suivante à l’invite Windows PowerShell :

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsNetworkBWAlternatePath"}

## Paramètres


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Paramètre</th>
<th>Obligatoire</th>
<th>Type</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>AlternatePath</em></p></td>
<td><p>Obligatoire</p></td>
<td><p>Booléen</p></td>
<td><p>Définissez le paramètre sur True afin de permettre aux appels passés avec le média de la modalité spécifiée dans le paramètre BWPolicyModality (audio ou vidéo) d’emprunter un autre chemin si le chemin primaire ne dispose pas de la bande passante adéquate.</p></td>
</tr>
<tr class="even">
<td><p><em>BWPolicyModality</em></p></td>
<td><p>Obligatoire</p></td>
<td><p>BWPolicyModality</p></td>
<td><p>Modalité à laquelle s’applique le paramètre de l’autre chemin.</p>
<p>Valeurs valides : audio, vidéo</p>
<p>Type de données complet : Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.BWPolicyModality</p></td>
</tr>
</tbody>
</table>


## Types d’entrées

Aucun.

## Types de retours

Crée un objet de type Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.BWAlternatePathType.

## Voir aussi

#### Autres ressources

[New-CsNetworkRegion](new-csnetworkregion.md)  
[Set-CsNetworkRegion](set-csnetworkregion.md)

