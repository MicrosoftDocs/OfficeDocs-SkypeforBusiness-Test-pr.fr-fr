---
title: New-CsEdgeAllowList
TOCTitle: New-CsEdgeAllowList
ms:assetid: 21a6d546-9e03-485c-b7ec-9deb778f2b01
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/JJ994023(v=OCS.15)
ms:contentKeyID: 53095374
ms.date: 05/20/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsEdgeAllowList

 

_**Dernière rubrique modifiée :** 2015-03-09_

Permet aux administrateurs de spécifier les domaines avec lesquels les utilisateurs pourront communiquer. L’applet de commande **New-CsEdgeAllowList**, qui ne peut être utilisée qu’avec Microsoft Lync Online, doit être utilisée avec les applets de commande **New-CsEdgeDomainPattern** et **Set-CsTenantFederationConfiguration**.

## Syntaxe

    New-CsEdgeAllowList [-AllowedDomain <PSListModifier>] [-Verbose]

## Exemples

## Exemple 1

Les commandes de l’exemple 1 affectent le domaine fabrikam.com à la liste des domaines autorisés pour le client associé au TenantId « bf19b7db-6960-41e5-a139-2aa373474354 ». Pour ce faire, la première commande de l’exemple utilise l’applet de commande **New-CsEdgeDomainPattern** pour créer un objet domaine pour fabrikam.com. Cet objet est stocké dans une variable nommée $x. Une fois l’objet domaine créé, l’applet de commande **New-CsEdgeAllowList** est utilisée pour créer une liste de domaines autorisés contenant uniquement le domaine fabrikam.com.

Une fois la liste des domaines autorisés créée, la commande finale dans l’exemple peut ensuite utiliser l’applet de commande **Set-CsTenantFederationConfiguration** pour configurer fabrikam.com comme seul domaine de la liste des domaines autorisés pour le client spécifié.

    $x = New-CsEdgeDomainPattern -Domain "fabrikam.com"
    $newAllowList = New-CsEdgeAllowList -AllowedDomain $x
    Set-CsTenantFederationConfiguration -Tenant "bf19b7db-6960-41e5-a139-2aa373474354" -AllowedDomains $newAllowList

Notez que le paramètre Tenant est seulement requis dans un déploiement hybride. Si vous êtes seulement connecté à Skype Entreprise Online, le paramètre Tenant peut être omis.

## Exemple 2

L’exemple 2 montre comment ajouter plusieurs domaines à une liste de domaines autorisés, en appelant l’applet de commande **New-CsEdgeDomainPattern** plusieurs fois (une fois pour chaque domaine devant être ajouté à la liste) et en stockant les objets domaine résultants dans des variables distinctes. Chacune de ces variables peut ensuite être ajoutée à la liste des domaines autorisés créée par l’applet de commande **New-CsEdgeAllowList** en utilisant simplement le paramètre AllowedDomain et en séparant le nom des variables avec des virgules :

$newAllowList = New-CsEdgeAllowList -AllowedDomain $x,$y

    $x = New-CsEdgeDomainPattern -Domain "contoso.com"
    $y = New-CsEdgeDomainPattern -Domain "fabrikam.com"
    $newAllowList = New-CsEdgeAllowList -AllowedDomain $x,$y
    Set-CsTenantFederationConfiguration -Tenant "bf19b7db-6960-41e5-a139-2aa373474354" -AllowedDomains $newAllowList

## Exemple 3

Dans l’exemple 3, tous les domaines sont supprimés de la liste des domaines autorisés. Pour ce faire, la première commande de l’exemple utilise l’applet de commande **New-CsEdgeAllowList** pour créer une liste vide de domaines autorisés en définissant la propriété AllowedDomain sur une valeur null ($Null). La référence d’objet résultante ($newAllowList) est ensuite utilisée avec l’applet de commande **Set-CsTenantFederationConfiguration** pour supprimer tous les domaines de la liste des domaines autorisés pour le client associé au TenantId « bf19b7db-6960-41e5-a139-2aa373474354 ».

    $newAllowList = New-CsEdgeAllowList -AllowedDomain $Null
    Set-CsTenantFederationConfiguration -Tenant "bf19b7db-6960-41e5-a139-2aa373474354" -AllowedDomains $newAllowList

## Description détaillée

