---
title: Get-CsNetworkInterRegionRoute
TOCTitle: Get-CsNetworkInterRegionRoute
ms:assetid: 31c38d92-1cef-40fe-bd04-26e5b373703e
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Gg425817(v=OCS.15)
ms:contentKeyID: 49296798
ms.date: 05/20/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsNetworkInterRegionRoute

 

_**Dernière rubrique modifiée :** 2015-03-09_

Extrait un ou plusieurs routages qui connectent des zones réseau au sein d’une configuration de contrôle d’admission des appels. Cette applet de commande est une nouveauté de Lync Server 2010.

## Syntaxe

    Get-CsNetworkInterRegionRoute [-Identity <XdsGlobalRelativeIdentity>] <COMMON PARAMETERS>

    Get-CsNetworkInterRegionRoute [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-LocalStore <SwitchParameter>]

## Exemples

## EXEMPLE 1

L’exemple 1 récupère l’itinéraire dont la propriété Identity est NA\_APAC\_Route.

    Get-CsNetworkInterRegionRoute -Identity NA_APAC_Route

## EXEMPLE 2

Dans l’exemple 2, nous utilisons le paramètre Filter pour récupérer tous les itinéraires dont la valeur de propriété Identity contient la chaîne APAC quelque part.

    Get-CsNetworkInterRegionRoute -Filter *APAC*

## EXEMPLE 3

Cet exemple récupère tous les itinéraires de zones qui utilisent la liaison de zones réseau NA\_EMEA. La commande commence par appeler l’applet de commande **Get-CsNetworkInterRegionRoute**. L’appel à cette applet de commande sans paramètre récupère tous les itinéraires définis pour la configuration de contrôle d’admission des appels. Cette collection d’itinéraires est ensuite redirigée vers l’applet de commande **Where-Object**. **Where-Object** prend la collection et récupère tous les éléments pour lesquels la valeur NA\_EMEA apparaît dans leur liste NetworkRegionLinks.

    Get-CsNetworkInterRegionRoute | Where-Object {$_.NetworkRegionLinks -eq "NA_EMEA"}

## EXEMPLE 4

L’exemple 4 récupère tous les routages de zones qui incluent la zone NorthAmerica. La première partie de la commande est un appel à l’applet de commande **Get-CsNetworkInterRegionRoute**. Cette applet de commande, appelée sans paramètre, extrait tous les routages de zones. Cette collection de routages est ensuite redirigée vers l’applet de commande **Where-Object**. L’applet de commande **Where-Object** limite la collection aux routages pour lesquels NorthAmerica est défini comme l’une des régions du routage. Pour cela, elle vérifie si le routage présente une valeur NetworkRegionID1 égale à (-eq) NorthAmerica ou (-or) une valeur NetworkRegionID2 égale à NorthAmerica.

    Get-CsNetworkInterRegionRoute | Where-Object {$_.NetworkRegionID1 -eq "NorthAmerica" -or $_.NetworkRegionID2 -eq "NorthAmerica"}

## Description détaillée

Chaque zone d’une configuration de contrôle d’admission des appels doit pouvoir accéder à toutes les autres zones. Alors que les liens de région définissent des restrictions de bande passante sur les connexions entre les régions et qu’ils représentent des liens physiques, un routage détermine le chemin lié que la connexion traverse d’une région à une autre. Cette applet de commande récupère des informations sur ces associations de routages.

Personnes autorisées à exécuter cette applet de commande : Par défaut, les membres des groupes qui suivent sont autorisés à exécuter localement l’applet de commande **Get-CsNetworkInterRegionRoute** : RTCUniversalUserAdmins, RTCUniversalServerAdmins. Pour retourner une liste de tous les rôles RBAC (Contrôle d’accès basé sur un rôle) auxquels cette applet de commande a été affectée (y compris les rôles RBAC personnalisés créés par vos soins), exécutez la commande suivante à l’invite Windows PowerShell :

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsNetworkInterRegionRoute"}

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
<td><p>Chaîne qui vous permet de récupérer des itinéraires d’après la mise en correspondance de la valeur Identity et de la chaîne à caractères génériques transmise comme valeur à ce paramètre.</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>Facultatif</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsGlobalRelativeIdentity</p></td>
<td><p>Identificateur unique de l’itinéraire de zone réseau à récupérer. Les itinéraires de zones réseau ne peuvent être créés qu’au niveau de l’étendue globale. Cet identificateur n’a donc pas besoin de spécifier d’étendue. Il contient en effet une chaîne au nom unique permettant d’identifier un itinéraire en particulier.</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>Facultatif</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Récupère les informations d’itinéraire entre les zones réseau à partir de la réplique locale du magasin central de gestion, au lieu du magasin central de gestion lui-même.</p></td>
</tr>
</tbody>
</table>


## Types d’entrées

Aucun.

## Types de retours

Cette applet de commande retourne un ou plusieurs objets de type Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.InterNetworkRegionRouteType.

## Voir aussi

#### Autres ressources

[New-CsNetworkInterRegionRoute](new-csnetworkinterregionroute.md)  
[Remove-CsNetworkInterRegionRoute](remove-csnetworkinterregionroute.md)  
[Set-CsNetworkInterRegionRoute](set-csnetworkinterregionroute.md)

