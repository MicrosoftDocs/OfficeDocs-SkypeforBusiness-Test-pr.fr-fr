---
title: New-CsCdrConfiguration
TOCTitle: New-CsCdrConfiguration
ms:assetid: e5890ac3-7a6c-4609-a866-84c39b76d3a9
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Gg399018(v=OCS.15)
ms:contentKeyID: 49299152
ms.date: 05/20/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsCdrConfiguration

 

_**Dernière rubrique modifiée :** 2015-03-09_

Crée un ensemble de paramètres d’enregistrement des détails des appels. L’enregistrement des détails des appels permet d’assurer le suivi des sessions de messagerie instantanée d’égal à égal, des appels téléphoniques VoIP (Voice over Internet Protocol) et des téléconférences. Ces données d’utilisation permettent de savoir qui appelle qui, à quelle heure et la durée de l’entretien. Cette applet de commande est une nouveauté de Lync Server 2010.

## Syntaxe

    New-CsCdrConfiguration -Identity <XdsIdentity> [-Confirm [<SwitchParameter>]] [-EnableCDR <$true | $false>] [-EnablePurging <$true | $false>] [-Force <SwitchParameter>] [-InMemory <SwitchParameter>] [-KeepCallDetailForDays <UInt32>] [-KeepErrorReportForDays <UInt32>] [-PurgeHourOfDay <UInt32>] [-WhatIf [<SwitchParameter>]]

## Exemples

## EXEMPLE 1

La commande dans l’exemple 1 utilise l’applet de commande **New-CsCdrConfiguration** pour créer un nouvel ensemble de paramètres d’enregistrement des détails des appels avec l’identité site:Redmond. Outre l’identité site:Redmond, les nouveaux paramètres ont également la propriété EnableCDR définie sur False. Étant donné que les paramètres du site ont priorité sur les paramètres globaux, cela signifie que l’enregistrement des détails des appels n’est pas utilisé sur le site de Redmond, indépendamment du fait que l’enregistrement des détails des appels est activé ou non au niveau de l’étendue globale.

    New-CsCdrConfiguration -Identity site:Redmond -EnableCDR $False

## EXEMPLE 2

L’exemple 2 utilise le paramètre InMemory pour démontrer comment vous pouvez créer une nouvelle collection de paramètres de configuration d’enregistrement des détails des appels qui n’existent au départ que dans la mémoire. Pour ce faire, l’exemple utilise d’abord l’applet de commande **New-CsCdrConfiguration** et le paramètre InMemory pour créer une collection virtuelle de paramètres avec l’identité site:Redmond. Cette collection virtuelle est stockée dans la variable $x ; si la collection n’était pas stockée dans une variable, elle serait créée avant de disparaître immédiatement.

Une fois la collection virtuelle créée, la commande présentée à la ligne 2 définit la valeur de la propriété EnableCDR sur False ($False). À la ligne 3, l’applet de commande **Set-CsCdrConfiguration** est ensuite utilisée pour transformer la collection virtuelle $x en une collection réelle de paramètres de configuration d’enregistrement des détails des appels qui est appliquée au site de Redmond. Si l’applet de commande **Set-CsCdrConfiguration** n’était pas appelée, la collection virtuelle disparaîtrait aussitôt la session Windows PowerShell terminée ou la variable $x supprimée.

    $x = New-CsCdrConfiguration -Identity site:Redmond -InMemory
    $x.EnableCDR = $False
    Set-CsCdrConfiguration -Instance $x

## Description détaillée

L’enregistrement des détails des appels offre un moyen de suivre l’utilisation des fonctionnalités de Lync Server, comme les appels téléphoniques VoIP (Voice over Internet Protocol), la messagerie instantanée, les transferts de fichiers, les conférences audio/vidéo et les sessions de partage d’applications. L’enregistrement des détails des appels (qui n’est disponible que si vous avez déployé le service d’analyse) conserve les informations d’utilisation : il consigne des informations telles que les parties impliquées dans l’appel, la durée de l’appel et le transfert éventuel de fichiers. (Toutefois, l’enregistrement des détails des appels n’enregistre pas l’appel lui-même.)

L’enregistrement des détails des appels garde également en mémoire les informations sur les erreurs relatives aux appels : données de diagnostic détaillées des sessions d’égal à égal et des téléconférences.

En tant qu’administrateur, vous pouvez déterminer si la fonction d’enregistrement des détails des appels est utilisé ou pas dans votre organisation ; si le service d’analyse a été déployé, vous pouvez aisément activer ou désactiver cette fonction. De plus, vous avez la possibilité de prendre une décision globalement (auquel cas l’enregistrement des détails des appels pourra être activé ou désactivé dans toute l’organisation) ou par site. Par exemple, vous pouvez utiliser l’enregistrement des détails des appels sur le site de Redmond, mais pas sur le site de Paris.

L’applet de commande **New-CsCdrConfiguration** vous permet de créer des collections de paramètres d’enregistrement des détails des appels au niveau de l’étendue Site. (Il n’est pas possible de créer de nouveaux paramètres au niveau de l’étendue globale.) Notez qu’un site peut héberger uniquement une seule collection de paramètres d’enregistrement des détails des appels. Cela signifie que vous ne pouvez pas créer de collection pour le site de Redmond s’il dispose déjà d’un ensemble de paramètres de configuration d’enregistrement des détails des appels. Si vous essayez, cette commande échouera.

