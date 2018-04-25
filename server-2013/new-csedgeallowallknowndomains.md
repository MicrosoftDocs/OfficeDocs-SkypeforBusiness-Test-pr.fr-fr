---
title: New-CsEdgeAllowAllKnownDomains
TOCTitle: New-CsEdgeAllowAllKnownDomains
ms:assetid: f9416909-c328-41b3-9215-7ebd091b0ca0
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/JJ994088(v=OCS.15)
ms:contentKeyID: 53095573
ms.date: 05/20/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsEdgeAllowAllKnownDomains

 

_**Dernière rubrique modifiée :** 2015-03-09_

Permet la fédération Microsoft Lync Online avec tous les domaines à l’exception des domaines inclus dans la liste des domaines bloqués.

Cette applet de commande peut seulement être utilisée avec Skype Entreprise Online.

## Syntaxe

    New-CsEdgeAllowAllKnownDomains [-Verbose]

## Exemples

## Exemple 1

Les deux commandes présentées dans l’exemple 1 configurent les paramètres de fédération pour le client avec l’identité « bf19b7db-6960-41e5-a139-2aa373474354 » pour autoriser tous les domaines connus. À cet effet, la première commande de l’exemple utilise l’applet de commande **New-CsEdgeAllowAllKnownDomains** pour créer une instance de l’objet Microsoft.Rtc.Management.WritableConfig.Settings.Edge.AllowAllKnownDomains. Cette instance est stockée dans une variable appelée « $x ». Dans la seconde commande, l’applet de commande **Set-CsTenantFederationConfiguration** est appelée avec le paramètre AllowedDomains. L’utilisation de la variable $x comme valeur de paramètre configure les paramètres de fédération pour autoriser tous les domaines connus.

    $x = New-CsEdgeAllowAllKnownDomains
    Set-CsTenantFederationConfiguration -Tenant "bf19b7db-6960-41e5-a139-2aa373474354" -AllowedDomains $x

## Exemple 2

L’exemple 2 démontre comment vous pouvez configurer tous vos clients pour autoriser la communication avec tous les domaines qui ne figurent pas explicitement dans la liste des domaines bloqués. À cet effet, la première commande de l’exemple utilise l’applet de commande **New-CsEdgeAllowAllKnownDomains** pour créer une instance d’un objet AllowAllKnownDomains, un objet stocké dans une variable appelée « $x ».

La seconde commande de l’exemple utilise ensuite l’applet de commande **Get-CsTenant** pour renvoyer une collection de tous les clients disponibles. Cette collection est ensuite redirigée vers l’applet de commande **ForEach-Object**. L’applet de commande **ForEach-Object** exécute alors l’applet de commande **Set-CsTenantFederationConfiguration** pour chaque client de la collection, en configurant la propriété AllowedDomains pour autoriser tous les domaines connus.

    $x = New-CsEdgeAllowAllKnownDomains
    Get-CsTenant | ForEach-Object {Set-CsTenantFederationConfiguration -Tenant $_.TenantID -AllowedDomains $x}

## Description détaillée

La fédération est un service qui permet aux utilisateurs d'échanger des messages instantanés et des informations de présence avec les utilisateurs d'autres domaines. Lync Online permet aux administrateurs d'utiliser les paramètres de configuration de la fédération pour déterminer :

  - si les utilisateurs peuvent communiquer avec des personnes appartenant à d'autres domaines et, le cas échéant, les domaines avec lesquels ils peuvent communiquer.

  - si les utilisateurs peuvent communiquer avec des personnes ayant des comptes auprès de fournisseurs publics de messagerie instantanée et de présence tels que Windows Live, AOL et Yahoo.

La fédération est gérée en partie à l'aide des listes de domaines autorisés et bloqués. La liste des domaines autorisés spécifie les domaines avec lesquels les utilisateurs peuvent communiquer, tandis que la liste des domaines bloqués spécifie les domaines avec lesquels les utilisateurs ne peuvent pas communiquer. Par défaut, les utilisateurs peuvent communiquer avec n'importe quel domaine n'apparaissant pas dans la liste des domaines bloqués. Les administrateurs peuvent toutefois modifier ce paramètre par défaut et limiter la communication aux domaines figurant dans la liste des domaines autorisés.

Lync Online ne permet pas de modifier directement les listes des domaines autorisés et bloqués. Par exemple, vous ne pouvez pas utiliser une commande semblable à la suivante, laquelle transmet une valeur de chaîne représentant un nom de domaine à la liste des domaines autorisés :

    Set-CsTenantFederationConfiguration -Tenant "bf19b7db-6960-41e5-a139-2aa373474354" -AllowedDomains "fabrikam.com"

Au lieu de cela, vous devez utiliser l’applet de commande **New-CsEdgeAllowAllKnownDomains** ou l’applet de commande **New-CsEdgeAllowList** pour créer un objet domaine, puis transmettez cet objet domaine dans l’applet de commande **Set-CsTenantFederationConfiguration**. L’applet de commande **New-CsEdgeAllowAllKnownDomains** est utilisée si vous souhaitez autoriser les utilisateurs à communiquer avec tous les domaines à l’exception de ceux spécifiés expressément dans la liste des domaines bloqués. L’applet de commande N**ew-CsEdgeAllowList** est utilisée si vous souhaitez limiter la communication des utilisateurs à une collection de domaines. Dans ce cas, les utilisateurs ne seront autorisés à communiquer qu’avec les domaines figurant dans la liste des domaines autorisés.

Pour configurer la fédération avec tous les domaines connus, utilisez un ensemble de commandes comme celui-ci :

    $x = New-CsEdgeAllowAllKnownDomains
    Set-CsTenantFederationConfiguration -Tenant "bf19b7db-6960-41e5-a139-2aa373474354" -AllowedDomains $x

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
<td><p>Cette applet de commande fournit uniquement les paramètres Windows PowerShell courants.</p></td>
<td><p>N/A</p></td>
<td><p>N/A</p></td>
<td><p>N/A</p></td>
</tr>
</tbody>
</table>


## Types d’entrées

Aucun. L’applet de commande **New-CsEdgeAllowAllKnownDomains** n’accepte pas l’entrée redirigée.

## Types de retours

L’applet de commande **New-CsEdgeAllowAllKnownDomains** crée des instances de l’objet Microsoft.Rtc.Management.WritableConfig.Settings.Edge.AllowAllKnownDomains.

## Voir aussi

#### Autres ressources

[New-CsEdgeAllowList](new-csedgeallowlist.md)  
[New-CsEdgeDomainPattern](new-csedgedomainpattern.md)  
[Set-CsTenantFederationConfiguration](set-cstenantfederationconfiguration.md)

