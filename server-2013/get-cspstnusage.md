---
title: Get-CsPstnUsage
TOCTitle: Get-CsPstnUsage
ms:assetid: 9dc82b88-303b-4678-8298-0dbc769f6781
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Gg412734(v=OCS.15)
ms:contentKeyID: 49298368
ms.date: 05/20/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsPstnUsage

 

_**Dernière rubrique modifiée :** 2015-03-09_

Retourne des informations sur les enregistrements de l’utilisation du réseau téléphonique commuté (RTC) utilisés au sein de votre organisation. Cette applet de commande est une nouveauté de Lync Server 2010.

## Syntaxe

    Get-CsPstnUsage [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Get-CsPstnUsage [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-LocalStore <SwitchParameter>]

## Exemples

## EXEMPLE 1

Cette commande renvoie la liste des utilisations du réseau téléphonique commuté globales disponibles dans votre organisation.

    Get-CsPstnUsage

## EXEMPLE 2

La commande affichée dans cet exemple renvoie une liste de toutes les utilisations définies du réseau téléphonique commuté, avec une seule utilisation répertoriée sur chaque ligne du résultat produit. L’appel de l’applet de commande **Get-CsPstnUsage** renvoie l’identité et la liste des utilisations. Si la liste des utilisations contient plus de trois ou quatre entrées, elle sera abrégée de la manière suivante dans la sortie :

Utilisation : {Internal, Local, Long Distance, International...}

Utilisez la commande de cet exemple pour afficher uniquement une liste des utilisations. Le résultat sera similaire à ceci :

Internal

Local

Long Distance

International

Restricted

    (Get-CsPstnUsage).Usage

## EXEMPLE 3

Cette commande retourne tous les noms des utilisations du réseau téléphonique commuté qui contiennent la chaîne tern. Par exemple, cette commande renverra les utilisations « Internal » et « International » mais pas l’utilisation « Local » ou « Long Distance ».

La première partie de la commande est l’applet de commande **Get-CsPstnUsage** entre parenthèses, ce qui signifie que la première opération réalisée est la récupération de l’ensemble des utilisations du réseau téléphonique commuté. La propriété .Usage renvoie uniquement les informations des utilisations du réseau téléphonique commuté et non l’identité. Cette liste d’utilisations est ensuite redirigée vers l’applet de commande **ForEach-Object** qui examine une à une les chaînes d’utilisation. L’instruction If compare la chaîne d’utilisation actuelle à la chaîne \*tern\* (les \* sont des caractères génériques) et affiche toutes les occurrences conformes à ce modèle.

    (Get-CsPstnUsage).Usage | ForEach-Object {if ($_ -like "*tern*") {$_}}

## Description détaillée

Les utilisations du réseau téléphonique commuté sont des valeurs de chaîne utilisées pour l’autorisation d’appel. Une utilisation du réseau téléphonique commuté lie une stratégie de voix à un itinéraire. L’applet de commande **Get-CsPstnUsage** récupère la liste de toutes les utilisations du réseau téléphonique commuté disponibles dans votre organisation.

Personnes autorisées à exécuter cette applet de commande : Par défaut, les membres des groupes qui suivent sont autorisés à exécuter localement l’applet de commande **Get-CsPstnUsage** : RTCUniversalUserAdmins, RTCUniversalServerAdmins. Pour retourner une liste de tous les rôles RBAC (Contrôle d’accès basé sur un rôle) auxquels cette applet de commande a été affectée (y compris les rôles RBAC personnalisés créés par vos soins), exécutez la commande suivante à l’invite Windows PowerShell :

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsPstnUsage"}

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
<td><p>Le paramètre Filter vous permet uniquement d’extraire les utilisations du réseau téléphonique commuté dont l’identité correspond à une chaîne à caractère générique donnée. Néanmoins, la seule identité disponible pour les utilisations du réseau téléphonique commuté est Global. Ce paramètre n’a donc aucune utilité pour cette applet de commande.</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>Facultatif</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>Niveau auquel ces paramètres sont appliqués. La seule identité applicable aux utilisations du réseau téléphonique commuté est Global.</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>Facultatif</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Récupère les informations d’utilisation du réseau téléphonique commuté à partir du magasin de données local au lieu du magasin central de gestion.</p></td>
</tr>
</tbody>
</table>


## Types d’entrées

Aucun.

## Types de retours

L’applet de commande **Get-CsPstnUsage** retourne des instances de l’objet Microsoft.Rtc.Management.WritableConfig.Policy.Voice.PSTNUsages.

## Voir aussi

#### Autres ressources

[Set-CsPstnUsage](set-cspstnusage.md)  
[Get-CsVoicePolicy](get-csvoicepolicy.md)  
[Get-CsVoiceRoute](get-csvoiceroute.md)

