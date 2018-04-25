---
title: New-CsConferenceDirectory
TOCTitle: New-CsConferenceDirectory
ms:assetid: fd5a4369-10cd-4337-94df-51bcaee4fde9
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Gg413080(v=OCS.15)
ms:contentKeyID: 49299458
ms.date: 05/20/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsConferenceDirectory

 

_**Dernière rubrique modifiée :** 2015-03-09_

Crée un annuaire des conférences en vue de l’utiliser dans votre organisation. Les annuaires des conférences permettent aux utilisateurs de conférence rendez-vous de rechercher plus facilement des informations sur une conférence. Cette applet de commande est une nouveauté de Lync Server 2010.

## Syntaxe

    New-CsConferenceDirectory -HomePool <String> -Identity <XdsGlobalRelativeIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## Exemples

## EXEMPLE 1

Crée un nouvel annuaire des conférences avec une propriété Identity 42. Cet annuaire sera hébergé sur le pool atl-cs-001.litwareinc.com.

    New-CsConferenceDirectory -Identity 42 -HomePool "atl-cs-001.litwareinc.com"

## Description détaillée

Lorsque vous créez un URI (Uniform Resource Identifier) de conférence rendez-vous, une adresse SIP unique lui est attribuée. Cependant, les adresses SIP sont difficiles à traduire pour les périphériques non compatibles SIP ; par exemple, un téléphone de réseau téléphonique commuté ne peut pas traduire une adresse SIP. De ce fait, Lync Server utilise les annuaires des conférences pour aider ces périphériques à trouver des conférences rendez-vous et à s’y connecter. Pour cela, il crée un annuaire des conférences SIP qui est associé à chaque URI de conférence rendez-vous et identifié par un entier et non par un URI SIP. Les téléphones PSTN et autres périphériques peuvent ensuite utiliser ces numéros (à la place des URI SIP) lorsqu’ils se connectent aux conférences ; concrètement, le numéro d’annuaire est inclus dans l’identification de conférence PSTN que les utilisateurs fournissent lorsqu’ils se connectent à une conférence rendez-vous.

Vous pouvez créer de nouveaux annuaires des conférences en appelant l’applet de commande **New-CsConferenceDirectory**.

Personnes autorisées à exécuter cette applet de commande : Par défaut, les membres des groupes qui suivent sont autorisés à exécuter localement l’applet de commande **New-CsConferenceDirectory** : RTCUniversalServerAdmins. Pour retourner une liste de tous les rôles RBAC (Contrôle d’accès basé sur un rôle) auxquels cette applet de commande a été affectée (y compris les rôles RBAC personnalisés créés par vos soins), exécutez la commande suivante à l’invite Windows PowerShell :

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsConferenceDirectory"}

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
<td><p><em>HomePool</em></p></td>
<td><p>Obligatoire</p></td>
<td><p>System.String</p></td>
<td><p>Nom de domaine complet (FQDN) du pool de serveurs d’inscriptions sur lequel sera hébergé le nouvel annuaire des conférences. Par exemple : -Identity atl-cs-001.litwareinc.com.</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>Obligatoire</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsGlobalRelativeIdentity</p></td>
<td><p>Identificateur numérique unique du nouvel annuaire des conférences. Les identités peuvent correspondre à un entier quelconque compris entre 0 et 9999 inclus. Cependant, elles doivent être uniques (par exemple, vous ne pouvez pas créer deux annuaires comportant l’identité 575). Il n’est pas nécessaire de respecter un ordre numérique particulier pour créer de nouveaux annuaires. Par exemple, vous pouvez créer un annuaire comportant l’identité 999, puis un annuaire avec l’identité 2, suivi d’un annuaire doté de l’identité 438, etc.</p></td>
</tr>
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
<td><p><em>WhatIf</em></p></td>
<td><p>Facultatif</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Décrit ce qui se passe si vous exécutez la commande sans l’exécuter réellement.</p></td>
</tr>
</tbody>
</table>


## Types d’entrées

Aucun. L’applet de commande **New-CsConferenceDirectory** n’accepte pas l’entrée redirigée.

## Types de retours

Crée de nouvelles instances de l’objet Microsoft.Rtc.Management.WritableConfig.Settings.PstnConf.ConferenceDirectories.

## Voir aussi

#### Autres ressources

[Get-CsConferenceDirectory](get-csconferencedirectory.md)  
[Move-CsConferenceDirectory](move-csconferencedirectory.md)  
[Remove-CsConferenceDirectory](remove-csconferencedirectory.md)

