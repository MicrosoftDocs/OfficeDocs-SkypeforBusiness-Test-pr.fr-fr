---
title: Remove-CsPublicProvider
TOCTitle: Remove-CsPublicProvider
ms:assetid: b9eec2f4-cf36-41b7-8023-67790cc8d4cd
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Gg412906(v=OCS.15)
ms:contentKeyID: 49298643
ms.date: 05/20/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsPublicProvider

 

_**Dernière rubrique modifiée :** 2015-03-09_

Supprime un fournisseur public configuré pour être utilisé dans votre organisation. Un fournisseur public est une organisation mettant à disposition du grand public des services de messagerie instantanée, des services de présence et d’autres types de services connexes. Lync Server est fourni avec trois fournisseurs publics configurés mais non activés : Yahoo\!, AIM (AOL) et Messenger (MSN). Cette applet de commande est une nouveauté de Lync Server 2010.

## Syntaxe

    Remove-CsPublicProvider -Identity <XdsGlobalRelativeIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## Exemples

## EXEMPLE 1

L’exemple 1 supprime le fournisseur public dont le paramètre Identity est Messenger. Une fois cette commande exécutée, Messenger n’apparaîtra plus dans la liste des fournisseurs publics configurés. À ce stade, le seul moyen de rétablir la fédération avec Messenger est de recréer le fournisseur.

    Remove-CsPublicProvider -Identity "Messenger"

## EXEMPLE 2

L’exemple 2 supprime tous les fournisseurs publics configurés en vue d’une utilisation dans l’organisation. Pour cela, la commande utilise d’abord l’applet de commande **Get-CsPublicProvider** pour retourner une collection de tous les fournisseurs publics actuellement configurés pour être utilisés. Cette collection est ensuite redirigée vers l’applet de commande **Remove-CsPublicProvider** qui, à son tour, supprime chaque fournisseur de la collection.

    Get-CsPublicProvider | Remove-CsPublicProvider

## EXEMPLE 3

Dans l’exemple 3, tous les fournisseurs publics qui sont actuellement désactivés sont supprimés de l’ensemble des fournisseurs publics configurés. Pour exécuter cette tâche, la commande utilise d’abord l’applet de commande **Get-CsPublicProvider** pour retourner une collection de tous les fournisseurs publics actuellement configurés pour être utilisés. Cette collection est redirigée vers l’applet de commande **Where-Object** qui sélectionne uniquement les fournisseurs dont la propriété Enabled est égale à False. Cette collection filtrée est ensuite redirigée vers l’applet de commande **Remove-CsPublicProvider**, qui supprime tous les éléments de la collection.

    Get-CsPublicProvider | Where-Object {$_.Enabled -eq $False} | Remove-CsPublicProvider

## Description détaillée

La fédération est le moyen par lequel deux organisations peuvent configurer une relation d’approbation destinée à simplifier la communication entre elles. Lorsqu’une fédération a été établie, les utilisateurs des deux organisations peuvent échanger des messages instantanés, souscrire à des notifications de présence et communiquer entre eux à l’aide d’applications SIP comme Lync 2013. Lync Server autorise trois types de fédération : 1) fédération directe entre votre organisation et une autre ; 2) fédération entre votre organisation et un fournisseur public ; et 3) fédération entre votre organisation et un fournisseur d’hébergement tiers.

Un fournisseur public est une organisation qui met à la disposition du grand public des services de communication SIP. Lorsque vous établissez une relation de fédération avec un fournisseur public, vous établissez en fait une fédération avec tout utilisateur disposant d’un compte hébergé par ce fournisseur. Par exemple, si vous établissez une fédération avec Messenger (MSN), vos utilisateurs pourront échanger des messages instantanés et des informations de présence avec toutes les personnes qui disposent d’un compte de messagerie instantanée Messenger.

Afin d’établir une fédération avec un fournisseur public, vous devez préalablement créer et activer ce dernier (le fournisseur public doit également créer une relation de fédération avec vous). Si vous décidez par la suite de mettre un terme à cette relation, utilisez l’applet de commande **Remove-CsPublicProvider** pour supprimer le fournisseur public. Lorsque vous supprimez un fournisseur public, celui-ci est supprimé de la liste des partenaires fédérés ; à cette étape, le seul moyen de rétablir la relation est de récréer le fournisseur. Pour suspendre provisoirement une relation, utilisez plutôt l’applet de commande **Disable-CsPublicProvider**. Lorsqu’un fournisseur public est désactivé, il n’est pas supprimé de la liste des partenaires fédérés, mais simplement marqué comme étant désactivé. Toute communication entre lui et votre organisation est suspendue. Pour rétablir la relation, il vous suffit d’utiliser l’applet de commande **Enable-CsPublicProvider** pour réactiver le fournisseur.

Personnes autorisées à exécuter cette applet de commande : Par défaut, les membres des groupes qui suivent sont autorisés à exécuter localement l’applet de commande **Remove-CsPublicProvider** : RTCUniversalServerAdmins. Pour retourner une liste de tous les rôles RBAC (Contrôle d’accès basé sur un rôle) auxquels cette applet de commande a été affectée (y compris les rôles RBAC personnalisés créés par vos soins), exécutez la commande suivante à l’invite Windows PowerShell :

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsPublicProvider"}

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
<td><p>Identificateur unique du fournisseur public à supprimer. L’identité est généralement le nom du site web fournissant les services (Yahoo!, AOL, MSN, etc.).</p></td>
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
<td><p>Supprime l’affichage de tous les messages d’erreur récupérable susceptibles d’apparaître lors de l’exécution de la commande.</p></td>
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

Objet Microsoft.Rtc.Management.WritableConfig.Settings.Edge.DisplayPublicProvider. L’applet de commande **Remove-CsPublicProvider** accepte les instances redirigées de l’objet fournisseur public.

## Types de retours

Aucun. Au lieu de cela, elle supprime des instances de l’objet Microsoft.Rtc.Management.WritableConfig.Settings.Edge.DisplayPublicProvider.

## Voir aussi

#### Autres ressources

[Disable-CsPublicProvider](disable-cspublicprovider.md)  
[Enable-CsPublicProvider](enable-cspublicprovider.md)  
[Get-CsPublicProvider](get-cspublicprovider.md)  
[New-CsPublicProvider](new-cspublicprovider.md)  
[Set-CsPublicProvider](set-cspublicprovider.md)

