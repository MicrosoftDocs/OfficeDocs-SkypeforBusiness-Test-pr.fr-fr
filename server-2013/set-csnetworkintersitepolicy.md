---
title: Set-CsNetworkInterSitePolicy
TOCTitle: Set-CsNetworkInterSitePolicy
ms:assetid: 973979bc-db2c-47a6-909e-5949a927f51c
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Gg398772(v=OCS.15)
ms:contentKeyID: 49298169
ms.date: 05/20/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsNetworkInterSitePolicy

 

_**Dernière rubrique modifiée :** 2015-03-09_

Modifie une stratégie intersite de réseau existante qui définit les restrictions de bande passante entre des sites directement liés au sein d’une configuration du service Contrôle d’admission des appels. Cette applet de commande est une nouveauté de Lync Server 2010.

## Syntaxe

    Set-CsNetworkInterSitePolicy [-Identity <XdsGlobalRelativeIdentity>] <COMMON PARAMETERS>

    Set-CsNetworkInterSitePolicy [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-BWPolicyProfileID <String>] [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-NetworkSiteID1 <String>] [-NetworkSiteID2 <String>] [-WhatIf [<SwitchParameter>]]

## Exemples

## EXEMPLE 1

Cet exemple modifie la stratégie de site réseau dont l’identité est Reno\_Portland. Nous utilisons le paramètre BWPolicyProfileID afin de donner au profil de stratégie de bande passante associé à cette stratégie de site réseau la valeur HighBWLimits.

    Set-CsNetworkInterSitePolicy -Identity Reno_Portland -BWPolicyProfileID HighBWLimits

## Description détaillée

Quand des sites de réseau partagent un lien direct, des restrictions de bande passante pour les connexions audio et vidéo peuvent être définies pour lesdits sites. Cette applet de commande modifie une stratégie intersite de réseau associant une restriction de bande passante à deux sites directement connectés.

Personnes autorisées à exécuter cette applet de commande : Par défaut, les membres des groupes qui suivent sont autorisés à exécuter localement l’applet de commande **Set-CsNetworkInterSitePolicy** : RTCUniversalServerAdmins. Pour retourner une liste de tous les rôles RBAC (Contrôle d’accès basé sur un rôle) auxquels cette applet de commande a été affectée (y compris les rôles RBAC personnalisés créés par vos soins), exécutez la commande suivante à l’invite Windows PowerShell :

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsNetworkInterSitePolicy"}

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
<td><p><em>BWPolicyProfileID</em></p></td>
<td><p>Facultatif</p></td>
<td><p>Chaîne</p></td>
<td><p>L’identité du profil de stratégie de bande passante définit les restrictions de cette stratégie de site. Vous pouvez récupérer une liste des profils disponibles en appelant l’applet de commande <strong>Get-CsNetworkBandwidthPolicyProfile</strong>.</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>Facultatif</p></td>
<td><p>.SwitchParameter</p></td>
<td><p>Vous demande confirmation avant d’exécuter la commande.</p></td>
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
<td><p>Identificateur unique de la stratégie de site réseau que vous souhaitez modifier. Les stratégies de site réseau étant créées au niveau de l’étendue globale seulement, il n’est pas nécessaire de spécifier une étendue pour cet identificateur. Il contient en effet une chaîne au nom unique permettant d’identifier la stratégie de site.</p></td>
</tr>
<tr class="odd">
<td><p><em>Instance</em></p></td>
<td><p>Facultatif</p></td>
<td><p>InterNetworkSitePolicyType</p></td>
<td><p>Référence d’objet à une stratégie de site ayant été modifiée dans la mémoire. Cet objet doit être de type Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.InterNetworkSitePolicyType et peut être récupéré en appelant l’applet de commande <strong>Get-CsNetworkInterSitePolicy</strong>.</p></td>
</tr>
<tr class="even">
<td><p><em>NetworkSiteID1</em></p></td>
<td><p>Facultatif</p></td>
<td><p>Chaîne</p></td>
<td><p>Identité (NetworkSiteID) de l’un des deux sites associés à cette stratégie. La combinaison de NetworkSiteID1 et NetworkSiteID2 doit être unique. (Vous ne pouvez pas par exemple, avoir deux stratégies de site définies connectant Reno à Portland).</p></td>
</tr>
<tr class="odd">
<td><p><em>NetworkSiteID2</em></p></td>
<td><p>Facultatif</p></td>
<td><p>Chaîne</p></td>
<td><p>Identité (NetworkSiteID) de l’un des deux sites associés à cette stratégie. La combinaison de NetworkSiteID1 et NetworkSiteID2 doit être unique. (Vous ne pouvez pas par exemple, avoir deux stratégies de site définies connectant Reno à Portland).</p></td>
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

Objet Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.InterNetworkSitePolicyType. Accepte l’entrée redirigée pour les objets de stratégie intersite de réseau.

## Types de retours

Cette applet de commande ne retourne aucune valeur. Elle modifie un objet de type Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.InterNetworkSitePolicyType.

## Voir aussi

#### Autres ressources

[New-CsNetworkInterSitePolicy](new-csnetworkintersitepolicy.md)  
[Remove-CsNetworkInterSitePolicy](remove-csnetworkintersitepolicy.md)  
[Get-CsNetworkInterSitePolicy](get-csnetworkintersitepolicy.md)

