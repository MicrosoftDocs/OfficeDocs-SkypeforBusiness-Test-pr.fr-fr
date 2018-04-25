---
title: Remove-CsNetworkInterRegionRoute
TOCTitle: Remove-CsNetworkInterRegionRoute
ms:assetid: 91948c03-2bcb-4e25-b0b6-23827e85bbb3
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Gg398743(v=OCS.15)
ms:contentKeyID: 49298072
ms.date: 05/20/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsNetworkInterRegionRoute

 

_**Dernière rubrique modifiée :** 2015-03-09_

Supprime un itinéraire qui connecte des régions réseau dans une configuration de contrôle d’admission des appels. Cette applet de commande est une nouveauté de Lync Server 2010.

## Syntaxe

    Remove-CsNetworkInterRegionRoute -Identity <XdsGlobalRelativeIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## Exemples

## EXEMPLE 1

L’exemple 1 supprime l’itinéraire dont l’identité est NA\_APAC\_Route.

    Remove-CsNetworkInterRegionRoute -Identity NA_APAC_Route

## EXEMPLE 2

L’exemple 2 supprime tous les itinéraires de région incluant la région NorthAmerica. La première partie de la commande appelle l’applet de commande **Get-CsNetworkInterRegionRoute**. Cette applet de commande, appelée sans paramètres, récupère tous les itinéraires de région. Cette collection d’itinéraires est ensuite redirigée vers l’applet de commande **Where-Object**. L’applet de commande **Where-Object** limite la collection aux itinéraires dont NorthAmerica est défini comme l’une des régions de l’itinéraire. Pour ce faire, elle vérifie si l’itinéraire dispose d’une valeur NetworkRegionID1 égale (-eq) à NorthAmerica ou (-or) une valeur NetworkRegionID2 égale à NorthAmerica. Une fois que la collection ne contient plus que les itinéraires incluant la région NorthAmerica, nous redirigeons la collection sur l’applet de commande **Remove-CsNetworkInterRegionRoute**, qui supprime chacun des itinéraires.

    Get-CsNetworkInterRegionRoute | Where-Object {$_.NetworkRegionID1 -eq "NorthAmerica" -or $_.NetworkRegionID2 -eq "NorthAmerica"} | Remove-CsNetworkInterRegionRoute

## Description détaillée

Chaque région au sein d’une configuration de contrôle d’admission des appels doit être dotée d’un moyen d’accéder à chacune des autres régions. Alors que les liens de région définissent des restrictions de bande passante sur les connexions entre les régions et qu’ils représentent des liens physiques, un itinéraire détermine le chemin lié que la connexion traverse d’une région à une autre. Cette applet de commande supprime l’une des ses associations d’itinéraires.

Personnes autorisées à exécuter cette applet de commande : Par défaut, les membres des groupes qui suivent sont autorisés à exécuter localement l’applet de commande **Remove-CsNetworkInterRegionRoute** : RTCUniversalServerAdmins. Pour retourner une liste de tous les rôles RBAC (Contrôle d’accès basé sur un rôle) auxquels cette applet de commande a été affectée (y compris les rôles RBAC personnalisés créés par vos soins), exécutez la commande suivante à l’invite Windows PowerShell :

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsNetworkInterRegionRoute"}

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
<td><p>Microsoft.Rtc.Management.Xds.XdsGlobalRelativeIdentity</p></td>
<td><p>Identificateur unique de l’itinéraire de la région de réseau que vous souhaitez supprimer. Les itinéraires de région de réseau étant créés au niveau de l’étendue globale seulement, il n’est pas nécessaire de spécifier une étendue pour cet identificateur. Il contient en effet une chaîne au nom unique permettant d’identifier l’itinéraire.</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>Facultatif</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Vous demande confirmation avant d’exécuter la commande.</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>Facultatif</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Supprime les invites de confirmation qui s’affichent avant d’effectuer des modifications.</p></td>
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

Objet Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.InterNetworkRegionRouteType. Accepte l’entrée redirigée pour les objets d’itinéraire entre les zones réseau.

## Types de retours

Cette applet de commande ne retourne aucune valeur. Elle supprime un objet de type Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.InterNetworkRegionRouteType.

## Voir aussi

#### Autres ressources

[New-CsNetworkInterRegionRoute](new-csnetworkinterregionroute.md)  
[Set-CsNetworkInterRegionRoute](set-csnetworkinterregionroute.md)  
[Get-CsNetworkInterRegionRoute](get-csnetworkinterregionroute.md)

