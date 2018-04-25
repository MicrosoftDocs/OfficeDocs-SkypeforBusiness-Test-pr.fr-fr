---
title: Get-CsConferenceDirectory
TOCTitle: Get-CsConferenceDirectory
ms:assetid: 2b7927ab-c6b3-42ce-9c27-9825cd47fd77
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Gg425771(v=OCS.15)
ms:contentKeyID: 49296717
ms.date: 05/20/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsConferenceDirectory

 

_**Dernière rubrique modifiée :** 2015-03-09_

Retourne des informations sur les annuaires des conférences configurés pour être utilisés dans votre organisation. Les annuaires des conférences permettent aux utilisateurs de conférence rendez-vous de rechercher plus facilement des informations sur une conférence. Cette applet de commande est une nouveauté de Lync Server 2010.

## Syntaxe

    Get-CsConferenceDirectory [-Identity <XdsGlobalRelativeIdentity>] <COMMON PARAMETERS>

    Get-CsConferenceDirectory [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-LocalStore <SwitchParameter>]

## Exemples

## EXEMPLE 1

La commande illustrée dans l’exemple 1 retourne des informations sur tous les annuaires des conférences configurés pour être utilisés dans votre organisation.

    Get-CsConferenceDirectory

## EXEMPLE 2

L’exemple 2 retourne des informations sur l’annuaire des conférences dont la propriété Identity est 2. Étant donné que les identités doivent être uniques, cette commande ne retournera jamais plus d’un annuaire des conférences.

    Get-CsConferenceDirectory -Identity 2

## EXEMPLE 3

L’exemple 3 retourne tous les annuaires des conférences hébergés sur le service UserServer:atl-cs-001.litwareinc.com. Pour cela, la commande appelle d’abord l’applet de commande **Get-CsConferenceDirectory** sans paramètre afin de retourner une collection de tous les annuaires des conférences de votre organisation. Cette collection est ensuite redirigée vers l’applet de commande **Where-Object** qui sélectionne uniquement les annuaires pour lesquels le ServiceID correspond à la valeur de chaîne à UserServer:atl-cs-001.litwareinc.com.

    Get-CsConferenceDirectory | Where-Object {$_.ServiceID -match "UserServer:atl-cs-001.litwareinc.com"}

## Description détaillée

Lorsque vous créez un URI (Uniform Resource Identifier) de conférence rendez-vous, une adresse SIP unique lui est attribuée. Cependant, les adresses SIP sont difficiles à traduire pour les périphériques non compatibles SIP ; par exemple, un téléphone de réseau téléphonique commuté (PSTN) ne peut pas traduire une adresse SIP. De ce fait, Lync Server utilise les annuaires des conférences pour aider ces périphériques à trouver des conférences rendez-vous et à s’y connecter. Pour cela, il crée un annuaire des conférences SIP qui est associé à chaque URI de conférence rendez-vous et identifié par un entier et non par un URI SIP. Les téléphones PSTN et autres périphériques peuvent alors utiliser ces numéros (à la place des URI SIP) lorsqu’ils se connectent aux conférences ; concrètement, le numéro d’annuaire est inclus dans l’identification de conférence PSTN que les utilisateurs fournissent lorsqu’ils se connectent à une conférence rendez-vous.

L’applet de commande **Get-CsConferenceDirectory** vous permet de retourner des informations sur tous les annuaires des conférences configurés pour être utilisés dans votre organisation.

Personnes autorisées à exécuter cette applet de commande : Par défaut, les membres des groupes qui suivent sont autorisés à exécuter localement l’applet de commande **Get-CsConferenceDirectory** : RTCUniversalUserAdmins, RTCUniversalServerAdmins. Pour retourner une liste de tous les rôles RBAC (Contrôle d’accès basé sur un rôle) auxquels cette applet de commande a été affectée (y compris les rôles RBAC personnalisés créés par vos soins), exécutez la commande suivante à l’invite Windows PowerShell :

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsConferenceDirectory"}

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
<td><p>Vous permet d’utiliser des caractères génériques pour spécifier la propriété Identity de l’annuaire ou des annuaires des conférences à récupérer. Étant donné que les propriétés Identities des annuaires ont des valeurs numériques, ce paramètre peut être de valeur minime. Toutefois, cette syntaxe retournera tous les annuaires des conférences qui ont une propriété commençant par 3 : -Filter &quot;3*&quot;.</p>
<p></p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>Facultatif</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsGlobalRelativeIdentity</p></td>
<td><p>Identificateur numérique (par exemple 7) de l’annuaire des conférences à retourner. Si ce paramètre est omis, l’applet de commande <strong>Get-CsConferenceDirectory</strong> retourne des informations sur tous les annuaires des conférences utilisés dans votre organisation.</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>Facultatif</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Récupère les données de l’annuaire des conférences à partir de la réplique locale du magasin central de gestion, au lieu du magasin central de gestion lui-même.</p></td>
</tr>
</tbody>
</table>


## Types d’entrées

Aucun. L’applet de commande **Get-CsConferenceDirectory** n’accepte pas l’entrée redirigée.

## Types de retours

L’applet de commande **Get-CsConferenceDirectory** retourne des instances de l’objet Microsoft.Rtc.Management.WritableConfig.Settings.PstnConf.ConferenceDirectories.

## Voir aussi

#### Autres ressources

[Move-CsConferenceDirectory](move-csconferencedirectory.md)  
[New-CsConferenceDirectory](new-csconferencedirectory.md)  
[Remove-CsConferenceDirectory](remove-csconferencedirectory.md)

