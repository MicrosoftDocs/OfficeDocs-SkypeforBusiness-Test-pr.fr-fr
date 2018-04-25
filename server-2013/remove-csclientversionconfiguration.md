---
title: Remove-CsClientVersionConfiguration
TOCTitle: Remove-CsClientVersionConfiguration
ms:assetid: 42065d1d-a0ef-4fa4-826b-d65b14b343c9
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Gg425925(v=OCS.15)
ms:contentKeyID: 49297025
ms.date: 05/20/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsClientVersionConfiguration

 

_**Dernière rubrique modifiée :** 2015-03-09_

Supprime le regroupement des paramètres de configuration définis de la version de client. Les paramètres de configuration de la version de client déterminent si Lync Server vérifie le numéro de version de chaque application cliente qui se connecte au système. Si le filtrage de version de client est activé, la possibilité pour l’application cliente de se connecter au système dépend des paramètres définis dans la stratégie de version de client appropriée. Cette applet de commande est une nouveauté de Lync Server 2010.

## Syntaxe

    Remove-CsClientVersionConfiguration -Identity <XdsIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## Exemples

## EXEMPLE 1

La commande illustrée dans l’exemple 1 supprime les paramètres de configuration de la version de client, dont le paramètre Identity est site:Redmond.

    Remove-CsClientVersionConfiguration -Identity site:Redmond

## EXEMPLE 2

Dans l’exemple 2, tous les paramètres de configuration de la version de client appliqués au niveau de l’étendue Site sont supprimés. Pour réaliser cette tâche, la commande appelle d’abord l’applet de commande **Get-CsClientVersionConfiguration** et le paramètre Filter. La valeur de filtre « site:\* » permet de s’assurer que seuls les paramètres de configuration de la version de client avec une identité commençant par la valeur de chaîne « site: » sont retournés. Cette collection filtrée est ensuite redirigée vers l’applet de commande **Remove-CsClientVersionConfiguration**, qui supprime chaque élément de la collection.

    Get-CsClientVersionConfiguration -Filter site:* | Remove-CsClientVersionConfiguration

## EXEMPLE 3

Dans l’exemple 3, tous les paramètres de configuration de la version de client actuellement désactivés sont supprimés. Pour ce faire, la commande appelle d’abord l’applet de commande **Get-CsClientVersionConfiguration** pour retourner une collection de tous les paramètres de configuration de la version de client actuellement utilisés dans l’organisation. Une fois ces données retournées, la collection est redirigée vers l’applet de commande **Where-Object** qui choisit uniquement les paramètres pour lesquels la propriété Enabled est égale à False. Ensuite, la collection filtrée est redirigée vers l’applet de commande **Remove-CsClientVersionConfiguration**, qui supprime chaque élément de cette collection.

    Get-CsClientVersionConfiguration | Where-Object {$_.Enabled -eq $False} | Remove-CsClientVersionConfiguration

## Description détaillée

Lync Server offre une grande souplesse aux administrateurs pour définir le logiciel client (ainsi que le numéro de version du logiciel, qui est tout aussi important) que les utilisateurs peuvent utiliser pour se connecter au système. Par exemple, il n’existe aucune contrainte technique qui impose aux utilisateurs de se connecter à Lync Server en utilisant Lync. D’un point de vue technique, rien n’empêche les utilisateurs de se connecter en utilisant Microsoft Office Communicator 2007 R2.

Toutefois, il peut exister des contraintes non techniques qui font qu’il est préférable que les utilisateurs ne se connectent pas en utilisant Office Communicator 2007 R2. Par exemple, Office Communicator 2007 R2 ne prend pas en charge les fonctionnalités et les fonctions de Lync. Par conséquent, les utilisateurs qui se connectent avec Office Communicator 2007 R2 auront une expérience différente de celle des utilisateurs qui se connectent via Lync. Cette situation peut poser des problèmes aux utilisateurs, ainsi qu’au personnel de l’assistance qui doit fournir un support pour un certain nombre d’applications clientes différentes.

Si cela pose un problème dans votre organisation, vous pouvez utiliser la fonctionnalité de filtrage de version de client afin de définir les applications clientes qui peuvent être utilisées pour se connecter à Lync Server. Lorsque vous installez Lync Server, un groupe de paramètres globaux de configuration des versions des clients est installé et activé. Outre les paramètres globaux, les paramètres de configuration de la version de client peuvent également être appliqués au niveau de l’étendue Site.

Tout paramètre de site créé peut être ensuite supprimé à l’aide de l’applet de commande **Remove-CsClientVersionConfiguration**. Notez que vous pouvez aussi exécuter l’applet de commande **Remove-CsClientVersionConfiguration** sur les paramètres globaux. Dans ce cas, les paramètres globaux ne seront pas supprimés. Toutefois, les propriétés globales seront réinitialisées à leurs valeurs par défaut.

Personnes autorisées à exécuter cette applet de commande : Par défaut, les membres des groupes qui suivent sont autorisés à exécuter localement l’applet de commande **Remove-CsClientVersionConfiguration** : RTCUniversalServerAdmins. Pour retourner une liste de tous les rôles RBAC (Contrôle d’accès basé sur un rôle) auxquels cette applet de commande a été affectée (y compris les rôles RBAC personnalisés créés par vos soins), exécutez la commande suivante à l’invite Windows PowerShell :

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsClientVersionConfiguration"}

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
<td><p>Identificateur unique de la collection de paramètres de configuration de la version de client à supprimer. Pour supprimer la collection globale, utilisez la syntaxe suivante : -Identity global. (Gardez à l’esprit que les paramètres globaux ne seront pas réellement supprimés. Toutefois, les propriétés globales seront toutes réinitialisées à leurs valeurs par défaut.) Pour supprimer une collection de sites, utilisez une syntaxe semblable à ceci : -Identity site:Redmond. Notez que les caractères génériques ne sont pas autorisés pour spécifier l’identité.</p></td>
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

Objet Microsoft.Rtc.Management.WritableConfig.Policy.ClientVersion.ClientVersionConfiguration. L’applet de commande **Remove-CsClientVersionConfiguration** accepte les instances redirigées de l’objet de configuration de la version de client.

## Types de retours

Aucun. Au lieu de cela, l’applet de commande supprime les instances de l’objet Microsoft.Rtc.Management.WritableConfig.Policy.ClientVersion.ClientVersionConfiguration.

## Voir aussi

#### Autres ressources

[Get-CsClientVersionConfiguration](get-csclientversionconfiguration.md)  
[New-CsClientVersionConfiguration](new-csclientversionconfiguration.md)  
[Set-CsClientVersionConfiguration](set-csclientversionconfiguration.md)

