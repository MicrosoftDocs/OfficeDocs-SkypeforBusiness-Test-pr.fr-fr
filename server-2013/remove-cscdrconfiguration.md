---
title: Remove-CsCdrConfiguration
TOCTitle: Remove-CsCdrConfiguration
ms:assetid: 64352746-a03c-434a-9baf-4d9cd630e9da
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Gg398451(v=OCS.15)
ms:contentKeyID: 49297418
ms.date: 05/20/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsCdrConfiguration

 

_**Dernière rubrique modifiée :** 2015-03-09_

Supprime la collection spécifiée de paramètres d’enregistrement des détails des appels. L’enregistrement des détails des appels permet d’assurer le suivi des sessions de messagerie instantanée d’égal à égal, des appels téléphoniques VoIP (Voice over Internet Protocol) et des téléconférences. Ces données d’utilisation permettent de savoir qui appelle qui, à quelle heure et la durée de l’entretien. Cette applet de commande est une nouveauté de Lync Server 2010.

## Syntaxe

    Remove-CsCdrConfiguration -Identity <XdsIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## Exemples

## EXEMPLE 1

La commande de l’exemple 1 utilise l’applet de commande **Remove-CsCdrConfiguration** pour supprimer les paramètres d’enregistrement des détails des appels affectés au site de Redmond. Utiliser le paramètre Identity garantit que seuls les paramètres affectés à un site spécifié seront supprimés.

    Remove-CsCdrConfiguration -Identity site:Redmond

## EXEMPLE 2

La commande illustrée dans l’exemple 2 supprime tous les paramètres d’enregistrement des détails affectés au niveau de l’étendue Site. Pour ce faire, la commande utilise d’abord l’applet de commande **Get-CsCdrConfiguration** et le paramètre Filter pour récupérer les paramètres d’enregistrement des détails des appels adéquats. La valeur de chaîne « site:\* » garantit que seuls les paramètres ayant une identité qui commence par les caractères « site: » sont retournés. La collection filtrée est ensuite redirigée vers l’applet de commande **Remove-CsCdrConfiguration** qui supprime tous les éléments dans la collection.

    Get-CsCdrConfiguration -Filter site:* | Remove-CsCdrConfiguration

## EXEMPLE 3

Dans l’exemple 3, tout paramètre d’enregistrement des détails des appels pour lequel la propriété KeepCallDetailForDays est inférieure à 30 jours est supprimé. Pour effectuer cette tâche, la commande appelle d’abord l’applet de commande **Get-CsCdrConfiguration** sans paramètre afin de retourner une collection de tous les paramètres d’enregistrement des détails des appels utilisés dans l’organisation. Cette collection est ensuite redirigée vers l’applet de commande **Where-Object** qui ne sélectionne que les paramètres pour lesquels la propriété KeepCallDetailForDays est inférieure à 30 jours. La collection filtrée est alors redirigée vers l’applet de commande **Remove-CsCdrConfiguration** qui supprime chaque élément contenu dans la collection.

    Get-CsCdrConfiguration | Where-Object {$_.KeepCallDetailForDays -lt 30} | Remove-CsCdrConfiguration

## Description détaillée

L’enregistrement des détails des appels permet de suivre l’utilisation des fonctionnalités Lync Server telles que les appels téléphoniques VoIP (Voice over Internet Protocol), les messages instantanés, les transferts de fichiers les conférences audio/vidéo et les sessions de partage d’applications. L’enregistrement des détails des appels (disponible uniquement si vous avez déployé le service Monitoring) conserve les informations d’utilisation : il enregistre diverses informations telles que les parties impliquées dans l’appel, la longueur de l’appel et le transfert éventuel des fichiers. (Cependant, l’enregistrement des détails des appels n’enregistre pas l’appel lui-même.)

CDR garde également en mémoire les informations sur les erreurs relatives aux appels : données de diagnostic détaillées des sessions d’égal à égal et des téléconférences.

En tant qu’administrateur, vous pouvez décider si l’enregistrement des détails des appels est utilisé dans votre organisation. En effet, si vous avez déployé le service de surveillance, vous pouvez aisément activer/désactiver l’enregistrement des détails des appels. De plus, vous avez la possibilité de prendre une décision globalement (auquel cas l’enregistrement des détails des appels pourra soit être activé ou désactivé dans toute l’organisation) ou par site. Par exemple, vous pouvez utiliser l’enregistrement des détails des appels sur le site de Redmond, mais pas sur le site de Paris.

Les paramètres spécifiques au site que vous créez à l’aide de l’applet de commande **New-CsCdrConfiguration** peuvent par la suite être supprimés à l’aide de l’applet de commande **Remove-CsCdrConfiguration**. Quand vous supprimez des paramètres spécifiques au site, l’enregistrement des détails des appels pour le site affecté sera automatiquement régi par les paramètres globaux de configuration de l’enregistrement des détails des appels.

Vous pouvez également exécuter l’applet de commande **Remove-CsCdrConfiguration** sur les paramètres globaux d’enregistrement des détails des appels. Toutefois, du fait que les paramètres globaux ne peuvent pas être supprimés, ils seront simplement réinitialisés à leurs valeurs par défaut. Par exemple, supposons que vous définissez la valeur de la propriété KeepCallDetailForDays dans les paramètres globaux sur 90. Si vous exécutez l’applet de commande **Remove-CsCdrConfiguration** sur les paramètres globaux, cette propriété sera réinitialisée à sa valeur par défaut, qui est de 60.

Personnes autorisées à exécuter cette applet de commande : Par défaut, les membres des groupes qui suivent sont autorisés à exécuter localement l’applet de commande **Remove-CsCdrConfiguration** : RTCUniversalServerAdmins. Pour retourner une liste de tous les rôles RBAC (Contrôle d’accès basé sur un rôle) auxquels cette applet de commande a été affectée (y compris les rôles RBAC personnalisés créés par vos soins), exécutez la commande suivante à l’invite Windows PowerShell :

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsCdrConfiguration"}

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
<td><p>Identificateur unique des paramètres de configuration d’enregistrement des détails des appels à supprimer. Pour « supprimer » les paramètres globaux, utilisez cette syntaxe : -Identity global. (Il est encore à noter que vous ne pouvez pas supprimer véritablement les paramètres globaux ; au lieu de cela, vous réinitialisez les propriétés à leurs valeurs par défaut.) Pour supprimer les paramètres configurés au niveau de l’étendue Site, utilisez une syntaxe similaire à celle-ci : -Identity site:Redmond. Vous ne pouvez pas utiliser de caractères génériques pour spécifier une identité.</p></td>
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

Microsoft.Rtc.Management.WritableConfig.Settings.CallDetailRecording.CdrSettings. L’applet de commande **Remove-CsCdrConfiguration** accepte l’entrée redirigée des objets de configuration d’enregistrement des détails des appels.

## Types de retours

Aucun. Au lieu de cela, l’applet de commande supprime les instances de l’objet Microsoft.Rtc.Management.WritableConfig.Settings.CallDetailRecording.CdrSettings.

## Voir aussi

#### Autres ressources

[Get-CsCdrConfiguration](get-cscdrconfiguration.md)  
[New-CsCdrConfiguration](new-cscdrconfiguration.md)  
[Set-CsCdrConfiguration](set-cscdrconfiguration.md)

