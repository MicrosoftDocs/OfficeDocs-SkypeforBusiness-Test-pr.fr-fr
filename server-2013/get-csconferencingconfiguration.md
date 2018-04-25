---
title: Get-CsConferencingConfiguration
TOCTitle: Get-CsConferencingConfiguration
ms:assetid: db4ab3bc-071c-4f73-a3a0-62dc8aed48a1
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Gg398965(v=OCS.15)
ms:contentKeyID: 49299059
ms.date: 05/20/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsConferencingConfiguration

 

_**Dernière rubrique modifiée :** 2015-03-09_

Retourne des informations sur les paramètres de configuration de conférence de votre organisation. Les paramètres de conférence déterminent certains éléments comme la taille maximale autorisée des documents et du contenu de la conférence, la période de grâce du contenu (à savoir, la durée pendant laquelle le contenu sera stocké avant d’être supprimé) et les URL des téléchargements internes et externes du client pris en charge. Cette applet de commande est une nouveauté de Lync Server 2010.

## Syntaxe

    Get-CsConferencingConfiguration [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Get-CsConferencingConfiguration [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-LocalStore <SwitchParameter>]

## Exemples

## EXEMPLE 1

L’exemple 1 retourne des informations sur tous les paramètres de configuration de conférence actuellement utilisés dans l’organisation. Pour ce faire, appelez l’applet de commande **Get-CsConferencingConfiguration** sans aucun paramètre.

    Get-CsConferencingConfiguration

## EXEMPLE 2

Dans l’exemple 2, les informations de configuration de conférence sont retournées pour le site Redmond (-Identity site:Redmond). Puisque les identités doivent être uniques, cette commande retournera toujours au mieux une collection unique de paramètres de configuration de conférence.

    Get-CsConferencingConfiguration -Identity site:Redmond

## EXEMPLE 3

La commande présentée dans l’exemple 3 retourne des informations sur tous les paramètres de configuration de conférence qui ont été appliqués au niveau de l’étendue Site. Pour cela, l’applet de commande **Get-CsConferencingConfiguration** est appelée avec le paramètre Filter. La valeur de filtre "site:\*" garantit que seuls les paramètres dont l’identité commence par la valeur de chaîne "site:" sont retournés.

    Get-CsConferencingConfiguration -Filter "site:*"

## EXEMPLE 4

La commande ci-dessus retourne des informations sur tous les paramètres de configuration de conférence où l’organisation n’est pas définie sur Litwareinc. Pour cela, la commande appelle d’abord l’applet de commande **Get-CsConferencingConfiguration** sans paramètre afin de retourner une collection de tous les paramètres de configuration de conférence utilisés dans l’organisation. La collection obtenue est ensuite redirigée vers l’applet de commande **Where-Object** qui sélectionne uniquement les paramètres dont la propriété Organization est différente de Litwareinc.

    Get-CsConferencingConfiguration | Where-Object {$_.Organization -ne "Litwareinc"}

## EXEMPLE 5

Dans l’exemple 5, des informations sont retournées uniquement pour les paramètres de configuration de conférence où l’espace de stockage de contenu maximal est supérieur à 100 mégaoctets. Pour cela, la commande appelle d’abord l’applet de commande **Get-CsConferencingConfiguration** sans paramètre afin de retourner une collection de tous vos paramètres de configuration de conférence. Cette collection est ensuite redirigée vers l’applet de commande **Where-Object** qui sélectionne uniquement les paramètres pour lesquels l’espace de stockage de contenu est supérieur à 100 mégaoctets.

    Get-CsConferencingConfiguration | Where-Object {$_.MaxContentStorageMB -gt 100}

## Description détaillée

Pour les conférences, la gestion et l’administration sont divisées entre deux ensembles d’applets de commande. Si vous souhaitez gérer les choses que les utilisateurs peuvent et ne peuvent pas faire (par exemple, pouvoir inviter des participants anonymes à se joindre à une conférence, être autorisés à proposer le partage d’application et/ou le transfert de fichiers lors d’une conférence), vous devez alors utiliser les applets de commande **CsConferencingPolicy**.

Outre les activités des utilisateurs, les administrateurs doivent gérer le Lync Server service de conférence web. Par exemple, les administrateurs doivent être en mesure, entre autres, de spécifier la quantité maximale de stockage de contenu attribuée à une conférence particulière et préciser la période de grâce avant que le contenu de la conférence soit automatiquement supprimé. Ils doivent également pouvoir spécifier les ports utilisés pour des activités telles que le partage d’application et le transfert de fichiers.

Ces dernières activités peuvent être gérées au moyen des applets de commande **CsConferencingConfiguration**. Ces applets de commande vous permettent de gérer les serveurs eux-mêmes. Les applets de commande **CsConferencingConfiguration** (qui peuvent être appliquées au niveau de l’étendue globale et des étendues Site et Service) ne sont pas utilisées pour spécifier si un utilisateur peut ou non partager des applications lors d’une conférence ; si le partage d’application est autorisé, toutefois, ces applets de commande vous permettent d’indiquer quels ports sont à utiliser pour cette activité. De même, les applets de commande vous permettent de spécifier, entre autres, les limites de stockage et les délais d’expiration, ainsi que des pointeurs vers des URL internes et externes où les utilisateurs peuvent obtenir de l’aide et des ressources ayant trait aux conférences.

L’applet de commande **Get-CsConferencingConfiguration** permet aux administrateurs de retourner des informations sur tous les paramètres de configuration de conférence actuellement utilisés dans leur organisation.

Personnes autorisées à exécuter cette applet de commande : Par défaut, les membres des groupes qui suivent sont autorisés à exécuter localement l’applet de commande **Get-CsConferencingConfiguration** : RTCUniversalUserAdmins, RTCUniversalServerAdmins. Pour retourner une liste de tous les rôles RBAC (Contrôle d’accès basé sur un rôle) auxquels cette applet de commande a été affectée (y compris les rôles RBAC personnalisés créés par vos soins), exécutez la commande suivante à l’invite Windows PowerShell :

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsConferencingConfiguration"}

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
<td><p><em>Filter</em></p></td>
<td><p>Facultatif</p></td>
<td><p>System.String</p></td>
<td><p>Vous permet d’utiliser des caractères génériques lors de la définition de l’identité des paramètres de configuration de conférence à retourner. Par exemple, cette syntaxe retourne tous les paramètres configurés au niveau de l’étendue Site : -Filter &quot;site:*&quot;. Cette syntaxe retourne tous les paramètres configurés au niveau de l’étendue Service : -Filter &quot;service:*&quot;.</p>
<p>Notez que vous ne pouvez pas utiliser les paramètres Identity et Filter dans la même commande.</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>Facultatif</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>Identificateur unique pour la collection de paramètres de configuration de conférence à récupérer. Pour récupérer les paramètres globaux, utilisez la syntaxe suivante : -Identity global. Pour récupérer les paramètres configurés au niveau de l’étendue Site, utilisez une syntaxe du type : -Identity &quot;site:Redmond&quot;. Pour récupérer les paramètres configurés au niveau de l’étendue Service, utilisez une syntaxe semblable à ceci : -Identity &quot;service:ConferencingServer:atl-cs-001.litwareinc.com&quot;.</p>
<p>Si ce paramètre n’est pas inclus, alors l’applet de commande <strong>Get-CsConferencingConfiguration</strong> retournera tous les paramètres de configuration de conférence actuellement utilisés dans votre organisation.</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>Facultatif</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Récupère les données de configuration de conférence à partir du réplica local du magasin central de gestion et non depuis le magasin central de gestion lui-même.</p></td>
</tr>
</tbody>
</table>


## Types d’entrées

Aucun. L’applet de commande **Get-CsConferencingConfiguration** n’accepte pas l’entrée redirigée.

## Types de retours

L’applet de commande **Get-CsConferencingConfiguration** retourne des instances de l’objet Microsoft.Rtc.Management.WriteableConfig.Settings.WebConf.ConfSettings.

## Voir aussi

#### Autres ressources

[New-CsConferencingConfiguration](new-csconferencingconfiguration.md)  
[Remove-CsConferencingConfiguration](remove-csconferencingconfiguration.md)  
[Set-CsConferencingConfiguration](set-csconferencingconfiguration.md)

