---
title: Set-CsVoiceTestConfiguration
TOCTitle: Set-CsVoiceTestConfiguration
ms:assetid: 7b95fc95-ec0e-4bb3-aed1-e8b72e305999
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Gg398614(v=OCS.15)
ms:contentKeyID: 49297834
ms.date: 05/20/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsVoiceTestConfiguration

 

_**Dernière rubrique modifiée :** 2015-03-09_

Modifie un scénario de test que vous pouvez utiliser pour tester des numéros de téléphone par rapport aux itinéraires et aux règles spécifiés. Cette applet de commande est une nouveauté de Lync Server 2010.

## Syntaxe

    Set-CsVoiceTestConfiguration [-Identity <XdsGlobalRelativeIdentity>] <COMMON PARAMETERS>

    Set-CsVoiceTestConfiguration [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Confirm [<SwitchParameter>]] [-DialedNumber <String>] [-ExpectedRoute <String>] [-ExpectedTranslatedNumber <String>] [-ExpectedUsage <String>] [-Force <SwitchParameter>] [-TargetDialplan <String>] [-TargetVoicePolicy <String>] [-WhatIf [<SwitchParameter>]]

## Exemples

## EXEMPLE 1

Cet exemple définit le numéro composé pour la configuration de test vocale TestConfig1 à 14255551212. Il s’agit du numéro qui sera contrôlé par rapport à la stratégie de voix et à l’itinéraire, afin de s’assurer que la normalisation s’effectue comme prévu, mais aussi que ce sont les itinéraires et les plans de numérotation corrects qui sont appliqués.

    Set-CsVoiceTestConfiguration -Identity TestConfig1 -DialedNumber 14255551212

## EXEMPLE 2

Cet exemple modifie les paramètres de la configuration de test vocal TestConfig1. La commande définit l’élément TargetDialplan en fonction du profil d’emplacement (plan de numérotation) pour site:Redmond1. Une modification du plan de numérotation pouvant impliquer une modification des règles de normalisation, l’élément ExpectedTranslationNumber a également été modifié pour obtenir la fonction attendue des règles de normalisation pour ce plan de numérotation.

    Set-CsVoiceTestConfiguration -Identity TestConfig1 -TargetDialplan site:Redmond1 -ExpectedTranslatedNumber "+912065551212"

## Description détaillée

Avant d’implémenter les itinéraires de communications vocales et les stratégies de voix, il est préférable de les tester sur divers numéros de téléphone afin de s’assurer que les résultats sont ceux que vous attendez. Pour ce faire, vous pouvez modifier des scénarios de test avec cette applet de commande.

L’applet de commande **Set-CsVoiceTestConfiguration** modifie l’itinéraire de communication vocale, l’utilisation, le profil d’emplacement (plan de numérotation) et la stratégie de voix par rapport auxquels le numéro de téléphone spécifié doit être testé. Toutes ces informations peuvent être définies et récupérées grâce à d’autres applets de commande définies dans les descriptions de paramètre de cette rubrique.

Les configurations modifiées par cette applet de commande sont testées via l’applet de commande **Test-CsVoiceTestConfiguration**.

