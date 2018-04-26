---
title: Remove-CsConferencingConfiguration
TOCTitle: Remove-CsConferencingConfiguration
ms:assetid: a3dff4b0-100b-46fa-9078-d3b0d4914d87
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Gg412767(v=OCS.15)
ms:contentKeyID: 49298394
ms.date: 05/20/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsConferencingConfiguration

 

_**Dernière rubrique modifiée :** 2015-03-09_

Supprime la collection de paramètres de configuration de conférence spécifiée. Les paramètres de conférence déterminent des caractéristiques telles que la taille maximale autorisée pour le contenu des conférences et des documents. Ils définissent aussi la période de grâce du contenu et les URL pour les téléchargements internes et externes du client pris en charge. Cette applet de commande est une nouveauté de Lync Server 2010.

## Syntaxe

    Remove-CsConferencingConfiguration -Identity <XdsIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## Exemples

## EXEMPLE 1

L’exemple 1 supprime les paramètres de configuration de conférence appliqués au site Redmond. Quand des paramètres de site tels que ceux-ci sont supprimés, les utilisateurs du site héritent automatiquement des paramètres contenus dans les paramètres globaux de configuration de conférence.

    Remove-CsConferencingConfiguration -Identity site:Redmond

## EXEMPLE 2

Dans l’exemple 2, la commande supprime tous les paramètres de configuration de conférence appliqués au niveau de l’étendue Site. Pour ce faire, la commande appelle d’abord l’applet de commande **Get-CsConferencingConfiguration** et le paramètre Filter. La valeur du filtre "site:" garantit que seuls les paramètres dont l’identité commence par les caractères "site:" sont retournés. Cette collection filtrée est alors redirigée vers l’applet de commande **Remove-CsConferencingConfiguration** qui supprime chaque élément de la collection.

    Get-CsConferencingConfiguration -Filter site:* | Remove-CsConferencingConfiguration

## EXEMPLE 3

L’exemple 3 supprime tous les paramètres de configuration de conférence dont l’organisation n’est pas définie sur Litwareinc. Pour effectuer cette tâche, la commande appelle d’abord l’applet de commande **Get-CsConferencingConfiguration** sans aucun paramètre, ce qui retourne la collection de tous les paramètres de configuration de conférence utilisés dans l’organisation. La collection est ensuite redirigée vers l’applet de commande **Where-Object** qui sélectionne uniquement les paramètres dont la propriété Organization est différente de Litwareinc. Enfin, la collection filtrée est redirigée vers l’applet de commande **Remove-CsConferencingConfiguration** qui supprime tous les paramètres de la collection.

    Get-CsConferencingConfiguration | Where-Object {$_.Organization -ne "Litwareinc"} | Remove-CsConferencingConfiguration

## Description détaillée

Pour les conférences, la gestion et l’administration sont divisées entre deux ensembles d’applets de commande. Si vous souhaitez gérer les choses que les utilisateurs peuvent et ne peuvent pas faire (par exemple, pouvoir inviter des participants anonymes à se joindre à une conférence, être autorisés à proposer le partage d’application et/ou le transfert de fichiers lors d’une conférence), vous devez alors utiliser les applets de commande **CsConferencingPolicy**.

Outre les activités des utilisateurs, les administrateurs doivent gérer le service de conférence web. Par exemple, les administrateurs doivent être en mesure, entre autres, de spécifier la quantité maximale de stockage de contenu attribuée à une conférence particulière et préciser la période de grâce avant que le contenu de la conférence soit automatiquement supprimé. Ils doivent également pouvoir spécifier les ports utilisés pour des activités telles que le partage d’application et le transfert de fichiers.

