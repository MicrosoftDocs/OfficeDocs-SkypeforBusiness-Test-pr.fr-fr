---
title: New-CsImFilterConfiguration
TOCTitle: New-CsImFilterConfiguration
ms:assetid: 1964cbf9-d7f1-4b4e-99d1-951ac42d82fe
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Gg398244(v=OCS.15)
ms:contentKeyID: 49296397
ms.date: 05/20/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsImFilterConfiguration

 

_**Dernière rubrique modifiée :** 2015-03-09_

Crée une nouvelle configuration de filtre de messagerie instantanée. Les filtres de messagerie instantanée servent à empêcher des utilisateurs d’envoyer des messages instantanés contenant des liens hypertexte actifs. Cette applet de commande est une nouveauté de Lync Server 2010.

## Syntaxe

    New-CsImFilterConfiguration -Identity <XdsIdentity> [-Action <Allow | Block | Warn>] [-AllowMessage <String>] [-BlockFileExtension <$true | $false>] [-Confirm [<SwitchParameter>]] [-Enabled <$true | $false>] [-Force <SwitchParameter>] [-IgnoreLocal <$true | $false>] [-InMemory <SwitchParameter>] [-Prefixes <PSListModifier>] [-WarnMessage <String>] [-WhatIf [<SwitchParameter>]]

## Exemples

## EXEMPLE 1

Dans l’exemple 1, l’applet de commande **New-CsImFilterConfiguration** est utilisée pour créer une nouvelle configuration de filtre de messagerie instantanée comportant l’identité site:Redmond (aucun paramètre supplémentaire n’étant spécifié, ces paramètres seront créés avec les valeurs par défaut).

    New-CsImFilterConfiguration -Identity site:Redmond

## EXEMPLE 2

Dans cette commande, l’applet de commande **New-CsImFilterConfiguration** est utilisée pour créer une nouvelle configuration de filtre de messagerie instantanée comportant l’identité site:Redmond Étant donné que le paramètre Prefixes a été spécifié, la nouvelle configuration inclura toutes les valeurs par défaut, y compris les préfixes par défaut à filtrer, ainsi que deux préfixes d’URI supplémentaires : rtsp: et urn:. Pour ajouter ces préfixes à la liste par défaut, nous utilisons un modificateur de liste d’ajout.

    New-CsImFilterConfiguration -Identity site:Redmond -Prefixes @{add="rtsp:","urn:"}

## EXEMPLE 3

Dans cette commande, l’applet de commande **New-CsFileTransferFilterConfiguration** est utilisée pour créer une nouvelle configuration de filtre de messagerie instantanée comportant l’identité site:Redmond Cet exemple est similaire à l’exemple 2, excepté que le modificateur de liste de remplacement a été utilisé à la place du modificateur de liste d’ajout. Cela signifie que tous les préfixes d’URI par défaut seront remplacés par ces deux préfixes (rtsp: et urn:). Par conséquent, seuls les URI dotés des préfixes rtsp: ou urn: seront filtrés dans les messages instantanés pour le site de Redmond.

    New-CsImFilterConfiguration -Identity site:Redmond -Prefixes @{replace="rtsp:","urn:"}

## Description détaillée

Lors de l’envoi des messages instantanés, les utilisateurs peuvent incorporer un URI (Uniform Resource Identifier) dans le texte d’un message pour proposer aux autres participants de la conversation un site web ou un partage en particulier. Lync Server peut être configuré de sorte que les liens hypertexte comportant certains préfixes soient bloqués ou désactivés. (En d’autres termes, les participants ne pourront pas simplement cliquer sur le lien pour être redirigés vers le site de référence de l’URI ; ils devront en effet copier et coller le lien manuellement dans un navigateur).

