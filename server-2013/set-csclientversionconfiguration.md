---
title: Set-CsClientVersionConfiguration
TOCTitle: Set-CsClientVersionConfiguration
ms:assetid: 7cd2e86f-2d31-4db2-9d0f-f1418fd4aba2
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Gg398623(v=OCS.15)
ms:contentKeyID: 49297855
ms.date: 05/20/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsClientVersionConfiguration

 

_**Dernière rubrique modifiée :** 2015-03-09_

Modifie le regroupement des paramètres de configuration définis de la version du client. Les paramètres de configuration de la version déterminent si Lync Server vérifie le numéro de version de chaque application cliente qui se connecte au système. Si le filtrage de version de client est activé, la possibilité pour l’application cliente de se connecter au système dépend des paramètres définis dans la stratégie de version de client appropriée. Cette applet de commande est une nouveauté de Lync Server 2010.

## Syntaxe

    Set-CsClientVersionConfiguration [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Set-CsClientVersionConfiguration [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Confirm [<SwitchParameter>]] [-DefaultAction <Allow | AllowWithUrl | Block | BlockWithUrl>] [-DefaultURL <String>] [-Enabled <$true | $false>] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## Exemples

## EXEMPLE 1

Dans l’exemple 1, l’applet de commande **Set-CsClientVersionConfiguration** permet de modifier la collection de paramètres avec l’identité « site:Redmond ». Dans ce cas, le paramètre Enabled est défini sur False afin de désactiver les paramètres de configuration des versions des clients.

    Set-CsClientVersionConfiguration -Identity site:Redmond -Enabled $False

## EXEMPLE 2

Dans la commande de l’exemple 2, la propriété DefaultUrl est modifiée pour tous les paramètres de configuration des versions des clients utilisés dans l’organisation. Pour ce faire, la commande appelle d’abord l’applet de commande **Get-CsClientVersionConfiguration** sans paramètres supplémentaires pour retourner tous les paramètres de configuration des versions des clients. Ces informations sont ensuite transmises à l’applet de commande **Set-CsClientVersionConfiguration** qui affecte la valeur https://litwareinc.com/csclients à DefaultUrl pour chaque collection de configurations.

    Get-CsClientVersionConfiguration | Set-CsClientVersionConfiguration -DefaultURL "https://litwareinc.com/csclients"

## EXEMPLE 3

Dans l’exemple 3, tous les paramètres de configuration des versions des clients sont modifiés lorsque la valeur de DefaultAction est Block. Pour effectuer cette tâche, la commande utilise d’abord l’applet de commande **Get-CsClientVersionConfiguration** pour retourner tous les paramètres de configuration des versions des clients actuellement utilisés. Ces informations sont ensuite redirigées vers l’applet de commande **Where-Object** qui choisit uniquement les éléments pour lesquels la propriété DefaultAction est définie sur Block. La collection filtrée est ensuite envoyée à l’applet de commande **Set-CsClientVersionConfiguration** qui exécute deux actions pour chacun des éléments de la collection : 1) elle affecte à DefaultAction la valeur BlockWithUrl et 2) elle affecte à DefaultUrl la valeur https://litwareinc.com/csclients.

    Get-CsClientVersionConfiguration | Where-Object {$_.DefaultAction -eq "Block"} | Set-CsClientVersionConfiguration -DefaultAction "BlockWithUrl" -DefaultURL "https://litwareinc.com/csclients"

## Description détaillée

Lync Server offre une grande souplesse aux administrateurs pour définir le logiciel client (ainsi que le numéro de version du logiciel, qui est tout aussi important) que les utilisateurs peuvent utiliser pour se connecter au système. Par exemple, il n’existe aucune contrainte technique qui impose aux utilisateurs de se connecter à Lync Server en utilisant Lync. D’un point de vue technique, rien n’empêche les utilisateurs de se connecter en utilisant Microsoft Office Communicator 2007 R2.

En revanche, il peut exister des contraintes non techniques qui peuvent inciter les utilisateurs à ne pas se connecter en utilisant Office Communicator 2007 R2. Par exemple, Office Communicator 2007 R2 ne prend pas en charge les fonctionnalités et les fonctions de Lync. Par conséquent, les utilisateurs qui se connectent avec Office Communicator 2007 R2 auront une expérience différente de celle des utilisateurs qui se connectent via Lync. Cette situation peut poser des problèmes aux utilisateurs, ainsi qu’au personnel de l’assistance qui doit fournir un support pour un certain nombre d’applications clientes différentes

Si cela pose un problème dans votre organisation, vous pouvez utiliser la fonctionnalité de filtrage de version de client afin de définir les applications clientes qui peuvent être utilisées pour se connecter à Lync Server. Lorsque vous installez Lync Server, un groupe de paramètres globaux de configuration des versions des clients est installé et activé. Ces paramètres déterminent si le filtrage des versions des clients est activé. Outre les paramètres globaux, des paramètres de configuration de la version cliente peuvent être appliqués au niveau de l’étendue Site. Dans ce cas, les paramètres de site sont prioritaires sur les paramètres globaux.

L’applet de commande **Set-CsClientVersionConfiguration** permet de modifier une collection existante de paramètres de configuration des versions des clients.

