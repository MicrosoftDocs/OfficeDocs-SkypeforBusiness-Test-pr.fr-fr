---
title: Get-CsNetworkConfiguration
TOCTitle: Get-CsNetworkConfiguration
ms:assetid: 08bc8eca-b244-4d5e-b089-1cc95605ba14
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Gg398140(v=OCS.15)
ms:contentKeyID: 49296177
ms.date: 05/20/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsNetworkConfiguration

 

_**Dernière rubrique modifiée :** 2015-03-09_

Extrait les paramètres globaux des fonctionnalités de contrôle d’admission des appels (CAC), Enhanced 9-1-1 (E9-1-1) et de déviation du trafic multimédia. Cette applet de commande est une nouveauté de Lync Server 2010.

## Syntaxe

    Get-CsNetworkConfiguration [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Get-CsNetworkConfiguration [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-LocalStore <SwitchParameter>]

## Exemples

## EXEMPLE 1

Cet exemple illustre l’extraction des paramètres de configuration réseau. Ces paramètres sont définis uniquement dans l’étendue globale. Un seul élément sera donc renvoyé.

    Get-CsNetworkConfiguration

## EXEMPLE 2

Il n’existe qu’un seul ensemble de paramètres de déviation du trafic multimédia qui s’applique globalement. Ces paramètres sont stockés dans la configuration réseau générale. Cette commande extrait d’abord cette configuration en appelant l’applet de commande **Get-CsNetworkConfiguration**, puis extrait la propriété MediaBypassSettings de la configuration.

    (Get-CsNetworkConfiguration).MediaBypassSettings

## Description détaillée

L’objet de configuration réseau inclut tous les paramètres globaux relatifs à la déviation du trafic multimédia et à une configuration CAC complète dans un déploiement Lync Server. Elle indique notamment si cette configuration a été ou non activée. Vous pouvez utiliser cette applet de commande pour extraire ces configurations et ces paramètres. Cependant, à l’exception de EnableBandwidthPolicyCheck et de MediaBypassSettings, il est recommandé d’utiliser des applets de commande spécifiques au type d’objet pour extraire les paramètres de configuration CAC. Par exemple, pour extraire les régions réseau, il sera généralement plus facile d’appeler l’applet de commande **Get-CsNetworkRegion** plutôt que l’applet de commande **Get-CsNetworkConfiguration** et d’extraire ensuite la propriété NetworkRegions de cette configuration.

Personnes autorisées à exécuter cette applet de commande : Par défaut, les membres des groupes qui suivent sont autorisés à exécuter localement l’applet de commande **Get-CsNetworkConfiguration** : RTCUniversalUserAdmins, RTCUniversalServerAdmins. Pour retourner une liste de tous les rôles RBAC (Contrôle d’accès basé sur un rôle) auxquels cette applet de commande a été affectée (y compris les rôles RBAC personnalisés créés par vos soins), exécutez la commande suivante à l’invite Windows PowerShell :

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsNetworkConfiguration"}

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
<td><p>Puisqu’il n’existera toujours qu’une seule configuration de réseau, vous n’avez pas besoin de ce paramètre pour cette applet de commande.</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>Facultatif</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>La valeur est toujours Global</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>Facultatif</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Extrait la configuration réseau du réplica local du magasin central de gestion, et non du magasin central de gestion lui-même.</p></td>
</tr>
</tbody>
</table>


## Types d’entrées

Aucun.

## Types de retours

L’applet de commande **Get-CsNetworkConfiguration** renvoie une instance de l’objet Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.NetworkConfigurationSettings.

## Voir aussi

#### Autres ressources

[Remove-CsNetworkConfiguration](remove-csnetworkconfiguration.md)  
[Set-CsNetworkConfiguration](set-csnetworkconfiguration.md)  
[Get-CsNetworkSite](get-csnetworksite.md)  
[Get-CsNetworkRegionLink](get-csnetworkregionlink.md)  
[Get-CsNetworkInterSitePolicy](get-csnetworkintersitepolicy.md)  
[Get-CsNetworkInterRegionRoute](get-csnetworkinterregionroute.md)  
[Get-CsNetworkRegion](get-csnetworkregion.md)  
[Get-CsNetworkSubnet](get-csnetworksubnet.md)  
[Get-CsNetworkBandwidthPolicyProfile](get-csnetworkbandwidthpolicyprofile.md)

