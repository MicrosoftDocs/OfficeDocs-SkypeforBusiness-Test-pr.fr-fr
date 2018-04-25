---
title: Get-CsAudioConferencingProvider
TOCTitle: Get-CsAudioConferencingProvider
ms:assetid: 4632e9d0-aa87-459f-ad7e-27125c11da5b
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/JJ994030(v=OCS.15)
ms:contentKeyID: 53095405
ms.date: 05/20/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsAudioConferencingProvider

 

_**Dernière rubrique modifiée :** 2015-03-09_

Renvoie des informations sur les fournisseurs de conférence audio qu’il est autorisé d’utiliser dans l’organisation. Les fournisseurs de conférence audio sont des sociétés tierces, qui fournissent des services de conférence aux organisations.

L’applet de commande **Get-CsAudioConferencingProvider** peut seulement être utilisée avec Microsoft Lync Online.

## Syntaxe

    Get-CsAudioConferencingProvider [[-Identity] <XdsGlobalRelativeIdentity>] [-LocalStore][<CommonParameters>]Get-CsAudioConferencingProvider [-Filter <string>] [-LocalStore] [<CommonParameters>]

## Exemples

## Exemple 1

La commande présentée dans l’exemple 1 renvoie des informations sur tous les fournisseurs de conférence audio disponibles pour être utilisés dans l’organisation.

    Get-CsAudioConferencingProvider

## Exemple 2

Dans l’exemple 2, des informations sont renvoyées pour un seul fournisseur de conférence audio : le fournisseur avec l’identité Fabrikam Telecom.

    Get-CsAudioConferencingProvider -Identity "Fabrikam Telecom"

## Exemple 3

L’exemple 3 démontre comment il est possible d’utiliser des caractères génériques (et le paramètre Filter) pour renvoyer des informations sur les fournisseurs de conférence audio. Dans cet exemple, la valeur de filtre « \*Fabrikam\* » renvoie tous les fournisseurs de conférence audio possédant la valeur de chaîne « Fabrikam » n’importe où dans leur identité.

    Get-CsAudioConferencingProvider -Filter "*Fabrikam*"

## Description détaillée

Un fournisseur de services d’audioconférence est une société tierce qui propose des services de conférence aux entreprises. Elle offre entre autres un moyen pour les utilisateurs situés hors site et non connectés au réseau de l’entreprise ou à Internet, de participer à la partie audio d’une conférence ou d’une réunion. Souvent, les fournisseurs d’audioconférences proposent des services haut de gamme en direct tels que la traduction, la transcription et une assistance opérateur par conférence.

Une fois que les organisations ont établi une sous-traitance avec un fournisseur de conférence audio, les utilisateurs peuvent être affectés en utilisant l’applet de commande **Set-CsUserAcp**. Les administrateurs peuvent extraire des informations sur les fournisseurs de conférence audio disponibles en utilisant l’applet de commande **Get-CsAudioConferencingProvider**.

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
<td><p>Permet d’utiliser des caractères génériques lors de l’indication du fournisseur (ou des fournisseurs) de conférence audio à renvoyer. Par exemple, cette syntaxe renvoie des informations sur tous les fournisseurs de conférence audio comportant la valeur de chaîne « fabrikam » n’importe où dans leur identité :</p>
<p>-Filter &quot;*fabrikam*&quot;</p>
<p>Notez que vous ne pouvez pas utiliser le paramètre Filter et le paramètre Identity dans la même commande.</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>Facultatif</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsGlobalRelativeIdentity</p></td>
<td><p>Identificateur unique du fournisseur de conférence audio à renvoyer. Par exemple :</p>
<p>-Identity &quot;Fabrikam Telecom&quot;</p>
<p>Si ni le paramètre Identity ni le paramètre Filter ne sont inclus dans une commande, l’applet de commande <strong>Get-CsAudioConferencingProvider</strong> renvoie des informations pour tous les fournisseurs disponibles.</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>Facultatif</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Extrait les données des fournisseurs de conférence audio à partir de la réplique locale du magasin de gestion centralisée plutôt que du magasin de gestion centralisée proprement dit.</p></td>
</tr>
</tbody>
</table>


## Types d’entrées

Aucun. L’applet de commande **Get-CsAudioConferencingProvider** n’accepte pas l’entrée redirigée.

## Types de retours

L’applet de commande **Get-CsAudioConferencingProvider** renvoie des instances de l’objet Microsoft.Rtc.Management.WritableConfig.Settings.AudioConferencingProvider.AudioConferencingProvider\#Decorated.

## Voir aussi

#### Autres ressources

[Get-CsUserAcp](get-csuseracp.md)  
[Remove-CsUserAcp](remove-csuseracp.md)  
[Set-CsUserAcp](set-csuseracp.md)

