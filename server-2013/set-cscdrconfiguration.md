---
title: Set-CsCdrConfiguration
TOCTitle: Set-CsCdrConfiguration
ms:assetid: 977f0d3e-796b-43a3-bc0c-82ea91741c52
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Gg398774(v=OCS.15)
ms:contentKeyID: 49298202
ms.date: 05/20/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsCdrConfiguration

 

_**Dernière rubrique modifiée :** 2015-03-09_

Modifie une collection existante de paramètres d’enregistrement des détails des appels. L’enregistrement des détails des appels permet d’assurer le suivi des sessions de messagerie instantanée d’égal à égal, des appels téléphoniques VoIP (Voix sur IP) et des téléconférences. Ces données d’utilisation permettent de savoir qui appelle qui, à quelle heure et la durée de l’entretien. Cette applet de commande est une nouveauté de Lync Server 2010.

## Syntaxe

    Set-CsCdrConfiguration [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Set-CsCdrConfiguration [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Confirm [<SwitchParameter>]] [-EnableCDR <$true | $false>] [-EnablePurging <$true | $false>] [-Force <SwitchParameter>] [-KeepCallDetailForDays <UInt32>] [-KeepErrorReportForDays <UInt32>] [-PurgeHourOfDay <UInt32>] [-WhatIf [<SwitchParameter>]]

## Exemples

## EXEMPLE 1

L’exemple 1 fixe l’heure de purge des enregistrements obsolètes. Dans le cas présent, l’heure de purge est définie sur 23 (ou 11:00 P.M.) avec le format 24 heures. Le paramètre Identity permet de vérifier que ces modifications ne sont effectuées que pour les paramètres d’enregistrement des détails des appels dont l’identité est site:Redmond.

    Set-CsCdrConfiguration -Identity site:Redmond -PurgeHourOfDay 23 

## EXEMPLE 2

L’exemple 2 est une variation de la commande illustrée dans l’exemple 1. Dans ce cas, la propriété PurgeHourOfDay est modifiée pour chaque collection de paramètres de configuration d’enregistrement des détails des appels utilisée dans l’organisation. Pour ce faire, la commande appelle d’abord l’applet de commande **Get-CsCdrConfiguration** (sans paramètres) afin de retourner une collection de tous les paramètres d’enregistrement des détails des appels en cours d’utilisation. Cette collection est ensuite redirigée vers l’applet de commande **Set-CsCdrConfiguration**, qui extrait chaque élément de la collection et attribue à la propriété PurgeHourOfDay la valeur 11:00 PM (23).

    Get-CsCdrConfiguration | Set-CsCdrConfiguration -PurgeHourOfDay 23 

## EXEMPLE 3

L’exemple 3 est une autre variation de la commande illustrée à l’exemple 1. Dans cet exemple, la propriété PurgeHourOfDay est modifiée pour tous les paramètres d’enregistrement des détails des appels ayant été configurés au niveau de l’étendue Site. Pour exécuter cette tâche, la commande appelle d’abord l’applet de commande **Get-CsCdrConfiguration** avec le paramètre Filter ; la valeur de filtre "site:\*" garantit que seuls les paramètres dont l’identité commence par la valeur de chaîne "site:\*" sont retournés. La collection filtrée est alors redirigée vers l’applet de commande **Set-CsCdrConfiguration** qui modifie la propriété PurgeHourOfDay pour chaque élément contenu dans la collection.

    Get-CsCdrConfiguration -Filter "site:*"| Set-CsCdrConfiguration -PurgeHourOfDay 23

## Description détaillée

L’enregistrement des détails des appels offre un moyen de suivre l’utilisation des fonctionnalités de Lync Server, comme les appels téléphoniques VoIP (Voice over Internet Protocol), la messagerie instantanée, les transferts de fichiers, les conférences audio/vidéo et les sessions de partage d’applications. L’enregistrement des détails des appels (qui n’est disponible que si vous avez déployé le service de surveillance) conserve les informations d’utilisation : il consigne des informations telles que les parties impliquées dans l’appel, la durée de l’appel et le transfert éventuel de fichiers. Toutefois, l’enregistrement des détails des appels n’enregistre pas l’appel proprement dit.

L’enregistrement des détails des appels garde également une trace des informations d’erreur des appels : données de diagnostic détaillées des sessions d’égal à égal et des téléconférences.

En tant qu’administrateur, vous pouvez déterminer si l’enregistrement des détails des appels est utilisé ou non dans votre organisation. En supposant que le service de surveillance a été déployé, vous pouvez activer ou désactiver l’enregistrement des détails des appels. Par ailleurs, vous pouvez prendre cette décision au niveau global (dans ce cas, l’enregistrement des détails des appels sera activé ou désactivé dans toute l’organisation) ou au niveau de sites individuels. Par exemple, vous pouvez utiliser l’enregistrement des détails des appels sur le site Redmond, mais pas sur le site Paris.

Les administrateurs peuvent également gérer la base de données d’enregistrement des détails des appels, par exemple, en spécifiant le nombre de jours durant lesquels les enregistrements sont conservés avant d’être purgés de la base de données. Ces modifications peuvent être effectuées à l’aide de l’applet de commande **Set-CsCdrConfiguration**.

Personnes autorisées à exécuter cette applet de commande : Par défaut, les membres des groupes qui suivent sont autorisés à exécuter localement l’applet de commande **Set-CsCdrConfiguration** : RTCUniversalServerAdmins. Pour retourner une liste de tous les rôles RBAC (Contrôle d’accès basé sur un rôle) auxquels cette applet de commande a été affectée (y compris les rôles RBAC personnalisés créés par vos soins), exécutez la commande suivante à l’invite Windows PowerShell :

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsCdrConfiguration"}

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
<td><p><em>EnableCDR</em></p></td>
<td><p>Facultatif</p></td>
<td><p>System.Boolean</p></td>
<td><p>Indique si l’enregistrement des détails des appels est activé ou non. La valeur par défaut est True.</p></td>
</tr>
<tr class="odd">
<td><p><em>EnablePurging</em></p></td>
<td><p>Facultatif</p></td>
<td><p>System.Boolean</p></td>
<td><p>Indique si les enregistrements des détails des appels doivent être périodiquement supprimés de la base de données d’enregistrement des détails des appels. Si la valeur est définie sur True (valeur par défaut), les enregistrements sont supprimés après la période spécifiée par les propriétés KeepCallDetailForDays (enregistrements des détails des appels) et KeepErrorReportForDays (erreurs des détails des appels). Si la valeur est définie sur False, les enregistrements des détails des appels sont conservés indéfiniment.</p></td>
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
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>Identificateur unique affecté à la collection des paramètres de configuration de l’enregistrement des détails des appels. Pour vous référer aux paramètres globaux, utilisez cette syntaxe : -Identity global. Pour vous référer à une collection configurée au niveau de l’étendue Site, utilisez une syntaxe de type : -Identity site:Redmond. Notez que vous ne pouvez pas utiliser de caractères génériques lorsque vous spécifiez une identité.</p>
<p>Si ce paramètre est omis, l’applet de commande <strong>Set-CsCdrConfiguration</strong> modifie les paramètres globaux.</p></td>
</tr>
<tr class="even">
<td><p><em>Instance</em></p></td>
<td><p>Facultatif</p></td>
<td><p>Objet CdrSettings</p></td>
<td><p>Permet de transmettre une référence à un objet à la cmdlet plutôt que de définir des valeurs de paramètre individuelles.</p></td>
</tr>
<tr class="odd">
<td><p><em>KeepCallDetailForDays</em></p></td>
<td><p>Facultatif</p></td>
<td><p>System.UInt32</p></td>
<td><p>Indique le nombre de jours durant lesquels les enregistrements des détails des appels sont conservés dans la base de données. Tout enregistrement plus ancien que le nombre de jours spécifié est automatiquement supprimé. (Notez que la purge ne se produit que si la propriété EnablePurging est définie sur True.)</p>
<p>Vous pouvez définir cette propriété sur n’importe quelle valeur d’entier comprise entre 1 et 2562 jours (environ 7 ans). La valeur par défaut est 60.</p></td>
</tr>
<tr class="even">
<td><p><em>KeepErrorReportForDays</em></p></td>
<td><p>Facultatif</p></td>
<td><p>System.UInt32</p></td>
<td><p>Indique le nombre de jours durant lesquels les rapports d’erreur sur l’enregistrement des détails des appels sont conservés. Tout rapport plus ancien que le nombre de jours spécifié est automatiquement supprimé. Les rapports d’erreur sur l’enregistrement des détails des appels sont des rapports de diagnostic téléchargés par des applications clientes comme Lync 2013.</p>
<p>Vous pouvez définir cette propriété sur n’importe quelle valeur d’entier comprise entre 1 et 2562 jours (environ 7 ans). La valeur par défaut est 60.</p></td>
</tr>
<tr class="odd">
<td><p><em>PurgeHourOfDay</em></p></td>
<td><p>Facultatif</p></td>
<td><p>System.UInt32</p></td>
<td><p>Indique l’heure locale du jour où les enregistrements qui ont expiré doivent être supprimés de la base de données d’enregistrements des détails des appels. L’heure est spécifiée au format 24 heures, 0 correspondant à minuit (00:00 AM) et 23 à 11:00 PM. Notez que vous ne pouvez indiquer que le chiffre des heures. Cela signifie que vous pouvez, par exemple, planifier la purge à 4:00 AM, mais pas à 4:30 AM ou 4:15 AM. La valeur par défaut est 2 (2:00 A.M.). Il est recommandé de planifier la purge en dehors des heures de travail.</p>
<p>La purge de la base de données ne se produit que si la propriété EnablePurging est définie sur True.</p></td>
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

Microsoft.Rtc.Management.WritableConfig.Settings.CallDetailRecording.CdrSettings. L’applet de commande **Set-CsCdrConfiguration** accepte l’entrée redirigée des objets de configuration d’enregistrement des détails des appels.

## Types de retours

L’applet de commande **Set-CsCdrConfiguration** ne renvoie aucune valeur ni objet. Au lieu de cela, l’applet de commande configure les instances de l’objet Microsoft.Rtc.Management.WritableConfig.Settings.CallDetailRecording.CDRSettings.

## Voir aussi

#### Autres ressources

[Get-CsCdrConfiguration](get-cscdrconfiguration.md)  
[New-CsCdrConfiguration](new-cscdrconfiguration.md)  
[Remove-CsCdrConfiguration](remove-cscdrconfiguration.md)