Notez que la configuration de version de client n’est pas une fonctionnalité de sécurité. La technologie s’appuie sur l’auto-création de rapports à partir des applications clientes et ne tente pas de vérifier si une application correspond réellement à l’application et au numéro de version qu’elle prétend être.

Personnes autorisées à exécuter cette applet de commande : Par défaut, les membres des groupes qui suivent sont autorisés à exécuter localement l’applet de commande **Set-CsClientVersionConfiguration** : RTCUniversalServerAdmins. Pour retourner une liste de tous les rôles RBAC (Contrôle d’accès basé sur un rôle) auxquels cette applet de commande a été affectée (y compris les rôles RBAC personnalisés créés par vos soins), exécutez la commande suivante à l’invite Windows PowerShell :

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsClientVersionConfiguration"}

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
<td><p><em>DefaultAction</em></p></td>
<td><p>Facultatif</p></td>
<td><p>Microsoft.Rtc.Management.WritableConfig.Policy.ClientVersion.DefaultAction</p></td>
<td><p>Indique l’action à exécuter si l’utilisateur tente de se connecter depuis une application cliente dont le numéro de version est introuvable dans la stratégie de version de client appropriée. DefaultAction doit avoir l’une des valeurs suivantes :</p>
<p>Allow. L’application cliente est autorisée à se connecter.</p>
<p>AllowWithUrl. L’application cliente est autorisée à se connecter. Par ailleurs, le message qui s’affiche à l’attention de l’utilisateur contient l’URL d’une page web depuis laquelle il peut télécharger une application cliente approuvée. Vous devez définir l’URL de cette page web comme valeur de la propriété DefaultUrl.</p>
<p>Block. L’application cliente n’est pas autorisée à se connecter.</p>
<p>BlockWithUrl. L’application cliente n’est pas autorisée à se connecter. Toutefois, le message de refus d’accès qui s’affiche à l’attention de l’utilisateur contient l’URL d’une page web depuis laquelle il peut télécharger une application cliente approuvée. Vous devez définir l’URL de cette page web comme valeur de la propriété DefaultUrl.</p>
<p>Cette propriété est ignorée si la propriété Enabled est affectée de la valeur False. Lorsque cette propriété a la valeur False, aucun filtrage de la version des clients n’a lieu.</p></td>
</tr>
<tr class="odd">
<td><p><em>DefaultURL</em></p></td>
<td><p>Facultatif</p></td>
<td><p>System.String</p></td>
<td><p>Définit l’URL de la page web depuis laquelle l’utilisateur peut télécharger une application cliente approuvée. Si vous la définissez et que DefaultAction a la valeur BlockWithURL, l’URL apparaît dans le message de refus d’accès qui s’affiche chaque fois qu’un utilisateur tente de se connecter depuis une application cliente non prise en charge.</p></td>
</tr>
<tr class="even">
<td><p><em>Enabled</em></p></td>
<td><p>Facultatif</p></td>
<td><p>System.Boolean</p></td>
<td><p>Indique si le filtrage des versions des clients est activé ou désactivé. Si la propriété Enabled est définie sur True, le serveur vérifie le numéro de version de chaque application cliente qui tente de se connecter. Le serveur autorise ou refuse l’accès en fonction de la stratégie de version de client appropriée. Si la propriété Enabled a la valeur False, toute application cliente en mesure de se connecter est autorisée à le faire.</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>Facultatif</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Supprime l’affichage de tous les messages d’erreur récupérable susceptibles d’apparaître lors de l’exécution de la commande.</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>Facultatif</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>Correspond à l’identificateur unique des paramètres de configuration de la version de client à modifier. Pour modifier les paramètres globaux, utilisez la syntaxe suivante : -Identity global. Pour modifier les paramètres associés à l’étendue du site, utilisez la syntaxe suivante : &quot;site:Redmond&quot;.</p>
<p>Si vous ne définissez pas ce paramètre, l’applet de commande <strong>Set-CsClientVersionConfiguration</strong> définit automatiquement les paramètres globaux.</p></td>
</tr>
<tr class="odd">
<td><p><em>Instance</em></p></td>
<td><p>Facultatif</p></td>
<td><p>Objets ClientVersionPolicy</p></td>
<td><p>Permet de transmettre une référence à un objet à la cmdlet plutôt que de définir des valeurs de paramètre individuelles.</p></td>
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

Objet Microsoft.Rtc.Management.WritableConfig.Policy.ClientVersion.ClientVersionConfiguration. L’applet de commande **Set-CsClientVersionConfiguration** accepte les instances redirigées de l’objet de configuration de la version du client.

## Types de retours

L’applet de commande **Set-CsClientVersionConfiguration** ne renvoie aucune valeur ni aucun objet. Au lieu de cela, l’applet de commande configure les instances de l’objet Microsoft.Rtc.Management.WritableConfig.Policy.ClientVersion.ClientVersionConfiguration.

## Voir aussi

#### Autres ressources

[Get-CsClientVersionConfiguration](get-csclientversionconfiguration.md)  
[New-CsClientVersionConfiguration](new-csclientversionconfiguration.md)  
[Remove-CsClientVersionConfiguration](remove-csclientversionconfiguration.md)

