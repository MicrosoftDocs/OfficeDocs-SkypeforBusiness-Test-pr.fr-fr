---
title: Remove-CsCallParkOrbit
TOCTitle: Remove-CsCallParkOrbit
ms:assetid: b8e7c236-f8de-45bd-966b-60c815b37aed
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Gg412901(v=OCS.15)
ms:contentKeyID: 49298657
ms.date: 05/20/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsCallParkOrbit

 

_**Dernière rubrique modifiée :** 2015-03-09_

Supprime une plage de numéros d’appels parqués spécifique. Cette applet de commande est une nouveauté de Lync Server 2010.

## Syntaxe

    Remove-CsCallParkOrbit -Identity <XdsGlobalRelativeIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## Exemples

## EXEMPLE 1

Dans cet exemple, l’applet de commande **Remove-CsCallParkOrbit** est utilisée pour supprimer la plage de numéros d’appels parqués appelée « Redmond CPO 1 ».

    Remove-CsCallParkOrbit -Identity "Redmond CPO 1"

## EXEMPLE 2

La commande appliquée dans cet exemple supprime toutes les plages de numéros d’appels parqués qui ont été définies pour une organisation. Elle appelle d’abord l’applet de commande **Get-CsCallParkOrbit** sans aucun paramètre pour récupérer toutes les plages de numéros d’appels parqués définies. Elle redirige ensuite cette collection de plages de numéros vers l’applet de commande **Remove-CsCallParkOrbit**, qui supprime alors chacun des numéros.

    Get-CsCallParkOrbit | Remove-CsCallParkOrbit

## EXEMPLE 3

Cette commande supprime toutes les plages de numéros d’appels parqués dont l’identité inclut la chaîne « Redmond », notamment « Redmond 501 », « CP Redmond 1 » et « ARedmond ». La commande appelle d’abord l’applet de commande **Get-CsCallParkOrbit** avec le paramètre Filter pour extraire toutes les plages de numéros d’appels parqués dont l’identité contient le texte « Redmond ». Cette collection est redirigée vers l’applet de commande **Remove-CsCallParkOrbit** qui supprime alors tout son contenu.

    Get-CsCallParkOrbit -Filter *Redmond* | Remove-CsCallParkOrbit

## Description détaillée

L’applet de commande **Remove-CsCallParkOrbit** supprime la plage de numéros d’appels parqués dont le nom est transmis au paramètre Identity obligatoire. Chaque numéro d’appel parqué au sein d’une organisation doit disposer d’une plage de numéros unique. La suppression d’un numéro d’appel parqué libère le nombre de numéros disponibles dans ce même numéro d’appel parqué. Les numéros libérés peuvent ensuite être utilisés avec un autre numéro d’appel parqué récemment défini.

Personnes autorisées à exécuter cette applet de commande : Par défaut, les membres des groupes qui suivent sont autorisés à exécuter localement l’applet de commande **Remove-CsCallParkOrbit** : RTCUniversalServerAdmins. Pour retourner une liste de tous les rôles RBAC (Contrôle d’accès basé sur un rôle) auxquels cette applet de commande a été affectée (y compris les rôles RBAC personnalisés créés par vos soins), exécutez la commande suivante à l’invite Windows PowerShell :

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsCallParkOrbit"}

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
<td><p>Nom de la plage de numéros d’appels parqués. Ce nom a été attribué par l’administrateur lors de la définition de la plage de numéros d’appels parqués.</p></td>
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
<td><p>Supprime les invites de confirmation qui s’affichent avant d’effectuer des modifications.</p></td>
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

Objet Microsoft.Rtc.Management.Voice.Helpers.DisplayCallParkOrbit. Accepte l’entrée redirigée pour les objets de numéro d’appel parqué.

## Types de retours

Cette applet de commande ne retourne aucune valeur. Elle supprime un objet de type Microsoft.Rtc.Management.Voice.Helpers.DisplayCallParkOrbit.

## Voir aussi

#### Autres ressources

[New-CsCallParkOrbit](new-cscallparkorbit.md)  
[Set-CsCallParkOrbit](set-cscallparkorbit.md)  
[Get-CsCallParkOrbit](get-cscallparkorbit.md)

