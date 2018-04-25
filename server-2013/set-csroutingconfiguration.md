---
title: Set-CsRoutingConfiguration
TOCTitle: Set-CsRoutingConfiguration
ms:assetid: ab69c6e8-262a-4ecb-b1af-513383c494fe
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Gg412811(v=OCS.15)
ms:contentKeyID: 49298486
ms.date: 05/20/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsRoutingConfiguration

 

_**Dernière rubrique modifiée :** 2015-03-09_

Modifie la liste des itinéraires de communications vocales. Cette applet de commande est une nouveauté de Lync Server 2010.

## Syntaxe

    Set-CsRoutingConfiguration [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Set-CsRoutingConfiguration [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Confirm [<SwitchParameter>]] [-EnableLocationBasedRouting <$true | $false>] [-Force <SwitchParameter>] [-Route <PSListModifier>] [-WhatIf [<SwitchParameter>]]

## Exemples

## EXEMPLE 1

Plusieurs étapes sont nécessaires à la modification d’un itinéraire de communications vocales dans une configuration du routage. Dans cet exemple, nous récupérons d’abord l’objet de configuration du routage en appelant l’applet de commande **Get-CsRoutingConfiguration**. Nous affectons ensuite l’objet récupéré (il y en a un seul) à la variable $a.

Sur la ligne 2 de ce même exemple, nous récupérons le contenu de la propriété Route à partir de la variable $a, soit un ensemble d’objets d’itinéraire de communications vocales. Nous redirigeons alors cet ensemble vers l’applet de commande **Where-Object** où nous y effectuons une recherche pour localiser tous les objets d’itinéraire de communications vocales dont le nom correspond à la chaîne LocalRoute. Nous affectons cet objet à la variable $b.

Ensuite, nous modifions l’objet d’itinéraire de communications vocales LocalRoute en attribuant la valeur $False à la propriété SuppressCallerId. En mettant à jour cet objet, nous avons également mis à jour l’objet contenu dans la variable $a. Néanmoins, l’objet en question est toujours conservé en mémoire. La dernière étape consiste à enregistrer nos modifications en transmettant la variable $a au paramètre Instance de l’applet de commande **Set-CsRoutingConfiguration**.

Il ne s’agit pas de la méthode recommandée pour modifier la configuration du routage. Pour modifier la configuration du routage, modifiez simplement les itinéraires de communications vocales à l’aide de l’applet de commande **Set-CsVoiceRoute**, comme indiqué ici :

Set-CsVoiceRoute -Identity LocalRoute -SuppressCallerId $False

Cette ligne accomplira la même tâche que celle décrite dans l’exemple 1.

    $a = Get-CsRoutingConfiguration
    $b = $a.Route | Where-Object {$_.Name -match "LocalRoute"}
    $b.SuppressCallerId = $False
    Set-CsRoutingConfiguration -Instance $a

## Description détaillée

Les itinéraires de communications vocales contiennent des instructions qui indiquent à Lync Server comment router les appels des utilisateurs Voix Entreprise vers des numéros de téléphone sur le réseau téléphonique commuté (PSTN) ou un autocommutateur privé (PBX). Avec cette applet de commande, vous pouvez modifier les paramètres de tout itinéraire de communications vocales défini dans un déploiement de Lync Server.

L’utilisation de cette applet de commande n’est pas recommandée. Pour modifier les configurations du routage, modifiez les itinéraires de communications vocales individuels en appelant l’applet de commande **Set-CsVoiceRoute**.

Personnes autorisées à exécuter cette applet de commande : Par défaut, les membres des groupes qui suivent sont autorisés à exécuter localement l’applet de commande **Set-CsRoutingConfiguration** : RTCUniversalServerAdmins. Pour retourner une liste de tous les rôles RBAC (Contrôle d’accès basé sur un rôle) auxquels cette applet de commande a été affectée (y compris les rôles RBAC personnalisés créés par vos soins), exécutez la commande suivante à l’invite Windows PowerShell :

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsRoutingConfiguration"}

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
<td><p><em>EnableLocationBasedRouting</em></p></td>
<td><p>Facultatif</p></td>
<td><p>Booléen</p></td>
<td><p>Quand la valeur est True, le routage des communications vocales est géré en tenant compte à la fois de l’emplacement de l’utilisateur qui émet l’appel et de celui de l’utilisateur qui le reçoit. La valeur par défaut est False.</p></td>
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
<td><p>Étendue de la configuration du routage. Cette valeur doit être Global.</p></td>
</tr>
<tr class="odd">
<td><p><em>Instance</em></p></td>
<td><p>Facultatif</p></td>
<td><p>PstnRoutingSettings</p></td>
<td><p>Objet de configuration du routage (Microsoft.Rtc.Management.WritablConfig.Policy.Voice.PstnRoutingSettings). Il est possible d’extraire un objet de ce type en appelant l’applet de commande <strong>Get-CsRoutingConfiguration</strong>.</p></td>
</tr>
<tr class="even">
<td><p><em>Route</em></p></td>
<td><p>Facultatif</p></td>
<td><p>PSListModifier</p></td>
<td><p>Liste de tous les itinéraires de communications vocales (objets Microsoft.Rtc.Management.WritableConfig.Policy.Voice.Route) définis pour le déploiement Lync Server.</p>
<p>Pour modifier des objets d’itinéraire de communications vocales, utilisez l’applet de commande <strong>Set-CsVoiceRoute</strong>. C’est le moyen que nous recommandons pour modifier des itinéraires dans cette liste.</p></td>
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

Objet Microsoft.Rtc.WritableConfig.Management.Policy.Voice.PSTNRoutingSettings. Accepte l’entrée redirigée pour un objet de configuration de routage.

## Types de retours

L’applet de commande **Set-CsRoutingConfiguration** ne retourne pas de valeurs ni d’objets. Au lieu de cela, l’applet de commande configure des instances de l’objet Microsoft.Rtc.Management.WritableConfig.Policy.Voice.PstnRoutingSettings.

## Voir aussi

#### Autres ressources

[New-CsRoutingConfiguration](new-csroutingconfiguration.md)  
[Remove-CsRoutingConfiguration](remove-csroutingconfiguration.md)  
[Get-CsRoutingConfiguration](get-csroutingconfiguration.md)  
[Set-CsVoiceRoute](set-csvoiceroute.md)  
[Get-CsVoiceRoute](get-csvoiceroute.md)

