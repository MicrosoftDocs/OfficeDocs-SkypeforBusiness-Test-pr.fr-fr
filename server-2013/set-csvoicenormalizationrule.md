---
title: Set-CsVoiceNormalizationRule
TOCTitle: Set-CsVoiceNormalizationRule
ms:assetid: 68850abb-4ac7-4ae1-bb6e-d991385f92a4
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Gg398491(v=OCS.15)
ms:contentKeyID: 49297477
ms.date: 05/20/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsVoiceNormalizationRule

 

_**Dernière rubrique modifiée :** 2015-03-09_

Modifie une règle de normalisation vocale. Les règles de normalisation vocale permettent de convertir une exigence de numérotation téléphonique (par exemple, composer le 9 pour accéder à une ligne externe) au format de numéro de téléphone E.164 utilisé par Lync Server. Cette applet de commande est une nouveauté de Lync Server 2010.

## Syntaxe

    Set-CsVoiceNormalizationRule [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Set-CsVoiceNormalizationRule [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Confirm [<SwitchParameter>]] [-Description <String>] [-Force <SwitchParameter>] [-IsInternalExtension <$true | $false>] [-Pattern <String>] [-Priority <Int32>] [-Translation <String>] [-WhatIf [<SwitchParameter>]]

## Exemples

## EXEMPLE 1

Cet exemple définit la description de la règle Prefix Redmond sur le site Redmond à « Ajouter un préfixe à tous les numéros sur le site Redmond ».

    Set-CsVoiceNormalizationRule -Identity "site:Redmond/Prefix Redmond" -Description "Add a prefix to all numbers on site Redmond"

## EXEMPLE 2

Cet exemple modifie la règle de normalisation vocale dont l’identité est global/SeattleFourDigit. Une nouvelle description a été spécifiée pour refléter les modifications apportées à la règle. En outre, une valeur Translation a été spécifiée de façon à ce que la règle traduise tout numéro correspondant au modèle existant de cette règle en un numéro identique mais portant le préfixe +1206556. Par exemple, si le modèle existant correspond à un numéro à quatre chiffres et que le numéro 1234 a été entré, cette règle traduit ce numéro de poste en numéro +12065561234.

    Set-CsVoiceNormalizationRule -Identity global/SeattleFourDigit -Description "Translate an internal four-digit extension" -Translation '+1206556$1'

## EXEMPLE 3

L’exemple 3 change le nom de la règle de normalisation. Rappelez-vous que modifier le nom modifie également la partie du nom de l’identité. L’applet de commande **Set-CsVoiceNormalizationRule** n’a pas de paramètre Name. Par conséquent, pour changer le nom, nous appelons d’abord l’applet de commande **Get-CsVoiceNormalizationRule** afin de récupérer la règle dont l’identité est global/RedmondFourDigit et nous affectons l’objet retourné à la variable $a. Nous affectons ensuite la chaîne RedmondRule à la propriété Name de l’objet. Ensuite, nous transmettons la variable au paramètre Instance de l’applet de commande **Set-CsVoiceNormalizationRule** pour que la modification soit permanente.

    $a = Get-CsVoiceNormalizationRule -Identity global/RedmondFourDigit
    $a.name = "RedmondRule"
    Set-CsVoiceNormalizationRule -Instance $a

## Description détaillée

Cette applet de commande modifie une règle de normalisation vocale nommée. Ces règles sont un élément obligatoire de l’autorisation téléphonique et du routage des appels. Elles définissent les exigences de conversion (ou traduction) des numéros d’un format Lync Server interne en format (E.164) standard. Il est utile de comprendre le fonctionnement des expressions régulières pour définir les modèles de numéro qui seront traduits.

Les règles modifiées avec cette applet de commande font partie du plan de numérotation et, outre le fait d’être accessibles via l’applet de commande **Get-CsVoiceNormalizationRule** elles le sont également via la propriété NormalizationRules renvoyée par un appel vers l’applet de commande **Get-CsDialPlan**.

Personnes autorisées à exécuter cette applet de commande : Par défaut, les membres des groupes qui suivent sont autorisés à exécuter localement l’applet de commande **Set-CsVoiceNormalizationRule** : RTCUniversalServerAdmins. Pour retourner une liste de tous les rôles RBAC (Contrôle d’accès basé sur un rôle) auxquels cette applet de commande a été affectée (y compris les rôles RBAC personnalisés créés par vos soins), exécutez la commande suivante à l’invite Windows PowerShell :

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsVoiceNormalizationRule"}

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
<td><p><em>Description</em></p></td>
<td><p>Facultatif</p></td>
<td><p>System.String</p></td>
<td><p>Description conviviale de la règle de normalisation.</p>
<p>Longueur de chaîne maximale : 512 caractères.</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>Facultatif</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Supprime les invites de confirmation qui s’affichent avant d’effectuer des modifications.</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>Facultatif</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>Identificateur unique de la règle. L’identité spécifiée doit inclure l’étendue suivie d’une barre oblique, puis du nom, par exemple : site:Redmond/Rule1, où site:Redmond est l’étendue et Rule1 est le nom.</p></td>
</tr>
<tr class="odd">
<td><p><em>Instance</em></p></td>
<td><p>Facultatif</p></td>
<td><p>NormalizationRule</p></td>
<td><p>Permet de transmettre une référence à un objet à la cmdlet plutôt que de définir des valeurs de paramètre individuelles. Cet objet doit être de type NormalizationRule et peut être récupéré en appelant l’applet de commande <strong>Get-CsVoiceNormalizationRule</strong></p></td>
</tr>
<tr class="even">
<td><p><em>IsInternalExtension</em></p></td>
<td><p>Facultatif</p></td>
<td><p>System.Boolean</p></td>
<td><p>Lorsqu’il est défini sur True, le résultat de l’application de cette règle sera un numéro interne à l’entreprise. Lorsqu’il est défini sur False, la règle génère un numéro externe. Cette valeur est ignorée si la valeur de la propriété OptimizeDeviceDialing du plan de numérotation associé est définie sur False.</p>
<p></p></td>
</tr>
<tr class="odd">
<td><p><em>Pattern</em></p></td>
<td><p>Facultatif</p></td>
<td><p>System.String</p></td>
<td><p>Expression régulière à laquelle le numéro composé doit correspondre pour que cette règle soit appliquée.</p>
<p></p></td>
</tr>
<tr class="even">
<td><p><em>Priority</em></p></td>
<td><p>Facultatif</p></td>
<td><p>System.Int32</p></td>
<td><p>Ordre dans lequel les règles sont appliquées. Un numéro peut correspondre à plusieurs règles. Ce paramètre définit l’ordre dans lequel les règles sont testées par rapport au numéro.</p></td>
</tr>
<tr class="odd">
<td><p><em>Translation</em></p></td>
<td><p>Facultatif</p></td>
<td><p>System.String</p></td>
<td><p>Modèle d’expression régulière qui sera appliqué au numéro afin de le convertir au format E.164.</p>
<p></p></td>
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

Objet Microsoft.Rtc.Management.WritableConfig.Policy.Voice.NormalizationRule. L’applet de commande **Set-CsVoiceNormalizationRule** accepte l’entrée redirigée pour les objets de règle de normalisation vocale.

## Types de retours

L’applet de commande **Set-CsVoiceNormalizationRule** ne retourne ni valeur ni objet. Au lieu de cela, l’applet de commande configure les instances de l’objet Microsoft.Rtc.Management.WritableConfig.Policy.Voice.NormalizationRule.

## Voir aussi

#### Autres ressources

[New-CsVoiceNormalizationRule](new-csvoicenormalizationrule.md)  
[Remove-CsVoiceNormalizationRule](remove-csvoicenormalizationrule.md)  
[Get-CsVoiceNormalizationRule](get-csvoicenormalizationrule.md)  
[Test-CsVoiceNormalizationRule](test-csvoicenormalizationrule.md)  
[Set-CsDialPlan](set-csdialplan.md)  
[Get-CsDialPlan](get-csdialplan.md)

