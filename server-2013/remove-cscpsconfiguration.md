---
title: Remove-CsCpsConfiguration
TOCTitle: Remove-CsCpsConfiguration
ms:assetid: 546343e1-a2e4-4bc0-bf6d-c8ae9bb3e690
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Gg398358(v=OCS.15)
ms:contentKeyID: 49297267
ms.date: 05/20/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsCpsConfiguration

 

_**Dernière rubrique modifiée :** 2015-03-09_

Supprime une configuration de service de parcage d’appel. Le parcage d’appel est un service qui permet à un utilisateur de « parquer » un appel téléphonique entrant. Le parcage d’un appel a pour effet de transférer ce dernier vers un numéro dans une plage spécifiée et de le mettre immédiatement en attente. N’importe qui (pas seulement la personne qui a répondu à l’appel) peut reprendre la conversation depuis le téléphone souhaité, en entrant simplement le numéro correct. Cette applet de commande est une nouveauté de Lync Server 2010.

## Syntaxe

    Remove-CsCpsConfiguration -Identity <XdsIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## Exemples

## EXEMPLE 1

La commande de l’exemple 1 utilise l’applet de commande **Remove-CsCpsConfiguration** pour supprimer la configuration de service de parcage d’appel dont l’identité est site:Redmond1. Puisque les identités sont uniques, cette commande ne supprimera qu’une seule configuration.

    Remove-CsCpsConfiguration -Identity site:Redmond1

## EXEMPLE 2

Dans l’exemple 2, toutes les configurations de service de parcage d’appel qui ont été définies au niveau de l’étendue Site sont supprimées. Pour réaliser cette tâche, la commande utilise d’abord l’applet de commande **Get-CsCpsConfiguration** et le paramètre Filter pour renvoyer toutes les configurations de parcage d’appel qui ont été définies au niveau de l’étendue Site ; le caractère générique site:\* permet de s’assurer que seuls les paramètres dont l’identité commence par la valeur de chaîne site: sont retournés. Cette collection filtrée est alors redirigée vers l’applet de commande **Remove-CsCpsConfiguration** qui procède à la suppression de chaque élément contenu dans la collection. Notez qu’à chaque fois que vous supprimez des paramètres de service de parcage d’appel d’un site, le site commencera automatiquement à utiliser les paramètres de service de parcage d’appel définis au niveau de l’étendue globale.

    Get-CsCpsConfiguration -Filter site:* | Remove-CsCpsConfiguration

## Description détaillée

Cette applet de commande permet de supprimer une configuration de service de parcage d’appel. Une configuration de service de parcage d’appel spécifie l’action effectuée sur un appel une fois que celui-ci a été parqué. Par exemple, si un appel parqué reste sans réponse après un certain temps, il peut être automatiquement transféré à une autre personne, comme un administrateur ou un Response Group. Les appels peuvent être configurés pour émettre une sonnerie après une certaine durée pour s’assurer qu’ils n’ont pas été oubliés. De plus, le service de parcage d’appel peut être configuré pour diffuser une musique d’attente à l’appelant pendant le parcage de l’appel.

Cette applet de commande peut être utilisée pour supprimer toutes les configurations de parcage d’appel, y compris la configuration globale. Toutefois, dans le cas de la configuration globale, la configuration ne sera pas supprimée, mais simplement réinitialisée à ses valeurs par défaut.

Personnes autorisées à exécuter cette applet de commande : Par défaut, les membres des groupes qui suivent sont autorisés à exécuter localement l’applet de commande **Remove-CsCpsConfiguration** : RTCUniversalServerAdmins. Pour retourner une liste de tous les rôles RBAC (Contrôle d’accès basé sur un rôle) auxquels cette applet de commande a été affectée (y compris les rôles RBAC personnalisés créés par vos soins), exécutez la commande suivante à l’invite Windows PowerShell :

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsCpsConfiguration"}

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
<td><p>Identificateur unique de la configuration de service de parcage d’appel que vous souhaitez supprimer. Cet identificateur sera de type Global ou site:&lt;nom_site&gt;, où &lt;nom_site&gt; est le nom du site auquel la configuration s’applique.</p></td>
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

Objet Microsoft.Rtc.Management.WritableConfig.Settings.CallParkServiceSettings.CallParkServiceSettings. Accepte l’entrée redirigée pour les objets de configuration des services de parcage d’appel.

## Types de retours

Supprime un objet de type Microsoft.Rtc.Management.WritableConfig.Settings.CallParkServiceSettings.CallParkServiceSettings.

## Voir aussi

#### Autres ressources

[New-CsCpsConfiguration](new-cscpsconfiguration.md)  
[Set-CsCpsConfiguration](set-cscpsconfiguration.md)  
[Get-CsCpsConfiguration](get-cscpsconfiguration.md)  
[Set-CsCallParkServiceMusicOnHoldFile](set-cscallparkservicemusiconholdfile.md)

