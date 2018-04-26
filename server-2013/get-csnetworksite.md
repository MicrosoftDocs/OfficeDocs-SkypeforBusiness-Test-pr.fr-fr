---
title: Get-CsNetworkSite
TOCTitle: Get-CsNetworkSite
ms:assetid: 9627869d-101f-4668-bee2-01fce1d84cbd
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Gg398766(v=OCS.15)
ms:contentKeyID: 49298134
ms.date: 05/20/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsNetworkSite

 

_**Dernière rubrique modifiée :** 2015-03-09_

Récupère un ou plusieurs sites réseau définis pour le service Contrôle d’admission des appels ou le système Enhanced 9-1-1 (E9-1-1). Cette applet de commande est une nouveauté de Lync Server 2010.

## Syntaxe

    Get-CsNetworkSite [-Identity <XdsGlobalRelativeIdentity>] <COMMON PARAMETERS>

    Get-CsNetworkSite [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-LocalStore <SwitchParameter>]

## Exemples

## EXEMPLE 1

L’appel de l’applet de commande **Get-CsNetworkSite** sans aucun paramètre retourne tous les sites de réseau configurés pour le contrôle d’admission des appels (CAC) ou le système E9-1-1 au sein du déploiement de Lync Server.

    Get-CsNetworkSite

## EXEMPLE 2

Cette commande récupère le site dont l’identité (et par définition NetworkSiteID) est Redmond.

    Get-CsNetworkSite -Identity Redmond

## EXEMPLE 3

La commande de l’exemple 3 appelle l’applet de commande **Get-CsNetworkSite** avec le paramètre Filter. La valeur du paramètre Filter est NA\*, ce qui signifie que cette commande récupère tous les sites dont l’identité commence par la chaîne NA et est suivie d’un certain nombre de caractères. Les sites retournés sont par exemple NARedmond, NAVancouver ou NAChicago.

    Get-CsNetworkSite -Filter NA*

## EXEMPLE 4

L’exemple 4 utilise deux applets de commande, **Get-CsNetworkSite** et **Where-Object**, pour récupérer tous les sites faisant partie de la région NorthAmerica. La commande commence par appeler l’applet de commande **Get-CsNetworkSite** sans aucun paramètre afin de récupérer tous les sites de réseau. Cette collection de sites est ensuite redirigée vers l’applet de commande **Where-Object** qui filtre la collection, en cherchant tous les sites de la collection pour lesquels la propriété NetworkRegionID est égale (-eq) à NorthAmerica.

    Get-CsNetworkSite | Where-Object {$_.NetworkRegionID -eq "NorthAmerica"}

## Description détaillée

Les sites de réseau sont les bureaux ou emplacements configurés au sein de chaque région d’un contrôle d’admission des appels (Call Admission Control ou CAC) ou encore d’un déploiement E9-1-1. Cette applet de commande récupère les paramètres d’un ou plusieurs sites existants.

Personnes autorisées à exécuter cette applet de commande : Par défaut, les membres des groupes qui suivent sont autorisés à exécuter localement l’applet de commande **Get-CsNetworkSite** : RTCUniversalUserAdmins, RTCUniversalServerAdmins. Pour retourner une liste de tous les rôles RBAC (Contrôle d’accès basé sur un rôle) auxquels cette applet de commande a été affectée (y compris les rôles RBAC personnalisés créés par vos soins), exécutez la commande suivante à l’invite Windows PowerShell :

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsNetworkSite"}

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
<td><p>Chaîne à caractère générique permettant de récupérer plusieurs sites en fonction de l’identité Site correspondant à la valeur Filter.</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>Facultatif</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsGlobalRelativeIdentity</p></td>
<td><p>Identificateur unique du site de réseau que vous souhaitez récupérer. Les sites n’étant créés qu’au niveau de l’étendue globale, il n’est pas nécessaire de spécifier une étendue. Vous ne devez spécifier que l’ID de site. (Notez qu’il s’agit de la même valeur que NetworkSiteID pour le site de réseau.)</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>Facultatif</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Extrait les données de site de réseau à partir du réplica local du magasin central de gestion, et non du magasin central de gestion proprement dit.</p></td>
</tr>
</tbody>
</table>


## Types d’entrées

Aucun.

## Types de retours

Récupère un objet de type Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.DisplayNetworkSiteType.

## Voir aussi

#### Autres ressources

[New-CsNetworkSite](new-csnetworksite.md)  
[Remove-CsNetworkSite](remove-csnetworksite.md)  
[Set-CsNetworkSite](set-csnetworksite.md)

