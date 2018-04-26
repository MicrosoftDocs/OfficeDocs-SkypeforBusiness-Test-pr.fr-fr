---
title: Set-CsNetworkSubnet
TOCTitle: Set-CsNetworkSubnet
ms:assetid: 9e85cdbb-b5fb-48d6-8f95-6e7cba9d9597
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Gg412739(v=OCS.15)
ms:contentKeyID: 49298337
ms.date: 05/20/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsNetworkSubnet

 

_**Dernière rubrique modifiée :** 2015-03-09_

Modifie un sous-réseau existant. Cette applet de commande est une nouveauté de Lync Server 2010.

## Syntaxe

    Set-CsNetworkSubnet [-Identity <XdsGlobalRelativeIdentity>] <COMMON PARAMETERS>

    Set-CsNetworkSubnet [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Confirm [<SwitchParameter>]] [-Description <String>] [-Force <SwitchParameter>] [-MaskBits <Int32>] [-NetworkSiteID <String>] [-WhatIf [<SwitchParameter>]]

## Exemples

## EXEMPLE 1

Cet exemple modifie le sous-réseau, avec la propriété Identity (ID de sous-réseau) 172.11.15.0. Le sous-réseau est modifié, avec une nouvelle valeur pour MaskBits (25) et une nouvelle valeur pour NetworkSiteID (Chicago).

    Set-CsNetworkSubnet -Identity 172.11.15.0 -MaskBits 25 -NetworkSiteID Chicago

## EXEMPLE 2

L’exemple 2 déplace tous les sous-réseaux du site Vancouver vers le site Chicago. Pour cela, nous commençons par appeler l’applet de commande **Get-CsNetworkSubnet**. Cet appel permet de récupérer une collection de tous les sous-réseaux définis au sein du déploiement de Lync Server. Cette collection de sous-réseaux est ensuite redirigée vers l’applet de commande **Where-Object**. L’applet de commande **Where-Object** restreint cette collection aux seuls sous-réseaux dont un NetworkSiteID est égal à (-eq) Vancouver. À présent que la collection ne contient plus que les sous-réseaux associés au site Vancouver, nous la redirigeons vers l’applet de commande **Set-CsNetworkSubnet**. Nous fournissons un paramètre à l’applet de commande **Set-CsNetworkSubnet** : NetworkSiteID. En transmettant au paramètre la valeur Chicago, nous indiquons à l’applet de commande **Set-CsNetworkSubnet** de changer l’ID de site réseau de chaque membre de la collection à Chicago.

    Get-CsNetworkSubnet | Where-Object {$_.NetworkSiteID -eq "Vancouver"} | Set-CsNetworkSubnet -NetworkSiteID Chicago

## Description détaillée

Chaque sous-réseau doit être associé à un site réseau afin de déterminer l’emplacement géographique de l’hôte appartenant à ce sous-réseau. Utilisez cette applet de commande pour modifier le site réseau associé, changer la description du sous-réseau ou modifier les masques de bits du sous-réseau.

Personnes autorisées à exécuter cette applet de commande : Par défaut, les membres des groupes qui suivent sont autorisés à exécuter localement l’applet de commande **Set-CsNetworkSubnet** : RTCUniversalServerAdmins. Pour retourner une liste de tous les rôles RBAC (Contrôle d’accès basé sur un rôle) auxquels cette applet de commande a été affectée (y compris les rôles RBAC personnalisés créés par vos soins), exécutez la commande suivante à l’invite Windows PowerShell :

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsNetworkSubnet"}

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
<td><p><em>Confirm</em></p></td>
<td><p>Facultatif</p></td>
<td><p>SwitchParameter</p></td>
<td><p>Vous demande confirmation avant d’exécuter la commande.</p></td>
</tr>
<tr class="even">
<td><p><em>Description</em></p></td>
<td><p>Facultatif</p></td>
<td><p>Chaîne</p></td>
<td><p>Description du sous-réseau en cours de modification.</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>Facultatif</p></td>
<td><p>SwitchParameter</p></td>
<td><p>Supprime les invites de confirmation qui s’affichent avant d’effectuer des modifications.</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>Facultatif</p></td>
<td><p>XdsGlobalRelativeIdentity</p></td>
<td><p>ID de sous-réseau unique du sous-réseau à modifier. Cette valeur sera soit une adresse IP (comme par exemple 174.11.12.0), soit une URL commençant par http: or https:.</p></td>
</tr>
<tr class="odd">
<td><p><em>Instance</em></p></td>
<td><p>Facultatif</p></td>
<td><p>SubnetType</p></td>
<td><p>Référence à l’objet de sous-réseau à modifier. Cet objet doit être du type Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.SubnetType, qui peut être récupéré par l’applet de commande <strong>Get-CsNetworkSubnet</strong>.</p></td>
</tr>
<tr class="even">
<td><p><em>MaskBits</em></p></td>
<td><p>Facultatif</p></td>
<td><p>Int32</p></td>
<td><p>Masque de bits à appliquer au sous-réseau.</p></td>
</tr>
<tr class="odd">
<td><p><em>NetworkSiteID</em></p></td>
<td><p>Facultatif</p></td>
<td><p>Chaîne</p></td>
<td><p>ID du site réseau auquel ce sous-réseau doit être appliqué. Vous pouvez récupérer des ID de site pour votre déploiement en appelant l’applet de commande <strong>Get-CsNetworkSite</strong>.</p></td>
</tr>
<tr class="even">
<td><p><em>WhatIf</em></p></td>
<td><p>Facultatif</p></td>
<td><p>SwitchParameter</p></td>
<td><p>Décrit ce qui se passe si vous exécutez la commande sans l’exécuter réellement.</p></td>
</tr>
</tbody>
</table>


## Types d’entrées

Objet Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.SubnetType. Accepte l’entrée redirigée pour les objets de sous-réseau.

## Types de retours

Cette applet de commande ne retourne aucune valeur. Elle modifie un objet de type Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.SubnetType.

## Voir aussi

#### Autres ressources

[New-CsNetworkSubnet](new-csnetworksubnet.md)  
[Remove-CsNetworkSubnet](remove-csnetworksubnet.md)  
[Get-CsNetworkSubnet](get-csnetworksubnet.md)

