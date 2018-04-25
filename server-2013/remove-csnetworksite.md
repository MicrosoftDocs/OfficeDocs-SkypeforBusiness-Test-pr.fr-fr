---
title: Remove-CsNetworkSite
TOCTitle: Remove-CsNetworkSite
ms:assetid: 07b543a6-3aa0-4fce-85f9-9ddc75d7b14f
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Gg398135(v=OCS.15)
ms:contentKeyID: 49296159
ms.date: 05/20/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsNetworkSite

 

_**Dernière rubrique modifiée :** 2015-03-09_

Supprime un site réseau qui a été défini pour le contrôle d’admission des appels (CAC) ou pour le système Enhanced 9-1-1 (E9-1-1). Cette applet de commande est une nouveauté de Lync Server 2010.

## Syntaxe

    Remove-CsNetworkSite -Identity <XdsGlobalRelativeIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## Exemples

## EXEMPLE 1

Cet exemple illustre la suppression du site comportant l’identité Vancouver de la configuration CAC ou E9-1-1.

    Remove-CsNetworkSite -Identity Vancouver

## EXEMPLE 2

L’exemple 2 illustre la suppression de tous les sites qui utilisent le profil de stratégie de bande passante appelé LowBWProfile de la configuration CAC ou E9-1-1. Dans cet exemple, l’applet de commande **Get-CsNetworkSite** est d’abord appelée pour extraire tous les sites réseau. Cet ensemble de sites est redirigé vers l’applet de commande **Where-Object**, qui limite l’ensemble aux sites dont l’identité BWPolicyProfileID est égale à (-eq) LowBWProfile. Ce nouvel ensemble est ensuite redirigé vers l’applet de commande **Remove-CsNetworkSite** pour supprimer ces sites.

    Get-CsNetworkSite | Where-Object {$_.BWPolicyProfileID -eq "LowBWProfile"} | Remove-CsNetworkSite

## Description détaillée

Les sites réseau sont les bureaux ou emplacements configurés au sein de chaque région d’un contrôle d’admission des appels (Call Admission Control ou CAC) ou encore d’un déploiement E9-1-1. Cette applet de commande permet de supprimer un site de la configuration CAC ou E9-1-1.

Personnes autorisées à exécuter cette applet de commande : Par défaut, les membres des groupes qui suivent sont autorisés à exécuter localement l’applet de commande **Remove-CsNetworkSite** : RTCUniversalServerAdmins. Pour retourner une liste de tous les rôles RBAC (Contrôle d’accès basé sur un rôle) auxquels cette applet de commande a été affectée (y compris les rôles RBAC personnalisés créés par vos soins), exécutez la commande suivante à l’invite Windows PowerShell :

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsNetworkSite"}

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
<td><p>Identificateur unique du site réseau que vous souhaitez supprimer. Les sites étant uniquement créés dans l’étendue globale, il est inutile de spécifier une étendue. Il suffit d’indiquer l’ID du site.</p></td>
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

Objet Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.DisplayNetworkSiteType. Accepte l’entrée redirigée pour les objets de site réseau.

## Types de retours

Cette applet de commande ne retourne aucune valeur. Elle supprime un objet du type Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.DisplayNetworkSiteType.

## Voir aussi

#### Autres ressources

[New-CsNetworkSite](new-csnetworksite.md)  
[Set-CsNetworkSite](set-csnetworksite.md)  
[Get-CsNetworkSite](get-csnetworksite.md)

