---
title: Get-CsNetworkRegion
TOCTitle: Get-CsNetworkRegion
ms:assetid: 5c9eef10-16c1-45f7-ae7b-2bee0965b421
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Gg398406(v=OCS.15)
ms:contentKeyID: 49297337
ms.date: 05/20/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsNetworkRegion

 

_**Dernière rubrique modifiée :** 2015-03-09_

Récupère une ou plusieurs régions de réseau. Les régions de réseau sont des concentrateurs de réseau ou les routeurs principaux d’un réseau d’entreprise. Cette applet de commande est une nouveauté de Lync Server 2010.

## Syntaxe

    Get-CsNetworkRegion [-Identity <XdsGlobalRelativeIdentity>] <COMMON PARAMETERS>

    Get-CsNetworkRegion [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-LocalStore <SwitchParameter>]

## Exemples

## EXEMPLE 1

L’exemple 1 récupère toutes les régions de réseau définies pour l’organisation.

    Get-CsNetworkRegion

## EXEMPLE 2

L’exemple 2 récupère les régions de réseau avec l’identité NorthAmerica. Puisque les identités sont uniques, cette commande récupère au plus une région de réseau.

    Get-CsNetworkRegion -Identity NorthAmerica

## EXEMPLE 3

Cet exemple récupère toutes les régions de réseau avec les identités qui se terminent par la chaîne « America ». Cela permet de récupérer les régions avec l’identité NorthAmerica, SouthAmerica et CentralAmerica.

    Get-CsNetworkRegion | Where-Object {$_.CentralSite -eq "site:Redmond"}

## EXEMPLE 4

Cet exemple récupère toutes les régions de réseau associées au site central de Redmond. La commande commence par appeler l’applet de commande **Get-CsNetworkRegion**, sans paramètre, afin de récupérer la collection de toutes les régions de réseau du déploiement de Lync Server. Cette collection est redirigée vers l’applet de commande **Where-Object**. L’applet de commande **Where-Object** filtre cette collection pour ne retourner que les éléments (régions de réseau) où la valeur CentralSite est égale à (-eq) site:Redmond.

    Get-CsNetworkRegion | Where-Object {$_.CentralSite -eq "site:Redmond"}

## Description détaillée

Une région de réseau interconnecte diverses parties d’un réseau sur plusieurs zones géographiques. Chaque région de réseau doit être associée à un site central. Utilisez cette applet de commande pour retrouver des informations relatives à une ou plusieurs régions de réseau et notamment les paramètres du site central associé, qui déterminent si d’autres chemins sont autorisés pour les connexions audio et vidéo et qui associent les sites de la région à une configuration de déviation du trafic multimédia.

Personnes autorisées à exécuter cette applet de commande : Par défaut, les membres des groupes qui suivent sont autorisés à exécuter localement l’applet de commande **Get-CsNetworkRegion** : RTCUniversalUserAdmins, RTCUniversalServerAdmins. Pour retourner une liste de tous les rôles RBAC (Contrôle d’accès basé sur un rôle) auxquels cette applet de commande a été affectée (y compris les rôles RBAC personnalisés créés par vos soins), exécutez la commande suivante à l’invite Windows PowerShell :

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsNetworkRegion"}

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
<td><p><em>Filter</em></p></td>
<td><p>Facultatif</p></td>
<td><p>System.String</p></td>
<td><p>Ce paramètre vous permet d’effectuer une recherche générique sur l’identité de toutes les régions de réseau configurées dans l’organisation. Utilisez le caractère générique pour filtrer n’importe quelle de l’identité.</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>Facultatif</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsGlobalRelativeIdentity</p></td>
<td><p>Identificateur unique de la région de réseau que vous souhaitez récupérer. L’identité prendra la forme d’une chaîne qui identifie de manière unique cette région. (Notez que l’identité est la même que pour NetworkRegionID)</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>Facultatif</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Extrait les informations des régions de réseau à partir du réplica local du magasin central de gestion et non du magasin central de gestion proprement dit.</p></td>
</tr>
</tbody>
</table>


## Types d’entrées

Aucun.

## Types de retours

Retourne un ou plusieurs objets de type Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.NetworkRegionType.

## Voir aussi

#### Autres ressources

[New-CsNetworkRegion](new-csnetworkregion.md)  
[Remove-CsNetworkRegion](remove-csnetworkregion.md)  
[Set-CsNetworkRegion](set-csnetworkregion.md)