Personnes autorisées à exécuter cette applet de commande : Par défaut, les membres des groupes qui suivent sont autorisés à exécuter localement l’applet de commande **Set-CsVoiceTestConfiguration** : RTCUniversalServerAdmins. Pour retourner une liste de tous les rôles RBAC (Contrôle d’accès basé sur un rôle) auxquels cette applet de commande a été affectée (y compris les rôles RBAC personnalisés créés par vos soins), exécutez la commande suivante à l’invite Windows PowerShell :

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsVoiceTestConfiguration"}

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
<td><p><em>DialedNumber</em></p></td>
<td><p>Facultatif</p></td>
<td><p>String</p></td>
<td><p>Numéro de téléphone que vous souhaitez utiliser pour tester les stratégies, les utilisations, etc.</p>
<p>Ne doit pas comporter plus de 512 caractères.</p></td>
</tr>
<tr class="odd">
<td><p><em>ExpectedRoute</em></p></td>
<td><p>Facultatif</p></td>
<td><p>String</p></td>
<td><p>Nom de l’itinéraire de communications vocales qui doit être utilisé lors du test de configuration. Si un autre itinéraire est appliqué avec le plan de numérotation (profil d’emplacement) cible et la stratégie de voix, le test échouera. Vous pouvez récupérer les itinéraires de communications vocales disponibles en appelant l’applet de commande <strong>Get-CsVoiceRoute</strong>.</p>
<p>Ne doit pas comporter plus de 256 caractères.</p></td>
</tr>
<tr class="even">
<td><p><em>ExpectedTranslatedNumber</em></p></td>
<td><p>Facultatif</p></td>
<td><p>String</p></td>
<td><p>Numéro de téléphone au format souhaité à l’issue de la traduction. Il s’agit de la valeur du paramètre DialedNumber une fois la normalisation effectuée. Si vous exécutez l’applet de commande <strong>Test-CsVoiceTestConfiguration</strong> et que DialedNumber ne génère pas la valeur de ExpectedTranslatedNumber, le test échouera.</p>
<p>Ne doit pas comporter plus de 512 caractères.</p></td>
</tr>
<tr class="odd">
<td><p><em>ExpectedUsage</em></p></td>
<td><p>Facultatif</p></td>
<td><p>String</p></td>
<td><p>Nom de l’utilisation du réseau PSTN prévue pour le test de configuration. Si un autre réseau PSTN est utilisé avec le plan de numérotation (profil d’emplacement) et la stratégie de voix cibles, le test échouera. Vous pouvez récupérer les utilisations disponibles en appelant l’applet de commande <strong>Get-CsPstnUsage</strong>.</p>
<p>Ne doit pas comporter plus de 256 caractères.</p></td>
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
<td><p>XdsGlobalRelativeIdentity</p></td>
<td><p>Chaîne qui identifie de manière unique le scénario de test que vous souhaitez modifier.</p>
<p>La valeur de ce paramètre n’inclut pas l’étendue, car cet objet ne peut être créé que dans l’étendue globale. Par conséquent, seul un nom unique est requis.</p></td>
</tr>
<tr class="even">
<td><p><em>Instance</em></p></td>
<td><p>Facultatif</p></td>
<td><p>TestConfiguration</p></td>
<td><p>Objet de type Microsoft.Rtc.Management.WritableConfig.Policy.Voice.TestConfiguration qui contient la configuration de test vocal existante, ainsi que les changements que vous souhaitez apporter à cette configuration. Ce type d’objet peut être récupéré par l’appel de l’applet de commande <strong>Get-CsVoiceTestConfiguraton</strong>.</p></td>
</tr>
<tr class="odd">
<td><p><em>TargetDialplan</em></p></td>
<td><p>Facultatif</p></td>
<td><p>String</p></td>
<td><p>Identité du plan de numérotation à utiliser pour ce test. Les plans de numérotation peuvent être récupérés en appelant l’applet de commande <strong>Get-CsDialPlan</strong>.</p>
<p>Ne doit pas comporter plus de 40 caractères.</p></td>
</tr>
<tr class="even">
<td><p><em>TargetVoicePolicy</em></p></td>
<td><p>Facultatif</p></td>
<td><p>String</p></td>
<td><p>Identité de la stratégie de voix sur laquelle ce test est exécuté. Les stratégies de voix peuvent être récupérées en appelant l’applet de commande <strong>Get-CsVoicePolicy</strong>.</p>
<p>Ne doit pas comporter plus de 40 caractères.</p></td>
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

Objet Microsoft.Rtc.Management.WritableConfig.Policy.Voice.TestConfiguration. Accepte l’entrée redirigée pour les objets de configuration vocale de test.

## Types de retours

Cette applet de commande retourne un objet de type Microsoft.Rtc.Management.WritableConfig.Policy.Voice.TestConfiguration.

## Voir aussi

#### Autres ressources

[New-CsVoiceTestConfiguration](new-csvoicetestconfiguration.md)  
[Remove-CsVoiceTestConfiguration](remove-csvoicetestconfiguration.md)  
[Get-CsVoiceTestConfiguration](get-csvoicetestconfiguration.md)  
[Test-CsVoiceTestConfiguration](test-csvoicetestconfiguration.md)  
[Get-CsVoiceRoute](get-csvoiceroute.md)  
[Get-CsPstnUsage](get-cspstnusage.md)  
[Get-CsDialPlan](get-csdialplan.md)  
[Get-CsVoicePolicy](get-csvoicepolicy.md)

