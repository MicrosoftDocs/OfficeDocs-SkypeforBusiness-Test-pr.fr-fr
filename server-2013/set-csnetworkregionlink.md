---
title: Set-CsNetworkRegionLink
TOCTitle: Set-CsNetworkRegionLink
ms:assetid: b3d5d203-2aa7-4a54-93d4-30bcda391d68
ms:mtpsurl: https://technet.microsoft.com/fr-fr/library/Gg412867(v=OCS.15)
ms:contentKeyID: 49298594
ms.date: 05/20/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsNetworkRegionLink

 

_**Dernière rubrique modifiée :** 2015-03-09_

Modifie un lien entre deux régions de réseau configurées pour le contrôle d’admission des appels. Cette applet de commande est une nouveauté de Lync Server 2010.

## Syntaxe

    Set-CsNetworkRegionLink [-Identity <XdsGlobalRelativeIdentity>] <COMMON PARAMETERS>

    Set-CsNetworkRegionLink [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-BWPolicyProfileID <String>] [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-NetworkRegionID1 <String>] [-NetworkRegionID2 <String>] [-WhatIf [<SwitchParameter>]]

## Exemples

## EXEMPLE 1

Cet exemple modifie le profil de stratégie de bande passante du lien de région réseau appelé NA\_EMEA en profil HighBWLimits. Le nom du lien de région réseau à modifier est précisé en tant que valeur du paramètre Identity. Nous avons ensuite affecté la valeur HighBWLimits au paramètre BWPolicyProfile. Ceci permettra d’affecter les restrictions de bande passante définies dans ce profil de stratégie de bande passante (HighBWLimits) aux connexions entre ces régions.

    Set-CsNetworkRegionLink -Identity NA_EMEA -BWPolicyProfileID HighBWLimits

## Description détaillée

Les régions au sein d’un réseau sont liées par le biais d’une connectivité WAN physique. Cette applet de commande modifie un lien entre deux régions afin de vous permettre de changer les régions liées, ainsi que les restrictions de bande passante pour les connexions audio et vidéo établies entre ces régions.

Personnes autorisées à exécuter cette applet de commande : Par défaut, les membres des groupes qui suivent sont autorisés à exécuter localement l’applet de commande **Set-CsNetworkRegionLink** : RTCUniversalServerAdmins. Pour retourner une liste de tous les rôles RBAC (Contrôle d’accès basé sur un rôle) auxquels cette applet de commande a été affectée (y compris les rôles RBAC personnalisés créés par vos soins), exécutez la commande suivante à l’invite Windows PowerShell :

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsNetworkRegionLink"}

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
<td><p><em>BWPolicyProfileID</em></p></td>
<td><p>Facultatif</p></td>
<td><p>Chaîne</p></td>
<td><p>Identité du profil de stratégie de bande passante qui définit les restrictions de ce lien. Vous pouvez récupérer une liste des profils disponibles en appelant l’applet de commande <strong>Get-CsNetworkBandwidthPolicyProfile</strong>.</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>Facultatif</p></td>
<td><p>SwitchParameter</p></td>
<td><p>Vous demande confirmation avant d’exécuter la commande.</p></td>
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
<td><p>XdsGlobalRelativeIdentity</p></td>
<td><p>Identificateur unique du lien de région réseau que vous souhaitez modifier. Les liens de région réseau sont créés uniquement au niveau de l’étendue globale. Par conséquent, cet identificateur ne doit pas nécessairement spécifier une étendue. Au lieu de cela, il contient une chaîne qui est un nom unique qui identifie ce lien.</p></td>
</tr>
<tr class="odd">
<td><p><em>Instance</em></p></td>
<td><p>Facultatif</p></td>
<td><p>NetworkRegionLinkType</p></td>
<td><p>Référence d’objet à un lien de région réseau. Cet objet doit être de type Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.NetworkRegionLinkType et peut être récupéré en appelant l’applet de commande <strong>Get-CsNetworkRegionLink</strong>.</p></td>
</tr>
<tr class="even">
<td><p><em>NetworkRegionID1</em></p></td>
<td><p>Facultatif</p></td>
<td><p>Chaîne</p></td>
<td><p>Identité de la région (NetworkRegionID) liée à la région identifiée par la propriété NetworkRegionID2.</p></td>
</tr>
<tr class="odd">
<td><p><em>NetworkRegionID2</em></p></td>
<td><p>Facultatif</p></td>
<td><p>Chaîne</p></td>
<td><p>Identité de la région (NetworkRegionID) liée à la région identifiée par la propriété NetworkRegionID1.</p></td>
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

Objet Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.NetworkRegionLinkType. Accepte l’entrée redirigée pour les objets du lien de région de réseau.

## Types de retours

Cette applet de commande ne retourne aucune valeur. Elle modifie un objet de type Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.NetworkRegionLinkType.

## Voir aussi

#### Autres ressources

[New-CsNetworkRegionLink](new-csnetworkregionlink.md)  
[Remove-CsNetworkRegionLink](remove-csnetworkregionlink.md)  
[Get-CsNetworkRegionLink](get-csnetworkregionlink.md)  
[Get-CsNetworkBandwidthPolicyProfile](get-csnetworkbandwidthpolicyprofile.md)

