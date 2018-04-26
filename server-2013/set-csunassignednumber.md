---
title: Set-CsUnassignedNumber
TOCTitle: Set-CsUnassignedNumber
ms:assetid: e7f52423-58d1-410a-9071-731bde45d3d4
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Gg399033(v=OCS.15)
ms:contentKeyID: 49299212
ms.date: 05/20/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsUnassignedNumber

 

_**Dernière rubrique modifiée :** 2015-03-09_

Modifie une plage existante de numéros affectés et les règles de routage qui s’appliquent à ces numéros. Cette applet de commande est une nouveauté de Lync Server 2010.

## Syntaxe

    Set-CsUnassignedNumber [-Identity <XdsGlobalRelativeIdentity>] [-Instance <PSObject>] [-NumberRangeEnd <String>] [-NumberRangeStart <String>] <COMMON PARAMETERS>

    Set-CsUnassignedNumber -ExUmAutoAttendantPhoneNumber <String> [-Identity <XdsGlobalRelativeIdentity>] [-Instance <PSObject>] [-NumberRangeEnd <String>] [-NumberRangeStart <String>] <COMMON PARAMETERS>

    Set-CsUnassignedNumber -AnnouncementName <String> -AnnouncementService <String> [-Identity <XdsGlobalRelativeIdentity>] [-Instance <PSObject>] [-NumberRangeEnd <String>] [-NumberRangeStart <String>] <COMMON PARAMETERS>

    Set-CsUnassignedNumber [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-Priority <Int32>] [-WhatIf [<SwitchParameter>]]

## Exemples

## EXEMPLE 1

Cet exemple modifie la plage de numéros non affectés portant le nom UNSet1. Nous devons d’abord affecter au paramètre Identity la valeur UNSet1, soit le nom du numéro non affecté à modifier. Nous utilisons ensuite les paramètres NumberRangeStart (+14255551000) et NumberRangeEnd (+14255551900) pour modifier la plage des numéros non affectés auxquels s’appliquent l’annonce ou le standard automatique spécifié.

    Set-CsUnassignedNumber -Identity UNSet1 -NumberRangeStart "+14255551000" -NumberRangeEnd "+14255551900"

## EXEMPLE 2

Cet exemple modifie l’annonce de tous les paramètres de la plage de numéros non affectés ayant actuellement une annonce dont le nom comporte la chaîne « Welcome ». Nous appelons d’abord l’applet de commande **Get-CsUnassignedNumber** pour récupérer tous les paramètres de numéros non affectés. Nous redirigeons cette collection de paramètres vers l’applet de commande **Where-Object** qui restreint la collection aux paramètres dont la propriété AnnouncementName contient (-match) la chaîne Welcome. Une fois ces paramètres définis, nous les redirigeons vers l’applet de commande **Set-CsUnassignedNumber** où nous modifions l’ID de serveur d’application du service d’annonce (ApplicationServer:redmond.litwareinc.com) avec le paramètre AnnouncementService et le nom de la nouvelle annonce (Help Desk Announcement) avec le paramètre AnnouncementName. Notez que même si la nouvelle annonce porte un nom différent, mais le même ID de service, vous devez toujours spécifier l’ID de service avec le nom.

    Get-CsUnassignedNumber | Where-Object {$_.AnnouncementName -match "Welcome"} | Set-CsUnassignedNumber -AnnouncementService ApplicationServer:redmond.litwareinc.com -AnnouncementName "Help Desk Announcement"

## Description détaillée

Les numéros non affectés sont des numéros de téléphone qui ont été affectés à une organisation, mais pas à des utilisateurs ou des téléphones spécifiques. Vous pouvez configurer Lync Server pour acheminer des appels vers les destinations désirées lors de l’appel d’un numéro non affecté. Cette applet de commande modifie les paramètres qui définissent ce routage.

Pour modifier certains paramètres de cette applet de commande, votre système doit déjà avoir des annonces définies ou un standard automatique de messagerie unifiée Exchange configuré. Pour savoir si vous avez des annonces, appelez l’applet de commande **Get-CsAnnouncement**. Pour créer une annonce, appelez l’applet de commande **New-CsAnnouncement**. Pour vérifier les paramètres du standard automatique de messagerie unifiée Exchange, exécutez l’applet de commande **Get-CsExUmContact**