Ces dernières activités peuvent être gérées au moyen des applets de commande **CsConferencingConfiguration**. Ces applets de commande vous permettent de gérer les serveurs eux-mêmes. Les applets de commande **CsConferencingConfiguration** (qui peuvent être appliquées au niveau de l’étendue globale et des étendues Site et Service) ne sont pas utilisées pour spécifier si un utilisateur peut ou non partager des applications lors d’une conférence. Toutefois, si le partage d’application est autorisé, ces applets de commande vous permettent d’indiquer quels ports sont à utiliser pour cette activité. De même, les applets de commande vous permettent de spécifier, entre autres, les limites de stockage et les délais d’expiration, ainsi que des pointeurs vers des URL internes et externes où les utilisateurs peuvent obtenir de l’aide et des ressources ayant trait aux conférences.

L’applet de commande **Remove-CsConferencingConfiguration** permet de supprimer les collections personnalisées de paramètres de configuration de conférence créés pour être utilisés dans votre organisation. Quand vous supprimez une collection de paramètres, tout serveur préalablement concerné par ces paramètres est automatiquement géré par la collection suivante dans la hiérarchie (service – site – étendue). Si les paramètres supprimés sont appliqués au niveau de l’étendue Service, les serveurs sont gérés par les paramètres du site. S’il n’existe pas de paramètres au niveau de l’étendue Site, les serveurs sont gérés par les paramètres globaux. De même, si vous supprimez les paramètres au niveau de l’étendue Site, les serveurs préalablement gérés par ces paramètres de site sont gérés par les paramètres globaux.

Notez que vous pouvez également exécuter l’applet de commande **Remove-CsConferencingConfiguration** sur les paramètres globaux. Cependant, dans ce cas, les paramètres globaux ne seront pas supprimés car Lync Server ne vous permet pas d’effectuer cette opération. Toutes les propriétés de la collection globale seront en revanche réinitialisées à leurs valeurs par défaut. Par exemple, si vous avez préalablement modifié la valeur de stockage à 200 Mo, cette propriété retrouve sa valeur par défaut de 100 Mo.

Personnes autorisées à exécuter cette applet de commande : Par défaut, les membres des groupes qui suivent sont autorisés à exécuter localement l’applet de commande **Remove-CsConferencingConfiguration** : RTCUniversalServerAdmins. Pour retourner une liste de tous les rôles RBAC (Contrôle d’accès basé sur un rôle) auxquels cette applet de commande a été affectée (y compris les rôles RBAC personnalisés créés par vos soins), exécutez la commande suivante à l’invite Windows PowerShell :

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsConferencingConfiguration"}

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
<td><p>Identificateur unique de la collection de paramètres de configuration de conférence à supprimer. Pour supprimer les paramètres configurés au niveau de l’étendue Site, utilisez une syntaxe similaire à celle-ci : -Identity &quot;site:Redmond&quot;. Pour supprimer les paramètres configurés au niveau de l’étendue Service, utilisez une syntaxe similaire à celle-ci : -Identity &quot;service:ConferencingServer:atl-cs-001.litwareinc.com&quot;.</p>
<p>L’applet de commande <strong>Remove-CsConferencingConfiguration</strong> peut aussi être exécutée sur les paramètres globaux. Toutefois, dans ce cas, ces paramètres ne seront pas supprimés. En revanche, toutes les propriétés seront simplement réinitialisées à leurs valeurs par défaut.</p></td>
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

Objet Microsoft.Rtc.Management.WritableConfig.Settings.WebConf.ConfSettings. L’applet de commande **Remove-CsConferencingConfiguration** accepte les instances redirigées de l’objet de configuration de conférence.

## Types de retours

Aucun. Au lieu de cela, l’applet de commande **Remove-CsConferencingConfiguration** supprime les instances existantes de l’objet Microsoft.Rtc.Management.WritableConfig.Settings.WebConf.ConfSettings.

## Voir aussi

#### Autres ressources

[Get-CsConferencingConfiguration](get-csconferencingconfiguration.md)  
[New-CsConferencingConfiguration](new-csconferencingconfiguration.md)  
[Set-CsConferencingConfiguration](set-csconferencingconfiguration.md)

