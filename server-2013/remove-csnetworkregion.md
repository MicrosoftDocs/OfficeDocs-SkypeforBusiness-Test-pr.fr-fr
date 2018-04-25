---
title: Remove-CsNetworkRegion
TOCTitle: Remove-CsNetworkRegion
ms:assetid: 661dce40-f601-4181-b8f1-3277a76d5df4
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Gg398466(v=OCS.15)
ms:contentKeyID: 49297446
ms.date: 05/20/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsNetworkRegion

 

_**Dernière rubrique modifiée :** 2015-03-09_

Supprime une région réseau existante. Les régions réseau correspondent aux concentrateurs réseau ou aux dorsales principales d’un réseau d’entreprise. Cette applet de commande est une nouveauté de Lync Server 2010.

## Syntaxe

    Remove-CsNetworkRegion -Identity <XdsGlobalRelativeIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## Exemples

## EXEMPLE 1

L’exemple 1 récupère les régions de réseau avec l’identité NorthAmerica. Puisque les identités sont uniques, cette commande supprime uniquement une région de réseau.

    Remove-CsNetworkRegion -Identity NorthAmerica

## EXEMPLE 2

Cet exemple récupère toutes les régions du réseau associées au site central de Redmond. La commande commence par appeler l’applet de commande **Get-CsNetworkRegion**, sans paramètre, afin de récupérer la collection de toutes les régions réseau du déploiement de Lync Server. Cette collection est redirigée vers l’applet de commande **Where-Object**. L’applet de commande **Where-Object** filtre cette collection pour ne retourner que les éléments (régions réseau) où la valeur CentralSite est égale à (-eq) site:Redmond. Une fois que vous avez restreint le choix de cette collection à quelques éléments, cette nouvelle collection est redirigée vers l’applet de commande **Remove-CsNetworkRegion**, qui supprime chaque élément dans la collection.

    Get-CsNetworkRegion | Where-Object {$_.CentralSite -eq "site:Redmond"} | Remove-CsNetworkRegion

## EXEMPLE 3

L’exemple récupère les régions de réseau avec l’identité NorthAmerica. Cependant, une région ne peut pas être supprimée si elle est associée à un site. Ainsi, cet exemple supprime d’abord toute association entre la région NorthAmerica et le site.

La commande commence par appeler l’applet de commande **Get-CsNetworkSite**, sans paramètre, afin de récupérer la collection de tous les sites de réseau pour le déploiement de Lync Server. Cette collection est redirigée vers l’applet de commande **Where-Object**. L’applet de commande **Where-Object** filtre cette collection pour ne retourner que les éléments (sites de réseau) où la valeur NetworkRegionID est égale à (-eq) NorthAmerica. Une fois le choix de cette collection restreint à ces éléments, cette nouvelle collection est redirigée vers l’applet de commande **Set-CsNetworkSite**. Pour chaque site dont l’identité NetworkRegionID contient NorthAmerica, nous définissons la valeur NetworkRegionID sur Null ($null). Cela supprime la référence à la région sur ce site. Cependant, l’ID de bipasse ne peut pas être associée à un site, s’il n’y en a pas. Ainsi, en plus de supprimer la référence à cette région en configurant l’identité NetworkRegionID sur Null, nous devons également supprimer l’association du bipasse en fixant la valeur BypassID à Null.

Une fois la ligne 1 complétée, tout site associé à la région NorthAmerica n’est plus relié à la région ou aux paramètres de contournement. À ce stade, nous appelons la ligne 2, qui supprime la région de réseau.

    Get-CsNetworkSite | Where-Object {$_.NetworkRegionID -eq "NorthAmerica"} | Set-CsNetworkSite -NetworkRegionID $null -BypassID $null
    Remove-CsNetworkRegion -Identity "NorthAmerica"

## Description détaillée

Une région réseau interconnecte diverses parties d’un réseau sur plusieurs zones géographiques. Chaque région réseau doit être associée à un site central. Le site central est le site du centre de données sur lequel est exécuté le service de stratégie de bande passante. Utiliser cette applet de commande pour supprimer une région de réseau.

Il est à noter qu’une région de réseau ne peut pas être supprimée si elle est associée à un site réseau (en d’autres termes, l’identité NetworkRegionID de tout site égal à l’identité de la région). Si vous essayez de supprimer une région associée à un site, vous recevrez un message d’erreur.

Personnes autorisées à exécuter cette applet de commande : Par défaut, les membres des groupes qui suivent sont autorisés à exécuter localement l’applet de commande **Remove-CsNetworkRegion** : RTCUniversalServerAdmins. Pour retourner une liste de tous les rôles RBAC (Contrôle d’accès basé sur un rôle) auxquels cette applet de commande a été affectée (y compris les rôles RBAC personnalisés créés par vos soins), exécutez la commande suivante à l’invite Windows PowerShell :

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsNetworkRegion"}

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
<td><p><em>Identity</em></p></td>
<td><p>Obligatoire</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsGlobalRelativeIdentity</p></td>
<td><p>L’identificateur unique de la région de réseau que vous souhaitez supprimer. L’identité sera sous la forme d’une chaîne qui identifie cette région de manière unique.</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>Facultatif</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Vous demande confirmation avant d’exécuter la commande.</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>Facultatif</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Supprime les invites de confirmation qui s’affichent avant d’effectuer des modifications.</p></td>
</tr>
<tr class="even">
<td><p><em>WhatIf</em></p></td>
<td><p>Facultatif</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Décrit ce qui se passe si vous exécutez la commande sans l’exécuter réellement.</p></td>
</tr>
</tbody>
</table>


## Types d’entrées

Objet Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.NetworkRegionType. Accepte l’entrée redirigée pour les objets de région réseau.

## Types de retours

Cette applet de commande ne retourne aucune valeur. Elle supprime un objet de type Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.NetworkRegionType.

## Voir aussi

#### Autres ressources

[New-CsNetworkRegion](new-csnetworkregion.md)  
[Set-CsNetworkRegion](set-csnetworkregion.md)  
[Get-CsNetworkRegion](get-csnetworkregion.md)

