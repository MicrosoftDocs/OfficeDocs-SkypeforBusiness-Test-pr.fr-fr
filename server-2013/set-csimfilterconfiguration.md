---
title: Set-CsImFilterConfiguration
TOCTitle: Set-CsImFilterConfiguration
ms:assetid: c2b08cc0-8261-4b8b-b2e9-5efa902ceb40
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Gg412960(v=OCS.15)
ms:contentKeyID: 49298770
ms.date: 05/20/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsImFilterConfiguration

 

_**Dernière rubrique modifiée :** 2015-03-09_

Modifie une configuration de filtre de message instantané existante. Les paramètres de filtre de message instantané sont utilisés pour empêcher les utilisateurs d’envoyer des messages instantanés contenant des liens hypertexte interactifs (sur lesquels il est possible de cliquer). Cette applet de commande est une nouveauté de Lync Server 2010.

## Syntaxe

    Set-CsImFilterConfiguration [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Set-CsImFilterConfiguration [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Action <Allow | Block | Warn>] [-AllowMessage <String>] [-BlockFileExtension <$true | $false>] [-Confirm [<SwitchParameter>]] [-Enabled <$true | $false>] [-Force <SwitchParameter>] [-IgnoreLocal <$true | $false>] [-Prefixes <PSListModifier>] [-WarnMessage <String>] [-WhatIf [<SwitchParameter>]]

## Exemples

## EXEMPLE 1

La commande présentée dans cet exemple désactive le filtrage URI pour les paramètres de filtre de message instantané dont l’identité est site:Redmond. Pour effectuer cette tâche, le paramètre Enabled est spécifié lors de l’appel de l’applet de commande **Set-CsImFilterConfiguration** avec la valeur $False.

    Set-CsImFilterConfiguration -Identity site:Redmond -Enabled $False

## EXEMPLE 2

L’exemple 2 ajoute un nouveau préfixe URI (urn:) à la liste des préfixes interdits par la configuration du filtre de messagerie instantanée de site:Redmond. Pour ajouter le nouveau préfixe, l’applet de commande **Get-CsImFilterConfiguration** est utilisée pour récupérer la configuration de site:Redmond ; l’objet retourné représentant cette configuration est stocké dans une variable appelée $x. Une fois les paramètres extraits, la méthode Add() est appelée à la ligne 2 pour ajouter urn: au groupe de préfixes stocké dans la propriété Prefixes. Cette opération modifie ainsi la valeur de la référence d’objet $x. Pour changer la configuration elle-même, la ligne 3 appelle l’applet de commande **Set-CsImFilterConfiguration**, en transmettant $x comme valeur de paramètre unique.

    $x = Get-CsImFilterConfiguration -Identity site:Redmond
    $x.Prefixes.Add("urn:")
    Set-CsImFilterConfiguration -Instance $x

## EXEMPLE 3

L’exemple 3 réalise exactement la même action que l’exemple 2, mais sur une seule ligne. Dans cette commande, le paramètre -Prefixes de l’applet de commande **Set-CsImFilterConfiguration** est utilisé pour ajouter urn: à la liste des préfixes. Le modificateur de liste add permet d’ajouter cette valeur à la liste des préfixes.

    Set-CsImFilterConfiguration -Identity site:Redmond -Prefixes @{add="urn:"}

## EXEMPLE 4

Dans cet exemple, le préfixe urn: est supprimé de la liste des préfixes bloqués par la configuration du filtre de messagerie instantanée de site:Redmond. Cet exemple est identique à l’exemple 3, mais au lieu d’appeler le modificateur de liste add pour ajouter un préfixe à la liste, le modificateur remove est appelé pour supprimer un préfixe.

    Set-CsImFilterConfiguration -Identity site:Redmond -Prefixes @{remove="urn:"}

## Description détaillée

Lors de l’envoi de messages instantanés, les utilisateurs peuvent incorporer un URI (Uniform Resource Identifier) dans le texte d’un message pour proposer aux autres participants de la conversation un site web ou un partage en particulier. Lync Server peut être configuré de sorte que les liens hypertexte comportant certains préfixes soient bloqués ou désactivés. (En d’autres termes, les participants ne pourront pas simplement cliquer sur le lien pour être redirigés vers le site référencé par l’URI, mais devront copier et coller le lien manuellement dans un navigateur.)

L’applet de commande **Set-CsImFilterConfiguration** vous permet de modifier la liste des préfixes URI qui seront filtrés, mais aussi d’activer et de désactiver complètement le filtrage, que ce soit globalement ou sur un site spécifique. Avec cette applet de commande, vous pouvez également mettre à jour divers messages d’avertissements aux utilisateurs.

Personnes autorisées à exécuter cette applet de commande : Par défaut, les membres des groupes qui suivent sont autorisés à exécuter localement l’applet de commande **Set-CsImFilterConfiguration** : RTCUniversalServerAdmins. Pour retourner une liste de tous les rôles RBAC (Contrôle d’accès basé sur un rôle) auxquels cette applet de commande a été affectée (y compris les rôles RBAC personnalisés créés par vos soins), exécutez la commande suivante à l’invite Windows PowerShell :

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsImFilterConfiguration"}

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
<td><p><em>Action</em></p></td>
<td><p>Facultatif</p></td>
<td><p>UrlFilterAction</p></td>
<td><p>La valeur de ce paramètre détermine l’action effectuée lorsqu’un lien hypertexte est inclus dans un message instantané :</p>
<p>Allow - Les liens hypertexte sont précédés d’un trait de soulignement afin que les liens ne soient plus actifs. De plus, si un message est spécifié dans la propriété AllowMessage, un message de notification sera inséré au début de chaque message instantané contenant des liens hypertexte.</p>
<p>Block - La remise des messages contenant des liens hypertexte est bloquée et Lync Server envoie un message d’erreur à l’expéditeur.</p>
<p>Warn - Les messages contenant des liens hypertexte sont remis aux participants destinataires, ainsi qu’un message d’avertissement qui est inséré au début de ces messages. Le message d’avertissement peut être spécifié à l’aide de la propriété WarnMessage. Si Warn est spécifié et qu’aucun message d’avertissement n’est entré, le filtrage des messages instantanés est désactivé, même si les paramètres de la propriété BlockFileExtension seront toujours appliqués.</p>
<p></p></td>
</tr>
<tr class="even">
<td><p><em>AllowMessage</em></p></td>
<td><p>Facultatif</p></td>
<td><p>Chaîne</p></td>
<td><p>Si une valeur est spécifiée pour ce paramètre, cette chaîne est insérée au début de chaque message contenant des liens hypertexte lorsque la valeur de la propriété Action est définie sur Allow. Vous pouvez utiliser ce message pour notifier aux utilisateurs des éléments comme les risques potentiels liés à la sélection de liens inconnus ou les exigences et politiques pertinentes de votre organisation.</p></td>
</tr>
<tr class="odd">
<td><p><em>BlockFileExtension</em></p></td>
<td><p>Facultatif</p></td>
<td><p>Booléen</p></td>
<td><p>Si ce paramètre est défini sur True, un lien hypertexte contenant un chemin d’accès au fichier avec une extension spécifiée par la propriété Extensions qui est définie dans la classe Microsoft.Rtc.Management.WritableConfig.Settings.ImFilter.FileTransferFilterConfiguration (extraite par l’appel de l’applet de commande <strong>Get-CsFileTransferFilterConfiguration</strong>) est bloqué et un message d’erreur est retourné à l’expéditeur. Si ce paramètre est défini sur False, aucun contrôle spécifique n’est effectué sur les chemins d’accès au fichier et les extensions.</p>
<p>Valeur par défaut : True</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>Facultatif</p></td>
<td><p>SwitchParameter</p></td>
<td><p>Vous demande confirmation avant d’exécuter la commande.</p></td>
</tr>
<tr class="odd">
<td><p><em>Enabled</em></p></td>
<td><p>Facultatif</p></td>
<td><p>Booléen</p></td>
<td><p>Active ou désactive cette fonction. Si ce paramètre est défini sur True, les liens hypertexte seront recherchés dans les messages instantanés et les règles de cette configuration seront appliquées. Si ce paramètre est défini sur False, les liens hypertexte ne seront pas recherchés dans les messages.</p>
<p>Valeur par défaut : True</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>Facultatif</p></td>
<td><p>SwitchParameter</p></td>
<td><p>Supprime les invites de confirmation qui s’affichent avant d’effectuer des modifications.</p></td>
</tr>
<tr class="odd">
<td><p><em>Identity</em></p></td>
<td><p>Facultatif</p></td>
<td><p>XdsIdentity</p></td>
<td><p>Identificateur unique des paramètres de configuration de filtre de message instantané que vous souhaitez modifier. Cette valeur sera soit de type global ou site:&lt;nom_site&gt;, où &lt;nom_site&gt; est le site auquel la configuration s’applique (par exemple, site:Redmond).</p>
<p></p></td>
</tr>
<tr class="even">
<td><p><em>IgnoreLocal</em></p></td>
<td><p>Facultatif</p></td>
<td><p>Booléen</p></td>
<td><p>La valeur de ce paramètre détermine si le filtrage doit être effectué sur les URI d’intranet local transmis dans les messages instantanés. Si ce paramètre est défini sur True, tout URI défini dans la zone Intranet de l’ordinateur local est ignoré. (L’ordinateur local est le serveur frontal exécutant l’application de filtre de message instantané.) Si ce paramètre est défini sur False, le filtrage spécifié s’applique à tous les liens hypertexte.</p>
<p>Valeur par défaut : True</p></td>
</tr>
<tr class="odd">
<td><p><em>Instance</em></p></td>
<td><p>Facultatif</p></td>
<td><p>ImFilterConfiguration</p></td>
<td><p>Permet de transmettre une référence à un objet à l’applet de commande plutôt que de définir des valeurs de paramètre individuelles. Cette applet de commande accepte un objet de type Microsoft.Rtc.Management.WritableConfig.Settings.ImFilter.ImFilterConfiguration, qui peut être récupéré en appelant l’applet de commande <strong>Get-CsImFilterConfiguration</strong>.</p></td>
</tr>
<tr class="even">
<td><p><em>Prefixes</em></p></td>
<td><p>Facultatif</p></td>
<td><p>PSListModifier</p></td>
<td><p>Liste des préfixes URI qui seront filtrés. Tout lien hypertexte inclus dans un message instantané et dont le préfixe correspond à l’un des préfixes présents dans cette liste sera filtré sur la base des paramètres spécifiés.</p>
<p>Valeur par défaut : callto:, file:, ftp., ftp:, gopher:, href, http:, https:, ldap:, mailto:, news:, nntp:, sip:, sips:, tel:, telnet:, www*.</p></td>
</tr>
<tr class="odd">
<td><p><em>WarnMessage</em></p></td>
<td><p>Facultatif</p></td>
<td><p>Chaîne</p></td>
<td><p>Ce paramètre contient le message d’avertissement qui est inséré au début de chaque message instantané contenant des liens hypertexte lorsque la valeur de la propriété Action est définie à Warn. En règle générale, ce message sera utilisé pour indiquer, par exemple, les risques potentiels engendrés par le fait de cliquer sur des liens inconnus ou de faire référence aux stratégies et besoins importants de votre organisation.</p></td>
</tr>
<tr class="even">
<td><p><em>WhatIf</em></p></td>
<td><p>Facultatif</p></td>
<td><p>SwitchParameter</p></td>
<td><p>Décrit ce qui se passe si vous exécutez la commande sans l’exécuter réellement.</p></td>
</tr>
</tbody>
</table>


## Types d’entrées

Objet Microsoft.Rtc.Management.WritableConfig.Settings.ImFilter.ImFilterConfiguration. Accepte l’entrée redirigée pour les objets de configuration de filtre de messagerie instantanée.

## Types de retours

L’applet de commande **Set-CsImFilterConfiguration** ne retourne ni valeur ni objet. Au lieu de cela, l’applet de commande configure les instances de l’objet Microsoft.Rtc.Management.WritableConfig.Settings.ImFilter.ImFilterConfiguration.

## Voir aussi

#### Autres ressources

[New-CsImFilterConfiguration](new-csimfilterconfiguration.md)  
[Remove-CsImFilterConfiguration](remove-csimfilterconfiguration.md)  
[Get-CsImFilterConfiguration](get-csimfilterconfiguration.md)

