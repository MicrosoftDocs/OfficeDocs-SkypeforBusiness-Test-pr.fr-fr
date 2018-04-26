---
title: Get-CsConferenceDisclaimer
TOCTitle: Get-CsConferenceDisclaimer
ms:assetid: 2382aaef-9c5e-43f8-99de-6c880134db7d
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Gg425714(v=OCS.15)
ms:contentKeyID: 49296537
ms.date: 05/20/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsConferenceDisclaimer

 

_**Dernière rubrique modifiée :** 2015-03-09_

Renvoie des informations sur la notification d’exclusion des conférences utilisée dans votre organisation. La notification d’exclusion des conférences est un message qui s’affiche pour les utilisateurs qui rejoignent la conférence à l’aide d’un lien hypertexte (par exemple, les utilisateurs qui collent un lien d’accès à la conférence dans un navigateur tel que Windows Internet Explorer). Cette applet de commande est une nouveauté de Lync Server 2010.

## Syntaxe

    Get-CsConferenceDisclaimer [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Get-CsConferenceDisclaimer [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-LocalStore <SwitchParameter>]

## Exemples

## EXEMPLE 1

La commande illustrée dans l’exemple 1 renvoie des informations sur la notification d’exclusion de conférences configurée pour être utilisée dans votre organisation. Dans la mesure où vous êtes limité à une seule notification d’exclusion (configurée dans l’étendue globale), il n’est pas nécessaire de spécifier une identité lors de l’exécution de cette commande.

    Get-CSConferenceDisclaimer

## Description détaillée

Lors de la configuration des paramètres de conférence, les administrateurs peuvent présenter une notification d’exclusion légale aux participants lorsqu’ils rejoignent des conférences hébergées par Lync Server. Cette notification d’exclusion sert généralement à expliquer les droits de propriété intellectuelle et les aspects juridiques liés à la conférence. Pour rejoindre la conférence, les utilisateurs doivent accepter les stipulations énoncées dans la notification d’exclusion. Notez que cette notification d’exclusion s’affiche uniquement pour les utilisateurs qui rejoignent une conférence à l’aide d’un lien hypertexte.

L’applet de commande **Get-CsConferenceDisclaimer** vous permet d’afficher le corps et l’en-tête de la notification d’exclusion de votre organisation.

Personnes autorisées à exécuter cette applet de commande : Par défaut, les membres des groupes qui suivent sont autorisés à exécuter localement l’applet de commande **Get-CsConferenceDisclaimer** : RTCUniversalUserAdmins, RTCUniversalServerAdmins. Pour retourner une liste de tous les rôles RBAC (Contrôle d’accès basé sur un rôle) auxquels cette applet de commande a été affectée (y compris les rôles RBAC personnalisés créés par vos soins), exécutez la commande suivante à l’invite Windows PowerShell :

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsConferenceDisclaimer"}

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
<td><p>Vous permet d’utiliser des valeurs à caractère générique pour faire référence à une notification d’exclusion des conférences. La notification d’exclusion des conférences ne pouvant être que globale et unique, il n’y a aucune raison d’utiliser le paramètre Filter. Vous pouvez toutefois utiliser la syntaxe suivante en guise de référence à la notification d’exclusion globale : -Filter « g* ». Cette syntaxe renvoie toutes les notifications d’exclusion des conférences dont l’identité commence par la lettre « g ».</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>Facultatif</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>Identité unique de la notification d’exclusion des conférences. La notification d’exclusion des conférences ne pouvant être que globale et unique, vous n’avez pas besoin de spécifier une identité lors de l’appel de l’applet de commande <strong>Get-CsConferenceDisclaimer</strong>. Vous pouvez toutefois utiliser la syntaxe suivante en guise de référence à la notification d’exclusion globale : -Identity global.</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>Facultatif</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Extrait les données de la notification d’exclusion des conférences du réplica local du magasin central de gestion, au lieu du magasin central de gestion lui-même.</p></td>
</tr>
</tbody>
</table>


## Types d’entrées

Aucun.

## Types de retours

L’applet de commande **Get-CsConferenceDisclaimer** renvoie des instances de l’objet Microsoft.Rtc.Management.WritableConfig.Settings.WebConf.ConferenceDisclaimer.

## Voir aussi

#### Autres ressources

[Remove-CsConferenceDisclaimer](remove-csconferencedisclaimer.md)  
[Set-CsConferenceDisclaimer](set-csconferencedisclaimer.md)

