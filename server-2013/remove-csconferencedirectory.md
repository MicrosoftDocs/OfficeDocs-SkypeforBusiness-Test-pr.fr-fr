---
title: Remove-CsConferenceDirectory
TOCTitle: Remove-CsConferenceDirectory
ms:assetid: c2c62a14-f3f3-472f-bf91-1fcea9e45425
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Gg412961(v=OCS.15)
ms:contentKeyID: 49298771
ms.date: 05/20/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsConferenceDirectory

 

_**Dernière rubrique modifiée :** 2015-03-09_

Supprime un annuaire des conférences existant. Les annuaires des conférences permettent aux utilisateurs de conférence rendez-vous de rechercher plus facilement des informations sur une conférence. Cette applet de commande est une nouveauté de Lync Server 2010.

## Syntaxe

    Remove-CsConferenceDirectory -Identity <XdsGlobalRelativeIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## Exemples

## EXEMPLE 1

La commande présentée dans l’exemple 1 supprime l’annuaire des conférences portant l’identité 2.

    Remove-CsConferenceDirectory -Identity 2

## EXEMPLE 2

L’exemple 2 supprime tous les annuaires des conférences trouvés sur le service UserServer:atl-cs-001.litwareinc.com. Pour ce faire, la commande appelle d’abord l’applet de commande **Get-CsConferenceDirectory** sans aucun paramètre ; elle retourne la collection de tous les annuaires des conférences actuellement utilisés dans l’organisation. Cette collection est alors redirigée vers l’applet de commande **Where-Object**, qui sélectionne seulement les annuaires hébergés sur le service UserServer:atl-cs-001.litwareinc.com. Cette collection filtrée est redirigée vers l’applet de commande **Remove-CsConferenceDirectory** et supprimée par celle-ci.

    Get-CsConferenceDirectory | Where-Object {$_.ServiceID -match "UserServer:atl-cs-001.litwareinc.com"} | Remove-CsConferenceDirectory

## Description détaillée

Lorsque vous créez un URI (Uniform Resource Identifier) de conférence rendez-vous, une adresse SIP unique lui est attribuée. Cependant, les adresses SIP sont difficiles à traduire pour les périphériques non compatibles SIP ; par exemple, un téléphone de réseau téléphonique commuté ne peut pas traduire une adresse SIP. De ce fait, Lync Server utilise les annuaires des conférences pour aider ces périphériques à trouver des conférences rendez-vous et à s’y connecter. Pour cela, il crée un annuaire des conférences SIP qui est associé à chaque URI de conférence rendez-vous et identifié par un entier et non par un URI SIP. Les téléphones PSTN et autres périphériques peuvent alors utiliser ces numéros lorsqu’ils se connectent aux conférences (plutôt qu’un URI de SIP) ; le numéro d’annuaire est inclus dans l’identification de conférence PSTN que les utilisateurs fournissent lorsqu’ils se connectent à une conférence rendez-vous.

Les annuaires des conférences sont créés à l’aide de l’applet de commande **New-CsConferenceDirectory**. À l’occasion, vous aurez peut-être besoin de supprimer un ou plusieurs de ces annuaires ; par exemple, vous devrez peut-être désaffecter le pool qui hébergeait les annuaires. Les annuaires des conférences peuvent être supprimés en appelant l’applet de commande **Remove-CsConferenceDirectory**. Veuillez noter que si vous devez déplacer un annuaire d’un pool vers un autre, il vous suffit d’appeler l’applet de commande **Move-CsConferenceDirectory**.

Personnes autorisées à exécuter cette applet de commande : Par défaut, les membres des groupes qui suivent sont autorisés à exécuter localement l’applet de commande **Remove-CsConferenceDirectory** : RTCUniversalServerAdmins. Pour retourner une liste de tous les rôles RBAC (Contrôle d’accès basé sur un rôle) auxquels cette applet de commande a été affectée (y compris les rôles RBAC personnalisés créés par vos soins), exécutez la commande suivante à l’invite Windows PowerShell :

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsConferenceDirectory"}

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
<td><p>Identité numérique de l’annuaire des conférences à supprimer.</p></td>
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
<td><p>S’il est présent, supprime l’annuaire des conférences même si le pool qui héberge l’annuaire est actuellement indisponible. Par défaut, l’applet de commande <strong>Remove-CsConferenceDirectory</strong> ne supprimera pas les annuaires si le pool correspondant ne peut pas être contacté.</p></td>
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

Objet Microsoft.Rtc.Management.WritableConfig.Settings.PstnConf.ConferenceDirectories. L’applet de commande **Remove-CsConferenceDirectory** accepte l’entrée redirigée pour les objets d’annuaire des conférences.

## Types de retours

Aucun. Au lieu de cela, l’applet de commande **Removes-CsConferenceDirectory** supprime les instances de l’objet Microsoft.Rtc.Management.WritableConfig.Settings.PstnConf.ConferenceDirectories.

## Voir aussi

#### Autres ressources

[Get-CsConferenceDirectory](get-csconferencedirectory.md)  
[Move-CsConferenceDirectory](move-csconferencedirectory.md)  
[New-CsConferenceDirectory](new-csconferencedirectory.md)

