---
title: Set-CsPstnUsage
TOCTitle: Set-CsPstnUsage
ms:assetid: ecba9ed6-4845-4035-933e-0c540d530b72
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Gg399069(v=OCS.15)
ms:contentKeyID: 49299228
ms.date: 05/20/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsPstnUsage

 

_**Dernière rubrique modifiée :** 2015-03-09_

Modifie un ensemble de chaînes qui identifient les utilisations PSTN (réseau téléphonique commuté) autorisées. Cette applet de commande peut être utilisée pour ajouter des utilisations à la liste des utilisations PSTN ou supprimer des utilisations de la liste. Cette applet de commande est une nouveauté de Lync Server 2010.

## Syntaxe

    Set-CsPstnUsage [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Set-CsPstnUsage [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-Usage <PSListModifier>] [-WhatIf [<SwitchParameter>]]

## Exemples

## EXEMPLE 1

Cette commande ajoute la chaîne « International » à la liste actuelle des utilisations PSTN disponibles.

    Set-CsPstnUsage -Identity global -Usage @{add="International"}

## EXEMPLE 2

Cette commande appelle la chaîne « Local » à partir de la liste des utilisations PSTN disponibles.

    Set-CsPstnUsage -Identity global -Usage @{remove="Local"}

## EXEMPLE 3

La commande présentée dans cet exemple effectue exactement la même action que dans l’exemple 2 : elle supprime l’utilisation PSTN « Local ». Cette exemple présente la commande sans spécifier de paramètre Identity. La seule identité disponible pour l’applet de commande **Set-CsPstnUsage** est l’identité Global ; si le paramètre Identity est omis, la valeur par défaut est Global.

    Set-CsPstnUsage -Usage @{remove="Local"}

## EXEMPLE 4

Cette commande remplace tous les éléments de la liste des utilisations dont les valeurs sont International et Restricted. Toutes les utilisations qui existaient précédemment sont supprimées.

    Set-CsPstnUsage -Usage @{replace="International","Restricted"}

## Description détaillée

Les utilisations PSTN sont des valeurs de chaîne utilisées pour l’autorisation d’appel. Une utilisation PSTN lie une stratégie de voix à un itinéraire. L’applet de commande **Set-CsPstnUsage** permet d’ajouter des utilisations téléphoniques à la liste des utilisations ou d’en supprimer de celle-ci. Cette liste est globale ; elle peut donc être utilisée à la fois par les stratégies et les itinéraires dans le déploiement Lync Server.

Personnes autorisées à exécuter cette applet de commande : Par défaut, les membres des groupes qui suivent sont autorisés à exécuter localement l’applet de commande **Set-CsPstnUsage** : RTCUniversalServerAdmins. Pour retourner une liste de tous les rôles RBAC (Contrôle d’accès basé sur un rôle) auxquels cette applet de commande a été affectée (y compris les rôles RBAC personnalisés créés par vos soins), exécutez la commande suivante à l’invite Windows PowerShell :

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsPstnUsage"}

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
<td><p>Supprime les invites de confirmation qui s’affichent avant d’effectuer des modifications.</p></td>
</tr>
<tr class="odd">
<td><p><em>Identity</em></p></td>
<td><p>Facultatif</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>Étendue au niveau de laquelle ces paramètres sont appliqués. L’identité de cette applet de commande est toujours l’identité Global.</p></td>
</tr>
<tr class="even">
<td><p><em>Instance</em></p></td>
<td><p>Facultatif</p></td>
<td><p>PstnUsages</p></td>
<td><p>Référence à un objet d’utilisation PSTN. Cet objet doit être de type PstnUsages et peut être récupéré en appelant l’applet de commande <strong>Get-CsPstnUsage</strong>.</p></td>
</tr>
<tr class="odd">
<td><p><em>Usage</em></p></td>
<td><p>Facultatif</p></td>
<td><p>System.Management.Automation.PSListModifier</p></td>
<td><p>Contient une liste des chaînes d’utilisations autorisées. Ces entrées peuvent être n’importe quelle valeur de chaîne.</p></td>
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

Objet Microsoft.Rtc.Management.WritableConfig.Policy.Voice.PstnUsages. Accepte l’entrée redirigée pour les objets d’utilisation PSTN.

## Types de retours

Cette applet de commande ne retourne ni valeur, ni objet. Au lieu de cela, elle configure les instances de l’objet Microsoft.Rtc.Management.WritableConfig.Policy.Voice.PstnUsages.

## Voir aussi

#### Autres ressources

[Get-CsPstnUsage](get-cspstnusage.md)

