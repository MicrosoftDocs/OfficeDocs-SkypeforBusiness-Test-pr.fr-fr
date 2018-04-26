---
title: Get-CsPublicProvider
TOCTitle: Get-CsPublicProvider
ms:assetid: c122505d-7209-4dcb-a888-5c73f58fa68a
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Gg412945(v=OCS.15)
ms:contentKeyID: 49298722
ms.date: 05/20/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsPublicProvider

 

_**Dernière rubrique modifiée :** 2015-03-09_

Retourne des informations sur les fournisseurs publics configurés pour être utilisés dans votre organisation. Un fournisseur public est une organisation mettant à disposition du grand public des services de messagerie instantanée, des services de présence et d’autres types de services connexes. Lync Server est fourni avec trois fournisseurs publics configurés mais non activés : Yahoo\!, AIM (AOL) et Messenger (MSN). Cette applet de commande est une nouveauté de Lync Server 2010.

## Syntaxe

    Get-CsPublicProvider [-Identity <XdsGlobalRelativeIdentity>] <COMMON PARAMETERS>

    Get-CsPublicProvider [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-LocalStore <SwitchParameter>]

## Exemples

## EXEMPLE 1

La commande présentée dans l’exemple 1 retourne une collection de tous les fournisseurs publics configurés pour être utilisés dans l’organisation. Si vous appelez l’applet de commande **Get-CsPublicProvider** sans paramètres supplémentaires, le système renvoie toujours la collection complète de fournisseurs publics.

    Get-CsPublicProvider

## EXEMPLE 2

Dans l’exemple 2, tous les fournisseurs publics ayant l’identité Messenger sont retournés. Puisque les identités doivent être uniques parmi les fournisseurs publics (et parmi les fournisseurs d’hébergement), cette commande renverra au maximum un seul élément.

    Get-CsPublicProvider -Identity "Messenger"

## EXEMPLE 3

L’exemple 3 renvoie tous les fournisseurs publics dont l’identité commence par la lettre W. Pour ce faire, vous devez inclure le paramètre Filter et la valeur de filtre « W\* ».

    Get-CsPublicProvider -Filter W*

## EXEMPLE 4

La commande présentée dans l’exemple 4 retourne une collection de tous les fournisseurs publics actuellement désactivés. Pour ce faire, la commande appelle d’abord l’applet de commande **Get-CsPublicProvider** pour retourner une collection de tous les fournisseurs publics configurés pour être utilisés dans l’organisation. Cette collection est redirigée vers l’applet de commande **Where-Object** qui sélectionne uniquement les fournisseurs dont la propriété Enabled est égale à False.

    Get-CsPublicProvider | Where-Object {$_.Enabled -eq $False}

## EXEMPLE 5

L’exemple 5 renvoie tous les fournisseurs publics dont la propriété VerificationLevel est définie sur AlwaysUnverifiable ou UseSourceVerification. (Les niveaux de vérification peuvent être définis sur AlwaysUnverifiable, UseSourceVerification ou AlwaysVerifiable.) Pour effectuer cette tâche, la commande appelle d’abord l’applet de commande **Get-CsPublicProvider** pour retourner la collection de tous les fournisseurs publics configurés pour être utilisés dans l’organisation. Cette collection est ensuite redirigée vers l’applet de commande **Where-Object** qui sélectionne uniquement les fournisseurs dont la propriété VerificationLevel n’est pas égale à AlwaysVerifiable. Résultat : seuls les fournisseurs dont la propriété VerificationLevel est définie sur AlwaysUnverifiable ou UseSourceVerification sont sélectionnés.

    Get-CsPublicProvider | Where-Object {$_.VerificationLevel -ne "AlwaysVerifiable"}

## Description détaillée

La fédération est le moyen par lequel deux organisations peuvent configurer une relation d’approbation pour faciliter la communication entre elles. Lorsqu’une fédération a été établie, les utilisateurs des deux organisations peuvent échanger des messages instantanés, souscrire à des notifications de présence et communiquer entre eux à l’aide d’applications SIP comme Lync 2013. Lync Server autorise trois types de fédération : 1) fédération directe entre votre organisation et une autre ; 2) fédération entre votre organisation et un fournisseur public ; et 3) fédération entre votre organisation et un fournisseur d’hébergement tiers.

Un fournisseur public est une organisation qui met à la disposition du grand public des services de communication SIP. Lorsque vous établissez une relation de fédération avec un fournisseur public, vous établissez en fait une fédération avec tout utilisateur disposant d’un compte hébergé par ce fournisseur. Par exemple, si vous établissez une fédération avec Messenger (MSN), vos utilisateurs pourront échanger des messages instantanés et des informations de présence avec toutes les personnes qui disposent d’un compte de messagerie instantanée Messenger.

Afin d’établir une fédération avec un fournisseur public, vous devez préalablement créer et activer ce dernier (le fournisseur public doit également créer une relation de fédération avec vous). L’applet de commande **Get-CsPublicProvider** vous permet de renvoyer des informations sur les fournisseurs publics qui ont été configurés pour être utilisés dans votre organisation.

Personnes autorisées à exécuter cette applet de commande : Par défaut, les membres des groupes qui suivent sont autorisés à exécuter localement l’applet de commande **Get-CsPublicProvider** : RTCUniversalUserAdmins, RTCUniversalServerAdmins. Pour retourner une liste de tous les rôles RBAC (Contrôle d’accès basé sur un rôle) auxquels cette applet de commande a été affectée (y compris les rôles RBAC personnalisés créés par vos soins), exécutez la commande suivante à l’invite Windows PowerShell :

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsPublicProvider"}

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
<td><p><em>Filter</em></p></td>
<td><p>Facultatif</p></td>
<td><p>System.String</p></td>
<td><p>Permet d’utiliser des valeurs de caractère générique afin de renvoyer un ou plusieurs fournisseurs publics. Par exemple, pour retourner une collection de tous les fournisseurs publics dont l’identité commence par la lettre Y, utilisez cette syntaxe : -Filter &quot;Y*&quot;. Pour retourner une collection de tous les fournisseurs publics qui contiennent la valeur de chaîne « Windows » dans leur identité, utilisez cette syntaxe : -Filter &quot;*Windows*&quot;.</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>Facultatif</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsGlobalRelativeIdentity</p></td>
<td><p>Identificateur unique du fournisseur public à renvoyer. Cette identité est généralement le nom du site web fournissant les services (par exemple Yahoo!, AOL, MSN, etc.).</p>
<p>Vous ne pouvez pas utiliser de caractères génériques lors de la spécification de l’identité. Afin d’utiliser des caractères génériques pour renvoyer un ou plusieurs fournisseurs publics, utilisez le paramètre Filter.</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>Facultatif</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Récupère les données du fournisseur public à partir du réplica local du magasin central de gestion, plutôt que du magasin central de gestion lui-même.</p></td>
</tr>
</tbody>
</table>


## Types d’entrées

Aucun. L’applet de commande **Get-CsPublicProvider** n’accepte pas les données redirigées.

## Types de retours

Renvoie des instances de l’objet Microsoft.Rtc.Management.WritableConfig.Settings.Edge.DisplayPublicProvider.

## Voir aussi

#### Autres ressources

[Disable-CsPublicProvider](disable-cspublicprovider.md)  
[Enable-CsPublicProvider](enable-cspublicprovider.md)  
[New-CsPublicProvider](new-cspublicprovider.md)  
[Remove-CsPublicProvider](remove-cspublicprovider.md)  
[Set-CsPublicProvider](set-cspublicprovider.md)

