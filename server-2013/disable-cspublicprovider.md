---
title: Disable-CsPublicProvider
TOCTitle: Disable-CsPublicProvider
ms:assetid: df1338ea-fe6d-45da-a39c-86108bb54ef5
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Gg398984(v=OCS.15)
ms:contentKeyID: 49299086
ms.date: 05/20/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Disable-CsPublicProvider

 

_**Dernière rubrique modifiée :** 2015-03-09_

Désactive un fournisseur public configuré pour être utilisé dans votre organisation. Un fournisseur public est une organisation mettant à la disposition du grand public des services de messagerie instantanée, des services de présence et des services associés. Lync Server est fourni avec trois fournisseurs publics configurés mais non activés : Yahoo\!, AOL et MSN. Cette applet de commande est une nouveauté de Lync Server 2010.

## Syntaxe

    Disable-CsPublicProvider [-Identity <XdsGlobalRelativeIdentity>] <COMMON PARAMETERS>

    Disable-CsPublicProvider [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## Exemples

## EXEMPLE 1

L’exemple 1 désactive le fournisseur public dont l’identité est MSN. Cette commande retourne une erreur si MSN est déjà désactivé.

    Disable-CsPublicProvider -Identity "Messenger"

## EXEMPLE 2

L’exemple 2 désactive tous les fournisseurs publics qui sont actuellement activés. Pour ce faire, la commande utilise d’abord l’applet de commande **Get-CsPublicProvider** pour récupérer une collection de tous les fournisseurs publics utilisés dans l’organisation. Cette collection est redirigée vers l’applet de commande **Where-Object** qui sélectionne uniquement les fournisseurs dont la propriété Enabled est égale à True. À son tour, cette collection filtrée est redirigée vers l’applet de commande **Disable-CsPublicProvider**, qui désactive chaque fournisseur de la collection.

    Get-CsPublicProvider | Where-Object {$_.Enabled -eq $True} | Disable-CsPublicProvider

## EXEMPLE 3

La commande présentée dans l’exemple 3 désactive tous les fournisseurs publics qui sont actuellement activés et qui ont un niveau de vérification défini sur AlwaysVerifiable. Pour effectuer cette tâche, la commande utilise d’abord l’applet de commande **Get-CsPublicProvider** pour récupérer une collection de tous les fournisseurs publics utilisés dans l’organisation. Cet ensemble est ensuite redirigé vers l’applet de commande **Where-Object**, qui sélectionne les fournisseurs répondant à deux critères : 1) la propriété VerificationLevel est égale à AlwaysVerifiable ; et 2) la propriété Enabled est égale à True. (L’opérateur -and indique à l’applet de commande **Where-Object** que les objets doivent correspondre à tous les critères spécifiés afin d’être sélectionnés.) La collection filtrée est alors redirigée vers l’applet de commande **Disable-CsPublicProvider**, qui désactive chaque fournisseur de cette collection.

    Get-CsPublicProvider | Where-Object {$_.VerificationLevel -ne "AlwaysVerifiable" -and $_.Enabled -eq $True} | Disable-CsPublicProvider

## Description détaillée

La fédération est le moyen par lequel deux organisations peuvent configurer une relation d’approbation pour faciliter la communication entre elles. Lorsqu’une fédération a été établie, les utilisateurs des deux organisations peuvent échanger des messages instantanés, souscrire à des notifications de présence et communiquer entre eux à l’aide d’applications SIP comme Lync 2013. Lync Server autorise trois types de fédération : 1) fédération directe entre votre organisation et une autre, 2) fédération entre votre organisation et un fournisseur public et 3) fédération entre votre organisation et un fournisseur d’hébergement tiers.

Un fournisseur public est une organisation mettant à disposition du grand public des services de communication SIP (Session Initiation Protocol). Lorsque vous établissez une relation de fédération avec un fournisseur public, vous établissez en fait une fédération avec tout utilisateur disposant d’un compte hébergé par ce fournisseur. Par exemple, si vous établissez une fédération avec Messenger (MSN), vos utilisateurs pourront échanger des messages instantanés et des informations de présence avec toutes les personnes qui disposent d’un compte de messagerie instantanée Messenger.

Afin d’établir une fédération avec un fournisseur public, vous devez préalablement le créer et l’activer. (Ce dernier doit en outre créer une relation de fédération avec vous). Lorsque vous créez un fournisseur public, vous avez la possibilité d’activer ou de désactiver cette relation de fédération. Si un fournisseur public est activé, les utilisateurs de votre organisation pourront échanger des messages instantanés et des informations de présence avec des personnes disposant de comptes chez le fournisseur public. Si un fournisseur public est désactivé, votre capacité à communiquer avec les personnes qui ont des comptes chez le fournisseur public sera suspendue et le restera jusqu’à ce que le fournisseur soit réactivé. Si vous souhaitez suspendre temporairement une relation avec un fournisseur, vous pouvez utiliser l’applet de commande **Disable-CsPublicProvider**. Si vous souhaitez entièrement supprimer ce fournisseur, utilisez l’applet de commande **Remove-CsPublicProvider**.

Personnes autorisées à exécuter cette applet de commande : Par défaut, les membres des groupes qui suivent sont autorisés à exécuter localement l’applet de commande **Disable-CsPublicProvider** : RTCUniversalServerAdmins. Pour retourner une liste de tous les rôles RBAC (Contrôle d’accès basé sur un rôle) auxquels cette applet de commande a été affectée (y compris les rôles RBAC personnalisés créés par vos soins), exécutez la commande suivante à l’invite Windows PowerShell :

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Disable-CsPublicProvider"}

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
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Vous demande confirmation avant d’exécuter la commande.</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>Facultatif</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Supprime l’affichage de tous les messages d’erreur récupérable susceptibles d’apparaître lors de l’exécution de la commande.</p></td>
</tr>
<tr class="odd">
<td><p><em>Identity</em></p></td>
<td><p>Facultatif</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsGlobalRelativeIdentity</p></td>
<td><p>Identificateur unique du fournisseur public à désactiver. L’identité correspond généralement au nom du site Web fournissant les services (Yahoo!, AOL, MSN, etc.).</p></td>
</tr>
<tr class="even">
<td><p><em>Instance</em></p></td>
<td><p>Facultatif</p></td>
<td><p>Objet DisplayPublicProvider</p></td>
<td><p>Permet de transmettre une référence à un objet à la cmdlet plutôt que de définir des valeurs de paramètre individuelles.</p></td>
</tr>
<tr class="odd">
<td><p><em>WhatIf</em></p></td>
<td><p>Facultatif</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Décrit ce qui se passe si vous exécutez la commande sans l’exécuter réellement.</p></td>
</tr>
</tbody>
</table>


## Types d’entrées

Objet Microsoft.Rtc.Management.WritableConfig.Settings.Edge.DisplayPublicProvider. L’applet de commande **Disable-CsPublicProvider** accepte les instances redirigées de l’objet de fournisseur public.

## Types de retours

Aucun. Au lieu de cela, l’applet de commande désactive les instances de l’objet Microsoft.Rtc.Management.WritableConfig.Settings.Edge.DisplayPublicProvider.

## Voir aussi

#### Autres ressources

[Enable-CsPublicProvider](enable-cspublicprovider.md)  
[Get-CsPublicProvider](get-cspublicprovider.md)  
[New-CsPublicProvider](new-cspublicprovider.md)  
[Remove-CsPublicProvider](remove-cspublicprovider.md)  
[Set-CsPublicProvider](set-cspublicprovider.md)