Personnes autorisées à exécuter cette applet de commande : Par défaut, les membres des groupes qui suivent sont autorisés à exécuter localement l’applet de commande **New-CsCdrConfiguration** : RTCUniversalServerAdmins. Pour retourner une liste de tous les rôles RBAC (Contrôle d’accès basé sur un rôle) auxquels cette applet de commande a été affectée (y compris les rôles RBAC personnalisés créés par vos soins), exécutez la commande suivante à l’invite Windows PowerShell :

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsCdrConfiguration"}

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
<td><p>Identificateur unique à affecter à la nouvelle collection de paramètres de configuration d’enregistrement des détails des appels. Puisque vous ne pouvez créer des collections qu’au niveau de l’étendue Site, l’identité sera toujours le préfixe « site: » suivi du nom du site (par exemple, « site:Redmond »).</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>Facultatif</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Vous demande confirmation avant d’exécuter la commande.</p></td>
</tr>
<tr class="odd">
<td><p><em>EnableCDR</em></p></td>
<td><p>Facultatif</p></td>
<td><p>System.Boolean</p></td>
<td><p>Indique si l’enregistrement des détails des appels est activé ou non. La valeur par défaut est True.</p></td>
</tr>
<tr class="even">
<td><p><em>EnablePurging</em></p></td>
<td><p>Facultatif</p></td>
<td><p>System.Boolean</p></td>
<td><p>Indique si les enregistrements des détails des appels doivent être périodiquement supprimés de la base de données d’enregistrements des détails des appels. Si la valeur est définie sur True (valeur par défaut), les enregistrements sont supprimés après la période indiquée par les propriétés KeepCallDetailForDays (enregistrements des détails des appels) et KeepErrorReportForDays (erreurs des détails des appels). Si la valeur est définie sur False, les enregistrements des détails des appels sont conservés indéfiniment.</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>Facultatif</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Supprime l’affichage de tous les messages d’erreur récupérable susceptibles d’apparaître lors de l’exécution de la commande.</p></td>
</tr>
<tr class="even">
<td><p><em>InMemory</em></p></td>
<td><p>Facultatif</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Crée une référence d’objet sans valider l’objet comme une modification définitive. Si vous affectez à une variable la sortie de cette cmdlet appelée avec ce paramètre, vous pouvez apporter des modifications aux propriétés de la référence d’objet, puis les valider en appelant la cmdlet Set- correspondante.</p></td>
</tr>
<tr class="odd">
<td><p><em>KeepCallDetailForDays</em></p></td>
<td><p>Facultatif</p></td>
<td><p>System.UInt32</p></td>
<td><p>Indique le nombre de jours durant lesquels les enregistrements des détails des appels sont conservés dans la base de données. Tout enregistrement plus ancien que le nombre de jours spécifié est automatiquement supprimé. (Notez que la purge ne se produit que si la propriété EnablePurging est définie sur True.)</p>
<p>Vous pouvez définir la propriété KeepCallDetailForDays sur n’importe quel entier entre 1 et 2562 jours (environ 7 ans). La valeur par défaut est 60.</p></td>
</tr>
<tr class="even">
<td><p><em>KeepErrorReportForDays</em></p></td>
<td><p>Facultatif</p></td>
<td><p>System.UInt32</p></td>
<td><p>Indique le nombre de jours durant lesquels les rapports d’erreur des détails des appels sont conservés. Tout rapport plus ancien que le nombre de jours spécifié est automatiquement supprimé. Les rapports d’erreur des détails des appels sont des rapports de diagnostic téléchargés par les applications clientes comme Lync 2013.</p>
<p>Vous pouvez définir cette propriété sur n’importe quelle valeur d’entier entre 1 et 2562 jours (environ 7 ans). La valeur par défaut est 60.</p></td>
</tr>
<tr class="odd">
<td><p><em>PurgeHourOfDay</em></p></td>
<td><p>Facultatif</p></td>
<td><p>System.UInt32</p></td>
<td><p>Indique l’heure locale du jour où les enregistrements qui ont expiré doivent être supprimés de la base de données d’enregistrements des détails des appels. L’heure de la journée est spécifiée à l’aide de l’horloge 24 heures, avec 0 qui représente minuit (0 h 00) et 23 qui représente 23 h 00. Notez que vous ne pouvez spécifier que le chiffre des heures, ce qui signifie que vous pouvez planifier la purge à 4 h 00 mais pas à 4 h 30 ou 4 h 15. La valeur par défaut est 2 (2 h 00). Il est recommandé de planifier la purge en dehors des heures de travail.</p>
<p>La purge de la base de données a lieu uniquement si la propriété EnablePurging a la valeur True.</p></td>
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

Aucun. L’applet de commande **New-CsCdrConfiguration** n’accepte pas l’entrée redirigée.

## Types de retours

Crée des instances de l’objet Microsoft.Rtc.Management.WritableConfig.Settings.CallDetailRecording.CdrSettings.

## Voir aussi

#### Autres ressources

[Get-CsCdrConfiguration](get-cscdrconfiguration.md)  
[Remove-CsCdrConfiguration](remove-cscdrconfiguration.md)  
[Set-CsCdrConfiguration](set-cscdrconfiguration.md)

