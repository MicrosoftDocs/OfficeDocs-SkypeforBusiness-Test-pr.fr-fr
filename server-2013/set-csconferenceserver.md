---
title: Set-CsConferenceServer
TOCTitle: Set-CsConferenceServer
ms:assetid: 90f9f1f1-0029-4f97-a8f4-719523cfad56
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Gg398738(v=OCS.15)
ms:contentKeyID: 49298066
ms.date: 05/20/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsConferenceServer

 

_**Dernière rubrique modifiée :** 2015-03-09_

Modifie les propriétés d’un serveur de conférence A/V (également appelé « serveur de conférence »). Le serveur de conférence dote vos conférences de fonctionnalités audio et vidéo (A/V). Cette applet de commande est une nouveauté de Lync Server 2010.

## Syntaxe

    Set-CsConferenceServer [-Identity <XdsGlobalRelativeIdentity>] [-AppSharingPortCount <UInt16>] [-AppSharingPortStart <UInt16>] [-AppSharingSipPort <UInt16>] [-AudioPortCount <UInt16>] [-AudioPortStart <UInt16>] [-AudioVideoSipPort <UInt16>] [-Confirm [<SwitchParameter>]] [-DataPsomPort <UInt16>] [-EdgeServer <String>] [-Force <SwitchParameter>] [-ImSipPort <UInt16>] [-MeetingPsomPort <UInt16>] [-PhoneSipPort <UInt16>] [-VideoPortCount <UInt16>] [-VideoPortStart <UInt16>] [-WhatIf [<SwitchParameter>]]

## Exemples

## EXEMPLE 1

La commande illustrée dans l’exemple 1 modifie le port SIP de messagerie instantanée du serveur de conférence ConferencingServer:atl-cs-001.litwareinc.com. Dans cet exemple, le port est modifié en 5075.

    Set-CsConferenceServer -Identity "ConferencingServer:atl-cs-001.litwareinc.com" -ImSipPort 5075

## EXEMPLE 2

L’exemple 2 est une variation de la commande illustrée dans l’exemple 1. Dans ce cas toutefois, le port SIP de messagerie instantanée est modifié pour tous les serveurs de conférence de l’organisation. Pour ce faire, la commande utilise d’abord l’applet de commande **Get-CsService** et le paramètre ConferencingServer pour retourner une collection de tous les serveurs de conférence en cours d’utilisation. Cette collection est ensuite redirigée vers l’applet de commande **ForEach-Object** qui exécute **Set-CsConferenceServer** sur chaque serveur de la collection et définit le port ImSipPort sur 5075.

    Get-CsService -ConferencingServer | ForEach-Object {Set-CsConferenceServer -Identity $_.Identity -ImSipPort 5075}

## Description détaillée

Les serveurs de conférence (ou serveurs de conférence A/V) apportent aux conférences des fonctionnalités audio et vidéo. En retour, l’applet de commande **Set-CsConferenceServer** permet de modifier les propriétés de ces serveurs. En particulier, vous pouvez préciser les ports utilisés pour le trafic audio, le trafic vidéo et le partage d’applications, par exemple. L’applet de commande **Set-CsConferenceServer** sert également à associer un serveur donné à un serveur Edge ou un serveur d’archivage.

