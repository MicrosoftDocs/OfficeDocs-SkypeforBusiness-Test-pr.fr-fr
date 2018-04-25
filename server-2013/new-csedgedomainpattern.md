---
title: New-CsEdgeDomainPattern
TOCTitle: New-CsEdgeDomainPattern
ms:assetid: 653bc148-c22b-4ad4-afdd-17aaeaa299d2
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/JJ994040(v=OCS.15)
ms:contentKeyID: 53095440
ms.date: 05/20/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsEdgeDomainPattern

 

_**Dernière rubrique modifiée :** 2015-03-09_

Permet de spécifier un domaine qui sera ajouté ou supprimé dans l’ensemble de domaines activés pour la fédération. Vous devez utiliser l’applet de commande **New-CsEdgeDomainPattern** lors de la modification des listes de domaines autorisés ou bloqués. Les valeurs de chaîne (comme « fabrikam.com ») ne peuvent pas être transmises directement aux applets de commande utilisées pour gérer l’une ou l’autre de ces listes.

L’applet de commande **New-CsEdgeDomainPattern** peut seulement être utilisée avec Skype Entreprise Online.

## Syntaxe

    New-CsEdgeDomainPattern -Domain <String> [-Verbose]

## Exemples

## Exemple 1

L’exemple 1 démontre comment vous pouvez affecter un domaine unique à la liste des domaines bloqués pour un client spécifié. À cet effet, la première commande de l’exemple crée un objet domaine pour le domaine fabrikam.com. Cette opération est effectuée en appelant l’applet de commande **New-CsEdgeDomainPattern** et en enregistrant l’objet domaine qui en résulte dans une variable appelée « $x ». La seconde commande utilise ensuite l’applet de commande **Set-CsTenantFederationConfiguration** et le paramètre BlockedDomains pour configurer fabrikam.com comme le seul domaine bloqué par le client dont le paramètre TenantId est « bf19b7db-6960-41e5-a139-2aa373474354 ».

    $x = New-CsEdgeDomainPattern -Domain "fabrikam.com"
    Set-CsTenantFederationConfiguration -Tenant "bf19b7db-6960-41e5-a139-2aa373474354" -BlockedDomains $x

## Description détaillée

La fédération est un service qui permet aux utilisateurs d’échanger des messages instantanés et des informations de présence avec les utilisateurs d’autres domaines. Skype Entreprise Online permet aux administrateurs d’utiliser les paramètres de configuration de la fédération pour déterminer :

  - si les utilisateurs peuvent communiquer avec des personnes appartenant à d’autres domaines et, le cas échéant, les domaines avec lesquels ils peuvent communiquer.

  - si les utilisateurs peuvent communiquer avec des personnes ayant des comptes auprès de fournisseurs publics de messagerie instantanée et de présence tels que Windows Live, AOL et Yahoo.

La fédération est gérée en partie à l’aide des listes de domaines autorisés et bloqués. La liste des domaines autorisés spécifie les domaines avec lesquels les utilisateurs peuvent communiquer, tandis que la liste des domaines bloqués spécifie les domaines avec lesquels les utilisateurs ne peuvent pas communiquer. Par défaut, les utilisateurs peuvent communiquer avec n’importe quel domaine n’apparaissant pas dans la liste des domaines bloqués. Les administrateurs peuvent toutefois modifier ce paramètre par défaut et limiter la communication aux domaines figurant dans la liste des domaines autorisés.

Skype Entreprise Online ne vous autorise pas à modifier directement la liste des domaines autorisés ou la liste des domaines bloqués. Par exemple, vous ne pouvez pas utiliser une commande similaire à celle-ci, qui transmet une valeur de chaîne représentant un nom de domaine dans la liste des domaines bloqués :

    Set-CsTenantFederationConfiguration -Tenant "bf19b7db-6960-41e5-a139-2aa373474354" -BlockedDomains "fabrikam.com"

Au lieu de cela, vous devez créer un objet domaine en utilisant l’applet de commande **New-CsEdgeDomainPattern**, stockez cet objet domaine dans une variable (dans cet exemple, « $x »), puis transmettez le nom de la variable dans la liste des domaines bloqués :

    $x = New-CsEdgeDomainPattern -Domain "fabrikam.com"
    Set-CsTenantFederationConfiguration -Tenant "bf19b7db-6960-41e5-a139-2aa373474354" -BlockedDomains $x

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
<td><p><em>Domain</em></p></td>
<td><p>Obligatoire</p></td>
<td><p>System.String</p></td>
<td><p>Nom de domaine complet du domaine à ajouter à la liste des domaines autorisés. Par exemple :</p>
<p>-Domain &quot;fabrikam.com&quot;</p>
<p>Notez que vous ne pouvez pas utiliser de caractères génériques lors de la spécification d’un nom de domaine.</p></td>
</tr>
</tbody>
</table>


## Types d’entrées

Aucun. L’applet de commande **New-CsEdgeDomainPattern** n’accepte pas l’entrée redirigée.

## Types de retours

L’applet de commande **New-CsEdgeDomainPattern** crée des instances de l’objet Microsoft.Rtc.Management.WritableConfig.Settings.Edge.DomainPattern.

## Voir aussi

#### Autres ressources

[New-CsEdgeAllowAllKnownDomains](new-csedgeallowallknowndomains.md)  
[New-CsEdgeAllowList](new-csedgeallowlist.md)  
[Set-CsTenantFederationConfiguration](set-cstenantfederationconfiguration.md)