La fédération est un service qui permet aux utilisateurs d’échanger des messages instantanés et des informations de présence avec les utilisateurs d’autres domaines. Lync Online permet aux administrateurs d’utiliser les paramètres de configuration de la fédération pour déterminer :

  - si les utilisateurs peuvent communiquer avec des personnes appartenant à d’autres domaines et, le cas échéant, les domaines avec lesquels ils peuvent communiquer.

  - si les utilisateurs peuvent communiquer avec des personnes ayant des comptes auprès de fournisseurs publics de messagerie instantanée et de présence tels que Windows Live, AOL et Yahoo.

La fédération est gérée en partie à l’aide des listes de domaines autorisés et bloqués. La liste des domaines autorisés spécifie les domaines avec lesquels les utilisateurs peuvent communiquer, tandis que la liste des domaines bloqués spécifie les domaines avec lesquels les utilisateurs ne peuvent pas communiquer. Par défaut, les utilisateurs peuvent communiquer avec n’importe quel domaine n’apparaissant pas dans la liste des domaines bloqués. Les administrateurs peuvent toutefois modifier ce paramètre par défaut et limiter la communication aux domaines figurant dans la liste des domaines autorisés.

Lync Online ne permet pas de modifier directement les listes des domaines autorisés et bloqués. Par exemple, vous ne pouvez pas utiliser une commande semblable à la suivante, laquelle transmet une valeur de chaîne représentant un nom de domaine à la liste des domaines autorisés :

    Set-CsTenantFederationConfiguration -Tenant "bf19b7db-6960-41e5-a139-2aa373474354" -AllowedDomains "fabrikam.com"

À la place, vous devez utiliser l’applet de commande **New-CsEdgeAllowAllKnownDomains** ou **New-CsEdgeAllowList** pour créer un objet domaine, puis transmettre celui-ci à l’applet de commande **Set-CsTenantFederationConfiguration**. Vous devez utiliser l’applet de commande **New-CsEdgeAllowAllKnownDomains** si vous voulez permettre aux utilisateurs de communiquer avec tous les domaines à l’exception de ceux expressément spécifiés dans la liste des domaines bloqués. Vous devez utiliser l’applet de commande **New-CsEdgeAllowList** si vous voulez limiter les communications des utilisateurs à une collection de domaines spécifiés. Dans ce cas, les utilisateurs ne seront autorisés à communiquer qu’avec les domaines figurant dans la liste des domaines autorisés.

Pour ajouter un domaine (fabrikam.com) à la liste des domaines autorisés, vous devez utiliser un ensemble de commandes semblables à celles-ci :

    $x = New-CsEdgeDomainPattern -Domain "fabrikam.com"
    $newAllowList = New-CsEdgeAllowList -AllowedDomain $x
    Set-CsTenantFederationConfiguration -Tenant "bf19b7db-6960-41e5-a139-2aa373474354" -AllowedDomains $newAllowList

Une fois la commande exécutée, les utilisateurs seront seulement autorisés à communiquer avec les utilisateurs du domaine fabrikam.com.

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
<td><p><em>AllowedDomain</em></p></td>
<td><p>Facultatif</p></td>
<td><p>System.Management.Automation.PSListModifier</p></td>
<td><p>Référence d’objet au nouveau domaine (ou ensemble de domaines) à ajouter à la liste des domaines autorisés. Les références d’objet domaine doivent être créées à l’aide de l’applet de commande <strong>New-CsEdgeDomainPattern</strong>. Plusieurs objets domaine peuvent être ajoutés en séparant les références d’objet avec des virgules, par exemple :</p>
<p>-AllowedDomain $x,$y</p></td>
</tr>
</tbody>
</table>


## Types d’entrées

Aucun. L’applet de commande **New-CsEdgeAllowList** n’accepte pas l’entrée redirigée.

## Types de retours

L’applet de commande **New-CsEdgeAllowList** crée des instances de l’objet Microsoft.Rtc.Management.WritableConfig.Settings.Edge.AllowList.

## Voir aussi

#### Autres ressources

[New-CsEdgeAllowAllKnownDomains](new-csedgeallowallknowndomains.md)  
[New-CsEdgeDomainPattern](new-csedgedomainpattern.md)  
[Set-CsTenantFederationConfiguration](set-cstenantfederationconfiguration.md)

