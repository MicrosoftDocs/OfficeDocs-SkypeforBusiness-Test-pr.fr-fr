---
title: Remove-CsConferenceDisclaimer
TOCTitle: Remove-CsConferenceDisclaimer
ms:assetid: 196252a1-2526-4944-9064-01d1846f3266
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Gg398243(v=OCS.15)
ms:contentKeyID: 49296396
ms.date: 05/20/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsConferenceDisclaimer

 

_**Dernière rubrique modifiée :** 2015-03-09_

Efface le texte de l’en-tête et du corps de la notification d’exclusion des conférences utilisée dans votre organisation. La notification d’exclusion des conférences est un message qui s’affiche pour les utilisateurs qui rejoignent la conférence à l’aide d’un lien hypertexte (par exemple, les utilisateurs qui collent un lien d’accès à la conférence dans un navigateur tel que Windows Internet Explorer). Cette applet de commande est une nouveauté de Lync Server 2010.

## Syntaxe

    Remove-CsConferenceDisclaimer -Identity <XdsIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## Exemples

## EXEMPLE 1

L’exemple 1 rétablit les valeurs de propriété de la notification d’exclusion globale. Cela signifie que l’en-tête et le corps de la notification d’exclusion sont définis sur des valeurs Null, ce qui vous permet d’obtenir une notification d’exclusion vide.

    Remove-CsConferenceDisclaimer -Identity global

## Description détaillée

Lors de la configuration des paramètres de conférence, les administrateurs peuvent présenter une notification d’exclusion légale aux participants lorsqu’ils rejoignent des conférences hébergées par Lync Server. Cette notification est généralement utilisée pour décrire les dispositions juridiques et les lois de propriété intellectuelle relatives à la conférence. Les utilisateurs ne peuvent rejoindre une conférence sans avoir accepté les stipulations énoncées dans la notification d’exclusion. Notez que cette notification d’exclusion s’affiche uniquement pour les utilisateurs qui rejoignent une conférence à l’aide d’un lien hypertexte.

Lync Server autorise une instance globale unique de notification d’exclusion des conférences. L’applet de commande **Remove-CsConferenceDisclaimer** vous permet de réinitialiser la notification d’exclusion des conférences : lorsque vous exécutez cette applet de commande, l’en-tête et le corps de la notification d’exclusion sont définis sur des valeurs null.

Personnes autorisées à exécuter cette applet de commande : Par défaut, les membres des groupes qui suivent sont autorisés à exécuter localement l’applet de commande **Remove-CsConferenceDisclaimer** : RTCUniversalServerAdmins. Pour retourner une liste de tous les rôles RBAC (Contrôle d’accès basé sur un rôle) auxquels cette applet de commande a été affectée (y compris les rôles RBAC personnalisés créés par vos soins), exécutez la commande suivante à l’invite Windows PowerShell :

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsConferenceDisclaimer"}

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
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>Identité unique de la notification d’exclusion de conférences à supprimer. Même si la notification d’exclusion des conférences doit être uniquement globale et unique, vous devez toujours utiliser le paramètre Identity lors de l’appel de l’applet de commande <strong>Remove-CsConferenceDisclaimer</strong>.</p></td>
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
<td><p><em>WhatIf</em></p></td>
<td><p>Facultatif</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Décrit ce qui se passe si vous exécutez la commande sans l’exécuter réellement.</p></td>
</tr>
</tbody>
</table>


## Types d’entrées

Objet Microsoft.Rtc.Management.WritableConfig.Settings.WebConf.ConferenceDisclaimer. L’applet de commande **Remove-CsConferenceDisclaimer** accepte l’entrée redirigée pour les objets de notification d’exclusion des conférences.

## Types de retours

Aucun. Au lieu de cela, l’applet de commande **Remove-CsConferenceDisclaimer** rétablit les valeurs de propriété par défaut des instances existantes de l’objet Microsoft.Rtc.Management.WritableConfig.Settings.WebConf.ConferenceDisclaimer.

## Voir aussi

#### Autres ressources

[Get-CsConferenceDisclaimer](get-csconferencedisclaimer.md)  
[Set-CsConferenceDisclaimer](set-csconferencedisclaimer.md)

