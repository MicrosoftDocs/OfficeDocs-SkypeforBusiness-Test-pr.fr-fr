---
title: Remove-CsNetworkSubnet
TOCTitle: Remove-CsNetworkSubnet
ms:assetid: 251ddb5c-4837-4810-b46f-d276f9535653
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Gg425726(v=OCS.15)
ms:contentKeyID: 49296561
ms.date: 05/20/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsNetworkSubnet

 

_**Dernière rubrique modifiée :** 2015-03-09_

Supprime un sous-réseau existant. Cette applet de commande est une nouveauté de Lync Server 2010.

## Syntaxe

    Remove-CsNetworkSubnet -Identity <XdsGlobalRelativeIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## Exemples

## EXEMPLE 1

Cet exemple supprime le sous-réseau avec la propriété Identity (ID de sous-réseau) 172.11.15.0.

    Remove-CsNetworkSubnet -Identity 172.11.15.0

## EXEMPLE 2

L’exemple 2 supprime tous les sous-réseaux associés au site Vancouver. Pour cela, nous commençons par appeler l’applet de commande **Get-CsNetworkSubnet**. Cela permet ainsi de récupérer une collection de tous les sous-réseaux définis au sein du déploiement Lync Server. Cette collection de sous-réseaux est ensuite redirigée vers l’applet de commande **Where-Object**. L’applet de commande **Where-Object** restreint cette collection aux seuls sous-réseaux dont un NetworkSiteID est égal à (-eq) Vancouver. À présent que la collection ne contient plus que les sous-réseaux associés au site Vancouver, nous la redirigeons vers **Remove-CsNetworkSubnet** qui supprime chaque élément de la collection.

    Get-CsNetworkSubnet | Where-Object {$_.NetworkSiteID -eq "Vancouver"} | Remove-CsNetworkSubnet

## Description détaillée

Chaque sous-réseau doit être associé à un site réseau afin de déterminer l’emplacement géographique de l’hôte appartenant à ce sous-réseau. Utilisez cette applet de commande pour supprimer un sous-réseau.

Personnes autorisées à exécuter cette applet de commande : Par défaut, les membres des groupes qui suivent sont autorisés à exécuter localement l’applet de commande **Remove-CsNetworkSubnet** : RTCUniversalServerAdmins. Pour retourner une liste de tous les rôles RBAC (Contrôle d’accès basé sur un rôle) auxquels cette applet de commande a été affectée (y compris les rôles RBAC personnalisés créés par vos soins), exécutez la commande suivante à l’invite Windows PowerShell :

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsNetworkSubnet"}

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
<td><p>ID de sous-réseau unique du sous-réseau à supprimer. Cette valeur sera une adresse IP (par ex., 174.11.12.0).</p></td>
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

Objet Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.SubnetType. Accepte l’entrée redirigée pour les objets de sous-réseau.

## Types de retours

Cette applet de commande ne retourne aucune valeur. Elle supprime un objet de type Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.SubnetType.

## Voir aussi

#### Autres ressources

[New-CsNetworkSubnet](new-csnetworksubnet.md)  
[Set-CsNetworkSubnet](set-csnetworksubnet.md)  
[Get-CsNetworkSubnet](get-csnetworksubnet.md)