L’applet de commande **New-CsImFilterConfiguration** vous permet de définir une liste des préfixes URI qui seront filtrés, en plus d’activer et de désactiver le filtrage, dans un site spécifique. L’appel de l’applet de commande **New-CsImFilterConfiguration** en spécifiant une seule identité entraîne la création d’une nouvelle configuration avec cette identité, en renseignant la liste des préfixes pour ce site avec un ensemble de préfixes par défaut qui seront filtrés.

Personnes autorisées à exécuter cette applet de commande : Par défaut, les membres des groupes qui suivent sont autorisés à exécuter localement l’applet de commande **New-CsImFilterConfiguration** : RTCUniversalServerAdmins. Pour retourner une liste de tous les rôles RBAC (Contrôle d’accès basé sur un rôle) auxquels cette applet de commande a été affectée (y compris les rôles RBAC personnalisés créés par vos soins), exécutez la commande suivante à l’invite Windows PowerShell :

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsImFilterConfiguration"}

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
<td><p>XdsIdentity</p></td>
<td><p>Identificateur unique spécifiant l’étendue de la configuration du filtre de messagerie instantanée. Les paramètres globaux existent par défaut et ne peuvent pas être recréés avec l’applet de commande <strong>New-CsImFilterConfiguration</strong>. Toutefois, vous pouvez créer des paramètres au niveau du site en spécifiant une valeur d’identité site:&lt;nom du site&gt;, où &lt;nom du site&gt; correspond au nom du site auquel les paramètres seront appliqués (par exemple, site:Redmond).</p>
<p>Type de données complet : Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
</tr>
<tr class="even">
<td><p><em>Action</em></p></td>
<td><p>Facultatif</p></td>
<td><p>UrlFilterAction</p></td>
<td><p>La valeur de ce paramètre détermine l’action qui sera effectuée lorsqu’un lien hypertexte est inclus dans un message instantané :</p>
<p>Allow - Les liens hypertexte sont précédés d’un trait de soulignement de sorte que les liens ne sont plus actifs. Si un message est spécifié dans la propriété AllowMessage, celui-ci sera inséré au début de chaque message instantané contenant des liens hypertexte.</p>
<p>Block : la remise des messages contenant des liens hypertexte est bloquée et Lync Server envoie un message d’erreur à l’expéditeur.</p>
<p>Warn - Les messages contenant des liens hypertexte actifs sont remis aux participants auxquels ils sont destinés, et un message d’avertissement est inséré au début de ces messages. Vous pouvez spécifier un message d’avertissement à l’aide de la propriété WarnMessage. Si le paramètre Warn est spécifié et qu’aucun message d’avertissement n’est saisi, le filtrage de la messagerie instantanée est désactivé, même si les paramètres de la propriété BlockFileExtension sont toujours validés.</p>
<p>Valeur par défaut : Allow, sauf si un message contient plus de 1 000 URL. Dans ce cas, la valeur par défaut est Block.</p>
<p>Type de données complet : Microsoft.Rtc.Management.WritableConfig.Settings.ImFilter.UrlFilterAction</p></td>
</tr>
<tr class="odd">
<td><p><em>AllowMessage</em></p></td>
<td><p>Facultatif</p></td>
<td><p>String</p></td>
<td><p>Si une valeur est spécifiée pour ce paramètre, cette chaîne est insérée au début de chaque message contenant des liens hypertexte lorsque la valeur de la propriété Action est définie sur Allow. Vous pouvez utiliser ce message pour notifier aux utilisateurs des éléments comme les risques potentiels liés à la sélection de liens inconnus ou les exigences et politiques pertinentes de votre organisation.</p></td>
</tr>
<tr class="even">
<td><p><em>BlockFileExtension</em></p></td>
<td><p>Facultatif</p></td>
<td><p>Boolean</p></td>
<td><p>Si ce paramètre est défini sur True, un lien hypertexte contenant un chemin d’accès au fichier avec une extension spécifiée par la propriété Extensions qui est définie dans la configuration de filtre de transfert de fichiers applicable (extraite par l’appel de l’applet de commande <strong>Get-CsFileTransferFilterConfiguration</strong>) est bloqué et un message d’erreur est retourné à l’expéditeur. Si ce paramètre est défini sur False, aucune vérification spécifique n’est effectuée sur les extensions de fichier.</p>
<p>Valeur par défaut : True</p></td>
</tr>
<tr class="odd">
<td><p><em>Confirm</em></p></td>
<td><p>Facultatif</p></td>
<td><p>SwitchParameter</p></td>
<td><p>Vous demande confirmation avant d’exécuter la commande.</p></td>
</tr>
<tr class="even">
<td><p><em>Enabled</em></p></td>
<td><p>Facultatif</p></td>
<td><p>Boolean</p></td>
<td><p>Active ou désactive cette fonctionnalité. Si ce paramètre est défini sur True, des liens hypertexte seront recherchés dans les messages instantanés et les règles de cette configuration seront appliquées. S’il est défini sur False, aucune recherche de liens hypertexte ne sera effectuée dans les messages.</p>
<p>Valeur par défaut : True</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>Facultatif</p></td>
<td><p>SwitchParameter</p></td>
<td><p>Supprime les invites de confirmation qui s’affichent avant d’effectuer des modifications.</p></td>
</tr>
<tr class="even">
<td><p><em>IgnoreLocal</em></p></td>
<td><p>Facultatif</p></td>
<td><p>Boolean</p></td>
<td><p>La valeur de ce paramètre détermine si le filtrage doit être effectué sur les URI Intranet locales transmises dans les messages instantanés. Si ce paramètre est défini sur True, tous les URI définis dans la zone Intranet de l’ordinateur local sont ignorés (L’ordinateur local est le serveur frontal exécutant l’application de filtre de messagerie instantanée.) Si ce paramètre est défini sur False, le filtrage spécifié est appliqué à tous les liens hypertexte.</p>
<p>Valeur par défaut : True</p></td>
</tr>
<tr class="odd">
<td><p><em>InMemory</em></p></td>
<td><p>Facultatif</p></td>
<td><p>SwitchParameter</p></td>
<td><p>Crée une référence d’objet sans valider l’objet comme une modification définitive. Si vous affectez à une variable la sortie de cette cmdlet appelée avec ce paramètre, vous pouvez apporter des modifications aux propriétés de la référence d’objet, puis les valider en appelant la cmdlet Set- correspondante.</p></td>
</tr>
<tr class="even">
<td><p><em>Prefixes</em></p></td>
<td><p>Facultatif</p></td>
<td><p>PSListModifier</p></td>
<td><p>Liste des préfixes URI qui seront filtrés. Tous les liens hypertexte inclus dans un message instantané dont le préfixe correspond à l’un des préfixes de cette liste seront filtrés en fonction des paramètres spécifiés.</p>
<p>Valeur par défaut : callto:, file:, ftp., ftp:, gopher:, href, http:, https:, ldap:, mailto:, news:, nntp:, sip:, sips:, tel:, telnet:, www*.</p></td>
</tr>
<tr class="odd">
<td><p><em>WarnMessage</em></p></td>
<td><p>Facultatif</p></td>
<td><p>String</p></td>
<td><p>Ce paramètre contient le message d’avertissement qui est inséré au début de chaque message instantané incluant des liens hypertexte lorsque la valeur de la propriété Action est définie sur Warn. En règle générale, ce message sera utilisé pour indiquer, par exemple, les risques potentiels engendrés par le fait de cliquer sur des liens inconnus ou de faire référence aux stratégies et besoins importants de votre organisation.</p></td>
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

Aucun.

## Types de retours

Crée un objet de type Microsoft.Rtc.Management.WritableConfig.Settings.ImFilter.ImFilterConfiguration.

## Voir aussi

#### Autres ressources

[Remove-CsImFilterConfiguration](remove-csimfilterconfiguration.md)  
[Set-CsImFilterConfiguration](set-csimfilterconfiguration.md)  
[Get-CsImFilterConfiguration](get-csimfilterconfiguration.md)

