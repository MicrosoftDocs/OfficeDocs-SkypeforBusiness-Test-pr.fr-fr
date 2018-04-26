---
title: Enable-CsPublicProvider
TOCTitle: Enable-CsPublicProvider
ms:assetid: 98370dfd-9a53-41a8-a1f3-bb7a516c3c5e
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Gg398780(v=OCS.15)
ms:contentKeyID: 49298210
ms.date: 05/20/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Enable-CsPublicProvider

 

_**Dernière rubrique modifiée :** 2015-03-09_

Active un fournisseur public configuré pour être utilisé dans votre organisation. Un fournisseur public est une organisation mettant à disposition du grand public des services de messagerie instantanée, des services de présence et d’autres types de services annexes. Lync Server est fourni avec trois fournisseurs publics configurés mais non activés : Yahoo\!, AIM (AOL) et Messenger (MSN). Cette applet de commande est une nouveauté de Lync Server 2010.

## Syntaxe

    Enable-CsPublicProvider [-Identity <XdsGlobalRelativeIdentity>] <COMMON PARAMETERS>

    Enable-CsPublicProvider [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## Exemples

## EXEMPLE 1

La commande présentée dans l’exemple 1 active le fournisseur public dont l’identité est Messenger. Cette commande retourne une erreur si Messenger est déjà activé.

    Enable-CsPublicProvider -Identity "Messenger"

## EXEMPLE 2

L’exemple 2 active tous les fournisseurs publics actuellement désactivés. Pour effectuer cette tâche, la commande utilise d’abord l’applet de commande **Get-CsPublicProvider** pour retourner la collection de tous les fournisseurs publics configurés pour être utilisés dans l’organisation. Cette collection est ensuite redirigée vers l’applet de commande **Where-Object** qui ne sélectionne que les fournisseurs pour lesquels la propriété Enabled est égale à False. La collection filtrée est alors redirigée vers l’applet de commande **Enable-CsPublicProvider**, qui active chaque fournisseur de la collection.

    Get-CsPublicProvider | Where-Object {$_.Enabled -eq $False} | Enable-CsPublicProvider

## EXEMPLE 3

L’exemple 3 active tous les fournisseurs publics qui ne le sont pas déjà dont le niveau de vérification est défini sur AlwaysVerifiable. Pour ce faire, la commande utilise d’abord l’applet de commande **Get-CsPublicProvider** pour retourner une collection de tous les fournisseurs publics utilisés dans l’organisation. Cette collection est redirigée vers l’applet de commande **Where-Object** qui choisit les fournisseurs correspondant à deux critères : 1) la propriété VerificationLevel est égale à AlwaysVerifiable et 2) la propriété Enabled est égale à False. (L’opérateur -and indique à l’applet de commande **Where-Object** que les objets doivent correspondre aux deux critères spécifiés afin d’être sélectionnés.) La collection filtrée est alors redirigée vers l’applet de commande **Enable-CsPublicProvider**, qui active chaque fournisseur de la collection.

    Get-CsPublicProvider | Where-Object {$_.VerificationLevel -eq "AlwaysVerifiable" -and $_.Enabled -eq $False} | Enable-CsPublicProvider

## Description détaillée

La fédération est le moyen par lequel deux organisations peuvent configurer une relation d’approbation facilitant la communication entre les deux groupes. Lorsqu’une fédération a été établie, les utilisateurs des deux organisations peuvent échanger des messages instantanés, souscrire à des notifications de présence et communiquer entre eux à l’aide d’applications SIP comme Lync 2013. Lync Server autorise trois types de fédération : 1) fédération directe entre votre organisation et une autre ; 2) fédération entre votre organisation et un fournisseur public et 3) fédération entre votre organisation et un fournisseur d’hébergement tiers.

Un fournisseur public est une organisation qui met à la disposition du grand public des services de communication SIP. Lorsque vous établissez une relation de fédération avec un fournisseur public, vous établissez en fait une fédération avec tout utilisateur disposant d’un compte hébergé par ce fournisseur. Par exemple, si vous établissez une fédération avec Messenger (MSN), vos utilisateurs pourront échanger des messages instantanés et des informations de présence avec toutes les personnes qui disposent d’un compte de messagerie instantanée MSN Messenger.

Afin d’établir une fédération avec un fournisseur public, vous devez préalablement le créer et l’activer. (Ce dernier doit en outre créer une relation de fédération avec vous.) Les fournisseurs publics peuvent être activés au moment de leur création ou plus tard, par le biais de l’applet de commande **Enable-CsPublicProvider**.

Personnes autorisées à exécuter cette applet de commande : Par défaut, les membres des groupes qui suivent sont autorisés à exécuter localement l’applet de commande **Enable-CsPublicProvider** : RTCUniversalServerAdmins. Pour retourner une liste de tous les rôles RBAC (Contrôle d’accès basé sur un rôle) auxquels cette applet de commande a été affectée (y compris les rôles RBAC personnalisés créés par vos soins), exécutez la commande suivante à l’invite Windows PowerShell :

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Enable-CsPublicProvider"}

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
<td><p>Identificateur unique du fournisseur public à activer. L’identité est généralement le nom du site web fournissant les services (par exemple Yahoo!, AOL ou MSN).</p></td>
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

Objet Microsoft.Rtc.Management.WritableConfig.Settings.Edge.DisplayPublicProvider. L’applet de commande **Enable-CsPublicProvider** accepte les instances redirigées de l’objet fournisseur public.

## Types de retours

Aucun. Au lieu de cela, l’applet de commande active les instances de l’objet Microsoft.Rtc.Management.WritableConfig.Settings.Edge.DisplayPublicProvider.

## Voir aussi

#### Autres ressources

[Disable-CsPublicProvider](disable-cspublicprovider.md)  
[Get-CsPublicProvider](get-cspublicprovider.md)  
[New-CsPublicProvider](new-cspublicprovider.md)  
[Remove-CsPublicProvider](remove-cspublicprovider.md)  
[Set-CsPublicProvider](set-cspublicprovider.md)

