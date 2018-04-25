---
title: Set-CsOutboundTranslationRule
TOCTitle: Set-CsOutboundTranslationRule
ms:assetid: fbf82146-7884-418c-8239-66c0ca0f2ba6
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Gg413073(v=OCS.15)
ms:contentKeyID: 49299430
ms.date: 05/20/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsOutboundTranslationRule

 

_**Dernière rubrique modifiée :** 2015-03-09_

Modifie une règle de traduction sortante existante. Une règle de traduction sortante permet de convertir des numéros de téléphone au format de numérotation local afin de communiquer avec des systèmes PBX (autocommutateur privé). Cette applet de commande est une nouveauté de Lync Server 2010.

## Syntaxe

    Set-CsOutboundTranslationRule [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Set-CsOutboundTranslationRule [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Confirm [<SwitchParameter>]] [-Description <String>] [-Force <SwitchParameter>] [-Pattern <String>] [-Priority <Int32>] [-Translation <String>] [-WhatIf [<SwitchParameter>]]

## Exemples

## EXEMPLE 1

Dans cet exemple, la règle de traduction sortante globale comportant l’identité site:Redmond/Prefix Redmond est modifiée. Nous avons inclus une description expliquant que cette règle concerne la traduction de numéros au format E.164 en numéros de téléphone à sept chiffres. De plus, les valeurs Pattern and Translation ont été spécifiées, ce qui entraînera une modification des valeurs existantes pour ces propriétés. Pour traduire un numéro E.164 (dans ce cas, 12 chiffres commençant par +1425), spécifié par l’expression régulière dans le modèle, en un numéro à sept chiffres, ces valeurs suppriment les cinq premiers chiffres. Par exemple, le numéro +14255551212 est traduit en numéro 5551212.

    Set-CsOutboundTranslationRule -Identity "site:Redmond/Prefix Redmond" -Description "Convert to seven digits" -Pattern '^\+1425(\d{7})$' -Translation '$1'

## EXEMPLE 2

Cet exemple modifie la propriété Name d’une règle de traduction sortante. Notez que cette action entraîne une modification de l’identité (Identity) de cette règle. La première commande présentée dans cet exemple appelle l’applet de commande **Get-CsOutboundTranslationRule**. Une identité site:Redmond\\OBR1 est spécifié afin de retourner une règle de traduction unique, à savoir la règle qui comporte l’identité donnée. Au lieu d’afficher cette règle, nous l’affectons à la variable $a. La ligne 2 de cet exemple affecte la chaîne « Outbound Rule 1 » à la propriété Name de la variable $a, soit la variable contenant une référence à la règle site:Redmond/OBR1. Sur la dernière ligne de cet exemple, nous appelons l’applet de commande **Set-CsOutboundTranslationRule** en spécifiant le paramètre Instance et en le transmettant à la variable $a. Si nous appelons maintenant l’applet de commande **Get-CsOutboundTranslationRule** avec la valeur Identity « site:Redmond/OBR1 », aucun élément ne sera retourné. Cela tient au fait que la règle comportant cette identité n’existe plus. Elle a été remplacée par la même règle, mais avec l’identité site:Redmond/Outbound Rule 1.

    $a = Get-CsOutboundTranslationRule -Identity "site:Redmond/OBR1"
    $a.Name = "Outbound Rule 1"
    Set-CsOutboundTranslationRule -Instance $a

## Description détaillée

Lync Server normalise les numéros de téléphone au format E.164. Cependant, de nombreux systèmes PBX (autocommutateur privé) ne sont pas compatibles avec ce format. Les règles de traduction sortantes convertissent le numéro au format de numérotation local avant de le transmettre au serveur de médiation ou à la passerelle. Appelez cette applet de commande pour modifier une règle de traduction sortante existante.

Chaque règle de traduction sortante est associée à une configuration de tronçon. Cela signifie que l’utilisation de cette applet de commande pour modifier une règle aura une incidence sur la configuration de tronçon correspondante. Vous pouvez associer plusieurs règles de traduction sortante à chaque configuration. Par conséquent, l’identité de chaque règle se compose d’une étendue et d’un nom unique au sein de cette dernière (au format étendue/nom ; par exemple : site:Redmond/OBR1). La règle est automatiquement associée à la configuration de tronçon comportant la même étendue. Le recours à l’applet de commande **Set-CsOutboundTranslationRule** est recommandé pour modifier des règles de traduction sortante dans une configuration de tronçon.

Personnes autorisées à exécuter cette applet de commande : Par défaut, les membres des groupes qui suivent sont autorisés à exécuter localement l’applet de commande **Set-CsOutboundTranslationRule** : RTCUniversalServerAdmins. Pour retourner une liste de tous les rôles RBAC (Contrôle d’accès basé sur un rôle) auxquels cette applet de commande a été affectée (y compris les rôles RBAC personnalisés créés par vos soins), exécutez la commande suivante à l’invite Windows PowerShell :

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsOutboundTranslationRule"}

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
<td><p>SwitchParameter</p></td>
<td><p>Vous demande confirmation avant d’exécuter la commande.</p></td>
</tr>
<tr class="even">
<td><p><em>Description</em></p></td>
<td><p>Facultatif</p></td>
<td><p>String</p></td>
<td><p>Description conviviale de la règle de traduction sortante. Cette description permet aux administrateurs d’identifier clairement l’objectif de la règle.</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>Facultatif</p></td>
<td><p>SwitchParameter</p></td>
<td><p>Supprime les invites de confirmation qui s’affichent avant d’effectuer des modifications.</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>Facultatif</p></td>
<td><p>XdsIdentity</p></td>
<td><p>Identificateur unique de la règle de traduction sortante que vous souhaitez modifier. L’identité se compose de l’étendue suivie d’un nom unique dans chaque étendue. Par exemple : site:Redmond/OutboundRule1.</p></td>
</tr>
<tr class="odd">
<td><p><em>Instance</em></p></td>
<td><p>Facultatif</p></td>
<td><p>TranslationRule</p></td>
<td><p>Référence d’objet à une règle de traduction sortante. Cet objet doit être du type Microsoft.Rtc.Management.WritableConfig.Settings.TrunkConfiguration.TranslationRule que vous pouvez extraire en appelant l’applet de commande <strong>Get-CsOutboundTranslationRule</strong>.</p></td>
</tr>
<tr class="even">
<td><p><em>Pattern</em></p></td>
<td><p>Facultatif</p></td>
<td><p>String</p></td>
<td><p>Expression régulière représentant le modèle de numéro auquel la traduction sera appliquée.</p></td>
</tr>
<tr class="odd">
<td><p><em>Priority</em></p></td>
<td><p>Facultatif</p></td>
<td><p>Int32</p></td>
<td><p>Si un numéro correspond au modèle de plusieurs règles de traduction sortante, ces dernières sont appliquées par ordre de priorité. Utilisez ce paramètre pour affecter une priorité à la règle.</p></td>
</tr>
<tr class="even">
<td><p><em>Translation</em></p></td>
<td><p>Facultatif</p></td>
<td><p>String</p></td>
<td><p>Expression régulière qui sera appliquée au numéro correspondant au modèle pour le préparer au routage sortant.</p></td>
</tr>
<tr class="odd">
<td><p><em>WhatIf</em></p></td>
<td><p>Facultatif</p></td>
<td><p>SwitchParameter</p></td>
<td><p>Décrit ce qui se passe si vous exécutez la commande sans l’exécuter réellement.</p></td>
</tr>
</tbody>
</table>


## Types d’entrées

Objet Microsoft.Rtc.Management.WritableConfig.Settings.TrunkConfiguration.TranslationRule. Accepte l’entrée redirigée pour les objets de règle de traduction sortante.

## Types de retours

Cette applet de commande ne retourne aucune valeur. Elle modifie un objet de type Microsoft.Rtc.Management.WritableConfig.Settings.TrunkConfiguration.TranslationRule.

## Voir aussi

#### Autres ressources

[New-CsOutboundTranslationRule](new-csoutboundtranslationrule.md)  
[Remove-CsOutboundTranslationRule](remove-csoutboundtranslationrule.md)  
[Get-CsOutboundTranslationRule](get-csoutboundtranslationrule.md)