Personnes autorisées à exécuter cette applet de commande : Par défaut, les membres des groupes qui suivent sont autorisés à exécuter localement l’applet de commande **Set-CsConferenceServer** : RTCUniversalServerAdmins. Pour retourner une liste de tous les rôles RBAC (Contrôle d’accès basé sur un rôle) auxquels cette applet de commande a été affectée (y compris les rôles RBAC personnalisés créés par vos soins), exécutez la commande suivante à l’invite Windows PowerShell :

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsConferenceServer"}

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
<td><p><em>AppSharingPortCount</em></p></td>
<td><p>Facultatif</p></td>
<td><p>System.UInt16</p></td>
<td><p>Nombre total de ports attribués au partage d’applications. Le nombre réel de ports à ouvrir démarre à la valeur configurée pour AppSharingPortStart et continue jusqu’au nombre de ports spécifié pour AppSharingPortCount. Ainsi, si AppSharingPortStart est défini sur 60000 et qu’AppSharingPortCount est défini sur 100, alors les ports 60000 à 60099 seront utilisés pour le partage d’applications.</p></td>
</tr>
<tr class="even">
<td><p><em>AppSharingPortStart</em></p></td>
<td><p>Facultatif</p></td>
<td><p>System.UInt16</p></td>
<td><p>Premier port de la gamme des ports multimédias attribués pour le partage d’applications. Par exemple : –AppSharingPortStart 60000.</p></td>
</tr>
<tr class="odd">
<td><p><em>AppSharingSipPort</em></p></td>
<td><p>Facultatif</p></td>
<td><p>System.UInt16</p></td>
<td><p>Port SIP utilisé pour écouter les demandes de partage d’applications. Les ports utilisés pour le partage d’applications sont configurés à l’aide des paramètres AppSharingPortStart et AppSharingPortCount.</p></td>
</tr>
<tr class="even">
<td><p><em>AudioPortCount</em></p></td>
<td><p>Facultatif</p></td>
<td><p>System.UInt16</p></td>
<td><p>Nombre total de ports attribués pour l’envoi et la réception de trafic audio. Le nombre réel de ports à ouvrir démarre à la valeur configurée pour AudioPortStart et continue jusqu’au nombre de ports spécifié pour AudioPortCount. Ainsi, si AudioPortStart est défini sur 60000 et qu’AudioPortCount est défini sur 100, alors les ports 60000 à 60099 seront utilisés pour le trafic audio.</p></td>
</tr>
<tr class="odd">
<td><p><em>AudioPortStart</em></p></td>
<td><p>Facultatif</p></td>
<td><p>System.UInt16</p></td>
<td><p>Premier port de la gamme des ports multimédias affectés à l’envoi et à la réception de trafic audio. Par exemple : –AudioPortStart 60000.</p></td>
</tr>
<tr class="even">
<td><p><em>AudioVideoSipPort</em></p></td>
<td><p>Facultatif</p></td>
<td><p>System.UInt16</p></td>
<td><p>Port SIP utilisé pour écouter les demandes entrantes de service audio et vidéo. Les ports utilisés pour le trafic audio et vidéo sont configurés à l’aide des paramètres AudioPortCount, AudioPortStart, VideoPortCount et VideoPortStart.</p></td>
</tr>
<tr class="odd">
<td><p><em>Confirm</em></p></td>
<td><p>Facultatif</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Vous demande confirmation avant d’exécuter la commande.</p></td>
</tr>
<tr class="even">
<td><p><em>DataPsomPort</em></p></td>
<td><p>Facultatif</p></td>
<td><p>System.UInt16</p></td>
<td><p>Port de données utilisé par le protocole PSOM (Persistent Shared Object Model).</p></td>
</tr>
<tr class="odd">
<td><p><em>EdgeServer</em></p></td>
<td><p>Facultatif</p></td>
<td><p>System.String</p></td>
<td><p>Emplacement du service du serveur Edge à associer au serveur de conférence. Par exemple : -EdgeServer &quot;EdgeServer:atl-edge-001.litwareinc.com&quot;.</p></td>
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
<td><p>Emplacement de service du serveur de conférence à modifier. Par exemple : -Identity &quot;ConferencingServer:atl-cs-001.litwareinc.com&quot;.</p>
<p>Notez que vous pouvez supprimer le préfixe ConferencingServer: lorsque vous définissez un serveur de conférence. Par exemple : -Identity &quot;atl-cs-001.litwareinc.com&quot;.</p>
<p></p></td>
</tr>
<tr class="even">
<td><p><em>ImSipPort</em></p></td>
<td><p>Facultatif</p></td>
<td><p>System.UInt16</p></td>
<td><p>Port utilisé pour le trafic de messagerie instantanée.</p></td>
</tr>
<tr class="odd">
<td><p><em>MeetingPsomPort</em></p></td>
<td><p>Facultatif</p></td>
<td><p>System.UInt16</p></td>
<td><p>Port utilisé pour le protocole PSOM. Il s’agit du protocole Microsoft utilisé pour les conférences.</p></td>
</tr>
<tr class="even">
<td><p><em>PhoneSipPort</em></p></td>
<td><p>Facultatif</p></td>
<td><p>System.UInt16</p></td>
<td><p>Port utilisé pour le trafic de téléphonie.</p></td>
</tr>
<tr class="odd">
<td><p><em>VideoPortCount</em></p></td>
<td><p>Facultatif</p></td>
<td><p>System.UInt16</p></td>
<td><p>Nombre total de ports attribués pour l’envoi et la réception de trafic vidéo. Le nombre réel de ports à ouvrir démarre à la valeur configurée pour VideoPortStart et continue jusqu’au nombre de ports spécifié pour VideoPortCount. Ainsi, si VideoPortStart est défini sur 60000 et que VideoPortCount est défini sur 100, alors les ports 60000 à 60099 seront utilisés pour le trafic vidéo.</p></td>
</tr>
<tr class="even">
<td><p><em>VideoPortStart</em></p></td>
<td><p>Facultatif</p></td>
<td><p>System.UInt16</p></td>
<td><p>Premier port de la gamme des ports attribués pour l’envoi et la réception de trafic vidéo. Par exemple : –VideoPortStart 60000.</p></td>
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

Aucun. L’applet de commande **Set-CsConferenceServer** n’accepte pas les données redirigées.

## Types de retours

L’applet de commande **Set-CsConferenceServer** ne retourne pas d’objets ni de valeurs. Au lieu de cela, l’applet de commande modifie les instances existantes de l’objet Microsoft.Rtc.Management.Xds.DisplayConferenceServer.

## Voir aussi

#### Autres ressources

[Get-CsConferencingConfiguration](get-csconferencingconfiguration.md)  
[Get-CsService](get-csservice.md)

