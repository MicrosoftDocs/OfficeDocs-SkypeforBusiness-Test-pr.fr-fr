---
title: Get-CsVoiceRoute
TOCTitle: Get-CsVoiceRoute
ms:assetid: 422abb2d-bff3-4b9a-b18c-d8202b01f69b
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Gg425926(v=OCS.15)
ms:contentKeyID: 49297021
ms.date: 05/20/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsVoiceRoute

 

_**Dernière rubrique modifiée :** 2015-03-09_

Renvoie des informations sur les itinéraires de communications vocales configurés pour être utilisés dans une organisation. Cette applet de commande est une nouveauté de Lync Server 2010.

## Syntaxe

    Get-CsVoiceRoute [-Identity <XdsGlobalRelativeIdentity>] <COMMON PARAMETERS>

    Get-CsVoiceRoute [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-LocalStore <SwitchParameter>]

## Exemples

## EXEMPLE 1

Récupère les propriétés de tous les itinéraires de communications vocales définis dans l’organisation.

    Get-CsVoiceRoute

## EXEMPLE 2

Récupère les propriétés de l’itinéraire de communications vocales Route1.

    Get-CsVoiceRoute -Identity Route1

## EXEMPLE 3

Cette commande affiche les paramètres d’itinéraire de communications vocales pour lesquels l’identité contient la chaîne « test » dans la valeur. Pour trouver la chaîne test uniquement à la fin de l’identité, utilisez la valeur \*test. De même, pour trouver la chaîne test uniquement au début de l’identité, spécifiez la valeur test\*.

    Get-CsVoiceRoute -Filter *test*

## EXEMPLE 4

Cette commande récupère tous les itinéraires de communications vocales auxquels aucune passerelle PSTN n’a été attribuée. Tous les itinéraires de communications vocales sont d’abord récupérés à l’aide de l’applet de commande **Get-CsVoiceRoute**. Ces itinéraires de communications vocales sont ensuite redirigés vers l’applet de commande **Where-Object**. **Where-Object** permet de restreindre les résultats de l’opération Get. Dans ce cas, nous analysons chaque itinéraire de communications vocales (ce que représente le $\_) et contrôlons la propriété Count de la propriété PstnGatewayList. Si le nombre de passerelles PSTN est 0, la liste est vide et aucune passerelle n’a été définie pour l’itinéraire.

    Get-CsVoiceRoute | Where-Object {$_.PstnGatewayList.Count -eq 0}

## Description détaillée

Cette applet de commande vous permet de récupérer un ou plusieurs itinéraires de communications vocales existants. Les itinéraires de communications vocales contiennent des instructions qui indiquent à Lync Server comment router les appels des utilisateurs Voix Entreprise vers des numéros de téléphone sur le réseau téléphonique commuté (PSTN) ou un autocommutateur privé (PBX).

Cette applet de commande peut être utilisée pour récupérer des informations sur les itinéraires de communications vocales, comme les passerelles PSTN auxquelles l’itinéraire est associé (le cas échéant), les utilisations PSTN associées à l’itinéraire, le modèle (sous la forme d’une expression régulière) qui identifie les numéros de téléphone auxquels l’itinéraire s’applique, ainsi que les paramètres d’ID d’appelant. L’utilisation PSTN associe l’itinéraire de communications vocales à une stratégie de voix.

Personnes autorisées à exécuter cette applet de commande : Par défaut, les membres des groupes qui suivent sont autorisés à exécuter localement l’applet de commande **Get-CsVoiceRoute** : RTCUniversalUserAdmins, RTCUniversalServerAdmins. Pour retourner une liste de tous les rôles RBAC (Contrôle d’accès basé sur un rôle) auxquels cette applet de commande a été affectée (y compris les rôles RBAC personnalisés créés par vos soins), exécutez la commande suivante à l’invite Windows PowerShell :

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsVoiceRoute"}

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
<td><p>Ce paramètre filtre les résultats de l’opération Get en fonction de la valeur de caractère générique transmise à ce paramètre.</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>Facultatif</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsGlobalRelativeIdentity</p></td>
<td><p>Chaîne qui identifie de façon unique l’itinéraire de communications vocales. Si aucune identité n’est fournie, tous les itinéraires de communications vocales de l’organisation sont retournés.</p>
<p></p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>Facultatif</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Récupère l’itinéraire de communications vocales à partir du réplica local du magasin central de gestion, au lieu du magasin central de gestion lui-même.</p></td>
</tr>
</tbody>
</table>


## Types d’entrées

Aucun.

## Types de retours

Cette applet de commande retourne des instances de l’objet Microsoft.Rtc.Management.WritableConfig.Policy.Voice.Route.

## Voir aussi

#### Autres ressources

[New-CsVoiceRoute](new-csvoiceroute.md)  
[Remove-CsVoiceRoute](remove-csvoiceroute.md)  
[Set-CsVoiceRoute](set-csvoiceroute.md)  
[Test-CsVoiceRoute](test-csvoiceroute.md)

