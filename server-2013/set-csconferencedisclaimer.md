---
title: Set-CsConferenceDisclaimer
TOCTitle: Set-CsConferenceDisclaimer
ms:assetid: 97afce6d-b031-466d-a170-3ca50d6df245
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Gg398776(v=OCS.15)
ms:contentKeyID: 49298213
ms.date: 05/20/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsConferenceDisclaimer

 

_**Dernière rubrique modifiée :** 2015-03-09_

Modifie les valeurs de propriété de la notification d’exclusion des conférences utilisée dans votre organisation. La notification d’exclusion des conférences est un message qui s’affiche pour les utilisateurs qui se joignent à une conférence en cliquant sur un lien hypertexte (par exemple, en collant le lien à la conférence dans un navigateur tel que Windows Internet Explorer). Cette applet de commande est une nouveauté de Lync Server 2010.

## Syntaxe

    Set-CsConferenceDisclaimer [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Set-CsConferenceDisclaimer [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Body <String>] [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-Header <String>] [-WhatIf [<SwitchParameter>]]

## Exemples

## EXEMPLE 1

La commande illustrée dans l’exemple 1 modifie les propriétés Header et Body de la notification d’exclusion des conférences de votre organisation. La notification d’exclusion étant unique, vous n’avez pas à spécifier d’identité lors de l’exécution de **Set-CsConferenceDisclaimer**.

    Set-CsConferenceDisclaimer -Header "Litwareinc.com Online Conference" -Body "Important note: Conferencing proceedings are recorded and archived."

## Description détaillée

Lors de la configuration des paramètres de conférence, les administrateurs peuvent présenter une clause d’exclusion de responsabilité aux utilisateurs lorsqu’ils se joignent à des conférences hébergées par Lync Server. Cette notification d’exclusion sert généralement à expliquer les droits de propriété intellectuelle et les aspects juridiques liés à la conférence. Les utilisateurs peuvent se joindre à une conférence sans accepter les conditions énoncées dans la clause d’exclusion. Notez cependant que cette clause d’exclusion ne s’affiche que pour les utilisateurs qui se joignent à une conférence en cliquant sur un lien hypertexte.

Lync Server autorise une instance globale unique de notification d’exclusion des conférences. L’applet de commande **Set-CsConferenceDisclaimer** permet de modifier la notification d’exclusion des conférences de votre organisation.

Personnes autorisées à exécuter cette applet de commande : Par défaut, les membres des groupes qui suivent sont autorisés à exécuter localement l’applet de commande **Set-CsConferenceDisclaimer** : RTCUniversalServerAdmins. Pour retourner une liste de tous les rôles RBAC (Contrôle d’accès basé sur un rôle) auxquels cette applet de commande a été affectée (y compris les rôles RBAC personnalisés créés par vos soins), exécutez la commande suivante à l’invite Windows PowerShell :

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsConferenceDisclaimer"}

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
<td><p><em>Body</em></p></td>
<td><p>Facultatif</p></td>
<td><p>System.String</p></td>
<td><p>Contenu de la notification d’exclusion des conférences.</p></td>
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
<td><p><em>Header</em></p></td>
<td><p>Facultatif</p></td>
<td><p>System.String</p></td>
<td><p>Titre donné à la notification d’exclusion des conférences.</p></td>
</tr>
<tr class="odd">
<td><p><em>Identity</em></p></td>
<td><p>Facultatif</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>Identité unique de la notification d’exclusion des conférences. La notification d’exclusion des conférences ne pouvant être que globale et unique, vous n’avez pas à spécifier d’identité lors de l’appel de l’applet de commande <strong>Set-CsConferenceDisclaimer</strong>. Vous pouvez toutefois utiliser la syntaxe suivante en guise de référence à la notification d’exclusion globale : -Identity global.</p></td>
</tr>
<tr class="even">
<td><p><em>Instance</em></p></td>
<td><p>Facultatif</p></td>
<td><p>Objet ConferenceDisclaimer</p></td>
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

Objet Microsoft.Rtc.Management.WritableConfig.Settings.WebConf.ConferenceDisclaimer. L’applet de commande **Set-CsConferenceDisclaimer** accepte les données redirigées pour les objets de notification d’exclusion des conférences.

## Types de retours

L’applet de commande **Set-CsConferenceDisclaimer** ne retourne ni objet ni valeur. Au lieu de cela, l’applet de commande modifie les instances existantes de l’objet Microsoft.Rtc.Management.WritableConfig.Settings.WebConf.ConferenceDisclaimer.

## Voir aussi

#### Autres ressources

[Get-CsConferenceDisclaimer](get-csconferencedisclaimer.md)  
[Remove-CsConferenceDisclaimer](remove-csconferencedisclaimer.md)