Personnes autorisées à exécuter cette applet de commande : Par défaut, les membres des groupes qui suivent sont autorisés à exécuter localement l’applet de commande **Set-CsUnassignedNumber** : RTCUniversalServerAdmins. Pour retourner une liste de tous les rôles RBAC (Contrôle d’accès basé sur un rôle) auxquels cette applet de commande a été affectée (y compris les rôles RBAC personnalisés créés par vos soins), exécutez la commande suivante à l’invite Windows PowerShell :

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsUnassignedNumber"}

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
<td><p><em>AnnouncementName</em></p></td>
<td><p>Obligatoire</p></td>
<td><p>String</p></td>
<td><p>Nom de l’annonce qui sera utilisée pour gérer les appels à cette plage de numéros.</p></td>
</tr>
<tr class="even">
<td><p><em>AnnouncementService</em></p></td>
<td><p>Obligatoire</p></td>
<td><p>String</p></td>
<td><p>Nom de domaine complet (FQDN) ou ID de service du serveur d’annonce.</p></td>
</tr>
<tr class="odd">
<td><p><em>ExUmAutoAttendantPhoneNumber</em></p></td>
<td><p>Obligatoire</p></td>
<td><p>String</p></td>
<td><p>Numéro de téléphone du standard automatique de la messagerie unifiée Exchange vers lequel acheminer les appels dans cette plage. Le contact du standard automatique de la messagerie unifiée Exchange doit déjà être configuré afin d’attribuer une valeur à ce paramètre.</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>Facultatif</p></td>
<td><p>SwitchParameter</p></td>
<td><p>Vous demande confirmation avant d’exécuter la commande.</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>Facultatif</p></td>
<td><p>SwitchParameter</p></td>
<td><p>Supprime les invites de confirmation qui s’affichent avant d’effectuer des modifications.</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>Facultatif</p></td>
<td><p>XdsGlobalRelativeIdentity</p></td>
<td><p>Nom unique de la plage de numéros non affectés que vous modifiez.</p></td>
</tr>
<tr class="odd">
<td><p><em>Instance</em></p></td>
<td><p>Facultatif</p></td>
<td><p>DisplayAnnouncementVacantNumberRange</p></td>
<td><p>Une référence à un objet contenant des paramètres de numéros non affectés. Cet objet doit être de type Microsoft.Rtc.Management.Voice.Helpers.DisplayAnnouncementVacantNumberRange et peut être récupéré en appelant l’applet de commande <strong>Get-CsUnassignedNumber</strong>.</p></td>
</tr>
<tr class="even">
<td><p><em>NumberRangeEnd</em></p></td>
<td><p>Facultatif</p></td>
<td><p>String</p></td>
<td><p>Dernier numéro de la plage de numéros non affectés. Il doit être supérieur ou égal à la valeur de NumberRangeStart. Pour définir une plage d’un seul numéro, utilisez le même numéro pour NumberRangeStart et NumberRangeEnd.</p>
<p>Le numéro doit correspondre à l’expression régulière (tel:)?(\+)?[1-9]\d{0,17}(;ext=[1-9]\d{0,9})?. Cela implique que le numéro peut commencer par la chaîne tel: (si vous ne définissez pas cette chaîne, elle est ajoutée automatiquement), un signe plus (+) et un chiffre compris entre 1 et 9. Le numéro de téléphone peut comporter jusqu’à 17 chiffres et il peut être suivi d’un poste au format ;ext=numéro de poste.</p></td>
</tr>
<tr class="odd">
<td><p><em>NumberRangeStart</em></p></td>
<td><p>Facultatif</p></td>
<td><p>String</p></td>
<td><p>Premier numéro de la plage de numéros non affectés. Il doit être inférieur ou égal à la valeur de NumberRangeEnd.</p>
<p>Le numéro doit correspondre à l’expression régulière (tel:)?(\+)?[1-9]\d{0,17}(;ext=[1-9]\d{0,9})?. Cela implique que le numéro peut commencer par la chaîne tel: (si vous ne spécifiez pas cette chaîne, elle sera automatiquement ajoutée pour vous), un signe plus (+) et un chiffre de 1 à 9. Le numéro de téléphone peut comporter jusqu’à 17 chiffres et peut être suivi d’un poste au format ;ext= suivi du numéro de poste.</p></td>
</tr>
<tr class="even">
<td><p><em>Priority</em></p></td>
<td><p>Facultatif</p></td>
<td><p>Int32</p></td>
<td><p>Il est possible que les plages de numéros non affectés se chevauchent Si un numéro se trouve dans plusieurs plages, la plage ayant la priorité la plus haute est utilisée.</p></td>
</tr>
<tr class="odd">
<td><p><em>WhatIf</em></p></td>
<td><p>Facultatif</p></td>
<td><p>SwitchParameter</p></td>
<td><p>Décrit ce qui se passe si vous exécutez la commande sans l’exécuter réellement.</p></td>
</tr>
</tbody>
</table>


## Types d’entrées

Objet Microsoft.Rtc.Management.Voice.Helpers.DisplayAnnouncementVacantNumberRange. Accepte l’entrée redirigée pour les objets de numéro non affecté.

## Types de retours

Cette applet de commande ne retourne aucune valeur. Elle modifie un objet de type Microsoft.Rtc.Management.Voice.Helpers.DisplayAnnouncementVacantNumberRange.

## Voir aussi

#### Autres ressources

[New-CsUnassignedNumber](new-csunassignednumber.md)  
[Remove-CsUnassignedNumber](remove-csunassignednumber.md)  
[Get-CsUnassignedNumber](get-csunassignednumber.md)  
[New-CsAnnouncement](new-csannouncement.md)  
[Get-CsAnnouncement](get-csannouncement.md)  
[Get-CsExUmContact](get-csexumcontact.md)

