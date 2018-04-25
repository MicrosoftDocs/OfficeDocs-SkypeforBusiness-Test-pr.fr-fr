---
title: Remove-CsNetworkRegionLink
TOCTitle: Remove-CsNetworkRegionLink
ms:assetid: f26cde90-e789-44a7-a304-695c85e64403
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Gg413012(v=OCS.15)
ms:contentKeyID: 49299330
ms.date: 05/20/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsNetworkRegionLink

 

_**Dernière rubrique modifiée :** 2015-03-09_

Supprime un lien entre deux régions configurées pour le contrôle d’admission des appels (CAC). Cette applet de commande est une nouveauté de Lync Server 2010.

## Syntaxe

    Remove-CsNetworkRegionLink -Identity <XdsGlobalRelativeIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## Exemples

## EXEMPLE 1

Le premier exemple supprime le lien de région de réseau avec le paramètre Identity NA\_EMEA.

    Remove-CsNetworkRegionLink -Identity NA_EMEA

## EXEMPLE 2

L’exemple 2 supprime tous les liens de région de réseau qui utilisent le profil de stratégie de bande passante appelé HighBWLimits. La première applet de commande appelée dans cet exemple est l’applet de commande **Get-CsNetworkRegionLink** (sans aucun paramètre). Elle récupère tous les liens de région. Cette collection de liens est ensuite redirigée vers l’applet de commande **Where-Object**. L’applet de commande **Where-Object** examine un par un chaque membre de la collection et vérifie la valeur de la propriété BWPolicyProfileID. Si cette propriété est égale à (-eq) HighBWLimits, le membre est redirigé vers l’applet de commande **Remove-CsNetworkRegionLink** qui supprime le lien.

    Get-CsNetworkRegionLink | Where-Object {$_.BWPolicyProfileID -eq "HighBWLimits"} | Remove-CsNetworkRegionLink

## Description détaillée

Au sein d’un réseau, les régions sont liées par une connexion physique WAN. Cette applet de commande n’a aucun impact sur les connexions physiques, mais elle supprime le lien dans la configuration du contrôle d’admission des appels.

Personnes autorisées à exécuter cette applet de commande : Par défaut, les membres des groupes qui suivent sont autorisés à exécuter localement l’applet de commande **Remove-CsNetworkRegionLink** : RTCUniversalServerAdmins. Pour retourner une liste de tous les rôles RBAC (Contrôle d’accès basé sur un rôle) auxquels cette applet de commande a été affectée (y compris les rôles RBAC personnalisés créés par vos soins), exécutez la commande suivante à l’invite Windows PowerShell :

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsNetworkRegionLink"}

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
<td><p>Identificateur unique du lien de région réseau que vous souhaitez supprimer. Les liens de région de réseau sont créés uniquement au niveau de l’étendue globale, si bien que cet identificateur n’a pas besoin de spécifier une étendue. Il contient plutôt une chaîne avec un nom unique qui identifie ce lien.</p></td>
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

Objet Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.NetworkRegionLinkType. Accepte l’entrée redirigée pour les objets de région de réseau.

## Types de retours

Cette applet de commande ne retourne aucune valeur. Elle supprime un objet de type Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.NetworkRegionLinkType.

## Voir aussi

#### Autres ressources

[New-CsNetworkRegionLink](new-csnetworkregionlink.md)  
[Set-CsNetworkRegionLink](set-csnetworkregionlink.md)  
[Get-CsNetworkRegionLink](get-csnetworkregionlink.md)

