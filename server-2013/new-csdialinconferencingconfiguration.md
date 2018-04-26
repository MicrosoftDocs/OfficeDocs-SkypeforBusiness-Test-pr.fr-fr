---
title: New-CsDialInConferencingConfiguration
TOCTitle: New-CsDialInConferencingConfiguration
ms:assetid: ac0b6e22-3883-4884-aa94-18f4029c7f1e
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Gg412816(v=OCS.15)
ms:contentKeyID: 49298527
ms.date: 05/20/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsDialInConferencingConfiguration

 

_**Dernière rubrique modifiée :** 2015-03-09_

Crée une collection de paramètres de configuration pour la conférence rendez-vous. Ces paramètres déterminent comment Lync Server doit répondre si les utilisateurs rejoignent ou quittent la conférence rendez-vous. Sont retournées en particulier les informations qui indiquent si les participants sont tenus ou non d’enregistrer leur nom en rejoignant la conférence et comment (ou si) le système doit annoncer qu’une personne a rejoint la conférence ou l’a quittée. Cette applet de commande est une nouveauté de Lync Server 2010.

## Syntaxe

    New-CsDialInConferencingConfiguration -Identity <XdsIdentity> [-Confirm [<SwitchParameter>]] [-EnableNameRecording <$true | $false>] [-EntryExitAnnouncementsEnabledByDefault <$true | $false>] [-EntryExitAnnouncementsType <UseNames | ToneOnly>] [-Force <SwitchParameter>] [-InMemory <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## Exemples

## EXEMPLE 1

La commande indiquée à l’exemple 1 crée une collection de paramètres de configuration de conférence rendez-vous appliqués au site Redmond. De plus, le paramètre facultatif EnableNameRecording est inclus afin de configurer la propriété EnableNameRecording avec la valeur False.

    New-CSDialInConferencingConfiguration -Identity site:Redmond -EnableNameRecording $False

## EXEMPLE 2

Dans l’exemple 2, le paramètre InMemory est utilisé pour créer une collection de paramètres de configuration pour la conférence rendez-vous qui n’existent initialement qu’en mémoire. Pour ce faire, l’exemple appelle d’abord l’applet de commande **New-CSDialInConferencingConfiguration** et le paramètre InMemory pour créer une collection virtuelle de paramètres enregistrés dans la variable $x. (Notez que cette collection a pour identité site:Redmond). Après la création de la collection virtuelle, la ligne 2 sert à modifier la valeur de la propriété EnableNameRecording. Enfin, la ligne 3 de l’exemple appelle l’applet de commande **Set-CSDialInConferencingConfiguration** pour transformer les paramètres de configuration virtuels enregistrés dans la variable $x en une collection réelle de paramètres appliqués au site Redmond.

    $x = New-CSDialInConferencingConfiguration -Identity site:Redmond -InMemory
    $x.EnableNameRecording = $False
    Set-CSDialInConferencingConfiguration -Instance $x

## Description détaillée

Quand les utilisateurs rejoignent (ou quittent) la conférence rendez-vous, Lync Server peut répondre de plusieurs manières. Par exemple, les participants peuvent être invités à enregistrer leur nom avant de se joindre à la conférence. De la même manière, les administrateurs peuvent décider s’ils souhaitent que Lync Server annonce que des participants ont rejoint ou quitté la conférence rendez-vous.

Ces « comportements de participation » sont gérés au moyen des paramètres de configuration de la conférence rendez-vous. Ils peuvent être configurés au niveau de l’étendue globale ou de l’étendue Site. (Les paramètres configurés au niveau du site ont priorité sur les paramètres configurés au niveau global.) Lorsque vous installez Lync Server pour la première fois, les seuls paramètres de configuration de conférence rendez-vous présents sont ceux qui interviennent au niveau de l’étendue globale ; en revanche, vous pouvez créer des paramètres au niveau de l’étendue Site en utilisant l’applet de commande **New-CSDialInConferencingConfiguration**.

Personnes autorisées à exécuter cette applet de commande : Par défaut, les membres des groupes qui suivent sont autorisés à exécuter localement l’applet de commande **New-CsDialInConferencingConfiguration** : RTCUniversalServerAdmins. Pour retourner une liste de tous les rôles RBAC (Contrôle d’accès basé sur un rôle) auxquels cette applet de commande a été affectée (y compris les rôles RBAC personnalisés créés par vos soins), exécutez la commande suivante à l’invite Windows PowerShell :

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsDialInConferencingConfiguration"}

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
<td><p>Renseigne sur l’identité des paramètres de configuration de conférence rendez-vous à créer. Étant donné que ces paramètres ne peuvent être créés qu’au niveau de l’étendue Site, utilisez une syntaxe similaire à ce qui suit, avec le préfixe site: suivi du nom du site : -Identity site:Redmond.</p>
<p>Notez qu’il ne peut y avoir qu’un groupe de paramètres de configuration de conférence rendez-vous par site. La commande fournie à titre d’exemple échouera si la collection de paramètres avec l’identité site:Redmond existe déjà.</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>Facultatif</p></td>
<td><p>SwitchParameter</p></td>
<td><p>Vous demande confirmation avant d’exécuter la commande.</p></td>
</tr>
<tr class="odd">
<td><p><em>EnableNameRecording</em></p></td>
<td><p>Facultatif</p></td>
<td><p>Booléen</p></td>
<td><p>Détermine si les utilisateurs doivent être invités à enregistrer leur nom ou pas avant de rejoindre la conférence. Définissez ce paramètre sur True ($True) pour exiger l’enregistrement du nom. Utilisez la valeur False ($False) pour ignorer l’enregistrement du nom. La valeur par défaut est True.</p></td>
</tr>
<tr class="even">
<td><p><em>EntryExitAnnouncementsEnabledByDefault</em></p></td>
<td><p>Facultatif</p></td>
<td><p>Booléen</p></td>
<td><p>S’il est configuré avec la valeur True, une annonce sera diffusée chaque fois qu’un participant rejoint ou quitte la conférence. S’il est configuré avec la valeur False (la valeur par défaut), il n’y a pas d’annonce quand un participant rejoint ou quitte la conférence.</p></td>
</tr>
<tr class="odd">
<td><p><em>EntryExitAnnouncementsType</em></p></td>
<td><p>Facultatif</p></td>
<td><p>EntryExitAnnouncementsType</p></td>
<td><p>Indique ce que doit faire le système chaque fois qu’un participant rejoint ou quitte la conférence. Les valeurs valides sont les suivantes :</p>
<p>UseNames. Le nom de la personne est annoncé lorsqu’elle rejoint ou quitte une conférence (par exemple « Ken Myer quitte la conférence »).</p>
<p>ToneOnly. Une tonalité se fait entendre chaque fois qu’un participant rejoint ou quitte la conférence.</p>
<p>La valeur par défaut est UseNames. Notez que les annonces ne sont diffusées que si la propriété EntryExitAnnouncementsEnabledByDefault est définie sur True.</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>Facultatif</p></td>
<td><p>SwitchParameter</p></td>
<td><p>Supprime l’affichage de tous les messages d’erreur récupérable susceptibles d’apparaître lors de l’exécution de la commande.</p></td>
</tr>
<tr class="odd">
<td><p><em>InMemory</em></p></td>
<td><p>Facultatif</p></td>
<td><p>SwitchParameter</p></td>
<td><p>Crée une référence d’objet sans valider l’objet comme une modification définitive. Si vous affectez à une variable la sortie de cette cmdlet appelée avec ce paramètre, vous pouvez apporter des modifications aux propriétés de la référence d’objet, puis les valider en appelant la cmdlet Set- correspondante.</p></td>
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

Aucun. L’applet de commande **New-CsDialInConferencingConfiguration** n’accepte pas les données redirigées.

## Types de retours

Crée de nouvelles instances de l’objet Microsoft.Rtc.Management.WritableConfig.Settings.DialInConferencingSettings.DialInConferencingConfiguration.

## Voir aussi

#### Autres ressources

[Get-CsDialInConferencingConfiguration](get-csdialinconferencingconfiguration.md)  
[Remove-CsDialInConferencingConfiguration](remove-csdialinconferencingconfiguration.md)  
[Set-CsDialInConferencingConfiguration](set-csdialinconferencingconfiguration.md)

