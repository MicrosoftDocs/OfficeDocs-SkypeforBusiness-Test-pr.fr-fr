---
title: Set-CsVoiceConfiguration
TOCTitle: Set-CsVoiceConfiguration
ms:assetid: dbab35ac-9a55-41d2-a726-9a26b2ff8e85
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Gg398967(v=OCS.15)
ms:contentKeyID: 49299060
ms.date: 05/20/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsVoiceConfiguration

 

_**Dernière rubrique modifiée :** 2015-03-09_

Modifie une liste de configurations de test vocales. Cette applet de commande est une nouveauté de Lync Server 2010.

## Syntaxe

    Set-CsVoiceConfiguration [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Set-CsVoiceConfiguration [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-VoiceTestConfigurations <PSListModifier>] [-WhatIf [<SwitchParameter>]]

## Exemples

## EXEMPLE 1

Plusieurs étapes sont nécessaires pour modifier une configuration de test vocale dans une configuration vocale. Dans cet exemple, nous récupérons d’abord l’objet de configuration vocale en appelant l’applet de commande **Get-CsVoiceConfiguration**. Nous affectons ensuite l’objet récupéré (il y en a un seul) à la variable $a.

À la ligne 2 de cet exemple, nous récupérons le contenu de la propriété VoiceTestConfigurations, qui représente une collection d’objets de configuration de test vocale, à partir de la variable $a. Nous redirigeons ensuite cette collection vers l’applet de commande **Where-Object**, puis recherchons dans la collection l’objet de configuration de test vocale dont le nom est égal à la chaîne TestConfig2. Nous affectons cet objet à la variable $b.

Ensuite, nous modifions l’objet de configuration de test vocale TestConfig2 en affectant de nouvelles valeurs aux propriétés DialedNumber et ExpectedTranslatedNumber. En mettant à jour cet objet, nous avons également mis à jour l’objet contenu dans la variable $a. Néanmoins, l’objet en question est toujours conservé en mémoire. La dernière étape consiste à enregistrer ces modifications en transmettant la variable $a au paramètre Instance de l’applet de commande **Set-CsVoiceConfiguration**.

Il ne s’agit pas de la méthode recommandée pour modifier une configuration vocale. Pour modifier une configuration vocale, modifiez simplement les configurations de test vocales individuelles à l’aide de l’applet de commande **Set-CsVoiceTestConfiguration** comme démontré ci-après :

Set-CsVoiceTestConfiguration -Identity TestConfig2 -DialedNumber 5551212 -ExpectedTranslatedNumber +5551212

Cette ligne accomplira la même tâche que celle décrite dans l’exemple 1.

    $a = Get-CsVoiceConfiguration
    $b = $a.VoiceTestConfigurations | Where-Object {$_.Name -eq "TestConfig2"}
    $b.DialedNumber = "5551212"
    $b.ExpectedTranslatedNumber = "+5551212"
    Set-CsVoiceConfiguration -Instance $a

## Description détaillée

Les configurations de test vocales servent à tester un numéro de téléphone par rapport à une stratégie de voix, un itinéraire et un plan de numérotation précis. Cette applet de commande permet de modifier des configurations de test vocales à partir d’une liste contenant toutes les configurations de test vocales employées dans le cadre d’un déploiement Lync Server.

Cette applet de commande modifie un objet de type VoiceConfiguration. Cet objet est simplement un objet conteneur pour les configurations de test vocales. Par conséquent, l’utilisation de cette applet de commande n’est pas recommandée. Pour modifier des configurations vocales, modifiez les configurations de test vocales individuelles en appelant l’applet de commande **Set-CsVoiceTestConfiguration**.

Personnes autorisées à exécuter cette applet de commande : Par défaut, les membres des groupes qui suivent sont autorisés à exécuter localement l’applet de commande **Set-CsVoiceConfiguration** : RTCUniversalServerAdmins. Pour retourner une liste de tous les rôles RBAC (Contrôle d’accès basé sur un rôle) auxquels cette applet de commande a été affectée (y compris les rôles RBAC personnalisés créés par vos soins), exécutez la commande suivante à l’invite Windows PowerShell :

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsVoiceConfiguration"}

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
<td><p><em>Force</em></p></td>
<td><p>Facultatif</p></td>
<td><p>SwitchParameter</p></td>
<td><p>Supprime les invites de confirmation qui s’affichent avant d’effectuer des modifications.</p></td>
</tr>
<tr class="odd">
<td><p><em>Identity</em></p></td>
<td><p>Facultatif</p></td>
<td><p>XdsIdentity</p></td>
<td><p>Étendue de cet objet. La seule valeur possible pour ce paramètre est Global.</p></td>
</tr>
<tr class="even">
<td><p><em>Instance</em></p></td>
<td><p>Facultatif</p></td>
<td><p>VoiceConfiguration</p></td>
<td><p>Référence à un objet de configuration vocale (Microsoft.Rtc.Management.WritableConfig.Policy.Voice.VoiceConfiguration). Ce type d’objet peut être récupéré par l’applet de commande <strong>Get-CsVoiceConfiguration</strong>.</p></td>
</tr>
<tr class="odd">
<td><p><em>VoiceTestConfigurations</em></p></td>
<td><p>Facultatif</p></td>
<td><p>PSListModifier</p></td>
<td><p>Liste de toutes les configurations de test vocales (objets Microsoft.Rtc.Management.WritableConfig.Policy.Voice.TestConfiguration) définies pour le déploiement Lync Server.</p>
<p>Pour modifier des objets individuels de configuration de test vocale, utilisez de préférence l’applet de commande <strong>Set-CsVoiceTestConfiguration</strong>. C’est le moyen que nous recommandons pour modifier des configurations dans cette liste.</p></td>
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

Objet Microsoft.Rtc.Management.WritableConfig.Policy.Voice.VoiceConfiguration. L’applet de commande **Set-CsVoiceConfiguration** accepte l’entrée redirigée pour un objet de configuration vocale.

## Types de retours

L’applet de commande **Set-CsVoiceConfiguration** ne retourne ni valeur, ni objet. Au lieu de cela, l’applet de commande configure des instances de l’objet Microsoft.Rtc.Management.WritableConfig.Policy.Voice.VoiceConfiguration.

## Voir aussi

#### Autres ressources

[Remove-CsVoiceConfiguration](remove-csvoiceconfiguration.md)  
[Get-CsVoiceConfiguration](get-csvoiceconfiguration.md)  
[New-CsVoiceTestConfiguration](new-csvoicetestconfiguration.md)  
[Set-CsVoiceTestConfiguration](set-csvoicetestconfiguration.md)  
[Get-CsVoiceTestConfiguration](get-csvoicetestconfiguration.md)

