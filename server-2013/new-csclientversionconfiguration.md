---
title: New-CsClientVersionConfiguration
TOCTitle: New-CsClientVersionConfiguration
ms:assetid: e7aac850-9e29-4d18-8929-74a89e9355cd
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Gg399029(v=OCS.15)
ms:contentKeyID: 49299175
ms.date: 05/20/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsClientVersionConfiguration

 

_**Dernière rubrique modifiée :** 2015-03-09_

Crée une collection de paramètres de configuration de version des clients. Les paramètres de configuration de version des clients déterminent si Lync Server vérifie le numéro de version de chaque application cliente qui se connecte au système. Si le filtrage de version de client est activé, la possibilité pour l’application cliente de se connecter au système dépend des paramètres définis dans la stratégie de version de client appropriée. Cette applet de commande est une nouveauté de Lync Server 2010.

## Syntaxe

    New-CsClientVersionConfiguration -Identity <XdsIdentity> [-Confirm [<SwitchParameter>]] [-DefaultAction <Allow | AllowWithUrl | Block | BlockWithUrl>] [-DefaultURL <String>] [-Enabled <$true | $false>] [-Force <SwitchParameter>] [-InMemory <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## Exemples

## EXEMPLE 1

La commande présentée dans l’exemple 1 crée une collection de paramètres de configuration de version des clients pour le site de Redmond. Dans cette commande, le paramètre Enabled est affecté de la valeur False, ce qui signifie que le filtrage des clients est désactivé pour le site de Redmond.

    New-CsClientVersionConfiguration -Identity site:Redmond -Enabled $False

## EXEMPLE 2

L’exemple 2 montre comment vous pouvez créer une collection de paramètres de configuration de version des clients en mémoire, modifier cette collection, puis transformer ces paramètres virtuels en une collection réelle de paramètres appliqués au site de Redmond. Pour ce faire, la première commande fait appel à l’applet de commande **New-CsClientVersionConfiguration** et au paramètre InMemory pour créer une collection en mémoire uniquement de paramètres avec l’identité site:Redmond. Cette collection est stockée dans une variable appelée $x et existe en mémoire uniquement : si vous mettez fin à votre session Windows PowerShell ou si vous supprimez la variable $x, ces paramètres de configuration de version des clients disparaîtront et ne seront jamais appliqués au site de Redmond.

Dans la commande 2, la valeur de la propriété DefaultAction pour les paramètres virtuels est définie sur Block. Dans la commande 3, l’applet de commande **Set-CsClientVersionConfiguration** est utilisée pour transformer les paramètres virtuels en une collection réelle de paramètres de configuration de version des clients qui est appliquée au site de Redmond.

    $x = New-CsClientVersionConfiguration -Identity site:Redmond -InMemory
    $x.DefaultAction = "Block" 
    Set-CsClientVersionConfiguration -Instance $x

## Description détaillée

Lync Server offre une grande souplesse aux administrateurs pour définir le logiciel client (ainsi que le numéro de version du logiciel, qui est tout aussi important) que les utilisateurs peuvent utiliser pour se connecter au système. Par exemple, il n’existe aucune contrainte technique qui impose aux utilisateurs de se connecter à Lync Server en utilisant Lync. D’un point de vue technique, rien n’empêche les utilisateurs de se connecter en utilisant Microsoft Office Communicator 2007 R2.

Toutefois, il peut exister des contraintes non techniques qui font qu’il est préférable que les utilisateurs ne se connectent pas en utilisant Office Communicator 2007 R2. Par exemple, Office Communicator 2007 R2 ne prend pas en charge les fonctionnalités et les fonctions de Lync. Par conséquent, les utilisateurs qui se connectent avec Office Communicator 2007 R2 auront une expérience différente de celle des utilisateurs qui se connectent via Lync. Cette situation peut poser des problèmes aux utilisateurs, ainsi qu’au personnel de l’assistance qui doit fournir un support pour un certain nombre d’applications clientes différentes.

Si cela pose un problème dans votre organisation, vous pouvez utiliser la fonctionnalité de filtrage de version de client afin de définir les applications clientes qui peuvent être utilisées pour se connecter à Lync Server. Lorsque vous installez Lync Server, un groupe de paramètres globaux de configuration de version des clients est installé et activé. Ces paramètres déterminent si le filtrage des versions des clients est activé.

En plus des paramètres globaux, l’applet de commande **New-CsClientVersionConfiguration** permet de créer des paramètres de configuration de version des clients au niveau de l’étendue Site. Lorsque vous appliquez les paramètres de configuration de version des clients au niveau de l’étendue Site, ces paramètres prévalent sur les paramètres globaux. Par exemple, supposons que vous avez activé le filtrage des versions des clients au niveau de l’étendue globale, puis que vous avez créé une collection distincte de paramètres pour le site de Redmond, une collection de paramètres pour laquelle le filtrage des versions des clients est désactivé. Dans ce cas, le filtrage des versions des clients sera désactivé pour tous les utilisateurs qui disposent de comptes sur le site de Redmond.

Notez toutefois que les utilisateurs anonymes sont affectés uniquement par les paramètres globaux. C’est la raison pour laquelle ils ne sont pas associés à un site.

Notez que la configuration de la version des clients n’est pas une fonction de sécurité. La technologie s’appuie sur l’auto-création de rapports à partir des applications clientes et ne tente pas de vérifier si une application correspond réellement à l’application et au numéro de version qu’elle prétend être.

Personnes autorisées à exécuter cette applet de commande : Par défaut, les membres des groupes qui suivent sont autorisés à exécuter localement l’applet de commande **New-CsClientVersionConfiguration** : RTCUniversalServerAdmins. Pour retourner une liste de tous les rôles RBAC (Contrôle d’accès basé sur un rôle) auxquels cette applet de commande a été affectée (y compris les rôles RBAC personnalisés créés par vos soins), exécutez la commande suivante à l’invite Windows PowerShell :

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsClientVersionConfiguration"}

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
<td><p>Identificateur unique à affecter à la nouvelle collection de paramètres de configuration de version des clients. Puisque vous ne pouvez créer des collections qu’au niveau de l’étendue Site, l’identité sera toujours le préfixe « site: » suivi du nom du site (par exemple, « site:Redmond »). Notez que la commande ci-dessus échouera si une collection de paramètres avec l’identité site:Redmond existe déjà.</p>
<p></p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>Facultatif</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Vous demande confirmation avant d’exécuter la commande.</p></td>
</tr>
<tr class="odd">
<td><p><em>DefaultAction</em></p></td>
<td><p>Facultatif</p></td>
<td><p>Microsoft.Rtc.Management.WritableConfig.Policy.ClientVersion.DefaultAction</p></td>
<td><p>Indique l’action à exécuter si l’utilisateur tente de se connecter depuis une application cliente dont le numéro de version est introuvable dans la stratégie de version de client appropriée. DefaultAction doit avoir l’une des valeurs suivantes :</p>
<p>Allow. L’application cliente est autorisée à se connecter.</p>
<p>AllowWithUrl. L’application cliente est autorisée à se connecter. Par ailleurs, le message qui s’affiche à l’attention de l’utilisateur contient l’URL d’une page Web depuis laquelle il peut télécharger une application cliente approuvée. Vous devez définir l’URL de cette page Web comme valeur de la propriété DefaultUrl.</p>
<p>Block. L’application cliente n’est pas autorisée à se connecter.</p>
<p>BlockWithUrl. L’application cliente n’est pas autorisée à se connecter. Toutefois, le message de refus d’accès qui s’affiche à l’attention de l’utilisateur contient l’URL d’une page Web depuis laquelle il peut télécharger une application cliente approuvée. Vous devez définir l’URL de cette page Web comme valeur de la propriété DefaultUrl.</p>
<p>Cette propriété est ignorée si la propriété Enabled est affectée de la valeur False. Lorsque cette propriété a la valeur False, aucun filtrage de la version des clients n’a lieu.</p></td>
</tr>
<tr class="even">
<td><p><em>DefaultURL</em></p></td>
<td><p>Facultatif</p></td>
<td><p>System.String</p></td>
<td><p>Définit l’URL de la page web depuis laquelle l’utilisateur peut télécharger une application cliente approuvée. Si vous la définissez et que DefaultAction a la valeur BlockWithUrl, l’URL apparaît dans le message de refus d’accès qui s’affiche chaque fois qu’un utilisateur tente de se connecter depuis une application cliente non prise en charge.</p></td>
</tr>
<tr class="odd">
<td><p><em>Enabled</em></p></td>
<td><p>Facultatif</p></td>
<td><p>System.Boolean</p></td>
<td><p>Indique si le filtrage des versions des clients est activé ou désactivé. Si la propriété Enabled est affectée de la valeur True, le serveur vérifie le numéro de version de chaque application cliente qui tente de se connecter ; le serveur autorise ou refuse l’accès en fonction de la stratégie de version de client appropriée. Si la propriété Enabled a la valeur False, toute application cliente en mesure de se connecter est autorisée à le faire.</p>
<p>La valeur par défaut est True.</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>Facultatif</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Supprime l’affichage de tous les messages d’erreur récupérable susceptibles d’apparaître lors de l’exécution de la commande.</p></td>
</tr>
<tr class="odd">
<td><p><em>InMemory</em></p></td>
<td><p>Facultatif</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Crée une référence d’objet sans valider l’objet comme une modification définitive. Si vous affectez à une variable la sortie de cette cmdlet appelée avec ce paramètre, vous pouvez apporter des modifications aux propriétés de la référence d’objet, puis les valider en appelant la cmdlet Set- correspondante.</p></td>
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

Aucun. L’applet de commande **New-CsClientVersionConfiguration** n’accepte pas l’entrée redirigée.

## Types de retours

Crée de nouvelles instances de l’objet Microsoft.Rtc.Management.WritableConfig.Policy.ClientVersion.ClientVersionConfiguration.

## Voir aussi

#### Autres ressources

[Get-CsClientVersionConfiguration](get-csclientversionconfiguration.md)  
[Remove-CsClientVersionConfiguration](remove-csclientversionconfiguration.md)  
[Set-CsClientVersionConfiguration](set-csclientversionconfiguration.md)

