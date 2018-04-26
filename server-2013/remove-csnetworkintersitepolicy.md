---
title: Remove-CsNetworkInterSitePolicy
TOCTitle: Remove-CsNetworkInterSitePolicy
ms:assetid: daf1afc8-cce4-4192-8ba4-05d26817198e
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Gg398963(v=OCS.15)
ms:contentKeyID: 49299058
ms.date: 05/20/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsNetworkInterSitePolicy

 

_**Dernière rubrique modifiée :** 2015-03-09_

Supprime une stratégie intersite de réseau qui définit les restrictions de bande passante entre les sites qui sont directement liés au sein d’une configuration de contrôle d’admission des appels (CAC). Cette applet de commande est une nouveauté de Lync Server 2010.

## Syntaxe

    Remove-CsNetworkInterSitePolicy -Identity <XdsGlobalRelativeIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## Exemples

## EXEMPLE 1

Cet exemple supprime la stratégie de site réseau ayant l’identité Reno\_Portland.

    Remove-CsNetworkInterSitePolicy -Identity Reno_Portland

## EXEMPLE 2

Dans l’exemple 2, nous supprimons toutes les stratégies de site réseau définies dans la configuration CAC. Nous commençons par appeler l’applet de commande **Get-CsNetworkInterSitePolicy** pour récupérer une collection de toutes les stratégies de site réseau. Cette collection est ensuite redirigée vers l’applet de commande **Remove-CsNetworkInterSitePolicy** qui supprime chaque élément de la collection.

    Get-CsNetworkInterSitePolicy | Remove-CsNetworkInterSitePolicy

## Description détaillée

Quand des sites de réseau partagent un lien direct, des restrictions de bande passante pour les connexions audio et vidéo peuvent être définies pour lesdits sites. Cette applet de commande supprime une stratégie de site réseau qui associe une stratégie de limite de bande passante à deux sites directement connectés.

Personnes autorisées à exécuter cette applet de commande : Par défaut, les membres des groupes qui suivent sont autorisés à exécuter localement l’applet de commande **Remove-CsNetworkInterSitePolicy** : RTCUniversalServerAdmins. Pour retourner une liste de tous les rôles RBAC (Contrôle d’accès basé sur un rôle) auxquels cette applet de commande a été affectée (y compris les rôles RBAC personnalisés créés par vos soins), exécutez la commande suivante à l’invite Windows PowerShell :

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsNetworkInterSitePolicy"}

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
<td><p>Identificateur unique de la stratégie de site réseau que vous souhaitez supprimer. Les stratégies de site de réseau étant créées au niveau de l’étendue globale seulement, il n’est pas nécessaire de spécifier une étendue pour cet identificateur. Il contient en effet une chaîne au nom unique permettant d’identifier la stratégie de site.</p></td>
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

Objet Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.InterNetworkSitePolicyType. Accepte l’entrée redirigée pour les objets de stratégie intersite de réseau.

## Types de retours

Cette applet de commande ne retourne aucune valeur. Elle supprime un objet de type Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.InterNetworkSitePolicyType.

## Voir aussi

#### Autres ressources

[New-CsNetworkInterSitePolicy](new-csnetworkintersitepolicy.md)  
[Set-CsNetworkInterSitePolicy](set-csnetworkintersitepolicy.md)  
[Get-CsNetworkInterSitePolicy](get-csnetworkintersitepolicy.md)

