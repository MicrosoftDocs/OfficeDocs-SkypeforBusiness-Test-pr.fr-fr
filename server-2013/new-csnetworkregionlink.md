---
title: New-CsNetworkRegionLink
TOCTitle: New-CsNetworkRegionLink
ms:assetid: 61a6a7be-8078-4d59-a78a-2f241f6bf800
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Gg398437(v=OCS.15)
ms:contentKeyID: 49297394
ms.date: 05/20/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsNetworkRegionLink

 

_**Dernière rubrique modifiée :** 2015-03-09_

Crée un lien entre deux régions configurées pour le service Contrôle d’admission des appels. Cette applet de commande est une nouveauté de Lync Server 2010.

## Syntaxe

    New-CsNetworkRegionLink -NetworkRegionLinkID <String> <COMMON PARAMETERS>

    New-CsNetworkRegionLink -Identity <XdsGlobalRelativeIdentity> <COMMON PARAMETERS>

    COMMON PARAMETERS: -NetworkRegionID1 <String> -NetworkRegionID2 <String> [-BWPolicyProfileID <String>] [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-InMemory <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## Exemples

## EXEMPLE 1

Cet exemple crée un nouveau lien de région de réseau appelé NA\_EMEA pour relier les régions NorthAmerica et EMEA. Le nom du lien de région est spécifié comme valeur du paramètre d’identité. (Cette valeur sera automatiquement assignée à NetworkRegionLinkID). Pour créer le lien, il faut obligatoirement connaître les deux régions de réseau à relier, dans ce cas, les régions appelées NorthAmerica et EMEA. Dans cet exemple, nous avons également assigné une valeur au paramètre BWPolicyProfile. Cela permettra d’assigner les limites de bande passante de ce profil de stratégie (LowBWLimits) aux connexions entre ces régions. Si aucune identité BWPolicyProfileID n’est fournie, il n’y a aucune limite de bande passante pour les connexions entre ces deux régions. (Certaines limitations peuvent tout de même exister entre ces sites : Pour plus d’informations, consultez la rubrique d’aide relative à l’applet de commande **New-CsNetworkSite**.)

    New-CsNetworkRegionLink -Identity NA_EMEA -NetworkRegionID1 NorthAmerica -NetworkRegionID2 EMEA -BWPolicyProfileID LowBWLimits

## Description détaillée

Régions dans un réseau relié par une connexion physique WAN. Cette applet de commande définit un lien entre deux régions et les limites de bande passante pour les connexions audio et vidéo entre ces régions.

Personnes autorisées à exécuter cette applet de commande : Par défaut, les membres des groupes qui suivent sont autorisés à exécuter localement l’applet de commande **New-CsNetworkRegionLink** : RTCUniversalServerAdmins. Pour retourner une liste de tous les rôles RBAC (Contrôle d’accès basé sur un rôle) auxquels cette applet de commande a été affectée (y compris les rôles RBAC personnalisés créés par vos soins), exécutez la commande suivante à l’invite Windows PowerShell :

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsNetworkRegionLink"}

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
<td><p>Un identificateur unique pour le lien de région de réseau nouvellement créé. Les liens de région de réseau ne sont créés que pour l’étendue globale, si bien que cet identificateur n’a pas besoin de spécifier une étendue. Il contient plutôt une chaîne avec un nom unique qui identifie ce lien.</p></td>
</tr>
<tr class="even">
<td><p><em>NetworkRegionID1</em></p></td>
<td><p>Obligatoire</p></td>
<td><p>System.String</p></td>
<td><p>Identité de la région (NetworkRegionID) reliée à une région identifiée par un paramètre NetworkRegionID2.</p></td>
</tr>
<tr class="odd">
<td><p><em>NetworkRegionID2</em></p></td>
<td><p>Obligatoire</p></td>
<td><p>System.String</p></td>
<td><p>L’identité de la région (NetworkRegionID) reliée à la région identifiée par le paramètre NetworkRegionID1.</p></td>
</tr>
<tr class="even">
<td><p><em>NetworkRegionLinkID</em></p></td>
<td><p>Obligatoire</p></td>
<td><p>System.String</p></td>
<td><p>Cette valeur est la même que l’identité. Vous ne pouvez pas spécifier à la fois une identité et un identificateur NetworkRegionLinkID. Une valeur saisie pour l’un des deux sera automatiquement utilisée pour les deux.</p></td>
</tr>
<tr class="odd">
<td><p><em>BWPolicyProfileID</em></p></td>
<td><p>Facultatif</p></td>
<td><p>System.String</p></td>
<td><p>L’identité du profil de stratégie de bande passante qui définit les limites pour ce lien. Vous pouvez récupérer une liste des profils disponibles en appelant l’applet de commande <strong>Get-CsNetworkBandwidthPolicyProfile</strong>.</p></td>
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
<td><p><em>InMemory</em></p></td>
<td><p>Facultatif</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Crée une référence d’objet sans valider l’objet comme une modification définitive. Si vous affectez à une variable la sortie de cette cmdlet appelée avec ce paramètre, vous pouvez apporter des modifications aux propriétés de la référence d’objet, puis les valider en appelant la cmdlet Set- correspondante.</p></td>
</tr>
<tr class="odd">
<td><p><em>WhatIf</em></p></td>
<td><p>Facultatif</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Décrit ce qui se passe si vous exécutez la commande sans l’exécuter réellement.</p></td>
</tr>
</tbody>
</table>


## Types d’entrées

Aucun.

## Types de retours

Cette applet de commande crée un objet de type Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.NetworkRegionLinkType.

## Voir aussi

#### Autres ressources

[Remove-CsNetworkRegionLink](remove-csnetworkregionlink.md)  
[Set-CsNetworkRegionLink](set-csnetworkregionlink.md)  
[Get-CsNetworkRegionLink](get-csnetworkregionlink.md)  
[Get-CsNetworkBandwidthPolicyProfile](get-csnetworkbandwidthpolicyprofile.md)  
[New-CsNetworkSite](new-csnetworksite.md)

